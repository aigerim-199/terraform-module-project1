Terraform & Ansible Project: AWS Infrastructure with Jenkins Installation

Overview

This project automates the provisioning of AWS infrastructure using Terraform and installs Jenkins using Ansible. The setup includes:

A VPC named group-1

Three public subnets

Internet Gateway & Route Table

Security Group with necessary ports

EC2 Instance named group-1, accessible in every AWS region

Bastion Host to allow passwordless SSH to the EC2 instance

Ansible Playbook to install Jenkins on the EC2 instance, triggered from Terraform

Infrastructure Details

AWS Resources Created

VPC (group-1)

Public Subnets (3 in different Availability Zones)

Internet Gateway & Route Table (for internet access)

Security Group (group-1)

Allows necessary ports (SSH, HTTP, etc.)

EC2 Instance (group-1)

Uses a globally accessible Linux AMI

Configured to allow passwordless SSH from Bastion Host

Bastion Host

Used to securely connect to the private EC2 instance

Prerequisites

Before running the project, ensure you have:

Terraform installed (Install Guide)

AWS CLI configured with appropriate credentials (Setup Guide)

Ansible installed (Install Guide)

Terraform Setup & Deployment

Clone the Repository:

git clone https://github.com/your-repo/terraform-ansible-jenkins.git
cd terraform-ansible-jenkins

Initialize Terraform:

terraform init

Plan Deployment:

terraform plan

Apply Terraform Configuration:

terraform apply -auto-approve

Retrieve EC2 Public IP:

terraform output

Ansible Setup & Jenkins Installation

Update Inventory File: (Replace with EC2 instance IP)

[jenkins]
ec2-instance ansible_host=<EC2_PUBLIC_IP> ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa

Run Ansible Playbook to Install Jenkins:

ansible-playbook -i inventory install_jenkins.yml

Access Jenkins Web UI:

Open browser: http://<EC2_PUBLIC_IP>:8080

Follow Jenkins setup instructions

Terraform-Ansible Integration

Terraform automatically triggers the Ansible playbook after instance creation using the remote-exec provisioner.

Example Terraform snippet:

provisioner "local-exec" {
  command = "ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i inventory install_jenkins.yml"
}

Cleanup

To destroy the created resources:

terraform destroy -auto-approve

Future Improvements

Convert Terraform code into reusable modules

Implement CI/CD pipeline for automated deployments

Use AWS Systems Manager (SSM) instead of a Bastion Host for enhanced security

License

This project is open-source and available under the MIT License.

Author

Aigerim-199
