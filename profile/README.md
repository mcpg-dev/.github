# MCPG

An MCP gateway and its ecosystem: the `mcpg` gateway, plugins, SDKs, a
Kubernetes operator, Helm charts, and infrastructure-as-code.

**Website and documentation:** https://mcpg.dev

## About these repositories

Every repository in this organization is a one-way mirror of a private
monorepo, published per project:

- **Issues are welcome** on each repository.
- **Pull requests are not accepted (yet)** — code changes happen upstream
  and flow out through releases.
- **Releases are tags.** Rust crates are consumed by git reference:
  `{ git = "https://github.com/mcpg-dev/<crate>", tag = "v<version>" }`.
