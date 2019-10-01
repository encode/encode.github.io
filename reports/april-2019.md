---
layout: reports
title: "April 2019"
---

## REST framework

The recent 3.9.3 will be our last to support Python 2.

We're no longer have any significant blockers towards 3.10, which we are planning
to release sometime during May.

## "Sketching out a Django Redesign"

My DjangoCon Europe KeyNote talk [is now available](https://www.youtube.com/watch?v=u8GSFEg5lnU).

You should watch this if you want an in-depth picture of why I think the async concurrency
model is going to be really important for Python's future, and the work around designing
a Web Stack to fit in with that.

## Requests III

The work on `requests-async` has gradually progressed into something that
may end up being the basis for Requests III.

Some of the more in-depth functionality for `requests-async` such as request/response
streaming, proxy support, etc. would have required a port of `urllib3` to async.
There's been some good work towards that elsewhere, but having looked into it,
my assessment is that a from-scratch implementation would be a achievable goal.

The proposal here, is for a new version of `requests` that includes:

* HTTP/2 and HTTP/1.1 support.
* `async`/`await` support for non-thread-blocking HTTP requests, plus a standard threaded client.

You can follow the work-to-date [in the `httpcore` repository](https://github.com/encode/httpcore).

I've been talking with Kenneth Reitz about the work here, and our hope is that
this work could be the foundation for a `requests3` release.

## Sanic

The release of the `requests-async` package has allowed the team behind the "Sanic"
web framework to start [progressing towards ASGI support](https://github.com/huge-success/sanic/pull/1562).

It's likely that I'll spend a small amount of time helping get things off
the ground here. Sanic is one of the most widely used `asyncio` web frameworks,
and having their community get behind a shared interface would be a really
big step forward towards us all working together more efficiently.

---

As ever thank you so much to all our sponsors, contributors, and users.

&mdash; Tom Christie, 2nd May, 2019.
