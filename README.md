This project demonstrates a production-style DevOps pipeline that integrates automated code quality scanning and continuous deployment using Jenkins and AWS services.

🚀 Project Overview

This repository implements a complete CI/CD workflow:

* Developer pushes code to GitHub
* Jenkins triggers the pipeline automatically
* Maven builds the application
* Checkstyle performs code standard validation
* SonarQube runs static code analysis
* Docker image is built
* Image is pushed to Amazon ECR
* Amazon ECS deploys the updated containerized application

🏗️ CI/CD Architecture
Developer Pushes Code
          ↓
        GitHub
          ↓
       Jenkins
          ↓
   Maven Build & Test
          ↓
 Checkstyle Validation
          ↓
 SonarQube Analysis
          ↓
     Docker Build
          ↓
    Push to AWS ECR
          ↓
 Deploy to AWS ECS
          ↓
 Running ECS Service
🛠️ Technologies Used
CI/CD Tools
Jenkins
GitHub
SonarQube
Checkstyle
Cloud & Containers
Docker
AWS ECR
AWS ECS
AWS IAM
Build Tools
Maven
Java
DevOps Concepts
Continuous Integration
Continuous Deployment
Static Code Analysis
Containerization
Infrastructure Automation
📂 Repository Structure
ECS-JenkinsCI-CD/
│
├── Jenkinsfile
├── Dockerfile
├── pom.xml
├── src/
├── target/
├── README.md
└── deployment/
⚙️ Prerequisites

Before running this project, ensure you have:

AWS Account
Jenkins Server
Docker Installed
Java JDK Installed
Maven Installed
SonarQube Server
AWS CLI Configured
ECS Cluster Created
ECR Repository Created
🔐 AWS IAM Permissions

The Jenkins server or IAM role should have permissions for:

AmazonEC2ContainerRegistryFullAccess
AmazonECS_FullAccess
CloudWatchLogsFullAccess
🔎 Code Quality Integration
✅ Checkstyle

Checkstyle is integrated into the Maven build process to enforce Java coding standards and maintain clean, consistent code quality.

Run locally:

mvn checkstyle:check
✅ SonarQube Analysis

SonarQube is integrated into the Jenkins pipeline for:

Static code analysis
Bug detection
Code smell detection
Security vulnerability scanning
Technical debt analysis
Quality gate enforcement

Run SonarQube analysis locally:

mvn sonar:sonar \
  -Dsonar.projectKey=ecs-jenkins-app \
  -Dsonar.host.url=http://<SONAR_SERVER>:9000 \
  -Dsonar.login=<SONAR_TOKEN>
🐳 Docker Commands
Build Docker Image
docker build -t ecs-jenkins-app .
Run Docker Container
docker run -p 8080:8080 ecs-jenkins-app
☁️ Amazon ECR Setup
Create ECR Repository
aws ecr create-repository --repository-name ecs-jenkins-app
Authenticate Docker to ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com
Tag Docker Image
docker tag ecs-jenkins-app:latest <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/ecs-jenkins-app:latest
Push Docker Image
docker push <ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/ecs-jenkins-app:latest
☁️ ECS Deployment
ECS Components
ECS Cluster
ECS Task Definition
ECS Service
Docker Containers
Application Load Balancer (Optional)
Deployment Workflow

Amazon ECS automatically pulls the latest image from ECR and updates the running tasks with minimal downtime.

📊 CI/CD Workflow Summary
Stage	Description
Checkout	Pull latest code from GitHub
Build	Compile Java application
Checkstyle	Validate coding standards
SonarQube	Perform static code analysis
Docker Build	Build container image
ECR Push	Upload image to Amazon ECR
ECS Deploy	Deploy updated containers
✅ Features
End-to-end CI/CD pipeline
Automated code quality validation
SonarQube static analysis integration
Docker containerization
AWS ECS deployment automation
Jenkins pipeline automation
Maven build lifecycle integration
Production-style DevOps workflow
📸 Future Enhancements
Terraform Infrastructure as Code
Jenkins Shared Libraries
Slack Notifications
Blue/Green ECS Deployments
Kubernetes Migration
GitHub Webhooks
AWS CloudWatch Monitoring
Trivy Container Security Scanning
📚 Skills Demonstrated

This project demonstrates hands-on experience with:

Jenkins Pipelines
CI/CD Automation
AWS ECS & ECR
Docker
Maven
SonarQube
Checkstyle
Java Build Automation
Static Code Analysis
DevOps Best Practices

👩🏽‍💻 Author
Tina Collins

GitHub Repository:
ECS-JenkinsCI-CD Repository
