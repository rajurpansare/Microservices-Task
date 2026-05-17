
# Kubernetes Microservices Deployment

## Project Overview
This project deploys four Node.js microservices on Kubernetes using Minikube.

### Services
| Service | Port | Purpose |
|---|---|---|
| User Service | 3000 | Handles user data |
| Product Service | 3001 | Handles product data |
| Order Service | 3002 | Handles order data |
| Gateway Service | 3003 | API Gateway for routing requests |

---

## Step 1: Install Required Tools

Docker Desktop
Minikube
kubectl
---

## Step 2: Project Structure

Create folders:

```bash
mkdir -p submission/deployments
mkdir -p submission/services
mkdir -p submission/ingress
mkdir -p submission/screenshots
```

Final structure:

```text
submission/
├── deployments/
├── services/
├── ingress/
├── screenshots/
└── README.md
```

---

## Step 3: Build Docker Images

---

## Build Services

```bash
cd user-service
docker build -t user-service:v1 .
```

---

## Build Product Service

```bash
cd ../product-service
docker build -t product-service:v1 .
```

---

## Build Order Service

```bash
cd ../order-service
docker build -t order-service:v1 .
```

---

## Build Gateway Service

```bash
cd ../gateway-service
docker build -t gateway-service:v1 .
```

---

# Step 5: Load Images into Minikube

Because Minikube uses its own Docker environment:

```bash
minikube image load user-service:v1
minikube image load product-service:v1
minikube image load order-service:v1
minikube image load gateway-service:v1
```

Verify:

```bash
minikube image ls
```

---

# Step 6: Create Deployment YAML Files

## 1. User Service Deployment

File:

```text
submission/deployments/user-service.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-service
spec:
  replicas: 1
  selector:
    matchLabels:
      app: user-service
  template:
    metadata:
      labels:
        app: user-service
    spec:
      containers:
      - name: user-service
        image: user-service:v1
        imagePullPolicy: Never
        ports:
        - containerPort: 3000
        resources:
          requests:
            memory: "128Mi"
            cpu: "100m"
          limits:
            memory: "256Mi"
            cpu: "250m"
        env:
        - name: NODE_ENV
          value: "production"
        readinessProbe:
          httpGet:
            path: /health
            port: 3000
          initialDelaySeconds: 5
          periodSeconds: 5
        livenessProbe:
          httpGet:
            path: /health
            port: 3000
          initialDelaySeconds: 15
          periodSeconds: 10
```

---

## 2. Product Service Deployment

File:

```text
submission/deployments/product-service.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: product-service
spec:
  replicas: 1
  selector:
    matchLabels:
      app: product-service
  template:
    metadata:
      labels:
        app: product-service
    spec:
      containers:
      - name: product-service
        image: product-service:v1
        imagePullPolicy: Never
        ports:
        - containerPort: 3001
        resources:
          requests:
            memory: "128Mi"
            cpu: "100m"
          limits:
            memory: "256Mi"
            cpu: "250m"
        env:
        - name: NODE_ENV
          value: "production"
        readinessProbe:
          httpGet:
            path: /health
            port: 3001
          initialDelaySeconds: 5
          periodSeconds: 5
        livenessProbe:
          httpGet:
            path: /health
            port: 3001
          initialDelaySeconds: 15
          periodSeconds: 10
```

---

## 3. Order Service Deployment

File:

```text
submission/deployments/order-service.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: order-service
spec:
  replicas: 1
  selector:
    matchLabels:
      app: order-service
  template:
    metadata:
      labels:
        app: order-service
    spec:
      containers:
      - name: order-service
        image: order-service:v1
        imagePullPolicy: Never
        ports:
        - containerPort: 3002
        resources:
          requests:
            memory: "128Mi"
            cpu: "100m"
          limits:
            memory: "256Mi"
            cpu: "250m"
        env:
        - name: NODE_ENV
          value: "production"
        readinessProbe:
          httpGet:
            path: /health
            port: 3002
          initialDelaySeconds: 5
          periodSeconds: 5
        livenessProbe:
          httpGet:
            path: /health
            port: 3002
          initialDelaySeconds: 15
          periodSeconds: 10
```

---

## 4. Gateway Service Deployment

File:

```text
submission/deployments/gateway-service.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: gateway-service
spec:
  replicas: 1
  selector:
    matchLabels:
      app: gateway-service
  template:
    metadata:
      labels:
        app: gateway-service
    spec:
      containers:
      - name: gateway-service
        image: gateway-service:v1
        imagePullPolicy: Never
        ports:
        - containerPort: 3003
        resources:
          requests:
            memory: "128Mi"
            cpu: "100m"
          limits:
            memory: "256Mi"
            cpu: "250m"
        env:
        - name: NODE_ENV
          value: "production"
        - name: USER_SERVICE_URL
          value: "http://user-service:3000"
        - name: PRODUCT_SERVICE_URL
          value: "http://product-service:3001"
        - name: ORDER_SERVICE_URL
          value: "http://order-service:3002"
        readinessProbe:
          httpGet:
            path: /health
            port: 3003
          initialDelaySeconds: 5
          periodSeconds: 5
        livenessProbe:
          httpGet:
            path: /health
            port: 3003
          initialDelaySeconds: 15
          periodSeconds: 10
```

---

# Step 7: Create Service YAML Files

## 1. User Service

File:

```text
submission/services/user-service.yaml
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: user-service
spec:
  selector:
    app: user-service
  ports:
  - protocol: TCP
    port: 3000
    targetPort: 3000
  type: ClusterIP
```

---

## 2. Product Service

File:

```text
submission/services/product-service.yaml
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: product-service
spec:
  selector:
    app: product-service
  ports:
  - protocol: TCP
    port: 3001
    targetPort: 3001
  type: ClusterIP
```

---

## 3. Order Service

File:

```text
submission/services/order-service.yaml
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: order-service
spec:
  selector:
    app: order-service
  ports:
  - protocol: TCP
    port: 3002
    targetPort: 3002
  type: ClusterIP
```

---

## 4. Gateway Service

File:

```text
submission/services/gateway-service.yaml
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: gateway-service
spec:
  selector:
    app: gateway-service
  ports:
  - protocol: TCP
    port: 3003
    targetPort: 3003
  type: ClusterIP
```

---

# Step 8: Deploy All Resources

Apply deployments:

```bash
kubectl apply -f submission/deployments/
```

Apply services:

```bash
kubectl apply -f submission/services/
```

---

# Step 9: Verify Deployment

Check pods:

```bash
kubectl get pods
```

Expected:

```bash
NAME                                READY   STATUS
user-service-xxxx                   1/1     Running
product-service-xxxx                1/1     Running
order-service-xxxx                  1/1     Running
gateway-service-xxxx                1/1     Running
```

---

Check services:

```bash
kubectl get svc
```

Expected:

```bash
NAME              TYPE        CLUSTER-IP
gateway-service   ClusterIP   xxx.xxx.xxx.xxx
order-service     ClusterIP   xxx.xxx.xxx.xxx
product-service   ClusterIP   xxx.xxx.xxx.xxx
user-service      ClusterIP   xxx.xxx.xxx.xxx
```

---

# Step 10: Test Inter-Service Communication

## Port Forward Gateway

```bash
kubectl port-forward svc/gateway-service 3003:3003
```

Open new terminal.

---

## Test Users API

```bash
curl http://localhost:3003/api/users
```

Expected:

```json
[
  {
    "id": 1,
    "name": "John Doe"
  }
]
```

---

## Test Products API

```bash
curl http://localhost:3003/api/products
```

---

## Test Orders API

```bash
curl http://localhost:3003/api/orders
```

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

# Step 12: Bonus Task - Ingress Setup 🌐

## Enable Ingress

```bash
minikube addons enable ingress
```

Verify:

```bash
kubectl get pods -n ingress-nginx
```

---

## Create Ingress YAML

File:

```text
submission/ingress/ingress.yaml
```

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: microservices-ingress
spec:
  ingressClassName: nginx
  rules:
  - host: microservices.local
    http:
      paths:
      - path: /api/users
        pathType: Prefix
        backend:
          service:
            name: user-service
            port:
              number: 3000

      - path: /api/products
        pathType: Prefix
        backend:
          service:
            name: product-service
            port:
              number: 3001

      - path: /api/orders
        pathType: Prefix
        backend:
          service:
            name: order-service
            port:
              number: 3002

      - path: /
        pathType: Prefix
        backend:
          service:
            name: gateway-service
            port:
              number: 3003
```

---

## Apply Ingress

```bash
kubectl apply -f submission/ingress/ingress.yaml
```

---

## Add Local DNS Entry

Get Minikube IP:

```bash
minikube ip
```

Example:

```bash
192.168.49.2
```

Edit hosts file:

```bash
sudo nano /etc/hosts
```

Add:

```text
192.168.49.2 microservices.local
```

---

## Test Ingress

```bash
curl http://microservices.local/api/users
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

