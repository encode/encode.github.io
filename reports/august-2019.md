---
layout: reports
title: "August 2019"
---

August has been a quiet month, due to family holidays.

*Up to Scotland on the sleeper train, and over to the Isle of Skye. Then later, camping in Dorset. And yes, it was lovely, since you ask.*

## HTTPX

We've got a fanastic team working together on `httpx` right now, making some really impressive progress, including:

* Allowing configuration for which HTTP version clients should use.
* Working towards support for Trio.
* Working towards a making our HTTP/2 implementation more robust.
* Preliminary discussions around HTTP/3 support.
* A middleware interface for customising more complex use cases.

## Uvicorn

Resolving issues with latest packaging versions.

## Starlette

Triaging various minor improvements, and server push support.

## What's next

A new release of Django REST framework, including improvements to the OpenAPI schema generation.

Continuing to help drive HTTPX towards a solid 1.0 release.

Trying to keep Starlette, Uvicorn, and Database well triaged.

Hopefully finding some time to work a little more on a possible MkDocs re-release.

I also need to spend some time updating the Stripe integration that handles our sponsor payments. This is neccessary in order to deal with upcoming legislation that mandates stricter security around card payment handling. It's probably also a good time for us to switch from "REST framework sponsorships" to "Encode OSS sponsorships", which would likely mean incorperating our sponsor placements across all our project documentation sites, rather than just the REST framework site.

---

As ever thank you so much to all our sponsors, contributors, and users.

&mdash; Tom Christie, 3rd September, 2019.
