# OpenSequenceDiagrams Core

WebSequenceDiagrams-compatible sequence diagram parser and SVG renderer built with Rust and WebAssembly.

## Project Structure

```
opensequencediagrams-core/
├── osd-core/     # Rust parser + SVG renderer
├── osd-wasm/     # WebAssembly bindings
├── osd-js/       # npm package output
└── .github/      # GitHub Actions workflows
```

## Development

### Prerequisites

- Rust 1.70+
- wasm-pack (`cargo install wasm-pack`)

### Build

```bash
# Build Rust library
cargo build

# Run tests
cargo test

# Build WASM
cd osd-wasm
wasm-pack build --target web --out-dir ../osd-js/pkg
```

## npm Package

- Package name: `@guide-inc-org/opensequencediagrams-core`
- npm: https://www.npmjs.com/package/@guide-inc-org/opensequencediagrams-core

### Installation

```bash
npm install @guide-inc-org/opensequencediagrams-core
```

### Usage

```javascript
import init, { render } from '@guide-inc-org/opensequencediagrams-core';

await init();
const svg = render('Alice->Bob: Hello');
```

## Release Process

Releases are automated via GitHub Actions. To publish a new version:

1. Update version in `osd-wasm/Cargo.toml` if needed
2. Create and push a version tag:

```bash
git tag v0.2.0
git push origin v0.2.0
```

The `publish.yml` workflow will automatically:
- Build WASM with wasm-pack
- Update package.json with the tag version
- Publish to npm

### GitHub Secrets

The following secret is configured for npm publishing:
- `NPM_TOKEN`: npm granular access token for `@guide-inc-org` scope

## CI/CD

### Workflows

| Workflow | Trigger | Description |
|----------|---------|-------------|
| `ci.yml` | push/PR to main | Run tests, format check, clippy |
| `publish.yml` | tag `v*` push | Build WASM and publish to npm |
