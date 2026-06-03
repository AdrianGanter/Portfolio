# CRYPTOGRAPHY BASICS

OVERVIEW
--------
Cryptography is the practice of securing information by transforming it into unreadable formats and restoring it using mathematical methods and secret keys.

CORE CONCEPTS
-------------

Plaintext
- Original readable data before encryption
- Can be text, images, files, or any binary data

Ciphertext
- Encrypted, unreadable output of plaintext
- Should not reveal meaningful information without the key

Cipher
- Algorithm used to encrypt and decrypt data
- Publicly known and mathematically defined

Key
- Secret value used by a cipher to encrypt/decrypt data
- Must remain private in symmetric systems
- In asymmetric systems, public/private key pairs are used

Encryption
- Process of converting plaintext into ciphertext using a cipher + key

Decryption
- Process of converting ciphertext back into plaintext using cipher + key

CLASSICAL ENCRYPTION EXAMPLE
----------------------------
Caesar Cipher:
- Plaintext: TRYHACKME
- Shift key: 3
- Result: WUBKDFNPH

Each letter is shifted through the alphabet (wraps after Z)

SYMMETRIC ENCRYPTION
--------------------
Same key used for encryption and decryption

Examples:
- DES   -> 56-bit key, deprecated (broken)
- 3DES  -> 168-bit key, legacy use only
- AES   -> 128/192/256-bit keys, modern standard

Key point:
- Fast and efficient
- Key distribution is the main challenge

ASYMMETRIC ENCRYPTION
---------------------
Uses a public/private key pair

Public key:
- Used to encrypt data

Private key:
- Used to decrypt data
- Must remain secret

Common algorithms:
- RSA (2048+ bit recommended minimum)
- Diffie-Hellman (key exchange)
- ECC (smaller keys, same security strength as RSA)

Key idea:
- One-way mathematical problems
- Easy to compute forward, infeasible to reverse

BASIC MATHEMATICS IN CRYPTOGRAPHY
----------------------------------

XOR Operation
- Binary operation: ⊕
- Returns 1 if bits are different, else 0

Truth table:
- 0 ⊕ 0 = 0
- 0 ⊕ 1 = 1
- 1 ⊕ 0 = 1
- 1 ⊕ 1 = 0

Modulo Operation
- Written as % or mod
- Returns remainder after division

Examples:
- 25 % 5 = 0
- 23 % 6 = 5
- 23 % 7 = 2

Key property:
- Not reversible (multiple inputs can produce same output)

RSA (SIMPLIFIED)
----------------
Core variables:
- p, q -> large prime numbers
- n = p × q
- e -> public exponent
- d -> private exponent
- m -> plaintext message
- c -> ciphertext

Key generation:
- Public key: (n, e)
- Private key: (n, d)

Encryption:
- c = m^e mod n

Decryption:
- m = c^d mod n

DIFFIE-HELLMAN KEY EXCHANGE
---------------------------
Purpose:
- Establish shared secret over insecure channel

Process:
1. Agree public values:
   - p (prime)
   - g (generator)

2. Choose private values:
   - Alice: a
   - Bob: b

3. Generate public keys:
   - A = g^a mod p
   - B = g^b mod p

4. Exchange public keys

5. Compute shared secret:
   - Alice: B^a mod p
   - Bob: A^b mod p

Result:
- Both derive same secret value

SSH (SECURE SHELL)
------------------
Purpose:
- Secure remote login using cryptographic keys

Key types:
- RSA (default)
- DSA (legacy)
- ECDSA (elliptic curve)
- Ed25519 (modern, fast, secure)
- Hardware-backed variants (SK keys)

Key generation:
- ssh-keygen -t rsa
- ssh-keygen -t ed25519

Usage:
`ssh -i private_key user@host`

Security notes:
- Private key permissions should be 600
- authorized_keys stores allowed public keys on server

DIGITAL CERTIFICATES
---------------------
Purpose:
- Verify identity of websites and servers (e.g. HTTPS)

Concept:
- Chain of trust
  Root CA → Intermediate CA → Certificate → Website

Browsers:
- Trust pre-installed root certificate authorities

Example use:
- HTTPS validation for secure web communication

PGP / GPG
---------
Purpose:
- Encrypt files and messages
- Provide digital signatures

Tools:
- PGP (standard)
- GPG (open-source implementation: GNU Privacy Guard)

Key generation:
- gpg --full-gen-key

Common commands:
- gpg --import backup.key
- gpg --decrypt file.gpg

Use cases:
- Email encryption
- File encryption
- Message signing

Security notes:
- Private keys can be passphrase-protected
- Tools like John the Ripper can attempt cracking weak passphrases
