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
    with:
      third_party_licenses: true
      # optional
      # third_party_licenses_dir: third_party_licenses
      # third_party_licenses_format: yaml
    permissions:
      contents: write
      id-token: write
      actions: read
      attestations: write
```

## Include third-party licenses in release archives

This workflow can generate third-party licenses before running GoReleaser, similar to the
approach used in `go-release-workflow`.

To include the generated files in release archives, configure your project `.goreleaser.yml`:

```yaml
archives:
  - files:
      - LICENSE*
      - third_party_licenses/**/*
```

`third_party_licenses_format` supports `yaml`, `json`, and `toml`.

## Licence

[MIT](./LICENSE)
