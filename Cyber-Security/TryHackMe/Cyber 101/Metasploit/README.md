# Metasploit Learning Overview (TryHackMe)

A consolidated README summarizing four Metasploit learning sections completed on TryHackMe: **Basics**, **Exploitation**, **Meterpreter**, and **Blue (MS17‑010 / EternalBlue)**. Each section below maps the core topics, hands‑on activities, key commands, and outcomes so the README aligns with the detailed notes and walkthroughs in the repository.

---

## 01 — Basics

### Overview
Foundational concepts and workflows for using the Metasploit Framework and its console (`msfconsole`).

### What this section covers
- Metasploit purpose and capabilities (scanning, exploiting, payload delivery, post‑exploitation).  
- Main components: **msfconsole**, **modules**, and **tools** (examples: `msfvenom`, `pattern_create`, `pattern_offset`).  
- Module types and payload structure (Auxiliary, Encoders, Evasion, Exploits, NOPs, Payloads; payload directories: Adapters, Singles, Stagers, Stages).  
- Common workflow: recon → identify vulnerability → select exploit → configure payload → launch → interact.

### Key skills & commands (text only)
- Module navigation: `search`, `use`, `info`, `show options`, `show payloads`.  
- Parameter management: `set`, `unset`, `setg`, `unsetg`.  
- Module execution: `exploit`, `run`, `exploit -z`, `check`.  
- Session basics: `sessions`, `sessions -i <ID>`, `background`, `CTRL+Z`.

### Outcome
Built confidence in navigating Metasploit, understanding module/payload structure, and running basic exploitation workflows.

---

## 02 — Exploitation

### Overview
Applying scanning and exploitation techniques, using the Metasploit database, and delivering payloads.

### What this section covers
- Scanning approaches inside and outside Metasploit (auxiliary scanners, `db_nmap`, and running Nmap from msfconsole).  
- UDP and SMB discovery modules (e.g., UDP sweep, `smb_enumshares`, `smb_version`).  
- Using the Metasploit database and workspaces to store scan results (`msfdb init`, `db_status`, `workspace`, `db_nmap`, `hosts`, `services`).  
- Creating and delivering payloads with `msfvenom` and handling format/encoder choices.

### Hands‑on activities & examples (text only)
- Port and UDP scanning with auxiliary modules; enumerated services and discovered web server versions.  
- Used SMB login scanner with a wordlist to recover credentials.  
- Saved Nmap results to the database and queried hosts/services.  
- Built payloads (ELF, PHP, etc.) with `msfvenom` and served them via a simple HTTP server for delivery.

### Outcome
Demonstrated a full exploitation chain: recon → vulnerability identification → exploit selection → payload creation/delivery → post‑exploitation credential extraction.

---

## 03 — Meterpreter

### Overview
In‑depth exploration of Meterpreter as a post‑exploitation agent and the common commands used during engagements.

### What this section covers
- Meterpreter fundamentals: in‑memory agent, platform variants (Windows, Linux, PHP, Python, Android, macOS, etc.), and choosing the correct payload variant.  
- Core Meterpreter commands for session management, filesystem access, networking, system interaction, and post‑exploitation (examples: `getuid`, `getpid`, `migrate`, `hashdump`, `search`, `shell`, `keyscan_*`, `screenshot`, `webcam_*`, `getsystem`).  
- Practical use: migrating to stable/privileged processes, dumping SAM hashes, searching for sensitive files, and extracting flags.

### Hands‑on actions (text only)
- Established Meterpreter sessions and enumerated system info and shares.  
- Backgrounded sessions and used post modules (e.g., `post/windows/gather/enum_shares`).  
- Migrated to privileged processes (e.g., `lsass.exe`) to run `hashdump` and crack NTLM hashes.  
- Located and read sensitive files (e.g., `secrets.txt`, `realsecret.txt`) and captured flags.

### Outcome
Gained practical experience with Meterpreter workflows, privilege escalation techniques, and post‑exploitation data collection.

---

## 04 — Blue (MS17‑010 / EternalBlue)

### Overview
A focused, real‑world exploit chain using EternalBlue to gain system access and perform post‑exploitation on a Windows target.

### What this section covers
- Recon and vulnerability scanning to identify MS17‑010.  
- Selecting and running the EternalBlue exploit module (`exploit/windows/smb/ms17_010_eternalblue`) and required options (notably `RHOSTS`).  
- Converting a basic shell to a Meterpreter session using the post module `post/multi/manage/shell_to_meterpreter`.  
- Migrating to SYSTEM processes, dumping hashes, cracking credentials, and locating flags in system, SAM, and user document locations.

### Walkthrough highlights (text only)
- Nmap and vulnerability script scans revealed MS17‑010.  
- Used the EternalBlue exploit module to obtain a shell, then converted to Meterpreter and migrated to a privileged process.  
- Performed `hashdump`, cracked a user password, and retrieved three flags from system root, SAM config, and an administrator’s documents folder.

### Outcome
Executed a complete exploit chain from discovery to system‑level access and data exfiltration, reinforcing real‑world post‑exploitation practices.

---

## Cross‑Sectional Learnings & Best Practices

- **Verification first:** Always run `show options` and `check` (when available) before exploiting.  
- **Use the database:** `msfdb` and `db_nmap` keep recon results organized and reproducible.  
- **Payload selection:** Choose payloads based on OS, installed components, and network constraints; expect trial and error.  
- **Session hygiene:** Migrate to stable processes, background sessions when needed, and track session IDs for post modules.  
- **Privilege escalation:** Use `getuid`, `getsystem`, and process migration to access SAM and other protected resources.  
- **Documentation:** Keep commands, IPs, session IDs, and findings documented in Markdown for clarity and reproducibility.

---
