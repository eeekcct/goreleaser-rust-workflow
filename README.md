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
      license_check: true
      goreleaser_timeout_minutes: 60
      # optional
      # third_party_licenses_dir: third_party_licenses
      # third_party_licenses_format: yaml
      # deny_toml_path: deny.toml
    permissions:
      contents: write
      id-token: write
      actions: read
      attestations: write
```

## Enforce license policy with cargo-deny

Set `license_check: true` to run `cargo deny check licenses` before GoReleaser.
When enabled, the caller repository must contain `deny.toml` (or a custom path via
`deny_toml_path`).

Example `deny.toml`:

```toml
[licenses]
allow = [
  "MIT",
  "Apache-2.0",
  "BSD-2-Clause",
  "BSD-3-Clause",
  "ISC",
  "Zlib",
]
confidence-threshold = 0.8
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
`goreleaser_timeout_minutes` defaults to `60`.

## Licence

[MIT](./LICENSE)
