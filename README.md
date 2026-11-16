# Terraform: AWS EC2 Web Server with Nginx

Terraform configuration that provisions an Ubuntu EC2 instance on AWS, opens HTTP with a security group, and installs Nginx automatically at boot using user data.

## What it creates

- **Security group** `web-sg`: allows inbound HTTP (port 80) and all outbound traffic
- **EC2 instance** (default `t3.micro`) attached to that security group
- **User data script** that installs Nginx, writes a test page showing the server's hostname, and enables the service

## Requirements

- Terraform 1.5 or later
- AWS credentials configured (for example with `aws configure`)
- An Ubuntu AMI ID for your region

## Usage

```bash
terraform init
terraform plan -var="ami_id=ami-xxxxxxxx"
terraform apply -var="ami_id=ami-xxxxxxxx"
```

Open the instance's public IP in a browser to see the Nginx test page.

Clean up when finished:

```bash
terraform destroy -var="ami_id=ami-xxxxxxxx"
```

## Variables

| Name | Default | Description |
|---|---|---|
| `region` | `us-east-1` | AWS region |
| `ami_id` | none (required) | Ubuntu AMI ID for your region |
| `instance_type` | `t3.micro` | EC2 instance size |

## Files

| File | Purpose |
|---|---|
| `main.tf` | Provider, security group and EC2 instance with user data |
| `variables.tf` | Input variables |
