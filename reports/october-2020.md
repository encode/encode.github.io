---
layout: reports
title: "October 2020"
---

I'm going to take a somewhat different tack in this monthly report, to talk a bit about some of the bigger picture about where I see Encode headed towards.

Nominally our sponsorships are for Django REST framework, but in terms of the work I've been putting out it's been a very long time since that's been where the majority of my effort has tended to be focused.

Over the last couple of years, alongside maintenance work on REST framework, I've also been:

* Focusing on maturing the async web ecosystem in Python. In particular helping expand ASGI beyond Django with the `uvicorn` web-server, and the `starlette` web framework.
* Building a new HTTP client with `httpx`, bringing all the good API work that `requests` established, while also adding a range of new features - HTTP/2 support, both sync and async variants including asyncio, trio, and curio, type annotations throughout, a really clear client/networking API layer between `httpx` and the lower-level `httpcore` package.

As well as exploring a number of other avenues.

One of the incomparable benefits of the collaborative sponsorship approach has been that I'm able to put my time and attention wherever it appears to be most valuable.

Having a relationship of trust with our sponsors allows me to focus on trying to benefit the community as effectively as possible, without always having to tie my time down to a predetermined goal.

My own intuition here is that the return on investment that this approach has yielded far greater returns for the community, than a more tightly goal-oriented approach would have provided.

With that in mind, there seems to be a few aspects I could do with working towards:

* Moving the sponsorships more clearly to “Encode OSS” sponsorships, rather than specifically “REST framework”.
* Adding sponsorship placements to our other projects, such as HTTPX.
* Building more strands of work under the sponsorship umbrella, such as writing more consistently, or spending more time on financial transparency reports.

In the short term tho, I’ll simply be spending some time getting back on track with working on HTTPX, having taken some time off due to family circumstances.

With thanks as ever to all our wonderful sponsors, maintainers & contributors.

&mdash; Tom Christie, 11th November, 2020.
