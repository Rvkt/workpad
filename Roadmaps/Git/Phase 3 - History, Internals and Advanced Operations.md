---
tags: [roadmap, roadmap/git]
---

# Phase 3: History, Internals and Advanced Operations

Part of [[Git Roadmap - Index|Git Mastery Roadmap]]. Previous: [[Phase 2 - Branching, Collaboration and Workflows]]. Next: [[Phase 4 - Automation, Hygiene and Team Practices]].

**Duration:** Weeks 5–6
**Objective:** Go beyond daily usage into history rewriting, debugging, and the internals that make recovery possible.

## Week 5: History Rewriting and Recovery

### Rewriting History

- [ ] `git commit --amend` for the most recent commit.
- [ ] Interactive rebase for rewriting older commits (reword, edit, squash, fixup, drop).
- [ ] `git commit --fixup` and `git rebase -i --autosquash`.
- [ ] `git filter-repo` (or `git filter-branch` as legacy context) for rewriting large swaths of history, e.g. removing a committed secret.
- [ ] Understand that rewritten history changes commit hashes and breaks other clones' history.
- [ ] Understand `--force-with-lease` as the safer alternative to `--force`.

### Recovery

- [ ] Understand that `git reflog` tracks HEAD and branch movements, not deleted file content.
- [ ] Recover a commit after a bad `reset --hard` using reflog.
- [ ] Recover a deleted branch by finding its last commit via reflog.
- [ ] Understand `git fsck --lost-found` for finding dangling commits reflog has expired past.
- [ ] Understand the reflog's expiration window and its limits.

### Practical Tasks

- [ ] Deliberately run `git reset --hard` past unpushed work, then recover it with reflog.
- [ ] Deliberately delete a branch, then recover it.
- [ ] Use `git commit --fixup` plus autosquash to clean up a feature branch's history.
- [ ] Simulate removing a committed secret from history and understand why rotating the credential still matters afterward.

**Deliverable:** No fear of history-rewriting operations, because recovery paths are understood and rehearsed.

## Week 6: Debugging, Diffing and Internals

### Debugging

- [ ] `git bisect start` / `good` / `bad` to binary-search a regression.
- [ ] `git bisect run <script>` to automate bisection.
- [ ] `git blame` to find when and why a line changed.
- [ ] `git log -S<string>` and `git log -G<regex>` ("pickaxe") to find when a string or pattern was introduced or removed.
- [ ] `git log --follow` to trace a file's history across renames.

### Diffing and Comparison

- [ ] `git diff <commit>..<commit>`.
- [ ] `git diff <branch>...<branch>` (triple-dot, merge-base diff) vs. two-dot diff.
- [ ] `git log branchA..branchB` to see commits unique to one side.
- [ ] Configure a better diff/merge tool.

### Internals Deeper Dive

- [ ] Understand refs as files under `.git/refs`.
- [ ] Understand packfiles and loose objects.
- [ ] Understand `git gc` and when Git repacks automatically.
- [ ] Understand how `git stash` stores its state as commits.
- [ ] Understand submodules and worktrees at a conceptual level, and when each is appropriate.

### Practical Tasks

- [ ] Use `git bisect` to find the exact commit that introduced a deliberately planted bug.
- [ ] Use the pickaxe (`-S`) to find when a specific function name was added.
- [ ] Trace a renamed file's full history with `--follow`.
- [ ] Inspect a repository's packfiles and loose objects directly.

**Deliverable:** The ability to debug "when/why did this change" questions precisely, and a working understanding of what's actually happening under the hood.
