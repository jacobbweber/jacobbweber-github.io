---
layout: post
title: Cheat Sheets
icon: fas fa-info-circle
order: 4
img_path: /images/
---

My memory recall is that of a goldfish, so I often need to refer to notes/documentation on command usage and sntax. I asked ChatGPT 4 to provide me some cheat sheets. So the contents of this page are a combination of official documentation and my own additions to frequently used commands.

# Minikube Commands Cheat Sheet

Remember to always check the official [Minikube documentation](https://minikube.sigs.k8s.io/docs/) for the most up-to-date information and detailed command usage.

## Basic Commands
- **Start Minikube**: `minikube start`
- **Stop Minikube**: `minikube stop`
- **Delete Minikube cluster**: `minikube delete`
- **View Minikube status**: `minikube status`
- **Access Minikube dashboard**: `minikube dashboard`

## Configuration and Management
- **List available Kubernetes versions**: `minikube get-k8s-versions`
- **Set Kubernetes version**: `minikube start --kubernetes-version v1.20.0`
- **Set memory allocation**: `minikube start --memory 4096`
- **Set CPU allocation**: `minikube start --cpus 2`
- **View Minikube config**: `minikube config view`
- **Set Minikube config**: `minikube config set memory 4096`

## Networking
- **List services**: `minikube service list`
- **Access a service**: `minikube service [service-name]`
- **Enable ingress addon**: `minikube addons enable ingress`
- **Disable ingress addon**: `minikube addons disable ingress`

## Data and Storage
- **Mount a local directory**: `minikube mount /local/path:/vm/path`
- **Set persistent volume size**: `minikube start --disk-size 50g`

## Troubleshooting
- **View logs**: `minikube logs`
- **Check Minikube environment**: `minikube kubectl -- get pods -A`
- **Restart Minikube**: `minikube stop && minikube start`

## Advanced Usage
- **Run with specific VM driver**: `minikube start --driver=virtualbox`
- **Enable a specific addon**: `minikube addons enable metrics-server`
- **Disable a specific addon**: `minikube addons disable metrics-server`
- **Run Minikube with a custom host IP**: `minikube start --host-only-cidr "192.168.99.1/24"`

---
---
---

# Kustomize Commands Cheat Sheet

Always ensure to check the official [Kustomize documentation](https://kubectl.docs.kubernetes.io/guides/introduction/kustomize/) for the most up-to-date and detailed information.

## Basic Commands
- **Build a Kustomization**: `kustomize build .`
- **Create a new Kustomization**: `kustomize create --autodetect`
- **Edit Kustomization file**: `kustomize edit add resource [resource-name.yaml]`

## Managing Resources
- **Add a resource**: `kustomize edit add resource [resource-file.yaml]`
- **Add a configmap generator**: `kustomize edit add configmap [configmap-name] --from-literal=key=value`
- **Add a secret generator**: `kustomize edit add secret [secret-name] --from-literal=key=value`
- **Remove a resource**: `kustomize edit remove resource [resource-name.yaml]`

## Configuring Overlays
- **Create an overlay**: `mkdir -p overlays/[environment] && kustomize create --autodetect -o overlays/[environment]`
- **Use an overlay in build**: `kustomize build overlays/[environment]`

## Setting Image and Field Values
- **Set image**: `kustomize edit set image [old-image]=[new-image]`
- **Set namespace**: `kustomize edit set namespace [namespace-name]`
- **Set field value**: `kustomize cfg set [dir] [field-name] [field-value]`

## Working with Patches
- **Add a patch**: `kustomize edit add patch [patch-file.yaml]`
- **Remove a patch**: `kustomize edit remove patch [patch-file.yaml]`

## Advanced Usage
- **Create a plugin**: `kustomize plugin [plugin-name]`
- **Run a Kustomize plugin**: `kustomize build --enable_alpha_plugins`

---
---
---

# kubectl Commands Cheat Sheet

Remember to always check the official [kubectl documentation](https://kubernetes.io/docs/reference/kubectl/overview/) for the most up-to-date and detailed command usage.

## Basic Commands
- **Get resources**: `kubectl get [resource]`
- **Describe resources**: `kubectl describe [resource] [name]`
- **Create a resource**: `kubectl create -f [filename.yaml]`
- **Delete a resource**: `kubectl delete -f [filename.yaml]`
- **Edit a resource**: `kubectl edit [resource] [name]`

## Namespace Management
- **List namespaces**: `kubectl get namespaces`
- **Create a namespace**: `kubectl create namespace [namespace-name]`
- **Delete a namespace**: `kubectl delete namespace [namespace-name]`

## Pod Management
- **List pods**: `kubectl get pods`
- **Create a pod**: `kubectl run [pod-name] --image=[image-name]`
- **Delete a pod**: `kubectl delete pod [pod-name]`

## Deployment Management
- **Create a deployment**: `kubectl create deployment [deployment-name] --image=[image-name]`
- **Get deployments**: `kubectl get deployments`
- **Update a deployment**: `kubectl set image deployment/[deployment-name] [container-name]=[new-image]`

## Service Management
- **Expose a deployment as a service**: `kubectl expose deployment [deployment-name] --type=[service-type] --port=[port]`
- **Get services**: `kubectl get services`

## Config and Secret Management
- **Create a configmap**: `kubectl create configmap [config-name] --from-literal=key=value`
- **Create a secret**: `kubectl create secret generic [secret-name] --from-literal=key=value`

## Logs and Debugging
- **View logs of a pod**: `kubectl logs [pod-name]`
- **Execute a command in a pod**: `kubectl exec [pod-name] -- [command]`

## Advanced Usage
- **Apply a configuration**: `kubectl apply -f [filename.yaml]`
- **Scale a deployment**: `kubectl scale deployment [deployment-name] --replicas=[number]`
- **Port forward to a local port**: `kubectl port-forward [pod-name] [local-port]:[pod-port]`
- **Rollout restart a deployment**: `kubectl rollout restart deployment/[deployment-name]`

---
---
---

# Linux RHEL Commands Cheat Sheet

This cheat sheet includes a range of essential commands for system information, package management, user management, network configuration, file system operations, process management, file permissions, disk usage, system logs, and firewall management in RHEL. For the most accurate and up-to-date details, refer to the official RHEL documentation and man pages. ​

## System Information
- **Check OS version**: `cat /etc/redhat-release`
- **View system hostname**: `hostnamectl`
- **Display system information**: `uname -a`

## Package Management (YUM/DNF)
- **Update package repository index**: `sudo yum update`
- **Install a package**: `sudo yum install [package-name]`
- **Remove a package**: `sudo yum remove [package-name]`
- **List installed packages**: `yum list installed`
- **Search for a package**: `yum search [keyword]`

## User Management
- **Add a new user**: `sudo adduser [username]`
- **Set password for a user**: `sudo passwd [username]`
- **Delete a user**: `sudo userdel [username]`
- **Add a user to a group**: `sudo usermod -aG [group-name] [username]`

## Network Configuration
- **Display network interfaces**: `nmcli d`
- **Configure a network interface**: `nmtui`
- **Restart network service**: `sudo systemctl restart network`

## File System Operations
- **List files and directories**: `ls -l`
- **Change directory**: `cd [directory]`
- **Copy files or directories**: `cp [source] [destination]`
- **Move/rename files or directories**: `mv [source] [destination]`
- **Delete files or directories**: `rm [file/directory]`

## Process Management
- **View running processes**: `ps -ef`
- **Kill a process**: `kill [PID]`
- **Start a service**: `sudo systemctl start [service-name]`
- **Stop a service**: `sudo systemctl stop [service-name]`
- **Enable a service to start on boot**: `sudo systemctl enable [service-name]`

## File Permissions
- **Change file permissions**: `chmod [permissions] [file]`
- **Change file ownership**: `chown [user]:[group] [file]`
- **Change file group ownership**: `chgrp [group] [file]`

## Disk Usage
- **Check disk space usage**: `df -h`
- **Check file/directory space usage**: `du -sh [file/directory]`

## System Logs
- **View system logs**: `journalctl`
- **Tail a log file**: `tail -f /var/log/[log-file]`

## Firewall Management
- **Check firewall status**: `sudo firewall-cmd --state`
- **List firewall rules**: `sudo firewall-cmd --list-all`
- **Add a firewall rule**: `sudo firewall-cmd --add-port=[port]/[protocol] --permanent`
- **Reload firewall**: `sudo firewall-cmd --reload`

---
---
---

# Ubuntu Commands Cheat Sheet

Remember to always consult the Ubuntu man pages and official documentation for the most accurate and detailed information.

## System Information
- **Check OS version**: `lsb_release -a`
- **View system hostname**: `hostnamectl`
- **Display kernel information**: `uname -r`

## Package Management (APT)
- **Update package lists**: `sudo apt update`
- **Upgrade installed packages**: `sudo apt upgrade`
- **Install a package**: `sudo apt install [package-name]`
- **Remove a package**: `sudo apt remove [package-name]`
- **Search for a package**: `apt search [keyword]`

## User Management
- **Add a new user**: `sudo adduser [username]`
- **Set password for a user**: `sudo passwd [username]`
- **Delete a user**: `sudo deluser [username]`
- **Add a user to a group**: `sudo usermod -aG [group-name] [username]`

## Network Configuration
- **Display network interfaces**: `ip addr`
- **Edit network interfaces file**: `sudo nano /etc/network/interfaces`
- **Restart network service**: `sudo systemctl restart networking`

## File System Operations
- **List files and directories**: `ls -lah`
- **Change directory**: `cd [directory]`
- **Copy files or directories**: `cp [source] [destination]`
- **Move/rename files or directories**: `mv [source] [destination]`
- **Delete files or directories**: `rm [file/directory]`

## Process Management
- **View running processes**: `top` or `htop`
- **Kill a process**: `kill [PID]` or `pkill [process-name]`
- **Start a service**: `sudo systemctl start [service-name]`
- **Stop a service**: `sudo systemctl stop [service-name]`
- **Enable a service to start on boot**: `sudo systemctl enable [service-name]`

## File Permissions
- **Change file permissions**: `chmod [permissions] [file]`
- **Change file ownership**: `chown [user]:[group] [file]`
- **Change file group ownership**: `chgrp [group] [file]`

## Disk Usage
- **Check disk space usage**: `df -h`
- **Check file/directory space usage**: `du -sh [file/directory]`

## System Logs
- **View system logs**: `journalctl`
- **Tail a log file**: `tail -f /var/log/[log-file]`

## Firewall Management
- **Check UFW status**: `sudo ufw status`
- **Enable UFW**: `sudo ufw enable`
- **Add a UFW rule**: `sudo ufw allow [port/protocol]`
- **Reload UFW**: `sudo ufw reload`

---
---
---

# HashiCorp Packer Commands Cheat Sheet
Always consult the official [Packer documentation](https://www.packer.io/docs) for the most detailed and updated information.

## Basic Commands
- **Initialize a Packer configuration**: `packer init .`
- **Validate a Packer template**: `packer validate [template-file]`
- **Build an image**: `packer build [template-file]`

## Template Inspection and Debugging
- **Inspect a template**: `packer inspect [template-file]`
- **Debug a build**: `PACKER_LOG=1 packer build [template-file]`

## Advanced Build Options
- **Build with specific variables**: `packer build -var 'key=value' [template-file]`
- **Only build a specific build**: `packer build -only=[builder-name] [template-file]`
- **Parallel build execution**: `packer build -parallel-builds=2 [template-file]`

## Environment Variables
- **Set Packer log level**: `export PACKER_LOG=1`
- **Set Packer log path**: `export PACKER_LOG_PATH='packerlog.txt'`

## Template Creation and Management
- **Create a new template file**: `touch [template-name].pkr.hcl`
- **Edit a template file**: Open `[template-name].pkr.hcl` in a text editor

## Plugin Management
- **Install a new plugin**: `packer init [template-file]`
- **Upgrade installed plugins**: `packer init -upgrade`

## HCL2 Transition
- **Convert a JSON template to HCL2**: `packer hcl2_upgrade [template-file.json]`

---
---
---

# HashiCorp Terraform Commands Cheat Sheet

Always consult the official [Terraform documentation](https://www.terraform.io/docs) for the most detailed and updated information.

## Basic Commands
- **Initialize a Terraform working directory**: `terraform init`
- **Validate a Terraform configuration**: `terraform validate`
- **Plan infrastructure changes**: `terraform plan`
- **Apply infrastructure changes**: `terraform apply`
- **Destroy managed infrastructure**: `terraform destroy`

## State Management
- **View current state**: `terraform show`
- **List resources in state**: `terraform state list`
- **Modify the state file**: `terraform state mv [source] [destination]`
- **Remove items from the state**: `terraform state rm [resource]`

## Workspace Management
- **List workspaces**: `terraform workspace list`
- **Create a new workspace**: `terraform workspace new [workspace-name]`
- **Select a workspace**: `terraform workspace select [workspace-name]`
- **Delete a workspace**: `terraform workspace delete [workspace-name]`

## Variable Management
- **Apply with variables**: `terraform apply -var 'key=value'`
- **Use variables file**: `terraform apply -var-file='file.tfvars'`

## Output Management
- **Show output values**: `terraform output`
- **Show specific output value**: `terraform output [output-name]`

## Formatting and Validation
- **Format Terraform code**: `terraform fmt`
- **Validate Terraform syntax**: `terraform validate`

## Advanced Options
- **Create a plan file**: `terraform plan -out=[file-name]`
- **Apply a specific plan file**: `terraform apply [plan-file]`

## Debugging and Troubleshooting
- **Enable detailed logs**: `export TF_LOG=TRACE`
- **Set log output path**: `export TF_LOG_PATH='terraform.log'`

---
---
---

# Ansible Commands Cheat Sheet

Remember to always refer to the official [Ansible documentation](https://docs.ansible.com/ansible/latest/index.html) for detailed and up-to-date command usage.

## Basic Commands
- **Ping a host**: `ansible [host] -m ping`
- **Run a single command**: `ansible [host] -m command -a '[command]'`
- **Run an ad-hoc command**: `ansible [host] -a '[command]'`

## Playbook Execution
- **Run a playbook**: `ansible-playbook [playbook-file.yml]`
- **Run a playbook with extra vars**: `ansible-playbook [playbook-file.yml] --extra-vars '[vars]'`
- **Run a playbook with tags**: `ansible-playbook [playbook-file.yml] --tags '[tag]'`

## Inventory Management
- **List hosts in inventory**: `ansible-inventory --list`
- **Show host details in inventory**: `ansible-inventory --host [host]`

## Vault Management
- **Create an encrypted file**: `ansible-vault create [file-name]`
- **Edit an encrypted file**: `ansible-vault edit [file-name]`
- **Encrypt an existing file**: `ansible-vault encrypt [file-name]`
- **Decrypt an encrypted file**: `ansible-vault decrypt [file-name]`
- **View an encrypted file**: `ansible-vault view [file-name]`

## Role and Collection Management
- **Create a new role**: `ansible-galaxy init [role-name]`
- **Install a role**: `ansible-galaxy install [role-name]`
- **Install a collection**: `ansible-galaxy collection install [collection-name]`

## Variable Management
- **Pass variables on the command line**: `ansible-playbook [playbook] -e '[var=value]'`
- **Use a variables file in a playbook**: `ansible-playbook [playbook] -e '@[variables-file.yml]'`

## Debugging and Testing
- **Check syntax of a playbook**: `ansible-playbook [playbook] --syntax-check`
- **Dry run a playbook (check mode)**: `ansible-playbook [playbook] --check`
