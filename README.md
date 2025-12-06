# Cloud-Native To-Do App on AWS EKS

![Python](https://img.shields.io/badge/Python-3.9-blue?logo=python)
![Flask](https://img.shields.io/badge/Flask-2.0-green?logo=flask)
![Docker](https://img.shields.io/badge/Docker-Container-blue?logo=docker)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestration-326ce5?logo=kubernetes)
![AWS EKS](https://img.shields.io/badge/AWS-EKS-orange?logo=amazon-aws)
![Prometheus](https://img.shields.io/badge/Prometheus-Monitoring-e6522c?logo=prometheus)

##  Overview
This project is a full-stack **Cloud-Native Web Application** designed to demonstrate the lifecycle of modern containerized deployments. The application is a "To-Do" manager built with **Flask (Python)** and **MongoDB**, containerized using **Docker**, and orchestrated on **Kubernetes**.

The infrastructure supports both local development (Minikube) and production-grade cloud deployment on **Amazon EKS (Elastic Kubernetes Service)**. It features advanced orchestration capabilities including automated health monitoring, zero-downtime rolling updates, and alerting pipelines.

##  Architecture
* **Frontend/Backend:** Python Flask Application serving a web UI.
* **Database:** MongoDB with Persistent Volume Claims (PVC) for data durability.
* **Container Registry:** Docker Hub for image versioning and distribution.
* **Orchestration:**
    * **Local:** Minikube cluster for testing.
    * **Cloud:** AWS EKS (Elastic Kubernetes Service) with LoadBalancers.
* **Observability:** Prometheus & AlertManager integrated with Slack for real-time notifications.

##  Key Features Implemented

### 1. High Availability & Resilience
* **Replication Controllers:** Configured to ensure a specific number of pod replicas are always running. Tested by manually deleting pods to verify auto-recovery .
* **Persistent Storage:** MongoDB data is persisted using Kubernetes Volumes, ensuring data survives container restarts.

### 2. Zero-Downtime Deployment
* **Rolling Updates:** Implemented a rolling update strategy with controlled `maxUnavailable` parameters. This allows the application to update from v1 to v2 without service interruption.

### 3. Self-Healing Systems
* **Liveness Probes:** Detects if the application has crashed or deadlocked and restarts the container automatically.
* **Readiness Probes:** Ensures traffic is not sent to a pod until it is fully started and ready to accept requests.

### 4. Monitoring & Alerting
* **Prometheus Integration:** scrapes metrics from the Kubernetes cluster.
* **Slack Alerts:** Configured AlertManager to trigger Slack notifications for critical events, such as `KubePodCrashLooping` or high CPU usage.

---

##  Project Structure

```text
cloud-native-todo-app/
├── app/                        # Application Source Code
│   ├── app.py                  # Flask Application with Health Endpoints
│   ├── Dockerfile              # Multi-stage Docker build instructions
│   ├── requirements.txt        # Python dependencies
│   ├── static/                 # CSS/JS Assets
│   └── templates/              # HTML Templates
├── k8s/                        # Kubernetes Manifests
│   ├── local-minikube/         # Deployments for local testing
│   ├── aws-eks/                # Production manifests (LoadBalancer, EKS)
│   ├── controllers/            # Replication Controllers & Rolling Update configs
│   └── monitoring/             # Prometheus & AlertManager configurations
├── docker-compose.yaml         # For local Docker testing without K8s
└── README.md
