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
      note:
        type: string
        description: Note to add to the release
        required: false

jobs:
  draft-release:
    uses: doddle/shared-workflows/.github/workflows/reusable-draft-new-release-workflow.yml@1.x
    with:
      semver: ${{ github.event.inputs.semver }}
      note: ${{ github.event.inputs.note }}
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
  publish-release:
    uses: doddle/shared-workflows/.github/workflows/reusable-publish-new-release-workflow.yml@1.x
    secrets:
      GH_TOKEN: ${{ secrets.GH_TOKEN }}
```
