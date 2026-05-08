This project demonstrates a production-style DevOps pipeline that integrates automated code quality scanning and continuous deployment using Jenkins and AWS services.

🚀 Project Overview

This repository implements a complete CI/CD workflow:

* Developer pushes code to GitHub
* Jenkins triggers the pipeline automatically using GitHub Webhooks
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
Slack Notifications
          ↓
     Docker Build
          ↓
    Push to AWS ECR
          ↓
 Deploy to AWS ECS
          ↓
 Running ECS Service
       ↓
 Slack Notifications
    

 
🛠️ Technologies Used
CI/CD Tools
* Jenkins
* GitHub
* GitHub Webhooks
* SonarQube
* Checkstyle
* Cloud & Containers
* Docker
* AWS ECR
* AWS ECS
* AWS IAM
Build Tools
* Maven
* Java
DevOps Concepts
* Continuous Integration
* Continuous Deployment
* Static Code Analysis
* Containerization
* Infrastructure Automation
📂 Repository Structure
ECS-JenkinsCI-CD/
* │
* ├── Jenkinsfile
* ├── Dockerfile
* ├── pom.xml
* ├── src/
* ├── target/
* ├── README.md

  
⚙️ Prerequisites
Before running this project, ensure you have:
* AWS Account
* Jenkins Server
* Docker Installed
* Java JDK Installed
* Maven Installed
* SonarQube Server
* AWS CLI Configured
* ECR Repository Created
* ECS Cluster Created
* Task definition Created
* ECS Service Created
🔐 AWS IAM Permissions

The Jenkins server or IAM role should have permissions for:

AmazonEC2ContainerRegistryFullAccess
AmazonECS_FullAccess
CloudWatchLogsFullAccess
🔎 Code Quality Integration
✅ Checkstyle

Checkstyle is integrated into the Maven build process to enforce Java coding standards and maintain clean, consistent code quality.

SonarQube is integrated into the Jenkins pipeline for:

* Static code analysis
* Bug detection
* Code smell detection
* Security vulnerability scanning
* Technical debt analysis
* Quality gate enforcement

☁️ Amazon ECR Setup
* Create ECR Repository
* Authenticate Docker to ECR
* Push Docker Image to ECR
☁️ ECS Deployment
ECS Components
* ECS Cluster
* ECS Task Definition
* ECS Service
* Docker Containers
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
Blue/Green ECS Deployments
Kubernetes Migration
GitHub Webhooks
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
