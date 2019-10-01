---
layout: reports
title: "January 2019"
---

## REST Framework
Carlton Gibson has continued leading triage on the project, with time funded by our sponsorships.

We've issued a 3.9.1 release, which includes security fixes for potential XSS injections.

We're aiming for a 3.10 release sometime around April, alongside Django 2.2. This will likely be the point at which we drop Python 2 support.

## ASGI & Async
There's been *lots* of ongoing work on maturing Starlette and Uvicorn. Although there's plenty of work to do in bringing the async ecosystem up to feature parity with existing thread-syncronous frameworks like Flask and Django, I think we're now starting to make serious inroads.

There are now a number of higher-level frameworks that build on Starlette. In particular Fast API, Responder, and Bocadillo.

Real-world experience with developing a server and framework against ASGI means I've been able to give feedback to the specification. In particular there's now [an open proposal](https://github.com/django/asgiref/issues/78) that could simplify the spec a little, by replacing ASGI's existing "double callable" style with a single async callable.

I've also released [a new project](https://github.com/encode/databases) - "databases". The project provides a simple user-friendly API for async database support. It currently includes Postgres and MySQL integration, and allows you to make use SQLAlchemy Core to run queries, or integrate with Alembic for migrations.

The next features on the roadmap for the databases project will be support for SQLite, and for executing raw string SQL queries.

Further along the line is another possibility too: By providing cross-database support with a common async interface the "databases" package is laying the foundation for an async ORM to build on top it.
## The big picture
Much of my work at the moment is on the leading-edge, since REST framework is in a pretty mature state. Having funded time for Carlton's continuing triage on the project means we're able to keep it in a healthy state, while also focusing a lot of development time on Python's emerging async ecosystem.

The work on each of `uvicorn`, `starlette`, and `databases` is likely to eventually result in an alternative that starts to gradually work towards feature parity with Django, as well as hopefully feeding back into the work on future Django versions, in particular Andrew Godwin's proposal for bringing ASGI to Django.

The goal here is for the Python ecosystem to have web framework tooling that is as productive to work with as Django, with performance characteristics that are competitive against Node, and with great support for WebSockets, HTTP/2, and other features.

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 13th February, 2019.
