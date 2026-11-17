# Phase 4: Infrastructure as Code and Cloud Fundamentals

Part of [[DevOps Roadmap - Index|Senior DevOps Engineer Roadmap]]. Previous: [[Phase 3 - Kubernetes and Orchestration]]. Next: [[Phase 5 - Observability and Security]].

**Duration:** Weeks 7–8
**Objective:** Provision real cloud infrastructure reproducibly, and understand the core services underpinning it.

## Week 7: Cloud Fundamentals

### Core Services (pick one primary provider)

- [ ] IAM: users, roles, policies, and the principle of least privilege.
- [ ] Compute: virtual machines and a managed container/Kubernetes offering.
- [ ] Networking: VPCs, subnets (public/private), security groups, routing.
- [ ] Storage: object storage (S3 or equivalent) and its access control model.
- [ ] Managed databases and why they're usually preferred over self-hosted for production.
- [ ] DNS and the provider's managed DNS service.

### Shared Responsibility and Cost

- [ ] Understand the shared responsibility model (what the provider secures vs. what you secure).
- [ ] Understand basic cost drivers: compute, egress, storage, and idle resources.
- [ ] Tag resources for cost attribution and ownership.

### Practical Tasks

- [ ] Create a least-privilege IAM role for a deployment pipeline (not an admin/root credential).
- [ ] Design a VPC with public and private subnets, and explain why the database belongs in the private subnet.
- [ ] Upload and retrieve an object from object storage with correctly scoped access control.
- [ ] Review a cloud bill (even a small one) and identify the top cost drivers.

**Deliverable:** A securely configured cloud account with least-privilege access, ready for infrastructure provisioning.

## Week 8: Terraform and Configuration Management

### Terraform Fundamentals

- [ ] Providers, resources, and data sources.
- [ ] `terraform init`, `plan`, `apply`, `destroy`.
- [ ] Variables, outputs, and `.tfvars` for environment-specific values.
- [ ] State: what it is, why it matters, and the danger of manual drift.
- [ ] Remote state with locking (S3 + DynamoDB, or the provider's equivalent).
- [ ] Modules for reusable infrastructure components.

### Terraform in Practice

- [ ] Workspaces or directory-per-environment for dev/staging/production.
- [ ] `terraform plan` in CI as a required check before apply.
- [ ] Importing existing manually created resources into Terraform state.
- [ ] Understanding and resolving state drift.

### Configuration Management

- [ ] Understand when configuration management (Ansible) complements IaC rather than replacing it.
- [ ] Write a basic Ansible playbook for a provisioning task Terraform doesn't own (e.g. app-level config).
- [ ] Idempotency as the core principle shared by Terraform and Ansible alike.

### Practical Tasks

- [ ] Write Terraform to provision the VPC, IAM role, and managed Kubernetes/compute from Week 7, with remote state.
- [ ] Add a `terraform plan` step to the CI pipeline from Phase 1, requiring review before `apply`.
- [ ] Deliberately introduce drift (change a resource manually) and reconcile it with Terraform.
- [ ] Write a small Ansible playbook and run it idempotently twice, confirming no changes the second time.

**Deliverable:** Real cloud infrastructure provisioned entirely through version-controlled, peer-reviewed Terraform with remote state.
