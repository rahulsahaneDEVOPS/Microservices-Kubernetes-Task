
# Microservices Kubernetes Deployment Assessment

![Kubernetes](https://img.shields.io/badge/Kubernetes-v1.35-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Minikube](https://img.shields.io/badge/Minikube-v1.38.1-FF6F00?style=for-the-badge&logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-v29.4-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-Express-339933?style=for-the-badge&logo=node.js&logoColor=white)
![Assignment](https://img.shields.io/badge/HeroVired-Completed-success?style=for-the-badge)

> End-to-end deployment of a containerized Node.js microservices application on Kubernetes using Minikube with ClusterIP Services, Health Probes, Resource Management and NGINX Ingress.

---

# Table of Contents

1. Project Overview
2. Architecture
3. Application Components
4. Repository Structure
5. Technology Stack
6. Environment
7. Prerequisites
8. Docker Images
9. Minikube Setup
10. Kubernetes Deployment
11. Service Discovery
12. Health Checks
13. Resource Management
14. Validation
15. Ingress
16. Troubleshooting
17. Screenshot Gallery
18. Learning Outcomes
19. Future Improvements
20. Author

---

# Project Overview

This project demonstrates deployment of four Node.js microservices on a local Kubernetes cluster created with Minikube.

The implementation includes:

- Kubernetes Deployments
- ClusterIP Services
- Labels & Selectors
- Resource Requests and Limits
- Liveness Probes
- Readiness Probes
- Internal DNS based Service Discovery
- API Gateway
- Bonus NGINX Ingress

---

# Architecture

```text
                         Client
                            │
              kubectl port-forward / Ingress
                            │
                    Gateway Service
          ┌─────────────────┼─────────────────┐
          │                 │                 │
          ▼                 ▼                 ▼
   User Service      Product Service    Order Service
```

---

# Application Components

| Service | Port | Purpose |
|---------|-----:|---------|
| User Service | 3000 | Returns users |
| Product Service | 3001 | Returns products |
| Order Service | 3002 | Creates & returns orders |
| Gateway Service | 3003 | API Gateway |

# Repository Structure

```text
Microservices-Kubernetes-Task/
├── deployments/
├── services/
├── ingress/
├── screenshots/
├── Microservices/
├── README.md
├── LICENSE
└── .gitignore
```

# Technology Stack

- Kubernetes
- Minikube
- Docker
- Node.js
- Express.js
- Git
- YAML

# Environment

| Component | Version |
|-----------|---------|
| Ubuntu | 22.04 |
| Kubernetes | v1.35 |
| Minikube | v1.38.1 |
| Docker | 29.x |

# Prerequisites

- Docker Engine
- kubectl
- Minikube
- Git

# Start Minikube

```bash
minikube start --driver=docker --cpus=2 --memory=4096
minikube status
kubectl get nodes
```

# Load Docker Images

```bash
minikube image load microservices-task-user-service:latest
minikube image load microservices-task-product-service:latest
minikube image load microservices-task-order-service:latest
minikube image load microservices-task-gateway-service:latest
```

# Deploy Kubernetes Resources

```bash
kubectl apply -f deployments/
kubectl apply -f services/
kubectl get deployments
kubectl get pods
kubectl get svc
```

# Service Discovery

Internal communication uses Kubernetes DNS:

- http://user-service:3000
- http://product-service:3001
- http://order-service:3002

# Health Checks

Each Deployment includes:

- Liveness Probe
- Readiness Probe
- Resource Requests
- Resource Limits
- Labels
- Selectors
- imagePullPolicy: Never

# Validation

```bash
kubectl port-forward service/gateway-service 3003:3003

curl http://localhost:3003/api/users
curl http://localhost:3003/api/products
curl http://localhost:3003/api/orders

curl -X POST http://localhost:3003/api/orders -H "Content-Type: application/json" -d '{"userId":1,"productId":2}'
```

# Bonus - NGINX Ingress

```bash
minikube addons enable ingress
kubectl apply -f ingress/ingress.yaml
kubectl get ingress
```

Update `/etc/hosts`

```text
<MINIKUBE_IP> microservices.local
```

# Troubleshooting

```bash
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl rollout restart deployment/<deployment-name>
```

# 📸 Deployment Workflow & Screenshots

This section documents the complete deployment workflow from repository creation to successful Kubernetes deployment and validation.

---

## Step 01 – Repository Creation
**Screenshot:** `01_No_available_destinations_to_fork_this_repository.png`

The original repository could not be forked, so a new GitHub repository was created manually.

![](screenshots/01_No_available_destinations_to_fork_this_repository.png)

---

## Step 02 – Create New GitHub Repository
**Screenshot:** `02_NewRepo_Microservices-Kubernetes-Task.png`

Created a dedicated repository for the Kubernetes assignment.

![](screenshots/02_NewRepo_Microservices-Kubernetes-Task.png)

---

## Step 03 – Start Minikube Cluster

```bash
minikube start --driver=docker --cpus=2 --memory=4096
```

**Screenshot:** `03_minikube_start.png`

![](screenshots/03_minikube_start.png)

---

## Step 04 – Verify Minikube Status

```bash
minikube status
```

**Screenshot:** `04_minikube_status.png`

![](screenshots/04_minikube_status.png)

---

## Step 05 – Verify Kubernetes Context

```bash
kubectl config current-context
```

**Screenshot:** `05_current_context.png`

![](screenshots/05_current_context.png)

---

## Step 06 – Verify Kubernetes Node

```bash
kubectl get nodes
```

**Screenshot:** `06_minikube_node.png`

![](screenshots/06_minikube_node.png)

---

## Step 07 – Verify Docker Images

```bash
docker images
```

**Screenshot:** `07_docker_images.png`

![](screenshots/07_docker_images.png)

---

## Step 08 – Load Images into Minikube

```bash
minikube image ls
```

**Screenshot:** `08_minikube_images.png`

![](screenshots/08_minikube_images.png)

---

## Step 09 – Verify User Service Logs

```bash
kubectl logs deployment/user-service
```

**Screenshot:** `09_user_logs.png`

![](screenshots/09_user_logs.png)

---

## Step 10 – Deploy User & Product Services

**Screenshot:** `10_k8s_user_product_status.png`

Verified User and Product deployments, pods and services.

![](screenshots/10_k8s_user_product_status.png)

---

## Step 11 – Deploy Order Service

**Screenshot:** `11_user_product_order_running.png`

Verified User, Product and Order services.

![](screenshots/11_user_product_order_running.png)

---

## Step 12 – Deploy Gateway Service

**Screenshot:** `12_all_services_running.png`

Verified all four services are running successfully.

![](screenshots/12_all_services_running.png)

---

## Step 13 – Gateway Logs

```bash
kubectl logs deployment/gateway-service
```

**Screenshot:** `13_gateway_logs.png`

![](screenshots/13_gateway_logs.png)

---

## Step 14 – Port Forward Gateway

```bash
kubectl port-forward service/gateway-service 3003:3003
```

**Screenshot:** `14_port_forward.png`

![](screenshots/14_port_forward.png)

---

## Step 15 – Test Users API

```bash
curl http://localhost:3003/api/users
```

**Screenshot:** `15_api_users.png`

![](screenshots/15_api_users.png)

---

## Step 16 – Test Orders API

```bash
curl http://localhost:3003/api/orders
```

**Screenshot:** `16_api_orders.png`

![](screenshots/16_api_orders.png)

---

## Step 17 – Create Order

```bash
curl -X POST http://localhost:3003/api/orders -H "Content-Type: application/json" -d '{"userId":1,"productId":2}'
```

**Screenshot:** `17_create_order.png`

![](screenshots/17_create_order.png)

---

## Step 18 – Retrieve Orders

```bash
curl http://localhost:3003/api/orders
```

**Screenshot:** `18_get_orders.png`

![](screenshots/18_get_orders.png)

---

## Step 19 – Enable NGINX Ingress

```bash
minikube addons enable ingress
```

**Screenshot:** `19_ingress_controller.png`

![](screenshots/19_ingress_controller.png)

---

## Step 20 – Create Ingress Resource

```bash
kubectl get ingress
```

**Screenshot:** `20_ingress_created.png`

![](screenshots/20_ingress_created.png)

---

## Step 21 – Validate Ingress

**Screenshot:** `21_ingress_test.png`

Verified successful routing through NGINX Ingress.

![](screenshots/21_ingress_test.png)


# Learning Outcomes

- Built Docker images for multiple services
- Deployed workloads using Kubernetes Deployments
- Exposed applications with ClusterIP Services
- Implemented health probes
- Used Kubernetes DNS for service discovery
- Validated microservice communication
- Configured NGINX Ingress
- Documented deployment using GitHub

# Future Improvements

- ConfigMaps
- Secrets
- Persistent Volumes
- Helm Charts
- Horizontal Pod Autoscaler
- CI/CD with GitHub Actions
- Prometheus & Grafana monitoring

# Assignment Checklist

| Requirement | Status |
|------------|:------:|
| Deployments | ✅ |
| Services | ✅ |
| Requests & Limits | ✅ |
| Environment Variables | ✅ |
| Readiness Probe | ✅ |
| Liveness Probe | ✅ |
| ClusterIP | ✅ |
| Service Discovery | ✅ |
| Gateway Validation | ✅ |
| Bonus Ingress | ✅ |

# Author

**Rahul Sahane**

GitHub: https://github.com/rahulsahaneDEVOPS/Microservices-Kubernetes-Task
