# AI Maintenance Contract — cic-kubernetes

---

## Mit szabad

- `schemas/domain/` módosítása, ha `make validate` zöld marad
- `schemas/adapters/` bővítése új adapter contract-tal
- `ai/DECISIONS.md` bővítése (D-NNN, dátummal)
- `ai/PROMPTMAP.yaml` státusz frissítése

## Mit nem szabad

- `schemas/atomic/` és `schemas/aggregate/` — upstream (cic-primitives)
- `schemas/index.yaml` — upstream (kivéve új kind hozzáadása)
- Workload management (Pod, Deployment, Service) hozzáadása — D-001 tiltja
- `make validate` megkerülése

## Scope határ — kérdéses esetben

Ha nem egyértelmű hogy valami CIC scope-e: "provisionálod vagy fogyasztod?"
- Provisionálod (lifecycle: create/upgrade/delete) → CIC scope
- Fogyasztod (alkalmazás deployol rá) → workload réteg, NEM ide

## Release folyamat

```bash
git checkout -b kubernetes/releases/vX.Y.Z
export VAULT_ADDR="https://127.0.0.1:18200"
export VAULT_TOKEN=$(cat $XDG_RUNTIME_DIR/vault/sign-token)
export VAULT_SKIP_VERIFY=1
make release
git tag "kubernetes/@vX.Y.Z"
git tag "cic-kubernetes@X.Y.Z"
```
