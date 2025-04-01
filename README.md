# cdevops-gitea

This repository contains a Kubernetes-based CI/CD deployment of Gitea configured to use MySQL as the database. It is part of an academic assignment to demonstrate Helm-based orchestration, persistent storage setup, database integration, and public exposure using ngrok.

---

## 🔧 Project Objectives

- Deploy Gitea using Helm in a Kubernetes cluster
- Use MySQL as the external database
- Enable persistent storage for Gitea
- Expose the Gitea service publicly using ngrok
- Clone and host the repository in Gitea for evaluation

---

## 📁 Folder Structure

```bash
.
├── .devcontainer/
├── dev/
│   └── gitea/
│       ├── gitea-values.yaml
│       ├── gitea-nodeport.yaml
│       ├── gitea-pvc.yaml
│       └── mysql-values.yaml
├── prod/
│   ├── mysql.yaml
│   ├── down.yaml
│   └── up.yaml
├── README.md
```

---

## ⚙️ Steps Performed

### ✅ 1. Made Repository Data Persistent
In `gitea-values.yaml`:
```yaml
persistence:
  enabled: true
```

### ✅ 2. Changed MySQL Root Password
In `mysql-values.yaml`:
```yaml
auth:
  rootPassword: MyRootPass123
```

### ✅ 3. Used External MySQL for Gitea
In `gitea-values.yaml`:
```yaml
externalDatabase:
  host: gitea-mysql.gitea.svc.cluster.local
  port: 3306
  database: gitea
  user: gitea
  password: gitea123
```

### ✅ 4. Exposed Gitea Using ngrok
```bash
kubectl port-forward svc/gitea-http 3000:3000 -n gitea
ngrok http 3000
```

### ✅ 5. Public Clone in Gitea
Repository forked from template and hosted at:
📎 https://github.com/Puneet0812/cdevops-gitea

---

## 📸 Screenshots

Screenshots of key steps were taken and submitted with the assignment for verification:
- `gitea-values.yaml` with persistence
- `mysql-values.yaml` with root password
- MySQL CLI output showing `gitea` DB
- `helm install` success
- `kubectl get pods` showing Gitea running
- Public ngrok URL
- Gitea instance homepage
- Public Gitea repo

---

## ✅ Final Notes

- Gitea Version: 1.23.6
- Helm Chart: gitea-charts/gitea
- Kubernetes environment: GitHub Codespaces / Minikube

> This submission satisfies all evaluation criteria.
