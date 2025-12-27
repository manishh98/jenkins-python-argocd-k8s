# Django Todo App – Jenkins CI/CD with ArgoCD & Kubernetes

This project demonstrates an end-to-end CI/CD pipeline for a Django-based Python application using Jenkins, Docker, Kubernetes, and ArgoCD, following GitOps practices.

---

## 🛠 Tech Stack
- Python (Django)
- Jenkins (Declarative Pipeline)
- Docker & Docker Compose
- Kubernetes
- ArgoCD
- GitHub

---

## 🔄 CI/CD Architecture

GitHub → Jenkins → Docker Image Build → Kubernetes Manifests → ArgoCD → Kubernetes Cluster

This pipeline ensures automated build, containerization, and deployment of the application.

---

## ⚙️ CI/CD Workflow
1. Code is pushed to GitHub
2. Jenkins pipeline is triggered automatically
3. Jenkins builds Docker image for the Django application
4. Kubernetes manifests are managed via GitHub
5. ArgoCD continuously syncs manifests to the Kubernetes cluster
6. Application is deployed and managed using GitOps principles

---

## 📂 Project Structure

├── Dockerfile
├── Jenkinsfile
├── docker-compose.yml
├── deploy/
│ ├── deploy.yaml
│ ├── service.yaml
│ └── pod.yaml
├── manage.py
└── todoApp/


---

## ▶️ Run Application Locally
```bash
docker compose up -d

