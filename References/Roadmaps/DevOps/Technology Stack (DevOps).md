# Recommended Technology Stack

Part of [[DevOps Roadmap - Index|Senior DevOps Engineer Roadmap]].

## Version Control and CI/CD

- [ ] Git
- [ ] GitHub Actions (or GitLab CI)
- [ ] Reusable workflow/pipeline templates

## Containers

- [ ] Docker / Docker Compose
- [ ] A container registry (Docker Hub, GHCR, ECR)
- [ ] Trivy or Grype for image scanning

## Orchestration

- [ ] Kubernetes (kind or minikube for local clusters)
- [ ] kubectl
- [ ] Helm
- [ ] Kustomize

## Infrastructure as Code

- [ ] Terraform
- [ ] Terraform Cloud or a remote backend (S3 + DynamoDB, or equivalent)
- [ ] Ansible (for configuration management where IaC alone isn't enough)

## Cloud Platform

- [ ] One primary cloud provider (AWS, GCP, or Azure) — depth over breadth
- [ ] IAM / identity and access management
- [ ] VPC / networking fundamentals
- [ ] Object storage (S3 or equivalent)
- [ ] Managed compute (EC2/Cloud Run/App Service) and managed Kubernetes (EKS/GKE/AKS)

## Observability

- [ ] Prometheus
- [ ] Grafana
- [ ] Loki or the ELK/EFK stack for logs
- [ ] OpenTelemetry for tracing
- [ ] Alertmanager

## Security

- [ ] Vault or cloud-native secrets managers
- [ ] OPA/Gatekeeper or Kyverno for policy enforcement
- [ ] Dependency and image vulnerability scanning in CI

## SRE and Incident Management

- [ ] An on-call/alerting tool conceptually (PagerDuty or equivalent)
- [ ] A status page and incident tracking convention
- [ ] A blameless postmortem template
