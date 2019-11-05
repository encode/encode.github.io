---
layout: reports
title: "October 2019"
---

## Django REST framework

I've been fairly focused on building out the async ecosystem this month,
so there's not been a huge amount of work from myself on REST framework.
I'm planning to redress this imbalance a bit more over the coming month.

We're due a new release shortly. Sometime mid-November is probably a
reasonable expectation here.

[Ticket 6981](https://github.com/encode/django-rest-framework/issues/6981) is the place to follow any developments here.

## MkAutoDoc

The MkDocs project was originally built for the docs for Django REST framework,
and is now used for all our projects at Encode. It has become fairly successful,
and I'm generally really happy with how it's come along. However, one weak point
is that MkDocs *only* supports prose documentation, and does not have any
equivalent to Sphinx's autodoc.

[The `mkautodoc` package](https://github.com/tomchristie/mkautodoc) is an
extension that helps to fill that gap, adding support for embedding docstring
API descriptions inside Markdown documentation.

We've started using `mkautodoc` with the `httpx` project, and will likely be
rolling it out across the documentation for several of our other projects.

## HostedAPI

I've been working [building out a small Starlette service](https://github.com/encode/hostedapi)
in production.

The aim of the work here initially is to help thrash out areas of the async
web stack (`uvicorn`, `starlette`, `databases`, `orm`, `httpx`, `typesystem`) that still
need work.

By building a proper live service, we can use that experience to help drive
areas that need work. The codebase is also a good reference point for users
wanting to build out their own Starlette services.

I'm keeping [a comprehensive progress log](https://github.com/encode/hostedapi/blob/master/PROGRESS.md) of work on the service.

## Uvicorn

Uvicorn has seen [several new releases](https://github.com/encode/uvicorn/blob/master/CHANGELOG.md),
with significant improvements to the logging behavior, as well as improved handling
of proxy headers. In particular we now have some really nice colorized logging,
and proxy header handling that now requires zero-config on services such as Heroku
that set the `ALLOW_FORWARDED_IPS` environment variable.

## Starlette

I'm working on [a new Starlette release](https://github.com/encode/starlette/pull/704),
which moves to a clearer style for configuring routing and middleware.

---

As ever thank you so much to all our sponsors, contributors, and users.

&mdash; Tom Christie, 5th November, 2019.
