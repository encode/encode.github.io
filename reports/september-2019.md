---
layout: reports
title: "September 2019"
---

## Growing Encode

There's a fairly large number of projects now under the Encode umbrella:

* Django REST framework - Django's leading API framework.
* HTTPX - An HTTP/1.1 and HTTP/2 client.
* Uvicorn, Starlette - Web Server and Web Framework.
* Databases, ORM - Low level and High level async database support.
* Typesystem - Type validation and form rendering.

We also have the Encode website, plus all the standard admin of running a
small business.

All of this means that I'm not able to be fully involved in triage across all
our projects at the same time, and have started putting more time into figuring
out how to help Encode continue to work productively.

As a result of this:

* I'm starting to invest more time into building and managing teams for the various projects.
* I'm planning to blog more, and treat Encode not only as the suite of projects we support,
but also as a guiding light in how to approach collaborative development.
* I've attended a full-day workshop "PlainScaling" on growing sustainable businesses. This was led by Jon Markwell, founder of [The Skiff](https://www.theskiff.org/) and several successful product companies.

## The Encode website

Our website was previously being built with a prototype of `mkdocs2`.
I've now switched this out to Jekyll, as it is a hugely mature and well-supported alternative.

Being able to take advantage of GitHub page's built-in support for building from Jekyll is also
a benefit, as there's no longer any separate build step, and I'm able to simply edit files directly
on the GitHub site in simple cases.

The website is also a public repo now, so we'll be able to accept Pull Request improvements to the site.

It's still feasible that I'll put more time into a MkDocs re-release at some point,
but on balance I think it's better for us to lean on well established tools where possible
rather than always having to use Encode-built tooling for everything we do.

## HTTPX

The HTTPX project is continuing to press ahead, in large part due to a fantastic maintainer team.

We've seen the addition of HTTP proxy support, plus support for the Trio concurrency library.

## Databases & ORM

The `databases` and `orm` packages now have a new maintainer team. We're close to having
support for the `aiopg` database driver, in addition to the existing `asyncpg` driver.

## Starlette & Uvicorn

The `starlette` and `uvicorn` packages also have a new maintainer team. I'll be putting
some time into trying to establish some good working patterns, so that my time doesn't have to
be the bottleneck for resolving most issues.

---

As ever thank you so much to all our sponsors, contributors, and users.

&mdash; Tom Christie, 1st October, 2019.
