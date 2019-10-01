---
layout: reports
title: "March 2019"
---

## REST framework

We’re gradually working towards a 3.10 release. The headline feature here will be proper OpenAPI schema generation. We’re pulling out the intermediary `CoreAPI` document-model approach that we’ve been using until now, since OpenAPI has now long become a widely adopted standard for modelling Web APIs.

Alongside this there’s been work on the stand-alone `apistar` tooling, which provides API documentation generation, schema validation, and a schema-driven client library.
## Requests-Async
We’re continuing to push forward the `async` landscape, since it represents a huge potential for Python.

[The `requests-async` package](https://github.com/encode/requests-async) brings async/await support to the ever-popular `requests` library.

There are currently a couple of constraints on the package - most notably we don’t yet have streaming upload/download support. We’ll likely invest some time in the coming month into resolving any outstanding feature-differences between `requests` and `requests-async`.
## ORM

The [new `orm` package](https://github.com/encode/orm) is an async ORM with a Django-like API.

Because it is built on top of `databases` it has support for SQLite, Postgres, and MySQL. Query building is based on SQLAlchemy core, which means we’re also able to provide migration support, through Alembic.

The ORM package is still in the development stage, but has a fairly fully-featured API.
## Progressing Async

The stack of async functionality that we now have expands all the way through from an ASGI server implementation, all the way up to an ORM.

* `uvicorn` - Web Server
* `starlette` - Web framework
* `databases` - Low level cross-database queries
* `orm` - High level cross-database ORM
* `requests-async` - ASync HTTP requests

Each of the pieces in the stack are necessary pre-requisites to Python offering a mature, fully featured, high-performance async web stack.

I’ll be talking about the work here, the payoff it’ll enable, and where Django might fit in with this, at DjangoCon Europe, next week.

---

As ever thank you so much to all our sponsors, contributors, and users.

&mdash; Tom Christie, 3rd April, 2019.
