# Phase 2: Branching, Collaboration and Workflows

Part of [[Git Roadmap - Index|Git Mastery Roadmap]]. Previous: [[Phase 1 - Git Fundamentals and Daily Workflow]]. Next: [[Phase 3 - History, Internals and Advanced Operations]].

**Duration:** Weeks 3–4
**Objective:** Work confidently with branches, merges, and conflicts in a multi-person repository.

## Week 3: Branching and Merging

### Branching

- [ ] `git branch`, `git switch` / `git checkout -b`.
- [ ] Understand fast-forward merges vs. three-way merges.
- [ ] `git merge` and reading a merge commit.
- [ ] Understand merge commit parents and `git log --graph` topology.
- [ ] Delete merged and unmerged branches safely (`-d` vs. `-D`).

### Conflict Resolution

- [ ] Understand conflict markers and what each section represents.
- [ ] Resolve conflicts using an editor and `git mergetool`.
- [ ] `git diff` during a conflict to see both sides.
- [ ] `git merge --abort` to bail out cleanly.
- [ ] Resolve conflicts involving renamed or moved files.

### Practical Tasks

- [ ] Create two branches that touch the same lines and resolve the conflict manually.
- [ ] Create a conflict involving a file renamed on one branch and edited on the other.
- [ ] Practice `git merge --abort` and restarting cleanly.

**Deliverable:** Comfort resolving real merge conflicts without guessing.

## Week 4: Rebasing and Collaboration Workflows

### Rebasing

- [ ] Understand what rebase actually does: replaying commits onto a new base.
- [ ] `git rebase <branch>`.
- [ ] Interactive rebase: `git rebase -i` for squash, reword, reorder, drop.
- [ ] Understand why rebase rewrites commit hashes.
- [ ] Understand the "golden rule" of rebase: never rewrite published history others depend on.
- [ ] `git rebase --abort` and `git rebase --continue`.
- [ ] `git pull --rebase` vs. `git pull` (merge).

### Merge vs. Rebase

- [ ] Articulate the trade-offs: linear history vs. preserved context.
- [ ] Decide when a merge commit is appropriate vs. when to rebase.
- [ ] Understand `git merge --no-ff` and when teams enforce it.

### Collaboration Workflows

- [ ] Understand trunk-based development.
- [ ] Understand GitHub Flow (feature branch + PR + merge to main).
- [ ] Understand Git Flow (develop/release/hotfix branches) and when it's overkill.
- [ ] Understand fork-and-pull-request workflows for open source.
- [ ] Write a clear pull request description and keep PRs small and reviewable.
- [ ] Understand code review etiquette from the Git side: responding to review commits, squashing before merge.

### Practical Tasks

- [ ] Rebase a feature branch onto an updated main and resolve conflicts during rebase.
- [ ] Use interactive rebase to clean up a messy commit history before opening a PR.
- [ ] Simulate a force-push after rebase on a shared branch and understand `--force-with-lease`.
- [ ] Compare the resulting history graph of the same change done via merge vs. via rebase.

**Deliverable:** The ability to choose and justify a branching strategy, and to rebase/merge deliberately rather than by habit.
