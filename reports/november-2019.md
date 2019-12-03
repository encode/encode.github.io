---
layout: reports
title: "November 2019"
---

## Django REST framework

We have a 3.11 release pending, that will offer compatibility with Django 3.0.

The release includes a number of improvements to our OpenAPI rendering,
and an important improvement in how we handle validators or defaults that need
access to the serializer context.

I'm planning on writing up the release notes and making the release this week.

Follow [ticket 6981](https://github.com/encode/django-rest-framework/issues/6981)
for any updates.

## HTTPX

There's been some significant work towards a 1.0 release of HTTPX. In order to
get there we've had to temporarily remove the synchronous variant of the client,
and only support the async client.

Our previous approach to providing a sync client was to run an event loop in the
background, and bridge between the sync and async portions of the code. There
were a couple of serious problems with this approach:

* In some contexts running a new async event loop in the existing thread is not
possible. In particular our sync client was failing when used with Jyupter.
* Having sync and async variants, both subclassing a common base class, with
bridging code on the sync variants was unduly complicating the implementation,
and impacting the project as a result.

Happily, I think we've got a much cleaner tack onto this now, which learns from
work done by the maintainers of `urllib3`.

In the new implementation, our sync code will be automatically generated from
the async codebase. We'll also have a very small sync backend implementation,
which will use standard thread-concurrency socket operations.

The end result will be that rather than having async code running behind a
sync facade, we'll have a properly sync-all-the-way-through codebase for the
synchronous client.

We'll still have to figure out how we want to name and namespace the two
different variants, but I'm confident that technically we're actually pretty
close to being able to put out an API stable 1.0 release.

## Starlette

There's been a significant new release of Starlette, including declarative-style
routing, in preference to the previous decorator style.

This could be described as now more Django-like than Flask-like.

This work is also being informed by progress on the HostedAPI service, which
is a starlette-in-production service that I'm working on in order to help
thrash out any remaining pain points with building production-ready async web
services with Starlette, Uvicorn, Databases, and TypeSystem.

---

As ever thank you so much to all our sponsors, contributors, and users.

&mdash; Tom Christie, 3rd December, 2019.
