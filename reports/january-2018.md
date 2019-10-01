---
layout: reports
title: "January 2018"
---

## CoreAPI

I've started work towards a 3.0 release of `coreapi` - the library that powers our schema representations, documentation generation, and client libraries.

Core API initially started out as an attempt to address hypermedia responses, and demonstrate how we could include both data and links in responses. However by far the biggest use-case has been it's ability to be used for API schema representations.

For all practical purposes, I think this is where our tooling needs to be in focused. Focusing solely on Schema support, rather than general purpose Hypermedia support will allow us to cut some complexity out of the project.

Version 3.0 will include better support for data type representations, which will be included in the core package, rather than in `coreschema`. The new version will also include built-in `OpenAPI support`.

## 3.8 release

We're currently working towards a 3.8 release. This is largely a maintainance release.

It's possible that some of the work on CoreAPI might tie in with our 3.8 release too, for example, we'd like to add support for including response schemas in our schema outputs, which might make it in to the 3.8 release.

## Triage

We're maintaining a fairly steady ticket count, with generally a little less that 100 open issues, and around 25-30 pull requests.

Having a regular income and being able to pay for both Carlton Gibson and my own time on the project has been invaluable in keeping our triage on track.

## Finances

Our income is currently around £5000/mo. This currently pays for Carlton Gibson's contracting time, 50% time from myself, and a small amount of ongoing time from Anna Ossowski, handling our invoices and other operations.

I'm currently spending the other 50% of my time on freelancing.

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 15th February, 2018.
