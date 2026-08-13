# mcpg-dev/.github

Organization defaults and the shared release workflow for the `mcpg-dev`
repositories: the org profile (`profile/README.md`) plus the reusable
workflows that every repository's release shim calls at the moving `v1`
tag.

Each repository carries a small `release.yml` shim that fires on its
`v{version}` release tag and calls `.github/workflows/release.yml@v1`
here with its tier:

| tier | repos | produces |
|---|---|---|
| `lib` | Rust libraries | verify (build/test/package) + GitHub Release with lockfile/SBOM/API-diff — crates are consumed by git+tag reference, not crates.io |
| `plugin` | `mcpg-plugin-*` | lib flow + 6-lane cdylib zips (Ed25519-signed when the org key is set) with cosign bundles + provenance attestations |
| `product` | `mcpg`, `mcpg-config`, `mcpg-plugin`, `mcpg-operator`, `mcpg-cloud` | lib flow + 6-lane binary tarballs (`{bin}-{version}-{triple}.tar.xz|.zip` + `.sha256` + `.sigstore.json` + attestation), SPDX SBOM + resolved lockfile, and — where the repo carries a Dockerfile — a multi-arch container image signed by digest |

Lanes: `x86_64/aarch64-unknown-linux-gnu` (native runners),
`x86_64/aarch64-unknown-linux-musl` (musl.cc cross, dynamic-linked so
the gateway can `dlopen` plugins), `aarch64-apple-darwin` (native),
`x86_64-pc-windows-gnu` (mingw cross).

Three org-variable gates phase the rollout: `OSS_CI_ENABLED` (unset ⇒
every run skips instantly), `OSS_RELEASES_PUBLISH` (cut real GitHub
Releases vs verify-only), and `OSS_ARTIFACTS_PUBLISH`
(binaries/zips/images ungate last, after key setup).
Signing is keyless cosign (pinned v2.4.1 — shipped verifiers read the
v2 formats) over GitHub OIDC; the only optional secret is
`OSS_PLUGIN_SIGNING_KEY` (a dedicated OSS Ed25519 seed for in-zip
plugin signatures).
