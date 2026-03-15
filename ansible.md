Configuration Management with Ansible

Overview

While Terraform handles the "virtual hardware," Ansible is responsible for the internal configuration of the operating system. It ensures that the target virtual machines are correctly set up with all necessary runtimes and tools to host our FastAPI application and Kubernetes cluster.

Architecture & Connectivity

Since the virtual machines reside in a private network behind a Proxmox host, Ansible is configured to use a ProxyJump. The control node (local machine) tunnels through the Proxmox server (62.210.89.4) to reach the internal VM IPs (e.g., 10.10.10.51).

Automation Workflow (setup-vm.yml)

The main playbook automates the following high-level tasks:

System Maintenance: Performs a full apt update and upgrade to ensure the OS is secure and up to date.

Container Runtime: Installs the Docker engine and configures user permissions (adding the user to the docker group) to allow container management without sudo.

Kubernetes Environment: * Downloads and installs the minikube binary.

Installs kubectl for cluster interaction.

Installs network dependencies such as socat and conntrack.

Cluster Initialization: Automatically starts a Minikube cluster using the Docker driver with optimized resource allocation (2 GB RAM) to maintain system stability.

Self-Healing: Includes logic to detect and delete corrupted Minikube profiles or stalled clusters before attempting a clean start.

Usage Commands

The configuration is triggered from the local machine:

# Test connectivity to the managed node
ansible fastapivm_test -i inventory.ini -m ping

# Execute the full configuration playbook
ansible-playbook -i inventory.ini setup-vm.yml -K


Benefits

Zero-Touch Deployment: A freshly cloned VM becomes a fully functional Kubernetes node without a single manual command.

Idempotency: The playbook can be run multiple times; Ansible only makes changes if the current state deviates from the defined configuration.

Speed: Reduces the setup time for a complete development stack from hours to under 10 minutes.
