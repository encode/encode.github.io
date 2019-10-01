---
layout: articles
title: "Working with HTTP requests in ASGI"
permalink: "/articles/working-with-http-requests-in-asgi"
---

*This article is part of an ongoing series exploring the emerging [ASGI standard](https://asgi.readthedocs.io/en/latest/). To keep up to date with the full series, subscribe to the [RSS feed](https://www.encode.io/feeds/articles.rss).*

In [our last article](asgi-http) we took a look at the basic structure of the ASGI interface. Now we're going to go into some more detail on the message structure for HTTP requests, and take a look at how we can use some of the datastructures that the Starlette package provides in order to work with HTTP requests in ASGI.

The first thing that occurs in any ASGI application is that it is instantiated with a "scope" dictionary, that provides some initial information about the incoming request.

Here's an example of how the scope dictionary might look for a simple HTTP request.

```python
>>> scope = {
    "type": "http",
    "http_version": "1.1",
    "method": "GET",
    "scheme": "https",
    "path": "/",
    "query_string": b"search=red+blue&maximum_price=20",
    "headers": [
        (b"host", b"www.example.org"),
        (b"accept", b"application/json")
    ],
    "client": ("134.56.78.4", 1453),
    "server": ("www.example.org", 443)
}
```

The scope dictionary is pretty similar to WSGI's "environ" dictionary. In fact, the ASGI specification [documents how to map between the two](https://asgi.readthedocs.io/en/latest/specs/www.html#wsgi-compatibility).

```python
environ = {
    "REQUEST_METHOD": "GET",
    "SCRIPT_NAME": "",
    "PATH_INFO": "/",
    "QUERY_STRING": "search=red+blue&maximum_price=20",
    "SERVER_NAME": "www.example.org",
    "SERVER_PORT": 443,
    "REMOTE_HOST": "134.56.78.4",
    "REMOTE_PORT": 1453,
    "SERVER_PROTOCOL": "HTTP/1.1",
    "HTTP_HOST": "www.example.org",
    "HTTP_ACCEPT": "application/json",
}
```

## The scope type

A fundamental difference between ASGI and WSGI, is that ASGI is a more general purpose messaging interface, whereas WSGI is strictly request/response.

The one element that must always be present in any ASGI scope is the "type" key, which is used to indicate the protocol type.

```
scope = {
    "type": "http",  # Deal with an incoming HTTP request.
    ...
```

## Request URL

The full URL of an incoming request can be constructed based on the information
contained in `scheme`, `server`, `path`, and `query_string`.

Since we don't want to have to typically be working from the raw ASGI information,
it's useful for us to have some reusable tooling that we can use to abstract
away some of the details for us.

[The Starlette framework](https://www.starlette.io) is deliberately designed as a
zero-dependency library, so that it can be used as the basis for all kinds of
ASGI applications or other higher-level frameworks.

One of the things that is provides is a set of basic datastructures for working
with ASGI. For example:

```python
>>> from starlette.datastructures import URL
>>> url = URL(scope=scope)
>>> url
URL('https://www.example.org/?search=red+blue&maximum_price=20')
>>> str(url)
'https://www.example.org/?search=red+blue&maximum_price=20'
```

The URL instance allows you to inspect the various components on the URL,
in the same way as a the standard library's `urlparse`:

```python
>>> url.scheme
'https'
```

You can also modify components of the URL, and return a new instance:

```python
>>> url.replace(hostname='www.example.com')
URL('https://www.example.com/?search=red&maximum_price=20')
```

## Request headers

HTTP headers in ASGI are mandated to be a list of pairs of bytes, representing
the header name and value. Because HTTP headers are case-insensitive, ASGI
enforces that the byte-wise header representation must be strictly lower-cased.

HTTP headers can also contain multiple instances of the same header name,
for example as used with `Set-Cookie`.

Starlette provides an immutable, case-insensitive, multi-dict for working with
HTTP request headers from ASGI.

```python
>>> from starlette.datastructures import Headers
>>> headers = Headers(scope=scope)
>>> headers
Headers({'host': 'www.example.org', 'accept': 'application/json'})
```

Instantiating a `Headers` datastructure is a cheap operation, and provides a more
convenient interface for inspecting the request headers than iterating over the
byte-wise pairs directly.

```python
>>> headers['Accept']
'application/json'
```

For response headers, Starlette provides a `MutableHeaders` data structure,
that is equivelent, but also also setting or deleting header values.

## Request query params

One particular part of the URL that we need to deal with is the request query
parameters, eg "?search=red+blue&maximum_price=20".

To work with these, use the `QueryParams` class, which provides an
immutable multi-dict implementation onto the parameters.

```python
>>> from starlette.datastructures import QueryParams
>>> params = QueryParams(scope=scope)
>>> params
QueryParams(query_string='search=red+blue&maximum_price=20')
>>> params['search']
'red blue'
```

## Request body

Most of the information about the incoming request is stored in the
"scope", and presented at the point the ASGI app is instantiated. However
for the request body, that's not possible.

In order to access the request body, we have to get a stream of messages
from the "receive" channel. Here's how we can obtain a single message in
the stream:

```python
message = await receive()
```

And an example of how an HTTP request body message is structured:

```python
{
    'type': 'http.request.body',
    'body': b'{"example": "Some JSON data"}',
    'more_body': False
}
```

If you're working with ASGI directly, here's a pattern for how you'd consume
the entire stream of the HTTP request body:

```
body = b''
more_body = True
while more_body:
    message = await receive()
    body += message.get('body', b'')
    more_body = message.get('more_body', False)
```

Starlette provides a lightweight way of wrapping both the "scope" and "receive"
channel up in a request interface, that gives simpler ways to get access
to the request body:

```
request = Request(scope, receive=receive)
body = await request.body()
```

Alternatively, to get a JSON-parsed representation:

```
request = Request(scope, receive=receive)
body = await request.json()
```

For large requests it's possible that you may not want to consume the entire
request body into memory at once.

From Python 3.6 onwards the [asynchronous generator syntax](https://www.python.org/dev/peps/pep-0525/) is supported, which allows us to provide a nice simple API onto streaming the request body...

```python
request = Request(scope, receive=receive)

async for chunk in request.stream():
    ... # Do something with "chunk"
```

We can combine this with request parsing in order to handle form data gracefully.

When handling HTTP multipart requests, you'll typically want to ensure that the
request parsing is able to stream any file upload content into temporary files
on disk, without having to load all the data into memory first.

```python
request = Request(scope, receive=receive)

# Any upload files in the request body will be streamed into temporary files.
form = await request.form()
```

## Summary

We've seen how the ASGI "scope" message is structured for HTTP
requests, and how the message body is streamed over the "receive" channel.

We've also used some of the fundamental datastructures that [Starlette](https://www.starlette.io/) provides,
in order to work with ASGI at a slightly higher level.
