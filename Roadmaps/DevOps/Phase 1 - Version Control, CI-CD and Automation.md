---
tags: [roadmap, roadmap/devops]
---

# Phase 1: Version Control, CI/CD and Automation

Part of [[DevOps Roadmap - Index|Senior DevOps Engineer Roadmap]]. Next: [[Phase 2 - Containers and Docker]].

**Duration:** Weeks 1–2
**Objective:** Establish a disciplined Git workflow and a working CI pipeline before touching infrastructure.

## Week 1: Git Workflows for Teams

This week assumes general Git fluency; see [[Git Roadmap - Index|Git Mastery Roadmap]] if commands like rebase and reflog aren't yet comfortable. The focus here is team and pipeline conventions specifically.

### Branching and Release Strategy

- [ ] Choose and justify a branching strategy (trunk-based vs. GitHub Flow vs. Git Flow) for a given team size and release cadence.
- [ ] Understand semantic versioning and how it maps to tags and releases.
- [ ] Define branch protection rules: required reviews, required status checks, no force-push to main.
- [ ] Define a commit convention (e.g. Conventional Commits) that CI and changelogs can key off of.

### Pull Request Discipline

- [ ] Keep PRs small and independently reviewable.
- [ ] Write PR descriptions that explain *why*, not just *what*.
- [ ] Use draft PRs for work-in-progress visibility.
- [ ] Require CI to pass before merge is allowed.

### Practical Tasks

- [ ] Set up branch protection on a real or test repository requiring review and passing checks.
- [ ] Define and document a commit convention for the project used throughout this roadmap.
- [ ] Tag a release and generate a changelog from commit history.

**Deliverable:** A documented Git workflow enforced by repository settings, not just convention.

## Week 2: CI/CD Pipeline Design

### CI Fundamentals

- [ ] Understand what a CI pipeline actually verifies: build, lint, type-check, test.
- [ ] Write a GitHub Actions workflow triggered on push and pull request.
- [ ] Use a matrix build to test across multiple versions/platforms.
- [ ] Cache dependencies to speed up repeated runs.
- [ ] Fail fast vs. run everything: decide pipeline ordering deliberately.

### CD Fundamentals

- [ ] Understand continuous delivery vs. continuous deployment.
- [ ] Build and push a container image as a pipeline artifact (preview — depth in Phase 2).
- [ ] Environment promotion: dev → staging → production.
- [ ] Manual approval gates for production deployment.
- [ ] Rollback strategy: how to undo a bad deploy quickly.

### Automation Principles

- [ ] Idempotent pipeline steps — safe to re-run.
- [ ] Secrets in CI: never in plaintext logs, scoped per environment.
- [ ] Pipeline-as-code: the pipeline definition lives in the repository, reviewed like any other change.

### Practical Tasks

- [ ] Build a complete CI workflow for the roadmap project: lint, test, build, on every PR.
- [ ] Add a CD stage that deploys to a staging environment automatically and production with manual approval.
- [ ] Deliberately break a build and verify the pipeline catches it before merge.
- [ ] Practice a rollback: deploy a bad version, then revert it through the pipeline.

**Deliverable:** A working CI/CD pipeline taking a code change from commit to a deployed (staging) environment automatically.
