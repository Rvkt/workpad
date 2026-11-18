---
tags: [roadmap, roadmap/python]
---

# Phase 5: Packaging, Deployment and Production Engineering

Part of [[Python Roadmap - Index|Senior Python Developer Roadmap]]. Previous: [[Phase 4 - Architecture, APIs and Data]]. Next: [[Phase 6 - Advanced Topics and Senior Engineering Practices]].

**Duration:** Weeks 9–10
**Objective:** Package, containerize, deploy, and observe a Python service reliably.

## Week 9: Packaging and Dependency Management

### Packaging

- [ ] `pyproject.toml` as the single source of project metadata.
- [ ] Build backends: Hatchling, setuptools, or others.
- [ ] Building a wheel and sdist with `build`.
- [ ] Publishing to a package index with `twine` (or understanding the process conceptually for private packages).
- [ ] Semantic versioning for a published package.
- [ ] Writing a clear public API (`__all__`, avoiding leaking internals).

### Dependency Management

- [ ] Lockfiles and reproducible installs (`uv.lock`, `poetry.lock`).
- [ ] Separating runtime, dev, and optional dependency groups.
- [ ] Auditing dependencies for vulnerabilities and unmaintained packages.
- [ ] Pinning strategy: exact pins vs. compatible ranges, and the trade-offs.

### Practical Tasks

- [ ] Package the Phase 1–4 code as an installable project with `pyproject.toml`.
- [ ] Build a wheel locally and install it in a clean virtual environment.
- [ ] Set up dependency groups for dev, test, and runtime.
- [ ] Run a dependency vulnerability audit and resolve any findings.

**Deliverable:** A properly packaged, installable Python project with reproducible dependencies.

## Week 10: Containerization, CI/CD and Observability

### Docker

- [ ] Write a multi-stage Dockerfile for a Python service.
- [ ] Minimize image size (slim base images, `.dockerignore`).
- [ ] Run as a non-root user in the container.
- [ ] Environment-based configuration inside containers.
- [ ] Local development with `docker compose`.

### CI/CD

- [ ] GitHub Actions workflow: lint, type-check, test, build.
- [ ] Caching dependencies in CI for faster runs.
- [ ] Running tests against a containerized database in CI.
- [ ] Building and pushing a container image on merge to main.
- [ ] Branch protection requiring passing checks.

### Observability

- [ ] Structured logging (JSON logs, correlation IDs).
- [ ] Integrating Sentry (or equivalent) for error tracking.
- [ ] Basic OpenTelemetry tracing for a request path.
- [ ] Health check and readiness endpoints.
- [ ] Avoiding logging of secrets and sensitive data.

### Practical Tasks

- [ ] Write a multi-stage Dockerfile for the FastAPI service and verify it runs correctly.
- [ ] Set up a GitHub Actions workflow running lint, type-check, and tests on every PR.
- [ ] Add structured logging with request correlation IDs to the service.
- [ ] Add a health check endpoint and verify it reports dependency status (e.g. database connectivity).

**Deliverable:** A containerized service with an automated CI pipeline and baseline observability.
