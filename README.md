<div align="center">

# 🚀 Three-Tier Blog Application | DevSecOps on Amazon EKS

### Kubernetes · CI/CD Automation · Container Security · Observability

**A hands-on DevOps project deploying a containerized three-tier application on Amazon EKS, integrating Jenkins CI/CD, automated code-quality checks, vulnerability scanning, Kubernetes security controls, and infrastructure monitoring.**

![AWS](https://img.shields.io/badge/AWS-EKS%20%7C%20ECR-10212B?style=for-the-badge&logo=amazonwebservices&logoColor=FF9900)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestration-10212B?style=for-the-badge&logo=kubernetes&logoColor=326CE5)
![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-10212B?style=for-the-badge&logo=jenkins&logoColor=D24939)
![Docker](https://img.shields.io/badge/Docker-Containers-10212B?style=for-the-badge&logo=docker&logoColor=2496ED)

</div>

---

## 🏗️ CI/CD Architecture

```text
GitHub Push
     ↓
Jenkins Pipeline
     ↓
Build & Test
     ↓
SonarQube → Quality Gate
     ↓
Docker Build → Trivy Scan
     ↓
Amazon ECR
     ↓
Amazon EKS
     ↓
Rolling Deployment & Validation
     ↓
Prometheus + Grafana Monitoring
```

## 🧩 Application Architecture

| Layer | Technology | Purpose |
|---|---|---|
| **Frontend** | React + Vite | User interface for viewing and interacting with blog posts |
| **Backend** | Node.js + Express | REST API handling application requests and database communication |
| **Database** | MySQL 8.0 | Persistent storage for users, posts, and comments |

**Application Flow:** `React Frontend → Express API → MySQL Database`

## ⚙️ Engineering Highlights

- **Three-Tier Architecture:** Deployed React, Node.js/Express, and MySQL workloads on Amazon EKS using Kubernetes Deployments, Services, and a StatefulSet.
- **CI/CD Automation:** Built a Jenkins pipeline integrating GitHub webhooks, application builds, SonarQube Quality Gate checks, Trivy image scanning, ECR publishing, and EKS deployment.
- **Containerization:** Implemented multi-stage Docker builds with non-root container execution and health checks.
- **Persistent Database:** Configured MySQL with a 5 GiB EBS-backed PersistentVolumeClaim and validated data persistence after pod recreation.
- **Kubernetes Reliability:** Configured two frontend and two backend replicas, readiness/liveness probes, resource limits, and rolling updates.
- **Security Controls:** Used Kubernetes Secrets, RBAC, and NetworkPolicy to manage credentials and restrict database connectivity.
- **Observability:** Implemented Prometheus and Grafana to monitor Kubernetes resource utilization, pod health, and cluster performance.

## 📊 Documented Results

| Validation | Outcome |
|---|---|
| Jenkins CI/CD Pipeline | Successful |
| SonarQube Quality Gate | Passed |
| Trivy Image Scanning | Completed |
| Frontend Deployment | 2/2 Replicas Available |
| Backend Deployment | 2/2 Replicas Available |
| MySQL Persistent Storage | 5 GiB PVC Bound |
| Database NetworkPolicy | Verified |
| Kubernetes Rolling Update | Successful |
| Prometheus & Grafana | Implemented |

*Results reflect the completed project implementation, not a currently active deployment.*

## 📚 Project Documentation

### 📄 [Explore the Complete Project Documentation →](./Project%20Documentation.pdf)

*Architecture · Jenkins CI/CD · Docker · SonarQube · Trivy · Amazon EKS · Kubernetes Security · Monitoring*

---

<div align="center">

**Build → Analyze → Scan → Publish → Deploy → Observe**

</div>
