# actions-python

This action is used to publish a python package to aws codeartifact.

## Test usage

```yaml
name: Test

on:
  pull_request

concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: true

jobs:
  test:
    uses: kraussmaffei/actions-python/.github/workflows/test.yml@main
    with:
      python-version: <python-version>
      python-package-path: $(echo ${GITHUB_REPOSITORY##*/} | tr -s '-' '_')
    secrets:
      pip-index-url: <pip-index-url>
      pip-extra-index-url: <pip-extra-index-url>
      user-token: <user-token>
      sonar-token: <sonar-token>
```

## Test and publish usage

```yaml
name: Test and publish library

on:
  push:
    branches: ["main"]

concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: false

jobs:
  publish-python-package:
    uses: kraussmaffei/actions-python/.github/workflows/test-and-publish.yml@main
    with:
      python-version: <python-version>
      python-package-path: $(echo ${GITHUB_REPOSITORY##*/} | tr -s '-' '_')
      aws-account-id: <aws-account-id>
      codeartifact-repository: <codeartifact-repository>
    secrets:
      pip-index-url: <pip-index-url>
      pip-extra-index-url: <pip-extra-index-url>
      user-token: <user-token>
      sonar-token: <sonar-token>
```

## Publish usage

Currently not intended to use. Use [Test and publish usage](#Test-and-publish-usage) instead

```yaml
name: Publish library

on:
  push:
    branches: ["main"]

concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: false

jobs:
  publish-python-package:
    uses: kraussmaffei/actions-python/.github/workflows/publish.yml@main
    with:
      python-version: <python-version>
      aws-account-id: <aws-account-id>
      codeartifact-repository: <codeartifact-repository>
    secrets:
      pip-index-url: <pip-index-url>
      pip-extra-index-url: <pip-extra-index-url>
      user-token: <user-token>
```
