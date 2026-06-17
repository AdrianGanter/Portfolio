# OWASP Top 10 2025 – Application Design Flaws

This room explores four key categories from the OWASP Top 10 (2025) that stem from weaknesses in application design rather than individual coding bugs. It focuses on how insecure architecture, misconfigurations, weak dependencies, and flawed assumptions can lead to real-world exploitation.

The room includes practical challenges demonstrating how attackers exploit these weaknesses across exposed services and intentionally vulnerable applications.

---

## Security Misconfigurations (A02)
Security misconfigurations occur when systems are deployed with unsafe defaults, exposed services, or incorrect permissions. These issues are not caused by code flaws but by improper setup or hardening of infrastructure.

**Key risks include:**
- Exposed admin panels or APIs
- Default credentials left unchanged
- Publicly accessible storage or services
- Verbose error messages revealing system details
- Unnecessary services exposed to the internet

---

## Software Supply Chain Failures (A06)
Supply chain failures arise when applications depend on unverified or vulnerable third-party components, libraries, or services.

**Key risks include:**
- Outdated or unmaintained dependencies
- Automatic updates without verification
- Compromised or malicious third-party packages
- Insecure build or deployment pipelines
- Lack of provenance tracking for dependencies

These issues highlight how external components can compromise an otherwise secure application.

---

## Cryptographic Failures (A03)
Cryptographic failures occur when encryption is missing, misused, or implemented with weak standards, exposing sensitive data.

**Key risks include:**
- Weak or deprecated algorithms
- Hard-coded secrets in code
- Poor key management practices
- Missing encryption in transit or at rest
- Invalid or self-signed certificates

These failures often lead to data exposure, credential theft, or full account compromise.

---

## Insecure Design (A10)
Insecure design refers to architectural flaws built into the system from the start, often due to missing threat modelling or incorrect assumptions about user behaviour.

**Key risks include:**
- Weak business logic controls
- Missing abuse-case considerations
- Over-trusting system or model outputs
- Lack of authentication in design assumptions
- No validation of critical workflows

Modern systems are particularly vulnerable when automation or AI components are trusted without proper safeguards.

---

## Summary
This room demonstrates that many real-world security issues are not caused by individual coding mistakes, but by how systems are designed, configured, and connected. Strong security requires secure architecture, proper dependency management, and continuous validation of assumptions across the entire application lifecycle.
