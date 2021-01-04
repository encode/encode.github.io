---
layout: reports
title: "December 2020"
---

# Django REST framework

REST framework these days is in the somewhat odd position of both being the primary driver of our sponsorships, while also being feature complete and generally not in need of any significant development beyond keeping pace with upcoming Django releases.

Work here probably needs to be focused on good communication aimed at minimising the workload needed to keep the project well maintained.

# HTTPX

We’ve not been making big promotional dances about HTTPX, nor is the level of attention to detail that’s gone into its development necessarily obvious at a surface level. I’m perfectly happy with both of those, and quietly confident in its potential to be a cornerstone of the Python HTTP ecosystem.

The work we’ve put in has kept the internal complexity to a minimum wherever possible, and will enable us to work on developing further functionality that perhaps wouldn’t be as feasible otherwise. One case here could be supporting WebSockets over both HTTP/1.1 and HTTP/2 connections. Another would be supporting HTTP/2 bi-directional streaming, perhaps even allowing for use-cases such as gRPC. Integrating HTTP/3 support is another possible avenue.

### Notes on a 1.0 release

Laying down a 1.0 milestone has been pending on one particularly thorny design decision, which I’ll give a brief outline of here. Taking a call on this won’t affect the vast majority of users, but it does propagate throughout the stack, and would change the low-level “Transport API”.

The design decision has to do with resource management at the level of an HTTP request. Whenever a request is issued, there subsequently needs to be a point at which the resources are afterwards released. Either because the HTTP response has been read to completion, because an error occurred, or because the client closed the connection pre-emptivly, having read the headers and status code, but without ingesting the response body.

Resource management like this can either be handled using context management...

```python
with transport.request(...) as response:
    ...
```

Or with explicit callbacks...

```python
try:
    response = transport.request(...)
finally:
    response.close()
```

There is an argument to be made in favour of the low-level API *always* being strictly context managed. There’s a very close parallel to the constraints of “structured concurrency” here, although the resources being governed are not threads of control, but network resources. However, it’s such a fundamental change to the internal stack throughout that we’ve not yet been confident enough to go ahead with a switch there, and the associated knock-on effects that it has on some lower-level parts of the public API.

Taking a call on this is likely the final major blocker before issuing a 1.0 release.

# Starlette

Work on Starlette has been on hold lately, as it is fairly feature complete, although would benefit from better documentation.

It is feasible that the next useful piece of work here could be integrating HTTPX as the test client.

# Financial report

Sponsor income for the financial year 2019/2020 was about £60k. Less admin expenses of £13k. (office rental, accountancy costs, conference travel, cost of software services). Less corporation tax of £5k. Total remaining for salary/dividends £42k.

At some point something will need to change here, at least a little, but we've currently enough in the business bank account to give us some runway for the time being.

---

With thanks as ever to all our wonderful sponsors, maintainers & contributors.

&mdash; Tom Christie, 4th January, 2021.
