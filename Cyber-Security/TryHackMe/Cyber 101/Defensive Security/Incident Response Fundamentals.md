# Incident Response Fundamentals

## Overview

Incident Response (IR) is the structured process of detecting, investigating, containing, eradicating, and recovering from cyber security incidents while minimizing business impact.

The objective is to quickly identify threats, reduce damage, restore operations, and improve future security defenses.

---

# What is a Security Incident?

Security tools analyze system and network events for suspicious activity.

When potentially malicious activity is identified, an **alert** is generated and investigated.

- **False Positive:** Alert is triggered, but no malicious activity exists.
- **True Positive:** Alert correctly identifies malicious activity.

A validated true positive becomes a **security incident**.

---

# Incident Severity

Incidents are prioritized based on business impact and risk.

| Severity | Description |
|-----------|-----------|
| Low | Minimal impact |
| Medium | Moderate impact requiring investigation |
| High | Significant impact requiring immediate action |
| Critical | Severe impact requiring urgent response |

---

# Common Types of Security Incidents

## Malware Infection
Malicious software designed to damage systems, steal data, or provide unauthorized access.

## Security Breach
Unauthorized access to systems, accounts, or sensitive information.

## Data Leak
Exposure of confidential information through malicious activity, human error, or misconfiguration.

## Insider Attack
Malicious actions performed by trusted users with legitimate access.

## Denial of Service (DoS)
Attack intended to disrupt the availability of systems, services, or applications.

---

# SANS Incident Response Lifecycle (PICERL)

| Phase | Purpose |
|---------|---------|
| Preparation | Establish teams, tools, and procedures |
| Identification | Detect and validate incidents |
| Containment | Limit the spread and impact |
| Eradication | Remove the threat from the environment |
| Recovery | Restore affected systems and services |
| Lessons Learned | Improve future detection and response efforts |

### Example Actions

- **Containment:** Isolate an infected host from the network.
- **Eradication:** Remove malware from compromised systems.
- **Recovery:** Restore systems from backups and validate integrity.
- **Lessons Learned:** Conduct post-incident review and identify improvements.

---

# NIST Incident Response Lifecycle

The NIST framework combines several SANS phases into four stages.

| NIST Phase | Equivalent SANS Phase(s) |
|------------|--------------------------|
| Preparation | Preparation |
| Detection & Analysis | Identification |
| Containment, Eradication & Recovery | Containment, Eradication, Recovery |
| Post Incident Activity | Lessons Learned |

---

# Incident Response Plan (IRP)

An Incident Response Plan is a formal document that defines how an organization prepares for, responds to, and recovers from security incidents.

### Key Components

- Roles and responsibilities
- Incident response methodology
- Stakeholder communication procedures
- Escalation paths
- Reporting requirements

---

# Incident Response Technologies

## SIEM (Security Information and Event Management)

- Centralized log collection
- Event correlation
- Alert generation
- Threat detection

## Antivirus (AV)

- Detects known malware
- Performs scheduled scans
- Quarantines malicious files

## EDR (Endpoint Detection and Response)

- Endpoint visibility and monitoring
- Advanced threat detection
- Host isolation and response capabilities
- Threat eradication support

---

# Playbooks vs Runbooks

## Playbooks

High-level response guides for specific incident types.

Example phishing playbook:

1. Notify stakeholders
2. Analyze email content and headers
3. Investigate attachments
4. Identify affected users
5. Isolate compromised hosts
6. Block malicious sender

## Runbooks

Detailed step-by-step instructions used to perform specific response actions.

**Playbook = What to do**  
**Runbook = How to do it**

---

# Practical Exercise: Phishing Incident Response

## Scenario

Investigated a phishing campaign targeting multiple users within an organization.

The objective was to determine the scope of compromise, identify affected systems, and support incident response activities.

---

## Investigation Findings

| Item | Result |
|---------|---------|
| Malicious Sender | Jeff Johnson |
| Threat Vector | Email Attachment |
| Devices that Downloaded Attachment | 3 |
| Devices that Executed File | 1 |

---

## Actions Performed

- Investigated phishing activity
- Identified affected hosts
- Determined infection scope
- Reviewed attack timeline
- Supported containment activities

---

## Outcome

- Malicious email source identified
- Impacted systems investigated
- Scope of compromise determined
- Incident successfully contained and resolved

**Flag:** `THM{My_First_Incident_Response}`

<img width="1905" height="1035" alt="image" src="https://github.com/user-attachments/assets/aa51a848-5243-4656-859f-6c0e7b736436" />


---

# Key Takeaways

- Security incidents originate from validated true positive alerts.
- Incident severity helps prioritize response efforts.
- Common incident types include malware, breaches, data leaks, insider threats, and DoS attacks.
- The SANS PICERL model provides a structured six-phase response process.
- NIST offers a simplified four-phase incident response framework.
- SIEM, AV, and EDR solutions support detection, investigation, and response activities.
- Playbooks standardize response procedures, while runbooks provide detailed execution steps.
- Effective incident response focuses on minimizing impact, restoring operations, and improving future defenses.
