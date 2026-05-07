# Onboarding (AI) — cic-kubernetes

## 1 perc alatt

- **Mi ez:** Kubernetes cluster infrastruktúra domain — nem workload management
- **Scope:** cluster lifecycle, node pool, control plane — Pod/Deployment/Service NEM ide tartozik
- **Anchor:** Talos MachineConfig (dependency.yaml-ban dokumentálva)
- **Mérce:** `make validate` — ha nem zöld, semmi sem kész

## Mielőtt bármit írsz

1. `mcp__cic-graph__kb_status` — KB elérhető?
2. Olvasd: `ai/SYSTEM_CONTEXT.md`
3. Olvasd: `ai/DECISIONS.md` — D-001..D-004

## Scope kérdés esetén

"Provisionálod vagy fogyasztod?"
- Provisionálod → CIC scope (KubernetesCluster, KubernetesNode)
- Fogyasztod → workload réteg, nem ide
