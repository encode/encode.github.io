---
layout: reports
title: "March 2018"
---

## 3.8 release

We've just released 3.8, which is largely a maintence based release. The schema output management command mentioned in the last monthly report will instead likely be pending our next major release.

## API Star

API Star will be getting a complete overhaul with a new 0.4 version that I'm very happy with. (https://github.com/encode/apistar/pull/400)

This involves quite a bit of slimming down, with several existing features removed, but the foundation that it gives is *far* less complex as a result.

In particular:

* The API documentation is temporarily out.
* The command routing is temporarily out.
* The `apistar` command line client is temporarily out.

However we do now have:

* A *far* nicer, simpler, and more complete typesystem.
* A *far* nicer, simpler, interface for dependency injection.
* Event hooks for running code on request/response/exception.
* OpenAPI as the default API Schema output.
* ASGI as the asyncio server-client interface.
* A redesigned client library, that's now able to interact with any API that exposes an OpenAPI schema.
* A framework that I'm actually proud of this time, and happy to see moving forward.

Over the coming months I'm going to be consolidating all the API Schema generation and documentation building into the `apistar` package. Previously this has been spread across `coreapi` and `coreschema`, with documentation templates in both REST framework and API Star.

## ASGI

The ASGI specification was recently updated alongside the Django Channels 2.0 release. We hadn't previously been able to use ASGI for API Star, because it was designed primarily around the requirements of Django Channels, rather than as a general server-client interface. Instead we'd been using an "ASGI-like" interface, which I was refering to as the Uvicorn Messaging Interface.

The newest ASGI specification means we no longer need the "Uvicorn Messaging Interface". As a result I've been updating Uvicorn to become an ASGI-compliant webserver. (https://github.com/encode/uvicorn/pull/63)

The end result of this work will be that:

* You'll be able to use either `daphne` or `uvicorn` to run Django Channels.
* You'll be able to use either `daphne` or `uvicorn` to run API Star in asyncio mode.

We'll also be in a position to start building up an ecosystem of shared tooling.

For example, adding ASGI support to the WhiteNoise package (https://github.com/evansd/whitenoise/pull/181) in order to easily support static file serving for asyncio applications.

You should expect to see new versions of API Star and Uvicorn sometime over the next few days.

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 6th April, 2018.
