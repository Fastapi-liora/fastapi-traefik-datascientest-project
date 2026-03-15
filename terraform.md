Infrastructure as Code (IaC) with Terraform

Overview

This project utilizes Terraform to manage the lifecycle of virtual machines on a Proxmox VE server. By using the "Infrastructure as Code" paradigm, we ensure that our hardware resources are version-controlled, reproducible, and documented within the codebase.

Technical Implementation

The configuration uses the bpg/proxmox provider to communicate with the Proxmox API.

Managed Resources

Production VM (ID 102): A pre-existing Ubuntu virtual machine that serves as our primary development environment. It has been imported into the Terraform state to allow for configuration management of its hardware parameters (e.g., 8 GB RAM, 4 vCPUs).

Test VM (ID 104): An automated clone of the production VM. This instance is used for testing deployments and CI/CD pipelines without risking the stability of the production environment. It is configured with 2 vCPUs and 4 GB RAM.

Key Features

Automated Cloning: Terraform handles the full cloning process, ensuring the test environment is a bit-for-bit replica of the production base.

Cloud-Init Integration: SSH public keys are automatically injected during provisioning to allow passwordless access for Ansible and administrative tasks.

State Management: The infrastructure state is tracked in a local terraform.tfstate file (excluded from Git for security), ensuring Terraform knows exactly which resources are currently active.

Usage Commands

To manage the infrastructure from a local machine:

# Initialize the provider and download plugins
terraform init

# Preview changes before applying
terraform plan

# Deploy or update the infrastructure
terraform apply

# Import an existing VM into the state
terraform import proxmox_virtual_environment_vm.fastapi_vm <node>/qemu/102


Benefits

Scalability: New test environments can be deployed in minutes by duplicating resource blocks.

Consistency: Eliminates "configuration drift" by defining hardware in code rather than through manual GUI clicks.
