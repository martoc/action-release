# Usage

## Overview

This GitHub Action creates a GitHub release and optionally uploads binary files to it.
It simplifies the CI/CD workflow by automating the release process.

## Prerequisites

### Secrets Configuration

Before using this action, ensure that you have the following configured:

* **GITHUB_TOKEN:** Automatically provided by GitHub Actions with `contents: write` permission.

## Environment Variables

The following environment variables are used to customise the release:

| Variable | Description | Required |
|----------|-------------|----------|
| `TAG_NAME` | The tag name for the release (e.g., `v1.0.0`) | Yes |
| `BIN_NAMES` | Space-separated list of binary file names to upload from `target/builds/` directory | No |

## Example

Here is an example of how to use this GitHub Action to create a release and upload binaries.

```yaml
name: Release

on:
  push:
    branches:
      - main

jobs:
  release:
    permissions:
      contents: write
      id-token: write
    runs-on: ubuntu-24.04
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 50
          fetch-tags: true
      - name: Tag
        uses: martoc/action-tag@v0
      - name: Release
        uses: martoc/action-release@v0
```

### With Binary Uploads

```yaml
name: Release with Binaries

on:
  push:
    branches:
      - main

jobs:
  release:
    permissions:
      contents: write
      id-token: write
    runs-on: ubuntu-24.04
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 50
          fetch-tags: true
      - name: Build
        run: |
          mkdir -p target/builds
          # Build your binaries here
      - name: Tag
        uses: martoc/action-tag@v0
      - name: Release
        uses: martoc/action-release@v0
        env:
          BIN_NAMES: "my-binary-linux-amd64 my-binary-linux-arm64"
```

## Notes

* The action automatically skips release creation for pull request events.
* Binary files must be placed in the `target/builds/` directory.
* The `TAG_NAME` environment variable is typically set by the `martoc/action-tag` action.
