# System Context — cic-kubernetes (AI számára)

Olvasd el mielőtt bármit módosítasz.

---

## Mi ez a rendszer?

A `cic-kubernetes` a CentralInfraCore **Kubernetes cluster infrastruktúra domain repo**.
A Kubernetes clustert mint infrastrukturális egységet kezeli — nem a workloadot ami fut benne.

**Analógia a többi domain-nel:**
```
ComputeResource  ← a gép (VM/fizikai/cloud node)
NetworkInterface ← a hálózat (switch port / OVS bridge)
StorageResource  ← a block volume
KubernetesCluster ← a cluster ami ezekre épül
```

---

## Scope

**Belül van (cluster infrastruktúra):**
- Cluster lifecycle: create, upgrade, delete
- Node pool kezelés: scale out/in, node join/leave
- Control plane állapot: API server, etcd, scheduler, controller manager
- Certificate management, kubeconfig
- Cluster networking config (pod CIDR, service CIDR, DNS domain)
- Node OS konfiguráció (kernel params, sysctls, NTP)

**Kívül van (workload/policy — NEM CIC scope):**
- Pod, Deployment, StatefulSet, DaemonSet
- Service, Ingress
- Helm release, Operator
- RBAC, NetworkPolicy
- ConfigMap, Secret

---

## Menedzselt egységek

**KubernetesCluster** — a cluster mint egész
- config: kubernetes_version, cluster_network, control_plane_endpoint
- state: health, api_server_status, etcd_status, node_count
- ops: upgrade, rotate_certs

**KubernetesNode** — egy node a clusterben
- config: machine_type (controlplane/worker), install_disk, node_network
- state: node_status, kubelet_version, allocated_resources
- ops: cordon, drain, reboot, reset
- hivatkozások: ComputeResource (az alatta lévő VM/fizikai gép)

---

## Adapter réteg

Különböző implementációk kezelik a cluster lifecycle-t:
- `talos-adapter` — Talos Linux alapú cluster (gRPC API)
- `kubespray-adapter` — kubespray alapú cluster
- `k3s-adapter` — k3s lightweight cluster

Az implementációk "hiányosságai" ugyanúgy kezelendők mint cic-network-nél:
- Hiányzó funkció → conformance by deletion (schema validation error)
- Részleges implementáció → D-012 not_implemented hard reject

---

## Kapcsolat más domain-ekkel

```
KubernetesCluster
  └── KubernetesNode
        ├── compute_ref → ComputeResource (cic-compute)
        ├── network_ref → NetworkInterface (cic-network)
        └── install_disk → StorageResource (cic-storage)
```

---

## Jelenlegi állapot (2026-05-07)

| Elem | Státusz |
|---|---|
| git bootstrap + primitives/@v0.1.3 merge | **defined** |
| project.yaml + dependency.yaml | **defined** |
| `schemas/domain/kubernetes-cluster.yaml` | **defined** |
| `schemas/domain/kubernetes-node.yaml` | **defined** |
| adapter contractok (talos/k3s/rke2/kubespray/cloud-managed) | **defined** |
| `schemas/mappings/talos-machineconfig-mapping.yaml` | **defined** |
| adapter conformance_matrix (gépi format) | **defined** |
| `make validate` zöld | **pending** |
| első signed release | **concept** |
