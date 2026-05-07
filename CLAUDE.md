# cic-kubernetes — Claude kontextus

## Mi ez a rendszer

A `cic-kubernetes` a CentralInfraCore **Kubernetes cluster infrastruktúra domain repo**
— a cic-primitives leszármazottja.

**Scope: a Kubernetes cluster mint infrastruktúra egység.** Nem az, ami fut rajta.

Kezeli: cluster lifecycle, node pool, control plane egészség, cert rotáció.
Nem kezeli: Pod, Deployment, Service, Helm release, RBAC, ConfigMap — workload/policy réteg.

Részletes architektúra: `ai/SYSTEM_CONTEXT.md`
Tervezési döntések: `ai/DECISIONS.md`
Kötelező szabályok: `ai/MAINTENANCE_CONTRACT.md`

---

## Boot sequence — minden session elején

1. `mcp__cic-graph__kb_status` — KB elérhető és friss?
2. `ai/DECISIONS.md` — scope döntések ismerete kötelező
3. `ai/SYSTEM_CONTEXT.md` — teljes Kubernetes domain kontextus
4. `ai/MAINTENANCE_CONTRACT.md` — mit szabad, mit nem

---

## Háromszintű státusz

| Státusz | Jelentés |
|---|---|
| **defined** | YAML séma létezik, `make validate` zöld |
| **draft** | Design megvan, séma még nincs |
| **concept** | Megbeszélt, formálisan nem rögzítve |

---

## Aktuális séma állapot

| Elem | Státusz |
|---|---|
| `kubernetes-cluster.yaml` | **draft** |
| `kubernetes-node.yaml` | **draft** |
| adapter contract(ok) | **concept** |

---

## Kompozíciós lánc

```
base-repo
    └──► cic-primitives (primitives/@v0.1.3)
              └──► cic-kubernetes (ez a repo)
```

---

## Mérce

```bash
make validate          # ha nem zöld, semmi sem kész
make release VERSION=  # signed artifact (Vault szükséges)
```
