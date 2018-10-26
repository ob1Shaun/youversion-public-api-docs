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

Example request using CURL:

.. code-block:: text
    :caption: Get the VOTD for the first day of the year

    curl --request GET \
        --url https://developers.youversionapi.com/1.0/verse_of_the_day/1 \
        --header 'accept: application/json' \
        --header 'referer: https://your-app-url.com/' \
        --header 'x-youversion-developer-token: {your_developer_token}'


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

Example request using CURL:

.. code-block:: text
    :caption: Get all current VOTD content for the whole year

    curl --request GET \
        --url https://developers.youversionapi.com/1.0/verse_of_the_day/ \
        --header 'accept: application/json' \
        --header 'referer: https://your-app-url.com/' \
        --header 'x-youversion-developer-token: {your_developer_token}'


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

TODO


.. _api-votd-images:

Verse Of The Day Images
=======================

TODO
