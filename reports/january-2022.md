---
layout: reports
title: "January 2022"
---

## Monday 3rd January

#### Work on `httpcore`

Added support for HTTP/2 when requests are made via proxy tunnelling.

* https://github.com/encode/httpcore/pull/468

## Tuesday 4th January

**Holiday**

## Wednesday 5th January

#### Work on `httpcore`

New minor version.

* https://github.com/encode/httpcore/pull/476

If TLS fails, then ensure the underlying socket is closed.

* https://github.com/encode/httpcore/pull/475

Slimming down the requirements file.

* https://github.com/encode/httpcore/pull/469
* https://github.com/encode/httpcore/pull/470
* https://github.com/encode/httpcore/pull/472
* https://github.com/encode/httpcore/pull/473
* https://github.com/encode/httpcore/pull/474

#### Work on `httpx`

Pass through `http1` and `http2` configuration arguments from `httpx` to `httpcore`, then release as a new minor version.

* https://github.com/encode/httpx/pull/2009
* https://github.com/encode/httpx/pull/2011

## Thursday 6th January

#### Work on `starlette`

Review work on behaviours around `Content-Length` headers for empty responses, and 204, 304, 1xx cases. Initially as a review comment, then collaborating on a pull request to address the issue.

* https://github.com/encode/starlette/pull/1270#issuecomment-1006510664
* https://github.com/encode/starlette/pull/1395

#### Work on `httpx`

New minor release resolving a regression in behaviour for streaming uploads.

* https://github.com/encode/httpx/pull/2016


## Friday 7th January

General triage across `starlette`, `httpx`, `httpcore`.

---

## Monday 10th January

General triage across `uvicorn`, `starlette`, `httpx`.

## Tuesday 11th January

General triage across `starlette`, `httpx`, `uvicorn`. (12 items.)

The most problematic issue is this case in https://github.com/encode/httpx/discussions/1951

## Wednesday 12th January

General triage across `starlette`, `httpx`

Resolved yesterdays problematic issue by changing our policy on attempting to help users with global resource leaks. The behaviour within `__del__` methods during a Python exit isn't reliable. Switching to no longer performing implicit closes on `__del__` brings us into line with the behaviour in `requests`.

- https://github.com/encode/httpx/pull/2026

Work on adding SOCKS support to httpcore.

- https://github.com/encode/httpcore/pull/478

Improve error messaging from httpcore when server disconnects before sending the response.

- https://github.com/encode/httpcore/pull/479

## Thursday 13th January

Continuing work on socks5 support for `httpcore`.

- https://github.com/encode/httpcore/pull/478

## Friday 14th January

Triage on Django REST framework, `uvicorn`, `starlette`.

---

## Monday 17th January

Triage on Django REST framework, `starlette`, `httpx`

Add `proxy_auth` argument to `HTTPProxy()`.

- https://github.com/encode/httpcore/pull/481

## Tuesday 18th January

Added docs for `SOCKSProxy` support to `httpcore`.

Released `httpcore` 0.14.5.

Integrating SOCKS support into `httpx`.

- https://github.com/encode/httpx/pull/2034

## Wednesday 19th January

General triage.

## Thursday 20th January

Pull request to `h11` adding a GitHub action for automated deployments.

- https://github.com/python-hyper/h11/pull/142

Team management work (redacted).

General triage. See below for a couple of good examples.

- https://github.com/encode/httpcore/discussions/486
- https://github.com/encode/httpx/discussions/2037

## Friday 21st January

Organisational issues. Looking at how we can have tighter control over `httpx` and `httpcore` releases, while still having a low-friction release process.

- https://github.com/encode/httpx/pull/2040
- https://github.com/encode/httpcore/pull/487

---

## Monday 24th January

The `httpcore`, `httpx`, `starlette` and `uvicorn` repositories now require approval from @encode/operations before deployments.

## Tuesday 25th January

Accounting.

Triage for `starlette`.

## Wednesday 26th January

I'm not super enthusiastic about the `charset_normalizer` dependency in `httpx`, so I've spent some time taking another look at if there's any more simple, but still effective approaches we can use for detecting text encodings on content that doesn't specify it.

Using the content from [this repository](https://github.com/tomchristie/top-1000) to try out simpler

## Thursday 27th January

General triage on `uvicorn`, `starlette`.

Spending some time thinking about better approach to character set detection in `httpx`.
* hex display for binary content in the command line client.

* Issue: https://github.com/encode/httpx/issues/2049

## Friday 28th January

Work on `httpcore`. Fix resource cleanup issue on task cancellation, and timeouts during streaming the response. Fix SOCKS proxy issue with `http` URLs.

* https://github.com/encode/httpcore/pull/491
* https://github.com/encode/httpcore/pull/492

"Automating package releases with GitHub" article.

* https://www.encode.io/articles/automating-package-releases-with-github
---

## Monday 31st January

General triage.
