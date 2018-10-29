.. YouVersion Public APIs documentation master file, created by
   sphinx-quickstart on Tue Oct 23 23:00:06 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

==================================================
YouVersion API Documentation
==================================================

👋🏽 Hello, and welcome!

We are so excited and thankful that you are interested in
building tools to help build the Kingdom!

This is the documentation site for our **currently very much in development**
public API's.

In the short term, we're starting with a public Verse Of The Day ("VOTD") API,
so that developers can build and experiment with projects that utilize
that information.


Quick Start: Get the Verse Of The Day!
======================================


Get a YouVersion API Developer Token
------------------------------------

You can get an authorization token, absolutely free, by visiting https://developers.youversion.com.

You can see more about that process and other API details at :ref:`getting-an-api-token`.


Paste your shiny new token into some example code...
----------------------------------------------------

Copy and paste one of the following examples into your platform, or language
of choice! Replace ``{your_developer_token}`` with the token you
copied from the Developer Portal!

.. content-tabs::

    .. tab-container:: curl
        :title: curl

        .. code-block:: text

            curl --request GET \
                --url 'https://developers.youversionapi.com/1.0/verse_of_the_day/1?version=kjv' \
                --header 'accept: application/json' \
                --header 'x-youversion-developer-token: {your_developer_token}'

    .. tab-container:: js
        :title: javascript

        .. code-block:: javascript

            // TODO

    .. tab-container:: node
        :title: node

        .. code-block:: javascript

            // TODO

    .. tab-container:: python
        :title: python

        .. code-block:: python

            import os

            import requests

            # Assuming you keep your tokens in environment variables:
            YOUVERSION_DEVELOPER_TOKEN = os.environ["YOUVERSION_DEVELOPER_TOKEN"]

            headers = {
                "accept": "application/json",
                "x-youversion-developer-token": YOUVERSION_DEVELOPER_TOKEN,
                "accept-language": "de",
            }

            response = requests.get(
                "https://developers.youversionapi.com/1.0/verse_of_the_day/1", headers=headers
            )

            print(response.content)


See the JSON response!
----------------------

You should now see a response that looks like the following:

.. code-block:: json

    {
        "image": {
            "attribution": "© YouVersion",
            "url": "//imageproxy-cdn.youversionapi.com/{width}x{height}/https://s3.amazonaws.com/static-youversionapi-com/images/base/6024/1280x1280.jpg"
        },
        "day": 1,
        "verse": {
            "html": null,
            "human_reference": "Isaiah 43:19",
            "usfms": [
                "ISA.43.19"
            ],
            "url": "https://www.bible.com/bible/1/ISA.43.19.KJV",
            "text": "Behold, I will do a new thing; now it shall spring forth; shall ye not know it? I will even make a way in the wilderness, and rivers in the desert."
        }
    }


That's a JSON formatted response containing the Verse Of The Day
for January 1st!

It even contains a URL for an image!

You can specify the Bible Version you'd like to receive, by specifying
a valid version abbreviation. That's documented here:

We also support images in various languages, documented at: :ref:`api-votd-images`


Build something interesting!
----------------------------

Use your newfound API powers to build something fun or interesting!

The full documentation for the Verse Of The Day API endpoints is at :ref:`api-votd`.

Otherwise, check out :ref:`getting-started` for some first-steps details.


But first?
==========

Before you'll be able to get started using the API's, you'll need to get
an access token to send along with each API request.

That's explained in the :ref:`getting-started` section.

If you already have a token, you can head on over to the API documentation, and
see example requests, responses, and how to interact with the API!


All the Docs So Far
===================

.. toctree::
   :maxdepth: 3
   :caption: Table of Contents:

   getting-started

   api/index


Open Digerati
=============

Curious what else we're doing with Open Source? This project is part of
Open Digerati! You can find out more at https://opendigerati.com/


This Documentation
==================

These docs are open source. Suggestions for improvements (and pull requests) are welcome! You can view the code repository at
https://github.com/lifechurch/youversion-public-api-docs.

They are
built and deployed to https://yv-public-api-docs-draft.netlify.com/
