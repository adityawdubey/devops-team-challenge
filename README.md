# devops-team-challenge

This monorepo provides a complete setup to deploy a minimalist microservice, SimpleTimeService, on Amazon EKS using Terraform and GitHub Actions for full CI/CD automation.

⚠️ Note: This monorepo is created only for submission purposes. In a real-world production scenario, it is recommended to maintain the infrastructure and service as separate repositories for better modularity, lifecycle management, and security.

# Repository Structure

❏ Terraform-eks-infrastructure 
- https://github.com/adityawdubey/terraform-eks-infrastructure
- Terraform code to provision EKS, VPC, IAM roles, and supporting AWS infrastructure

❏ simple-time-service 
- https://github.com/adityawdubey/simple-time-service
- FastAPI-based microservice with Docker & K8s manifests


## Terraform Infrastructure Overview 
Repo: https://github.com/adityawdubey/terraform-eks-infrastructure

- Automated provisioning of an EKS cluster with VPC, subnets, and managed node groups
- A highly available Multi-AZ VPC with public/private subnets and NAT gateways
- Integration of critical EKS add-ons: CoreDNS, kube-proxy, AWS VPC CNI, and EBS CSI Driver
- Kubernetes RBAC best practices for secure access control
- Automated deployment of add-ons with proper IAM permissions
- Deployed the AWS Load Balancer Controller with full Ingress support
- Configured DNS + ALB Ingress to expose workloads securely
- CI/CD 

## SimpleTimeService 
Repo: https://github.com/adityawdubey/simple-time-service

- A lightweight REST API that returns the current timestamp and the client’s IP.
- FastAPI-based microservice
- Runs as a non-root user
- Lightweight python:3.12-slim Docker image
- Health checks, resource limits, and Kubernetes manifests included
- Dockerized and Kubernetes-ready
- CI/CD 

## Requirements: 

- AWS CLI & Terraform installed
- Docker installed (for local builds)
- kubectl configured with your EKS cluster
- Properly configured GitHub secrets and environment variables (see both repo READMEs)

## How to Deploy

### 1) Terraform infrastructure
Follow steps from terraform-eks-infrastructure/Readme.md to deploy 

### 2) Service K8s deployment
Follow only the Kubernetes Deployment steps from simple-time-service/Readme.md

```
cd simple-time-service
kubectl apply -f k8s-manifests
```


## Further Exploration: 

- Replace Static AWS Secrets with Secure OIDC Authentication
- Enhance your GitHub Actions workflow by adding a step to run unit tests using tools like pytest or unittest before building and deploying the container image.
- Integrate SSL certificates from AWS Certificate Manager (ACM) into your Ingress setup to serve the application over HTTPS. 
- Add Observability with Prometheus, Grafana, or CloudWatch
