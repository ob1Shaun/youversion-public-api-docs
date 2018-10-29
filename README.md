# YouVersion Public API Docs (source)

This project contains the Sphinx-generated documentation to describe our
publicly available APIs.

The live version of this documentation is currently hosted at: https://yv-public-api-docs-draft.netlify.com/

## How to modify and work on the docs

### Set up

- Clone this repo!
- Run `pipenv install` to get Sphinx and build dependencies installed.

### Modify or create some content

The all the documentation is in the `docs/` directory. We build it with
Sphinx (http://www.sphinx-doc.org/), using reStructuredText formatting (http://www.sphinx-doc.org/en/master/usage/restructuredtext/basics.html).

### Build and view the docs locally

- Run `make html` from the project root (builds docs into `docs/build/html/`)

To view the docs, you can find the `index.html` file in the
build output directory. To make sure everything behaves like
it will on the web, I like to run a local web server from
that directory.

Like this:

- `cd docs/build/html/`
- and `python -m http.server 8000` (assuming Python 3+)
- open browser to `http://0.0.0.0:8000/`
- See docs!

### Other details

This project uses the 'contentui' extension for Sphinx, to lay out the
code snippets in a tabbed UI. It enables a new directive that looks like this:

```rst
.. content-tabs::

    .. tab-container::
        :title: Tab 1

        This content is shown when "Tab 1" is the selected tab.

    .. tab-container::
        :title: Tab 2

        This content is shown when "Tab 1" is the selected tab.
```

See their docs for more info: https://sphinxcontrib-contentui.readthedocs.io/en/latest/index.html

## License

See the `LICENSE` file in this repository.