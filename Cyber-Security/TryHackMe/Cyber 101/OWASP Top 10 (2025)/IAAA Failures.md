# OWASP Top 10 (2025) - IAAA Failures

## Overview

Studied OWASP Top 10 (2025) categories related to failures in Identity, Authentication, Authorisation, and Accountability (IAAA). Explored how weaknesses in these areas can lead to unauthorized access, privilege escalation, account compromise, and reduced incident visibility.

---

## IAAA Model

### Identity

The unique account or identifier representing a user or service.

### Authentication

Verifying that a user is who they claim to be.

### Authorisation

Determining what actions or resources a user is permitted to access.

### Accountability

Recording and monitoring user activity to support auditing and investigations.

---

## A01: Broken Access Control

Broken Access Control occurs when applications fail to properly enforce permissions on user requests.

### Key Concepts

* Insecure Direct Object Reference (IDOR)
* Horizontal Privilege Escalation
* Vertical Privilege Escalation
* Server-side access validation

### Practical Exercise

* Manipulated URL parameters to access records belonging to other users.
* Identified how insecure object references can expose unauthorized data.
* Observed horizontal privilege escalation where data from other users could be viewed without obtaining additional privileges.

---

## A07: Authentication Failures

Authentication Failures occur when applications incorrectly verify user identities or improperly manage authentication mechanisms.

### Common Causes

* Username enumeration
* Weak password policies
* Missing rate limiting or account lockouts
* Session management flaws
* Registration and login logic weaknesses

### Practical Exercise

* Exploited a flaw in the registration process to impersonate a privileged account.
* Demonstrated how poor identity validation can result in unauthorized account access.

---

## A09: Logging and Monitoring Failures

Logging and Monitoring Failures reduce visibility into malicious activity and hinder incident response efforts.

### Key Concepts

* Security event logging
* Authentication monitoring
* Brute-force detection
* Audit trails
* Alert generation

### Practical Exercise

* Investigated application logs following a simulated attack.
* Identified indicators of brute-force activity.
* Traced attacker actions through authentication and application logs.
* Determined the affected account and actions performed after compromise.

---

## Key Takeaways

* Understand the relationship between Identity, Authentication, Authorisation, and Accountability.
* Recognize common Broken Access Control vulnerabilities, including IDOR.
* Understand how authentication weaknesses can lead to account compromise.
* Use logging and monitoring data to support investigations and incident response.
* Appreciate the importance of secure access controls, authentication mechanisms, and audit logging within web applications.
