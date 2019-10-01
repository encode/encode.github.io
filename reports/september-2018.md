---
layout: reports
title: "September 2018"
---

## REST framework

The Django REST framework 3.9 will be released later this week. This will include a new schema generation command for writing an `OpenAPI` specification.

Given that the API ecosystem has now pretty much standardized on OpenAPI as the format for describing API services, we're going to be gradually moving away from `coreapi`, and towards writing OpenAPI specifications.

This should open up a greater range of API documentation, client library generation, and other API tooling.

## API Star

The focus of [the API Star project](https://docs.apistar.com/) has been significantly re-scoped with the release of 0.6. The project is now a stand-alone toolkit for:

* Generating API documentation.
* Validating API schemas.
* Using as a dynamic client library.
* Providing a type system for request/response validation.

There is no longer any server-framework as part of the package at all. Instead I'll be aiming for it to be a general purpose tool kit that can be used alongside any Python web framework.

Refocusing the project in this way is intended to be to the benefit of REST framework developers, as it'll help us focus on tools such as the OpenAPI-driven client library, which will gradually start to replace the existing `coreapi` package.

Here's an example of how the client library is looking:

```python
import apistar


schema = """
openapi: 3.0.0
info:
  title: Widget API
  version: '1.0'
  description: An example API for widgets
paths:
  /widgets:
    get:
      summary: List all the widgets.
      operationId: listWidgets
      parameters:
      - in: query
        name: search
        description: Filter widgets by this search term.
        schema:
          type: string
"""

client = apistar.Client(schema)
result = client.request('listWidgets', search='cogwheel')
```

## Starlette

Starlette has taken over from `apistar` in terms of my focus on building out a really nicely designed and well-scoped ASGI framework. There's lots of work currently going on into maturing it, including:

* Support for class-based WebSocket handlers.
* Support for in-process background tasks.
* Support for CORS and other middleware.

## MkDocs

I've been starting a bit of exploratory work towards a possible next iteration of `mkdocs`.

The MkDocs project is what we use for all our documentation, and was originally built in order to generate the Django REST framework docs. It's a great project, with a pretty decent user-base, but currently is really only designed specifically for themed project documentation, rather than general purpose static sites or blogs.

I haven't reached any firm decisions about how to progress this yet, and the project is not yet particularly intended for public use, but if you're interested in keeping an eye on things, the repository is currently at https://github.com/tomchristie/mkdocs2

I'm using this latest project to build the [Encode OSS website](../index.html) and [monthly reports](index.md).

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 1st October, 2018.
