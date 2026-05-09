# Self-Healing Kubernetes System

## Project Overview
This project demonstrates Kubernetes self-healing capabilities using Flask, Docker, Jenkins, and Minikube.

The application includes health endpoints and failure simulation endpoints. Kubernetes uses liveness and readiness probes to detect failures and automatically restart containers.

## Tech Stack
- Python (Flask)
- Docker
- Kubernetes
- Minikube
- Jenkins
- Git & GitHub
- Docker Hub

## Project Structure
self-healing-k8s/
├── app.py
├── requirements.txt
├── Dockerfile
├── deployment.yaml
├── service.yaml
├── Jenkinsfile
└── README.md

## Application Endpoints
- `/` → Home page
- `/health` → Returns application health
- `/fail` → Makes application unhealthy
- `/recover` → Restores healthy state
- `/crash` → Forces application crash

## Kubernetes Self-Healing Features
- Liveness probe automatically restarts unhealthy containers
- Readiness probe removes unhealthy pods from service
- Deployment recreates deleted pods
- Multiple replicas provide high availability

## Build Docker Image
```bash
docker build -t rajbhimani18/self-healing-app:latest .
docker push rajbhimani18/self-healing-app:latest