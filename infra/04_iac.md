[← Back to Index](./README.md)

# 4. Infrastructure-as-Code (IaC)

Clicking buttons in the console is forbidden. Everything must be code.

## Junior -> Mid: The Basics
**Goal:** Can modify existing Terraform/Ansible code and apply changes.

### 1. Terraform Basics
- **Concept:** Declarative infrastructure.
- **Key Skills:**
    - **HCL Syntax:** Resources, Variables, Outputs.
    - **Workflow:** `terraform init`, `plan`, `apply`.
    - **State:** Understanding that Terraform tracks what it created in a `tfstate` file.

### 2. Ansible Basics
- **Concept:** Configuration management (configuring the servers).
- **Key Skills:**
    - **Playbooks:** YAML files defining tasks.
    - **Inventory:** List of servers to configure.
    - **Modules:** Using `apt`, `yum`, `copy`, `service` modules.

---

## Mid -> Senior: Modular & Scalable IaC
**Goal:** Writes reusable modules and manages state for teams.

### 1. Advanced Terraform
- **Concept:** DRY (Don't Repeat Yourself).
- **Key Knowledge:**
    - **Modules:** Creating reusable components (e.g., a standard "VPC" module).
    - **Remote State:** Storing state in S3 + DynamoDB (for locking) so teams can collaborate.
    - **Workspaces:** Managing environments (dev, prod) with the same code.

### 2. Ansible Roles
- **Concept:** Organizing playbooks.
- **Key Knowledge:**
    - **Roles:** Grouping tasks, vars, and handlers.
    - **Galaxy:** Using community roles.
    - **Vault:** Encrypting secrets in git.

### 3. Testing IaC
- **Concept:** Linting and validation.
- **Key Knowledge:**
    - **tfsec / checkov:** Scanning Terraform for security issues.
    - **ansible-lint:** Enforcing style.

---

## Senior -> Lead: Governance & Policy
**Goal:** Enforces standards and manages drift.

### 1. Policy-as-Code
- **Concept:** Guardrails.
- **Key Knowledge:**
    - **Sentinel / OPA:** "Prevent S3 buckets from being public" before the code is applied.
    - **AWS Config:** Detecting drift (when someone changes something manually).

### 2. Advanced State Management
- **Concept:** Refactoring infrastructure.
- **Key Knowledge:**
    - **Import:** Bringing existing resources under Terraform control.
    - **Moved Blocks:** Refactoring code without destroying/recreating resources.
    - **Taint:** Forcing a resource to be recreated.

### 3. Alternative Tools
- **Concept:** Choosing the right tool.
- **Key Knowledge:**
    - **Pulumi:** Using TypeScript/Python instead of HCL.
    - **Crossplane:** Managing cloud resources using Kubernetes manifests.
