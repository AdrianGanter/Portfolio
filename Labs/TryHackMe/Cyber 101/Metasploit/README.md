# Metasploit Learning Overview (TryHackMe)

A structured summary of the four Metasploit modules completed on TryHackMe, covering foundational concepts, exploitation workflows, post‑exploitation, and a real‑world vulnerability (MS17‑010).

---

## 01 — Basics

### Overview
Exploring the foundational components of the Metasploit Framework.

### Key Concepts Learned
- Understanding module types (auxiliary, exploit, post, payloads)
- Navigating modules using `search`, `use`, `info`
- Setting required options such as `RHOSTS`, `RPORT`, and payloads
- Executing modules correctly and validating results

### Outcome
Developed confidence in navigating Metasploit, configuring modules, and running basic exploitation workflows.

---

## 02 — Exploitation

### Overview
Diving deeper into scanning, exploitation, databases, and payload delivery.

### Hands‑On Skills
- Using Metasploit’s built‑in scanners and auxiliary modules
- Running exploitation workflows in `msfconsole`
- Successfully exploiting a target machine and obtaining a Meterpreter session
- Performing `hashdump` and retrieving user credentials
- Creating a payload, transferring it to a target, executing it, and capturing multiple password hashes

### Outcome
Demonstrated a full exploitation chain from recon → exploit → post‑exploitation → credential extraction.

---

## 03 — Meterpreter

### Overview
An in‑depth look at Meterpreter and its post‑exploitation capabilities.

### Hands‑On Actions
- Exploited a VM and established a Meterpreter session
- Gathered system information and enumerated shares
- Backgrounded the session and used `enum_shares`
- Identified a process ID and migrated to a stable process
- Performed `hashdump` and cracked NTLM hashes to plaintext
- Used `search` to locate sensitive files and extract their contents

### Outcome
Gained strong familiarity with Meterpreter commands, privilege escalation, and post‑exploitation techniques.

---

## 04 — Blue (MS17‑010 / EternalBlue)

### Overview
Using the EternalBlue exploit to gain access to a vulnerable Windows machine.

### What Was Completed
- Conducted recon and vulnerability scanning
- Exploited MS17‑010 to gain system‑level access
- Upgraded shell to Meterpreter and migrated to an authority‑level process
- Performed `hashdump` and cracked credentials
- Navigated the system to locate and extract three different flags

### Outcome
Successfully executed a real‑world exploit chain and demonstrated post‑exploitation skills on a Windows target.

---

