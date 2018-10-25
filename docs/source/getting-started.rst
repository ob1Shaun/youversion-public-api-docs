===============
Getting Started
===============


Base URL
========

Unless otherwise noted, all URLs referenced in this documentation have the following base:

    https://developers.youversion.com/api/1.0

Our APIs are served over HTTPS. Unencrypted HTTP connections are not supported.


Authentication
==============

Requests are authenticated by sending along a YouVersion API Developer Token.

That token is sent as a request header ``X-YouVersion-Developer-Token``, the value of which is provided in the YouVersion API Developers Portal.

In addition to that token, our API endpoints expect a couple **required** headers
to be sent along with the request. Currently, those are:

- ``accept``: Presently we'll be responding to public APIs with JSON, so the valid value here is ``application/json``.
- ``referer``: A "referer" value is required. Ideally, this is the URL of the app or website that is making the request.

For example, here's what a CURL request might look like for getting the Verse Of The Day for the first day of the year:

.. code-block:: text

    curl --request GET \
        --url https://developers.youversionapi.com/1.0/verse_of_the_day/1 \
        --header 'accept: application/json' \
        --header 'referer: https://your-app-url.com/' \
        --header 'x-youversion-developer-token: {your_developer_token}'


Getting an API Token
====================

TODO: Walkthrough. Where and how?

Visit the YouVersion API Developers Portal: https://developers.youversion.com


Applications built with YouVersion Public APIs
==============================================

None yet! Want yours listed here?


Help Integrating the API
========================

This is currently a YouVersion "Ship-It Week" project, and you're welcome to
ask questions and provide feedback via our Slack channel, `#yv-votd-api`, in
the Open Digerati Slack Team https://opendigerati.slack.com/

You can get an invite to Open Digerati Slack by visiting the home page (https://opendigerati.com/)
and following the "Slack" link in the main menu.
