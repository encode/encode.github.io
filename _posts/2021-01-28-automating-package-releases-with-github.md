---
layout: articles
title: "Automating package releases with GitHub"
permalink: "/articles/automating-package-releases-with-github"
---

# Automating package releases with GitHub

I've spent some time this week improving our release workflow on several projects in the `encode` GitHub organisation.

We'd already got this to a pretty nice place, but there was a bit more we could do to ensure that our workflow was both low friction and secure.

Let's jump straight in...

## Using GitHub workflows to automate deploys

For a while now we've been using GitHub workflows to automatically deploy to PyPI, whenever a release is tagged on GitHub.

This has been working really well for us. It's really low friction, and it allows anyone on the maintenance team to issue a new release. It also ensures that the "deploy to release" phase isn't a blackbox "now a maintainer does some private magic on their local machine". Anyone is able to dig in an inspect the workflow, and see the console output of the script performing the deploy.

 Here's what we needed in order to get that setup...

 In order to be able to authenticate with PyPI we [need an API token](https://pypi.org/help/#apitoken). We create one of these tokens, and copy it down someplace.

 We can then [add that token as a "Repository secret"](https://docs.github.com/en/actions/security-guides/encrypted-secrets) in the GitHub repository settings interface. Once we've created a `PYPI_TOKEN` secret, and stored the API token value to it we can forget about the token entirely. It's no longer visible to us in either the PyPI or GitHub interfaces, and the only way it is ever accessed is through GitHub's workflows.

 Next up we'll need a workflow that uses the safely secured API token to actually perform the deployment. Here's our [`publish` workflow for `httpx`](https://github.com/encode/httpx/blob/master/.github/workflows/publish.yml).

 The rules for the workflow specify that it should be trigged whenever a tag is pushed to the repository...

 ```yaml
 on:
  push:
    tags:
      - '*'
```

We'd probably like to switch this to `v*` at some point, but historically our releases are tagged in the `0.21.1` style, so right now that's what we've got.

The action steps themselves are all nice and simple and clean. We use the GitHub "[Scripts to Rule Them All](https://github.blog/2015-06-30-scripts-to-rule-them-all/)" pattern, and I really like how it feels both from a local development perspective, and how clean it keeps our GitHub workflows.

```yaml
      - name: "Install dependencies"
        run: "scripts/install"
      - name: "Build package & docs"
        run: "scripts/build"
      - name: "Publish to PyPI & deploy docs"
        run: "scripts/publish"
```

The secret is pulled in by the workflow, here:

```yaml
        env:
          TWINE_USERNAME: __token__
          TWINE_PASSWORD: ${{ secrets.PYPI_TOKEN }}
```

This sets up the `TWINE_USERNAME` and `TWINE_PASSWORD` environment variables, so that when `twine` performs the deploy to PyPI it can use our safely secured API credentials.

Great! Now anyone on the team with `write` permission can [create a release](https://github.com/encode/httpx/releases) directly through the GitHub website, and [a PyPI deployment will automatically be triggered](https://github.com/encode/httpx/actions/workflows/publish.yml).

## Who's on the team?

We've got a pretty liberal policy towards inviting folks onto the `encode` maintenance team. If you've made any meaningful contribution then we'll add you to the team.

The [Python Hyper](https://python-hyper.org/en/latest/one-of-the-team.html) and [Trio](https://trio.readthedocs.io/en/stable/contributing.html#joining-the-team) teams both use this policy, and I think it's a pretty decent approach.

As the Trio docs state:

> Relax, you got this! And we’ve got your back. Remember, it’s just software, and everything’s in version control: worst case we’ll just roll things back and brainstorm ways to avoid the issue happening again. We think it’s more important to welcome people and help them grow than to worry about the occasional minor mishap.

Moreover, while the invite policy is liberal and helps encourage folks to jump in, our repository settings strictly ensure that all pull request require review and approval before they can be merged.

However... there's a bit of a conflict here. While we might like having a liberal policy on bringing new members onto the maintenance team, we might not want to be quite so relaxed about permissions to okay a release.

## Operations approval for deployments

It makes sense to be welcoming folks onto the maintenance team, but ideally we'd still like package deployments to require a strict sign-off.

Unlike pull requests, tagging a release in GitHub doesn't have any kind of "reviews" process, or anyway of requiring sign-off from a limited set of team members.

Personally I'd probably prefer it if release tags were only available to team members with either ["maintain" or "admin"](https://docs.github.com/en/organizations/managing-access-to-your-organizations-repositories/repository-roles-for-an-organization#repository-roles-for-organizations) permission, but not available to folks with "write" permission.

That'd allow us to have one larger team with "write" permission onto repositories, who are able to merge and approve pull requests, plus one smaller operations team with "maintain" permissions, who can additionally create releases.

Thankfully there is a different approach we can take. Enter [GitHub environments](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment#about-environments).

A GitHub environment is a context within which workflows are run. Crucially environments can be setup with their own constrained set of environment secrets, *and can be configured as requiring review before running*.

To get everything set up just the way we want it, we create a new "operations" team with a limited number of trusted individuals. We then create a new environment "deploy", which we configure as requiring review from the ops team.

At this point we'd also like to tighten up access to our PyPI API token. Instead of having the token stored as a "repository secret" and available to any workflow, we instead delete that, and create a new token stored as an "environment secret" associated only with the "deploy" environment.

Our PyPI token is now strictly gated to an environment that always requires ops sign-off in order to run.

Finally, we [need to adapt our workflow script](https://github.com/encode/httpx/pull/2040/files) so that it uses this new environment:

 ```yaml
     environment:
        name: deploy
```

And we're done.

Now whenever a new release is created in GitHub, the automated deployment process kicks in, and [requires sign-off from anyone on our operations team](https://github.com/encode/httpx/actions/runs/1751376911) before [publishing the release to PyPI](https://pypi.org/project/httpx/).

Low friction, well secured, automated package deployments. Lovely.
