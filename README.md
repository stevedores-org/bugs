# Stevedores Org — Bug Audit Dashboard

Tracking progress of bug audits and fixes across all `stevedores-org` repositories.

## 📊 Summary Status

| Repository | Language / Tech | Audit Status | Bugs Found | Status |
| :--- | :--- | :--- | :--- | :--- |
| **oxidizedgraphRAG** | Rust | Done | 2 | ✅ Fixed (PRs pending) |
| **agent-scheduler** | Rust / Nix | Done | 0 | ✅ Clean |
| **agy-cli-1** | Rust / Nix | Done | 0 | ✅ Clean |
| **ai-agent-ci** | Rust / Go | Pending | 0 | ⏳ Auditing |
| **aivcs** | Rust / Nix | Pending | 0 | ⏳ Auditing |
| **data-fabric** | Rust / TS | Done | 0 | ✅ Clean |
| **gh-bot** | K8s Manifests | Done | 0 | ✅ Clean |
| **local-ci** | Go / Nix | Done | 0 | ✅ Clean |
| **mom-stevedores** | Rust | Pending | 0 | ⏳ Auditing |
| **nix-cache** | TS (Bun) | Done | 0 | ✅ Clean |
| **ogre** | Documentation | Done | 0 | ✅ Clean |
| **oxidizedgraph** | Rust / Nix | Pending | 0 | ⏳ Auditing |
| **oxidizedMCP** | Rust | Pending | 0 | ⏳ Auditing |
| **oxidizedRAG** | Rust / Nix | Pending | 0 | ⏳ Auditing |

---

## 🐛 Discovered Bugs & Fixes

### 1. `oxidizedgraphRAG` (develop branch)
* **Bug**: Root `Cargo.toml` referenced `oxidizedgraph` and `graphrag-core` using hardcoded absolute paths pointing to `/Users/aivcs/...` instead of relative paths. This caused compilation failures in CI and on other development machines.
* **Fix**: Replaced absolute paths with relative paths pointing to sibling directories (`../oxidizedgraph` and `../oxidizedRAG/graphrag-core`).
* **PR**: Open targeting `develop`.

### 2. `oxidizedgraphRAG` (main branch)
* **Bug**: The `crates/gemini/Cargo.toml` referenced `rag-core` and `embeddings` using `.workspace = true` inheritance, but these local dependencies were not declared in the root workspace's `dependencies` block, causing compilation to fail.
* **Fix**: Changed dependencies to use relative path declarations (`{ path = "../rag-core" }` and `{ path = "../embeddings" }`) to match the rest of the workspace members.
* **PR**: Open targeting `main` (or `develop` once merged).

---

*Last Updated: 2026-06-11 13:42:00-05:00*