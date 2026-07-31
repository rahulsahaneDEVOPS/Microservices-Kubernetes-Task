# Microservices Kubernetes Deployment Assessment

![Kubernetes](https://img.shields.io/badge/Kubernetes-v1.35-blue)
![Minikube](https://img.shields.io/badge/Minikube-v1.38.1-red)
![Docker](https://img.shields.io/badge/Docker-29.4-blue)
![Node.js](https://img.shields.io/badge/Node.js-Express-green)
![Status](https://img.shields.io/badge/Assignment-Completed-brightgreen)

## Objective

Deploy a Node.js based microservices application on Kubernetes using Minikube and validate inter-service communication.

---

## Project Structure

```text
Microservices-Kubernetes-Task/
├── deployments/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
├── services/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
├── ingress/
│   └── ingress.yaml
├── screenshots/
├── Microservices/
└── README.md
```

## Application Components

| Service | Port |
|---------|-----:|
| User Service | 3000 |
| Product Service | 3001 |
| Order Service | 3002 |
| Gateway Service | 3003 |

## Prerequisites

- Ubuntu 22.04
- Docker
- Minikube
- kubectl
- Git

## Start Minikube

```bash
minikube start --driver=docker --cpus=2 --memory=4096
minikube status
kubectl get nodes
```

## Load Docker Images

```bash
minikube image load microservices-task-user-service:latest
minikube image load microservices-task-product-service:latest
minikube image load microservices-task-order-service:latest
minikube image load microservices-task-gateway-service:latest
```

## Deploy

```bash
kubectl apply -f deployments/
kubectl apply -f services/
```

Verify:

```bash
kubectl get deployments
kubectl get pods
kubectl get svc
```

## Test Gateway

```bash
kubectl port-forward service/gateway-service 3003:3003
```

In another terminal:

```bash
curl http://localhost:3003/api/users
curl http://localhost:3003/api/products
curl http://localhost:3003/api/orders

curl -X POST http://localhost:3003/api/orders \
-H "Content-Type: application/json" \
-d '{"userId":1,"productId":2}'

curl http://localhost:3003/api/orders
```

## Bonus - Ingress

```bash
minikube addons enable ingress
kubectl apply -f ingress/ingress.yaml
kubectl get ingress
```

Add to `/etc/hosts`:

```text
<MINIKUBE_IP> microservices.local
```

Test:

```bash
curl http://microservices.local/api/users
curl http://microservices.local/api/products
curl http://microservices.local/api/orders
```

## Troubleshooting

```bash
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl rollout restart deployment/<deployment-name>
```

## Technologies

- Kubernetes
- Minikube
- Docker
- Node.js
- Express.js
- Git

## Assignment Status

| Task | Status |
|------|:------:|
| Deployments | ✅ |
| Services | ✅ |
| Resource Requests & Limits | ✅ |
| Environment Variables | ✅ |
| Liveness Probe | ✅ |
| Readiness Probe | ✅ |
| ClusterIP | ✅ |
| Inter-Service Communication | ✅ |
| Bonus Ingress | ✅ |

## Screenshots

| Screenshot | Preview |
|------------|---------|
| 01 - No Available Destinations to Fork Repository | ![](screenshots/01_No_available_destinations_to_fork_this_repository.png) |
| 02 - New GitHub Repository | ![](screenshots/02_NewRepo_Microservices-Kubernetes-Task.png) |
| 03 - Minikube Start | ![](screenshots/03_minikube_start.png) |
| 04 - Minikube Status | ![](screenshots/04_minikube_status.png) |
| 05 - Current Kubernetes Context | ![](screenshots/05_current_context.png) |
| 06 - Minikube Node | ![](screenshots/06_minikube_node.png) |
| 07 - Docker Images | ![](screenshots/07_docker_images.png) |
| 08 - Images Loaded into Minikube | ![](screenshots/08_minikube_images.png) |
| 09 - User Service Logs | ![](screenshots/09_user_logs.png) |
| 10 - User & Product Services Running | ![](screenshots/10_k8s_user_product_status.png) |
| 11 - User, Product & Order Services Running | ![](screenshots/11_user_product_order_running.png) |
| 12 - All Kubernetes Services Running | ![](screenshots/12_all_services_running.png) |
| 13 - Gateway Logs | ![](screenshots/13_gateway_logs.png) |
| 14 - Port Forward | ![](screenshots/14_port_forward.png) |
| 15 - User API Test | ![](screenshots/15_api_users.png) |
| 16 - Orders API Test | ![](screenshots/16_api_orders.png) |
| 17 - Create Order | ![](screenshots/17_create_order.png) |
| 18 - Get Orders | ![](screenshots/18_get_orders.png) |
| 19 - Ingress Controller | ![](screenshots/19_ingress_controller.png) |
| 20 - Ingress Created | ![](screenshots/20_ingress_created.png) |
| 21 - Ingress Test | ![](screenshots/21_ingress_test.png) |

## Author

**Rahul Sahane**

GitHub Repository:

https://github.com/rahulsahaneDEVOPS/Microservices-Kubernetes-Task
