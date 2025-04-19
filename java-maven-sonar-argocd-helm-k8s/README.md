# CI/CD Pipeline with Jenkins, SonarQube, Docker, Kubernetes & ArgoCD

This project demonstrates a complete CI/CD pipeline for a Spring Boot application using modern DevOps tools and best practices. It automates the entire process from code commit to deployment on a Kubernetes cluster using GitOps.

## 🔧 Tools & Technologies

- **Jenkins** – Build automation and CI/CD pipeline orchestration
- **SonarQube** – Static code analysis and quality scanning
- **Docker** – Containerization of the Spring Boot application
- **DockerHub** – Registry for storing built Docker images
- **Kubernetes** – Deployment and orchestration of containerized workloads
- **ArgoCD** – GitOps-based continuous deployment

## 📌 Pipeline Overview

1. **Code Commit** – Developer pushes code to GitHub.
2. **Jenkins Pipeline** – Automatically triggered:
    - Builds the project using Maven
    - Runs SonarQube analysis
    - Builds a Docker image and pushes to DockerHub
    - Updates the Kubernetes manifests with the new image tag
3. **Git Push** – The updated manifests are committed to GitHub.
4. **ArgoCD Sync** – ArgoCD detects the change and deploys the new version to Kubernetes.

## ✅ Features

- End-to-end automation from code to production
- Static code analysis with SonarQube
- Docker image build and push
- Kubernetes deployment via ArgoCD
- GitOps approach for consistent, version-controlled delivery
- Secure credentials management in Jenkins

## 📁 Directory Structure

├── Jenkinsfile # Declarative Jenkins pipeline 

├── k8s-manifests/ # Kubernetes deployment and service YAMLs 

├── src/ # Java Spring Boot application code 

├── Dockerfile # Docker build configuration 

└── [README.md](http://readme.md/) # Project documentation

## 🚀 How to Run

> This assumes you have Jenkins, Docker, Kubernetes (Minikube or other), SonarQube, and ArgoCD properly set up.
> 
1. Clone the repository:
    
    ```bash
    git clone <https://github.com/waseralkarim/JenkinsProject-EndToEnd-CICD.git>
    ```
    
2. Configure Jenkins:

Set up tools: JDK, Maven, SonarQube Scanner, Docker

Add credentials: GitHub, DockerHub, Kubernetes access

1. Run the pipeline from Jenkins:

The app is built, scanned, containerized, and pushed

Kubernetes manifests are updated and committed back to GitHub

1. ArgoCD:

Automatically detects the changes and deploys the updated app to your cluster
