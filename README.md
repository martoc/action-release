[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# action-release

A GitHub Action that creates a GitHub release and optionally uploads binary files to it. Simplifies the CI/CD workflow by automating the release process.

## Features

- Automatic GitHub release creation
- Optional binary file uploads from `target/builds/`
- Skip release on pull request events
- Uses GitHub API for release creation

## Quick Start

```yaml
- name: Tag
  uses: martoc/action-tag@v0

- name: Release
  uses: martoc/action-release@v0
```

## Documentation

- [Usage Guide](./docs/USAGE.md) - Detailed usage instructions and examples
- [Code Style](./docs/CODESTYLE.md) - Code style guidelines for contributors

## Environment Variables

| Variable | Description |
|----------|-------------|
| `TAG_NAME` | Tag name for the release (required) |
| `BIN_NAMES` | Space-separated list of binaries to upload from `target/builds/` |

## Permissions

The action requires the following permissions:

```yaml
permissions:
  contents: write
```

## Licence

This project is licenced under the MIT Licence - see the [LICENCE](LICENSE) file for details.
