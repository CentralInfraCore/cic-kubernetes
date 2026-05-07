# Roadmap — cic-kubernetes

## Phase 1 — Bootstrap ✓ (kész)

| Feladat | Státusz |
|---|---|
| git init + primitives/@v0.1.3 merge | ✓ done |
| project.yaml + dependency.yaml | ✓ done |
| CLAUDE.md + ai/ dokumentáció | ✓ done |

## Phase 2 — KubernetesCluster + KubernetesNode séma

| Feladat | Státusz |
|---|---|
| `schemas/domain/kubernetes-cluster.yaml` | pending |
| `schemas/domain/kubernetes-node.yaml` | pending |
| cross-domain referenciák (compute/network/storage) | pending |
| `make validate` zöld | pending |

## Phase 3 — Adapter contractok

| Feladat | Státusz |
|---|---|
| `schemas/adapters/talos-adapter.yaml` | concept |
| `schemas/adapters/kubespray-adapter.yaml` | concept |
| `schemas/adapters/k3s-adapter.yaml` | concept |

## Phase 4 — Validáció

| Feladat | Státusz |
|---|---|
| Talos csapat review | concept |
| Séma finalizálás review alapján | concept |

## Phase 5 — Első signed release (kubernetes/@v0.1.0)

| Feladat | Státusz |
|---|---|
| Release branch + Vault signing + tag | concept |
