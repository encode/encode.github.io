---
layout: reports
title: "September 2017"
---

This month we're welcoming Carlton Gibson to the team.

Carlton has been one of our core contributors for several years. We're fortunate enough that our sustainable funding has now enabled us to take him on in a part-time capacity. He has taken responsibility for most of the REST framework triage work, and additionally he and Tom have been collaborating closely on the upcoming 3.7 release.

## 3.7 release

The 3.7 release focuses on improved schema generation & API documentation. We've approached this by allowing more configurable per-view customization of how the API schema is generated. This will allow developers to fill in the gaps when the default behaviour isn't sufficient to correctly introspect the schema.

We're  planning to make the 3.7 release available in the next few days.

This work has been made possible by Bayer - https://www.bayer.com/ - who have sponsored the release. We're hugely thankful for their support.

## Triage

The issue count has been reduced from around 175 open tickets at the start of the month, to 145 open tickets at the end. We're expecting to be able to reduce this further over the next month, as the customizable schema generation in 3.7 is helping wrap up a number of long-standing tickets.

## API Star

Work has been continuing on API Star. We've recently added `asyncio` support, and will be working towards Flask and Django compatibity.

There's plenty of rough edges still, as the dependency injection style presents a different set of design challenges than REST framework, although you should expect to see things starting to smooth out with a 0.3 release planned for later this month.

## Working towards hosted APIs

We want teams working with REST framework or API Star to be able to get their backend system into production as seemlessly and quickly as possible.

In order to enable that I've started working on a hosted API product. The plan is that teams will be able to use the product to build out their Admin and API in production from day one, while still being free to export that into the framework code that they can modify and self host at any time.

We'll be keeping you up to date with progress in the monthly releases, and will start making the project public once it's sufficiently mature.

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 2nd October, 2017.
