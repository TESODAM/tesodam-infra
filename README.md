# 🏗️ Infra Monorepo for Tesodam

This repository contains all infrastructure tooling configurations for the **production environment** of the Tesodam platform. It includes deployment manifests, container builds, Helm configurations, and GitHub Actions workflows for continuous delivery.

## 📁 Repository Structure

```
tesodam-infra/
├── .github/
│   └── workflows/
│       ├── vault-deploy.yaml
│       └── dispatch.yaml
│
├── environments/
│   └── prod/
│       ├── vault/
│       └── ...
│
├── vault/
│   ├── Dockerfile
│   └── helm/
│       └── values.yaml
└── ...
```


## 🚀 Tools Managed

- [ ] HashiCorp Vault
- [ ] Apache Kafka *(coming soon)*
- [ ] Redis Streams *(coming soon)*
- [ ] KeyDB *(coming soon)*
- [ ] ClickHouse DB *(coming soon)*
- [ ] Vespa AI *(coming soon)*
- [ ] NGINX Ingress Controller *(optional)*

---

## ⚙️ CI/CD Pipeline

### 🛠️ Stack
- **CI/CD:** GitHub Actions
- **Container Registry:** GitHub Container Registry (GHCR)
- **CD Tool:** ArgoCD
- **Target Platform:** Kubernetes (via EKS, GKE, AKS, or self-hosted)

### 🧠 How It Works

1. You push a change (e.g., to `vault/`).
2. A GitHub Actions workflow:
   - Builds the Docker image
   - Pushes it to GHCR
   - Triggers ArgoCD sync or applies Kubernetes manifests
3. The updated service is deployed to the respective Kubernetes cluster.

### 🧠 Selective Deployments
Workflows are scoped per tool. 
Eg: If you only update Vault, only Vault's build and deployment are triggered.


## 🌍 Cloud Provider Agnostic

This repo is built to deploy infrastructure tools to **any Kubernetes cluster**, regardless of where it's hosted:

- ✅ *AWS EKS* - ArgoCD Server, HashiCorp Vault
- ✅ *Google Cloud GKE*
- ✅ *Azure AKS*
- ✅ *Self-hosted clusters* (e.g., k3s, k0s, bare metal)

Cluster-specific overrides (like node selectors or storage classes) can be defined under `environments/prod/<tool>/`.

---

## 🔮 Future Roadmap

- [ ] Start deploying the other needed infra tools as per phases planned
- [ ] Auto-sync ArgoCD after workflow success
- [ ] Add dashboards for Analytics (Grafana/Prometheus)
- [ ] Extend Vault with dynamic secrets and audit logs

---

## ✅ Status

| Environment | Description    | Status |
|-------------|----------------|--------|
| `prod`      | Production use | ⚠️ Creation In-Progress |
---
