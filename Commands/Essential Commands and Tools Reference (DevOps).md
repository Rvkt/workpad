# Essential Commands and Tools Reference

Part of [[DevOps Roadmap - Index|Senior DevOps Engineer Roadmap]]. A quick-lookup table; the phase notes cover the *why* behind each tool.

| Category | Command / Tool | Purpose |
|---|---|---|
| Containers | `docker build`, `docker run`, `docker exec` | Build and run containers |
| Containers | `docker compose up` | Run a multi-container stack locally |
| Containers | `trivy image <image>` | Scan an image for vulnerabilities |
| Kubernetes | `kubectl apply -f`, `get`, `describe` | Manage and inspect cluster objects |
| Kubernetes | `kubectl logs`, `kubectl logs --previous` | View current and crashed container logs |
| Kubernetes | `kubectl exec -it <pod> -- sh` | Live debugging inside a pod |
| Kubernetes | `helm install/upgrade` | Package and deploy templated manifests |
| IaC | `terraform init/plan/apply/destroy` | Provision infrastructure |
| IaC | `terraform state list` | Inspect what Terraform manages |
| Config mgmt | `ansible-playbook <playbook>.yml` | Apply idempotent configuration |
| CI/CD | GitHub Actions workflow YAML | Define pipeline stages as code |
| Observability | `promql` queries in Grafana | Query and visualize metrics |
| Observability | `kubectl top pod/node` | Quick resource usage snapshot |
| Networking | `curl -v`, `dig`, `ss` | Diagnose connectivity from a host or pod |
| Security | `grype` / `trivy fs` | Scan source/dependencies for vulnerabilities |
| Security | `vault kv get/put` | Read/write secrets from Vault |
