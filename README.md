# docs

📝 documentation repository for gaia

## pre-requisites

We use [mkdocs](https://www.mkdocs.org/) to build the documentation as a static website, from markdown files.
The theme used is [mkdocs-material](https://squidfunk.github.io/mkdocs-material/).

See [mkdocs-material documentation](https://squidfunk.github.io/mkdocs-material/getting-started/) for installation instruction.

```bash
pip3 install mkdocs-material
```

## serving the documentation locally

```bash
mkdocs serve
```

## publishing the docs locally

```bash
mkdocs gh-deploy
```