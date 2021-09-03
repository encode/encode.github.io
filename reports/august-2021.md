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

 ## Weeknotes: Friday 13th August, 2021.

 The most significant piece of work this week has been re-assessing the automatic charset decoding policy in HTTPX.

 When an HTTP response is returned it'll generally have a `Content-Type` header indicating if the response is a text document, such as `text/html`, or a binary file, such as `image/jpg`. For textual content we need to pick a character set to use in order to decode the raw binary content into a unicode string.

 Ideally the server will indicate which encoding is being used within the `Content-Type` header, with a value such as `text/html; charset=utf-8`. However, the `charset` parameter isn't always present, and we need a policy to determine what to do in these cases.

 Previously we'd adopted a keep-it-simple policy in `httpx`, and attempted `utf-8` with fallbacks to other common encodings, but having been prompted to re-assess this, it seemed worth some time taking an evidence led approach onto determining what decoding policy to use.

 In [this repository](https://github.com/tomchristie/top-1000) I've taken a list of 1000 most accessed websites, and saved the downloaded content and response headers. Of these sites...

 * ~75% Included a Content-Type header complete with an explicit charset.
 * ~20% Did not include a charset, and decoded okay with `utf-8`.
 * ~5% Did not include a charset, and did not docode okay with `utf-8`.

 Based on these results we've decided to reintroduce automatic charset detection for cases that don't include a `charset` parameter. The results also demonstated sufficiently that the newer `charset_normalizer` package performed as well or better than `chardet` at detection, while being significantly faster.

 ## Weeknotes: Friday 20th August, 2021.

 Released HTTPX 0.19

 ### Added

 * Add support for `Client(allow_redirects=<bool>)`.
 * Add automatic character set detection, when no `charset` is included in the response `Content-Type` header.

 ### Changed

 * Event hooks are now also called for any additional redirect or auth requests/responses.
 * Strictly enforce that upload files must be opened in binary mode.
 * Strictly enforce that client instances can only be opened and closed once, and cannot be re-opened.
 * Drop `mode` argument from `httpx.Proxy(..., mode=...)`.

 ## Weeknotes: Friday 27th August, 2021.

 **Holiday.**
