
# Automated Container Deployment and Administration in AWS

This repository contains a fully automated Continuous Integration/Continuous Deployment (CI/CD) pipeline for deploying a containerized web application on Amazon Web Services (AWS). 
##  Architecture Overview

The system architecture follows a layered automation model:
1. **Developer Push**: Code changes are pushed to the GitHub repository.
2. **CI/CD Trigger**: A GitHub Actions workflow is triggered upon a push to the main branch.
3. **Infrastructure as Code (IaC)**: AWS CloudFormation provisions an EC2 instance (Ubuntu) and configures security groups to open ports 22 (SSH) and 80 (HTTP).
4. **Configuration Management**: The workflow connects to the EC2 instance via a secure SSH connection and executes an Ansible playbook.
5. **Containerization**: Ansible updates system packages, installs Docker, pulls the latest code, and builds a Docker image.
6. **Application Deployment**: A Docker container running an Nginx web application is deployed and exposed on port 80.

##  Technology Stack

* **Cloud Provider**: AWS (EC2, CloudFormation)
* **Configuration Management**: Ansible
* **Containerization**: Docker
* **CI/CD**: GitHub Actions
* **Web Server**: Nginx

##  Repository Structure

* cloudformation/ - Contains the AWS CloudFormation YAML template for provisioning the EC2 instance and Security Groups.
* `ansible/ - Contains the Ansible playbook used to configure the server, install dependencies, and run the Docker container.
* src/ - Contains the sample web application (static HTML files).
* Dockerfile - Instructions for packaging the Nginx web application into a Docker container.
* .github/workflows/ - Contains the YAML workflow file that dictates the GitHub Actions CI/CD pipeline.

## Setup and Deployment Instructions

To use this pipeline in your own environment, follow these steps:

### Prerequisites
* An active AWS Account.
* A GitHub Account.
* An SSH Key pair generated for secure server access.

### Configuration Steps
1. **Fork/Clone the Repository**: Clone this repository to your local machine.
2. **Configure GitHub Secrets**: Go to your repository settings -> Secrets and variables -> Actions. Add the following secrets to allow GitHub Actions to authenticate with AWS and SSH into the EC2 instance:
   * AWS_ACCESS_KEY_ID
   * AWS_SECRET_ACCESS_KEY
   * AWS_REGION (e.g.,us-east-1)
   * SSH_PRIVATE_KEY (Ensure this is properly formatted)
3. **Trigger the Pipeline**: Make a change to the codebase (e.g., update the index.html file) and push the changes to the "main" branch.
4. **Monitor the Build**: Navigate to the "Actions" tab in your GitHub repository to watch the deployment process.
5. **Access the Application**: Once the pipeline completes successfully, navigate to the Public IP address of your newly created EC2 instance in your web browser.

##  Troubleshooting Common Issues

* **SSH Authentication Failures**: If GitHub Actions fails to connect to the EC2 instance, verify that your `SSH_PRIVATE_KEY` secret is formatted correctly with proper line breaks.
* **Port 80 Conflicts**: If the Docker container fails to start, it may be because port 80 is occupied by a previous container. Ensure your Ansible playbook includes steps to stop and remove old containers before starting new ones.
* **Docker Permissions**: If Ansible encounters permission denied errors while running Docker commands, ensure the EC2 user is added to the Docker group in your playbook.

