# IMOS Documentation

This repository contains the documentation for IMOS (Interactive Model Operating System).

## Building the Documentation

The documentation is built using [MkDocs](https://www.mkdocs.org/) with the [Material theme](https://squidfunk.github.io/mkdocs-material/).

### Prerequisites

- Python 3.x
- pip

### Setup

Install the required dependencies:

```bash
pip install mkdocs mkdocs-material
```

### Local Development

To preview the documentation locally:

```bash
mkdocs serve
```

Then open your browser to `http://127.0.0.1:8000/`

### Building

To build the static site:

```bash
mkdocs build
```

The built site will be in the `site/` directory.

### Deployment

To deploy to GitHub Pages:

```bash
mkdocs gh-deploy
```

## Contributing

Contributions to improve the documentation are welcome! Please submit a pull request.
