---
layout: reports
title: "October 2021"
---

### HTTPCore

My most focused work this month has been on reworking the `httpcore` package. I've been spending a good chunk of time in documenting this redesign, and focusing on trying to provide an HTTP package that is tightly scoped in only providing the absolute core HTTP networking functionality, while still being a useful tool in it's own right.

### Hidden complexities

Handling connection pooling for both HTTP/1.1 and HTTP/2 connections is actually pretty tricky to get right. There aren't any other Python packages that handle this, and it has a number of awkward corner cases.

For example:

* When opening a connection we can't know upfront if it will end up being HTTP/1.1 or HTTP/2. We don't want to unnecessarily initiate new connections to the server if a single HTTP/2 connection will be sufficient, so when we have a connection that is still being established we need to queue incoming requests onto that connection, and retry them if it ends up being an HTTP/1.1 connection.
* A long-lived HTTP/2 connection can eventually exhaust the stream ID space. We can't know at the point of queueing a request onto a connection if this will occur, and need to retry the request on a new HTTP/2 connection if this condition does occur.

Being able to devote full-time focused work to redesigning `httpcore` is the kind of work that very likely might not be viable without a funded open-source model.

### Roadmap

The work on `httpcore` has been a substantial redesign. One a new release is made, we'll need a corresponding new release of HTTPX, which is backed by this new work.

Once that's done, it'd probably make sense for my to spend some time working on an `httpcore` based adapter for `requests`. This would be interesting as it would have the potential to bring HTTP/2 support either to `requests`, or perhaps to the widely-used `httpie` command-line tool.
