---
tags:
  - "#git"
  - "#command"
---

# Git Show Changed Files in Commit

Different approaches to inspect files modified, added, or deleted across single or multiple Git commits depending on whether you need commit metadata, a deduplicated file list, or insertion/deletion statistics.

---

## 🛠️ Approaches Overview

| Approach | Command Pattern | Best Used For |
| :--- | :--- | :--- |
| **1. Files in Specific Commit** | `git show --name-only --format=fuller <hash>` | Deep audit of a single commit with full author & committer metadata |
| **2. Unique Files Across Commits** | `git diff-tree --no-commit-id --name-only -r <hashes...> \| sort -u` | Deduplicated list of affected files across a batch or release |
| **3. Files with Commit Messages** | `git log -N --name-only --format="Commit: %h \| %s"` | Quick scan of recent commits and the files touched by each |
| **4. Change Summary with Stats** | `git log -N --stat` / `git show --stat <hash>` | High-level overview showing insertion and deletion numbers |

---

## 1. Files Changed in Each Commit (Detailed Audit)

Inspects the exact files modified by one or more commits, retaining author, committer, and timestamp headers without printing the entire patch diff.

```bash
git show --name-only --format=fuller <commit-hash>
```

### Example

```bash
git show --name-only --format=fuller e7504fbe005dbe3fc6c2254f6f027469408db3bf
git show --name-only --format=fuller ec16763c547f924c80e14ac94c8e07bff74656f7
git show --name-only --format=fuller 53e5747dddc4f1a9c4a8dd1d26ab578713ef7dfa
```

### Flags
- `--name-only`: Lists only affected file paths instead of unified diff chunks.
- `--format=fuller`: Displays `Author`, `AuthorDate`, `Commit`, and `CommitDate`.

---

## 2. All Unique Files Changed Across Multiple Commits

Extracts a clean, sorted, deduplicated list of every file modified across multiple commits (ideal for deployment scripts, CI/CD pipelines, or PR reviews).

```bash
git diff-tree --no-commit-id --name-only -r <commit1> <commit2> ... | sort -u
```

### Example

```bash
git diff-tree --no-commit-id --name-only -r \
  e7504fbe005dbe3fc6c2254f6f027469408db3bf \
  ec16763c547f924c80e14ac94c8e07bff74656f7 \
  53e5747dddc4f1a9c4a8dd1d26ab578713ef7dfa | sort -u
```

### Flags
- `diff-tree`: Low-level plumbing command that compares trees directly.
- `--no-commit-id`: Suppresses printing the commit SHA prefix.
- `-r`: Recurses into subdirectories to catch nested files.
- `sort -u`: Deduplicates file paths that were modified in more than one of the specified commits.

---

## 3. Files Changed with Commit Messages (Compact Log)

Displays a quick commit-by-commit summary with short SHA, commit message subject, and the files changed in that commit.

```bash
git log -N --name-only --format="Commit: %h | %s"
```

### Example (Last 3 Commits)

```bash
git log -3 --name-only --format="Commit: %h | %s"
```

### Single Specific Commit

```bash
git log -1 --name-only --format="Commit: %h | %s" <commit-hash>
```

---

## 4. Change Summary with Insertions and Deletions (Diffstat)

Reports the file list alongside the number of insertions and deletions (`+` and `-` bars) to understand the magnitude of each change.

### Recent Commits History

```bash
git log -3 --stat
```

### Single Specific Commit

```bash
git show --stat <commit-hash>
```

---

## 💡 Recommendation

> [!tip] Quick Choice Guide
> - **Use Option 3 (`git log --name-only`)** for a quick commit-by-commit file list with message context.
> - **Use Option 4 (`git log --stat`)** when you also need to report or gauge the size/volume of the changes.
> - **Use Option 2 (`git diff-tree | sort -u`)** when generating a unique file list across multiple commits for scripting or release notes.
> - **Use Option 1 (`git show --name-only --format=fuller`)** for in-depth author/committer audit on specific commits.

---

## ⚠️ Notes & Caveats

- Ensure target commit SHAs exist in the local Git object store. If inspecting remote commits, fetch them first with `git fetch origin`.
- On Windows PowerShell, multiline backslashes `\` can be replaced with standard single-line commands or PowerShell backticks `` ` ``.

---

## Related

- [[Work MOC|Work MOC]]
- [[Home|Home Dashboard]]
