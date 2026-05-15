# End-to-End CI/CD Pipeline on Amazon EKS using Jenkins, Docker, Helm & Kubernetes

## Overview

This project demonstrates a complete enterprise-style CI/CD pipeline for deploying a Java web application to Amazon EKS using Jenkins, Docker, Helm, Kubernetes, and AWS services.

The pipeline automates the full software delivery lifecycle:

* Building the application using Maven
* Running unit tests and static code analysis
* Performing SonarQube quality checks
* Uploading build artifacts to Nexus Repository
* Building Docker images
* Pushing images to DockerHub
* Deploying applications to Amazon EKS using Helm
* Exposing applications using NGINX Ingress Controller and Route53 DNS

---

# Architecture

```text
GitHub
   ↓
Jenkins CI/CD Pipeline
   ↓
Maven Build & Testing
   ↓
SonarQube Analysis
   ↓
Nexus Artifact Repository
   ↓
Docker Image Build
   ↓
DockerHub Registry
   ↓
Helm Deployment
   ↓
Amazon EKS Cluster
   ↓
NGINX Ingress Controller
   ↓
Route53 DNS
   ↓
Public Application Access
```

---

# Technologies Used

## CI/CD

* Jenkins
* Maven
* SonarQube
* Nexus Repository
* Slack Notifications

## Containerization & Orchestration

* Docker
* Kubernetes
* Helm
* Amazon EKS
* NGINX Ingress Controller

## AWS Services

* Amazon EKS
* EC2
* Route53
* IAM
* Elastic Load Balancer (ELB)

## Application Stack

* Java
* Spring Boot
* MySQL
* RabbitMQ
* Memcached

---

# Features

* Automated CI/CD pipeline using Jenkins
* Dockerized Java application
* Kubernetes deployment using Helm charts
* Ingress-based application exposure
* Route53 DNS integration
* Automated application deployment to Amazon EKS
* SonarQube code quality analysis
* Nexus artifact management
* Slack pipeline notifications
* Kubernetes service discovery for microservices communication

---

# Project Structure

```text
EKS-Jenkins-CI-CD/
│
├── Docker-files/
│   └── app/multistage/Dockerfile
│
├── helm/
│   └── vproappcharts/
│       ├── Chart.yaml
│       ├── values.yaml
│       └── templates/
│
├── kubernetes/
│   └── vpro-app/
│
├── src/
│
├── userdata/
│
├── Jenkinsfile
├── pom.xml
├── settings.xml
└── README.md
```

---

# Jenkins Pipeline Stages

## Build

Builds the Java application using Maven.

```bash
mvn clean install -DskipTests
```

---

## Test

Runs unit tests.

```bash
mvn test
```

---

## Checkstyle Analysis

Performs static code analysis.

```bash
mvn checkstyle:checkstyle
```

---

## SonarQube Analysis

Analyzes code quality and technical debt.

---

## Quality Gate

Waits for SonarQube quality gate validation.

---

## Upload Artifact

Uploads WAR artifact to Nexus Repository.

---

## Build App Image

Builds Docker image using a multistage Dockerfile.

---

## Upload App Image

Pushes Docker image to DockerHub.

---

## Deploy to EKS

Deploys the application to Amazon EKS using Helm.

```bash
helm upgrade --install vproapprelease helm/vproappcharts \
--namespace vproappjenkins \
--create-namespace \
--set appimage.repository=tcollins520/vprofileapp \
--set appimage.tag=${BUILD_NUMBER}
```

---

# EKS Cluster Creation

The Amazon EKS cluster was created using eksctl.

```bash
eksctl create cluster \
--name vproapp-jenkins-eks \
--region us-east-1 \
--nodegroup-name workers \
--node-type t3.small \
--nodes 2
```

---

# Install NGINX Ingress Controller

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

helm repo update

helm upgrade --install ingress-nginx ingress-nginx/ingress-nginx \
--namespace ingress-nginx \
--create-namespace
```

---

# Configure Route53 DNS

Create a Route53 CNAME record pointing the application domain to the AWS Load Balancer created by the ingress controller.

Example:

```text
vproappjenkins.tcapp.xyz
```

---

# Kubernetes Service Discovery

The application was updated to use Kubernetes service names:

| Component | Kubernetes Service |
| --------- | ------------------ |
| MySQL     | vprodb             |
| Memcached | vprocache01        |
| RabbitMQ  | vpromq01           |

---

# Application URL

```text
http://vproappjenkins.tcapp.xyz
```

---

# Challenges Solved

This project involved troubleshooting and resolving:

* IAM permission issues
* Kubernetes YAML formatting errors
* Helm templating issues
* Jenkins pipeline failures
* EKS authentication problems
* Kubernetes ingress configuration
* Route53 DNS routing
* Kubernetes service discovery
* MySQL authentication issues
* Kubernetes secret management
* Application configuration migration from ECS to EKS

---

# Future Improvements

* GitOps deployment using Argo CD
* HTTPS using cert-manager and Let's Encrypt
* Monitoring using Prometheus and Grafana
* Horizontal Pod Autoscaler (HPA)
* Terraform infrastructure provisioning
* Blue/Green or Canary deployments

---

# Conclusion

This project demonstrates a production-style CI/CD workflow integrating Jenkins, Docker, Kubernetes, Helm, and Amazon EKS for automated application delivery.

It showcases real-world DevOps practices including:

* Infrastructure orchestration
* Continuous Integration
* Continuous Delivery
* Kubernetes networking
* Service discovery
* Cloud-native deployments
* Automated application lifecycle management

---

# Author

Tina Collins
