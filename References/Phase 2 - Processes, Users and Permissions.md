# Phase 2: Processes, Users and Permissions

Part of [[Linux Roadmap - Index|Linux System Administration Roadmap]]. Previous: [[Phase 1 - Shell Fundamentals and the Filesystem]]. Next: [[Phase 3 - Networking, Services and System Administration]].

**Duration:** Weeks 3–4
**Objective:** Understand and control processes, and design correct permission schemes.

## Week 3: Process Management and Job Control

### Processes

- [ ] Understand PID, PPID, and the process tree.
- [ ] `ps aux`, `ps -ef`, `pstree`.
- [ ] `top` / `htop` for live process monitoring.
- [ ] Understand process states (running, sleeping, zombie, stopped).
- [ ] Understand what a zombie process actually is and why it happens.
- [ ] Signals: `SIGTERM`, `SIGKILL`, `SIGHUP`, `SIGINT` and their differences.
- [ ] `kill`, `killall`, `pkill`.

### Job Control

- [ ] Foreground vs. background jobs (`&`, `fg`, `bg`).
- [ ] `jobs`, `Ctrl+Z` to suspend.
- [ ] `nohup` and `disown` for processes that survive logout.
- [ ] `screen` / `tmux` for persistent terminal sessions.
- [ ] Understand parent/child process relationships and orphaned processes.

### Practical Tasks

- [ ] Start a long-running process, background it, then bring it back to the foreground.
- [ ] Deliberately create a zombie process and explain why it's not cleaned up.
- [ ] Use `tmux` to run a long task that survives an SSH disconnect.
- [ ] Send different signals to a running process and observe the differences.

**Deliverable:** Confidence managing running processes and understanding what each signal actually does.

## Week 4: Users, Groups and Permissions

### Users and Groups

- [ ] `/etc/passwd`, `/etc/shadow`, `/etc/group` structure.
- [ ] `useradd`, `usermod`, `userdel`, `groupadd`.
- [ ] `su` vs. `sudo`, and configuring `/etc/sudoers` safely with `visudo`.
- [ ] Understand UID/GID, and the special meaning of UID 0 (root).
- [ ] `id`, `whoami`, `groups`.

### Permissions

- [ ] Read/write/execute permission bits for owner/group/other.
- [ ] `chmod` with symbolic (`u+x`) and octal (`755`) notation.
- [ ] `chown`, `chgrp`.
- [ ] setuid, setgid, and the sticky bit, and what each actually does.
- [ ] Access Control Lists (`getfacl`, `setfacl`) for permissions beyond owner/group/other.
- [ ] Understand umask and default permission creation.

### Practical Tasks

- [ ] Create a new user, add them to a group, and verify their effective permissions.
- [ ] Configure a `sudoers` entry granting a user limited, specific command access.
- [ ] Set up a shared directory where two groups need different access levels using ACLs.
- [ ] Explain and demonstrate why a world-writable script with setuid root is dangerous.

**Deliverable:** A correctly designed multi-user permission scheme, understood down to the bit level.
