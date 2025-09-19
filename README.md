# 📘 Terraform — Complete Reference Guide

This document is a one-stop reference for Infrastructure as Code using **Terraform**.  
It covers installation, commands, providers, variables, modules, workspaces, backends, provisioners, and Vault integration.

---

## ⚙️ 1. Core Terraform Workflow

**Command Lifecycle:**

```bash
terraform init      # Initialize working directory, download providers/modules
terraform plan      # Show what changes will be made before applying
terraform apply     # Execute the plan and create/update infrastructure
terraform destroy   # Destroy the created infrastructure
🌐 2. Providers
Definition:
Providers are plugins that tell Terraform which cloud or service to interact with
(e.g. Amazon Web Services, Microsoft Azure, Google Cloud Platform).

Types of Providers:

Cloud Providers: AWS, Azure, GCP

SaaS Providers: Datadog, GitHub, Kubernetes

Infrastructure Providers: VMware vSphere, OpenStack

Basic Configuration Example:

hcl

provider "aws" {
  region = "us-east-1"
}
🌍 3. Multi-Region Setup
Deploy resources to multiple regions in the same cloud:

hcl

provider "aws" {
  region = "us-east-1"
  alias  = "us_east"
}

provider "aws" {
  region = "us-west-2"
  alias  = "us_west"
}

resource "aws_instance" "east_vm" {
  provider = aws.us_east
  ami = var.ami
  instance_type = var.instance_type
}

resource "aws_instance" "west_vm" {
  provider = aws.us_west
  ami = var.ami
  instance_type = var.instance_type
}
☁️ 4. Multi-Cloud Setup
Deploy resources to different clouds using multiple provider blocks:

hcl

provider "aws" {
  region = "us-east-1"
}

provider "azurerm" {
  features {}
}

resource "aws_instance" "example" {
  # AWS resource
}

resource "azurerm_resource_group" "example" {
  name     = "rg1"
  location = "East US"
}
⚙️ 5. Variables
Purpose: Used to parameterize Terraform configurations.

Types:

Input Variables — passed into Terraform to customize resources

Output Variables — display values after creation (e.g., IPs, URLs)

Defining variables (vars.tf):

hcl

variable "instance_type" {
  default = "t2.micro"
}
Passing values from .tfvars:

bash

terraform apply -var-file=dev.tfvars
Output Example:

hcl

output "public_ip" {
  value = aws_instance.example.public_ip
}
⚡ 6. Conditional Expressions
hcl

resource "aws_s3_bucket" "example" {
  bucket = "mybucket"
  acl    = var.env == "prod" ? "private" : "public-read"
}
🧠 7. Built-in Functions
length(list) — Get length of a list

file("path") — Read file content

upper("string") — Convert to uppercase

concat(list1, list2) — Combine lists

📦 8. Modules
Modular approach allows reusable building blocks.

Module Structure:

css

modules/
  ec2/
    main.tf
    variables.tf
    outputs.tf
Using a module:

hcl

module "ec2" {
  source = "./modules/ec2"
  ami    = var.ami
  instance_type = var.instance_type
}
💾 9. Backends & State Management
Remote Backend: Store state file remotely (e.g., Amazon S3)

hcl

terraform {
  backend "s3" {
    bucket = "tf-state-bucket"
    key    = "global/terraform.tfstate"
    region = "us-east-1"
  }
}
State Locking with Amazon DynamoDB:

hcl

dynamodb_table = "terraform-lock"
🧩 10. Provisioners
Used to run scripts after a resource is created.

Simple boot-time setup → user_data

Complex post-provisioning → provisioners

hcl

provisioner "remote-exec" {
  inline = [
    "sudo apt update",
    "sudo apt install -y nginx"
  ]
}
🧠 11. Workspaces
Manage multiple environments from the same configuration:

bash

terraform workspace new dev
terraform workspace select dev
terraform workspace show
🔐 12. Vault Integration & Secrets Management
HashiCorp Vault is used to manage secrets.

Modes: Dev / Prod

Secrets Engines: aws, kv, kubernetes, etc.

Access = like IAM Roles

Policies = like IAM Policies

Usage:

Fetch secrets dynamically from Vault using vault provider or data sources

Keeps sensitive data out of state files

📚 13. Common Commands Reference
Purpose	Command
Initialize	terraform init
Plan changes	terraform plan
Apply changes	terraform apply
Destroy infrastructure	terraform destroy
Use var file	terraform apply -var-file=prod.tfvars
Create workspace	terraform workspace new dev
Switch workspace	terraform workspace select dev
Show current workspace	terraform workspace show

📌 14. Key Takeaways
Use providers to define where infra is created

Use variables and .tfvars to make configs reusable

Use modules for DRY, reusable code

Use workspaces for environment separation

Use remote backend + state locking for collaboration

Use Vault to manage secrets safely

Use provisioners only for post-setup tasks
