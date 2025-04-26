# 🚀 Cloud-Native-Deployment-on-EKS

This project demonstrates how to containerize a simple application, push it to AWS Elastic Container Registry (ECR), and deploy it on a Kubernetes cluster using Amazon Elastic Kubernetes Service (EKS).

<img width="1285" alt="Screenshot 2025-04-08 at 12 59 29 PM" src="https://github.com/user-attachments/assets/b96a5ce4-b9be-4484-8a88-fdcba14287d0" />




---

## 🛠️ Tech Stack

- Docker 🐳
- Amazon EKS ☁️
- Amazon ECR 🗃️
- Kubernetes (kubectl) ⚙️
- EC2 (for provisioning and managing the setup)

---


## ✅ Prerequisites

Before deploying, ensure the following:

- AWS CLI, kubectl, eksctl, and Docker are installed ✅
- AWS credentials are configured (`aws configure`) ✅
- An EKS Cluster is created and ready (`kubectl get nodes`) ✅
- Docker is running and you’re logged in to ECR ✅

---
# Instance

<img width="1440" alt="Screenshot 2025-04-07 at 8 56 20 PM" src="https://github.com/user-attachments/assets/d702798f-9824-4ac1-b857-0ed9d3bb1df4" />



# Cluster Creation & Nodes
<img width="1440" alt="Screenshot 2025-04-09 at 10 22 07 PM" src="https://github.com/user-attachments/assets/e3631731-f836-4dbc-bcac-12aa88615fc0" />

# Build the Image using Docker 

<img width="1440" alt="Screenshot 2025-04-09 at 10 52 32 PM" src="https://github.com/user-attachments/assets/bf3615e8-a466-4d43-bed0-50b14730f5fe" />

# Push the Image to ECR

<img width="858" alt="Screenshot 2025-04-09 at 11 01 33 PM" src="https://github.com/user-attachments/assets/d2b90280-c87d-45f2-ba7b-38662cb921a3" />


# Apply deployment.yaml & Service.yaml

<img width="1440" alt="Screenshot 2025-04-09 at 11 06 34 PM" src="https://github.com/user-attachments/assets/e337f62e-a686-4d40-b3e7-51e004040899" />

# Access the Application

<img width="1440" alt="Screenshot 2025-04-08 at 12 05 33 AM" src="https://github.com/user-attachments/assets/ed75e03a-05b2-4cd7-9306-63420f37dfe9" />



## 🚧 Setup Instructions

### 1. 🔧 Clone the Repository

```bash
git clone https://github.com/your-username/aws-eks-docker-app-deployment.git
cd aws-eks-docker-app-deployment

# Create ECR repository
aws ecr create-repository --repository-name hello-app --region ap-south-1

# Authenticate Docker with ECR
aws ecr get-login-password --region ap-south-1 | \
docker login --username AWS --password-stdin <your-account-id>.dkr.ecr.ap-south-1.amazonaws.com

# Build Docker image
docker build -t hello-app .

# Tag image for ECR
docker tag hello-app:latest <your-account-id>.dkr.ecr.ap-south-1.amazonaws.com/hello-app:latest

# Push image to ECR
docker push <your-account-id>.dkr.ecr.ap-south-1.amazonaws.com/hello-app:latest

kubectl apply -f deployment.yaml
kubectl get pods

kubectl apply -f service.yaml
kubectl get svc hello-app

http://<EXTERNAL-IP>
