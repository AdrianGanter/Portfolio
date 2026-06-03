# JOHN THE RIPPER

OVERVIEW
--------
John the Ripper is a password cracking tool used to recover plaintext passwords from hashes using wordlists, rules, and multiple cracking modes.

BASIC EXECUTION
---------------
`john [options] [file]`

- `john` -> launches the tool
- `options` -> define cracking behaviour
- `file` -> file containing hashes

WORDLIST MODE
-------------
`john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`

- `--wordlist` -> uses dictionary attack
- wordlist file -> list of possible passwords
- hash file -> target hashes

IDENTIFYING HASH TYPES
----------------------
Tools:
- https://hashes.com/en/tools/hash_identifier
- `hash-id.py` (hash identifier script)

Run:
`python3 hash-id.py`

FORMAT-SPECIFIC CRACKING
------------------------
`john --format=<format> --wordlist=<wordlist> <file>`

Example:
`john --format=raw-sha256 --wordlist=rockyou.txt hashes.txt`

Important:
- Some formats require `raw-` prefix
- Use `john --list=formats | grep -i <type>` to verify format name

WINDOWS HASHES (NTLM / NTHASH)
------------------------------
- NTLM used in modern Windows systems
- Stored in SAM database
- Derived from MD4

Sources:
- SAM database
- NTDS.dit (Active Directory)
- tools like Mimikatz

Note:
- “Pass-the-hash” attacks may bypass cracking entirely

CRACKING /etc/shadow FILES
--------------------------
Step 1: Combine passwd + shadow
`unshadow passwd.txt shadow.txt > combined.txt`

Step 2: Crack hash
`john --wordlist=/usr/share/wordlists/rockyou.txt combined.txt`

Optional format:
`john --format=sha512crypt combined.txt`

UNSHADOW TOOL
-------------
Used to merge Linux authentication files:

`unshadow /etc/passwd /etc/shadow > output.txt`

SINGLE CRACK MODE
-----------------
Purpose:
- Uses username-based word mangling

Run:
`john --single --format=<format> hashes.txt`

Example input format:
`mike:1efee03cdcb96d90ad48ccc7b8666033`

Word mangling examples:
- Markus1
- MARKus
- Markus!

Uses:
- Username
- GECOS field (full name, phone, etc.)

GECOS FIELD
-----------
- Stored in /etc/passwd (5th field)
- Contains user metadata
- John uses this for wordlist generation

CUSTOM RULES
-------------
Defined in:
- `/etc/john/john.conf` or `/opt/john/john.conf`

Rule structure:
`[List.Rules:RuleName]`

Common modifiers:
- `Az` -> append characters
- `A0` -> prepend characters
- `c`  -> capitalize letters

Character sets:
- `[0-9]` -> numbers
- `[A-Z]` -> uppercase letters
- `[a-z]` -> lowercase letters
- `[A-z]` -> mixed case
- `[!£$%@]` -> symbols

Example rule:
`[List.Rules:PoloPassword]`
`cAz"[0-9][!£$%@]"`

ARCHIVE CRACKING
----------------

ZIP FILES
---------
Convert:
`zip2john file.zip > zip_hash.txt`

Crack:
`john zip_hash.txt`

RAR FILES
---------
Convert:
`rar2john file.rar > rar_hash.txt`

Crack:
`john rar_hash.txt`

SSH PRIVATE KEYS
----------------
Convert:
`ssh2john id_rsa > id_rsa_hash.txt`

Alternative:
`python3 /opt/john/ssh2john.py id_rsa > id_rsa_hash.txt`

Crack:
`john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt`

VIEW CRACKED PASSWORDS
----------------------
`cat ~/.john/john.pot`

or:
`cat /home/user/src/john/run/john.pot`

SUMMARY OF WORKFLOW
-------------------
1. Identify hash type
2. Convert file if needed (zip2john, ssh2john, unshadow)
3. Choose mode (wordlist, single, rules)
4. Run John
5. Check results in john.pot

KEY MODES
---------
- `--wordlist` -> dictionary attack
- `--single` -> username-based attack
- `--format` -> specify hash type

CONCLUSION
----------
John the Ripper is a flexible password cracking framework supporting multiple formats, attack modes, and preprocessing tools for real-world hash extraction scenarios.
