# Build legacy Python wheels in a fork

This repository includes a workflow at `.github/workflows/fork-legacy-python-wheels.yml` to build Linux CPU wheels for:

- `cp38-cp38` (Python 3.8)
- `cp39-cp39` (Python 3.9)
- `cp310-cp310` (Python 3.10)

Note: the workflow overrides the Docker base image to public `quay.io/pypa/manylinux_2_28_x86_64`, so it works in forks without Microsoft-internal registry access.

## Run manually

1. Open **Actions** in your fork.
2. Run **Fork Legacy Python Wheels** (`workflow_dispatch`).
3. Download wheel files from workflow artifacts.

## Auto publish to GitHub Release

Push a tag matching `fork-ort-v*`, for example:

```bash
git tag fork-ort-v1.22.0-py38-py310
git push origin fork-ort-v1.22.0-py38-py310
```

The workflow will upload wheels and create/update a GitHub Release for that tag.

## Python version marker in package metadata

`setup.py` now reads `ORT_PYTHON_REQUIRES` (default: `>=3.10`).

The legacy wheel workflow sets:

```bash
ORT_PYTHON_REQUIRES=>=3.8
```

so built fork wheels can be installed by Python 3.8+.
