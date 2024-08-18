# Microservice Orchestration with Kubernetes (Yolo)
## Deployment Explanation
## Overview

This document explains the process of deploying an application from a local Minikube environment to Google Cloud Kubernetes Engine (GKE). The application consists of a backend service connected to a MongoDB database and a frontend service.

## Prerequisites
    - Google Cloud Account: Ensure you have an active Google Cloud account if not signin or signup.
    - Billing Enabled: Billing must be enabled on your Google Cloud project.
    - Google Cloud SDK: Installed and configured on your local machine.
    - Kubectl: Installed and configured on your local machine.
    - Minikube: Installed and running on your local machine.

### Installing Minikube
     - For Linux users
   - `curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64`
   - `sudo install minikube-linux-amd64 /usr/local/bin/minikube`

    - To confirm if minikube is installed succesfully, run the following command
   - `minikube version`

    - Expected output
   - `minikube version: v1.33.1`

    - To Start Minikube
   - `minikube start`

    - Check if minikube is running
   - `minikube status`

### Installing Kubectl
    - Run this command
  - `sudo snap install kubectl --classic`

Once all this is set up navigate to your working directory in my case I will navigate to `/home/kevin/devops/IP2/yolo`.

    - Create directory
 - `mkdir manifests`

 Then add the below files inside: 

    - Create three files
 - `touch backend-deployment.yaml`
 - `touch frontend-deployment.yaml`
 - `touch mongodb-deployment.yaml`


Update the files with the deployment content including the service for you to be able to access it over the internet

    - Execute the below comands
- `kubectl apply -f backend-deployment.yaml`
- `kubectl apply -f frontend-deployment.yaml`
- `kubectl apply -f mongodb-deployment.yaml`

This will create `pods`

    - To view if pods and services have been created execute the below command.
- `kubectl get pods`
- `kubectl get services`

    - Incase of an Error run the below command with the deployment name. This will show `logs` or show more infomation about the `pod` created
- `kubectl logs`
- `kubectl describe`

    -   Example
- `kubectl logs frontend-deployment`
