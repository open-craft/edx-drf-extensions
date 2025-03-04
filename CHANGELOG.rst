Change Log
==========

..
   This file loosely adheres to the structure of https://keepachangelog.com/,
   but in reStructuredText instead of Markdown.

   This project adheres to Semantic Versioning (https://semver.org/).

.. There should always be an "Unreleased" section for changes pending release.

Unreleased
----------

[7.0.1] - 2021-08-10
--------------------

Fixed
~~~~~

* Removed dropped ``require_exp`` and ``require_iat`` options from jwt.decode and instead used ``require`` option with both ``exp`` and ``iat``. For more info visit this: https://pyjwt.readthedocs.io/en/stable/changelog.html#dropped-deprecated-require-options-in-jwt-decode
* This fixes an error in previous release which had a multiple breaking changes


[7.0.0] - 2021-08-03
--------------------

Changed
~~~~~~~

* **BREAKING CHANGE:** ``generate_jwt_token``: Now returns string (instead of bytes), and no longer requires decoding. This was to keep consistent with change to ``jwt.encode`` in `pyjwt` upgrade (see below).
* **BREAKING CHANGE:** Upgraded dependency ``pyjwt[crypto]`` to 2.1.0, which introduces its own breaking changes that may affect consumers of this library. Pay careful attention to the 2.0.0 breaking changes documented in https://pyjwt.readthedocs.io/en/stable/changelog.html#v2-0-0.

[6.6.0] - 2021-07-13
--------------------

Added
~~~~~

* Added support for django3.1 and 3.2

[6.5.0] - 2021-02-12
--------------------

Added
~~~~~

* Added a new custom attribute `jwt_auth_failed` to both monitor failures, and to help prepare for future refactors.


[6.4.0] - 2021-01-19
--------------------

Added
~~~~~

* Added a new custom attribute `request_is_staff_or_superuser`

[6.3.0] - 2021-01-12
--------------------

Removed
~~~~~~~~

* Drop support for Python 3.5

[6.2.0] - 2020-08-24
--------------------

Updated
~~~~~~~

* Renamed "custom metric" to "custom attribute" throughout the repo. This was based on a `decision (ADR) captured in edx-django-utils`_.

  * Deprecated RequestMetricsMiddleware due to rename.  Use RequestCustomAttributesMiddleware instead.

.. _`decision (ADR) captured in edx-django-utils`: https://github.com/edx/edx-django-utils/blob/master/edx_django_utils/monitoring/docs/decisions/0002-custom-monitoring-language.rst

[6.1.2] - 2020-07-19
--------------------

Fixed
~~~~~~~

* `_get_user_from_jwt` no longer throws an `UnsupportedMediaType` error for failing to parse "new user" requests.



[6.1.1] - 2020-07-19
--------------------

Fixed
~~~~~~~

* Latest `drf-jwt` is throwing error in case of any other Authorization Header. Fixing that issue in `JwtAuthentication` class.



[6.1.0] - 2020-06-26
--------------------

Changed
~~~~~~~

* Update `drf-jwt` to pull in new allow-list(they called it blacklist) feature.

Added
~~~~~

Fixed
~~~~~



[6.0.0] - 2020-05-05
--------------------

Changed
~~~~~~~

* **BREAKING CHANGE**: Renamed 'request_auth_type' to 'request_auth_type_guess'. This makes it more clear that this metric could report the wrong value in certain cases. This could break dashboards or alerts that relied on this metric.
* **BREAKING CHANGE**: Renamed value `session-or-unknown` to `session-or-other`. This name makes it more clear that it is the method of authentication that is in question, not whether or not the user is authenticated. This could break dashboards or alerts that relied on this metric.

Added
~~~~~

* Added 'jwt-cookie' as new value for 'request_auth_type_guess'.
* Added new 'request_authenticated_user_found_in_middleware' metric. Helps identify for what middleware step the request user was set, if it was set. Example values: 'process_request', 'process_view', 'process_response', or 'process_exception'.

Fixed
~~~~~

* Fixed/Added setting of authentication metrics for exceptions as well.
* Fixed 'request_auth_type_guess' to be more accurate when recording values of 'unauthenticated' and 'no-user'.
