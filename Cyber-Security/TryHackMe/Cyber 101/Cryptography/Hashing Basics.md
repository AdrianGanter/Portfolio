# HASHING BASICS

OVERVIEW
--------
A hash function takes input data of any size and produces a fixed-size output called a digest.

Key properties:
- Deterministic: same input → same output
- One-way: infeasible to reverse
- Fast to compute
- Highly sensitive: small input change → completely different hash

COMMON ENCODINGS (NOT HASHING)
------------------------------
- Hexadecimal (used by most hash outputs like SHA/MD5 tools)
- Base64 (encoding, not security)

Examples:
- `md5sum`
- `sha1sum`
- `sha256sum`
- `sha512sum`

Note:
- Hash outputs are often displayed in hexadecimal (2 characters per byte)

PASSWORD STORAGE CONCEPT
------------------------
- Servers do NOT store plaintext passwords
- They store password hashes instead
- Login verification:
  - Input password → hash it → compare with stored hash

HASH COLLISIONS
---------------
A hash collision occurs when two different inputs produce the same hash output.

Why it happens:
- Infinite possible inputs
- Finite output space (pigeonhole principle)

Goal of secure hashing:
- Make collisions extremely unlikely and hard to engineer

PASSWORD HASH PREFIXES (LINUX / UNIX)
--------------------------------------
- `$y$`        -> yescrypt (modern default, recommended)
- `$gy$`       -> gost-yescrypt
- `$7$`        -> scrypt
- `$2a$/$2b$/$2y$/$2x$` -> bcrypt
- `$6$`        -> sha512crypt
- `$1$`        -> md5crypt
- `$md5`       -> SunMD5

Example `/etc/shadow` format:
- username:`$algorithm$salt$hash`:metadata

Example breakdown:
`$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4`

- `y`     -> yescrypt algorithm
- `j9T`   -> parameters
- salt   -> random value used in hashing
- hash    -> resulting digest

WINDOWS PASSWORD HASHING
------------------------
- Uses NTLM (based on MD4)
- Stored in SAM database

Hash types:
- NT hash
- LM hash (legacy, weak, often disabled)

Note:
- NTLM hashes resemble MD4/MD5 outputs, so context is required for identification

CRACKING HASHES
----------------
Common tools:
- `hashcat`
- `john`

Hashcat syntax:
`hashcat -m <hash_type> -a <attack_mode> hashfile wordlist`

Parameters:
- `-m` -> hash type ID (e.g., 1000 = NTLM)
- `-a` -> attack mode
- hashfile -> file containing hash
- wordlist -> password list (e.g., rockyou.txt)

Attack modes:
- `0` -> Straight (dictionary attack)
- `1` -> Combination
- `3` -> Brute force
- `6` -> Hybrid (wordlist + mask)
- `7` -> Hybrid (mask + wordlist)

Example:
`hashcat -m 3200 -a 0 hash.txt rockyou.txt`

Show cracked results:
`hashcat --show -m 3200 hash.txt`

Example workflow:
`hashcat -m 1400 -a 0 hash1.txt rockyou.txt`
`hashcat --show -m 1400 hash1.txt`

INTEGRITY CHECKING
------------------
Hashing ensures file integrity:
- Same file → same hash
- Even 1-bit change → completely different hash

Use case:
- Verify downloads
- Detect tampering
- Validate system integrity

HMAC (KEYED HASH MESSAGE AUTHENTICATION CODE)
---------------------------------------------
HMAC combines:
- Hash function
- Secret key

Purpose:
- Ensure data integrity + authenticity

Process overview:
1. Pad key
2. XOR with constant (ipad)
3. Hash message with result
4. XOR key with second constant (opad)
5. Hash again → final HMAC

Formula (conceptual):
`HMAC(K, M) = H((K ⊕ opad) || H((K ⊕ ipad) || M))`

ENCODING VS HASHING VS ENCRYPTION
----------------------------------

Hashing:
- One-way
- Not reversible
- Used for integrity & password storage

Encoding:
- Reversible transformation
- No security purpose
- Examples: Base64, ASCII, UTF-8

Encryption:
- Two-way (with key)
- Provides confidentiality
- Requires cipher + key

Base64 example:
- Encode: `TryHackMe → VHJ5SGFja01lCg==`
- Decode restores original text
