---
layout: reports
title: "November 2021"
---

## HTTPX

HTTPX 0.21 has now been released, which integrates against the newly redesigned `httpcore` package described in the last monthly report.

The most notable features that this enables are some improvements in the command-line client.

* SSL certificate information is now displayed when using the `-v`/`--verbose` flag.
* Connection information indicating the connected IP is now displayed when using the `-v`/`--verbose` flag.
* When HTTP/2 is enabled with `--http2`, the request will now correctly display as either HTTP/1.1 or HTTP/2 depending on if connection actually ended up negotiating as HTTP/2 or not.

These improvements are possible as a result of the new `trace` extension supported by the latest `httpcore` version.

Alongside this, the redesigned `httpcore` has been released as 0.14. For more information see the [comprehensive new documentation](https://www.encode.io/httpcore/).

Release notes:

* [`httpx 0.21`](https://github.com/encode/httpx/blob/master/CHANGELOG.md#0210-15th-november-2021)
* [`httpcore 0.14`](https://github.com/encode/httpcore/blob/master/CHANGELOG.md#0140-november-11th-2021)
