# Phase 6: Site Reliability Engineering and Senior Practices

Part of [[DevOps Roadmap - Index|Senior DevOps Engineer Roadmap]]. Previous: [[Phase 5 - Observability and Security]].

**Duration:** Weeks 11–12
**Objective:** Apply SRE discipline and senior-level engineering judgment to the system built in Phases 1–5.

## Week 11: SRE Fundamentals

### SLIs, SLOs and Error Budgets

- [ ] Understand Service Level Indicators (SLIs) as the metrics that actually matter to users.
- [ ] Define a Service Level Objective (SLO) for the roadmap application (e.g. 99.5% successful requests).
- [ ] Understand error budgets and how they balance reliability work against feature work.
- [ ] Connect SLOs to the alerting configured in Phase 5 — alert on error-budget burn rate, not arbitrary thresholds.

### Capacity and Reliability Patterns

- [ ] Understand graceful degradation vs. hard failure.
- [ ] Circuit breakers and retries with backoff — and the danger of retry storms.
- [ ] Rate limiting to protect a service from overload.
- [ ] Health checks as a precondition for safe autoscaling and load balancing.
- [ ] Chaos engineering at a conceptual level: deliberately injecting failure to validate resilience.

### Practical Tasks

- [ ] Define an SLO for the roadmap application and derive an error budget from it.
- [ ] Update alerting to fire based on error-budget burn rate rather than a fixed threshold.
- [ ] Add retry-with-backoff to a client call in the application, and verify it doesn't amplify an outage.
- [ ] Kill a pod or instance under load and observe whether the system degrades gracefully or fails hard.

**Deliverable:** A defined SLO, burn-rate-based alerting, and at least one validated resilience pattern.

## Week 12: Incident Response and Engineering Judgment

### Incident Response

- [ ] Define an incident severity scale and what triggers each level.
- [ ] Run a simulated incident end to end: detect → triage → mitigate → resolve.
- [ ] Write a timeline during the incident, not reconstructed afterward from memory.
- [ ] Understand the role of an incident commander in a larger team.

### Postmortems

- [ ] Write a blameless postmortem: what happened, impact, root cause, contributing factors, action items.
- [ ] Distinguish root cause from contributing factors — rarely is there exactly one cause.
- [ ] Track postmortem action items to completion, not just to the document.

### Senior Engineering Judgment

- [ ] Write a short design doc proposing a non-trivial change to the system, with alternatives considered and rejected.
- [ ] Review a peer's (or past) infrastructure change for correctness, security, and operability — not just "does it work."
- [ ] Explain, in plain terms to a non-DevOps stakeholder, a trade-off made somewhere in this roadmap (e.g. why Kubernetes was or wasn't the right call).
- [ ] Identify and document technical debt introduced during the roadmap, and prioritize it.

### Practical Tasks

- [ ] Run a simulated incident on the roadmap system (e.g. deliberately exhaust a resource) and respond to it using the defined severity scale.
- [ ] Write a complete blameless postmortem for that incident, including at least two concrete action items.
- [ ] Write a one-page design doc proposing one real improvement to the system, with trade-offs stated explicitly.
- [ ] Create a technical debt register for the project covering everything deferred or shortcut across all six phases.

**Deliverable:** A completed incident response cycle with a real postmortem, a design doc demonstrating trade-off reasoning, and a documented technical debt register — the practical synthesis of the whole roadmap.
