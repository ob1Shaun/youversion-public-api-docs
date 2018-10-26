.. _api-versions:

========
Versions
========

The Versions endpoint provides a list of valid Bible Versions. The abbreviations
for these versions are used by the Verse Of The Day APIs, when passing
the ``version`` parameter.


Get a list of available Bible Versions
======================================

**GET** /versions
~~~~~~~~~~~~~~~~~~~~~~

Example request

.. content-tabs::

    .. tab-container:: curl
        :title: curl

        .. code-block:: text

            curl --request GET \
                --url https://developers.youversionapi.com/1.0/versions \
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

            # TODO


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
