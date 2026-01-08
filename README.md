# NGINX on Amazon EKS using Terraform

## Overview
This project demonstrates a complete DevOps workflow to provision a managed Kubernetes cluster on AWS using Terraform and deploy a simple NGINX application on Amazon EKS. The application is containerized using Docker and exposed publicly using a Kubernetes LoadBalancer service.

This setup showcases Infrastructure as Code (IaC), containerization, Kubernetes deployment, and cloud-native best practices.

---

## Architecture
- Terraform for Infrastructure as Code
- Amazon EKS (Managed Kubernetes)
- Amazon VPC with public and private subnets
- Dockerized NGINX application
- Kubernetes Deployment and Service (LoadBalancer)

---

## Prerequisites
Ensure the following tools are installed and configured:

- AWS CLI (`aws configure` completed)
- Terraform (>= 1.5)
- kubectl
- Docker
- Docker Hub account
- AWS account with EKS permissions

---

## Project Structure
.
├── terraform/
│ ├── main.tf
│ ├── variables.tf
│ └── outputs.tf
├── k8s/
│ ├── deployment.yaml
│ └── service.yaml
├── Dockerfile
├── index.html
└── README.md

---

## Infrastructure Setup (Terraform)

### Step 1: Initialize Terraform
```bash
cd terraform
terraform init
Step 2: Provision EKS Cluster
bash
Copy code
terraform apply
Note: EKS provisioning may take 10–15 minutes.

Configure kubectl
bash
Copy code
aws eks update-kubeconfig \
  --region us-east-1 \
  --name nginx-eks
Verify cluster access:

bash
Copy code
kubectl get nodes

Build and Push Docker Image

docker build -t nginx-app .
docker tag nginx-app YOUR_DOCKERHUB_USERNAME/nginx-app:latest
docker push YOUR_DOCKERHUB_USERNAME/nginx-app:latest
Update the image name in k8s/deployment.yaml accordingly.

Deploy Application to Kubernetes

kubectl apply -f k8s/
Check deployment status:

kubectl get pods
kubectl get svc nginx-service

Access the Application

kubectl get svc nginx-service
Open the EXTERNAL-IP in your browser:

http://<EXTERNAL-IP>
You should see:

Hello World from NGINX on EKS 🚀
