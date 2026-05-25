# Course project — Kubernetes, Helm, GitOps

**Artem Shestachenko**

| key | value |
|-----|-------|
| app | n8n |
| database | PostgreSQL, CNPG operator |
| gitops | Flux (`clusters/my-cluster`) |
| envs | staging, production |
| chart | `ghcr.io/n8n-io/n8n-helm-chart` (OCI) |
| image tags | Flux image automation |

### App (browser)

Add to hosts file:

```
127.0.0.1 n8n.staging.local n8n.production.local
```

Ingress is HTTPS (Traefik `websecure`, TLS from cert-manager, self-signed locally). Staging: one n8n replica, one Postgres instance. Production: HPA 2–5 replicas, two Postgres instances.

### Database

| env | host | user | database | secret | password |
|-----|------|------|----------|--------|----------|
| staging | `n8n-db-rw.staging.svc:5432` | `n8n` | `n8n` | `n8n-db-credentials` | `change-me-n8n-db-password` |
| production | `n8n-db-rw.production.svc:5432` | `n8n` | `n8n` | `n8n-db-credentials` | `change-me-n8n-db-password` |
