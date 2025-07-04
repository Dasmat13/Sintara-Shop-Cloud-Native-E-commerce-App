<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Sintara Shop - Cloud Native E-commerce App</title>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body class="bg-gray-50 text-gray-800 font-sans">
  <div class="max-w-5xl mx-auto p-6">
    <h1 class="text-4xl font-bold mb-2">🛍️ Sintara Shop</h1>
    <p class="text-lg mb-6">A full-stack microservices-based e-commerce application built with Docker, Kubernetes, and CI/CD using GitHub Actions.</p>

    <h2 class="text-2xl font-semibold mb-2">📐 Architecture Overview</h2>
    <div class="bg-white p-4 rounded shadow mb-6">
      <pre class="whitespace-pre-wrap text-sm font-mono">
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
    </div>

    <h2 class="text-2xl font-semibold mb-2">🚀 Tech Stack</h2>
    <ul class="list-disc list-inside mb-6">
      <li><strong>Frontend:</strong> Express.js</li>
      <li><strong>API Gateway:</strong> Node.js</li>
      <li><strong>Product Service:</strong> Python + Flask</li>
      <li><strong>Database:</strong> MongoDB</li>
      <li><strong>Containerization:</strong> Docker</li>
      <li><strong>Orchestration:</strong> Kubernetes (Minikube)</li>
      <li><strong>CI/CD:</strong> GitHub Actions</li>
    </ul>

    <h2 class="text-2xl font-semibold mb-2">🛠️ Setup Instructions</h2>
    <ol class="list-decimal list-inside mb-6">
      <li>Install prerequisites: Docker, Minikube, kubectl, Node.js ≥ 18, Python ≥ 3.9</li>
      <li>Clone the repo: <code class="bg-gray-100 px-1">git clone https://github.com/your-username/sintara-shop.git</code></li>
      <li>Build Docker Images:
        <pre class="bg-gray-100 p-2 text-sm mt-2">docker build -t dasmat/frontend:latest ./frontend
docker build -t dasmat/api-gateway:latest ./api-gateway
docker build -t dasmat/product-service:latest ./product-service

docker push dasmat/frontend:latest
docker push dasmat/api-gateway:latest
docker push dasmat/product-service:latest</pre>
      </li>
      <li>Deploy to Minikube:
        <pre class="bg-gray-100 p-2 text-sm mt-2">minikube start
kubectl apply -f k8s-manifests/</pre>
      </li>
    </ol>

    <h2 class="text-2xl font-semibold mb-2">🌐 Port Mappings</h2>
    <table class="table-auto w-full mb-6 border border-collapse">
      <thead>
        <tr class="bg-gray-200">
          <th class="border px-4 py-2 text-left">Service</th>
          <th class="border px-4 py-2">Cluster Port</th>
          <th class="border px-4 py-2">NodePort</th>
          <th class="border px-4 py-2">Description</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="border px-4 py-2">API Gateway</td>
          <td class="border px-4 py-2">8080</td>
          <td class="border px-4 py-2">30080</td>
          <td class="border px-4 py-2">Handles all requests</td>
        </tr>
        <tr>
          <td class="border px-4 py-2">Frontend</td>
          <td class="border px-4 py-2">80</td>
          <td class="border px-4 py-2">32037</td>
          <td class="border px-4 py-2">Web UI</td>
        </tr>
        <tr>
          <td class="border px-4 py-2">Product Service</td>
          <td class="border px-4 py-2">5000</td>
          <td class="border px-4 py-2">-</td>
          <td class="border px-4 py-2">Backend API</td>
        </tr>
        <tr>
          <td class="border px-4 py-2">MongoDB</td>
          <td class="border px-4 py-2">27017</td>
          <td class="border px-4 py-2">-</td>
          <td class="border px-4 py-2">NoSQL Database</td>
        </tr>
      </tbody>
    </table>
    <p>Access the app: <code class="bg-gray-100 px-1">http://&lt;minikube-ip&gt;:32037</code></p>

    <h2 class="text-2xl font-semibold mb-2">🔁 CI/CD with GitHub Actions</h2>
    <p>On push to <code class="bg-gray-100 px-1">main</code>, Docker images are built and pushed to Docker Hub.</p>
    <h3 class="text-lg font-semibold mt-4">Sample Workflow</h3>
    <pre class="bg-gray-100 p-4 text-sm overflow-x-auto">
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
      run: echo "$" | docker login -u "dasmat" --password-stdin

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

    <h2 class="text-2xl font-semibold mb-2">📎 Useful Commands</h2>
    <ul class="list-disc list-inside mb-6">
      <li><code>minikube ip</code></li>
      <li><code>kubectl get pods</code></li>
      <li><code>kubectl get svc</code></li>
      <li><code>kubectl apply -f k8s-manifests/</code></li>
      <li><code>kubectl logs deployment/&lt;name&gt;</code></li>
    </ul>

    <h2 class="text-2xl font-semibold mb-2">📃 License</h2>
    <p class="mb-12">MIT © Dasmat</p>
  </div>
</body>
</html>
