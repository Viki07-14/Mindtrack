# 🚀 Trend App -- Production Ready React Application Deployment using DevOps CI/CD

## Project Overview

This project demonstrates an end-to-end DevOps workflow for deploying a
React application on **AWS EKS** using **Docker, Terraform, Jenkins,
Kubernetes, DockerHub, Prometheus and Grafana**.

### Technology Stack

  Category           Technology
  ------------------ ----------------------------------
  Source Control     GitHub
  Application        React
  CI/CD              Jenkins
  IaC                Terraform
  Containerization   Docker & Docker Compose
  Registry           DockerHub (`vikimano/trend-app`)
  Orchestration      Kubernetes (AWS EKS)
  Monitoring         Prometheus & Grafana

## Repository

-   GitHub: https://github.com/Viki07-14/Trendapp

## Project Structure

``` text
Trendapp/
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml
├── k8s/
│   ├── deployment.yaml
│   └── service.yaml
├── terraform/
├── Jenkinsfile
├── .gitignore
├── .dockerignore
└── README.md
```

## Application Setup

``` bash
git clone https://github.com/Viki07-14/Trendapp.git
cd Trendapp
npm install
npm start
```

Application runs on **http://localhost:3000**

## Docker

Build:

``` bash
docker compose -f docker/docker-compose.yml build --no-cache
```

Run:

``` bash
docker compose -f docker/docker-compose.yml up -d
```

Docker Compose:

``` yaml
services:
  trend-app:
    build:
      context: ..
      dockerfile: docker/Dockerfile
    ports:
      - "3001:3000"
    container_name: trend-app
```

DockerHub image:

``` text
vikimano/trend-app
```

## Terraform

``` bash
terraform init
terraform plan
terraform apply
```

Creates AWS infrastructure including VPC, IAM and Jenkins EC2.

## Jenkins CI/CD Pipeline

Pipeline stages:

1.  Checkout source from GitHub
2.  Build Docker image using Docker Compose
3.  Push image to DockerHub
4.  Run application locally
5.  Verify EKS access
6.  Deploy to Kubernetes
7.  Retrieve LoadBalancer hostname

GitHub webhook triggers Jenkins automatically on every push.

## Kubernetes

Deployment image:

``` text
vikimano/trend-app:latest
```

Deploy:

``` bash
kubectl apply -f k8s/
kubectl rollout status deployment/trend-app
kubectl get pods
kubectl get svc
```

Application is exposed through a **LoadBalancer** service.

## Monitoring

Prometheus collects cluster and application metrics.

Grafana provides dashboards for: - Node metrics - Pod metrics - CPU &
Memory - Application health

## Useful Commands

``` bash
kubectl get nodes
kubectl get pods
kubectl get svc
kubectl logs <pod-name>
```

## Version Control

``` bash
git add .
git commit -m "Deployment update"
git push origin main
```

## Project Outcome

-   Automated CI/CD with Jenkins
-   Dockerized React application
-   Images stored in DockerHub
-   Infrastructure provisioned with Terraform
-   Deployment to AWS EKS
-   Monitoring with Prometheus & Grafana
-   Production-ready Kubernetes deployment
