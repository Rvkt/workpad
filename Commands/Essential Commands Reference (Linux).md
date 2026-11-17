# Essential Commands Reference

Part of [[Linux Roadmap - Index|Linux System Administration Roadmap]]. A quick-lookup table; the phase notes cover the *why* behind each command.

| Category | Command | Purpose |
|---|---|---|
| Navigation | `pwd`, `cd`, `ls -la` | Filesystem navigation |
| Files | `find`, `du -sh`, `df -h` | Locate files, inspect disk usage |
| Links | `ln`, `ln -s` | Hard and symbolic links |
| Text | `grep -E`, `sed`, `awk` | Search, transform, and extract text |
| Text | `cat`, `less`, `tail -f` | View and follow file contents |
| Pipelines | `xargs`, `tee` | Build commands from input, split output |
| Processes | `ps aux`, `top` / `htop` | Inspect running processes |
| Processes | `kill`, `pkill`, `killall` | Send signals to processes |
| Jobs | `jobs`, `fg`, `bg`, `nohup` | Foreground/background job control |
| Sessions | `tmux` / `screen` | Persistent terminal sessions |
| Users | `useradd`, `usermod`, `id`, `groups` | User and group management |
| Permissions | `chmod`, `chown`, `setfacl`/`getfacl` | Access control |
| Privilege | `sudo`, `visudo` | Controlled privilege escalation |
| Networking | `ip addr`, `ip route` | Interface and routing configuration |
| Networking | `ss`, `lsof -i` | Inspect open ports and connections |
| Networking | `curl`, `dig`, `traceroute`/`mtr` | HTTP, DNS, and path diagnostics |
| Services | `systemctl status/start/enable` | Manage systemd services |
| Logs | `journalctl -u <unit> -f` | Follow a service's logs |
| Logs | `logrotate` | Rotate and retain log files |
| Performance | `vmstat`, `iostat`, `free -h` | System resource snapshots |
| Limits | `ulimit`, `nice`/`renice` | Per-process resource and priority limits |
| Security | `fail2ban-client status` | Check brute-force protection |
| Scheduling | `crontab -e` | Schedule recurring tasks |
| Scripting | `set -euo pipefail` | Safer bash script defaults |
