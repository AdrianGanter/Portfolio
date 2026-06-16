# CAPA: The Basics

## Overview

CAPA (Common Analysis Platform for Artifacts) is a malware analysis tool developed by Mandiant that identifies capabilities within executables by matching behavior-based rules.

Supported artifacts include:

- Portable Executables (PE)
- ELF binaries
- .NET assemblies
- Shellcode
- CAPE sandbox reports

CAPA helps analysts quickly understand what a program is capable of without performing full manual reverse engineering.

---

## Analysis Types

### Static Analysis
- Examines files without executing them
- Safer for malware investigation
- Primary focus of this room

### Dynamic Analysis
- Observes malware while it is running
- Requires an isolated environment or sandbox

---

# Running CAPA

### Basic Scan

```powershell
capa.exe .\cryptbot.bin
```

### Common Parameters

| Option | Purpose |
|----------|----------|
| `-h` | Display help menu |
| `-v` | Verbose output |
| `-vv` | Very verbose output |
| `-j` | Output results as JSON |

### Examples

```powershell
capa.exe .\cryptbot.bin
```

```powershell
capa.exe .\cryptbot.bin -v
```

```powershell
capa.exe .\cryptbot.bin -vv
```

```powershell
capa.exe -j -vv .\cryptbot.bin > cryptbot_vv.json
```

### Reading Output Files

```powershell
Get-Content .\cryptbot.txt
```

```powershell
Get-Content .\cryptbot_vv.txt
```

---

# Understanding CAPA Output

CAPA organizes findings into several categories:

## ATT&CK Mapping

Maps observed capabilities to MITRE ATT&CK tactics and techniques.

Examples:

- Obfuscated Files or Information (T1027)
- PowerShell Execution (T1059.001)
- File and Directory Discovery (T1083)
- Scheduled Tasks (T1053.005)

---

## MAEC Category

Provides malware classification.

Example:

```text
launcher
```

---

# Malware Behavior Catalogue (MBC)

MBC is a catalog of malware objectives, behaviors, and methods used to standardize malware analysis and reporting.

---

## MBC Structure

### Format 1

```text
OBJECTIVE::Behavior::Method [Identifier]
```

Example:

```text
ANTI-STATIC ANALYSIS::Executable Code Obfuscation::Argument Obfuscation [B0032.020]
```

### Format 2

```text
OBJECTIVE::Behavior [Identifier]
```

Example:

```text
COMMUNICATION::HTTP Communication [C0002]
```

---

# MBC Objectives

Objectives describe the malware's overall intent.

Examples:

| Objective | Purpose |
|------------|------------|
| Anti-Behavioral Analysis | Evade sandboxes and behavioral analysis |
| Anti-Static Analysis | Make reverse engineering harder |
| Collection | Gather information |
| Command and Control | Communicate with attacker infrastructure |
| Credential Access | Steal credentials |
| Defense Evasion | Avoid detection |
| Discovery | Learn about system environment |
| Execution | Run commands or code |
| Exfiltration | Steal data |
| Impact | Damage or manipulate systems |
| Lateral Movement | Spread across networks |
| Persistence | Maintain long-term access |
| Privilege Escalation | Gain elevated permissions |

---

# Micro-Objectives

Lower-level actions often used by malware.

Examples:

| Micro-Objective | Example Behaviors |
|-----------------|------------------|
| PROCESS | Create Process |
| MEMORY | Allocate Memory |
| COMMUNICATION | HTTP Communication |
| DATA | String Checking, Encoding |

---

# Common Behaviors Identified

| Behavior | ID | Meaning |
|-----------|----|----------|
| Lab Machine Detection | B0009 | Detect virtual machines |
| Executable Code Obfuscation | B0032 | Hide true code functionality |
| Command and Scripting Interpreter | E1059 | Execute scripts or commands |
| File and Directory Discovery | E1083 | Enumerate files |
| Obfuscated Files or Information | E1027 | Encode or hide data |

---

# Common Micro-Behaviors

| Behavior | ID |
|------------|----|
| Allocate Memory | C0007 |
| Create Process | C0017 |
| HTTP Communication | C0002 |
| Check String | C0019 |
| Encode Data | C0026 |
| Create Directory | C0046 |
| Delete File | C0047 |
| Read File | C0051 |
| Write File | C0052 |

---

# Methods (Sub-Techniques)

Methods provide additional detail about a behavior.

| Method | ID |
|----------|----|
| Argument Obfuscation | B0032.020 |
| Stack Strings | B0032.017 |
| Read HTTP Header | C0002.014 |
| Base64 Encoding | C0026.001 |
| XOR Encoding | C0026.002 |
| Standard Algorithm Encoding | E1027.m02 |

---

# CAPA Capabilities

Capabilities represent specific behaviors identified by CAPA rules.

Examples observed in CryptBot:

### Anti-Analysis

- Reference anti-VM strings
- Reference VMware strings
- Reference VirtualBox strings
- Obfuscated stack strings

### Communication

- Reference HTTP User-Agent strings
- Check HTTP status codes

### Data Manipulation

- Reference Base64 strings
- Encode data using XOR

### File System

- Create directories
- Delete files
- Read files
- Write files

### Process Interaction

- Create processes
- Allocate/change RWX memory
- Access thread-local storage

### Persistence

- Schedule task via `at`
- Schedule task via `schtasks`

### Execution

- Run PowerShell expressions

### Impact

- Reference cryptocurrency strings

---

# Namespaces

Namespaces group related capabilities.

## Common Top-Level Namespaces (TLN)

### anti-analysis
Detects:

- Anti-VM techniques
- Obfuscation
- Anti-debugging

### communication
Detects:

- Network communications
- HTTP activity
- C2 behaviors

### data-manipulation
Detects:

- Encoding
- Encryption
- Data transformation

### executable
Detects:

- PE attributes
- TLS sections
- Debug information

### host-interaction
Detects:

- File operations
- Process activity
- System interaction

### impact
Detects:

- Potential harmful effects
- Data destruction
- Cryptocurrency-related activity

### linking
Detects:

- Runtime linking
- External library loading

### load-code
Detects:

- Dynamic code loading
- PowerShell execution
- PE export parsing

### persistence
Detects:

- Scheduled tasks
- Long-term system access

### nursery
Contains experimental or unfinished rules.

---

# Capability → Rule Relationship

The capability name is generally the rule filename with spaces replaced by hyphens.

Example:

Capability:

```text
reference Base64 string
```

Rule:

```text
reference-base64-string.yml
```

Another example:

Capability:

```text
schedule task via schtasks
```

Rule:

```text
schedule-task-via-schtasks.yml
```

---

# CAPA Web Explorer

CAPA Web Explorer provides a graphical interface for analyzing verbose CAPA results.

### Workflow

Generate JSON output:

```powershell
capa.exe -j -vv .\cryptbot.bin > cryptbot_vv.json
```

Upload JSON into:

```text
CAPA Web Explorer
```

Benefits:

- Easier navigation
- Rule inspection
- Interactive analysis
- Search and filtering

---

# Investigating Rule Matches

CAPA rules contain features that trigger detections.

### Example: VMware Detection

Rule checks for strings matching:

```text
VMWare
```

using regex-based conditions.

### Example: Scheduled Tasks

Rule checks for:

```text
schtasks
```

and

```text
/create
```

or:

```text
Register-ScheduledTask
```

If matched, CAPA identifies persistence via scheduled tasks.

---

# Exercises Completed

### Generated CAPA Reports

```powershell
capa.exe .\cryptbot.bin
```

```powershell
capa.exe .\cryptbot.bin -v
```

```powershell
capa.exe .\cryptbot.bin -vv
```

### Viewed Report Files

```powershell
Get-Content .\cryptbot.txt
```

```powershell
Get-Content .\cryptbot_vv.txt
```

### Generated JSON Output

```powershell
capa.exe -j -vv .\cryptbot.bin > cryptbot_vv.json
```

### Explored Results in CAPA Web Explorer

- Uploaded JSON report
- Investigated rule matches
- Reviewed namespaces
- Examined malware capabilities
- Used search and filtering functionality

---

# Key Takeaways

- CAPA performs automated capability analysis on malware samples.
- Static analysis can reveal malware functionality without execution.
- MBC provides standardized malware objectives, behaviors, and methods.
- Namespaces organize capabilities into logical categories.
- CAPA rules are stored as YAML files and map directly to detected capabilities.
- Verbose (`-v`) and very verbose (`-vv`) modes provide deeper insight into detections.
- CAPA Web Explorer makes large analysis outputs significantly easier to investigate.
- CAPA can quickly identify persistence, communication, obfuscation, file operations, process activity, and other malicious behaviors.
