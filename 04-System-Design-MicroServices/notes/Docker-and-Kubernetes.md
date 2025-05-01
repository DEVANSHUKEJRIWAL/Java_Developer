# 🐳 Docker + ☸️ Kubernetes (K8s) – Basics for Microservices

Docker and Kubernetes are essential tools for **packaging, running, and scaling microservices** reliably across environments.

---

## 🧱 What is Docker?

**Docker** is a containerization platform that packages your application and its dependencies into a single unit called a **container**.

###  Why Use Docker?

| Benefit                | Description                                |
|------------------------|--------------------------------------------|
| Environment consistency| Works the same on dev, test, and prod      |
| Easy deployment        | Package once, run anywhere                 |
| Lightweight            | Faster than virtual machines               |
| Version control        | Image versions for rollback or upgrades    |

---

## 🧪 Dockerfile for Spring Boot App

```Dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/myapp.jar myapp.jar
ENTRYPOINT ["java", "-jar", "myapp.jar"]
```

###  Commands

```text
# Build the Docker image
docker build -t myapp .

# Run the container
docker run -p 8080:8080 myapp
```

### 📦 Docker Compose for Microservices
```yaml
version: '3'
services:
  user-service:
    image: my-user-service
    ports:
      - "8081:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=docker
    depends_on:
      - mysql

  mysql:
    image: mysql:8
    environment:
      - MYSQL_ROOT_PASSWORD=root
      - MYSQL_DATABASE=mydb
```
###  Run all services with:
```text
docker-compose up
```

## ☸️ What is Kubernetes?

Kubernetes is an orchestration platform that manages and scales containers in production.

###  Why Kubernetes?
```text
| Benefit         | Description                                   |
|-----------------|-----------------------------------------------|
| Auto-restart    | Automatically restarts failed containers      |
| Auto-scaling    | Adds/removes containers based on load         |
| Rolling updates | Deploy with zero downtime                     |
| Self-healing    | Replaces dead containers automatically        |
```
### 🧪 Basic Kubernetes Concepts
```text
| Term        | Meaning                                           |
|-------------|---------------------------------------------------|
| Pod         | The smallest deployable unit (holds containers)   |
| Deployment  | Manages pods and updates them                     |
| Service     | Exposes pods to the network (internal/external)   |
| ConfigMap   | Externalizes configuration                        |

```
### 📦 Sample Kubernetes Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user-service
spec:
  replicas: 2
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
        image: my-user-service:latest
        ports:
        - containerPort: 8080
```
###  Create and manage:
```text
kubectl apply -f deployment.yml
kubectl get pods
kubectl delete -f deployment.yml
```
### 🔄 Docker vs Kubernetes
```text
| Feature          | Docker                              | Kubernetes                           |
|------------------|-------------------------------------|-------------------------------------|
| Packaging        | Builds and runs single containers   | Orchestrates multiple containers    |
| Scaling          | Manual                              | Auto-scaling supported              |
| Restart on fail  | Manual                              | Self-healing                        |
| Load balancing   | External tools                      | Built-in `Service` resource         |
```
### 🧠 When to Use
```text
| Scenario                        | Recommended Tool           |
|---------------------------------|----------------------------|
| Local dev or single app         | ✅ Docker only             |
| Multiple microservices at scale | ✅ Docker + Kubernetes     |
| Need zero-downtime deployments  | ✅ Kubernetes              |
```