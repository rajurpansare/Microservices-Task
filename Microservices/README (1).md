
# Kubernetes Microservices Deployment using Minikube

## Project Overview

This project demonstrates deployment of a containerized Node.js microservices application on Kubernetes using Minikube. The application architecture follows the microservices approach where multiple independent services communicate with each other within a Kubernetes cluster.

The project focuses on Kubernetes deployments, service configuration, container orchestration, service discovery, and validation of inter-service communication using Minikube.

---

# Objective

The main objective of this project is to:

- Deploy multiple Node.js microservices on Kubernetes
- Configure Kubernetes Deployments and Services
- Enable communication between services inside the cluster
- Use Minikube as the local Kubernetes environment
- Validate application accessibility and pod health
- Understand container orchestration concepts using Kubernetes

---

# Application Components

The application consists of four containerized Node.js microservices:

| Service Name | Description | Port |
|---|---|---|
| User Service | Handles user-related operations | 3000 |
| Product Service | Handles product-related operations | 3001 |
| Order Service | Handles order-related operations | 3002 |
| Gateway Service | Acts as API gateway and entry point | 3003 |

The Gateway Service serves as the external access point for the application and routes requests to internal services.

---

# Project Structure

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
- Visual Studio Code
- Git & GitHub

---

# Kubernetes Resources Implemented

## Deployments

Separate Kubernetes Deployment manifests were created for all four microservices.

Each deployment includes:

- Container image configuration
- Labels and selectors
- Resource requests and limits
- Environment variables
- Replica configuration
- Liveness and readiness probe configuration

Deployments ensure high availability and automated pod management inside the cluster.

---

## Services

Kubernetes Services were created for all microservices to enable communication within the cluster.

### Service Types Used

| Service | Type |
|---|---|
| User Service | ClusterIP |
| Product Service | ClusterIP |
| Order Service | ClusterIP |
| Gateway Service | NodePort |

ClusterIP services provide internal communication between services, while the Gateway Service uses NodePort to allow external access from the browser.

---

# Minikube Configuration

Minikube was used as the local Kubernetes environment for deploying and testing the application.

The Docker driver was configured with Minikube to simplify container management and local deployment.

The Kubernetes cluster was successfully initialized, and all deployments and services were applied using kubectl.

---

# Deployment Process

The deployment process involved the following steps:

1. Building Docker images for all microservices
2. Starting Minikube cluster
3. Applying Kubernetes Deployment manifests
4. Applying Kubernetes Service manifests
5. Verifying pod status and service configuration
6. Testing application accessibility through Gateway Service

All Kubernetes resources were deployed successfully and verified using kubectl commands.

---

# Service Communication

The microservices communicate internally using Kubernetes service discovery.

ClusterIP services allow internal communication using service names rather than IP addresses. This enables reliable and scalable communication between services inside the Kubernetes cluster.

The Gateway Service acts as the central entry point and communicates with the User, Product, and Order services.

---

# Validation and Testing

The deployment was validated using the following methods:

- Verification of running pods
- Verification of Kubernetes services
- Docker container log inspection
- Gateway Service accessibility testing
- Minikube service exposure testing

All microservices were successfully deployed and reached Running state inside the Kubernetes cluster.

---

# Screenshots Included

The screenshots folder contains evidence of successful deployment and testing:

| Screenshot | Description |
|---|---|
| pods.png | Running Kubernetes pods |
| logs.png | Application and service logs |
| service-test.png | Gateway service accessibility test |

---

# Troubleshooting Performed

During deployment, the following issues were identified and resolved:

- Docker image pull issues
- Minikube configuration setup
- Kubernetes probe failures
- Pod restart issues
- Service accessibility verification

Liveness and readiness probes were temporarily adjusted because the sample Node.js services did not expose dedicated health-check endpoints.

---

# Key Kubernetes Concepts Demonstrated

This project demonstrates practical implementation of:

- Kubernetes Deployments
- Kubernetes Services
- Pod Management
- ReplicaSets
- ClusterIP Networking
- NodePort Exposure
- Container Orchestration
- Service Discovery
- Resource Management
- Minikube Local Cluster Setup

---

### Docker build images:

<img width="940" height="690" alt="image" src="https://github.com/user-attachments/assets/cd97f420-9c0d-44e9-a9e8-d16357676dd0" />

<img width="940" height="698" alt="image" src="https://github.com/user-attachments/assets/34104959-0cd9-4d19-b048-a5210f4088fa" />

<img width="940" height="712" alt="image" src="https://github.com/user-attachments/assets/419166a1-3c8e-4a23-883b-69631c7791a8" />

<img width="940" height="726" alt="image" src="https://github.com/user-attachments/assets/4f7931f8-a4ec-49e0-af04-23ca97143cc4" />

<img width="940" height="764" alt="image" src="https://github.com/user-attachments/assets/4a9d714d-60b2-4df0-af34-2daad982a2db" />

## pods.png, logs.png & services.png: 

<img width="940" height="467" alt="image" src="https://github.com/user-attachments/assets/ffd091ae-6e53-4ccf-b9d5-aff1b387d5d2" />

<img width="940" height="311" alt="image" src="https://github.com/user-attachments/assets/3812524a-d36f-4154-acf0-89ca47a2754e" />

<img width="940" height="422" alt="image" src="https://github.com/user-attachments/assets/f812dae1-7190-4bef-9655-641debe38568" />

### Test in Browser

Open browser > Hit the above URLs > Ensure responses are received
http://localhost:3000 → User Service
<img width="625" height="144" alt="image" src="https://github.com/user-attachments/assets/1c020847-d30d-4230-bd00-96d467102752" />

http://localhost:3001 → Product Service
<img width="737" height="180" alt="image" src="https://github.com/user-attachments/assets/6d127c5b-9116-4ea3-9261-45c43bd51229" />

http://localhost:3002 > Order Service
<img width="526" height="139" alt="image" src="https://github.com/user-attachments/assets/11279d81-b7b2-4520-9922-4a1a03d23fbf" />

http://localhost:3003 → Gateway Service

--------


# Conclusion

This project successfully demonstrates deployment and orchestration of a microservices-based Node.js application using Kubernetes and Minikube.

All services were containerized, deployed, exposed, and validated successfully within the Kubernetes cluster. The project provides hands-on understanding of Kubernetes architecture, deployment strategies, service communication, and local cluster management using Minikube.

------

## Author
Sweta Patil
