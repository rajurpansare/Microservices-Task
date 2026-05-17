
# Kubernetes Microservices Deployment

## Project Overview
This project demonstrates deployment of a containerized Node.js microservices application on Kubernetes using Minikube. The application architecture follows the microservices approach where multiple independent services communicate with each other within a Kubernetes cluster.

The project focuses on Kubernetes deployments, service configuration, container orchestration, service discovery, and validation of inter-service communication using Minikube.

---
## Objective

The main objective of this project is to:

- Deploy multiple Node.js microservices on Kubernetes
- Configure Kubernetes Deployments and Services
- Enable communication between services inside the cluster
- Use Minikube as the local Kubernetes environment
- Validate application accessibility and pod health
- Understand container orchestration concepts using Kubernetes
---

## Services

The application consists of four containerized Node.js microservices:

| Service | Port | Purpose |
|---|---|---|
| User Service | 3000 | Handles user data |
| Product Service | 3001 | Handles product data |
| Order Service | 3002 | Handles order data |
| Gateway Service | 3003 | API Gateway for routing requests |

The Gateway Service serves as the external access point for the application and routes requests to internal services.

---

## Step 2: Project Structure

```text
Submission/
├── deployments/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
│
├── services/
│   ├── user-service.yaml
│   ├── product-service.yaml
│   ├── order-service.yaml
│   └── gateway-service.yaml
│
├── screenshots/
│   ├── pods.png
│   ├── logs.png
│   └── service-test.png
│
└── README.md
```

---

# Technologies Used

The following technologies and tools were used in this project:

- Kubernetes
- Minikube
- Docker Desktop
- Node.js
- kubectl
- Git & GitHub

---


## Kubernetes Resources Implemented

### Deployments

Separate Kubernetes Deployment manifests were created for all four microservices.

Each deployment includes:

- User Service deployment
- Product Service deployment
- Order Service deployment
- Gateway Service deployment

- Correct container image reference
- Resource limits and requests
- Environment variables
- Liveness and readiness probes
- Proper labels and selectors

---

## Services

 Service | Port | Purpose |
|---|---|---|
| User Service | 3000 | Handles user data |
| Product Service | 3001 | Handles product data |
| Order Service | 3002 | Handles order data |
| Gateway Service | 3003 | API Gateway for routing requests |


---

## Validation and Testing
The deployment was validated using the following methods:

Verification of running pods
Verification of Kubernetes services
Docker container log inspection
Gateway Service accessibility testing
Minikube service exposure testing
All microservices were successfully deployed and reached Running state inside the Kubernetes cluster.


Check pods:


```bash
kubectl get pods
```

Output:

```bash
<img width="528" height="118" alt="Screenshot 2026-05-17 at 8 12 46 PM" src="https://github.com/user-attachments/assets/cedf61e7-3bb2-48c1-87ba-fc1c9c4a6b83" />
```

---

Check services:

```bash
kubectl get svc
```

Output:

```bash
<img width="559" height="101" alt="Screenshot 2026-05-17 at 8 15 24 PM" src="https://github.com/user-attachments/assets/98162278-e9f0-40c0-81a0-799605b187b3" />
```

---

Check Inter-Service Communication API

API Test

```bash
curl http://localhost:3003/api/users
```

```bash
curl http://localhost:3003/api/products
```

```bash
curl http://localhost:3003/api/orders
```

<img width="589" height="86" alt="Screenshot 2026-05-17 at 8 19 26 PM" src="https://github.com/user-attachments/assets/e2504c76-9aaa-437b-ae5f-5c05422efd48" />

---

## Create Order

```bash
curl -X POST http://localhost:3003/api/orders \
-H "Content-Type: application/json" \
-d '{
  "userId":1,
  "productId":1
}'
```

---

# Step 11: Check Logs

Gateway logs:

```bash
kubectl logs deployment/gateway-service
```

User service logs:

```bash
kubectl logs deployment/user-service
```

Product service logs:

```bash
kubectl logs deployment/product-service
```

Order service logs:

```bash
kubectl logs deployment/order-service
```

---

# Step 13: Capture Screenshots 📸

## Pods Screenshot

```bash
kubectl get pods
```

Save screenshot as:

```text
submission/screenshots/pods.png
```

---

## Logs Screenshot

```bash
kubectl logs deployment/gateway-service
```

Save as:

```text
submission/screenshots/logs.png
```

---

## API Test Screenshot

Use:

```bash
curl http://localhost:3003/api/users
```

Save as:

```text
submission/screenshots/service-test.png
```

---

# Step 14: Create README.md

Create file:

```text
submission/README.md
```

Include:

- Project overview
- Minikube setup
- Docker image build steps
- Kubernetes deployment steps
- Service testing commands
- Ingress configuration
- Troubleshooting section

---

# Troubleshooting Guide 🧰

## Pods Stuck in ImagePullBackOff

Solution:

```bash
minikube image load user-service:v1
```

---

## Check Pod Details

```bash
kubectl describe pod <pod-name>
```

---

## Restart Deployment

```bash
kubectl rollout restart deployment gateway-service
```

---

## Verify Service Discovery

Run temporary pod:

```bash
kubectl run testpod --image=busybox -it --rm -- sh
```

Inside pod:

```bash
wget -qO- http://user-service:3000/users
```

If response comes back, Kubernetes DNS is working correctly.

---

# Final Submission Checklist ✅

Before creating submission.zip verify:

- All pods are Running
- All services are created
- APIs are working
- Screenshots are added
- README.md exists
- ingress.yaml added if attempting bonus task

---

# Create Final ZIP

```bash
zip -r submission.zip submission/
```

---

# Important Viva Questions 🎯

## Why use ClusterIP?
ClusterIP allows internal communication between services inside Kubernetes.

## Difference between Deployment and Service?
- Deployment manages pods.
- Service exposes pods using stable networking.

## What is readiness probe?
Checks whether pod is ready to receive traffic.

## What is liveness probe?
Checks whether application is alive. Kubernetes restarts failed containers automatically.

## Why use Ingress?
Ingress provides centralized routing and external access.

---

Your Kubernetes cluster is now transformed into a tiny digital city where services gossip through DNS names, pods regenerate like sci‑fi clones, and Ingress acts like an air traffic controller directing API packets through invisible sky-lanes ☸️

