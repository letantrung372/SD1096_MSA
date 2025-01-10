# Sample Microservices Application

This repository contains a sample microservices application with frontend and backend services, designed to demonstrate deployment on both Azure and AWS cloud platforms.

## Architecture Overview

The application consists of three main components:
- Frontend Service: React-based web interface
- Backend Service: Node.js REST API
- MongoDB Database: NoSQL database for data persistence

## Repository Structure

```
root/
├── mongodb.yaml                     # MongoDB deployment for Azure
├── README.md                        # This file
└── src/
    ├── azure-pipelines.yml         # Azure Pipeline template
    ├── backend/
    │   ├── Dockerfile              # Backend container image definition
    │   ├── Jenkinsfile             # Jenkins pipeline for AWS deployment
    │   ├── azure-pipelines.yml     # Azure pipeline using template
    │   ├── k8s/
    │   │   └── deployment.yml      # Azure K8s deployment config
    │   ├── package.json            # Node.js dependencies
    │   └── server.js               # Main backend application
    └── frontend/
        ├── Dockerfile              # Frontend container image definition
        ├── Jenkinsfile             # Jenkins pipeline for AWS deployment
        ├── azure-pipelines.yml     # Azure pipeline using template
        ├── k8s/
        │   └── deployment.yml      # Azure K8s deployment config
        ├── package.json            # React dependencies
        └── src/                    # React application source
```
## Building and Deploying

### Azure
1. Create Azure DevOps Pipeline using the YAML files
2. Configure service connections for ARM, ACR and AKS
3. Run the pipeline

### AWS
1. Configure Jenkins with shared library
2. Set up AWS and GitHub credentials in Jenkins
3. Create pipeline jobs using the Jenkinsfiles
4. Run the pipelines
