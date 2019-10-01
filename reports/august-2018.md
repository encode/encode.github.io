---
layout: reports
title: "August 2018"
---

## [REST framework](https://github.com/encode/django-rest-framework)

Triage has been ticking over on REST framework.

I've started to pick up the work on our next headline feature which will be OpenAPI schema generation. The plan is to gradually move away from our internal CoreSchema representation, and instead move everything to a more cross-compatible set of tooling around OpenAPI.

The `coreapi` client won't be disappearing in the near future, but we would like to gradually move towards powering all of our API docs and client libraries from OpenAPI schemas.

This ought to open up a wider range of tooling, make the tooling more widely accessible, and also provide a better environment for teams working with a range of frameworks.

## [Uvicorn](https://github.com/encode/uvicorn)

Uvicorn has continued to mature, and has a bunch of functionality, stability, and performance improvements. There are  a few different cases where you might consider using uvicorn as your webserver:

* If you're running Django Channels, you might consider switching from Daphne to Channels.
* If you're writing asyncio applications you should either look at using Starlette, or writing plain ASGI applications.
* If you're running a standard Django application, you can now use Uvicorn as your webserver, using the `--wsgi` switch.

## [Starlette](https://github.com/encode/starlette)

Starlette is an ASGI framework/toolkit.

I've been working on Starlette in order to try to provide the foundational building blocks that ASGI needs in order to seriously succeed as an interface specification.

The design of Starlette is modular, allowing you to use it as a complete framework, or treat individual components as ASGI building blocks. I'm aiming to promote an asyncio ecosystem that include lots of middleware and mountable applications that're compatible across a range of frameworks.

If you need to write a high-throughput asyncio service, then I'd highly recommend Starlette. Honestly, it's probably the nicest thing I've worked on.

One component in particular worth mentioning is Starlette's TestClient, which allows you to make HTTP or WebSocket requests to any ASGI application.

If your team is working with Django Channels, then I'd recommend trying Starlette's TestClient for testing your application, as an alternative to Channel's built-in `ApplicationCommunicator`/`WebsocketCommunicator`.

I'll be planning to submit a Pull Request adding it to the Channels testing documentation sometime in the near future.

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 6th Sept, 2018.
