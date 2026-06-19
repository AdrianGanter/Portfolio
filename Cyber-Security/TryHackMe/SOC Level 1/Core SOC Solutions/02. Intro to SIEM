# Introduction to SIEM

## Overview

A Security Information and Event Management (SIEM) platform is a centralised security solution used by SOC analysts to collect, analyse, and correlate logs from multiple systems.

Its primary purpose is to detect threats, investigate incidents, and provide visibility across an environment.

---

# Why SIEM?

Without a SIEM:

- Logs are spread across multiple devices
- Different systems generate different log formats
- Manual analysis is slow and inefficient
- Important security events can be missed

SIEM solves these problems by centralising and automating log analysis.

---

# Log Sources

## Host-Centric Logs

Generated directly from systems and endpoints.

Examples:

- User logins
- File access
- Process execution
- PowerShell activity

Sources:

- Windows
- Linux
- Servers

---

## Network-Centric Logs

Generated from network activity.

Examples:

- VPN connections
- SSH sessions
- Web traffic
- Firewall events

Sources:

- Firewalls
- IDS/IPS
- Routers
- VPN appliances

---

# Core SIEM Functions

### Log Collection
Aggregates logs from multiple devices into a single platform.

### Normalization
Converts different log formats into a standard structure.

### Correlation
Links related events together to identify suspicious activity.

### Alerting
Triggers alerts when predefined detection rules are matched.

### Dashboards
Provides visibility into alerts, events, and security trends.

---

# Common Log Sources

## Windows

Important Event IDs:

| Event ID | Description |
|-----------|-----------|
| 4624 | Successful login |
| 4625 | Failed login |
| 4688 | Process creation |
| 104 | Event log cleared |

## Linux

Common locations:

- `/var/log/auth.log`
- `/var/log/secure`
- `/var/log/cron`
- `/var/log/httpd`

## Web Servers

Typically record:

- Source IP
- Timestamp
- HTTP Method
- URL
- Status Code
- User Agent

---

# Log Ingestion Methods

- Agent / Forwarder
- Syslog
- Manual Upload
- Port Forwarding

---

# Detection Rules

SIEMs generate alerts when specific conditions are met.

Examples:

- Multiple failed login attempts
- Successful login after repeated failures
- Large outbound data transfers
- USB device insertion

Example:

**Event ID 104** → Alert when Windows event logs are cleared.

---

# Alert Investigation

Typical workflow:

1. Review alert
2. Examine related events
3. Determine True or False Positive
4. Investigate further if required
5. Contain or remediate the threat

Possible actions:

- Tune detection rules
- Contact asset owner
- Isolate infected host
- Block malicious IPs

---

# Practical Lab

Investigated a SIEM alert involving cryptocurrency mining malware.

### Findings

| Artifact | Result |
|-----------|-----------|
| Process | cudominer.exe |
| User | chris |
| Hostname | HR_02 |
| Trigger Keyword | miner |
| Classification | True Positive |


<img width="1902" height="984" alt="image" src="https://github.com/user-attachments/assets/3d1dc8c0-9145-458f-8966-7999e21ab637" />


---

# Key Takeaways

- SIEM centralises security logs for monitoring and investigation.
- Host and network logs provide valuable security visibility.
- Log normalization and correlation improve threat detection.
- Detection rules generate alerts for suspicious activity.
- Analysts investigate alerts and determine appropriate response actions.
