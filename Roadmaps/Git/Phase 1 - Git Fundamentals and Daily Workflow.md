---
tags: [roadmap, roadmap/git]
---

# Phase 1: Git Fundamentals and Daily Workflow

Part of [[Git Roadmap - Index|Git Mastery Roadmap]]. Next: [[Phase 2 - Branching, Collaboration and Workflows]].

**Duration:** Weeks 1–2
**Objective:** Build fluency with the core daily commands and a correct mental model of what a repository actually is.

## Week 1: Core Concepts and the Object Model

### Repository Fundamentals

- [ ] Understand what `.git` actually contains.
- [ ] Understand the working directory, staging area (index), and repository as three distinct states.
- [ ] Understand blobs, trees, commits, and tags as Git's four object types.
- [ ] Understand how a commit references a tree and a parent commit.
- [ ] Understand content-addressable storage and SHA hashing.
- [ ] Understand how branches are just movable pointers to commits.
- [ ] Understand HEAD and what "detached HEAD" means.
- [ ] Inspect objects directly with `git cat-file`.

### Daily Commands

- [ ] `git init`, `git clone`.
- [ ] `git status`, `git diff`, `git diff --staged`.
- [ ] `git add`, `git add -p` for partial staging.
- [ ] `git commit`, `git commit --amend`.
- [ ] `git log`, `git log --oneline --graph --all`.
- [ ] `git show`.
- [ ] Write meaningful, conventional commit messages.

### Practical Tasks

- [ ] Create a repository and inspect its `.git` directory structure manually.
- [ ] Use `git cat-file -p` to read a commit, tree, and blob by hash.
- [ ] Practice partial staging with `git add -p` on a file with unrelated changes.
- [ ] Make a series of small, atomic commits with clear messages.

**Deliverable:** A correct mental model of commits as snapshots, and fluency with the daily add/commit/diff/log loop.

## Week 2: Remotes, .gitignore and Undoing Changes

### Remotes

- [ ] Understand origin and upstream conventions.
- [ ] `git remote add`, `git remote -v`.
- [ ] `git fetch` vs. `git pull`.
- [ ] `git push`, tracking branches, and `--set-upstream`.
- [ ] Understand fast-forward vs. non-fast-forward pushes.

### Ignoring and Cleaning

- [ ] Write effective `.gitignore` patterns.
- [ ] Understand global vs. repository-level ignore files.
- [ ] `git rm --cached` to untrack already-committed files.
- [ ] `git clean -n` / `git clean -fd` to remove untracked files safely.

### Undoing Changes

- [ ] Understand the difference between `git restore`, `git reset`, and `git revert`.
- [ ] `git restore <file>` to discard working directory changes.
- [ ] `git reset --soft` / `--mixed` / `--hard` and what each moves.
- [ ] `git revert` for safely undoing a published commit.
- [ ] Understand `git reflog` as the safety net for "lost" commits.

### Practical Tasks

- [ ] Set up a remote and practice fetch/pull/push cycles.
- [ ] Deliberately make a mess (wrong commit, accidentally staged file, committed secret) and fix it with the correct undo command for each case.
- [ ] Delete a branch, then recover its last commit using `git reflog`.

**Deliverable:** Confidence distinguishing restore/reset/revert, and the ability to recover from common mistakes without anxiety.
