---
layout: reports
title: "October 2018"
---

## REST framework

October saw the release of Django REST framework 3.9.

We'll follow up this month with a 3.9.1 to address any initial issues in the new schema generation.

## ASGI

I've been spending a significant amount of time helping mature the ASGI ecosystem.

This has been through working on [Starlette](https://www.starlette.io/) which is laying down patterns for building ASGI frameworks in a way that encourages re-usable components, through [Uvicorn](https://www.uvicorn.org/), as well as through a [number of blog posts](https://www.encode.io/articles/) introducing the subject.

* Added support for ASGI lifetime messages to Uvicorn, added support for startup and shutdown events to Starlette.
* Added middleware support to Starlette, and implemented several reusable ASGI middleware classes including CORS, Trusted hosts, HTTPS redirects, GZip, and HTTP Sessions.
* Implemented an ASGI middleware base class that exposes a standard request/response interface to the end developer.
* Implemented an [ASGI middleware for Sentry integration](https://github.com/encode/sentry-asgi).
* Added async form parsing support to Starlette.
* Added GraphQL support to Starlette.
* Improved URL routing in Starlette, with `app.url_path_for`, `request.url_for`, and support for nested URL names similar to Django's namespaced URLs.
* Added API schema support to Starlette.
* Added debug-level logging to Uvicorn.
* I have discussing helping the Sanic framework to adopt ASGI, which you can follow [on their discussion group](https://community.sanicframework.org/t/considering-asgi-support/70).

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 6th November, 2018.
