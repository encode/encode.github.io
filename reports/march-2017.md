---
layout: reports
title: "March 2017"
---

## 3.6 Release

The 3.6 version was released at the start of the month, along with headline features of Interactive API documentation, and JavaScript client library. We’ve since been following up with bug fixes and minor improvements, resulting in two more minor releases.

## Triage

The issue count has been kept steady at around 165 open tickets.
We’ve had to close around 120 tickets over the month in order to keep the triage state on an even keel.

## "Rethinking the API framework"

This month I've started publically presenting design work that I’ve been undertaking for a fresh approach onto building a Python API framework.

This has initially been presented as the "Level Up! Rethinking the API framework." talk, at DjangoCon Europe in Florence.

The talk explains the design motivations behind this approach, and introduces the new [API Star](https://github.com/tomchristie/apistar) framework.

I'll be publishing the slides for this talk over the coming days. The API Star framework doesn't yet tie in with Django or REST framework, but I have some thoughts about how that might develop.

I'm convinced that this is an important piece of future-focused work, that's going to develop into a project that's hugely valuable
to our users and sponsors, so I'll likely be working on both API Star and Django REST framework in parallel for a while.

Following the repository is probably the best way to keep up to date with progress there, but I'll also be talking more about the project as it matures.

## Moving to a GitHub organisation

The `django-rest-framework` repository has finally matured enough to move from being a personal repository. We've moved the repository under [the "encode" organisation](https://github.com/encode/), which will be a central point for any open source projects that involve work paid out of our collaborative funding model.

Moving to an organisation also has several practical benefits in helping us to move away from being a "bus factor 1" project, and ensuring that we're legally and logistically able to transfer ownership and management of the project as needed.

This is an important insurance policy for the many companies relying on REST framework as part of their business.

## Our Community & Operations Manager role

Our community & operations position was originally launched with a 3 month commitment. Since Anna's fantastic work on reaching out to the community and gradually helping to grow our subscriptions, I'm now broadly confident that we can sustain this part-time position on a rolling basis.

Having someone else on the team who is deeply involved in the operational side of the business has been greatly beneficial in keeping everything running smoothly, and is an important part of making sure that we aren't entirely reliant on any one single person.

This month Anna heavily focused on another round of fundraising. She created a sponsorship prospectus, updated the [funding page](https://fund.django-rest-framework.org/topics/funding/) on the REST Framework website, reached out to and followed up with close to 300 prospective sponsors, and sourced over 200 new prospective sponsor contacts.  She created email templates for all sponsor communication and wrote and updated internal housekeeping documentation. Anna managed all daily operations, which includes communication with sponsors, scheduling calls with prospective sponsors, reviewing payments in Stripe, keeping sponsorship information on our website up-to-date, updating internal spreadsheets, monitoring our new [Twitter account](https://twitter.com/restframework), etc.

Additionally, Anna started gathering ideas for and writing first blog posts and tweets since we are working on starting a blog on the [encode.io](http://www.encode.io) website and getting more active on Twitter, which we are hoping will help us spread the word about Django REST framework and gain new sponsors.

## What’s Next?

Given the current turnover of tickets, keeping up with triage is going to fill a large amount of time. I’ll be starting to think about functionality for the 3.7 release, and also continuing to work on API Star.

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 7th April, 2017.
