---
layout: reports
title: "August 2021"
---

## Weeknotes: Friday 6th August, 2021.

#### HTTPCore

I've been putting more work into the [revised version of `httpcore`][0].

The repository now includes a simple README which is starting to outline how the interface looks...

```python
import httpcore

response = httpcore.request("GET", "https://www.example.com/")

print(response)
# <Response [200]>
print(response.status)
# 200
print(response.headers)
# [(b'Accept-Ranges', b'bytes'), (b'Age', b'557328'), (b'Cache-Control', b'max-age=604800'), ...]
print(response.content)
# b'<!doctype html>\n<html>\n<head>\n<title>Example Domain</title>\n\n<meta charset="utf-8"/>\n ...'
```

I've also [opened an issue][1] which sketches out my plans for the documentation and API.

What I'm particularly excited about here is the way that the design will allow you to drop into the network stack at various layers. I think the fundamentals of the design are going to make it much easier for developers to properly dig into and understand how the connection pooling works, and what's happening at each layer.

For example:

* Being able to examine the connections within the connection pool, and see what state each of them are in.
* Being able to work directly with individual HTTP connections, and get a better understanding of the different states an HTTP connection can be in.
* Being able to work directly at the network layer, or customise the network backend in order to perform logging, record/replay, network mocking, and other advanced functionality.

#### HTTPX

I've started drawing up a potential kickstarter to launch alongside the HTTPX 1.0 release. This has also helped me start to clarify what the roadmap for HTTPX ought to look like.

* Issuing an HTTPX 1.0 release. I've outlined my thoughts on [final blockers to this][2].
* An HTTPX 1.1 release, alongside an updated HTTPCore.
* An HTTPX 1.2 release, including an integrated command line client.

#### Django REST framework

I've made a tentative start on re-committing to a little more time on REST framework, by working through a couple of existing issues and discussions.

Really the project could do with having 1-day-a-week of my time dedicated to it.

I made the mistake this week of earmarking Friday for that work. In coming weeks I think it'd work better to have it be at the start of the week, since I think that'd help keep it prioritised.

[0]: https://github.com/tomchristie/httpcore-the-directors-cut
[1]: https://github.com/tomchristie/httpcore-the-directors-cut/issues/3
[2]: https://github.com/encode/httpx/issues/947#issuecomment-893576096
