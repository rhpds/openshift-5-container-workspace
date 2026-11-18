# OpenShift 5 container workshop workspace

GitOps source for the student environment. Your editable copy of this
repository lives in your own Gitea namespace; Argo CD watches it and applies
whatever you commit.

## Layout

| Path | Used by | Purpose |
| --- | --- | --- |
| `national-parks/` | Module 2, 3 | Complete National Parks stack |
| `national-parks/kustomization.yaml` | Module 2 | Entry point for the stack |
| `national-parks/national-parks-gitops-info.yaml` | Module 2, 3 | ConfigMap edited to watch a sync |
| `national-parks/00-mongodb-credentials.yaml` | Module 2 | One-time Job that creates the MongoDB Secret |
| `national-parks/01-mongodb.yaml` | Module 2 | MongoDB 8 Deployment and correct Service |
| `national-parks/02-nationalparks-backend.yaml` | Module 2 | Python backend ImageStream, BuildConfig, Service, Route |
| `national-parks/03-parksmap-discovery.yaml` | Module 2 | ParksMap ServiceAccount, Role and RoleBinding |
| `national-parks/04-parksmap-frontend.yaml` | Module 2, 3 | ParksMap Deployment (Module 3 breaks its readiness port) |
| `national-parks/05-park-data-bootstrap.yaml` | Module 2 | PostSync Job that seeds the park dataset |
| `weathernow/` | Module 4, 5 | Lightweight WeatherNow Kustomization and manifest |
| `scripts/` | Module 3, 4 | Helper scripts the lab instructions download and run |

## Argo CD paths

- National Parks Application: path `national-parks`
- WeatherNow Application: path `weathernow`

## Helper scripts

The workshop downloads these from `raw/main/scripts/` rather than from the
lab documentation repository, so they always match this workspace:

- `scripts/prepare-module03-baseline.sh` — restores the healthy Module 2/3
  baseline in your own namespaces.
- `scripts/setup-weathernow-gitops.sh` — adds the WeatherNow source and its
  Argo CD Application once, before Module 4.

Never commit passwords or generated Secrets. The MongoDB credentials Job
creates them inside the cluster namespace.
