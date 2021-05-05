---
layout: reports
title: "March 2021"
---

After nearly a year of mostly homeschooling, with all sorts of challenges along the way, we're gradually starting to get into a slightly more normal place in the UK. Schools at least have reopened, the small co-working  office I work out of is available again, and personally having been through a difficult few months I'm in a position to start focusing more fully on work again.

## Django REST framework

REST framework has had two new releases.

The issue tracker stood at around ~160 issues at the start of the month and is now down to ~100 issues.

I've been spending some time updating our workflow in order to try to keep the project more manageable, and ensure that available time can be focused on the most valuable issues.

In order to do this we've been switching over to a "Discussions first" workflow. The idea here is that the first point of contact as a collaborator ought to be GitHub's "Discussions" interface, rather than "Issues" or "Pull Requests". Starting a discussion is lower impact in terms of maintenance time, since they don't have any open/close status, and don't necessarily always need to be outright categorised & resolved by the core team. If a discussion is started and it gains traction, then we can request that it be escalated into a pull request or issue.

This ought to help us keep the issue tracker reserved for work that is genuinely and clearly actionable, and reduce the number of drive-by pull requests and issues that we have to deal with.

## HTTPX

We've been preparing for an upcoming 0.18 release, which I'll document in our next monthly report.

It's been a long careful road towards a 1.0, but the payoff is going to be worth it. Spending a great deal of time on finessing elements of the API all the way through the stack is eventually going to make it possible to do some things with HTTPX that aren't neatly provided for by existing libraries.
