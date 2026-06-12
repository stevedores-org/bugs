# Stevedores Org — Bug Audit Dashboard

Tracking progress of bug audits and fixes across all `stevedores-org` repositories.

## 📊 Summary Status

| Repository | Language / Tech | Audit Status | Bugs Found | Status |
| :--- | :--- | :--- | :--- | :--- |
| **oxidizedgraphRAG** | Rust | Done | 2 | ✅ Fixed (PRs pending) |
| **agent-scheduler** | Rust / Nix | Done | 0 | ✅ Clean |
| **agy-cli-1** | Rust / Nix | Done | 0 | ✅ Clean |
| **ai-agent-ci** | Rust / Go | Done | 0 | ✅ Clean |
| **aivcs** | Rust / Nix | Done | 0 | ✅ Clean |
| **data-fabric** | Rust / TS | Done | 0 | ✅ Clean |
| **gh-bot** | K8s Manifests | Done | 0 | ✅ Clean |
| **local-ci** | Go / Nix | Done | 0 | ✅ Clean |
| **mom-stevedores** | Rust | Done | 0 | ✅ Clean |
| **nix-cache** | TS (Bun) | Done | 0 | ✅ Clean |
| **ogre** | Documentation | Done | 0 | ✅ Clean |
| **oxidizedgraph** | Rust / Nix | Done | 0 | ✅ Clean |
| **oxidizedMCP** | Rust | Done | 0 | ✅ Clean |
| **oxidizedRAG** | Rust / Nix | Done | 11 | ⚠️ 11 tests failed; integration tests hung |

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

### 3. `oxidizedRAG` (develop branch)
* **Bug/Issue**: Compiles correctly, but 11 tests under `graphrag-core` failed (primarily under `rograg::intent_classifier`, `rograg::logic_form`, `rograg::streaming`, and `rograg::validator`). Additionally, integration tests `graph::incremental::tests::test_basic_entity_upsert`, `test_production_graph_store_entity_upsert`, `test_production_graph_store_event_publishing`, and `test_production_graph_store_relationship_upsert` hung indefinitely (timed out/blocked on entity upsert).
* **Fix**: Needs investigation into mock databases/services dependencies required for these tests.

---

*Last Updated: 2026-06-11 20:12:00-05:00*