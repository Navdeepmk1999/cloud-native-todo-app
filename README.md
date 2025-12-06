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
* [cite_start]**Frontend/Backend:** Python Flask Application serving a web UI[cite: 160].
* [cite_start]**Database:** MongoDB with Persistent Volume Claims (PVC) for data durability[cite: 175].
* [cite_start]**Container Registry:** Docker Hub for image versioning and distribution[cite: 156].
* **Orchestration:**
    * [cite_start]**Local:** Minikube cluster for testing[cite: 296].
    * [cite_start]**Cloud:** AWS EKS (Elastic Kubernetes Service) with LoadBalancers.
* [cite_start]**Observability:** Prometheus & AlertManager integrated with Slack for real-time notifications[cite: 962].

##  Key Features Implemented

### 1. High Availability & Resilience
* **Replication Controllers:** Configured to ensure a specific number of pod replicas are always running. [cite_start]Tested by manually deleting pods to verify auto-recovery [cite: 604-607].
* [cite_start]**Persistent Storage:** MongoDB data is persisted using Kubernetes Volumes, ensuring data survives container restarts[cite: 100].

### 2. Zero-Downtime Deployment
* **Rolling Updates:** Implemented a rolling update strategy with controlled `maxUnavailable` parameters. [cite_start]This allows the application to update from v1 to v2 without service interruption[cite: 831].

### 3. Self-Healing Systems
* [cite_start]**Liveness Probes:** Detects if the application has crashed or deadlocked and restarts the container automatically[cite: 888].
* [cite_start]**Readiness Probes:** Ensures traffic is not sent to a pod until it is fully started and ready to accept requests[cite: 950].

### 4. Monitoring & Alerting
* **Prometheus Integration:** scrapes metrics from the Kubernetes cluster.
* [cite_start]**Slack Alerts:** Configured AlertManager to trigger Slack notifications for critical events, such as `KubePodCrashLooping` or high CPU usage[cite: 1071, 1136].

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
