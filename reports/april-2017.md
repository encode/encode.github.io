---
layout: reports
title: "April 2017"
---

Work during April has largely focused on triage, preparation for PyCon, organisational work, and initial development of our newer project, API Star.

## Triage

The issue count has been reduced from around 165 open tickets at the start of the month, to 150 open tickets at the end. We’ve closed about 80 tickets over the month.

There are a number of minor fixes that will be released with the upcoming 3.6.3 version. You should expect to see this land either this week or next.

## PyCon

We’ve been doing plenty of preparation for PyCon. This’ll be hosted in Portland, Oregon, this month. We’re fortunate enough to have a booth at the event, and have a number of lovely folks who’ve offered to give us a hand with the staffing.

## API Star

I’m continuing to invest time into API Star. This might seem counter-intuitive, given that REST framework already exists, but I think there’s some very important future-focused work to be done here, that we couldn’t easily fit into the existing Django REST framework project.

It’s very possible that some of this work will eventually feed back into REST framework. For those wanting a little more information on this all, there is an open thread on the discussion group about [how API Star fits in with Django REST framework.](http://discuss.apistar.org/t/how-does-api-star-fit-in-with-django-rest-framework/15)

Once the project is in a sufficiently mature state I’ll consider bringing it into the `encode` GitHub organisation.

We will of course be featuring our existing sponsor placements on both sites, once we have a documentation site for API Star.

## Reducing the operational bus-factor

Myself and Anna have been spending some time documenting the processes around the business side of Encode. The most important aspect of this is about making sure that funded work on Django REST framework should be able to continue if I’m unexpectedly no longer able to work on the project at any point. This tends to be behind-the-scenes work at the moment, but making sure that everything is squared away is an important insurance policy for everyone who relies on the project.

## Our Community & Operations Manager role

This month Anna focused on fundraising again. She reached out to over 100 prospective new sponsors and followed up with a big batch of previously contacted sponsors.

She managed all daily sponsorship operations such as communication with sponsors, checking payments, issuing invoices, and adding new sponsors to our website.

Anna invested time into contributing to the company internal documentation, resources, and roadmap, which have been moved over to GitHub this month in order to keep everything in one place.

Anna has also been putting together resources for our volunteers for the Django REST framework booth at PyCon.

## What’s Next?

As ever, we’re going to need to keep a focus on triage, and keeping the issue count manageable. I don’t think we’re quite ready to start feature work on the 3.7 release, since there’s plenty of minor issues that still need resolving, particularly around cases where our API documentation or schema generation doesn’t work quite as expected.

The major bits of feature work are likely to be:

* I would expect feature work on our 3.7 release to start in June and to land in July.
* There will be ongoing work on API Star, alongside Django REST framework.

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 2nd May, 2017.
