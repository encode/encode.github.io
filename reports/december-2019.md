---
layout: reports
title: "December 2019"
---

## Django REST framework

REST framework 3.11 has been released, with compatibility with Django 3.0,
a number of Open API improvement, and a better API for validators and defaults
that require context information.

Full release notes [are available here](https://www.django-rest-framework.org/community/3.11-announcement/).

## HTTPX

We've been working flat-out on bringing sync support back to HTTPX, and are pretty close to being able to do that now.

Improvements to HTTPX in December include:

* Automatic detection of either Asyncio or Trio.
* New streaming API.
* Redesigned HTTP/2 implementation.
* Better Timeout configuration.
* Unified `Response` and `Request` classes that can be used in either async or sync contexts.
* Various bug fixes.

For more information see [the project change log](https://github.com/encode/httpx/blob/master/CHANGELOG.md).

## Uvicorn

There's been various bits of work on ensuring that Uvicorn runs properly on Windows.

Platform differences in passing sockets between threads had meant that multi-worker and reload support was not reliably working. We've now issued a 0.11 release, which should resolve these issues.

---

As ever thank you so much to all our sponsors, contributors, and users.

&mdash; Tom Christie, 3rd January, 2020.
