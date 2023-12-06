# Kubernetes Node.js with Nginx Template

![Kubernetes](https://img.shields.io/badge/Kubernetes-Deployed-brightgreen)
![Node.js](https://img.shields.io/badge/Node.js-v14.17.4-green)
![Nginx](https://img.shields.io/badge/Nginx-v1.21.3-green)
![License](https://img.shields.io/badge/license-MIT-blue)

## Overview

This repository serves as a template for deploying a Node.js application with Nginx as a reverse proxy onto Google Kubernetes Engine (GKE) in Google Cloud Platform (GCP). It sets up a scalable and load-balanced environment for your Node.js application using Kubernetes.

## Structure

- `.github/workflows/deploy.yml`: GitHub Actions workflow for CI/CD deployment to Kubernetes.
- `k8s/`: Kubernetes configurations for Nginx and Node.js deployments.
- `nginx/`: Nginx Dockerfile and configuration.
- `nodejs/`: Node.js application with Dockerfile, server setup, and package configuration.
- `.gitignore`: Specifies intentionally untracked files to ignore.
- `README.md`: Documentation and project overview.

## Workflow

### CI/CD Pipeline

The GitHub Actions workflow (`deploy.yml`) automates the deployment process:
- It builds Docker images for Nginx and Node.js apps.
- Sets up Google Cloud SDK for GCP authentication.
- Configures Docker CLI, builds, and pushes Docker images to Google Container Registry.
- Installs `kubectl` plugin and configures Kubernetes context.
- Applies Nginx and Node.js deployments and services.
- Utilizes notifications for successful or failed deployments via Telegram.

### Kubernetes Configurations

- `nginx-deployment.yaml`: Sets up Nginx deployment with 2 replicas.
- `nginx-service.yaml`: Defines a LoadBalancer service for the Nginx deployment.
- `nodejs-deployment.yaml`: Configures Node.js deployment with 2 replicas and autoscaling based on CPU utilization.
- `nodejs-service.yaml`: Specifies a LoadBalancer service for the Node.js deployment.

### Dockerfiles & Application Setup

- `nginx/Dockerfile`: Builds the Nginx Docker image and copies custom configuration.
- `nginx/nginx.conf`: Custom Nginx configuration for proxying requests to the Node.js service.
- `nodejs/Dockerfile`: Builds the Node.js Docker image, installs dependencies, exposes port 3000, and runs the server.
- `nodejs/package.json` & `nodejs/server.js`: Basic setup for a Node.js server.

## Usage

1. Replace the placeholder code in `nodejs/server.js` with your Node.js application logic.
2. Customize the Nginx configuration in `nginx/nginx.conf` if needed.
3. Configure secrets and environment variables in your repository settings for GCP authentication and Telegram notifications.

## Deployment

To deploy this template to your GCP Kubernetes cluster:
1. Fork or clone this repository.
2. Configure the GitHub repository secrets for GCP authentication, Telegram bot token, etc.
3. Push changes to the `main` branch to trigger the CI/CD workflow for deployment.
