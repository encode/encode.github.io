---
layout: reports
title: "October 2016"
---

The headline this month has been the 3.5 release. This included improved schema generation, the `requests` test client, the `coreapi` test client, provisional support for RAML schemas, error validation codes, and client library upload and download support.

I've also started work on a DEP for simpler URL routing in Django, which I'm hoping to get into Django core.

## Issues & pull requests

We're down from 160 open issues & pull requests at the start of the month, to 133 at the end.

There's been a total of 140 issues closed over the course of October. I've decided not to itemize the closed issues in the monthly summaries any longer, as I don't believe they're actually valuable. It's possible that I may consider substituting this with more detailed week-by-week style reports.

## Upcoming work

There's a fair bit of work on the table right now. The JavaScript client library and the API documentation tooling should tie together nicely, making it easier and faster to get client integrations up and running with your REST framework service.

There's plenty to do here, so expect this list to look fairly similar throughout both November and December, with a 3.6 release planned for January.

* Start work on the JavaScript client library, for 3.6.
* Start work on API documentation tooling, for 3.6.
* Start work on simpler URL routing in Django core.
* Write DEPs for introducing request parsing and content negotiation into Django core.
* Ongoing triage work. Aim to have issues count in double digits by end of the month, and pull requests count down to a single page (<25).
* Improve RAML support. Consider HAL and/or API blueprint support next.
* Revisit the interface for handling authentication in `coreapi`.
* Improve the `coreapi` documentation, for the core project, and for the command line client.
* Design & investigatory work towards a possible asyncio framework.

## Finance

We've now just passed a little over our baseline sustainability figure! As a result I've now started purchasing some JavaScript development time in order to help push work on the client library forward at a faster pace.

There's still a lot that further sponsorships would allow us to do, both in ensuring future stability, and in accelerating the existing work. If your business has not yet signed up for a paid plan, please consider doing so.

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 1st October, 2016.
