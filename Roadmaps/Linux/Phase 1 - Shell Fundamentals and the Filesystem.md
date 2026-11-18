---
tags: [roadmap, roadmap/linux]
---

# Phase 1: Shell Fundamentals and the Filesystem

Part of [[Linux Roadmap - Index|Linux System Administration Roadmap]]. Next: [[Phase 2 - Processes, Users and Permissions]].

**Duration:** Weeks 1–2
**Objective:** Build fluency navigating and manipulating the filesystem entirely from the shell.

## Week 1: Shell Basics and Filesystem Hierarchy

### Shell Fundamentals

- [ ] Understand the shell prompt, `$PATH`, and command resolution.
- [ ] Understand absolute vs. relative paths.
- [ ] `pwd`, `cd`, `ls`, `ls -la`.
- [ ] Shell history, tab completion, and keyboard shortcuts (`Ctrl+R`, `Ctrl+A/E`).
- [ ] Understand standard input, output, and error (stdin/stdout/stderr) as file descriptors 0/1/2.
- [ ] Redirection: `>`, `>>`, `<`, `2>`, `&>`.
- [ ] Pipes (`|`) and command chaining (`&&`, `||`, `;`).
- [ ] Environment variables: `export`, `env`, `.bashrc` / `.bash_profile`.

### Filesystem Hierarchy

- [ ] Understand the Filesystem Hierarchy Standard: `/bin`, `/etc`, `/var`, `/home`, `/tmp`, `/usr`, `/opt`.
- [ ] Understand what lives in `/proc` and `/sys` as virtual filesystems.
- [ ] `mkdir`, `rmdir`, `cp`, `mv`, `rm`, `touch`.
- [ ] Understand hard links vs. symbolic links (`ln`, `ln -s`).
- [ ] Understand inodes conceptually.
- [ ] `find` for locating files by name, type, size, and modification time.
- [ ] `du`, `df` for disk usage.

### Practical Tasks

- [ ] Navigate a multi-level directory structure using only relative paths.
- [ ] Redirect a command's stdout to a file and stderr to a different file in one line.
- [ ] Chain three commands with pipes to filter and transform output.
- [ ] Find all files larger than 100MB modified in the last 7 days.

**Deliverable:** Fluent shell navigation and basic file manipulation without reaching for a GUI.

## Week 2: Text Processing and Package Management

### Text Processing

- [ ] `cat`, `less`, `head`, `tail`, `tail -f`.
- [ ] `grep` and regular expressions (`-E`, `-i`, `-v`, `-r`).
- [ ] `sed` for stream editing (substitution, deletion).
- [ ] `awk` for field-based processing.
- [ ] `cut`, `sort`, `uniq`, `wc`.
- [ ] `xargs` for building commands from input.
- [ ] `tee` for splitting output to a file and stdout simultaneously.

### Package Management

- [ ] `apt` (Debian/Ubuntu) fundamentals: update, upgrade, install, remove, search.
- [ ] `dnf` / `yum` (RHEL/Fedora) fundamentals.
- [ ] Understand package repositories and signing keys.
- [ ] Understand the difference between a package manager and a language-specific package manager (pip, npm).
- [ ] `dpkg` / `rpm` for inspecting installed packages directly.

### Practical Tasks

- [ ] Use `grep`, `sed`, and `awk` together to extract and transform data from a log file.
- [ ] Write a one-liner using `xargs` to operate on a list of files found by `find`.
- [ ] Install, upgrade, and cleanly remove a package, inspecting what files it installed.
- [ ] Parse a CSV-like file with `awk` to compute a sum or average of a column.

**Deliverable:** Comfort processing text and logs at the command line, and managing software through the system package manager.
