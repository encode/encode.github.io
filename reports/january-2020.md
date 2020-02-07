---
layout: reports
title: "January 2020"
---

## HTTPX

Most work during January has been focused on HTTPX.

The latest releases reintroduce sync support, meaning that `httpx` now provides:

* Requests feature parity, with a mostly requests-compatible API.
* Provides both standard sync APIs and async APIs.
* Async support for either `asyncio` or `trio`.
* HTTP/1.1 and HTTP/2 support.

We believe that we've got the API pretty much complete at this point, so our latest releases may be considered beta releases for a 1.0 due sometime over the coming weeks.

Having an HTTP client for Python with both sync and async support, plus HTTP/1.1 and HTTP/2 is a big step forward. It'll also tie in nicely with Andrew Godwin's ongoing work on bring async views to Django.

I'm now working on refining some of the lower level bits of the API. The intention is that we'll have a very clear interface split between the high-level client (httpx), and a low-level network interface component (httpcore).

* https://github.com/encode/httpx
* https://github.com/encode/httpcore

This will be beneficial for a couple of reasons:

* A really clear separation of concerns here will make each component easier to understand in isolation.
* It'll provide more potential for collaboration across the ecosystem. For example, other Python HTTP clients could potentially switch to using `httpcore` for the core networking layer, in order to gain HTTP/2 support, without having to change their high-level APIs.

Switching the httpx backend to httpcore will also ensure that we have more consistent networking behaviour across our sync and async variants. (Current releases are using urllib3 for the sync case, and https's built-in networking for the async case.)

I've also spent some time preparing an "Introducing HTTPX" talk, that I'll be presenting at PyCon US, and other conferences this year.

&mdash; Tom Christie, 7th February, 2020.
