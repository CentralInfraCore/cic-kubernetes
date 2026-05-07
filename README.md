# cic-kubernetes

> Emberi belépő: ez a README. AI belépő: `ai/ONBOARDING.md`.

A CIC **Kubernetes cluster infrastruktúra domain** — cluster lifecycle, node pool,
control plane konfiguráció és adapter contractok.

**Nem workload-management réteg.** Pod, Deployment, Service, Helm — NEM ide tartozik.

## Scope

```
Belül:   cluster lifecycle, node pool, control plane, cert management
Kívül:   Pod, Deployment, Service, RBAC, ConfigMap, Helm release
```

## Kompozíciós lánc

```
cic-primitives (@v0.1.3)  ← schema alap
  └──► cic-kubernetes     ← ez a repo
         ├── ref: cic-compute (@v0.2.1)
         ├── ref: cic-network (@v0.2.0)
         └── ref: talos-machineconfig (v1alpha1) — config anchor
```

## Séma elemek

| Fájl | Tartalom |
|---|---|
| `schemas/domain/kubernetes-cluster.yaml` | KubernetesCluster — cluster lifecycle |
| `schemas/domain/kubernetes-node.yaml` | KubernetesNode — node bootstrap |
| `schemas/adapters/talos-adapter.yaml` | Talos Linux (teljes) |
| `schemas/adapters/k3s-adapter.yaml` | k3s (részleges) |
| `schemas/adapters/rke2-adapter.yaml` | RKE2/Rancher (közel teljes) |
| `schemas/adapters/kubespray-adapter.yaml` | kubespray/Ansible (részleges) |
| `schemas/adapters/cloud-managed-adapter.yaml` | GKE, EKS, AKS, OKE, DOKS |
| `mappings/talos-machineconfig-mapping.yaml` | Talos config → CIC mező mapping |

## Mérce

```bash
make validate   # ha nem zöld, semmi sem kész
```
