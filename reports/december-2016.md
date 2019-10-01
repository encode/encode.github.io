---
layout: reports
title: "December 2016"
---

## Announcing our Community & Operations Manager

I'm excited to announce that Anna Ossowski will be joining us in order to focus on community management, fundraising, and taking on responsibility for various aspects of running a business that supports Django REST framework.

Anna will be well known to many of you in the Python and Django communities. She is involved in PyLadies, PyCon US, and DjangoCon US, and additionally has experience working as Community Manager for the Pinax project, with the folks at Eldarion.

## Current work

I'm continuing to work towards the upcoming 3.6 release, which is expected to be available towards the end of February. The headline features of this release will be:

* A JavaScript client library for interacting with REST framework APIs.
* Built-in API documentation, that includes live API integration, and automatically generated code examples for all our supported client libraries. (Initially Python, JavaScript, and a Command Line client.)

While these tools will be integrated seamlessly into REST framework, it's worth noting that I'm actually working towards both of these being usable with *any* Web API that exposes a supported API schema format, such as Swagger.

#### API documentation

Most of the development time at the moment is going into building out the API documentation for the next release of REST framework. This will include generated documentation for the Python and JavaScript client libraries, plus others as we develop them.

One particular aspect of the API documentation that I'm spending a lot of time on is that Core API needs some further work in order to better describe expected input and output types, which is not currently supported. You can keep track of that ongoing work at the coreschema repository - https://github.com/core-api/python-coreschema - although you'll probably want to wait until it has been documented, and the motivation more fully explained, before diving in.

#### JavaScript client library

I'm continuing to collaborate on the JavaScript client library with the team at my former employer, DabApps. Hoping to be able to release this towards the end of February.

#### Simpler path routing DEP

I'm deferring any work on this in favor of 3.6 release features. This won't make the Django 1.11 release.

## Issues & pull requests

Keep on top of triage has been continuing to fall behind slightly in preference to the feature work required for the 3.6 release. We're up from 150 open issues & pull requests at the start of the month, to 160 at the end.

## Financial

Right now the business is roughly break-even for supporting one full-time employee. Taking on the Community & Operations manager means we're below break-even for the moment, but we're hoping that the fundraising aspect of the role will compensate for that.

There are a number of aspects where we'd like to be able to have enough revenue to move the project forward more quickly. Some examples of work we'd like to be able to fund currently include:

If we could increase our sponsorships by 50% we'd additionally be able to consider a part-time role that's entirely focused on ticket triage and resolution, which would be a huge benefit to the project.

If we could increase our sponsorships by 100% we'd furthermore be in a position to pay for development time on building API client libraries in a range of programming languages. These would be integrated directly into the upcoming API documentation.

In our view, the collaborative investment model is a smart approach to developing open source software. By allowing companies to collectively share the development cost of these efforts we're able to deliver better tooling for your developers, without pushing the cost of that onto any single company or organization.

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 12th January, 2017.
