---
layout: reports
title: "August 2020"
---

# Django REST framework

I've started drawing up the release notes for 3.12. It's likely that we'll issue
a release within the next two weeks, since there's plenty of new functionality
that's waiting for release right now.

# HTTPX

Our latest HTTPX releases include a number of refinements and bugfixes, as well as some new functionality:

* Default headers such as `User-Agent` are now set on `client.headers`, rather than constructed directly on the request instance,
making it easier to remove or override them from all client requests.
* [Unix Domain Socket support](https://www.python-httpx.org/advanced/#custom-transports).
* Support for connecting [via a specfic local address](https://www.python-httpx.org/advanced/#custom-transports).
* When a client has `auth=...` set, we now support disabling auth on a per-request basis.

We've also made significant progress on a number of more major features, such as:

* Supporting connection retries with `Client(retries=<int>)`.
* Supporting an event hooks API.
* Supporting async or sync authentication flows that require I/O.
* Preliminary work on an HTTPX command line tool.
* Allowing `Request` or `Response` instances to be used in wider contexts, such as for unit testing auth classes...
  * Only adding mandatory headers such as `Host: ...` when requests are instantiated directly.
  * Supporting usages like `response = httpx.Response(content=..., text=..., html=..., json=...)`

---

Thanks as ever to all our sponsors, contributors, and users,

&mdash; Tom Christie, 3rd August, 2020.
