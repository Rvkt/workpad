# Phase 4: Performance, Security and Automation

Part of [[Linux Roadmap - Index|Linux System Administration Roadmap]]. Previous: [[Phase 3 - Networking, Services and System Administration]].

**Duration:** Weeks 7–8
**Objective:** Diagnose performance bottlenecks, harden systems, and automate recurring work with shell scripts.

## Week 7: Performance Monitoring and Resource Management

### CPU and Memory

- [ ] `top` / `htop` interpretation: load average, CPU%, memory breakdown.
- [ ] Understand load average vs. CPU utilization.
- [ ] `free -h` for memory usage, and the meaning of "available" vs. "free".
- [ ] `vmstat` for a quick system-wide resource snapshot.
- [ ] Understand swap and when heavy swapping indicates a real problem.

### Disk and I/O

- [ ] `iostat` for disk I/O statistics.
- [ ] `df -h`, `du -sh` for disk usage investigation.
- [ ] `lsof` for finding which process holds a file or port open.
- [ ] Diagnosing a full disk caused by deleted-but-open file handles.

### Resource Limits

- [ ] `ulimit` for per-process resource limits.
- [ ] `/etc/security/limits.conf` for persistent limits.
- [ ] cgroups at a conceptual level (what containers are built on).
- [ ] `nice` / `renice` for CPU scheduling priority.

### Practical Tasks

- [ ] Diagnose a simulated high-load scenario using `top`, `vmstat`, and `iostat` to identify the bottleneck type.
- [ ] Find and reclaim disk space held by a deleted-but-open file using `lsof`.
- [ ] Set a resource limit for a user and verify it's enforced.
- [ ] Use `nice`/`renice` to deprioritize a CPU-heavy background job.

**Deliverable:** The ability to identify whether a performance problem is CPU-, memory-, disk-, or I/O-bound, using the correct tool for each.

## Week 8: Security Hardening and Shell Scripting

### Security Hardening

- [ ] Disable root SSH login; enforce key-based auth.
- [ ] Keep packages updated; understand unattended-upgrades.
- [ ] Minimize running services to reduce attack surface.
- [ ] Configure `fail2ban` or equivalent against brute-force attempts.
- [ ] Understand SELinux / AppArmor at a conceptual level and check their status.
- [ ] File integrity basics: checksums (`sha256sum`) for verifying downloads.

### Shell Scripting

- [ ] `#!/usr/bin/env bash` shebang and script permissions.
- [ ] Variables, conditionals (`if`/`elif`/`else`), and `[[ ]]` test expressions.
- [ ] Loops (`for`, `while`) over files, lines, and command output.
- [ ] Functions and local variables.
- [ ] Positional arguments (`$1`, `$@`, `$#`) and flag parsing with `getopts`.
- [ ] `set -euo pipefail` and why it belongs in almost every script.
- [ ] Trapping signals (`trap`) for cleanup on exit or interrupt.
- [ ] Exit codes and checking them (`$?`).

### Automation

- [ ] `cron` syntax and `crontab -e`.
- [ ] Choosing between cron and a systemd timer.
- [ ] Idempotent scripts: safe to re-run without side effects.
- [ ] Logging script output for later troubleshooting.

### Practical Tasks

- [ ] Harden a fresh VM: disable root SSH, enforce keys, configure a firewall, install `fail2ban`.
- [ ] Write a backup script with `set -euo pipefail`, argument parsing, and a `trap` for cleanup on failure.
- [ ] Schedule the backup script with cron and verify it runs and logs correctly.
- [ ] Make the script idempotent and safe to re-run after a partial failure.

**Deliverable:** A hardened server and a working, idempotent automation script — the practical synthesis of the whole roadmap.
