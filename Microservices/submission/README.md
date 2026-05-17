
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


<img width="535" height="88" alt="Screenshot 2026-05-17 at 4 31 30 PM" src="https://github.com/user-attachments/assets/ae49927a-8f8e-4949-8168-77a29b826e2d" />


---

Check services:

```bash
kubectl get svc
```

Output:

<img width="559" height="101" alt="Screenshot 2026-05-17 at 8 15 24 PM" src="https://github.com/user-attachments/assets/98162278-e9f0-40c0-81a0-799605b187b3" /> 


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
Output: 

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
Output: 

<img width="660" height="100" alt="Screenshot 2026-05-17 at 8 25 06 PM" src="https://github.com/user-attachments/assets/64c9a73f-f3fb-4730-bb99-c3b963558fea" />

---

## Logs

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
Output:

<img width="583" height="114" alt="Screenshot 2026-05-17 at 8 25 48 PM" src="https://github.com/user-attachments/assets/188814ca-d557-496f-ac44-63321196bd75" />

---

## Screenshots 📸

Pods Screenshot
Logs Screenshot
API Screenshot

---
Author

Rajendra Raghunath Pansare

---
