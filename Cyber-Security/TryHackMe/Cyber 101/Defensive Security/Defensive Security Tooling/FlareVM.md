# FlareVM: Arsenal of Tools

## Overview

FlareVM is a Windows-based malware analysis, incident response, and digital forensics environment containing a wide range of tools used for:

- Static malware analysis
- Dynamic malware analysis
- Reverse engineering
- Memory forensics
- Network analysis
- Incident response investigations

The platform consolidates commonly used security tools into a single investigation environment.

---

# Key Investigation Tools

## Process Monitor (Procmon)

Used to monitor real-time system activity including:

- File system operations
- Registry modifications
- Process activity
- Thread activity

### Practical Understanding

- Applied filters to isolate specific processes
- Monitored process behaviour during execution
- Identified file access and system interactions
- Used for malware behaviour observation


---

## Process Explorer (Procexp)

Used to examine running processes and parent-child relationships.

### Practical Understanding

- Identified process hierarchy
- Examined process IDs (PIDs)
- Determined parent and child process relationships
- Investigated active network connections from processes

### Example

Observed:

Explorer.exe

└── cobaltstrike.exe

Used process properties to review TCP/IP connections and destination hosts.

<img width="1366" height="588" alt="image" src="https://github.com/user-attachments/assets/be0d7fa8-81f2-4425-97f4-7c3dce703e75" />

---

## HxD

Hex editor used for examining binary files.

### Practical Understanding

- Viewed raw hexadecimal file contents
- Compared hexadecimal and ASCII representations
- Identified file signatures (magic bytes)
- Examined executable headers

### Example

Detected:

4D 5A

(MZ header)

This indicates the file is a Windows Portable Executable (PE).

---

## CFF Explorer

Portable Executable (PE) analysis tool.

### Practical Understanding

Used to examine:

- File hashes
- PE headers
- DOS headers
- Compilation details
- Architecture information
- Executable metadata

### Information Gathered

- MD5
- SHA1
- SHA256
- PE structure
- DOS Header values
- e_magic signature

<img width="813" height="545" alt="image" src="https://github.com/user-attachments/assets/8a933ff7-9e21-47f6-9032-3a8ae4b937c3" />

---

## Wireshark

Network protocol analysis tool.

### Practical Understanding

- Captured network traffic
- Reviewed source and destination IP addresses
- Examined protocols and ports
- Investigated encrypted communications

### Observed

- TLS encrypted traffic
- Source and destination connections
- Protocol usage during execution

<img width="1366" height="616" alt="image" src="https://github.com/user-attachments/assets/8c660c80-03dd-4209-ad00-e18a15d83de2" />


---

## PEStudio

Static analysis tool used to inspect executables without executing them.

### Practical Understanding

Reviewed:

- Entropy values
- Manifest information
- Imported APIs
- Version metadata
- Indicators of packing or obfuscation
- File descriptions

### Analysis Findings

Suspicious indicators included:

- Executable masquerading as Registry Editor
- Russian-language metadata
- Missing Rich Header
- Potential packing/obfuscation

### Notable APIs Identified

#### Process Execution

- set_UseShellExecute

Used to launch additional processes through the Windows shell.

#### Cryptography

- CryptoStream
- RijndaelManaged
- CipherMode
- CreateDecryptor

Indicators of AES/Rijndael encryption functionality commonly observed in malware and ransomware.

<img width="1366" height="619" alt="image" src="https://github.com/user-attachments/assets/b8bee0a8-8ffc-45e6-9efe-2ef0bf0431a6" />


---

## FLOSS (FLARE Obfuscated String Solver)

Tool used to extract strings from binaries.

### Practical Exercises

Executed:

FLOSS.exe .\windows.exe > windows.txt

### Purpose

- Extract static strings
- Identify hidden indicators
- Reveal embedded APIs
- Discover potential URLs, file paths, registry keys, and configuration data

### Findings

Extracted strings aligned with APIs identified during PEStudio analysis, validating static analysis results.

---

# Malware Investigation Exercise

## Static Analysis

### Target

windows.exe

### Analysis Performed

- Opened in PEStudio
- Reviewed hashes on VirusTotal
- Examined metadata
- Investigated imported APIs
- Checked entropy values
- Reviewed manifest configuration

### Key Findings

- Suspicious metadata
- Potential obfuscation
- Cryptographic functionality present
- Capability to spawn additional processes

---

## Dynamic Analysis

### Target

cobaltstrike.exe

### Process Explorer Investigation

Identified:

- Parent process relationship
- Active process information
- Network connections
- Destination IP and ports

### Process Monitor Investigation

Applied filters to isolate:

cobaltstrike.exe

Observed:

- Network activity
- Connection attempts
- Destination communications

### Validation

Confirmed outbound connection activity to:

47.120.46.210

Demonstrated how multiple tools can be used to validate investigative findings rather than relying on a single source of evidence.

---

# Skills Demonstrated

- Static malware analysis
- Dynamic malware analysis
- PE file inspection
- Hash verification
- Process analysis
- Parent-child process investigation
- Network traffic analysis
- API analysis
- String extraction
- Hex analysis
- Tool validation and cross-referencing
- Malware triage workflow
- Initial incident response investigation techniques
