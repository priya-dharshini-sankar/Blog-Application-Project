# 🚀 Production-Level Three-Tier Blog Application on Amazon EKS

A production-oriented three-tier Blog Application deployed on **Amazon EKS** with Docker, Jenkins CI/CD, Amazon ECR, SonarQube, Trivy, Prometheus, and Grafana.

## 📌 Project Overview

This project demonstrates the deployment and automation of a three-tier Blog Application consisting of:

- **Frontend** – React + NGINX
- **Backend** – Node.js + Express
- **Database** – MySQL

The application is containerized using Docker and deployed on Amazon EKS with persistent database storage.

## 🏗️ Architecture

```text
GitHub
   ↓
Jenkins CI/CD
   ↓
SonarQube → Quality Gate
   ↓
Docker Build
   ↓
Trivy Scan
   ↓
Amazon ECR
   ↓
Amazon EKS
   ├── Frontend
   ├── Backend
   └── MySQL + Persistent Storage
          ↓
   Prometheus + Grafana
````

## 🛠️ Technology Stack

| Category        | Technologies               |
| --------------- | -------------------------- |
| Frontend        | React, Vite, NGINX         |
| Backend         | Node.js, Express           |
| Database        | MySQL 8.0                  |
| Containers      | Docker                     |
| Registry        | Amazon ECR                 |
| Orchestration   | Kubernetes, Amazon EKS     |
| CI/CD           | Jenkins                    |
| Code Quality    | SonarQube                  |
| Security        | Trivy                      |
| Monitoring      | Prometheus, Grafana        |
| Storage         | Kubernetes PVC, Amazon EBS |
| Version Control | Git, GitHub                |

## 🔄 CI/CD Pipeline

The Jenkins pipeline automates:

```text
Checkout
→ Build
→ Test
→ SonarQube Analysis
→ Quality Gate
→ Docker Build
→ Trivy Scan
→ Image Versioning
→ ECR Push
→ EKS Deployment
→ Deployment Validation
```

A GitHub webhook automatically triggers Jenkins when code is pushed.

## ☁️ AWS & Kubernetes

The application is deployed on Amazon EKS using:

* EKS Cluster and Managed Node Group
* Amazon ECR
* Amazon EBS persistent storage
* Kubernetes Deployments and StatefulSet
* Kubernetes Services
* ConfigMaps and Secrets
* LoadBalancer
* NetworkPolicy

Frontend and Backend use multiple replicas with readiness/liveness probes and RollingUpdate deployment strategy.

## 🔐 Security

The project implements:

* Dedicated IAM user for Jenkins
* Kubernetes RBAC
* Restricted database network access
* Kubernetes Secrets
* Non-root containers
* Trivy vulnerability scanning
* Persistent and private database access
* Git protection for sensitive configuration

## 📊 Monitoring & Logging

Prometheus and Grafana are used to monitor:

* CPU and memory
* Pod status
* Pod restarts
* Node health
* Application metrics

Kubernetes logs are used to inspect Frontend, Backend, Database, and workload activity.

## 📂 Project Structure

```text
BlogReact/
├── backend/
├── frontend/
├── database/
├── k8s/
├── Jenkinsfile
├── sonar-project.properties
├── .gitignore
└── README.md
```

## ✅ Project Outcome

The Blog Application was successfully containerized, published to Amazon ECR, deployed on Amazon EKS, and integrated with an automated Jenkins CI/CD pipeline.

The project demonstrates **CI/CD automation, containerization, Kubernetes deployment, persistent storage, security, rolling deployment, monitoring, and logging**.

