# GitHub Copilot Instructions

## Project Overview
This project is focused on automated Docker deployment using AWS, Ansible, and Nginx. The architecture includes EC2 instances managed through CloudFormation and applications deployed in Docker containers.

## Developer Workflows
1. **Setting Up the Environment**: Use the provided Ansible playbook to set up the necessary environment on the EC2 instance.
2. **Building Docker Images**: Modify the `Dockerfile` as needed and build images using Docker commands.
3. **Deployment**: Deploy applications using Docker containers on the EC2 instance.

## Project-Specific Conventions
- **Repository Structure**: Follow the existing folder structure for organization. Key folders include `ansible/`, `app/`, and `cloudformation/`.
- **Naming Conventions**: Use descriptive names for Docker images and containers.

## Integration Points
- **Ansible**: The playbook located in `ansible/playbook.yml` automates the setup of the EC2 instance and installs necessary dependencies.
- **CloudFormation**: The `cloudformation/ec2.yml` file defines the infrastructure for the EC2 instance, including security groups and instance types.
- **Docker**: The `app/Dockerfile` specifies how to build the Docker image for the application.

## Additional Notes
- Ensure that the security group allows SSH and HTTP traffic as defined in the CloudFormation template.
- Regularly update the Ansible playbook and Dockerfile to reflect any changes in dependencies or application structure.