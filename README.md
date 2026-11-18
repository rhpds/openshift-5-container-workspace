# OpenShift 5 container workshop workspace

GitOps source for the student environment. Your editable copy of this
repository lives in your own Gitea namespace; Argo CD watches it and applies
whatever you commit.

## Layout

| Path | Used by | Purpose |
| --- | --- | --- |
| `kustomization.yaml` | Module 2 | Entry point for the full National Parks stack |
| `national-parks-gitops-info.yaml` | Module 2, 3 | ConfigMap edited to watch a sync |
| `00-mongodb-credentials.yaml` | Module 2 | One-time Job that creates the MongoDB Secret |
| `01-mongodb.yaml` | Module 2 | MongoDB 8 Deployment and correct Service |
| `02-nationalparks-backend.yaml` | Module 2 | Python backend ImageStream, BuildConfig, Service, Route |
| `03-parksmap-discovery.yaml` | Module 2 | ParksMap ServiceAccount, Role and RoleBinding |
| `04-parksmap-frontend.yaml` | Module 2, 3 | ParksMap Deployment (Module 3 breaks its readiness port) |
| `05-park-data-bootstrap.yaml` | Module 2 | PostSync Job that seeds the park dataset |
| `weathernow/` | Module 4, 5 | Lightweight WeatherNow Kustomization and manifest |

## Argo CD paths

- National Parks Application: path `.`
- WeatherNow Application: path `weathernow`

Never commit passwords or generated Secrets. The MongoDB credentials Job
creates them inside the cluster namespace.
