📘 Terraform — Complete Reference Guide

This document is a one-stop reference for infrastructure as code using Terraform.
It covers installation, commands, providers, variables, modules, workspaces, backends, provisioners, and vault integration.

⚙️ 1. Core Terraform Workflow

Command Lifecycle

terraform init
Initializes the working directory, downloads providers/modules.

terraform plan
Shows what changes will be made before applying them.

terraform apply
Executes the plan and creates/updates infrastructure.

terraform destroy
Destroys the created infrastructure.

🌐 2. Providers

Definition:
Providers are plugins that let Terraform know which cloud or service to interact with (Amazon Web Services, Microsoft Azure, Google Cloud Platform, etc.).

Types of Providers

Cloud Providers — Amazon Web Services (AWS), Microsoft Azure (Azure), Google Cloud Platform (GCP)

SaaS Providers — Datadog, GitHub, Kubernetes

Infrastructure Providers — VMware vSphere, OpenStack

Basic Configuration Example

provider "aws" {
  region = "us-east-1"
}

🌍 3. Multi-Region Setup

Deploying resources to multiple regions in the same cloud:

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
  ami      = var.ami
  instance_type = var.instance_type
}

resource "aws_instance" "west_vm" {
  provider = aws.us_west
  ami      = var.ami
  instance_type = var.instance_type
}

☁️ 4. Multi-Cloud Setup

Deploying resources to different clouds by using multiple provider blocks:

provider "aws" {
  region = "us-east-1"
}

provider "azurerm" {
  features {}
}

resource "aws_instance" "example" { ... }

resource "azurerm_resource_group" "example" {
  name     = "rg1"
  location = "East US"
}

⚙️ 5. Variables

Variables are used to parameterize configurations.

Types of Variables

Input variables: Passed into Terraform to customize resources.

Output variables: Used to display values after creation (e.g. IPs, URLs).

Defining variables in vars.tf

variable "instance_type" {
  default = "t2.micro"
}


Passing values from .tfvars file

terraform apply -var-file=dev.tfvars


Output Example

output "public_ip" {
  value = aws_instance.example.public_ip
}

⚡ 6. Conditional Expressions

Control logic inside Terraform:

resource "aws_s3_bucket" "example" {
  bucket = "mybucket"
  acl    = var.env == "prod" ? "private" : "public-read"
}

🧠 7. Built-in Functions

Examples:

length(list) — Get length of a list

file("path") — Read file content

upper("string") — Convert to uppercase

concat(list1, list2) — Combine lists

📦 8. Modules

Modular approach allows reusable building blocks.

Creating a module

modules/
  ec2/
    main.tf
    variables.tf
    outputs.tf


Using a module

module "ec2" {
  source = "./modules/ec2"
  ami    = var.ami
  instance_type = var.instance_type
}

💾 9. Backends & State Management

Remote backend: Stores state file remotely (e.g., Amazon S3)

terraform {
  backend "s3" {
    bucket = "tf-state-bucket"
    key    = "global/terraform.tfstate"
    region = "us-east-1"
  }
}


State Locking: Using Amazon DynamoDB table to lock state during changes:

dynamodb_table = "terraform-lock"

🧩 10. Provisioners

Used to run scripts on the resource after it’s created.

For simple boot-time setup → use user_data

For complex post-provisioning → use provisioners

provisioner "remote-exec" {
  inline = [
    "sudo apt update",
    "sudo apt install -y nginx"
  ]
}

🧠 11. Workspaces

Used to manage multiple environments (dev, test, prod) from same configuration.

terraform workspace new dev
terraform workspace select dev
terraform workspace show

🔐 12. Vault Integration & Secrets Management

HashiCorp Vault is used to manage secrets.

Vault Modes: Dev and Prod

Secrets Engines: aws, kv, kubernetes, etc.

Access: Like IAM Roles

Policies: Like IAM Policies

Usage:

Fetch secrets dynamically from Vault using vault provider or data sources.

Keeps sensitive data out of state files.

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

Use providers to define where infra is created.

Use variables and .tfvars to make configs reusable.

Use modules for DRY, reusable code.

Use workspaces for environment separation.

Use remote backend + state locking for team collaboration.

Use Vault to manage secrets safely.

Use provisioners only for post-setup tasks.
