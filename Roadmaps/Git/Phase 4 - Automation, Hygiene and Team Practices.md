---
tags: [roadmap, roadmap/git]
---

# Phase 4: Automation, Hygiene and Team Practices

Part of [[Git Roadmap - Index|Git Mastery Roadmap]]. Previous: [[Phase 3 - History, Internals and Advanced Operations]].

**Duration:** Weeks 7–8
**Objective:** Apply Git at team scale — automation, conventions, and repository health.

## Week 7: Hooks and Automation

### Git Hooks

- [ ] Understand client-side hooks: `pre-commit`, `commit-msg`, `pre-push`.
- [ ] Understand server-side hooks: `pre-receive`, `update`, `post-receive`.
- [ ] Write a `pre-commit` hook to block committing secrets or lint failures.
- [ ] Write a `commit-msg` hook to enforce a commit message convention.
- [ ] Understand hook limitations: hooks live in `.git/hooks` and are not versioned by default.
- [ ] Use a hook manager (e.g. Husky, pre-commit framework, or Lefthook) to version and share hooks across a team.

### Commit and Branch Conventions

- [ ] Understand Conventional Commits and when a team should adopt them.
- [ ] Understand semantic versioning's relationship to commit history.
- [ ] Define branch naming conventions (`feature/`, `fix/`, `chore/`).
- [ ] Understand squash-merge vs. merge-commit vs. rebase-merge PR strategies and their effect on `main`'s history.

### CI Integration

- [ ] Understand how CI systems trigger on push and PR events.
- [ ] Configure branch protection rules (required reviews, required status checks).
- [ ] Understand shallow clones (`--depth`) and why CI uses them for speed.
- [ ] Understand how CI caches depend on consistent branch/tag naming.

### Practical Tasks

- [ ] Write and install a `pre-commit` hook that runs a linter before allowing a commit.
- [ ] Configure a shared hook manager so the hook is versioned with the repository.
- [ ] Set up branch protection on a test repository requiring a passing check before merge.

**Deliverable:** Automated enforcement of team conventions without relying on manual discipline.

## Week 8: Repository Hygiene and Scale

### Repository Hygiene

- [ ] Review and prune stale remote-tracking branches (`git fetch --prune`).
- [ ] Understand `git gc` and repository bloat over time.
- [ ] Understand Git LFS for large binary assets and when it's warranted.
- [ ] Audit `.gitattributes` for line-ending normalization and diff/merge strategies per file type.
- [ ] Understand shallow vs. full clones for large monorepos.

### Multi-Repository and Large-Scale Concerns

- [ ] Understand monorepo vs. polyrepo trade-offs at a conceptual level.
- [ ] Understand sparse-checkout for working with a subset of a large repository.
- [ ] Understand worktrees for working on multiple branches simultaneously without re-cloning.
- [ ] Understand how submodules pin a dependency to a specific commit, and their common pitfalls.

### Incident Response

- [ ] Define a runbook for "secret committed to history": rotate credential, rewrite history, force-push, notify collaborators to re-clone.
- [ ] Define a runbook for "main branch force-pushed accidentally": recover via reflog on any machine that still has the old ref, or via another collaborator's local copy.
- [ ] Document repository-specific conventions (branch strategy, commit style, protected branches) for new team members.

### Practical Tasks

- [ ] Prune stale remote-tracking branches in a real repository.
- [ ] Set up `git worktree` to check out two branches side by side and verify both build independently.
- [ ] Write a short incident runbook for a committed-secret scenario.
- [ ] Review an existing team's `.gitattributes` and `.gitignore` for gaps.

**Deliverable:** A repository maintained in a healthy state over time, and documented runbooks for the incidents that inevitably happen on a real team.
