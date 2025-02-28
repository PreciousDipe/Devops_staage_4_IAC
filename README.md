# AWS EC2 Infrastructure as Code (IaC)

Terraform configuration for provisioning a secure Ubuntu EC2 instance with Ansible provisioning capabilities.

## Key Components

### Infrastructure
- **EC2 Instance** (Ubuntu 22.04 LTS)
- **Security Group** with rules for:
  - SSH (22)
  - HTTP/HTTPS (80, 443)
  - Custom ports (8080-8083)
  - Redis (6379)
  - Full outbound access

### Security
- 🔑 Auto-generated RSA 4096 SSH key pair
- 🔒 Local private key storage with 400 permissions
- 🔐 Terraform-managed credentials

### Provisioning
- 📦 Automated Ansible setup
- 📄 Playbook deployment (`deploy.yml`)
- 📋 Inventory file generation

## Usage

```bash
# Initialize Terraform
terraform init

# Deploy infrastructure (will prompt for confirmation)
terraform apply

# Connect to instance
ssh -i hng.pem ubuntu@$(terraform output -raw instance_ip)

# Destroy resources
terraform destroy
```

## Important Notes
- 🚨 Private key (`hng.pem`) is generated automatically - keep this secure!
- ⚠️ Security group allows public access to multiple ports - adjust for production use
- 🔄 Ansible provisioning runs automatically after instance creation
- 📄 Customize `deploy.yml` for application-specific configuration

## File Structure
- `main.tf` - Core infrastructure configuration
- `provider.tf` - AWS provider setup
- `deploy.yml` - Ansible playbook (executed automatically)