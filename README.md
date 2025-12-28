# 🚀 AWS KinD Tutorial – 3-Tier Application on Kubernetes

This repository demonstrates how to deploy a **3-tier application architecture** on a **multi-node Kubernetes cluster** created using **KinD (Kubernetes in Docker)** and running on an **AWS EC2 instance**.

The project is designed to help beginners and DevOps practitioners understand **real-world Kubernetes concepts** using a simple yet practical setup.

---

## 🧱 Architecture Overview

The application follows a classic **3-tier architecture**:

### 1️⃣ Database Layer
- **MongoDB**
- Deployed as a Kubernetes Deployment
- Exposed internally using a ClusterIP Service
- Credentials managed using Kubernetes Secrets

### 2️⃣ API Layer
- **Python + Flask**
- Exposes REST APIs for CRUD operations on Tutorial data
- Communicates with MongoDB via Kubernetes Service

### 3️⃣ Frontend Layer
- **Node.js**
- Simple UI to perform CRUD operations
- Exposed externally using a **NodePort Service**

---

aws_kind_tutorial_dev/
├── README.md
└── manifest/
├── mongo-secret.yaml
├── mongo-deployment.yaml
├── mongo-service.yaml
├── api-deployment.yaml
├── api-service.yaml
├── frontend-deployment.yaml
└── frontend-service.yaml


---

## ⚙️ Prerequisites

Ensure the following tools are installed on your local system or EC2 instance:

- Docker
- kubectl
- KinD
- Git

Verify installations:
```bash
docker --version
kubectl version --client
kind version

Create a 3-Node KinD Kubernetes Cluster

Create a KinD configuration file named kind-cluster.yaml:

kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker


Create the cluster:

kind create cluster --name kind-3tier-cluster --config kind-cluster.yaml


Verify the cluster:

kubectl get nodes

🔐 Deploy MongoDB (Database Layer)
1. Create MongoDB Secret
kubectl apply -f manifest/mongo-secret.yaml

2. Deploy MongoDB
kubectl apply -f manifest/mongo-deployment.yaml

3. Create MongoDB Service
kubectl apply -f manifest/mongo-service.yaml


Verify:

kubectl get pods
kubectl get svc

🔌 Deploy API Layer (Flask)
1. Deploy API
kubectl apply -f manifest/api-deployment.yaml

2. Create API Service
kubectl apply -f manifest/api-service.yaml


Verify:

kubectl get pods
kubectl get svc

🎨 Deploy Frontend Layer (Node.js)
1. Deploy Frontend
kubectl apply -f manifest/frontend-deployment.yaml

2. Expose Frontend using NodePort
kubectl apply -f manifest/frontend-service.yaml


Check the service:

kubectl get svc frontend

🌐 Access the Application

From your browser:

http://<EC2_PUBLIC_IP>:<NODE_PORT>