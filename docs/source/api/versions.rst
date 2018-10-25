========
Versions
========

The Versions endpoint provides a list of valid Bible Versions. The abbreviations
for these versions are used by the Verse Of The Day APIs, when passing
the `version` parameter.


Get a list of available Bible Versions
======================================

**GET** /versions
~~~~~~~~~~~~~~~~~~~~~~

Example request using CURL:

.. code-block:: text

    curl --request GET \
        --url https://developers.youversionapi.com/1.0/versions \
        --header 'accept: application/json' \
        --header 'referer: https://your-app-url.com/' \
        --header 'x-youversion-developer-token: {your_developer_token}'




Example Response
================

.. code-block:: json

    {
        "data": [
            {
                "version": {
                    "abbreviation": "KJV",
                    "copyright": "Crown Copyright in UK",
                    "title": "King James Version"
                }
            },
            {
                "version": {
                    "abbreviation": "ASV",
                    "copyright": "PUBLIC DOMAIN",
                    "title": "American Standard Version"
                }
            }
        ],
        "next_page": false,
        "page_size": 25
    }


Configuration response properties
=================================

.. list-table::
    :header-rows: 1
    :widths: 10 10 30

    * - Property
      - Type
      - Description
    * - data
      - list of Bible Versions
      - This item is a list of objects representing a particular Bible Version.
        Each version represented here is a valid version for requesting VOTD text.
        The value of the *abbreviation* key can be provided to the *verse_of_the_day*
        or *verse_of_the_day/{day}/* endpoints as the *version* parameter.
    * - next_page
      - boolean
      - Boolean indicating whether a "next page" exists, if results are paginated.
    * - page_size
      - integer
      - Page size of response. How many Verse Of The Day resources are provided for this response.
