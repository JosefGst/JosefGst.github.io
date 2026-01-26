# JosefGst.github.io

Welcome :wave: to my personal web-page. [Click me!](https://josefgst.github.io/) :smile:

Heavily inspired by [knmcguire](https://github.com/knmcguire/knmcguire.github.io/tree/main)

## Dependencies
```
pip install pre-commit
npm install -g markdown-link-check
```

## Development
### Install dependencies
```bash
uv venv .venv
uv sync
```
### Source virtual environment
```bash
source .venv/bin/activate
```

### Run locally
```bash
mkdocs serve
```

### Run pre-commit checks
```bash
pre-commit run --all-files
```

## Install the git hook scripts

    pre-commit install  # (runs every time you commit in git)

## To update this file:

    pre-commit autoupdate
