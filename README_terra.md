🏗️ Terraform – End-to-End Concepts
1. Introduction to Terraform

What it is:
Terraform is an open-source Infrastructure as Code (IaC) tool created by HashiCorp.
It allows you to define, provision, and manage infrastructure across various cloud and on-prem platforms using a declarative configuration language (HCL).

Purpose:
Automate infrastructure deployment, ensure consistency, version infrastructure, and enable collaboration between teams.

2. Core Terraform Workflow

Terraform follows a predictable workflow:

Write: Define infrastructure resources in .tf files.

Initialize: Prepare working directory with provider plugins.

Plan: Preview changes Terraform will make.

Apply: Create or modify infrastructure as per plan.

Destroy: Tear down resources if no longer needed.

3. Terraform Architecture

Terraform CLI: The command-line interface to run Terraform commands.

Providers: Plugins that interact with specific APIs (e.g. Amazon Web Services, Microsoft Azure, Google Cloud, Kubernetes, etc.).

Provisioners: Execute actions/scripts on local or remote machines as part of resource creation or destruction.

Terraform Core: Engine that reads configuration, builds the dependency graph, and manages state.

State File: Keeps track of infrastructure deployed so Terraform knows what exists and what to change.

4. Terraform Configuration Structure

Providers: Define the platform or service to interact with.

Resources: Represent components like servers, networks, databases.

Data Sources: Fetch read-only information from existing infrastructure.

Variables: Parameterize values for reusability.

Outputs: Display or pass values from created resources.

Modules: Group of resources reused as logical units.

5. Terraform State

Purpose:
Maintains a snapshot of the infrastructure Terraform manages.

Types:

Local state: Stored on the local machine.

Remote state: Stored in a remote backend (e.g. Amazon S3, Terraform Cloud, etc.) for team collaboration.

State Locking: Prevents simultaneous changes to avoid conflicts.

State Drift: When real infrastructure changes outside Terraform, causing a mismatch with state.

6. Terraform Modules

Definition:
Reusable building blocks that encapsulate resources, variables, and outputs.

Benefits:

Code reuse and maintainability

Consistency across environments

Types:

Root Module: Your main working directory.

Child Modules: Called from root or other modules.

7. Terraform Variables and Outputs

Variables:

Input variables allow parameterization of resources.

Can be set through .tfvars, environment variables, or CLI.

Outputs:

Provide values after apply.

Help share data between modules or display useful information.

8. Terraform Providers

What they do:
Abstract the APIs of cloud platforms and services.

Examples: Amazon Web Services, Microsoft Azure, Google Cloud, Kubernetes, GitHub, Datadog etc.

Lifecycle: Installed on terraform init.

9. Terraform Lifecycle & Resource Management

Lifecycle Meta-Arguments:

create_before_destroy: Creates new before destroying old.

prevent_destroy: Prevents accidental deletion.

ignore_changes: Ignores specific attribute changes.

Resource Dependencies:

Terraform builds a dependency graph automatically.

depends_on can define explicit dependencies.

10. Terraform Backends

Purpose:
Define where state files are stored and how they are accessed.

Examples: Amazon S3, Terraform Cloud, Azure Blob Storage, Google Cloud Storage

Features:

Remote collaboration

State locking

Versioning

11. Terraform Workspaces

Purpose:
Enable managing multiple environments (dev, staging, prod) from the same configuration.

Default Workspace: default

Named Workspaces: Isolated state per workspace.

12. Terraform Provisioners

Purpose:
Execute scripts or commands on resources during creation or destruction.

Types:

local-exec: Runs locally.

remote-exec: Runs on the remote resource.

(Best used sparingly — prefer configuration management tools instead.)

13. Terraform Functions and Expressions

Purpose:
Enhance logic and flexibility.

Examples:
String manipulation, numeric operations, conditionals, loops (for, for_each, count).

14. Terraform CLI Commands (Conceptually)

init – Initializes working directory.

plan – Shows the proposed changes.

apply – Executes the planned changes.

destroy – Deletes all managed infrastructure.

refresh – Updates state with real-world infrastructure.

validate – Checks configuration syntax.

(You don’t need the syntax here, just understand what each does.)

15. Terraform Cloud and Enterprise

Terraform Cloud: SaaS platform by HashiCorp for:

Remote state storage

Remote execution

Policy enforcement

Collaboration

Terraform Enterprise: Self-hosted version for organizations needing more control.

16. Terraform Best Practices

Use version control (Git) for all configurations.

Separate environments using workspaces or different state files.

Use remote state for collaboration.

Structure configuration with modules.

Implement state locking to avoid race conditions.

Apply naming conventions and documentation.

17. Terraform Limitations

Not ideal for configuration management (use Ansible or Chef for that).

Can be state-sensitive — manual changes outside Terraform can cause drift.

Requires careful planning for resource dependencies.

✅ Summary

Terraform is a declarative IaC tool that lets you provision, manage, and version infrastructure across multiple platforms.
It works by using providers, resources, state, and modules, orchestrated via the plan → apply → destroy lifecycle.
With proper design and practices, Terraform can make infrastructure deployments reliable, repeatable, and scalable.
