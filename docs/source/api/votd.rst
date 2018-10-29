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
                --url https://developers.youversionapi.com/1.0/verse_of_the_day/1?version=kjv \
                --header 'accept: application/json' \
                --header 'x-youversion-developer-token: {your_developer_token}'

    .. tab-container:: js
        :title: javascript

        .. code-block:: javascript

            fetch('https://developers.youversionapi.com/1.0/verse_of_the_day/1?version=kjv', {
                headers: {
                    'X-YouVersion-Developer-Token': '{your_developer_token}',
                    'Accept-Language': 'en',
                    Accept: 'application/json',
                }
            })
            .then((result) => result.json())
            .then((json) => console.log(json))

    .. tab-container:: python
        :title: python

        .. code-block:: python

            import os
            import requests

            # Assuming you keep your tokens in environment variables:
            YOUVERSION_DEVELOPER_TOKEN = os.environ['YOUVERSION_DEVELOPER_TOKEN']

            headers = {
                'accept': "application/json",
                "x-youversion-developer-token": YOUVERSION_DEVELOPER_TOKEN,
                "accept-language": "en"
            }
            response = requests.get(
                "https://developers.youversionapi.com/1.0/verse_of_the_day/1?version=kjv",
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
      - **Required**. The :doc:`Bible Version <versions>` abbreviation that you want the content returned in. See the :doc:`<versions>` endpoint docs for valid options.


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
        "verse": {
            "human_reference": "Isaiah 43:19",
            "usfms": [
                "ISA.43.19"
            ],
            "url": "https://www.bible.com/bible/1/ISA.43.19.KJV",
            "text": "Behold, I will do a new thing; now it shall spring forth; shall ye not know it? I will even make a way in the wilderness, and rivers in the desert.",
            "html": null
        },
        "day": 1,
        "image": {
            "url": "//imageproxy-cdn.youversionapi.com/{width}x{height}/https://s3.amazonaws.com/static-youversionapi-com/images/base/6024/1280x1280.jpg",
            "attribution": "© YouVersion"
        }
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
            --url 'https://developers.youversionapi.com/1.0/verse_of_the_day?version=kjv' \
            --header 'accept: application/json' \
            --header 'x-youversion-developer-token: {your_developer_token}'

    .. tab-container:: js
        :title: javascript

            fetch('https://developers.youversionapi.com/1.0/verse_of_the_day?version=kjv', {
                headers: {
                    'X-YouVersion-Developer-Token': '{your_developer_token}',
                    'Accept-Language': 'en',
                    Accept: 'application/json',
                }
            })
            .then((result) => result.json())
            .then((json) => console.log(json))

    .. tab-container:: python
        :title: python

            import os

            import requests

            # Assuming you keep your tokens in environment variables:
            YOUVERSION_DEVELOPER_TOKEN = os.environ["YOUVERSION_DEVELOPER_TOKEN"]

            headers = {
                "accept": "application/json",
                "x-youversion-developer-token": YOUVERSION_DEVELOPER_TOKEN,
                "accept-language": "en",
            }

            response = requests.get(
                "https://developers.youversionapi.com/1.0/verse_of_the_day?version=kjv",
                headers=headers
            )

            print(response.content)


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
      - **Required**. The :doc:`Bible Version <api/versions>` abbreviation that you want the content returned in. See the :doc:`<versions>` endpoint for valid options.


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
                "verse": {
                    "human_reference": "Isaiah 43:19",
                    "usfms": [
                        "ISA.43.19"
                    ],
                    "url": "https://www.bible.com/bible/1/ISA.43.19.KJV",
                    "text": "Behold, I will do a new thing; now it shall spring forth; shall ye not know it? I will even make a way in the wilderness, and rivers in the desert.",
                    "html": null
                },
                "day": 1,
                "image": {
                    "url": "//imageproxy-cdn.youversionapi.com/{width}x{height}/https://s3.amazonaws.com/static-youversionapi-com/images/base/6024/1280x1280.jpg",
                    "attribution": "© YouVersion"
                }
            },
            {
                "verse": {
                    "human_reference": "Hebrews 13:5",
                    "usfms": [
                        "HEB.13.5"
                    ],
                    "url": "https://www.bible.com/bible/1/HEB.13.5.KJV",
                    "text": "Let your conversation be without covetousness; and be content with such things as ye have: for he hath said, I will never leave thee, nor forsake thee.",
                    "html": null
                },
                "day": 2,
                "image": {
                    "url": "//imageproxy-cdn.youversionapi.com/{width}x{height}/https://s3.amazonaws.com/static-youversionapi-com/images/base/6025/1280x1280.jpg",
                    "attribution": "© YouVersion"
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
pass an the ``version`` query parameter with your request. This param is required,
and our examples thus far have been using ``kjv`` as the value.

The list of valid values for ``version`` are available from the
:doc:`versions` endpoint.

See those docs for accessing that endpoint. We use the Version ``abbreviation``
value to specify the Bible Version for the ``version`` query parameter.

E.g., here's the endpoint URL we've been using to get King James Version text
when requesting Verse Of The Day:

    https://developers.youversionapi.com/1.0/verse_of_the_day/1?**version=kjv**

You could replace the ``kjv`` there with any valid version abbreviation, as
returned by the :doc:`versions` endpoints.


.. _api-votd-images:

Verse Of The Day Images
=======================

You may notice that each Verse Of The Day Resource is returned with an
``image`` property, which contains an ``attribution`` and ``url`` value.

As a reminder, here's a snippet of what that section of the response looks like:

.. code-block:: javascript

    // ...
    "image": {
        "attribution": "© YouVersion",
        "url": "//imageproxy-cdn.youversionapi.com/{width}x{height}/https://s3.amazonaws.com/static-youversionapi-com/images/base/6024/1280x1280.jpg"
    },
    // ...


Image Sizes
-----------

The URL returned in **url** will provide some values for you to replace.

* **{width}** and **{height}** : should be replaced with integers, each with
  a max of ``1280``. Because our VOTD images are currently square (1:1 size ratio)
  the image CDN with automatically crop the square to the smallest size you
  provide here. For the time, it's best and most consistent for these
  integers to be the same.

For example, if you wanted to get the VOTD Image as a 250x250px thumbnail,
you could use the following URL (replacing ``{width}`` and ``{height}`` each with ``250``:

.. code-block:: text

    https://imageproxy-cdn.youversionapi.com/250x250/https://s3.amazonaws.com/static-youversionapi-com/images/base/6024/1280x1280.jpg


Using the Image URL
-------------------

.. attention::

    You may notice the URL returned in **url**  is prefixed with an "image-proxy" CDN URL.

    For performance and caching, you'll want to use the full URL provided,
    replacing just the template variables. Utilizing just the S3/other location
    directly will result in unnecessary increase in load times, and larger
    image sizes.

The URL provided is "schemaless": It has no "http(s):" before the first two
slashes. This is to maintain some backwards compatibility until all existing
platforms were able to transition to HTTPS. (E.g., to prevent
mixed-content warnings on some web pages).

You should almost always be serving content over HTTPS, so you'll usually
just need to prefix the provided value with ``https:``.

E.g., for a 500px square image, this:

    ``//imageproxy-cdn.youversionapi.com/500x500/https://s3.amazonaws.com/static-youversionapi-com/images/base/6024/1280x1280.jpg``

should become this:

    ``https://imageproxy-cdn.youversionapi.com/500x500/https://s3.amazonaws.com/static-youversionapi-com/images/base/6024/1280x1280.jpg``



.. _api-votd-languages:

Languages and Verse Of The Day Images
-------------------------------------

We have a small (but growing!) list of non-English languages for which we
maintain Verse Of The Day Image support.

To retreive an image in a specified language, you can pass the ``Accept-Language``
HTTP header with your request. If an image exists for the specified language,
its URL will be retured in the ``image`` property, in place of the usual
English image URL.

Here's an example request for a Verse Of The Day Image in Spanish:

.. content-tabs::

    .. tab-container:: curl
        :title: curl

        .. code-block:: text

            curl --request GET \
            --url 'https://developers.youversionapi.com/1.0/verse_of_the_day/1?version=kjv' \
            --header 'accept: application/json' \
            --header 'accept-language: es' \
            --header 'x-youversion-developer-token: hfAHdr4Z8NjSqY0JkspC6j0cSPg'

    .. tab-container:: js
        :title: javascript

        .. code-block:: javascript

            fetch('https://developers.youversionapi.com/1.0/verse_of_the_day/1?version=kjv', {
            headers: {
                'X-YouVersion-Developer-Token': '{your_developer_token}',
                Accept: 'application/json',
                'Accept-Language': 'es',
            }
            })
            .then((result) => result.json())
            .then((json) => console.log(json))

    .. tab-container:: python
        :title: python

        .. code-block:: python
            :emphasize-lines: 11

            import os

            import requests

            # Assuming you keep your tokens in environment variables:
            YOUVERSION_DEVELOPER_TOKEN = os.environ["YOUVERSION_DEVELOPER_TOKEN"]

            headers = {
                "accept": "application/json",
                "x-youversion-developer-token": YOUVERSION_DEVELOPER_TOKEN,
                "accept-language": "es",
            }

            response = requests.get(
                "https://developers.youversionapi.com/1.0/verse_of_the_day/1?version=kjv",
                headers=headers
            )

            print(response.content)

.. note::

    The **text** for the Verse Of The Day will always match the requested
    **version** param, regardless of ``Accept-Language`` value.

    ``Accept-Language`` is currently only used here to specify the language
    for the **image** returned with the response.


Valid Langauge Tags
~~~~~~~~~~~~~~~~~~~

Here is a list of valid language tags, and their language titles, for use
requesting alternate Verse Of The Day Images.

.. list-table::
    :header-rows: 1
    :widths: 50 50

    * - Language Name
      - Language Tag (for ``Accept-Language`` header)
    * - Afrikaans
      - af
    * - Chinese, Simplified
      - zh_CN
    * - Chinese, Traditional
      - zh_TW
    * - Dutch
      - nl
    * - English
      - en
    * - French
      - fr
    * - German
      - de
    * - Greek
      - el
    * - Indonesian
      - id
    * - Italian
      - it
    * - Khmer
      - km
    * - Korean
      - ko
    * - Portuguese
      - pt
    * - Romanian
      - ro
    * - Russian
      - ru
    * - Spanish
      - es
    * - Swahili
      - sw
    * - Swedish
      - sv
    * - Tagalog/Filipino
      - tl
    * - Ukrainian
      - uk
    * - Vietnamese
      - vi
    * - Zulu
      - zu

.. note::

    This list is updated as we are
    able to find translation help for our catalog of localizable images. If helping
    with something that sounds interesting to you, check out our
    volunteers information page: https://www.youversion.com/volunteers/