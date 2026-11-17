# Senior DevOps Engineer Roadmap

**Level:** Intermediate → Senior/Lead
**Duration:** 12 Weeks
**Weekly Commitment:** 3–5 Hours
**Prerequisite:** Comfort with the shell, equivalent to [[Linux Roadmap - Index|the Linux System Administration Roadmap]].
**Learning Approach:** Build and operate a real deployment pipeline end to end, not isolated tool tutorials.

---

## Learning Objectives

By completing this roadmap, the goal is to develop competency in:

- [ ] Version control workflows and CI pipeline design.
- [ ] Containerization with Docker.
- [ ] Container orchestration with Kubernetes.
- [ ] Infrastructure as Code with Terraform.
- [ ] Configuration management and provisioning.
- [ ] Core cloud platform services (compute, networking, storage, IAM).
- [ ] Observability: metrics, logging, and tracing.
- [ ] Security practices across the pipeline (secrets, scanning, least privilege).
- [ ] Site Reliability Engineering practices: SLOs, incident response, postmortems.
- [ ] Designing a deployment pipeline from first principles, not copying a template blindly.

---

## Roadmap Notes

- [[Technology Stack (DevOps)]]
- [[Phase 1 - Version Control, CI-CD and Automation]] (Weeks 1–2)
- [[Phase 2 - Containers and Docker]] (Weeks 3–4)
- [[Phase 3 - Kubernetes and Orchestration]] (Weeks 5–6)
- [[Phase 4 - Infrastructure as Code and Cloud Fundamentals]] (Weeks 7–8)
- [[Phase 5 - Observability and Security]] (Weeks 9–10)
- [[Phase 6 - Site Reliability Engineering and Senior Practices]] (Weeks 11–12)
- [[Essential Commands and Tools Reference (DevOps)]]
- [[Learning Resources (DevOps)]]

---

## Weekly Progress Tracking

- [ ] [[Phase 1 - Version Control, CI-CD and Automation|Phase 1: Version Control, CI/CD and Automation]]
- [ ] [[Phase 2 - Containers and Docker|Phase 2: Containers and Docker]]
- [ ] [[Phase 3 - Kubernetes and Orchestration|Phase 3: Kubernetes and Orchestration]]
- [ ] [[Phase 4 - Infrastructure as Code and Cloud Fundamentals|Phase 4: Infrastructure as Code and Cloud Fundamentals]]
- [ ] [[Phase 5 - Observability and Security|Phase 5: Observability and Security]]
- [ ] [[Phase 6 - Site Reliability Engineering and Senior Practices|Phase 6: Site Reliability Engineering and Senior Practices]]

### Completion Criteria

The roadmap should not be considered complete merely because all topics have been studied.

You should be able to:

- [ ] Design and implement a CI/CD pipeline from a blank repository to a deployed service.
- [ ] Write a production-quality multi-stage Dockerfile and explain every line.
- [ ] Deploy, scale, and debug an application on Kubernetes without copying a tutorial manifest unmodified.
- [ ] Write Terraform that provisions real cloud infrastructure idempotently, with remote state.
- [ ] Explain the shared responsibility model and apply least-privilege IAM to a real workload.
- [ ] Set up metrics, logs, and traces for a service and use them to diagnose a real incident.
- [ ] Define an SLO, explain error budgets, and connect them to a concrete alerting policy.
- [ ] Write a blameless postmortem for a simulated incident with clear, actionable follow-ups.
- [ ] Explain the trade-offs behind a given architecture decision to a team, not just implement it.

---

## Execution Rules

1. Follow the phases in order; Kubernetes (Phase 3) assumes solid Docker fundamentals from Phase 2.
2. Build one real project across all phases (e.g. a small web app) rather than disconnected exercises — each phase adds a layer to the same system.
3. Automate everything twice: do it manually once to understand it, then automate it to prove you understood it.
4. Treat infrastructure changes with the same rigor as application code: version-controlled, reviewed, tested.
5. Prefer managed services and well-known patterns over exotic tooling unless a requirement justifies the complexity.
6. Practice failure deliberately: kill a pod, revoke a credential, fill a disk — and recover it.
7. Document every non-trivial decision's trade-offs, not just the steps taken.

**Final Goal:** Design, build, operate, and troubleshoot a complete deployment pipeline and its production infrastructure independently, with the judgment to make and justify senior-level architecture decisions.
