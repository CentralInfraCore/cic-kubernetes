# LLM Rules — cic-kubernetes

- Minden állításhoz: **defined** / **draft** / **concept**
- `schemas/atomic/` és `schemas/aggregate/` upstream — ne módosítsd
- Pod, Deployment, Service, Helm, RBAC, ConfigMap: D-001 alapján TILTOTT
- Scope kérdés: "provisionálod vagy fogyasztod?" — csak az előbbi CIC scope
- Minden döntést `ai/DECISIONS.md`-be (D-NNN formátum)
- `make validate` — ha nem zöld, javíts
