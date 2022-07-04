shared-workflows
================

Stores generic workflows to simplify gitflow releases that we uses in our organisation

## How to use

- In the root of the repository, create a directory called `.github/workflows`
- In that directory, create a file called `draft-release.yml`
- In that file, copy the content of the following:

```yaml
name: draft release

on:
  workflow_dispatch:
    inputs:
      semver:
        type: choice
        description: "Semantic version to draft"
        options:
        - patch
        - minor
        - major
        required: true

jobs:
  draft-release:
    uses: doddle/shared-workflows/.github/workflows/reusable-draft-new-release-workflow.yml@1.x
    with:
      semver: ${{ github.event.inputs.semver }}
    secrets:
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```

- In that directory, create a file called `publish-release.yml`
- In that file, copy the content of the following:

```yaml
name: publish release

on:
  pull_request:
    branches:
      - master
    types:
      - closed

jobs:
  publish-release:
    uses: doddle/shared-workflows/.github/workflows/reusable-publish-new-release-workflow.yml@1.x
    secrets:
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```
