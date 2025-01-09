# CI/CD Setup for MSA Application Repository

## 1. Introduction

This document provides detailed instructions for setting up CI/CD pipelines for an MSA (Microservices Architecture) application repository using Azure DevOps. The setup ensures seamless integration, deployment, and resource management for backend, frontend, and database components.

## 2. CI/CD Pipeline (Azure DevOps)

### Setup Steps:

1. **Create Azure DevOps Project**\
   Create a new project in Azure DevOps to manage the CI/CD pipelines for the MSA application.

2. **Configure Service Connections**\
   Set up service connections to enable Azure DevOps to interact with Azure services such as ACR, AKS, and ARM.

3. **Import Pipeline Definitions**\
   Add the pipeline definitions from the repository to the Azure DevOps project and link them with the configured service connections.

### Configure Service Connections

#### 1. ACR Service Connection

The ACR service connection allows Azure DevOps to push and pull images from the Azure Container Registry.

**Steps to Configure:**\
Navigate to **Project Settings** > **Service connections** in Azure DevOps. Create a new service connection of type **Azure Resource Manager**, select the subscription containing the ACR, and choose the resource group where the ACR is located. Finally, grant permissions to pipelines to use this connection.

#### 2. AKS Service Connection

The AKS service connection enables Azure DevOps to interact with the AKS cluster for deployment.

**Steps to Configure:**\
Go to **Project Settings** > **Service connections** in Azure DevOps. Create a new service connection of type **Kubernetes**, provide the cluster name, namespace, and credentials, and grant pipeline permissions to use the connection.

#### 3. ARM Service Connection

The ARM service connection facilitates interaction with Azure Resource Manager (ARM) for managing resources.

**Steps to Configure:**\
Navigate to **Project Settings** > **Service connections** in Azure DevOps. Create a new service connection of type **Azure Resource Manager**, select the subscription and resource group to manage, and grant permissions to pipelines to use the connection.

### Pipeline Structure

```
root  
├── mongodb.yaml                     # Deployment file for MongoDB  
└── src  
    ├── azure-pipelines.yml          # Azure Pipeline template  
    ├── backend  
    │   ├── azure-pipeline.yml       # Pipeline for backend (uses template)  
    │   ├── Dockerfile               # Dockerfile for backend service  
    │   └── k8s  
    │       └── deployment.yml       # Deployment file for backend  
    └── frontend  
        ├── azure-pipeline.yml       # Pipeline for frontend (uses template)  
        ├── Dockerfile               # Dockerfile for frontend service  
        └── k8s  
            └── deployment.yml       # Deployment file for frontend  
```

### Pipeline Stages

1. **Build Docker Image and Push to ACR**\
   Build a Docker image using the provided Dockerfile. Tag the image with the current build number or Git commit SHA. Push the built image to an Azure Container Registry (ACR).

2. **Deploy to AKS**\
   Deploy the application (backend, frontend, and MongoDB) to an AKS cluster using the respective Kubernetes manifest files (`deployment.yml`).

3. **Cleanup**\
   Retain the last 5 images in the ACR and remove older images to free up storage space.

