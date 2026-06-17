# Security Principles

## Overview

Studied foundational information security concepts including the CIA Triad, security models, defence-in-depth strategies, secure design principles, trust models, and risk management fundamentals.

---

## CIA Triad

The CIA Triad forms the foundation of information security:

### Confidentiality

Ensures information is only accessible to authorized individuals.

### Integrity

Ensures data remains accurate and protected from unauthorized modification.

### Availability

Ensures systems and services remain accessible when required.

### Additional Concepts

* **Authenticity** – Verifies that information originates from a legitimate source.
* **Non-Repudiation** – Prevents individuals from denying actions they performed.

---

## DAD Triad

Represents attacks against the CIA Triad:

| Security Objective | Opposing Threat      |
| ------------------ | -------------------- |
| Confidentiality    | Disclosure           |
| Integrity          | Alteration           |
| Availability       | Destruction / Denial |

---

## Security Models

### Bell-LaPadula

Confidentiality-focused model:

* No Read Up
* No Write Down

### Biba

Integrity-focused model:

* No Read Down
* No Write Up

### Clark-Wilson

Protects integrity through controlled data handling, validation, and approved transformation procedures.

---

## Defence in Depth

Implements multiple layers of security controls rather than relying on a single protective measure.

Examples include:

* Physical security
* Access controls
* Network segmentation
* Monitoring and logging
* Endpoint protection

---

## Secure Design Principles

Key principles covered:

* Least Privilege
* Attack Surface Minimisation
* Layering
* Redundancy
* Encapsulation
* Secure Error Handling
* Centralized Security Controls

---

## Trust Models

### Trust but Verify

Trust entities while continuously validating behaviour through monitoring, auditing, and logging.

### Zero Trust

Assumes no user, device, or system should be trusted by default. Access must be continuously verified through authentication and authorization controls.

---

## Risk Management Fundamentals

### Vulnerability

A weakness that could be exploited.

### Threat

A potential danger capable of exploiting a vulnerability.

### Risk

The likelihood and impact of a threat exploiting a vulnerability.

---

## Key Takeaways

* Understand the CIA Triad and core security objectives.
* Recognize common attacks against confidentiality, integrity, and availability.
* Understand how Bell-LaPadula, Biba, and Clark-Wilson support security objectives.
* Apply Defence in Depth and Least Privilege concepts.
* Understand Zero Trust principles and continuous verification.
* Differentiate between vulnerabilities, threats, and risks when assessing security posture.
