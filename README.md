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

### with mkdocs

```shell
mkdocs serve
```

### with docker

```shell
docker run --rm -it -p 8000:8000 -v $(pwd):/docs squidfunk/mkdocs-material
```

## publishing the docs locally

```bash
mkdocs gh-deploy --force
```