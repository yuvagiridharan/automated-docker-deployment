# Automated Container Deployment and Administration in AWS

This  project repository contains a fully automated Continuous Integration/Continuous Deployment (CI/CD) pipeline for deploying a containerized web application on Amazon Web Services (AWS) without any manual touch during deployment infrastructure . 
##  Architecture Overview

The system architecture follows a layered automation models:
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

## Repository Structure

```text
.
├── .github/
│   └── workflows/
│       └── deploy.yml         # CI/CD Orchestrator: Triggers the automated pipeline on push
├── ansible/
│   ├── devops-key.pem        # SSH Key for EC2 access
│   ├── hosts                 # Ansible inventory file
│   └── playbook.yml          # Configuration: Installs Docker & deploys app
├── app/
│   ├── Dockerfile            # Containerization: Blueprint for the Nginx web server image
│   └── index.html            # Application Code: Your static web application
└── cloudformation/
    └── ec2.yml               # Infrastructure: Provisions the Ubuntu EC2 instance & firewalls
```

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
   **Infrastructure as Code (IaC)**:
    * using AWS service of cloudformation in this project to make service  internal connect together and avoid configuration drift while automate the structure in         all  scripts
    * Using Templates to avoid Human Errors and  make the structure available in all time zone and implementation 
     
3. **Trigger the Pipeline**: Make a change to the codebase from Vs code  by use of command (e.g., update the index.html file) and push the changes to the "main" branch.
   
   git add .
   git commit -m "command to show action part"
   git push origin main
4. **Monitor the Build**: Navigate to the "Actions" tab in your GitHub repository to watch the deployment process.
 
5. **Access the Application**: Once the pipeline completes successfully, navigate to the Public IP address of your newly created EC2 instance in your web browser.
