Part of [[Git Roadmap - Index|Git Mastery Roadmap]].

# Git Notes (Explained Simply)

These are plain-English study notes. The roadmap files are checklists of things to practice. This file is the explanation underneath them — what the ideas actually mean, in simple words, so the checklist makes sense instead of feeling like memorization.

---

## Phase 1: Git Fundamentals and Daily Workflow

### What is Git, really?

Git is a tool that keeps a history of every version of your project. Think of it like a video game's save system: every time you "commit," you create a save point you can always go back to. Nothing you've committed is ever truly lost.

### The three places your files can live

When you work with Git, a file can be in three different "zones," and understanding this is the single most important thing in Phase 1:

1. **Working directory** — the actual files on your computer, the ones you're editing right now.
2. **Staging area (the "index")** — a holding area where you put the changes you're about to save. Think of it like a shopping basket: you pick which changes go in before checking out.
3. **Repository** — the permanent history, made of saved snapshots (commits).

So the flow is: you edit a file (working directory) → you `git add` it (moves it to the staging area / basket) → you `git commit` it (locks it into history).

### Blobs, trees, commits, tags — Git's four building blocks

These sound technical but they're simple once you see the pattern:

- **Blob** = the content of a file (just the raw data, no filename attached).
- **Tree** = a folder listing — it says "this folder contains these files and subfolders," and points to the blobs/trees inside it.
- **Commit** = a snapshot. It points to one tree (the state of the whole project at that moment), points back to its parent commit (the previous snapshot), and carries a message, author, and date.
- **Tag** = a permanent, human-friendly label stuck on a specific commit, usually for marking a release like "v1.0."

So a commit is basically: "here's the whole project at this moment, here's who did it and why, and here's what came before it." Chain enough commits together and you get your project's full history.

### Content-addressable storage and SHA hashing

Every object (blob, tree, commit) in Git is identified by a hash — a long string like `a1b2c3...` that's calculated from its content. If the content is identical, the hash is identical. This means Git never stores the same content twice, and it means that if even one character changes, you get a completely different hash. This is why commit IDs look random but are actually a fingerprint of the exact content.

### Branches are just pointers

A branch is not a copy of your project. It's just a sticky note that says "this is where `main` currently is" — pointing at one specific commit. When you commit new work, Git just moves that sticky note forward to the new commit. That's why creating a branch in Git is instant and cheap — you're not copying files, you're just placing a new sticky note.

### HEAD and "detached HEAD"

`HEAD` is a pointer to "whatever you currently have checked out" — normally it points to a branch (like `main`), which in turn points to a commit. A "detached HEAD" means you've checked out a specific commit directly instead of a branch. You can look around and even make new commits, but if you switch away without creating a branch first, those commits become hard to find again (though never truly deleted — more on that with `reflog`). It's not dangerous, just easy to get confused in.

### Daily commands, explained

- `git init` — turns a normal folder into a Git repository (starts tracking history here).
- `git clone` — downloads a copy of someone else's repository, including its full history.
- `git status` — tells you what's changed, what's staged, and what's untracked right now.
- `git diff` — shows the exact line-by-line changes in your working directory that aren't staged yet.
- `git diff --staged` — shows the changes that ARE staged (in the basket), ready to be committed.
- `git add` — moves a change from the working directory into the staging area (the basket).
- `git add -p` — lets you stage a file piece by piece ("patch mode") instead of all at once, useful when one file has two unrelated changes.
- `git commit` — saves everything currently staged as a new permanent snapshot.
- `git commit --amend` — fixes the most recent commit (e.g., you forgot a file or made a typo in the message) instead of making a brand new one.
- `git log` — shows the history of commits.
- `git log --oneline --graph --all` — same thing, but condensed to one line per commit and drawn as a visual branching diagram.
- `git show` — shows the full details (message + changes) of one specific commit.
- `git cat-file` — lets you peek directly at a raw Git object (a blob, tree, or commit) by its hash — useful for seeing "under the hood" that a commit really is just a tree pointer plus metadata.

**Why this matters:** once you really believe that a commit is just a snapshot (not a diff, not magic), and a branch is just a movable label, everything else in Git — merging, rebasing, resetting — becomes "moving labels and stitching snapshots together" instead of mysterious.

### Remotes

A "remote" is just another copy of the repository, usually sitting on a server like GitHub. `origin` is the conventional nickname for the main remote you cloned from. "Upstream" usually refers to the original repository you forked from, if you're contributing to someone else's project.

- `git remote add` — tells your local repo about another copy (gives it a name and URL).
- `git remote -v` — lists the remotes you currently know about.
- `git fetch` — downloads new commits from the remote but does NOT touch your current work — it just updates your knowledge of what's out there.
- `git pull` — does a fetch AND then tries to merge those new commits into your current branch, in one step.
- `git push` — uploads your local commits to the remote so others can see them.
- Tracking branches / `--set-upstream` — this just links your local branch to a specific remote branch, so plain `git push` and `git pull` know where to go without you specifying every time.
- **Fast-forward vs non-fast-forward push**: a fast-forward push means your branch's history is simply "ahead" of the remote — no conflict, Git just slides the pointer forward. A non-fast-forward push means the remote has commits you don't have locally — Git refuses the push until you pull/merge first, to avoid accidentally erasing someone else's work.

### Ignoring and cleaning files

- `.gitignore` — a file listing patterns for things Git should never track (e.g., `node_modules/`, `*.log`). This keeps build artifacts and secrets out of history.
- Global vs repo-level ignore — a global ignore file applies to every repo on your machine (e.g., your OS's junk files); a repo-level `.gitignore` is specific to that project and gets shared with your team.
- `git rm --cached` — stops tracking a file without deleting it from your disk. Useful when you accidentally committed something that should've been ignored.
- `git clean -n` — shows what untracked files WOULD be deleted (a dry run, nothing actually happens).
- `git clean -fd` — actually deletes those untracked files and folders. Use carefully — this is permanent.

### Undoing changes — the three different "undo" commands

This trips up almost everyone, so here's the plain breakdown:

- `git restore <file>` — throws away uncommitted changes in your working directory, restoring the file to how it last looked in the repository. Use this when you made a mess and haven't committed yet.
- `git reset` — moves your branch pointer backward to an earlier commit. It has three flavors depending on what you want to happen to your changes:
  - `--soft` — moves the pointer back, but keeps all your changes staged (ready to re-commit).
  - `--mixed` (the default) — moves the pointer back, keeps your changes in the working directory, but unstages them.
  - `--hard` — moves the pointer back AND throws away all changes. This is the dangerous one — your edits disappear from your working directory too.
- `git revert` — instead of erasing a commit, it creates a brand new commit that undoes the effects of an earlier one. This is the safe choice for anything already pushed/shared, because it doesn't rewrite history — it just adds a correction on top.

Simple rule of thumb: **restore** = "undo my uncommitted edits." **reset** = "move my branch backward in time" (only do `--hard` on commits nobody else has). **revert** = "publicly undo a commit that others may already have."

### git reflog — your safety net

Every time `HEAD` moves (new commit, checkout, reset, rebase...), Git secretly logs it in the reflog. So even if you do something scary like `reset --hard` and seemingly lose work, the old commit still exists and `git reflog` can show you its hash so you can get back to it. This is why experienced Git users rarely panic — almost nothing is actually gone, it's just temporarily unreferenced.

---

## Phase 2: Branching, Collaboration and Workflows

### Branching and merging in plain words

Branching lets you work on something new without touching the main line of work. Imagine `main` as the trunk of a tree, and a feature branch as a new limb growing off it — you can work on that limb freely, and later decide whether to graft it back onto the trunk.

- `git branch` — lists or creates branches.
- `git switch` / `git checkout -b` — moves you onto a branch (the `-b` version creates it first).
- **Fast-forward merge** — happens when the branch you're merging in is simply "ahead" with no new commits on the other side; Git just slides the pointer forward, no new commit needed.
- **Three-way merge** — happens when both branches have new commits since they split. Git looks at the common ancestor and both tips, then creates a new "merge commit" that combines both lines of work.
- `git merge` — performs the merge described above.
- A **merge commit** has two parents instead of one — that's literally how you can tell, in the history graph, that two lines of work joined together there.
- Deleting branches: `-d` only deletes a branch if it's already fully merged (safe); `-D` force-deletes it even if it has unmerged work (dangerous — you could lose commits unless reflog saves you).

### Conflicts — what they actually are

A conflict happens when Git can't automatically decide how to combine two changes to the same lines of a file. It's not an error exactly — it's Git saying "you two edited the same spot differently, you decide which parts to keep." Git marks the disputed area in the file with special markers like:

```
<<<<<<< HEAD
your version
=======
their version
>>>>>>> branch-name
```

You edit the file to keep what you want (deleting the markers), then stage and commit it to finish the merge.

- `git mergetool` — opens a visual tool to make this editing easier instead of doing it by hand.
- `git diff` during a conflict — shows you both sides so you can compare before deciding.
- `git merge --abort` — cancels the whole merge attempt and puts you back to how things were before you started, if things get too messy.
- Conflicts with renamed files are trickier because Git has to first figure out "this file was renamed" before it can even compare content — sometimes it guesses wrong, so renamed-file conflicts need extra attention.

### Rebasing — what it really does

Rebasing takes the commits you made on your branch and "replays" them one by one on top of a different starting point (usually the latest `main`). Picture it like this: instead of saying "my branch and main grew apart and we're stitching them together" (merge), rebase says "pretend I started my work AFTER all of main's latest changes" — it rewrites your commits as if that were true from the start.

- `git rebase <branch>` — does this replay onto the named branch.
- **Interactive rebase** (`git rebase -i`) — lets you edit your own commit history before replaying it: squash (combine commits), reword (change a message), reorder, or drop (delete) commits. Great for cleaning up messy "oops", "fix typo", "actually fix it" commits into one clean commit before sharing your work.
- **Why hashes change** — because a commit's hash depends on its content AND its parent. If you replay a commit onto a new parent, even if the actual code change is identical, it becomes a technically new commit with a new hash.
- **The golden rule of rebase** — never rebase commits that other people have already pulled and built on top of. If you do, their history and yours no longer match, causing confusion and duplicate commits. Rebasing your own not-yet-shared work is totally safe.
- `git rebase --abort` / `--continue` — abort cancels and restores your branch to before the rebase started; continue is what you run after resolving a conflict mid-rebase, to keep replaying the remaining commits.
- `git pull --rebase` vs plain `git pull` — plain pull does fetch + merge (creates a merge commit if histories diverged); `--rebase` does fetch + rebase instead (replays your local commits on top, keeping history linear, no merge commit).

### Merge vs rebase — how to actually choose

Merge preserves exactly what happened (including the fact that two branches diverged and rejoined) — more "honest" history, but can look cluttered with lots of merge commits. Rebase produces a clean, linear, easy-to-read history — but it rewrites commits, so it's only safe for work nobody else has already pulled. A common team rule: rebase your own feature branch to clean it up before opening a pull request, but merge (not rebase) once it's going into the shared `main` branch.

`git merge --no-ff` forces a merge commit even when a fast-forward would've been possible — some teams use this intentionally so the history graph clearly shows "this is where feature X was merged," rather than disappearing invisibly into a straight line.

### Collaboration workflows, in plain terms

- **Trunk-based development** — everyone commits small changes directly (or via very short-lived branches) straight into the main line frequently. Favors speed and continuous integration over long-lived branches.
- **GitHub Flow** — make a feature branch, open a pull request, get it reviewed, merge into `main`. Simple and common for most modern teams.
- **Git Flow** — a heavier structure with dedicated `develop`, `release`, and `hotfix` branches alongside `main`. Useful for projects with scheduled releases and multiple versions in production at once, but overkill for small or fast-moving teams.
- **Fork-and-pull-request** — used in open source: you can't push directly to someone else's repo, so you copy it ("fork"), make changes there, then ask them to pull your changes in via a pull request.
- A good pull request is small, focused on one thing, and has a description explaining *why* the change was made, not just *what* changed — this makes it reviewable in minutes instead of hours.
- `--force-with-lease` — a safer version of force-push. Regular `--force` overwrites the remote branch no matter what. `--force-with-lease` checks first that nobody else has pushed new work since you last looked — if they have, it refuses, protecting you from accidentally erasing a teammate's commits.

---

## Phase 3: History, Internals and Advanced Operations

### Rewriting history, without fear

"Rewriting history" sounds alarming, but it just means replacing old commits with new ones that have the same intent but cleaner form (better message, combined commits, removed mistake). The key thing to remember: Git never truly destroys old commits immediately — they stick around until garbage collection, which is why recovery is almost always possible (see reflog below).

- `git commit --amend` — replaces your very last commit with a corrected version (new message and/or new staged changes).
- Interactive rebase lets you go further back and reword, edit, squash (combine into the previous commit), fixup (combine but discard the message), or drop (remove entirely) older commits.
- `git commit --fixup` + `git rebase -i --autosquash` — a shortcut workflow: you mark a commit as "this fixes an earlier commit," and autosquash automatically reorders and combines them for you during the next interactive rebase, instead of you manually reordering things.
- `git filter-repo` (and the older `git filter-branch`) — tools for rewriting LARGE amounts of history at once, e.g., scrubbing a secret or password that was accidentally committed many commits ago. This changes every commit hash after that point.
- **Important consequence**: once you rewrite history that others have already fetched, their copy no longer matches. They'll need to re-sync (often by re-cloning or carefully rebasing), which is why rewriting shared history always needs clear communication to the team.
- If you remove a secret from history, you must still treat that secret as compromised and rotate/change it — deleting it from Git doesn't undo the fact that it was exposed at some point (someone may have already copied it).

### Recovery — Git's safety net in more detail

- `git reflog` records every time `HEAD` or a branch pointer moved — not file content directly, but it lets you find the commit that content was saved in. So if you know roughly when something existed, reflog can usually point you back to it.
- Recovering from a bad `reset --hard`: find the old commit hash in `git reflog`, then `git reset --hard <that hash>` (or check it out into a new branch) to get your work back.
- Recovering a deleted branch: the branch's last commit still exists as an object; reflog (or `git log` on another ref that touched it) can reveal its hash, and you can create a new branch pointing at it.
- `git fsck --lost-found` — a deeper recovery tool for finding "dangling" commits that aren't referenced by any branch and have already dropped out of the reflog. A last resort when reflog itself has expired.
- The reflog isn't permanent — it expires after a configurable window (90 days by default for reachable work, shorter for truly orphaned commits), so recovery isn't infinite, but it's generous enough that most real mistakes are recoverable within days or weeks.

### Debugging with Git

- `git bisect` — a way of binary-searching your history to find exactly which commit introduced a bug. You tell Git one commit that was "good" (bug didn't exist) and one that was "bad" (bug exists), and Git checks out commits in between, asking you each time "good or bad?" — narrowing it down in roughly log2(n) steps instead of checking every commit one by one.
- `git bisect run <script>` — automates the above: instead of you manually testing each checkout, you give Git a script that returns pass/fail, and it runs the whole search unattended.
- `git blame` — shows, line by line, which commit last touched each line of a file and who authored it. Useful for asking "why does this line exist?"
- `git log -S<string>` (the "pickaxe") — finds commits where the number of times a specific string appears in the file changed (added or removed), useful for finding exactly when a function or variable was introduced or deleted.
- `git log -G<regex>` — similar to pickaxe but matches a pattern/regex change in the actual diff content, more flexible for complex searches.
- `git log --follow` — tracks a file's history even across renames, so you don't lose the trail just because a file got renamed or moved at some point.

### Diffing and comparison

- `git diff A..B` (two dots) — compares the actual content of two commits/branches directly, tip to tip.
- `git diff A...B` (three dots) — compares each branch against their common ancestor ("merge base") instead of directly against each other — this answers "what did branch B actually add since it split from A," which is usually the more useful question when comparing feature branches.
- `git log branchA..branchB` — lists the commits that exist on branchB but not on branchA — handy for "what's new that I haven't merged yet."

### Internals, demystified

- **Refs** are just small text files under `.git/refs` containing a commit hash — that's literally what a branch or tag is on disk: a filename (the branch name) containing one line (a hash).
- **Loose objects** are individual files Git stores per object when they're first created. **Packfiles** are compressed bundles of many objects stored together efficiently — Git periodically compresses loose objects into packfiles to save space.
- `git gc` ("garbage collect") — cleans up and compresses the repository, packing loose objects together and removing genuinely unreachable data once it's safely past the recovery window.
- `git stash` — temporarily shelves your uncommitted changes so you can switch tasks cleanly. Under the hood, it's secretly just storing your changes as special commits that aren't attached to any branch, which is why they show up in certain Git internals even though they don't appear in your normal log.
- **Submodules** — a way of embedding one Git repository inside another, pinned to a specific commit, usually used for shared libraries. They're powerful but famously easy to get into a confusing state with (e.g., forgetting to update the pinned commit).
- **Worktrees** — let you check out a second branch into a separate folder at the same time, without needing to re-clone or stash your current work — useful when you need to work on two branches side-by-side.

---

## Phase 4: Automation, Hygiene and Team Practices

### Git hooks — automatic checks

A hook is just a script that Git automatically runs at a certain point in time, like a tripwire. They let you enforce rules without relying on people remembering to do them manually.

- **Client-side hooks** run on your own machine:
  - `pre-commit` — runs right before a commit is created; commonly used to run a linter or block committing secrets.
  - `commit-msg` — runs after you write a commit message, used to enforce a message format (e.g., requiring "feat:" or "fix:" prefixes).
  - `pre-push` — runs before pushing, e.g., to run tests one last time.
- **Server-side hooks** run on the remote server, not your machine:
  - `pre-receive` — runs before the server accepts incoming commits, can reject a push entirely.
  - `update` — similar, but runs once per branch being updated.
  - `post-receive` — runs after the push is accepted, often used to trigger deployments or notifications.
- **Limitation**: hooks live in the hidden `.git/hooks` folder, which is NOT copied when someone clones your repository — so by default, hooks aren't shared with the team automatically.
- **Hook managers** (Husky, the pre-commit framework, Lefthook) solve that limitation: they let you commit the hook configuration as a normal tracked file, which then installs the real hooks for everyone automatically when they set up the project.

### Conventions that keep history useful

- **Conventional Commits** — a standard format for commit messages, like `feat: add login page` or `fix: correct off-by-one error`. The benefit is that tools (and humans) can scan history and immediately tell what kind of change each commit was.
- This connects to **semantic versioning** (the `MAJOR.MINOR.PATCH` version numbers you see on software) — if commit messages consistently say whether a change is a breaking change, a feature, or a fix, tools can automatically figure out the next version number.
- **Branch naming conventions** (`feature/`, `fix/`, `chore/`) — simple prefixes that make it obvious at a glance what a branch is for, and let automation (like CI rules) treat different branch types differently.
- **PR merge strategies**:
  - *Squash-merge* — combines all of a branch's commits into a single commit on `main`. Cleanest history, but loses the granular story of how the feature was built.
  - *Merge commit* — keeps every individual commit plus adds one merge commit tying it together. Preserves full detail, but can clutter history.
  - *Rebase-merge* — replays each commit individually onto `main` with no merge commit at all. Clean and linear, but loses the "this was one unit of work" grouping that squash gives you.

### CI integration, in plain terms

CI (Continuous Integration) is automation that reacts to your Git activity — usually "run tests/checks whenever someone pushes or opens a pull request."

- **Branch protection rules** — settings on the remote (like GitHub) that prevent people from pushing directly to important branches (like `main`) without going through review and passing checks first.
- **Shallow clones** (`--depth`) — download only the most recent slice of history instead of the entire project history. CI systems use this because they usually only need the current code, not years of history, so it's much faster.
- CI caching depending on consistent naming just means: if your cache system is keyed off branch or tag names, renaming branches unpredictably can silently break your cache and slow builds down.

### Repository hygiene — keeping things tidy over time

- `git fetch --prune` — cleans up your local list of remote branches that no longer exist on the server (e.g., branches that were already deleted after merging), so your branch list doesn't get cluttered with ghosts.
- Over time, a repository accumulates lots of loose data; `git gc` (mentioned above) keeps this compact, but very large repos can still get genuinely slow or heavy without active maintenance.
- **Git LFS** (Large File Storage) — a system for handling big binary files (videos, design files, datasets) without bloating the main repository; it stores a small pointer in Git and the actual large file elsewhere.
- `.gitattributes` — a config file for telling Git how to treat specific file types, e.g., normalizing line endings between Windows and Mac/Linux, or telling Git how to diff/merge certain file formats sensibly (like treating binary files as binary, not as text).
- Shallow vs full clones for large repos — the same idea as CI shallow clones above, but applied generally: a huge monorepo might default new clones to a shallow or partial checkout so nobody has to download its entire multi-year history just to start working.

### Working at a larger scale

- **Monorepo vs polyrepo** — a monorepo keeps many projects in one single repository (simpler dependency management, but can get large and slow); a polyrepo splits each project into its own repository (more isolated, but coordinating changes across them is harder).
- **Sparse-checkout** — lets you check out only a subset of folders from a huge repository instead of the whole thing, useful when a monorepo is too large to reasonably download in full.
- **Worktrees** (again, from Phase 3) — handy at scale because switching branches in a huge repo can be slow; a worktree avoids that by letting two branches exist as separate folders simultaneously.
- **Submodules pitfalls** — the most common one is forgetting that a submodule is pinned to an exact commit, not "whatever is latest" — so teammates can end up looking at outdated submodule code without realizing it needs an explicit update.

### Incident response — what to do when things go wrong

- **Secret committed to history**: the correct order is (1) rotate/replace the actual credential immediately — assume it's compromised the moment it was pushed, (2) rewrite history to remove it (e.g., with `filter-repo`), (3) force-push the cleaned history, (4) tell every collaborator to re-clone or carefully re-sync, since their old copies still contain the secret.
- **Main branch accidentally force-pushed over**: don't panic — check `git reflog` on any machine (yours or a teammate's) that still remembers the old position of `main`, and reset/push it back. As long as one machine still has the old commit referenced somewhere, the "lost" history can be restored.
- **Documentation for new team members** — writing down your team's actual conventions (branch names, commit style, which branches are protected) matters because Git itself enforces almost none of this by default; without documentation, every new person has to learn the unwritten rules the hard way.

---

**The big-picture takeaway**: almost everything in Git is built from three simple ideas — commits are snapshots, branches are movable pointers, and nothing is truly deleted until garbage collection runs. Once those three ideas are solid, every command in this roadmap is just a specific way of creating, moving, or inspecting those same basic building blocks.
