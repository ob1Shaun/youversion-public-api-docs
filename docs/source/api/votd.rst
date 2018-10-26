.. _api-votd:


================
Verse Of The Day
================

Get YouVersion Verse Of The Day content for display in your own website or app!

.. image:: votd-example.png
    :width: 100%
    :alt: example display
    :align: center


.. _api-votd-get-single:

Get a single Verse Of The Day item
==================================

**GET** /verse_of_the_day/{int: day_of_year}
--------------------------------------------

Example request


.. content-tabs::

    .. tab-container:: curl
        :title: curl

        .. code-block:: text
            :caption: Get the VOTD for the first day of the year

            curl --request GET \
                --url https://developers.youversionapi.com/1.0/verse_of_the_day/1 \
                --header 'accept: application/json' \
                --header 'referer: https://your-app-url.com/' \
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
            YOUVERSION_DEVELOPER_TOKEN = os.environ['YOUVERSION_DEVELOPER_TOKEN']

            headers = {
                'accept': "application/json",
                "referer": "https://your-app-url.com/",
                "x-youversion-developer-token": YOUVERSION_DEVELOPER_TOKEN,
                "accept-language": "de"
            }
            response = requests.get(
                "https://developers.youversionapistaging.com/1.0/verse_of_the_day/1",
                headers=headers
            )






Query Parameters
~~~~~~~~~~~~~~~~

.. list-table::
    :header-rows: 1
    :widths: 10 30

    * - Param
      - Description
    * - fields
      - Optional. A comma separated list of fields to return. Default is `*` (all fields).
    * - version
      - Optional. The :doc:`Bible Version <versions>` abbreviation that you want the content returned in. See the :doc:`Configuration <configuration>` endpoint for valid options.


Request Headers
~~~~~~~~~~~~~~~

.. list-table::
    :header-rows: 1
    :widths: 50 50

    * - Header
      - Description
    * - `X-YouVersion-Developer-Token`
      - **Required**. Authentication token.

        See Getting Started section for how to get a token.


Example Response
~~~~~~~~~~~~~~~~

.. code-block:: json

    {
        "day": 1,
        "image": {
            "attribution": "YouVersion",
            "id": 42
        },
        "verse": {
            "html": null,
            "human_reference": "John 3:16",
            "text": "For God so loved the world, that he gave his only begotten Son, that whosoever believeth in him should not perish, but have everlasting life.",
            "url": "https://www.bible.com/bible/1/JHN.3.16",
            "usfms": [
                "JHN.3.16"
            ]
        },
    }


.. _api-votd-get-multiple:

Get many Verse Of The Day items
===============================

It's possible to page through the Verse Of The Day items, getting multiple "days"
at a time. Some apps might do this to precache several days at a time, to prevent
having to request the Verse Of The Day on startup, for example.


.. tip::

    One caveat worth mentioning: For various reasons, we use a single "rolling calendar" of 366 total "days".
    That means we assign verses to "Day 1" or "Day 50" instead of "January 1st" or "February 19th".

    We can provide more details soon, but here's what this means in the short term: "the past is subject to change".
    More specifically, in the later half of a given year, we usually begin rolling out changes for *next years* VOTD.
    Those changes will start showing up in days `1` through `180`, for example.
    Because that's the beginning of the *next year*.

    "Today", and usually 30 days into the past or future *should* remain stable at all times.
    Going further in either direction, and the space-time continuum starts to get a little weird.


**GET** /verse_of_the_day
--------------------------------------------

Example request

.. content-tabs::

    .. tab-container:: curl
        :title: curl

        .. code-block:: text
            :caption: Get all current VOTD content for the whole year

            curl --request GET \
                --url https://developers.youversionapi.com/1.0/verse_of_the_day/ \
                --header 'accept: application/json' \
                --header 'referer: https://your-app-url.com/' \
                --header 'x-youversion-developer-token: {your_developer_token}'

    .. tab-container:: js
        :title: javascript

        TODO

    .. tab-container:: node
        :title: node

        TODO

    .. tab-container:: python
        :title: python

        TODO


Query Parameters
~~~~~~~~~~~~~~~~

.. list-table::
    :header-rows: 1
    :widths: 10 30

    * - Param
      - Description
    * - fields
      - Optional. A comma separated list of fields to return. Default is `*` (all fields).
    * - page
      - Optional. Integer, representing the page number of results to return. Defaults to `1`.
    * - page_size
      - Optional. Integer representing "size of page", for pagination purposes. How many items to return per page.
    * - version
      - Optional. The :doc:`Bible Version <versions>` abbreviation that you want the content returned in. See the :doc:`Configuration <configuration>` endpoint for valid options.


Request Headers
~~~~~~~~~~~~~~~

.. list-table::
    :header-rows: 1
    :widths: 50 50

    * - Header
      - Description
    * - `X-YouVersion-Developer-Token`
      - **Required**. Authentication token.

        See :ref:`getting-started` section for how to get a token.


Response Properties
~~~~~~~~~~~~~~~~~~~

.. list-table::
    :header-rows: 1
    :widths: 10 10 30

    * - Property
      - Type
      - Description
    * - data
      - array
      - List of VOTD objects. See the Verse Of The Day resource examples for details of what it contains.
    * - next_page
      - boolean
      - Boolean indicating whether a "next page" exists, if results are paginated.
    * - page_size
      - integer
      - Page size of response. How many Verse Of The Day resources are provided for this response.


Example Response
~~~~~~~~~~~~~~~~

.. code-block:: json

    {
        "data": [
            {
                "day": 1,
                "image": {
                    "attribution": "YouVersion",
                    "id": 42
                },
                "verse": {
                    "html": null,
                    "human_reference": "John 3:16",
                    "text": "For God so loved the world, that he gave his only begotten Son, that whosoever believeth in him should not perish, but have everlasting life.",
                    "url": "https://www.bible.com/bible/1/JHN.3.16.KJV",
                    "usfms": [
                        "JHN.3.16"
                    ]
                }
            },
            {
                "day": 2,
                "image": {
                    "attribution": "YouVersion",
                    "id": 44
                },
                "verse": {
                    "html": null,
                    "human_reference": "Galatians 5:22",
                    "text": "But the fruit of the Spirit is love, joy, peace, longsuffering, gentleness, goodness, faith,",
                    "url": "https://www.bible.com/bible/1/GAL.5.22.KJV",
                    "usfms": [
                        "GAL.5.22"
                    ]
                }
            }
        ],
        "next_page": true,
        "page_size": 2
    }


.. _api-votd-bible-version:

Specifying Bible Version
========================

If you'd like to retrieve VOTD with text from a specific Bible version, you can
pass an optional ``version`` query parameter with your request.
The list of valid values for ``version`` are available from the
:doc:`versions` endpoint.

Here's an example request for a single VOTD, in the King James Version:

.. content-tabs::

    .. tab-container:: curl
        :title: curl

        .. code-block:: text

            curl --request GET \
                --url 'https://developers.youversionapistaging.com/1.0/verse_of_the_day/1?version=kjv' \
                --header 'accept: application/json' \
                --header 'referer: https://your-app-url.com/' \
                --header 'x-youversion-developer-token: {your_developer_token}'

    .. tab-container:: js
        :title: javascript

        TODO

    .. tab-container:: node
        :title: node

        TODO

    .. tab-container:: python
        :title: python

        TODO

.. _api-votd-languages:

Languages and default Versions
------------------------------

.. note::

    Some of the bahavior described here is still Work In Progress, and
    may not be 100% accurate.

YouVersion APIs maintain a list of default Bible Versions for many languages,
for use when language information is included in the request, but a Version was
not specified.

This allows us to do our best to honor the ``Accept-Language`` header from
browsers and other API clients, and send something that most likely matches
the end users' language and expectations.

If you send the optional ``Accept-Language`` header with your request, on a
VOTD endpoint, **and** you don't specify a value for the ``version``
query parameter, we'll try to send content back in a version that makes sense.

Here's an example of a request that specifies a language, but no version:

.. content-tabs::

    .. tab-container:: curl
        :title: curl

        .. code-block:: text

            curl --request GET \
                --url 'https://developers.youversionapistaging.com/1.0/verse_of_the_day/1' \
                --header 'accept: application/json' \
                --header 'referer: https://your-app-url.com/' \
                --header 'x-youversion-developer-token: {your_developer_token}'
                --header 'accept-language: de'


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

            # TODO


Response:

.. code-block:: json

    {}

TODO


.. _api-votd-images:

Verse Of The Day Images
=======================

You may notice that each Verse Of The Day Resource is returned with an
``image`` property, containing an ``attribution`` and an ``id``.

.. note::

    This is a work in progress. For a glimpse at what you might be working
    with, see: :ref:`configuration-response`


.. note::

    Note: The URL returned in **verse_of_the_day_images_base_url** will provide some values for you to replace.

    - **{width}** and **{height}** : should be replaced with integers, each with a max of `1280`. Because our VOTD images are currently square, 1:1 size ratio, the
      image CDN with automatically crop the square to the smallest size you provide here. For the time, it's best and most consistent for these integers to be the same.
    - **{image_id}**: An integer representing the VOTD image you want to display. This value is provided on the Verse Of The Day Resource, as the `id` property on the `image` object property.


.. attention::

    You may notice the URL returned in **verse_of_the_day_images_base_url**  is prefixed with an "image-proxy" CDN URL.

    For performance and caching, you'll want to use the full URL provided, replacing just the template variables. Utilizing just the S3/other location directly will result in unnecessary increase in load times, and larger image sizes.
