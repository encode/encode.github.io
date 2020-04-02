---
layout: reports
title: "March 2020"
---

## REST framework

We'd been planning a new release, with the latest Open API improvements. Unsurprisingly this has been pushed back due to all the juggling commitments, looking after family members & switching over to home schooling.

I'll be aiming to roll a 3.12 release for the end of this month.

## HTTPX

HTTPX has continued to mature, with a 0.12 release. We're about ready to roll a pre-release of our first version to switch to using `httpcore`. This will give us...

* Same codebase for both sync + async variants. (HTTPX currently uses `urllib3` for sync, and our `h11`/`h2` based implementation for async.)
* A really tightly defined dispatch interface.
* Enable HTTP/2 support for the sync case.

We'll then plan on going over the existing API in detail, and issuing a 1.0 release shortly.

## Async Web Stack

I've been putting some tentative work into other areas where I think Python's async web stack needs some levelling up.

[The `savannah` repo](https://github.com/encode/savannah) contains some work that could be the start of a migrations tool for the `orm` package.

[The `staradmin` repo](https://github.com/encode/staradmin) provides a simple admin-like interface for Starlette and other ASGI frameworks.

Related to both of those has also been some work on possible future versions of `typesystem` and `orm`.

The plan is to use staradmin as an MVP of the Django-like functionality that we'd want to see in a mature async webstack, complete with ORM, Migrations, and an Admin interface.

## Funding

Like almost every business right now, our funding situation is being impacted. I'll plan on reviewing how it's looking at the end of this month.

---

Wishing you all strength, warmth & love,

&mdash; Tom
