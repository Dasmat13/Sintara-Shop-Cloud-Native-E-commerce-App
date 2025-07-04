# Sintara-Shop-Cloud-Native-E-commerce-App

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sintara Shop - Cloud Native E-commerce App</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      line-height: 1.6;
      margin: 0;
      padding: 0;
      background: #f5f5f5;
      color: #333;
    }
    .container {
      max-width: 900px;
      margin: auto;
      background: #fff;
      padding: 2rem;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    h1, h2, h3 {
      color: #2c3e50;
    }
    code, pre {
      background: #eee;
      padding: 0.5em;
      display: block;
      margin: 1em 0;
      overflow-x: auto;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin: 1em 0;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 0.75em;
      text-align: left;
    }
    th {
      background: #f0f0f0;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🛍️ Sintara Shop - Cloud Native E-commerce App</h1>
    <p>A full-stack microservices-based e-commerce application built with Docker, Kubernetes, and CI/CD using GitHub Actions.</p>

    <h2>📐 Architecture Overview</h2>
    <pre>
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
    </pre>

    <h2>🚀 Tech Stack</h2>
    <ul>
      <li>Frontend: Express.js</li>
      <li>API Gateway: Node.js</li>
      <li>Product Service: Python + Flask</li>
      <li>Database: MongoDB</li>
      <li>Containerization: Docker</li>
      <li>Orchestration: Kubernetes (Minikube)</li>
      <li>CI/CD: GitHub Actions</li>
    </ul>

    <h2>🛠️ Setup Instructions</h2>
    <h3>1. Prerequisites</h3>
    <ul>
      <li>Docker</li>
      <li>Minikube</li>
      <li>kubectl</li>
      <li>Node.js ≥ 18</li>
      <li>Python ≥ 3.9</li>
    </ul>

    <h3>2. Clone the Repository</h3>
    <pre>git clone https://github.com/your-username/sintara-shop.git
cd sintara-shop-cloud-native-e-commerce-app</pre>

    <h3>3. Build Docker Images</h3>
    <pre>
docker build -t dasmat/frontend:latest ./frontend
docker build -t dasmat/api-gateway:latest ./api-gateway
docker build -t dasmat/product-service:latest ./product-service

docker push dasmat/frontend:latest
docker push dasmat/api-gateway:latest
docker push dasmat/product-service:latest
    </pre>

    <h3>4. Deploy to Minikube</h3>
    <pre>
minikube start
kubectl apply -f k8s-manifests/
    </pre>

    <h2>🌐 Port Mappings</h2>
    <table>
      <tr><th>Service</th><th>Cluster Port</th><th>NodePort</th><th>Description</th></tr>
      <tr><td>API Gateway</td><td>8080</td><td>30080</td><td>Handles all requests</td></tr>
      <tr><td>Frontend</td><td>80</td><td>32037</td><td>Web UI</td></tr>
      <tr><td>Product Service</td><td>5000</td><td>-</td><td>Backend API</td></tr>
      <tr><td>MongoDB</td><td>27017</td><td>-</td><td>NoSQL Database</td></tr>
    </table>
    <p>Access the app: <code>http://&lt;minikube-ip&gt;:32037</code></p>

    <h2>🔁 CI/CD with GitHub Actions</h2>
    <p>On push to <code>main</code>, the following happens:</p>
    <ul>
      <li>Docker images are built</li>
      <li>Images are pushed to Docker Hub</li>
    </ul>

    <h3>Sample Workflow</h3>
    <pre>
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
      run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "dasmat" --password-stdin

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
    </pre>

    <h2>📎 Useful Commands</h2>
    <pre>
minikube ip
kubectl get pods
kubectl get svc
kubectl apply -f k8s-manifests/
kubectl logs deployment/&lt;name&gt;
    </pre>

    <h2>📃 License</h2>
    <p>MIT © Your Name</p>
  </div>
</body>
</html>
