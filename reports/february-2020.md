---
layout: reports
title: "February 2020"
---

## Broadcaster

I've been spending some time working on how we can improve the state of realtime
web functionality in Python.

One core component that's required for scaling realtime systems past a single
host is having some kind of mechanism for "broadcasting" messages across
multiple servers.

Having a broadcast mechanism allows hosts to subscribe to a particular channel,
such as "chat events in the 'python' chatroom", and receive all events that
occur on that channel event, regardless of if the event occurs on the same
host server or not.

The outcome of this work so far is [a new package, broadcaster](https://github.com/encode/broadcaster),
which provides a broadcast API onto a number of different backend services,
currently including:

* Redis PUB/SUB.
* Apache Kafka.
* An in-memory broadcast backend.

#### Comparing Django Channels and Broadcaster

Django already has an answer to broadcasting messages, in the form of Django
Channels. With Django Channels, broadcast functionality is communicated using
the ASGI `send`/`receive` messages, with a "Channel Layer" acting as a message
bus for both WebSocket messaging and broadcast events.

The approach in the `broadcaster` is different, in that a broadcast backend is
treated as an independent backing service, configured similarly to a database
backend, or a cache backend. The core package provides a simple consistent
interface for subscribing to a channel or or broadcasting a message onto a
channel, while the backend implementation handles marshaling those API calls
into the actual network calls for the particular backend implementation.

#### Motivation

Given that Django Channels currently exists, it's fair to ask why take another
approach onto broadcast functionality? I think `broadcaster` is a lighter
approach that's more likely to be suitable for integrating with other existing
frameworks. It'll also allow us to explore adding functionality such as
APIs for retrieving event history.

## HTTPCore

Another package released in the last month is `httpcore`. The HTTP Core package
is an absolutely minimal HTTP client that doesn't provide any client smarts
such as redirect handling, session cookies, URL parsing, multipart uploads,
or anything at all other than simply "send an HTTP request and return a response".

The intent is to use `httpcore` as the backend to `httpx`, so that there's
a meticulously clear interface split between the high-level client, and the
low-level network handling.

## Django REST framework

There's been continuing triage on REST framework, and Carlton Gibson has been
progressing some of the Open API related issues.

Ideally REST framework could do with a funded part time position in the way
that we've been able to offer at some points in the past, although we're not in
a financial position to do that currently.

## Finances

Our total revenue for the last month was about £5,300. Operating costs including
desk space, accountants, and various hosting and services were around £650,
*without* pricing in for conference costs.

## Call for sponsors

While I wouldn't describe Encode as "at risk" yet, we're pretty tight on
supporting a full time salary right now. I regularly turn down freelance work
in order to keep focusing on Open Source work, and I'd like to remain in a position
where I can continue to do so without the business coming under too much pressure.

Our impact in the Python Web space includes:

* Over 10,000 issues and pull requests fielded in "Encode" repositories to date.
* Maintaining Django REST framework, which now appears in over 100,000 GitHub repositories.
* Pushing forward the Python HTTP space with HTTPX, the only Python client to support both HTTP/1.1 and HTTP/2,
  and provide both sync and async APIs.
* Ensuring that Python continues to remain competitive in the high performance Web App space, with Uvicorn and
  Starlette, now also the basis for the FastAPI framework, which is rapidly growing in popularity.
* Helping mature Python's async web ecosystem with Databases, ORM, Broadcaster, and Typesystem.

You can [sign up as a sponsor on GitHub](https://github.com/sponsors/encode) or via
our [REST framework sponsorship site](https://fund.django-rest-framework.org/topics/funding/).

---

Thanks as ever to all our sponsors, contributors, and users,

&mdash; Tom Christie, 2nd March, 2020.
