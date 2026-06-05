# SOC Fundamentals

## Overview

A Security Operations Center (SOC) is a dedicated team responsible for continuously monitoring, detecting, investigating, and responding to security threats across an organization's networks, systems, and assets.

The primary goal of a SOC is to maintain effective **Detection** and **Response** capabilities to minimize the impact of security incidents and protect organizational data.

---

# Core Functions of a SOC

## Detection

SOC teams monitor for security threats and suspicious activity, including:

### Vulnerabilities
- Identifying weaknesses in systems, applications, or operating systems
- Supporting remediation efforts such as patch management
- Reducing the overall attack surface of the organization

### Unauthorized Activity
- Detecting suspicious logins and account misuse
- Identifying abnormal user behavior
- Investigating indicators of account compromise

### Policy Violations
- Monitoring for actions that breach company security policies
- Examples include:
  - Downloading unauthorized software
  - Sharing confidential information insecurely
  - Use of prohibited services or applications

### Intrusions
- Detecting unauthorized access to systems or networks
- Identifying compromised devices and malicious activity
- Monitoring for exploitation attempts against organizational assets

---

## Response

When a threat is detected, the SOC supports incident response activities by:

- Investigating alerts
- Determining scope and impact
- Assisting with containment
- Supporting eradication and recovery efforts
- Performing root cause analysis

---

# The Three Pillars of a SOC

A mature SOC relies on three key components working together:

## People
Skilled security professionals who investigate, validate, and respond to threats.

## Process
Established procedures that ensure alerts and incidents are handled consistently and effectively.

## Technology
Security tools that provide visibility, detection, automation, and response capabilities.

---

# SOC Roles and Responsibilities

## SOC Analyst Level 1 (L1)

The first responder to security alerts.

Responsibilities:
- Alert triage
- Initial investigation
- Severity assessment
- Escalation and reporting

## SOC Analyst Level 2 (L2)

Performs deeper investigations when additional analysis is required.

Responsibilities:
- Correlating data from multiple sources
- Investigating complex alerts
- Supporting Level 1 analysts

## SOC Analyst Level 3 (L3)

Senior analysts responsible for advanced threat detection and incident response.

Responsibilities:
- Threat hunting
- Incident response support
- Containment, eradication, and recovery activities

## Security Engineer

Responsible for deploying and maintaining security technologies.

Responsibilities:
- Tool deployment
- Configuration management
- Platform maintenance

## Detection Engineer

Creates and maintains detection logic used by security tools.

Responsibilities:
- Developing detection rules
- Improving alert quality
- Reducing false positives

## SOC Manager

Oversees SOC operations and processes.

Responsibilities:
- Team coordination
- Process management
- Reporting security posture to leadership

---

# SOC Processes

## Alert Triage

The first step after receiving an alert.

The objective is to determine:
- Severity
- Impact
- Required response actions

### The 5 Ws Framework

<img width="740" height="627" alt="image" src="https://github.com/user-attachments/assets/a475ac97-d590-4b10-b71c-519c9b130e99" />

SOC analysts use the 5 Ws to investigate alerts:

| Question | Purpose |
|-----------|-----------|
| What? | What activity occurred? |
| When? | When did it happen? |
| Where? | Which system or location was involved? |
| Who? | Which user or device initiated the activity? |
| Why? | What caused the activity? Was it legitimate or malicious? |

---

## Reporting

After triage, analysts create reports or tickets containing:

- Investigation findings
- The 5 Ws
- Supporting evidence
- Recommended actions

These reports allow higher-level analysts and response teams to act quickly.

---

## Incident Response & Forensics

For critical incidents, additional activities may include:

- Containment of affected systems
- Removal of malicious activity
- System recovery
- Digital forensic analysis
- Root cause determination

---

# SOC Technologies

## SIEM (Security Information and Event Management)

A centralized platform that collects and analyzes logs from multiple sources.

Capabilities:
- Log aggregation
- Event correlation
- Alert generation
- Threat detection
- User behavior analytics
- Threat intelligence integration

**Primary Function:** Detection

---

## EDR (Endpoint Detection and Response)

Provides visibility into endpoint activity and supports response actions.

Capabilities:
- Real-time monitoring
- Historical endpoint visibility
- Endpoint investigations
- Automated response actions

---

## Firewall

Controls and monitors network traffic entering and leaving a network.

Capabilities:
- Traffic filtering
- Access control enforcement
- Blocking unauthorized communications
- Detection of suspicious network activity

---

# Practical Exercise: Level 1 SOC Investigation

## Scenario

Investigated a SIEM alert indicating potential port scanning activity within the network.

The vulnerability assessment team had previously informed the SOC that scanning activity would be conducted from a known internal host.

---

## Alert Investigation Using the 5 Ws

| Question | Finding |
|-----------|-----------|
| What? | Port Scan |
| When? | June 12, 2024 - 17:24 |
| Where? | Destination Host: 10.0.0.3 |
| Who? | Source Host: Nessus |
| Why? | Intended vulnerability assessment activity |

### Additional Finding

- Response traffic was observed from the destination host back to the scanning host.

### Outcome

- Alert validated as legitimate activity
- No malicious behavior identified
- Alert closed successfully

**Flag:** `THM{000_INTRO_TO_SOC}`

---

# Key Takeaways

- A SOC operates continuously to detect and respond to security threats.
- Detection and Response are the core functions of a SOC.
- Effective SOC operations rely on People, Process, and Technology.
- Alert triage is a critical responsibility of Level 1 analysts.
- The 5 Ws framework provides a structured approach to investigations.
- SIEM, EDR, and Firewalls are foundational technologies within a SOC environment.
- Proper analysis is required to distinguish legitimate activity from malicious behavior before escalating incidents.


<img width="1917" height="1035" alt="image" src="https://github.com/user-attachments/assets/aa6138c8-7241-47ed-91a5-0b6d7c04ab7d" />

