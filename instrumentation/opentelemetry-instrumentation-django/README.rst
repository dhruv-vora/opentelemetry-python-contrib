OpenTelemetry Django Tracing
============================

|pypi|

.. |pypi| image:: https://badge.fury.io/py/opentelemetry-instrumentation-django.svg
   :target: https://pypi.org/project/opentelemetry-instrumentation-django/

This library allows tracing requests for Django applications.

Installation
------------

::

    pip install opentelemetry-instrumentation-django

Configuration
-------------

Exclude lists
*************
To exclude certain URLs from being tracked, set the environment variable ``OTEL_PYTHON_DJANGO_EXCLUDED_URLS`` with comma delimited regexes representing which URLs to exclude.

For example,

::

    export OTEL_PYTHON_DJANGO_EXCLUDED_URLS="client/.*/info,healthcheck"

will exclude requests such as ``https://site/client/123/info`` and ``https://site/xyz/healthcheck``.

Request attributes
********************
To extract certain attributes from Django's request object and use them as span attributes, set the environment variable ``OTEL_PYTHON_DJANGO_TRACED_REQUEST_ATTRS`` to a comma
delimited list of request attribute names. 

For example,

::

    export OTEL_PYTHON_DJANGO_TRACED_REQUEST_ATTRS='path_info,content_type'

will extract path_info and content_type attributes from every traced request and add them as span attritbues.

Django Request object reference: https://docs.djangoproject.com/en/3.1/ref/request-response/#attributes

Request and Response hooks
***************************
The instrumentation supports specifying request and response hooks. These are functions that get called back by the instrumentation right after a Span is created for a request
and right before the span is finished while processing a response. The hooks can be configured as follows:

::

    def request_hook(span, request):
        pass

    def response_hook(span, request, response):
        pass

    DjangoInstrumentation().instrument(request_hook=request_hook, response_hook=response_hook)


References
----------

* `Django <https://www.djangoproject.com/>`_
* `OpenTelemetry Instrumentation for Django <https://opentelemetry-python-contrib.readthedocs.io/en/latest/instrumentation/django/django.html>`_
* `OpenTelemetry Project <https://opentelemetry.io/>`_
