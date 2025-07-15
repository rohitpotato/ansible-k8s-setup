# Kubernetes Cluster Setup Automation

This repository contains Ansible playbooks for automating the setup and configuration of my k3s cluster with essential components and best practices.

Applies manifests from: https://github.com/rohitpotato/k8s-apps

## Overview

The playbook automates the following:
- Installation of required dependencies
- Deployment of core Kubernetes manifests
- Setup of essential cluster components:
  - cert-manager for SSL/TLS certificate management
  - Traefik as the ingress controller with HTTPS redirection
  - ArgoCD for GitOps-based deployment management
  - Application manifests via ArgoCD

## Prerequisites

- Ansible 2.9 or higher
- Target machines should have:
  - SSH access configured
  - Sudo privileges
  - Python installed
- Git access to the k8s-apps repository

## Directory Structure

```
k8s-setup/
├── files/                    # Additional scripts and files
│   └── install-cilium.sh     # Cilium CNI installation script
├── inventory.ini             # Inventory file with target hosts
├── main.yml                  # Main playbook
└── roles/                    # Ansible roles
    ├── install-dependencies/     # Role for installing dependencies
    │   └── tasks/
    │       └── main.yml
    ├── install-k8s-base-manifests/  # Role for deploying base K8s manifests
    │   └── tasks/
    │       └── main.yaml
    └── vault/                    # Role for Vault operations
        └── tasks/
```

## Usage

1. Update the inventory file with your target hosts:
   ```ini
   [vps]
   your-server ansible_host=<IP_ADDRESS> ansible_user=<USER>
   ```

2. Run the playbook:
   ```bash
   ansible-playbook -i inventory.ini main.yml
   ```

## Components Installed

### 1. Core Dependencies
- Container runtime
- Kubernetes components (kubelet, kubeadm, kubectl)
- Required system packages

### 2. Base Kubernetes Manifests
- cert-manager (v1.18.2)
- Traefik middleware for HTTPS redirection
- ArgoCD in the `argocd` namespace
- Base application configurations

### 3. GitOps Configuration
- ArgoCD project setup
- Application configurations
- RBAC settings
- Ingress configurations