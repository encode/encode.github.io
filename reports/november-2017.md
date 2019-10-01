---
layout: reports
title: "November 2017"
---

This month's report is based on writing up a retrospective of our Mozilla Award from Summer 2016. We'll be publishing this write-up more formally on the REST framework website in the near future.

## Background

In summer 2016 the Django REST framework project [was awarded $50,000 from Mozilla, through its ongoing MOSS program.](https://blog.mozilla.org/blog/2016/04/13/mozilla-open-source-support-moss-update-q1-2016/)

The project was already well-established, but the scope of the framework and the size of our userbase meant that it was becoming unsustainable to continue to push the project forward without a significant amount of funded time being made available.

Our proposal included adding client libraries, improving support for API schema generation, and improved integration with WebSockets, for realtime API endpoints.

## Work to date

Over 2016 and 2017 the award has helped fund time from Tom Christie, Anna Ossowski, and Carlton Gibson. Together with the project's other contributors, we've been able to make a series of major releases from 3.4 through to 3.7.

Major functionality we've added in that period has included:

* Python client library.
* JavaScript client library.
* Command line client.
* Integrated schema support. (Swagger, RAML, CoreJSON)
* New test client.
* Interactive API documentation.

There has also been work not on REST framework itself, but in the surrounding ecosystem.

Tom has been able to help navigate the "Simplified URL routing syntax" feature into Django 2.0, alongside a number of other contributors.

There has been work around async and realtime, although not yet directly in REST framework itself. This has included developing a new Python Web-Server, Uvicorn, with an ASGI-like asyncio interface, as well as significant exploratory work towards a new framework, API Star.

Over the last 18 months we've been closing incoming issues and pull requests at a sustained rate of around 80 issues/month.  

We've gone from standing at around 210 open issues and pull requests at the start of the period, to being at  around 110 to date.

## Sustainability

The Mozilla Award has also been a foundational part of allowing us to launch an ongoing, sustainable business model behind the project. Having a significant amount of runway funding meant that Tom Christie was in a position to leave full-time employment, and launch a sponsorship model for funding REST framework.

The result of this is that although the MOSS funding is now exhausted, the project still has money in the bank, and a decent amount of monthly recurring revenue.

We're aiming to keep our finances transparent through our monthly reports.

As a rough guide we are currently at around £5,500 monthly recurring revenue. Against this Tom draws a salary of £60k/year. Together with short amounts of freelancing we've also been in a position to take on freelance work from both Anna Ossowski (Fundraising & Operations), and Carlton Gibson (Triage & Feature Work).

## Impact

There are now around 100 third party packages available for use with REST framework, and we've had over 700 contributors to date.

We'd currently estimate something like 100,000 monthly active developers working with the framework, supporting perhaps some tens of thousands of companies, and certainly impacting many millions of end-users.

A project supporting this many developers and companies cannot realistically operate without dedicated working hours towards its support. We wouldn't be in such a strong position without the MOSS award giving us enough runway to be able to launch our sponsorship model.

## What's next

We'll be continuing to keep a strong focus on triage, and keeping the project healthy. We've also got some feature work planned on improving websocket integration, and support for exposing expected response structures in the API documentation.

There's also likely to be further work expanding our horizons with the API Star project.

As an independent open source project with a sustainable business model, we're something of an exception. It is worth highlighting that we're currently only able to operate by including some amount of freelancing into our schedule.

If you business uses and relies on Django REST framework we would *strongly* encourage you to [sign up to our sponsorship program today](https://fund.django-rest-framework.org/topics/funding/) and help ensure that we're able to keep supporting and pushing forward the project.

---

Thanks as ever to our wonderful sponsors, contributors, and users of the framework!

&mdash; Tom Christie, 4th December, 2017.
