🏗️ Terraform – End-to-End Concepts


📌 1. Introduction to Terraform

What is Terraform?
Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp.
It allows you to define, provision, and manage infrastructure across multiple cloud and on-premises environments using a declarative language (HCL).

Purpose & Benefits

Automate infrastructure deployment

Ensure consistency and repeatability

Enable version control for infrastructure

Facilitate collaboration between teams

⚙️ 2. Core Terraform Workflow

Terraform operates through a predictable lifecycle:

Write – Define infrastructure resources in .tf files

Initialize – Install required provider plugins

Plan – Preview the changes to be made

Apply – Create/modify infrastructure as per plan

Destroy – Remove infrastructure when no longer needed

🧠 3. Terraform Architecture

Terraform CLI – Command-line tool to run Terraform commands

Providers – Plugins that communicate with cloud/service APIs

Provisioners – Execute scripts on local/remote machines

Terraform Core – Engine that processes configuration and manages state

State File – Records deployed infrastructure to track changes

🧩 4. Terraform Configuration Structure

Providers – Define which platform or cloud to use

Resources – Individual infrastructure components (servers, DBs, networks)

Data Sources – Read-only information from existing infrastructure

Variables – Parameterize values for flexibility

Outputs – Display or pass data from created resources

Modules – Reusable logical groups of resources

📂 5. Terraform State

Purpose – Maintain a snapshot of managed infrastructure.

Types of State:

Local State – Stored locally on disk

Remote State – Stored on remote backend (Amazon S3, Terraform Cloud etc.)

Key Concepts:

State Locking – Prevents simultaneous edits

State Drift – Occurs when resources change outside Terraform

🧱 6. Terraform Modules

Definition – Reusable building blocks that encapsulate resources, variables, and outputs.

Benefits:

Reuse and maintainability

Consistency across environments

Types:

Root Module – Main working directory

Child Modules – Called within root or other modules

⚡ 7. Terraform Variables & Outputs

Variables

Input values for parameterization

Supplied via .tfvars, CLI, or environment variables

Outputs

Provide values after apply

Useful for sharing data between modules or displaying key info

🌐 8. Terraform Providers

Role – Abstract the APIs of cloud platforms and services.
Examples – Amazon Web Services, Microsoft Azure, Google Cloud, Kubernetes, GitHub, Datadog
Lifecycle – Installed during terraform init

🔁 9. Lifecycle & Resource Management

Lifecycle Meta-Arguments:

create_before_destroy – Create new before destroying old

prevent_destroy – Prevent accidental deletions

ignore_changes – Ignore certain attribute changes

Dependencies:

Implicit dependency graph built automatically

depends_on for explicit dependencies

💾 10. Terraform Backends

Purpose – Define where Terraform stores its state.

Examples – Amazon S3, Terraform Cloud, Azure Blob Storage, Google Cloud Storage

Features

Enables collaboration

Supports state locking

Maintains state history/versioning

🧪 11. Terraform Workspaces

Purpose – Isolate environments (dev, staging, prod) with separate states.

Default Workspace: default

Named Workspaces: Custom environments

⚙️ 12. Terraform Provisioners

Purpose – Run scripts/commands during resource lifecycle.

Types:

local-exec – Runs locally

remote-exec – Runs on the remote machine

⚠️ Use sparingly — prefer configuration management tools like Ansible

🧮 13. Terraform Functions & Expressions

Purpose – Add logic and flexibility to configurations.
Common Use Cases

String operations

Numeric calculations

Conditional statements

Iterations (for_each, count)

🖥️ 14. Terraform CLI Commands (Conceptual)

init – Initialize working directory

plan – Preview proposed changes

apply – Execute the plan

destroy – Delete all managed resources

refresh – Sync state with real infrastructure

validate – Validate configuration syntax

☁️ 15. Terraform Cloud & Enterprise

Terraform Cloud

SaaS by HashiCorp

Remote state storage

Remote execution

Policy enforcement

Team collaboration

Terraform Enterprise

Self-hosted version

Full control for organizations

💡 16. Terraform Best Practices

Use version control (Git)

Separate environments via workspaces or state files

Use remote state for collaboration

Structure code with modules

Implement state locking

Follow naming conventions and documentation

⚠️ 17. Terraform Limitations

Not ideal for configuration management (use Chef or Ansible)

State-sensitive — manual changes can cause drift

Requires careful handling of resource dependencies

✅ Summary

Terraform is a declarative IaC tool that enables you to provision, manage, and version infrastructure reliably across multiple platforms.
By leveraging providers, state, modules, and the plan → apply → destroy workflow, it makes deployments consistent, scalable, and repeatable.
