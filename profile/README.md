# MCPG

An MCP gateway and its ecosystem: the `mcpg` gateway, plugins, SDKs, a
Kubernetes operator, Helm charts, and infrastructure-as-code.

**Website and documentation:** https://mcpg.dev

**Install the CLI suite** (`mcpg`, `mcpg-config`, `mcpg-cloud`, `mcpg-plugin`):

```sh
npx model-context-protocol-gateway --help      # npm
uvx model-context-protocol-gateway --help      # PyPI
cargo install model-context-protocol-gateway --version <version>   # crates.io
```

## About these repositories

- **Issues are welcome** on each repository.
- **Pull requests are not accepted (yet)** — development happens upstream
  and flows out through releases.
- **Releases are tags.** Rust crates are consumed by git reference:
  `{ git = "https://github.com/mcpg-dev/<crate>", tag = "v<version>" }`.
  The one crate on crates.io, `model-context-protocol-gateway`, installs the
  CLI suite's release binaries.
