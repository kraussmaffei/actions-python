# km-reusable-workflows

This is the repo where our reusable workflows are stored to.

## Python quality tasks usage

```yaml
name: Continuous Integration

on:
  push:
    branches: ["main"]
  pull_request:
    branches: ["main"]

concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: false

jobs:
  python-quality-tasks:
    uses: kraussmaffei/actions-python/.github/workflows/quality-tasks.yml@main
    with:
      python-version: "3.8"
      python-package-path: $(echo ${GITHUB_REPOSITORY##*/} | tr -s '-' '_')
    secrets:
      pip-index-url: <pip-index-url>
      pip-extra-index-url: <pip-extra-index-url>
      user-token: <user-token>
      sonar-token: <sonarcloud-token>
```

## Build and push usage

```yaml
name: Continuous Integration

on:
  push:
    branches: ["main"]
  pull_request:
    branches: ["main"]

concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: false

jobs:
  publish-python-package:
    needs: [python-quality-tasks]
    uses: kraussmaffei/actions-python/.github/workflows/build-and-publish.yml@main
    with:
      python-version: "3.8"
      aws-account-id: <account-id-to-use>
      aws-region: <region-to-use>
      codeartifact-domain: <your-codeartifact-domain>
      codeartifact-repository: <your-codeartifact-rpository>
    secrets:
      pip-index-url: <pip-index-url>
      pip-extra-index-url: <pip-extra-index-url>
      user-token: <user-token>
```
