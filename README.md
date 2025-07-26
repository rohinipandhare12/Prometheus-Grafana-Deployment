# 🚀 Deploy Prometheus and Grafana on Kubernetes using Terraform & Helm

## 📘 Introduction

In modern DevOps, observability is key to ensuring robust infrastructure and application performance. This project automates the deployment of **Prometheus** and **Grafana** on a **Kubernetes cluster** using **Terraform** and **Helm**. It demonstrates Infrastructure as Code (IaC) to streamline monitoring stack deployment and management.

---

## 🎯 Objectives

- ✅ Provision a Kubernetes cluster using **Terraform**
- ✅ Install and configure **Helm** for package management
- ✅ Deploy **Prometheus** and **Grafana** using Helm charts
- ✅ Connect Grafana to Prometheus for real-time metric visualization
- ✅ Automate the entire setup using Terraform

---

## 🧰 Technology Stack

| Component       | Tool/Version       |
|----------------|--------------------|
| OS             | Ubuntu 22.04       |
| Container Engine | Docker            |
| Kubernetes     | Minikube (local)   |
| IaC Tool       | Terraform           |
| Package Manager| Helm                |
| Monitoring     | Prometheus          |
| Visualization  | Grafana             |

---

## ⚙️ Requirements

- Ubuntu (local or cloud-based)
- Docker
- Minikube or Kubernetes (EKS/AKS/GKE)
- Terraform
- `kubectl`
- Helm

---

## 📊 Architecture Diagram

+------------------------------------------------------------+
| Terraform (IaC) |
| - Provisions cluster (Minikube/EKS) |
| - Deploys Helm charts for Prometheus and Grafana |
+----------------------------+-------------------------------+
|
v
+------------------------------------------------------------+
| Kubernetes Cluster (Minikube / EKS) |
| |
| +-------------------+ +-------------------------+ |
| | Prometheus Pod | <----> | Monitored Applications | |
| | (Helm Chart) | +-------------------------+ |
| | - Scrapes metrics | |
| | - Exposes 9090 | |
| +-------------------+ |
| |
| +-------------------+ |
| | Grafana Pod | |
| | (Helm Chart) | |
| | - Connects to | |
| | Prometheus | |
| | - Dashboards on | |
| | port 3000 | |
| +-------------------+ |
+------------------------------------------------------------+

      ^                               
            | Port-forward or LoadBalancer 
+----------------------------+
| Developer Machine |
| - kubectl, Helm, Terraform|
| - Access Prometheus (9090)|
| - Access Grafana (3000) |
+----------------------------+



---

## 🛠️ Implementation Steps

1. **System Setup**

   sudo apt update && sudo apt upgrade -y
   sudo apt install docker.io -y
   sudo apt install -y curl wget apt-transport-https
Install Kubernetes Tools

Install kubectl

Install minikube

Install helm

Install terraform

Start Kubernetes Cluster


minikube start
Add Helm Repositories

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
Deploy Prometheus & Grafana


kubectl create namespace monitoring
helm install prometheus prometheus-community/prometheus -n monitoring
helm install grafana grafana/grafana -n monitoring
Access Dashboards


kubectl port-forward svc/prometheus-server 9090:80 -n monitoring
kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode
kubectl port-forward svc/grafana 3000:80 -n monitoring
Automate via Terraform

Use Terraform configuration to automate Helm releases for Prometheus and Grafana.

Example structure:


terraform/
├── main.tf
├── providers.tf
└── values/
    ├── prometheus-values.yaml
    └── grafana-values.yaml

✅ Results
Prometheus successfully scrapes metrics and serves on port 9090.

Grafana is configured to use Prometheus as a data source and accessible on port 3000.

Dashboards provide real-time visibility into Kubernetes workloads.

🧾 Conclusion
This project demonstrates how Terraform and Helm can be combined to automate observability stack deployment on Kubernetes.
Prometheus and Grafana enhance the visibility and monitoring capabilities, ensuring high availability and performance of applications in the cluster.
