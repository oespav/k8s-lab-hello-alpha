# hello-alpha

Owned by **team-alpha**. A multi-version helloworld service, deployed by Argo CD
from this repo into namespace `team-alpha` and exposed at
`https://hello.example.com/hello` through the platform's shared `public` gateway.

## Layout

```
chart/                      Helm chart: Deployments + Services per version, HTTPRoute
environments/lab/values.yaml  what runs in the lab cluster (versions, weights, hostname)
```

## Ship a change

1. Edit `environments/lab/values.yaml` (e.g. shift `weight` between v1 and v2).
2. Commit and push to `main`.
3. Argo CD syncs within ~30 s. Watch it in the Argo CD UI (app `hello-alpha`) and
   in the traffic console.

## What the platform decides (not this repo)

- The namespace (`team-alpha`) and that it may use the `public` gateway
- That this repo may only create Deployments, Services, ConfigMaps,
  ServiceAccounts, HTTPRoutes, HPAs and PDBs, and only in `team-alpha`

Those live in `platform-infra/argocd/tenants/team-alpha.yaml`. Need something else?
Open a PR there.
