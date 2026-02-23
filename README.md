# Lab 6: Automated CI/CD Pipeline with Jenkins & NGINX Load Balancing

## 📌 Overview
This repository contains the configuration and codebase for an automated Continuous Integration and Continuous Deployment (CI/CD) pipeline. The project demonstrates how to orchestrate Docker containers using Jenkins to build, deploy, and manage a backend C++ application securely routed behind an NGINX load balancer.



## 🛠️ Technologies Used
* **CI/CD:** Jenkins (Declarative Pipeline & Freestyle Jobs)
* **Containerization:** Docker & Docker Networks
* **Load Balancing:** NGINX
* **Backend:** C++ (Custom web server)
* **Version Control:** Git & GitHub

## 🏗️ Project Architecture
1. **Jenkins Automation:** A `Jenkinsfile` defines the CI/CD pipeline, automatically pulling code from GitHub and executing build steps.
2. **Dockerized Backends:** The pipeline builds a Docker image from the C++ source code and deploys multiple container instances (`backend1`, `backend2`) onto a custom, isolated Docker network.
3. **NGINX Reverse Proxy:** An NGINX container acts as the entry point on port 80, routing incoming HTTP traffic to the active backend containers.

## 🚀 Key Features Implemented
* **Pipeline as Code:** Complete deployment automation using a `Jenkinsfile` with distinct stages (Build Image, Deploy Backends, Deploy NGINX).
* **Parameterized Jobs:** Dynamic Jenkins builds allowing the user to select the number of backend containers to deploy on the fly.
* **Load Balancing Strategies:** Configured and tested multiple NGINX traffic distribution methods:
  * **Round-Robin (Default):** Sequential traffic distribution across available servers.
  * **Least Connections (`least_conn`):** Routes new requests to the server with the fewest active connections.
  * **IP Hash (`ip_hash`):** Ensures session persistence by consistently routing requests from the same client IP to the same backend container.

## ⚙️ Pipeline Execution
The deployment is fully automated via Jenkins. Triggering the pipeline job in the Jenkins dashboard executes the `Jenkinsfile`, which cleans up old containers, builds the fresh image, provisions the backend infrastructure, and restarts the NGINX load balancer to apply the latest configurations.
