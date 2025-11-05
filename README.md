# goreleaser-rust-workflow

A GitHub Action to build and release Rust projects using [GoReleaser](https://goreleaser.com/).

## Usage

```yaml
name: Release
on:
  push:
    tags:
      - "v*"
jobs:
  release:
    uses: eeekcct/goreleaser-rust-workflow/.github/workflows/release.yml@v0.1.0
    permissions:
      contents: write
      id-token: write
      actions: read
      attestations: write
```

## Licence

[MIT](./LICENSE)
