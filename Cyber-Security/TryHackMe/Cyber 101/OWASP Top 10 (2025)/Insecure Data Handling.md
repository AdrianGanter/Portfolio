# OWASP Top 10 2025 – Insecure Data Handling

This room covers three OWASP 2025 categories focused on how applications process, trust, and protect data. It highlights how insecure handling of input, cryptography, and external data sources can lead to exploitation even when core application logic appears secure.

The practical sections demonstrate real-world exploitation techniques including injection, weak cryptography, and insecure deserialization.

---

## A04: Cryptographic Failures
Cryptographic failures occur when sensitive data is not properly protected due to weak, missing, or incorrectly implemented encryption.

**Common issues include:**
- Storing passwords without proper hashing
- Using weak or deprecated algorithms (e.g., MD5, SHA-1)
- Exposing encryption keys in code or configuration files
- Failing to encrypt data in transit or at rest
- “Rolling your own crypto” instead of using trusted libraries

**Prevention:**
- Use modern hashing algorithms (bcrypt, scrypt, Argon2)
- Use well-tested cryptographic libraries only
- Store secrets in secure vaults or environment managers
- Avoid hardcoding credentials or keys

---

## A05: Injection
Injection flaws occur when user input is improperly handled and interpreted as executable code or queries by backend systems.

**Common types include:**
- SQL Injection
- Server-Side Template Injection (SSTI)
- Command injection
- LDAP/XML injection

**Typical causes:**
- Unsanitised or unvalidated input
- String concatenation in queries or commands
- Trusting user input in system execution contexts

**Prevention:**
- Use parameterised queries / prepared statements
- Avoid shell execution with raw input
- Validate and sanitise all input
- Enforce strict type and format constraints

---

## A08: Software or Data Failures
Software or data failures occur when applications trust external software, updates, or data sources without verifying integrity or origin.

**Common issues include:**
- Unverified third-party libraries or updates
- Insecure deserialisation (e.g., pickle abuse)
- Loading untrusted scripts or configuration data
- Missing integrity checks on critical files or binaries
- Weak or missing build and deployment verification

**Prevention:**
- Verify integrity using hashes or signatures
- Enforce trusted supply chains for dependencies
- Restrict and validate deserialisation processes
- Apply strict controls to build and deployment pipelines
- Maintain provenance tracking for external components

---

## Summary
This room demonstrates how insecure data handling arises when applications fail to properly validate, protect, or verify data at every stage of processing. The core theme is trust: never assume input, code, or external dependencies are safe without explicit verification.

These weaknesses remain highly relevant in modern systems, especially with increased reliance on automation, third-party components, and dynamic data processing.
