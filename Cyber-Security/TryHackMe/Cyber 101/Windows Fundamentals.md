# Windows Fundamentals

## Core Concepts

- **File System** — Windows uses NTFS (New Technology File System) for managing files and permissions.
- **User & Group Management** — Managed via `lusrmgr.msc`. Users and groups control access and permissions across the system.
- **Event Viewer** — Logs system, application, and security events, essential for monitoring and troubleshooting.
- **Windows Registry** — A hierarchical database storing system and application configuration settings.
- **Task Manager** — Provides real-time monitoring of processes, CPU, memory, and network usage.
- **Resource Monitor** — More detailed view of CPU, memory, disk, and network activity.
- **Windows Update** — Security patches released on Patch Tuesday (2nd Tuesday of each month).

---

## Key System Tools

| Tool | Access | Purpose |
|---|---|---|
| System Configuration | `msconfig` | Troubleshoot startup and configuration issues |
| Computer Management | `compmgmt.msc` | Manage users, storage, services, and more |
| System Information | `msinfo32` | View hardware, OS, and environment details |
| Resource Monitor | `resmon` | Detailed CPU, memory, disk, and network stats |
| Event Viewer | `eventvwr` | View and analyse system and security logs |
| WMI Control | `wmimgmt.msc` | Configure Windows Management Instrumentation |

---

## Command Prompt Essentials

| Command | Purpose |
|---|---|
| `dir` | List contents of a directory (equivalent to `ls` on Linux) |
| `dir /a` | List all files including hidden ones |
| `dir /s filename.txt` | Search for a file in the current directory and subdirectories |
| `cd` | Change or display current directory (equivalent to `cd`/`pwd` on Linux) |
| `type filename.txt` | Read the contents of a file (equivalent to `cat` on Linux) |
| `whoami` | Display the current logged-in user account |
| `hostname` | Display the computer name |
| `systeminfo` | Display detailed OS and system information |
| `ipconfig` | Show network configuration and IP addresses |
| `netstat` | Display active TCP/IP connections and protocol stats |
| `cls` | Clear the terminal screen |

> Full command reference: [ss64.com/nt](https://ss64.com/nt)

---

## Windows Security Features

- **Trusted Platform Module (TPM)** — Hardware-based security chip that handles cryptographic operations. Tamper-resistant and used to protect security functions at the hardware level.
- **BitLocker** — Drive encryption feature that protects data on lost or stolen devices by encrypting the entire drive. Works in conjunction with TPM.
- **Windows Security Centre** — Centralised dashboard for managing antivirus, firewall, device health, and other security settings.
