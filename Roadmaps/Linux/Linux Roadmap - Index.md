---
tags: [roadmap, roadmap/linux]
---

# Linux System Administration Roadmap

**Level:** Intermediate → Senior/Lead
**Duration:** 8 Weeks
**Weekly Commitment:** 3–5 Hours
**Learning Approach:** Hands-on practice on a real or virtual machine, understanding mechanisms rather than memorizing commands.

---

## Learning Objectives

By completing this roadmap, the goal is to develop competency in:

- [ ] The shell, filesystem hierarchy, and text-processing tools.
- [ ] Process management and job control.
- [ ] Users, groups, and permission models.
- [ ] Package management and system services.
- [ ] Networking configuration and diagnostics.
- [ ] System logging and troubleshooting.
- [ ] Performance monitoring and resource management.
- [ ] Shell scripting and task automation.
- [ ] Security hardening and access control.
- [ ] Explaining Linux behavior from first principles, not folklore.

---

## Roadmap Notes

- [[Phase 1 - Shell Fundamentals and the Filesystem]] (Weeks 1–2)
- [[Phase 2 - Processes, Users and Permissions]] (Weeks 3–4)
- [[Phase 3 - Networking, Services and System Administration]] (Weeks 5–6)
- [[Phase 4 - Performance, Security and Automation]] (Weeks 7–8)
- [[Essential Commands Reference (Linux)]]
- [[Learning Resources (Linux)]]

---

## Weekly Progress Tracking

- [ ] [[Phase 1 - Shell Fundamentals and the Filesystem|Phase 1: Shell Fundamentals and the Filesystem]]
- [ ] [[Phase 2 - Processes, Users and Permissions|Phase 2: Processes, Users and Permissions]]
- [ ] [[Phase 3 - Networking, Services and System Administration|Phase 3: Networking, Services and System Administration]]
- [ ] [[Phase 4 - Performance, Security and Automation|Phase 4: Performance, Security and Automation]]

### Completion Criteria

The roadmap should not be considered complete merely because all topics have been studied.

You should be able to:

- [ ] Navigate and manipulate a filesystem entirely from the shell, without a GUI.
- [ ] Explain the difference between a process, a thread, and a zombie, and diagnose each.
- [ ] Design a permission scheme for a multi-user system using owners, groups, and ACLs correctly.
- [ ] Diagnose a "service won't start" problem using logs and `systemctl status` methodically.
- [ ] Capture and interpret network traffic to debug a connectivity issue.
- [ ] Identify a resource bottleneck (CPU, memory, disk I/O, network) using the correct tool for each.
- [ ] Write a shell script that handles errors, arguments, and edge cases correctly.
- [ ] Harden a fresh server against common attack vectors (SSH, firewall, unnecessary services).
- [ ] Recover a system from a full disk, a runaway process, or a misconfigured service without reinstalling.

---

## Execution Rules

1. Follow the phases in order; later diagnostics assume fluency with processes and permissions from Phase 2.
2. Practice on a disposable VM or container — break things deliberately and fix them.
3. Read `man <command>` before searching the web; the manual pages are authoritative.
4. When something goes wrong, diagnose with logs (`journalctl`, `/var/log`) before reaching for a fix.
5. Prefer understanding *why* a command works over memorizing flags; the flags follow naturally once the model is clear.
6. Practice recovery scenarios deliberately (full disk, killed service, locked-out user) before a real incident forces it.

**Final Goal:** Administer, troubleshoot, secure, and automate Linux systems confidently, with the underlying mechanisms understood well enough to diagnose problems you've never seen before.
