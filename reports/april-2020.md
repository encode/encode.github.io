---
layout: reports
title: "April 2020"
---

# Django REST framework

While there has been a bunch of triage and minor fixes, our 3.12 release is still pending. I'll be looking at resolving this as a priority for May.

# HTTPX

We've now issued a 0.13 pre-release for `httpx`. You can install this release using `pip install httpx --pre`.

The 0.13 release is a big milestone since it drops `urllib3` for the sync client, and instead uses `httpcore` for both the async and the sync clients.

This means that:

* Our networking behaviour between both the sync and async clients should now be identical.
* We have HTTP/2 support for the sync client.
* The low level HTTP transport interface is really tightly defined by the `httpcore` API, with a strict separation of concerns between the component that makes the HTTP requests, and the component that adds extra client smarts on top of that. (`httpcore` and `httpx`, respectively.)

In order to make this possible, we've dropped support for a lesser-used feature of being able to make requests directly to a Unix domain socket.

We'll give our pre-release a while to get bedded-in, before promoting it to a full 0.13 release. At that point we're ready to start reviewing any final API points that need addressing prior to a 1.0 release.

# Dashboard

The `dashboard` package is the first-pass of an admin-like interface for Starlette and other ASGI frameworks.

Dashboard is designed to be able to plug directly into the ORM package, but may also to be used with alternate datasources too. A `DataSource` interface provides the contract that is required for alternate implementations.

The package currently depends on pre-release versions of `orm` and `typesystem`, and is still very much in a design stage, but you'll be able to get a bit of an idea of how the API looks from the README.

# Project management improvements

The scope of the async web stack has been growing over the last few months, so that we're now maintaining several projects in this space, including `uvicorn`, `starlette`, `databases`, `orm`, `typesystem`, `broadcaster`, `httpcore`, and `httpx`.

In order to keep scaling the maintenance work on those projects we've made some changes to the project management approach:

* We're now inviting any contributor who authors a successful pull request onto the maintainers team.
* Our GitHub settings enforce that all changes have to come via a pull request, and all pull requests require review.
* We've setup GitHub Actions to deploy to PyPI and update the documentation whenever a release is created in the GitHub interface, allowing anyone on the maintenance team to issue releases.

It's worth talking through our GitHub Action workflows a little,  since they might be valuable for other teams working with PyPI and MkDocs.

## Our workflow approach

We follow [GitHub's "Scripts to Rule Them All" pattern](https://github.blog/2015-06-30-scripts-to-rule-them-all/) for install, deploy, and test scripts.

Any complexity is kept out of the workflow steps, which just call into the scripts. For example, here's the "steps" configuration for our Test Suite workflow:

```yaml
steps:
  - uses: "actions/checkout@v2"
  - uses: "actions/setup-python@v1"
    with:
      python-version: "${{ matrix.python-version }}"
  - name: "Install dependencies"
    run: "scripts/install"
  - name: "Run linting checks"
    run: "scripts/check"
  - name: "Build package & docs"
    run: "scripts/build"
  - name: "Run tests"
    run: "scripts/test"
```

## Deploying to PyPI

We've created an API token for each PyPI package, and then stored that in the repo secrets as `PYPI_TOKEN`.

The workflow file uses the API token to setup an appropriate environment for the publish script to run with...

```yaml
env:
  TWINE_USERNAME: __token__
  TWINE_PASSWORD: ${{ secrets.PYPI_TOKEN }}
```

Once we've done that we're able to either:

* Run `scripts/publish` from within a GitHub action, where it will use a PyPI token as the auth credentials.
* Run `scripts/publish` locally, where it will user whatever user PyPI credentials are currently setup.

Our publish workflow is setup to run whenever a release is tagged in GitHub...

```yaml
on:
  push:
    tags:
      - '*'
```

## Deploy the docs, using MkDocs

Deploying the documentation from a GitHub action is simple enough. We can use `mkdocs gh-deploy` to push a documentation release to the `gh-pages` branch.

There's two extra things we need to take care of...

* Deploys need to use the `--force` flag, so `mkdocs gh-deploy --force`.
* We need to set an appropriate user/email git configuration, when we're running within a GitHub action.

To set the Git user when we're running the deploy script as a GitHub action we use the following...

```shell
if [ ! -z "$GITHUB_ACTIONS" ]; then
  git config --local user.email "41898282+github-actions[bot]@users.noreply.github.com"
  git config --local user.name "GitHub Action"

  ...
```

The email address there *happens* to be the GitHub Action bot's designated email, which ensures that commits to the `gh-pages` branch display the bot avatar properly in the GitHub interface.

---


Thanks as ever to all our sponsors, contributors, and users,

&mdash; Tom Christie, 1st May, 2020.
