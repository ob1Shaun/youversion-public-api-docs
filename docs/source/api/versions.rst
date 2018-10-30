========
Versions
========

The Versions endpoint provides a list of valid Bible Versions. The abbreviations
for these versions are used by the Verse Of The Day APIs, when passing
the ``version`` parameter.


Get a list of available Bible Versions
======================================

**GET** /versions
-----------------

Example request

.. content-tabs::

    .. tab-container:: curl
        :title: curl

        .. code-block:: text

            curl --request GET \
                --url https://developers.youversionapi.com/1.0/versions \
                --header 'accept: application/json' \
                --header 'x-youversion-developer-token: {your_developer_token}'

    .. tab-container:: js
        :title: javascript

        .. code-block:: javascript

            fetch('https://developers.youversionapi.com/1.0/versions', {
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
            YOUVERSION_DEVELOPER_TOKEN = os.environ["YOUVERSION_DEVELOPER_TOKEN"]

            headers = {
                "accept": "application/json",
                "x-youversion-developer-token": YOUVERSION_DEVELOPER_TOKEN,
                "accept-language": "en",
            }

            response = requests.get(
                "https://developers.youversionapi.com/1.0/versions",
                headers=headers
            )

            print(response.content)



Example Response
================

.. code-block:: json

    {
        "data": [
            {
                "local_title": "King James Version",
                "local_abbreviation": "KJV",
                "abbreviation": "KJV",
                "title": "King James Version",
                "id": 1,
                "copyright_short": "Crown Copyright in UK"
            },
            {
                "local_title": "American Standard Version",
                "local_abbreviation": "ASV",
                "abbreviation": "ASV",
                "title": "American Standard Version",
                "id": 12,
                "copyright_short": "PUBLIC DOMAIN"
            }
        ],
        "next_page": false,
        "page_size": 25
    }


Versions response properties
============================

.. list-table::
    :header-rows: 1
    :widths: 10 10 30

    * - Property
      - Type
      - Description
    * - data
      - list of :doc:`Bible Versions <versions>`
      - This item is a list of objects representing a particular :doc:`Bible Version <versions>`.
        Each version represented here is a valid version for requesting VOTD text.
        The value of the *abbreviation* key can be provided to the :doc:`Verse Of The Day <votd>`
        endpoints as the ``version`` parameter.
    * - next_page
      - boolean
      - Boolean indicating whether a "next page" exists, if results are paginated.
    * - page_size
      - integer
      - Page size of response. How many Verse Of The Day resources are provided for this response.


Bible Version object properties
-------------------------------

.. list-table::
    :header-rows: 1
    :widths: 10 10 50

    * - Property
      - Type
      - Description
    * - local_title
      - string
      - TODO
    * - local_abbreviation
      - string
      - TODO
    * - abbreviation
      - string
      - TODO
    * - title
      - string
      - TODO
    * - id
      - integer
      - This value is used for getting information about a single Bible Version,
        or for passing to endpoints that accept a specified version. E.g.,
        the ``version_id`` parameter on calls for :doc:`votd` expect this value.
    * - copyright_short
      - string
      - TODO