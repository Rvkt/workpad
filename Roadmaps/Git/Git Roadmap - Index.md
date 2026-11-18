---
tags: [roadmap, roadmap/git]
---

# Git Mastery Roadmap

**Level:** Intermediate → Senior/Lead
**Duration:** 8 Weeks
**Weekly Commitment:** 2–4 Hours
**Learning Approach:** Deliberate practice on real repositories, understanding internals rather than memorizing commands.

---

## Learning Objectives

By completing this roadmap, the goal is to develop competency in:

- [ ] Git's object model and internal data structures.
- [ ] Daily workflow commands used fluently and correctly.
- [ ] Branching strategies and collaboration workflows.
- [ ] Merge vs. rebase trade-offs and when to use each.
- [ ] Safe history rewriting and recovery from mistakes.
- [ ] Conflict resolution under real-world pressure.
- [ ] Git hooks, automation, and CI integration.
- [ ] Repository hygiene at team and organization scale.
- [ ] Debugging regressions with bisect and blame.
- [ ] Explaining Git behavior from first principles, not folklore.

---

## Roadmap Notes

- [[Phase 1 - Git Fundamentals and Daily Workflow]] (Weeks 1–2)
- [[Phase 2 - Branching, Collaboration and Workflows]] (Weeks 3–4)
- [[Phase 3 - History, Internals and Advanced Operations]] (Weeks 5–6)
- [[Phase 4 - Automation, Hygiene and Team Practices]] (Weeks 7–8)
- [[Essential Commands Reference]]
- [[Learning Resources (Git)]]

---

## Weekly Progress Tracking

- [ ] [[Phase 1 - Git Fundamentals and Daily Workflow|Phase 1: Git Fundamentals and Daily Workflow]]
- [ ] [[Phase 2 - Branching, Collaboration and Workflows|Phase 2: Branching, Collaboration and Workflows]]
- [ ] [[Phase 3 - History, Internals and Advanced Operations|Phase 3: History, Internals and Advanced Operations]]
- [ ] [[Phase 4 - Automation, Hygiene and Team Practices|Phase 4: Automation, Hygiene and Team Practices]]

### Completion Criteria

The roadmap should not be considered complete merely because all topics have been studied.

You should be able to:

- [ ] Explain what a commit, tree, and blob actually are, not just how to create one.
- [ ] Choose between merge and rebase deliberately, and justify the choice to a team.
- [ ] Recover a "lost" commit using reflog without panic.
- [ ] Resolve a non-trivial merge conflict involving renamed and restructured files.
- [ ] Write and use a Git hook to enforce a team convention.
- [ ] Bisect a regression to the exact offending commit.
- [ ] Rewrite history safely on a shared branch, including communicating the force-push.
- [ ] Design a branching strategy appropriate to a given team size and release cadence.
- [ ] Debug a broken repository (corrupted refs, detached HEAD, diverged history) without re-cloning as the first resort.

---

## Execution Rules

1. Follow the phases in order; internals in Phase 3 make much more sense after fundamentals and workflows are solid.
2. Practice every command on a disposable test repository before using it on real work.
3. Read `git <command> --help` before searching the web — the manual pages are authoritative and precise.
4. When something goes wrong, diagnose with `git status`, `git log --oneline --graph`, and `git reflog` before reaching for a fix.
5. Prefer understanding the object model over memorizing command flags; the flags follow naturally once the model is clear.
6. Practice recovery scenarios deliberately (reset --hard, deleted branches, bad rebases) in a throwaway repo — don't wait for a real incident to learn recovery.

**Final Goal:** Use Git fluently and safely as a daily tool, understand its internals well enough to recover from any mistake, and design branching and collaboration workflows appropriate for a team.
