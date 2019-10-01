---
layout: reports
title: "November 2016"
---

This month I've largely been working on various aspects of the upcoming 3.6 release...

#### API documentation tooling

The documentation tooling will exist both as a standalone command-line tool, and as an installable Django application. The planned functionality includes:

* Support for generating API documentation from Swagger, RAML, JSON HyperSchema, and API Blueprint schema formats.
* Support for automatic code samples. (Initially in JavaScript, Python, and for the Command Line, but other languages are also planned.)
* Support for documentation themes and theme customization.
* Live API interaction.

The majority of the tool is now complete - you can find the project at https://github.com/core-api/coredocs

The repository also includes links to examples of the built API documentation.

#### JavaScript client library

I've been collaborating on the JavaScript client library with the team at my former employer, DabApps. Progress is coming along nicely, and the client library is planned to be integrated into the documentation tool, allowing for live API interaction from the docs.

#### Simpler path routing DEP

I've done some work on the documentation for the path routing DEP in Django. Sjoerd Job Postmus has done a great job of kicking off the implementation. The alpha deadline for 1.11 is mid-January. There's not too much of substance that needs to be addressed, but we'll probably need more involved feedback on the proposal if we're to hit the deadline.

## Issues & pull requests

Keep on top of triage has been falling behind slightly in preference to the feature work required for the 3.6 release. We're up from 133 open issues & pull requests at the start of the month, to 150 at the end.

There's been a total of 81 issues closed over the course of November.

## Coming up

With the release of `coredocs`, the Core API ecosystem that powers REST framework's documentation is in need of a refresh throughout. This will move away from the abstract discussion of what Core API is, and move towards what Core API provides: Schema driven API documentation and client libraries.

We'll also need to put some work into representing API authentication information in the Core API representation. The aim of this will be to allow generic clients to authenticate against the API, without the developer having to manage the workflow themselves.

## Finance

We're currently a small amount over the baseline sustainability figure, although not with much headroom. I'll plan to issue a rough breakdown of expenditure at the end of the year.

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 5th December, 2016.
