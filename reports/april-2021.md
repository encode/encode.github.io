---
layout: reports
title: "April 2021"
---

## HTTPX

The headline work this month has been the HTTPX 0.18 release.

Our CHANGELOG is the best place to get fully up to speed [on all the work that's
gone into our latest release](https://github.com/encode/httpx/blob/master/CHANGELOG.md#0180-27th-april-2021).

Some of the more important aspects of the release include:

* The low-level transport API has now been formalized.
* The `QueryParams` model now presents an immutable interface.
* `Request` and `Response` instances can now be serialized with `pickle`.

---

### Transport API

It's worth digging into our Transport API, since it's a pretty powerful feature
of HTTPX, and we've spent a long time making sure we've got it *just so*.

The "transport" in HTTPX is the component that actually deals with sending
the request, and returning the response. An important aspect of the design of our
Transport API is that it only deals with low-level primitive datatypes, and does
not deal with `Request` or `Response` instances directly. This ensures a clean
separation of design-space, making the each of the user-facing `Client` component
and the low-level networking `Transport` easier to reason about in isolation.

We currently include four built-in transports:

* `httpx.HTTPTransport()` - Our default network transport. A light wrapper around `httpcore`.
* `httpx.ASGITransport()` - A transport that issues requests to an ASGI app, such as FastAPI or Starlette.
* `httpx.WSGITransport()` - A transport that issues requests to a WSGI app, such as Flask or Django.
* `httpx.MockTransport()` - A transport that delegates to a handler function, passing it a `Request` instance, and expecting a `Response` instance to be returned. Useful for simple mocking out of HTTP calls.

It's possible that at a later date we could also include an optional
`httpx.URLLib3Transport()`, allowing users to switch the networking component to
the excellent and long-established `urllib3` package.

Providing a transport API allows for all sorts of interesting use-cases.
Transports can be composed in order to provide functionality such as:

* Adding a client-side HTTP caching layer.
* Request/response recording and playback.
* Support for alternate protocols, such as transports for `file://` or `ftp://` schemes.
* Support for advanced retry or rate-limiting policies.

To create a transport class you need to subclass `httpx.BaseTransport`, and
implement the `handle_request` method.

This API is best illustrated with a short example:

```python
import json
import httpx


class HelloWorldTransport(httpx.BaseTransport):
    """
    A mock transport that always returns a JSON "Hello, world!" response.
    """

    def handle_request(self, method, url, headers, stream, extensions):
        message = {"text": "Hello, world!"}
        content = json.dumps(message).encode("utf-8")
        stream = httpx.ByteStream(content)
        headers = [(b"content-type", b"application/json")]
        extensions = {}
        return 200, headers, stream, extensions


client = httpx.Client(transport=HelloWorldTransport())
response = client.get("https://example.org/")
print(response.json())  # Prints: {"text": "Hello, world!"}
```

---

### Requests with the Transport API

The arguments to the `handle_request` method are as follows:

#### method

The request method as a byte string. For example: `b"GET"`.

#### url

The request URL. This is in a pre-parsed form of a four-tuple of `(scheme, host, optional port, target)`.
This format is important because:

* There are some types of requests that can be made against a transport that cannot
  be expressed with a URL string. Proxy `CONNECT` requests that include a complete
  URL for the target portion of the request, or `OPTIONS *` requests.
* We need to parse the URL string in the client code, and for performance reasons we'd like
  to not have to parse the URL again. There are also security reasons for ensuring that
  only a single implementation for URL parsing is used throughout.

The plain byte-wise representation can be accessed via the `URL.raw` property:

```python
>>> httpx.URL("https://www.example.com/some/path?query").raw
(b"https", b"www.example.com", None, b"/some/path?query")
```

#### headers

A list of two-tuples of bytes. For example: `[(b"Host", b"www.example.com"), (b"User-Agent", b"httpx")]`

#### stream

A subclass of `httpx.SyncByteStream` which must implement an `__iter__` bytes iterator method.
Subclasses may also optionally implement a `close()` method.

The `httpx.ByteStream()` class may be used for the simple case of passing a plain bytestring
as the request body.

#### extensions

A dictionary of optional extensions that do not otherwise fit within the Transport API.
More on this below.

---

### Responses with the Transport API.

The return value of the `handle_request` method is a four-tuple consisting of:

#### status_code

The response HTTP status code, as an integer. For example: `200`.

#### headers

A list of two-tuples of bytes. For example: `[(b"Content-Type", b"application/json"), (b"Content-Length", b"1337")]`

#### stream

A subclass of `httpx.SyncByteStream`. If calling into a transport directly, you can read either read
entire body using the `.read()` method on the stream, or else iterate over the stream ensuring to call
`.close()` on completion.

```python
transport = httpx.HTTPTransport()

# Reading the entire response body in a single call.
status_code, headers, stream, extensions = transport.handle_request(...)
body = stream.read()

# Streaming the response body.
status_code, headers, stream, extensions = transport.handle_request(...)
try:
    for chunk in stream:
        ...
finally:
    stream.close()
```

#### extensions

A dictionary of optional extensions that do not otherwise fit within the Transport API.
More on this below.

---

### Extensions

Given the maxim that "All abstractions are leaky", it's important that when an abstraction
*does* leak, it only does so in well-isolated areas. The `extensions` request argument, and
response value provide for features that are entirely optional or that would not otherwise
fit within our transport API.

Our current request extensions are:

* `"timeout"` - A dictionary of optional timeout values, used for setting per-request timeouts.
    May include values for 'connect', 'read', 'write', or 'pool'.

Our current response extensions are:

* `"reason_phrase"` - The reason-phrase of the HTTP response, as bytes. Eg `b'OK'`.
        HTTP/2 onwards does not include a reason phrase on the wire.
        When no key is included, a default based on the status code may
        be used. An empty-string reason phrase should not be substituted
        for a default, as it indicates the server left the portion blank
        eg. the leading response bytes were b"HTTP/1.1 200 <CRLF>".
* `"http_version"` - The HTTP version, as bytes. Eg. b"HTTP/1.1".
        When no http_version key is included, HTTP/1.1 may be assumed.

In the future, extensions will allow us to provide for more complex functionality,
such as returning a bi-directional stream API in response to `Upgrade` or `CONNECT`
requests.

---

### Async Transports

For async cases a transport class should subclass `httpx.AsyncBaseTransport` and implement the `handle_async_request` method.

A transport class may provide both sync and async styles.

---

The 0.18 release is expected to be our last major release before a fully API-stable 1.0.

Thanks as ever to all our sponsors, contributors, and users,

&mdash; Tom Christie, 5th May, 2021.
