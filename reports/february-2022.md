---
layout: reports
title: "February 2022"
---

## Triage

One of my main aims this month has been to reduce the issue and pull request
backlog across our projects. A lot of this ends up being able making sure that
the projects are clearly scoped, and declining to accept feature work on
projects.

I'd like to see all of our projects in a position where we've only one or two
pages worth of information on GitHub's issues or pull requests.

I've written in the past about my thoughts on [sustainable open source
management](https://www.dabapps.com/blog/sustainable-open-source-management/),
and the importance of keeping projects tightly scoped.

Here's how the triage work has gone this month. The numbers here are the total
number of open issues and pull requests for each project at the start and
end of the month:

* Starlette: 147 → 67
* Uvicorn: 135 → 87
* REST framework: 224 → 231
* HTTPX: 63 → 42

Examples of a couple of other projects that I think are managing their issues in
ways I'd like us to aspire to:

* [Flask](https://github.com/pallets/flask), and the other Pallets projects. At
  the time of writing, Flask has 14 open issues, and no open pull requests.
  This is an outstanding example of good project maintenance, considering that
  Flask is included as a dependancy by nearly 1 million GitHub repositories.
* [MkDocs Material](https://github.com/squidfunk/mkdocs-material). Martin Donath
  continues to manage this project with meticulous attention.

Next month's report will again include the triage figures for these four
projects. Clearly REST framework is going to need some seriously dedicated time
in order to get into shape - hopefully that'll be easier to do once the other
projects are all feeling sufficiently tightly managed.

## API Stability

Another important goal at the moment is reaching a 1.0 version for `httpx`.

I've been working a bit this month on a couple of changes related to this:

* Dropping our `charset-normalizer` dependancy. See [discussion #2083](https://github.com/encode/httpx/discussions/2083).
* Dropping our `rfc3986` dependancy.
