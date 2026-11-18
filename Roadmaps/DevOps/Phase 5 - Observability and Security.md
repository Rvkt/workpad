---
tags: [roadmap, roadmap/devops]
---

# Phase 5: Observability and Security

Part of [[DevOps Roadmap - Index|Senior DevOps Engineer Roadmap]]. Previous: [[Phase 4 - Infrastructure as Code and Cloud Fundamentals]]. Next: [[Phase 6 - Site Reliability Engineering and Senior Practices]].

**Duration:** Weeks 9–10
**Objective:** Make the running system observable and defensible, not just deployed.

## Week 9: Observability

### Metrics

- [ ] Understand the four golden signals: latency, traffic, errors, saturation.
- [ ] Deploy Prometheus and scrape metrics from the application and cluster.
- [ ] Write a basic Grafana dashboard for the roadmap application.
- [ ] Understand counters, gauges, and histograms, and when to use each.

### Logging

- [ ] Structured (JSON) logging vs. unstructured text logs.
- [ ] Centralize logs with Loki or an ELK/EFK stack.
- [ ] Correlate logs with a request/trace ID across services.
- [ ] Avoid logging secrets and sensitive data.

### Tracing

- [ ] Understand distributed tracing conceptually: spans, trace IDs, context propagation.
- [ ] Instrument the roadmap application with OpenTelemetry.
- [ ] View a trace end to end across at least two components (e.g. app → database call).

### Alerting

- [ ] Configure Alertmanager rules based on symptoms, not just raw thresholds.
- [ ] Avoid alert fatigue: alert on what requires human action, not everything that moves.
- [ ] Route alerts by severity.

### Practical Tasks

- [ ] Instrument the roadmap application with metrics and build a dashboard showing the four golden signals.
- [ ] Centralize its logs and correlate a single request across logs and traces using a shared ID.
- [ ] Configure an alert that fires on a real symptom (e.g. elevated error rate) and verify it both fires and resolves correctly.
- [ ] Deliberately break the application and use only metrics/logs/traces — not the code — to diagnose it.

**Deliverable:** Full observability for the roadmap application: metrics, logs, traces, and a working alert.

## Week 10: Security Across the Pipeline

### Secrets Management

- [ ] Never store secrets in Git, even "private" repos.
- [ ] Use a secrets manager (Vault, or the cloud provider's equivalent) or at minimum CI-native encrypted secrets.
- [ ] Rotate credentials, and design for rotation rather than assuming it never happens.
- [ ] Scope secrets per environment — staging and production never share credentials.

### Pipeline and Supply Chain Security

- [ ] Scan dependencies for known vulnerabilities in CI.
- [ ] Scan container images for vulnerabilities before pushing to a registry.
- [ ] Pin dependency and base image versions rather than tracking `latest`.
- [ ] Understand the basic idea of software supply chain attacks and why pinning/scanning mitigates them.

### Infrastructure and Runtime Security

- [ ] Least-privilege IAM, revisited with real workloads from Phase 4.
- [ ] Network policies in Kubernetes to restrict pod-to-pod traffic.
- [ ] Policy enforcement (OPA/Gatekeeper or Kyverno) for cluster-wide rules (e.g. no root containers).
- [ ] Encrypt data at rest and in transit as a default, not an afterthought.

### Practical Tasks

- [ ] Move any plaintext secrets in the roadmap project to a proper secrets manager or encrypted CI secret store.
- [ ] Add dependency and image scanning as required (blocking) CI checks.
- [ ] Write a Kubernetes NetworkPolicy restricting the database to accept connections only from the application pod.
- [ ] Write a policy (OPA/Kyverno) blocking any pod from running as root, and verify it rejects a non-compliant manifest.

**Deliverable:** A pipeline and running system with no plaintext secrets, scanned dependencies/images, and enforced least-privilege access.
