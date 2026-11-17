# Essential Commands Reference

Part of [[Git Roadmap - Index|Git Mastery Roadmap]]. A quick-lookup table; the phase notes cover the *why* behind each command.

| Category | Command | Purpose |
|---|---|---|
| Inspect | `git status` | Working directory and staging state |
| Inspect | `git log --oneline --graph --all` | Visualize commit topology |
| Inspect | `git diff` / `git diff --staged` | Unstaged / staged changes |
| Inspect | `git show <ref>` | View a single commit's changes |
| Inspect | `git blame <file>` | Who/when changed each line |
| Inspect | `git log -S<string>` | Find when a string was added/removed (pickaxe) |
| Stage/Commit | `git add -p` | Stage changes interactively, hunk by hunk |
| Stage/Commit | `git commit --amend` | Edit the most recent commit |
| Stage/Commit | `git commit --fixup <ref>` | Mark a commit as a fixup for autosquash |
| Undo | `git restore <file>` | Discard working directory changes |
| Undo | `git reset --soft/--mixed/--hard <ref>` | Move HEAD/branch, optionally unstage or discard |
| Undo | `git revert <ref>` | Create a new commit undoing a published one |
| Undo | `git reflog` | Recover from almost any local mistake |
| Branching | `git switch -c <branch>` | Create and switch to a branch |
| Branching | `git merge <branch>` | Three-way or fast-forward merge |
| Branching | `git rebase -i <ref>` | Interactively rewrite commit history |
| Branching | `git rebase --abort` / `--continue` | Bail out of or continue a rebase |
| Remote | `git fetch --prune` | Fetch and remove stale remote-tracking branches |
| Remote | `git push --force-with-lease` | Safer force-push after rewriting history |
| Debugging | `git bisect start/good/bad` | Binary search for a regressing commit |
| Debugging | `git log --follow <file>` | Trace a file's history across renames |
| Hygiene | `git gc` | Compress and clean up the repository |
| Hygiene | `git clean -fd` | Remove untracked files and directories |
| Advanced | `git worktree add <path> <branch>` | Check out another branch without re-cloning |
| Advanced | `git filter-repo` | Rewrite large portions of history (e.g. remove secrets) |
