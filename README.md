# Logos VPS Setup with Ansible

This repository contains Terraform and Ansible configurations to initialize the logos.fexel.net VPS.

## Structure

- `main.tf` - Terraform configuration for VPS provisioning
- `setup.yaml` - Ansible playbook for VPS initialization
- `inventory.ini` - Ansible inventory file

## Prerequisites

- Ansible installed on your local machine
- SSH access to the VPS with the Terraform SSH key

## Setup Instructions

### 1. Update Inventory

Edit `inventory.ini` to match your VPS IP address or hostname:

```ini
[logos]
logos.fexel.net ansible_user=root ansible_ssh_private_key_file=~/.ssh/hostinger_tf
```

### 2. Run the Playbook

```bash
ansible-playbook -i inventory.ini setup.yaml
```

## What the Playbook Does

1. **System Setup**
   - Updates apt cache
   - Upgrades all packages

2. **Install Packages**
   - Installs Docker and Docker Compose
   - Installs fail2ban

3. **User Management**
   - Creates users: allan and igor
   - Creates home directories with proper ownership

4. **Directory Structure**
   - Creates `/home/username/docker/stacks` directory for each user
   - Creates `/home/username/docker/appdata` directory for each user

5. **Docker Access**
   - Adds both users to the docker group
   - Allows users to run docker commands without sudo

6. **Sudo Access**
   - Grants passwordless sudo access to both users

## Notes

- The playbook uses the Terraform SSH key for initial root access
- Users can run Docker commands directly without `sudo` after login
- Both users have passwordless sudo access for administrative tasks
- All user directories are created with appropriate permissions
