---
layout: reports
title: "February 2019"
---

## REST framework

We've issued a 3.9.2 release, with large number of minor improvements, updates
and bug fixes.

* Routers: invalidate _urls cache on register().
* Deferred schema renderer creation to avoid requiring pyyaml.
* Added 'request_forms' block to base.html.
* Fixed SchemaView to reset renderer on exception.
* Update Django Guardian dependency.
* Ensured support for Django 2.2.
* Made templates compatible with session-based CSRF.
* Adjusted field validators to accept non-list iterables.
* Added SearchFilter.get_search_fields() hook.
* Fix DeprecationWarning when accessing collections.abc classes via collections.
* Allowed Q objects in limit_choices_to introspection.
* Added lazy evaluation to composed permissions.
* Add negation ~ operator to permissions composition.
* Avoided calling distinct on annotated fields in SearchFilter.
* Introduced RemovedInDRF…Warning classes to simplify deprecations.

## TypeSystem

I've released a new stand-alone package for data validation and form rendering:
[TypeSystem](https://www.encode.io/typesystem/).

* Handles both data validation and form rendering equally.
* Supports positional error marking within JSON or YAML documents.
* Supports templated form generation, or pre-packaged form themes.

The `typesystem` package is important for a couple of different reasons.

* We'd like to properly pull the API documentation generation out of being a
REST framework built-in, and into a standalone package. `apistar` has been a
start on this, but a stand-alone package that can nicely render form inputs
based on information in an API schema would help improve the API documentation
generation substantially.
* REST framework's serializers being able to support data validation *or* form
rendering has always been a big feature - it's important that we bring that
into a standalone package, to make it more widely available.
* The `databases` and `typesystem` packages together are the two foundational
pieces we'd need in order to implement a fully async ORM.

## The ASGI ecosystem

Uvicorn, Starlette, and Databases have all been maturing nicely, with
various improvements in each.

There has been significant work towards a 3.0 version of the ASGI specification,
which uses a single-callable interface, rather than the previous double-callable
structure:

* `async def asgi(scope, receive, send)`

This will result in simpler ASGI implementations and neater tracebacks.

Servers such as Daphne, Uvicorn, and Hypercorn will remain compatible with
both versions of the specification for the foreseeable future.

## Finances

I've not had a chance to fully review our finances recently, but we're
running a bit in the red right now. This isn't an imminent issue, as there's
currently enough in the bank to operate at the current level for a while,
but it'll need closer review over the next couple of months.

There's a *really strong business case* in signing up for a sponsorship if your
company has any significant investment in:

* Making your business highly visible to the widest possible audience of
developers and potential job applicants.
* Ensuring Django REST framework can remain well supported for the for
foreseeable future.
* Ensuring the Python web ecosystem remains a highly competitive choice over the
medium and long term.

---

As ever thank you so much to all our sponsors, contributors, and users.

&mdash; Tom Christie, 7th March, 2019.
