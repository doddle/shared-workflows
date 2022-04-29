shared-workflows
================

Stores generic workflows to simplify gitflow releases that we uses in our organisation

Example pipeline to draft a release
```yaml
name: draft release

on:
  workflow_dispatch:
    inputs:
      semver:
        type: choice
        description: Type of semver release your doing
        options:
        - patch
        - minor
        - major
        required: true

jobs:
  call-workflow-passing-data:
    uses: doddle/shared-workflows/.github/workflows/reusable-draft-new-release-workflow.yml@master
    with:
      semver: ${{ github.event.inputs.semver }}
    secrets:
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```

Example pipeline to publish a release
```yaml
name: publish release

on:
  pull_request:
    branches:
      - master
    types:
      - closed

jobs:
  call-workflow-passing-data:
    uses: doddle/shared-workflows/.github/workflows/reusable-publish-new-release-workflow.yml@master
    secrets:
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```