# Linux Fundamentals

A working knowledge of Linux is essential in a SOC environment for log analysis, incident response, and system investigation. Below is a summary of core concepts and commands I am proficient with.

---

## Core Concepts

- **File System Hierarchy** — Key directories include `/etc` (system config & credentials), `/var` (logs & variable data), `/tmp` (volatile storage, useful in pentesting), and `/root` (root user home).
- **User Permissions** — Linux uses Read/Write/Execute permissions per user/group/other, managed via `ls -l` and `chmod`.
- **Processes** — Every running program has a Process ID (PID). Processes can be monitored, managed, and killed using signals (`SIGTERM`, `SIGKILL`, `SIGSTOP`).
- **SSH** — Secure Shell enables encrypted remote access and file transfers between systems.
- **Cron Jobs** — Scheduled tasks defined in a crontab, useful for automating backups, scripts, and recurring jobs.

---

## Essential Commands

| Command | Purpose |
|---|---|
| `ls -lh` | List files with permissions and human-readable sizes |
| `cat <file>` | Read file contents — useful for viewing logs |
| `grep "value" <file>` | Search file contents for a specific string (e.g. an IP in an access log) |
| `find -name "*.txt"` | Recursively search the filesystem for files by name |
| `pwd` | Print current working directory |
| `ps aux` | List all running processes, including system and other-user processes |
| `top` | Real-time process monitoring |
| `kill <PID>` | Terminate a process by its ID |
| `uname -a` | Display OS, kernel version, and architecture |
| `df -h` | Show disk usage in human-readable format |
| `nano <file>` | Create or edit a file in the terminal |
| `chmod` | Modify file permissions |
| `ssh user@ip` | Connect to a remote machine securely |
| `wget <url>` | Download a file from the web via HTTP |
| `systemctl [start\|stop\|enable\|disable] <service>` | Manage system services (e.g. apache2) |

---

## Operators

| Operator | Function |
|---|---|
| `&&` | Run a second command only if the first succeeds |
| `>` | Redirect output to a file (overwrites) |
| `>>` | Append output to a file |
| `&` | Run a command in the background |

---

## SOC-Relevant Highlights

- **Log investigation:** `cat` and `grep` are go-to tools for parsing web server logs and identifying suspicious IPs or patterns.
- **Process analysis:** `ps aux` and `top` support identification of unusual or malicious processes during incident response.
- **File discovery:** `find` and `grep` enable rapid hunting across the filesystem for indicators of compromise.
- **`/etc/passwd` & `/etc/shadow`:** Awareness of where Linux stores user credentials (sha512 encrypted) is critical for both defence and forensics.
```
