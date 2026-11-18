# Phase 3: Networking, Services and System Administration

Part of [[Linux Roadmap - Index|Linux System Administration Roadmap]]. Previous: [[Phase 2 - Processes, Users and Permissions]]. Next: [[Phase 4 - Performance, Security and Automation]].

**Duration:** Weeks 5–6
**Objective:** Configure networking, manage services, and diagnose system issues using logs.

## Week 5: Networking Fundamentals and Diagnostics

### Networking Basics

- [ ] IP addressing, subnets, and CIDR notation.
- [ ] `ip addr`, `ip route` (modern) vs. `ifconfig`, `route` (legacy).
- [ ] DNS resolution and `/etc/resolv.conf`, `/etc/hosts`.
- [ ] `ping`, `traceroute` / `mtr` for connectivity diagnostics.
- [ ] `curl` / `wget` for HTTP diagnostics.
- [ ] `ss` / `netstat` for inspecting open ports and connections.
- [ ] `dig` / `nslookup` for DNS diagnostics.

### Firewalls and Access

- [ ] `iptables` fundamentals (chains, rules).
- [ ] `ufw` / `firewalld` as higher-level firewall managers.
- [ ] SSH configuration (`/etc/ssh/sshd_config`), key-based auth, disabling password auth.
- [ ] SSH tunneling and port forwarding.
- [ ] Understand common ports (22, 80, 443, 3306, 5432) and what runs on them.

### Practical Tasks

- [ ] Diagnose a simulated "can't reach this host" problem using ping, traceroute, and DNS tools in sequence.
- [ ] Configure a firewall to allow only SSH and HTTP(S), and verify with `ss`.
- [ ] Set up SSH key-based authentication and disable password login.
- [ ] Use an SSH tunnel to access a service only bound to localhost on a remote machine.

**Deliverable:** Methodical network diagnosis skills and a correctly configured, secured SSH + firewall setup.

## Week 6: Services, Logging and Boot

### systemd

- [ ] Understand systemd as PID 1 and the init system.
- [ ] `systemctl start/stop/restart/enable/disable/status`.
- [ ] Writing a custom `.service` unit file.
- [ ] Understand unit dependencies (`Wants`, `Requires`, `After`).
- [ ] `systemctl daemon-reload` and when it's needed.
- [ ] Timers (`systemd` timers) as a cron alternative.

### Logging

- [ ] `journalctl` fundamentals: `-u`, `-f`, `--since`, `-p`.
- [ ] Traditional `/var/log` structure (`syslog`, `auth.log`, application logs).
- [ ] `logrotate` for log rotation and retention.
- [ ] Understand log levels and why they matter for triage.

### Boot Process

- [ ] High-level boot sequence: firmware/BIOS → bootloader (GRUB) → kernel → initramfs → systemd → targets.
- [ ] Understand runlevels / systemd targets conceptually.
- [ ] Boot into rescue/single-user mode for recovery.

### Practical Tasks

- [ ] Write a systemd service unit for a simple script and enable it to start on boot.
- [ ] Diagnose a deliberately broken service using `systemctl status` and `journalctl -u`.
- [ ] Configure `logrotate` for a custom application log.
- [ ] Boot into rescue mode and reset a forgotten root password (in a disposable VM).

**Deliverable:** The ability to manage services end to end — write, enable, diagnose, and log — and recover a broken boot.
