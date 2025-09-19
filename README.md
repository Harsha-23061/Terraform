📘 Terraform — Complete Reference Guide

A complete end-to-end reference to mastering Infrastructure as Code (IaC) using Terraform by HashiCorp.
This guide covers conceptual understanding, workflow, and hands-on usage.

🧠 1. Introduction to Terraform

What is Terraform?
Terraform is an Infrastructure as Code (IaC) tool that allows you to define, provision, and manage infrastructure resources using declarative .tf configuration files.

Why Use Terraform?

Version-controlled infrastructure

Automated & reproducible deployments

Multi-cloud support

Scalable team collaboration

Terraform Architecture:

Terraform Core — executes plans and manages state

Providers — plugins to interact with cloud/SaaS platforms

State — tracks the real-world infrastructure created

⚙️ 2. Terraform Core Workflow
Step	Command	Description
Initialize	terraform init	Downloads required providers/modules
Plan	terraform plan	Shows what changes will be made
Apply	terraform apply	Creates or updates infrastructure
Destroy	terraform destroy	Destroys created infrastructure

Flow: Write → init → plan → apply → manage → destroy

🌐 3. Providers

Definition: Plugins that tell Terraform which platform or service to provision resources on.

Types of Providers:

Cloud: Amazon Web Services, Microsoft Azure, Google Cloud Platform

SaaS: Datadog, GitHub, Kubernetes

Infrastructure: VMware vSphere, OpenStack

Basic Example

provider "aws" {
  region = "us-east-1"
}

🌍 4. Multi-Region Setup (Same Cloud)

Deploy resources to multiple regions within the same cloud:

provider "aws" {
  region = "us-east-1"
  alias  = "us_east"
}

provider "aws" {
  region = "us-west-2"
  alias  = "us_west"
}

resource "aws_instance" "east_vm" {
  provider      = aws.us_east
  ami           = var.ami
  instance_type = var.instance_type
}

resource "aws_instance" "west_vm" {
  provider      = aws.us_west
  ami           = var.ami
  instance_type = var.instance_type
}

☁️ 5. Multi-Cloud Setup

Deploy resources across different clouds:

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

⚙️ 6. Variables

Purpose: Parameterize configurations for flexibility.

Types:

Input Variables — pass values into Terraform

Output Variables — print values after apply

Define in vars.tf:

variable "instance_type" {
  default = "t2.micro"
}


Use via .tfvars file:

terraform apply -var-file=dev.tfvars


Output Example:

output "public_ip" {
  value = aws_instance.example.public_ip
}

⚡ 7. Conditional Expressions

Control logic inside Terraform:

resource "aws_s3_bucket" "example" {
  bucket = "mybucket"
  acl    = var.env == "prod" ? "private" : "public-read"
}

🧠 8. Built-in Functions

length(list) → length of list

file("path") → read file content

upper("string") → convert to uppercase

concat(list1, list2) → merge lists

📦 9. Modules

Use a modular approach to make code reusable and maintainable.

Structure

modules/
  ec2/
    main.tf
    variables.tf
    outputs.tf


Usage

module "ec2" {
  source        = "./modules/ec2"
  ami           = var.ami
  instance_type = var.instance_type
}

💾 10. Remote Backends & State Locking

State: Terraform tracks infrastructure in a terraform.tfstate file.

Remote Backend example using Amazon S3:

terraform {
  backend "s3" {
    bucket = "tf-state-bucket"
    key    = "global/terraform.tfstate"
    region = "us-east-1"
  }
}


Locking: Use Amazon DynamoDB to lock state and prevent simultaneous updates:

dynamodb_table = "terraform-lock"

🧩 11. Provisioners

Run scripts on resources after creation:

Use user_data for simple bootstrapping

Use provisioners for complex tasks

provisioner "remote-exec" {
  inline = [
    "sudo apt update",
    "sudo apt install -y nginx"
  ]
}

🧠 12. Workspaces

Workspaces let you manage multiple environments (dev, test, prod):

terraform workspace new dev
terraform workspace select dev
terraform workspace show

🔐 13. Vault Integration & Secrets Management

Use HashiCorp Vault to securely manage secrets:

Modes: Dev / Prod

Secrets Engines: aws, kv, kubernetes

Concepts:

Access = like IAM Role

Policies = like IAM Policy

Use the Vault provider to fetch secrets dynamically, keeping secrets out of state files.

📚 14. Common Commands Reference
Purpose	Command
Initialize	terraform init
Plan changes	terraform plan
Apply changes	terraform apply
Destroy infra	terraform destroy
Use var file	terraform apply -var-file=prod.tfvars
Create workspace	terraform workspace new dev
Switch workspace	terraform workspace select dev
Show workspace	terraform workspace show
📌 15. Key Takeaways

✅ Providers define where infra is created
✅ Use variables + .tfvars for reusability
✅ Use modules for DRY architecture
✅ Workspaces = multiple environments
✅ Use remote backend + locking for teams
✅ Use Vault for secure secrets
✅ Use provisioners for post-deploy setup
