---
layout: reports
title: "August 2016"
---

This month has been a mix of triage, and working towards the 3.5.0 release.

## Issues & pull requests

We're down from 192 tickets at the start of the month, to 166 at the end. There will be a continuing emphasis on triage over September, to keep pushing the number down to a more manageable amount.

### Triaged

* `#4337` - Check allowed methods before checking permissions and stuff. *Reviewed & closed.*
* `#4333` - Add search_fields for fast token lookup. *Reviewed & closed.*
* `#4332` - urljoin with leading slash remove part of path. *Accepted & merged.*
* `#4335` - Possible exception during validation of IPAddressField. *Closed via `#4338`.*
* `#4336` - Test case for #4335. *Closed via `#4338`.*
* `#4318` - Invalid data type assigned into model while update. *Closed via #4339`.*
* `#4202` - Optionally sort JSON output. *Reviewed & closed.*
* `#4292` - FileUploadParser not compatible with Django Upload Handlers. *Reviewed & closed.*
* `#3610` - FileUploadParser should use more descriptive error when filename not included. *Closed via `#4340`.*
* `#4296` - Test large files. *Closed via `#4340`.*
* `#4341` - Format_suffix_patterns does not handle formats with `.` in them. *Reviewed & closed.*
* `#4342` - Fix ModelSerializer.get_validators with Meta property.  *Reviewed & closed.*
* `#4343` - OPTIONS Broken if View Renderer does not Handle Dict.  *Reviewed & closed.*
* `#3110` - Add regression test for grouped choices metadata. *Closed via `#3225`.*
* `#4205` - is_valid() fails for serializer with RegexValidator.
* `#4204` - Add failing test of deepcopy issue in is_valid.
* `#3565` - Partial updates always change fields that are not in data, read only, and have a default. *Closed via `#4346`.*
* `#4345` - Browsable API markdown description broken if tabs are used in code indentation. *Closed via `#4347`.*
* `#4236` - Change template context generation in TemplateHTMLRenderer. *Accepted & merged.*
* `#4257` - Added Limit/Offset pagination without counts. *Reviewed & closed.*
* `#4134` - UniqueTogetherValidator error message should return verbose_name. *Closed via `#3435`.*
* `#4276` - Need a test case against #4273. *Closed via `#4310`.*
* `#4060` - DRF does not accept unbounded RangeField. *Closed via `#4348`.*
* `#4198` - Always defer to explicit overrides. *Closed via `#4349`.*
* `#4199` - Fix #4198. *Closed via `#4349`.*
* `#2760` - Could not resolve URL if router is included under a namespace. *Closed via `#3816`.*
* `#4350` - Questionable Code in CursorPagination. *Reviewed & closed.*
* `#4351` - run_validators does not seem to conform the steps in Django. *Reviewed & closed.*
* `#4356` - "schemas.py" lacks support of "HEAD". *Reviewed & closed.*
* `#4355` - Add imports in validators docs. *Accepted & merged.*
* `#4354` - Django 1.10 RemovedInDjango20Warning: Using user.is_authenticated() and user.is_anonymous() as a method is deprecated. *Closed via `#4358`.*
* `#4330` - Schema generator ignores detail_route and list_route overrides of serializer_class.*Closed via `#4359`.*
* `#4331` - Fix detail_route and list_route overrides of serializer_class in schema generator. *Closed via `#4359`.*
* `#4365` - Update documentation. *Closed via commit `febaa4d`.*
* `#4366` - Fixed various typos. *Accepted & merged.*
* `#4367` - Add test for raising non-ValidationError in serializer, and it 'escape'. *Closed*
* `#4369` - Router Improvements. *Closed*
* `#4119` - Add tests for html-form-rendering choice fields. *Closed via `#4374`.*
* `#4121` - MultipleChoiceField incorrectly indicates value / selection state in HTML form output. *Closed via `#4374`.*
 * `#4120` - ChoiceField defined with integer option values fails to indicate field state in HTML form output. *Closed via `#4374`.*
 * `#4137` - Improve HTML form rendering of choice fields. *Closed via `#4374`.*
* `#3877` - Improve relation choices limiting (using html_cutoff). *Closed via `#4375`.*
* `#3329` - Improve relation choices limiting. *Closed via `#4375`.*
* `#4122` - Improve HTML form rendering. *Closed via `#4375`.*
* `#3330` - Limits the number of related items added to the choices dictionary on RelatedField. *Closed via `#4375`.*
* `#4372` - DecimalField fails when `max_digits=None`. *Closed via `#4377`.*
* `#4370` - Fix handling of ALLOWED_VERSIONS and no DEFAULT_VERSION. *Accepted & merged.*
* `#4172` - Show Traceback HTML in browsable API. *Accepted & merged.*
* `#4042` - Traceback HTML not shown in browsable API. *Closed via `#4172`.*
* `#3872` - Add failing test for issue #3868. *Closed via `#4378`.*
* `#3868` - Fix resolving var 'value', was missing 'field'. *Closed via `#4378`.*
* `#3365` - choices representation of RelatedField. *Closed via `#4379`.*
* `#4111` - Choice values are always represented as strings. *Closed via `#4379`.*
* `#3985` - RelatedField(required=False) throws KeyError when the data is missing. *Reviewed & closed.*
`#2829` - Patching a field on a model with a ManyToManyField removes the related objects. *Reviewed & closed.*
* `#3394` - CharField should not accept collections as valid input. *Closed via `#4380`.*
* `#3474` - ModelSerializer.is_valid doesn't pass initial_data into validate() method when partial=True. *Reviewed & closed.*
* `#4381` - Update permissions.md. *Accepted & merged.*
* `#4278` - SchemaGenerator doesn't pass request attribute. *Closed via `#4383`.*
* `#4279` - Add failing test case for `#4278`. *Closed via `#4383`.*
* `#4373` - 'ViewSet' object has no attribute 'request' during Schema generation. *Closed via `#4383`.*
* `#4382` - SchemaGenerator does not pass in serializer context. *Closed via `#4383`.*
* `#4376` - Consider including list routes under associated categories when generating CoreAPI schema. *Closed via `#4386`.*
* `#4385` - Allow customization of ObtainAuthToken response. *Reviewed and closed.*
* `#4362` - exclude OPTIONS requests from throttling. *Reviewed and closed.*
* `#4201` - Paginators always repeat the query even if the count is 0. *Closed via `#4388`.*
* `#4389` - Fix comment for SerializerMethodField.bind method. *Accepted & merged.*
* `#4391` - Schema structure is not suitable for detail_route or list_route with multiple methods. *Closed via `#4394`.*
* `#4329` - Schema autogeneration. *Closed via `#4387` and `#4394`*.
* `#4260` - Don't strip empty query params when paginating. *Accepted & merged.*
* `#4392` - Add test to ensure blank parameters are preserved in next link. *Closed via `#4260`.*
* `#4393` - Blank parameters are not passed into `next` field in results. *Closed via `#4260`.*
* `#4403` - Fix template syntax error for `as_list_of_strings`. *Accepted & merged.*
* `#4404` - Docstring of Field.get_default is misleading. *Closed via `785b206`.*
* `#4398` - 'ViewSet' object has no attribute 'action' during Schema generation. *Closed via `#4408`.*
* `#4412` - Replace utf8 character ' with its ascii counterpart, makes bdist_rpm happy on CentOS 7. *Accepted & merged.*
* `#4413` - ObtainAuthToken view doesn't show specific message when the user is disabled. *Reviewed & closed.*
* `#4410` - rest_framework api view not working when CSRF_HEADER_NAME param is not default. *Closed via `#4415`.*
* `#4409` - Tracebacks not printed on console v 3.4.4. *Closed via `#4416`.*
* `#4401` - Schemas should automatically respect API root location. *Reviewed & closed.*
* `#4419` - PKOnlyObject doesn't have __str__/__unicode__ methods. *Closed via `#4423`.*
* `#3508` - Improve Create to show the original exception traceback. *Accepted & merged.*
* `#4427` - Extend @api_view decorator to support custom kwargs which will be set to returned APIView instance.
* `#4428` - Allow api_view setup attrs mentioned explicitly.
* `#4429` - Skip HiddenField from Schema fields. *Accepted & merged.*
* `#4425` - SchemaGenerator add Serializer HiddenFields to parameters. *Closed via `#4429`.*
* `#4432` - Inconsistent behavior when authenticating users. *Reviewed & closed.*
* `#4435` - Missing , in rest_framework/base.html window.drf script. *Closed via commit `97806f9`.*
* `#4430` - DurationField with choices. *Reviewed & accepted.*
* `#4450` - Unauthenticated response. *Reviewed & closed.*
* `#4447` - Improve support for generic relations. *Reviewed & closed.*
* `#4445` - Offline Documentation as PDF. *Reviewed & closed.*
* `#4446` - Not filtering on view queryset nested relations in place of FilterSet model. *Reviewed & closed.*
* `#4451` - Throttling random request code example fix. *Accepted & merged.*
* `#4439` - Unsupported operand type(s) when using IsAuthenticated in Python 2.7 and 3.4. *Reviewed & closed, with follow up in Django ticket #27154.*
* `#4455` - Shorter commands in Quickstart. *Reviewed with feedback.*
* `#4453` - Update ko_KR translation. *Closed & directed to transifex.*
* `#4454` - Introduced Latvian translation. *Closed & directed to transifex.*

### Authored

* `#4338` - Handle non-string input for IP fields.
* `#4339` - Quantize incoming digitals.
* `#4340` - Descriptive error from FileUploadParser when filename not included.
* `#4344` - Update from Django 1.10 beta to Django 1.10.
* `#4346` - Serializer defaults should not be included in partial updates.
* `#4347` - Dedent tabs in docstrings.
* `#4348` - Test cases for DictField with allow_null options.
* `#4349` - extra_kwargs takes precedence over uniqueness kwargs.
* `#4357` - Filter HEAD out from schemas.
* `#4358` - Access `request.user.is_authenticated` as property not method, under Django 1.10+
* `#4359` - Include kwargs passed to 'as_view' when generating schemas.
* `#4371` - Fix call to TemplateHTMLRenderer.resolve_context() fallback method.
* `#4374` - Resolve form display with ChoiceField, MultipleChoiceField and non-string choices.
* `#4375` - Limit queryset when rendering relational choices.
* `#4377` - Allow `max_digits=None` on DecimalField.
* `#4378` - Test case for rendering checkboxes in vertical form style.
* `#4379` - .choices property of RelatedField should preserve non-string values.
* `#4380` - Stricter type validation for CharField.
* `#4383` - Pass request to schema generation.
* `#4386` - Fix schema categories for custom list actions.
* `#4387` - Add form field descriptions to schemas.
* `#4388` - Do not re-run query for empty results with LimitOffsetPagination.
* `#4394` - Fix issue with generating categories for schema endpoints.
* `#4395` - Version 3.4.4.
* `#4407` - Do not include request.FILES items in request.POST.
* `#4408` - Include `.action` attribute on viewsets when generating schemas.
* `#4415` - Allow custom CSRF_HEADER_NAME setting.
* `#4416` - Improve debug error handling.
* `#4423` - Add `__str__` method to `PKOnlyObject`.

## New functionality

I've been working towards the 3.5.0 release, in particular:

* A `requests` test client. Allows you to test your application using the python `requests` library as the client. Interestingly this opens the possibility of writing test cases that can be run either locally, or against a staging or live environment.
* A `coreapi` test client. Allows you to test your application using the `coreapi` client library.
* Client library support for file uploads and downloads.
* 2.0 versions of `coreapi` and `coreapi-cli`.

## Admin

There is now a management site for sponsors to update their sponsorship details:

https://fund.django-rest-framework.org/management/

I've not yet handed out invitations to everyone. Email me if you'd like a login. I expect to be sending out invitations & details later in September.

## Finance

Against a baseline of £48,000/yr revenue (not salary) we're now at somewhere over 90% sustainability.

Reaching the tipping point of sustainability is tremendously important to the long-term success of the project. If your business has not yet signed up for a paid plan, please consider doing so:

https://fund.django-rest-framework.org/topics/funding/

---

As ever, thanks to all our sponsors, contributors, and users for your ongoing support.

&mdash; Tom Christie, 2nd September, 2016.
