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