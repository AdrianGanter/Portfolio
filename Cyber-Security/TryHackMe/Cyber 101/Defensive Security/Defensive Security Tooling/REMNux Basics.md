# REMnux: Getting Started

## Overview
REMnux is a Linux distribution designed for malware analysis and reverse engineering. In this room, I used several REMnux tools to perform static malware analysis, simulate network activity, and preprocess forensic evidence for investigation.

---

# Static Malware Analysis with OleDump

## Purpose
Used `oledump.py` to analyze Microsoft Office documents containing embedded VBA macros.

### Key Concepts
- OLE2 (Object Linking and Embedding) files can contain multiple embedded data streams.
- VBA macros are commonly used by malware to execute malicious code when a document is opened.
- OleDump identifies and extracts these streams for analysis.

### Commands Used

List OLE streams:

```bash
oledump.py agenttesla.xlsm
```

Inspect a specific stream:

```bash
oledump.py agenttesla.xlsm -s 4
```

Decompress VBA macro code:

```bash
oledump.py agenttesla.xlsm -s 4 --vbadecompress
```

### Findings
The VBA macro contained an obfuscated PowerShell command.

Obfuscation was removed using CyberChef by:
- Replacing `*` with nothing
- Replacing `^` with nothing

<img width="1365" height="612" alt="image" src="https://github.com/user-attachments/assets/2309102f-4774-4588-8de5-ab0fe65898d7" />

### Decoded PowerShell Behaviour

```powershell
powershell -WindowStyle hidden -executionpolicy bypass
```

The script:

1. Launches PowerShell in a hidden window.
2. Bypasses PowerShell execution policy restrictions.
3. Downloads a file using `Invoke-WebRequest`.
4. Saves the file to a temporary location.
5. Executes the downloaded file using `Start-Process`.


### Indicators Observed

Downloaded file:

```text
Doc-3737122pdf.exe
```

Downloaded from:

```text
http://193.203.203.67/rt/Doc-3737122pdf.exe
```

### Malware Technique Demonstrated
A malicious Office document executes a VBA macro that downloads and launches a second-stage payload, helping attackers evade detection.

---

# Malware Network Simulation with INetSim

## Purpose
Used INetSim to simulate internet services commonly contacted by malware.

### Configuration

Edit INetSim configuration:

```bash
sudo nano /etc/inetsim/inetsim.conf
```

Configure DNS responses:

```text
dns_default_ip <REMnux_IP>
```

Verify configuration:

```bash
cat /etc/inetsim/inetsim.conf | grep dns_default_ip
```

Start INetSim:

```bash
sudo inetsim
```

### Services Simulated
- DNS
- HTTPS
- FTP
- SMTP
- POP3

### Testing Malware-like Behaviour

Downloaded files from the simulated server:

```bash
sudo wget https://<REMnux_IP>/second_payload.zip --no-check-certificate
```

```bash
sudo wget https://<REMnux_IP>/second_payload.ps1 --no-check-certificate
```

### Observations
- INetSim returned fake payloads.
- Simulated how malware retrieves secondary payloads from command-and-control infrastructure.
- Allowed safe observation of network activity without contacting real servers.

---

# Reviewing INetSim Logs

## Purpose
Analyze network connections generated during testing.

### Report Location

```bash
/var/log/inetsim/report/
```

Read report:

```bash
sudo cat /var/log/inetsim/report/report.<session>.txt
```

### Information Captured
- Connection timestamps
- Protocol used
- HTTP/HTTPS method
- Requested URL
- File returned by INetSim

### Example Findings

```text
HTTPS connection
Method: GET
URL: https://10.49.x.x/second_payload.zip
```

### Key Takeaway
INetSim provides a safe environment for observing malware network behaviour while generating useful forensic logs.

---

# Memory Analysis with Volatility 3

## Purpose
Used Volatility 3 to preprocess a Windows memory image (`wcry.mem`) for forensic analysis.

### Memory Image

```text
wcry.mem
```

### Plugins Used

#### Process Tree

```bash
vol3 -f wcry.mem windows.pstree.PsTree
```

Displays processes in parent-child hierarchy.

#### Active Processes

```bash
vol3 -f wcry.mem windows.pslist.PsList
```

Lists running processes.

#### Command Line Arguments

```bash
vol3 -f wcry.mem windows.cmdline.CmdLine
```

Shows commands used to launch processes.

#### File Objects

```bash
vol3 -f wcry.mem windows.filescan.FileScan
```

Scans memory for file artefacts.

#### Loaded DLLs

```bash
vol3 -f wcry.mem windows.dlllist.DllList
```

Displays DLLs loaded by processes.

#### Process Scanning

```bash
vol3 -f wcry.mem windows.psscan.PsScan
```

Identifies processes from memory structures.

#### Injected Code Detection

```bash
vol3 -f wcry.mem windows.malfind.Malfind
```

Detects potentially injected or malicious code regions.

---

# Automated Volatility Preprocessing

## Purpose
Automate collection of forensic artefacts.

### Command Used

```bash
for plugin in windows.malfind.Malfind windows.psscan.PsScan windows.pstree.PsTree windows.pslist.PsList windows.cmdline.CmdLine windows.filescan.FileScan windows.dlllist.DllList; do vol3 -q -f wcry.mem $plugin > wcry.$plugin.txt; done
```

### Outcome
Generated separate output files for each plugin, allowing faster investigation and evidence review.

---

# Memory String Extraction

## Purpose
Extract readable strings from memory for keyword searching and artefact discovery.

### ASCII Strings

```bash
strings wcry.mem > wcry.strings.ascii.txt
```

### Unicode Little Endian

```bash
strings -e l wcry.mem > wcry.strings.unicode_little_endian.txt
```

### Unicode Big Endian

```bash
strings -e b wcry.mem > wcry.strings.unicode_big_endian.txt
```

### Benefits
Extracted:
- Usernames
- File paths
- URLs
- Commands
- Potential malware artefacts

### Key Takeaway
Preprocessing memory evidence significantly speeds up later forensic analysis by making important artefacts searchable and easier to review.

<img width="1361" height="619" alt="image" src="https://github.com/user-attachments/assets/0128ea19-9fff-4f3b-bb8f-d8f2dbc260fc" />

---

# Skills Demonstrated

- Static malware analysis
- VBA macro inspection
- PowerShell payload analysis
- Malware deobfuscation using CyberChef
- Network simulation with INetSim
- Malware traffic observation
- Log analysis
- Memory forensics with Volatility 3
- Automated forensic preprocessing
- String extraction from memory images
- Malware investigation workflow



