.. _api-configuration:

=============
Configuration
=============

.. note::

    This API may be removed shortly, as better options are being actively developed.


The "Configuration" endpoint provides default template values,
and shows valid values for some parameters that you can pass to related
API calls.

It will help answer questions that might arise for other endpoints, like:

- What Bible Versions are valid?
- What URL should I use to get a Verse Of The Day image?
- What language tags are valid for an endpoint?


Get the Configuration info
==========================

**GET** /configuration
~~~~~~~~~~~~~~~~~~~~~~

.. tip::

    Remember this is a suffix of our API Base URLs, shown in the Getting Started section.


Example request using CURL:

.. content-tabs::

    .. tab-container:: curl
        :title: curl

        .. code-block:: text

            curl --request GET \
                --url https://developers.youversionapi.com/1.0/configuration \
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
        "verse_of_the_day_bible_versions": [
            {
                "abbreviation": "KJV",
                "copyright": "Crown Copyright in UK",
                "title": "King James Version",
            },
            {
                "abbreviation": "ASV",
                "copyright": null,
                "title": "American Standard Version"
            }
        ],
        "verse_of_the_day_images_language_tags": [
            "af",
            "bg",
            "cs",
            "da",
            "de",
            "en",
            "es",
            "fi",
            "fr",
            "hu",
            "id",
            "it",
            "km",
            "ko",
            "lv",
            "mn",
            "ms",
            "nl",
            "no",
            "pl",
            "pt",
            "ro",
            "ru",
            "sk",
            "sq",
            "sv",
            "sw",
            "tl",
            "tr",
            "uk",
            "vi",
            "zh"
        ],
        "verse_of_the_day_images_base_url": "//imageproxy-cdn.youversionapi.com/{width}x{height}/https://s3.amazonaws.com/static-youversionapi-com/images/base/{image_id}/1280x1280.jpg"
    }


Configuration response properties
=================================

.. list-table::
    :header-rows: 1
    :widths: 10 10 30

    * - Property
      - Type
      - Description
    * - verse_of_the_day_bible_versions
      - list of :doc:`Bible Versions <versions>`
      - This item is a list of objects representing a particular :doc:`Bible Version <versions>`.
        Each version represented here is a valid version for requesting VOTD text.
        The value of the *abbreviation* key can be provided to the :doc:`Verse Of The Day <votd>`
        endpoints as the ``version`` parameter.
    * - verse_of_the_day_images_language_tags
      - list of language tags
      - This is a list of language tags that are valid for passing to the :doc:`VOTD <votd>` endpoints, when specifying an Accept-Language header on the request.
    * - verse_of_the_day_images_base_url
      - string
      - This is a template URL for retrieving :ref:`VOTD images <api-votd-images>`. See those docs, and the note below.

.. note::

    Note: The URL returned in **verse_of_the_day_images_base_url** will provide some values for you to replace.

    - **{width}** and **{height}** : should be replaced with integers, each with a max of `1280`. Because our VOTD images are currently square, 1:1 size ratio, the
      image CDN with automatically crop the square to the smallest size you provide here. For the time, it's best and most consistent for these integers to be the same.
    - **{image_id}**: An integer representing the VOTD image you want to display. This value is provided on the Verse Of The Day Resource, as the `id` property on the `image` object property.


.. attention::

    You may notice the URL returned in **verse_of_the_day_images_base_url**  is prefixed with an "image-proxy" CDN URL.

    For performance and caching, you'll want to use the full URL provided, replacing just the template variables. Utilizing just the S3/other location directly will result in unnecessary increase in load times, and larger image sizes.
