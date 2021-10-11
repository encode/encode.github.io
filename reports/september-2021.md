---
layout: reports
title: "September 2021"
---

### HTTPX

We now have a 1.0 pre-release for HTTPX.

The `1.0.0.beta0` release adds a huge new feature, in the form of a command-line client...

<img width="700" src="https://github.com/encode/httpx/raw/master/docs/img/httpx-help.png" alt='httpx --help'>

<img width="700" src="https://github.com/encode/httpx/raw/master/docs/img/httpx-request.png" alt='httpx http://httpbin.org/json'>

The release also includes some design changes. The most notable of these is that
redirect responses are no longer automatically followed, unless specifically requested.

This design decision prioritises a more explicit approach to redirects, in order
to avoid code that unintentionally issues multiple requests as a result of
misconfigured URLs.

For example, previously a client configured to send requests to `http://api.github.com/`
would end up sending every API request twice, as each request would be redirected to `https://api.github.com/`.

If you do want auto-redirect behaviour, you can enable this either by configuring
the client instance with `Client(follow_redirects=True)`, or on a per-request
basis, with `.get(..., follow_redirects=True)`.

This change is a classic trade-off between convenience and precision, with no "right"
answer. See [discussion #1785](https://github.com/encode/httpx/discussions/1785) for more
context.

The other major design change is an update to the Transport API, which is the low-level
interface against which requests are sent. Previously this interface used only primitive
datastructures, like so...

```python
(status_code, headers, stream, extensions) = transport.handle_request(method, url, headers, stream, extensions)
try
    ...
finally:
    stream.close()
```

Now the interface is much simpler...

```python
response = transport.handle_request(request)
try
    ...
finally:
    response.close()
```

### Django REST framework

I've been making a little time for triage on REST framework. Heavy going, given the age of the project and the volume of (often outdated) issues, but making a bit of progress on getting the pull request and issue numbers down.

### Finances

Catching up on monthly finances, trimming down on a couple of expenses.

A rough breakdown of how Encode's monthly finances currently look...

* Income: £5,100 (~65% Stripe subscriptions, ~30% GitHub sponsors, ~5% direct billing.)
* Salary: £3,700
* Expenses: £650 (Fixed desk in a co-working space, accountants, software subscriptions.)

Taxes are missing from that monthly breakdown because they're not monthly. I'll need to take a review at the end of the company's financial year in order to determining if we're currently breaking even or not. (Hint: It looks a bit tight, but probably about okay at the moment.)
