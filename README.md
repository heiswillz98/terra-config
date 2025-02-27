# TODO Application Infrastructure

This repository contains **Terraform** and **Ansible** configurations to provision and deploy a TODO application on **AWS**.

---

## Table of Contents
1. [Requirements](#requirements)
2. [Setup Instructions](#setup-instructions)
3. [Infrastructure Details](#infrastructure-details)
4. [Environment Variables](#environment-variables)
5. [Access the Application](#access-the-application)

---

## Requirements

Before you begin, ensure you have the following installed and configured:

- **Terraform**: [Install Terraform](https://learn.hashicorp.com/tutorials/terraform/install-cli)
- **Ansible**: [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- **AWS CLI**: [Install and Configure AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- **SSH Key Pair**: Create an SSH key pair for the EC2 instance.

---

## Setup Instructions

Follow these steps to set up the infrastructure and deploy the application:

### **1. Clone the Repository**
```bash
git clone https://github.com/heiswillz98/terra-config.git
cd terra-config
cd terraform
terraform init
terraform apply -auto-approve
```

### **2. Deployment Details**
This command will:
✅ **Provision an EC2 instance** on AWS.  
✅ **Configure security groups** to allow SSH, HTTP, and HTTPS traffic.  
✅ **Install Docker, Docker Compose**, and other dependencies on the EC2 instance.  
✅ **Clone the TODO application repository** and deploy it using Docker Compose.

---

## Infrastructure Details

The infrastructure consists of the following components:

### **EC2 Instance**
- **AMI**: Ubuntu 22.04 LTS
- **Instance Type**: `t2.micro` (Free Tier eligible)
- **SSH Access**: Port `22` open to the public
- **Web Access**: Ports `80` (HTTP) and `443` (HTTPS) open to the public

### **Traefik (Reverse Proxy)**
- **SSL/TLS support** for secure HTTPS connections
- **Automatically redirects HTTP traffic** to HTTPS

---

## Environment Variables

The following environment variables are used in the application:

```bash
JWT_SECRET=<your-jwt-secret>
REDIS_HOST=redis-queue
REDIS_PORT=6379
REDIS_CHANNEL=log_channel
```

These variables are defined in the \`.env\` file and passed to the Docker containers.

---

## Access the Application

Once the deployment is complete, you can access the application using the following URLs:

- **Frontend**: `https://<public-ip>`
- **Auth API**: `https://<public-ip>/api/auth`
- **Todos API**: `https://<public-ip>/api/todos`
- **Users API**: `https://<public-ip>/api/users`
- **Traefik Dashboard**: `http://<public-ip>:8080`

Replace `<public-ip>` with the public IP address of your EC2 instance. You can find the public IP in the Terraform output or in the AWS Management Console.

