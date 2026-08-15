# Kennel Operations Documentation

This public repository contains the sanitized technical documentation for Kennel Operations, an operational planning and workload system for a Rovaniemi sled-dog kennel.

The application source is maintained separately in a private repository. This repository is a controlled publication copy; the private application repository remains the authoritative documentation source.

## Documentation site

The documentation is built with MkDocs and Material for MkDocs:

<https://oshaltaev-1995.github.io/kenneloperations-docs/>

## Local build

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
mkdocs build --strict
```

The current documented production release is `e55bf50e38da6a343a73db2c3825149c0e1eb64d`, deployed on 2026-08-15.

Documentation updates are published explicitly from the reviewed, sanitized source set. No cross-repository credential or automatic source-sync mechanism is used.
