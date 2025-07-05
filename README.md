# 🛍️ Sintara Shop - Cloud Native E-commerce App

A full-stack microservices-based e-commerce application built with Docker, Kubernetes, and CI/CD using GitHub Actions.

---

## 📐 Architecture Overview
```
+-----------------+
|  Frontend (UI)  |
| React / Express |
+--------+--------+
         |
         v
+--------+--------+
|   API Gateway   |
| Node.js / Express|
+--------+--------+
         |
 +-------+--------+
 |                |
+------+-----+  +--------+
| Product API |  | MongoDB |
+------------+  +--------+
```

---

## 🚀 Tech Stack
- **Frontend:** Express.js
- **API Gateway:** Node.js
- **Product Service:** Python + Flask
- **Database:** MongoDB
- **Containerization:** Docker
- **Orchestration:** Kubernetes (Minikube)
- **CI/CD:** GitHub Actions

---

## 🛠️ Setup Instructions

1. **Install prerequisites:** Docker, Minikube, kubectl, Node.js ≥ 18, Python ≥ 3.9
2. **Clone the repo:**
   ```bash
   git clone https://github.com/Dasmat13/Sintara-Shop-Cloud-Native-E-commerce-App.git
   ```
3. **Build Docker Images:**
   ```bash
   docker build -t dasmat/frontend:latest ./frontend
   docker build -t dasmat/api-gateway:latest ./api-gateway
   docker build -t dasmat/product-service:latest ./product-service

   docker push dasmat/frontend:latest
   docker push dasmat/api-gateway:latest
   docker push dasmat/product-service:latest
   ```
4. **Deploy to Minikube:**
   ```bash
   minikube start
   kubectl apply -f k8s-manifests/
   ```

---

## 🌐 Port Mappings
| Service          | Cluster Port | NodePort | Description        |
|------------------|--------------|----------|--------------------|
| API Gateway      | 8080         | 30080    | Handles all requests |
| Frontend         | 80           | 32037    | Web UI             |
| Product Service  | 5000         | -        | Backend API        |
| MongoDB          | 27017        | -        | NoSQL Database     |

**Access the app:**
```
http://<minikube-ip>:32037
```

---

## 🔁 CI/CD with GitHub Actions

On push to the `main` branch, Docker images are built and pushed to Docker Hub.

### Sample Workflow
```yaml
name: Docker CI/CD for dasmat

on:
  push:
    branches: [ main ]

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout repository
      uses: actions/checkout@v3

    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2

    - name: Login to Docker Hub
      run: echo "$DOCKER_PASSWORD" | docker login -u "dasmat" --password-stdin

    - name: Build and Push Frontend
      run: |
        docker build -t dasmat/frontend:latest ./frontend
        docker push dasmat/frontend:latest

    - name: Build and Push Product Service
      run: |
        docker build -t dasmat/product-service:latest ./product-service
        docker push dasmat/product-service:latest

    - name: Build and Push API Gateway
      run: |
        docker build -t dasmat/api-gateway:latest ./api-gateway
        docker push dasmat/api-gateway:latest
```

---

## 📎 Useful Commands
- `minikube ip`
- `kubectl get pods`
- `kubectl get svc`
- `kubectl apply -f k8s-manifests/`
- `kubectl logs deployment/<name>`

---

## 📃 License
MIT © Dasmat
