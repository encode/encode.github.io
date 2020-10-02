---
layout: reports
title: "September 2020"
---

# Django REST framework

## 3.12 Release

Django REST framework 3.12 has finally been released.

There's a host of smaller issues resolved in this, plus a few headline features
around schema generation.

See the [release announcement](https://www.django-rest-framework.org/community/3.12-announcement/)
for details.

## 3.11.2 Security release

We've also issued a security release, in version 3.11.2.

This release resolves a potential XSS issue in the browsable API.

# HTTPX

We're continuing to work towards a 1.0 release.

Our latest release of 0.15 brings with it a number of new features,
including the following...

## Using Request and Response instances directly

We've improved support for being able to use `Request` and `Response` instances
as stand-alone models. For example...

```python
# Create a response instance, with JSON content.
response = Response(200, json={"hello, world!"})
```

This work will allow you use request and response instances in more contexts.

For example, it becomes easier to unit test authentication classes. It's also
allow us to work towards providing a mock transport handler for stubbing

## Support for event hooks

HTTPX allows you to register "event hooks" with the client, that are called
every time a particular type of event takes place.

There are currently two event hooks:

* `request` - Called once a request is about to be sent. Passed the `request` instance.
* `response` - Called once the response has been returned. Passed the `response` instance.

These allow you to install client-wide functionality such as logging and monitoring.

```python
def log_request(request):
    print(f"Request event hook: {request.method} {request.url} - Waiting for response")

def log_response(response):
    request = response.request
    print(f"Response event hook: {request.method} {request.url} - Status {response.status_code}")

client = httpx.Client(event_hooks={'request': [log_request], 'response': [log_response]})
```

You can also use these hooks to install response processing code, such as this
example, which creates a client instance that always raises `httpx.HTTPStatusError`
on 4xx and 5xx responses.

```python
def raise_on_4xx_5xx(response):
    response.raise_for_status()

client = httpx.Client(event_hooks={'response': [raise_on_4xx_5xx]})
```

Event hooks must always be set as a *list of callables*, and you may register
multiple event hooks for each type of event.

As well as being able to set event hooks on instantiating the client, there
is also an `.event_hooks` property, that allows you to inspect and modify
the installed hooks.

```python
client = httpx.Client()
client.event_hooks['request'] = [log_request]
client.event_hooks['response'] = [log_response, raise_on_4xx_5xx]
```

## Support for authentication flows which require I/O

Our authentication API already supports authentication classes which make one
or multiple requests, and which work equally with both `Client` and `AsyncClient`.

However if you need to perform I/O within an authentication class, things become
more complex, as thread-blocking I/O should not be performed within an async
context, and async I/O cannot be performed within a sync context.

We've [now added support for authentication classes which require I/O](https://www.python-httpx.org/advanced/#customizing-authentication),
allowing developers to support *either* the sync I/O case, *or* the
async I/O case, *or* both cases.

## Support for Curio

The `AsyncClient` now supports [the curio async framework](https://github.com/dabeaz/curio).

When working with async, the `httpx` client will autodetect if you're in an
`asyncio`, `trio`, or `curio` context, and everything will *just work*...

```python
import curio
import httpx

async def main():
    async with httpx.AsyncClient() as client:
        r = await client.get("https://www.httpbin.org/json")
        print(r.status_code)
        print(r.json())

curio.run(main)
```

## Monitoring download progress

When performing a large download you'll sometimes want to monitor the ongoing
progress, by periodically comparing how many bytes have been downloaded against
the `Content-Length` header included in the response.

This is actually more awkward to do than might be expected at first, because
HTTP supports compression on responses, and clients such as `httpx`, `requests`,
and `urllib3` will transparently handle the decompression for you when iterating
over the response bytes.

We now provide [access to the underlying number of bytes that have been read from
the response body](https://www.python-httpx.org/advanced/#monitoring-download-progress),
allowing for accurate download progress monitoring.

## HTTPX command line client

We've released [a beta version of an `httpx` command line client](https://github.com/encode/httpx-cli)...

```shell
$ pip install httpx-cli
$ httpx https://www.httpbin.org/json
HTTP/1.1 200 OK
date: Fri, 02 Oct 2020 15:08:10 GMT
content-type: application/json
content-length: 429
connection: keep-alive
server: gunicorn/19.9.0
access-control-allow-origin: *
access-control-allow-credentials: true

{
    "slideshow": {
        "author": "Yours Truly",
        "date": "date of publication",
        "slides": [
            {
                "title": "Wake up to WonderWidgets!",
                "type": "all"
            },
            {
                "items": [
                    "Why <em>WonderWidgets</em> are great",
                    "Who <em>buys</em> WonderWidgets"
                ],
                "title": "Overview",
                "type": "all"
            }
        ],
        "title": "Sample Slide Show"
    }
}
```

## HTTP header casing

Our underlying HTTP transport uses the fantastically engineered [`h11` library](https://github.com/python-hyper/h11)
for it's HTTP/1.1 support. Because the HTTP spec mandates that header names
must be treated as case-insensitive, the `h11` library has historically taken
a nice simple approach, and simply normalized header names by always lowercasing
them.

However, there are plenty of non-compliant bits of HTTP infrastructure in the
wild, so in *some* cases you really do want to be able to preserve the
header casing used.

We've now got a [pull request against `h11`](https://github.com/python-hyper/h11/pull/104) that:

* Continues to support the existing `h11` API without modification.
* While preserving HTTP header casing.
* With minimal performance implications.

---

Thanks as ever to all our sponsors, contributors, and users,

&mdash; Tom Christie, 2nd October, 2020.
