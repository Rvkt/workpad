---
tags: [roadmap, roadmap/devops]
---

# Phase 2: Containers and Docker

Part of [[DevOps Roadmap - Index|Senior DevOps Engineer Roadmap]]. Previous: [[Phase 1 - Version Control, CI-CD and Automation]]. Next: [[Phase 3 - Kubernetes and Orchestration]].

**Duration:** Weeks 3–4
**Objective:** Build, run, and optimize containers as the deployable unit for the rest of the roadmap.

## Week 3: Docker Fundamentals

### Container Concepts

- [ ] Understand containers vs. virtual machines: namespaces and cgroups conceptually.
- [ ] Understand images as layered, immutable filesystems.
- [ ] Understand the union filesystem and layer caching.
- [ ] `docker run`, `docker ps`, `docker logs`, `docker exec`.
- [ ] `docker build`, tags, and the build context.

### Writing Dockerfiles

- [ ] `FROM`, `RUN`, `COPY`, `WORKDIR`, `ENV`, `EXPOSE`, `CMD` vs. `ENTRYPOINT`.
- [ ] Multi-stage builds to separate build-time and runtime dependencies.
- [ ] Minimizing image size: slim/distroless base images, `.dockerignore`.
- [ ] Running as a non-root user inside the container.
- [ ] Layer ordering for effective build caching.

### Practical Tasks

- [ ] Write a multi-stage Dockerfile for the roadmap project, minimizing final image size.
- [ ] Verify the image runs as a non-root user and exposes only the required port.
- [ ] Measure the image size and build time before and after applying caching/layering best practices.
- [ ] Use `docker exec` to inspect a running container's filesystem and environment.

**Deliverable:** A production-quality, minimal Docker image with every Dockerfile line explainable.

## Week 4: Docker Compose, Networking and Registries

### Docker Compose

- [ ] Define a multi-container application (app + database + cache) in `docker-compose.yml`.
- [ ] Service dependencies and startup ordering (`depends_on`, health checks).
- [ ] Volumes for persistent data vs. bind mounts for local development.
- [ ] Environment variable injection via `.env` files.

### Networking

- [ ] Understand Docker's default bridge network and container-to-container DNS.
- [ ] Custom networks for isolating services.
- [ ] Port publishing (`-p`) vs. internal container communication.

### Registries and Image Lifecycle

- [ ] Push and pull images from a registry (Docker Hub, GHCR, or a cloud registry).
- [ ] Image tagging strategy (`latest` pitfalls, semantic/commit-sha tags).
- [ ] Scan images for vulnerabilities (Trivy or equivalent) as a CI step.
- [ ] Clean up dangling images and unused volumes (`docker system prune`).

### Practical Tasks

- [ ] Compose the full roadmap project (app + database) locally with `docker-compose.yml`, including health checks.
- [ ] Push the built image to a registry from the CI pipeline built in Phase 1.
- [ ] Add an image vulnerability scan to the CI pipeline and fix any findings.
- [ ] Verify the application data persists across container restarts using a named volume.

**Deliverable:** A fully containerized local development environment and an image published through CI to a registry.
