# DevOps CI/CD Platform

## Overview

A production-style DevOps portfolio project demonstrating a complete CI/CD workflow from source code commit to container image delivery.

This project is being built using industry-standard DevOps tools and practices, focusing on automation, containerization, CI/CD pipelines, Kubernetes deployment, and infrastructure management.

## Project Goal

Build an end-to-end CI/CD platform that automates:

Source Code ? Build ? Test ? Docker Image ? Docker Registry ? Kubernetes Deployment

The project is designed to simulate a real-world DevOps environment and showcase practical experience with CI/CD, containerization, Kubernetes, Helm, and cloud infrastructure.

---

## Architecture

GitHub
?
Jenkins Pipeline
?
Docker Build
?
Docker Hub
?
Kubernetes Cluster
?
Helm Deployment

---

## Tech Stack

### Source Control

* Git
* GitHub

### CI/CD

* Jenkins

### Containerization

* Docker
* Docker Hub

### Container Orchestration

* Kubernetes (Upcoming)
* Helm (Upcoming)

### Cloud

* AWS EC2 (Planned)

### Operating System

* Ubuntu Linux

---

## Features Implemented

### CI Pipeline

* Source code managed in GitHub
* Automated Jenkins pipeline
* Dependency installation using containerized Node.js build environment
* Docker image creation
* Automated Docker Hub image publishing

### Containerization

* Custom Dockerfile
* Optimized Docker image build process
* Docker Hub integration

### Security

* Docker Hub access token authentication
* Jenkins credential management

---

## Challenges Faced

### Jenkins Docker Integration

* Docker CLI unavailable inside Jenkins container
* Resolved by mounting Docker binary and Docker socket

### Container Workspace Mapping

* Jenkins workspace path differed from host filesystem path
* Corrected volume mappings for containerized builds

### Docker Hub Credential Scope

* Jenkins pipeline could not access user-scoped credentials
* Resolved using Global Credentials Store

### CI Build Failures

* Debugged package installation failures caused by incorrect workspace mounts
* Validated Docker volume mappings manually before pipeline execution

---

## Current Status

### Completed

* GitHub Repository
* Dockerized Application
* Jenkins Setup
* Jenkins Pipeline
* Docker Hub Integration
* Automated Image Publishing

### In Progress

* Kubernetes Deployment Manifests
* Service Configuration
* Helm Charts

### Planned

* Kubernetes Cluster on AWS EC2
* Automated Deployment from Jenkins to Kubernetes
* Ingress Configuration
* Rolling Updates
* Helm-Based Releases

---

## Repository Structure

devops-cicd-platform/

+-- app/

+-- docker/

+-- docs/

+-- helm/

+-- jenkins/

+-- kubernetes/

---

## Author

Mritunjay Bhagat

DevOps Engineer | Full Stack Developer

Linux • Docker • Jenkins • Kubernetes • AWS • Terraform


## Challenges Faced

### 1. Jenkins Container Could Not Access Docker

* Jenkins was deployed inside a Docker container.
* Docker socket was mounted, but Docker CLI was not available inside the Jenkins container.
* Resolved by mounting the host Docker binary and validating Docker access from Jenkins.

### 2. Node.js Dependencies Failed During CI Build

* Jenkins pipeline failed with `npm: not found`.
* Instead of installing Node.js directly inside Jenkins, dependencies were installed using a dedicated Node.js Docker container.
* This ensured a reproducible and containerized build process.

### 3. Jenkins Workspace vs Host Filesystem Path Issues

* Docker commands executed by Jenkins use the host Docker daemon.
* Jenkins workspace paths inside the container differed from actual host paths.
* Identified and corrected volume mount mappings after manually validating workspace locations and Docker mounts.

### 4. Docker Compose Configuration Errors

* Incorrect YAML formatting caused Docker Compose validation failures.
* Troubleshooting involved validating compose syntax and correcting volume definitions.

### 5. Git Workflow Issues

* Jenkins continued using older pipeline configurations because local changes were not committed and pushed to GitHub.
* Reinforced the importance of verifying Git status, commits, and repository synchronization during CI/CD troubleshooting.

### 6. Jenkins Credential Scope Issue

* Docker Hub credentials were initially created under the Jenkins user credential store.
* Pipeline failed with `Could not find credentials entry with ID 'dockerhub-credentials'`.
* Root cause analysis showed the credential scope was not accessible to pipeline execution.
* Resolved by creating the credential in the Global Credentials store and referencing it through Jenkins `credentialsId`.

