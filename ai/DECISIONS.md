# Tervezési döntések — cic-kubernetes

---

## D-001 — Scope: cluster infrastruktúra, nem workload (2026-05-07)

**Döntés:** A cic-kubernetes a Kubernetes clustert mint infrastrukturális egységet kezeli.
Workload management (Pod, Deployment, Service, Helm) — NEM ide tartozik.

**Miért:** A CIC infrastruktúra menedzsment réteg — ugyanolyan logikával mint
a ComputeResource a gépet, a StorageResource a volume-ot kezeli. A cluster
infrastruktúra (node-ok, control plane, networking config) = CIC scope.
A cluster tartalom = alkalmazás csapat felelőssége.

---

## D-002 — Config anchor: Talos MachineConfig (2026-05-07)

**Döntés:** A séma tervezésének fogalmi referenciája a Talos MachineConfig/ClusterConfig
(v1alpha1). Ez teljes körűen lefedi a Kubernetes cluster infrastruktúra konfigurációját.

**Miért:** Nincs RFC 8343 szintű formális standard Kubernetes cluster management-re.
A Talos config a legteljesebb, strukturált, deklaratív spec erre a területre.

**Implementáció-agnosztikus:** A séma Kubernetes cluster infrastruktúrát ír le,
nem Talos-specifikusan. Kubespray, k3s, más implementációk is implementálják —
hiányaik a cic-yang-féle conformance mechanizmussal kezelendők.

**Validáció:** A Talos csapat validálja a sémát — ők az anchor autoritása.

---

## D-003 — Két menedzselt egység: KubernetesCluster + KubernetesNode (2026-05-07)

**Döntés:** Két önálló DomainComposition:
- `KubernetesCluster` — a cluster egésze (control plane config, networking, cert management)
- `KubernetesNode` — egy node (machine type, install, kubelet config)

**Miért:** A cluster és a node különböző lifecycle-al bír:
- Node hozzáadható/eltávolítható a cluster törlése nélkül
- Control plane upgrade különbözik a worker node upgrade-től
- A node hivatkozik ComputeResource-ra (az alatta lévő VM/fizikai gép)

---

## D-004 — Cross-domain referenciák (2026-05-07)

**Döntés:** A KubernetesNode hivatkozik más domain-ekre:
- `compute_ref` → ComputeResource (cic-compute) — az alatta lévő gép
- `network_ref` → NetworkInterface (cic-network) — node hálózati interfész
- `install_disk` → StorageResource (cic-storage) — boot disk

**Miért:** A cluster node egy ComputeResource-on fut, NetworkInterface-en kommunikál,
StorageResource-on tárol. A CIC cross-domain referencia mechanizmus (CIC address) ezt
természetesen lehetővé teszi.
