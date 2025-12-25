# OpenEV Data Documentation

Welcome to the repository for the website that holds the documentation of OpenEV Data. This site is built using MkDocs, a static site generator for displaying markdown documentation. If you're looking to make modifications or simply set it up locally, here's what you need to know.

## Prerequisites

* **Python**: 3.13+ is required <https://www.python.org/>
* **Poetry**: Used for consistent dependency management <https://python-poetry.org/>

## Local Setup

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/open-ev-data/open-ev-data.github.io.git && cd open-ev-data.github.io
   ```

2. **Install Dependencies**:
   ```bash
   poetry install
   ```

3. **Serve the Website Locally**:
   ```bash
   poetry run mkdocs serve
   ```
   This will start a local server, and you can access the site at `http://localhost:8000`.

## Making Changes

### Markdown

MkDocs uses Markdown for content. If you're new to Markdown, here's a [quick guide](https://www.markdownguide.org/basic-syntax/).

### Adjusting Site Content

If you want to add a new page, you can create a new markdown file in the `/docs` directory. To make the page visible in the navigation, add it in the `mkdocs.yml` file under the `nav` section. Take a look at the other markdown files for examples. Ideally add some frontmatter for at least the title to stay consistent.

### Customizing Appearance

We use the Material for MkDocs theme. In the file `docs/assets/stylesheets/extra.css` you can find all the customizations and add to them. This file basically overrides the default styling.

## Deployment

This site uses GitHub Actions to publish documentation versions. The deployment is triggered by pushing semantic version tags (e.g., `v1.0.0`).

### Automatic Deployment

When you push a tag with `v*.*.*` format:

```bash
git tag v1.0.0
git push origin v1.0.0
```

The pipeline will:
1. Extract the version (e.g., v1.0.0 → 1.0.x)
2. Deploy documentation with that version
3. Update the `latest` alias
4. Set `latest` as default

### Manual Deployment

You can also trigger deployment manually from the GitHub Actions tab using the "workflow_dispatch" option.

### Versioning

The project uses [mike](https://github.com/jimporter/mike) for documentation versioning:

- **Patch versions** (v1.0.1, v1.0.2) map to the same minor version (1.0.x)
- **Minor versions** (v1.1.0, v1.2.0) create new documentation versions (1.1.x, 1.2.x)
- **Latest** alias always points to the most recent version

Example:
- `v1.0.0`, `v1.0.1`, `v1.0.2` → All deploy to version `1.0.x`
- `v1.1.0` → Creates new version `1.1.x`
- `v2.0.0` → Creates new version `2.0.x`

When the pipeline completes, view the documentation at <https://open-ev-data.github.io>

## About

Open-source documentation for OpenEV Data - the single source of truth for electric vehicle specifications.

## License

This documentation is licensed under CC-BY 4.0.

