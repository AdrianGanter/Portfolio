# Human & System Attack Vectors

---

# Humans as Attack Vectors

## Core Idea
Humans are often the weakest link in cyber security because they can be manipulated into giving access, running malware, or revealing sensitive information.

Attackers usually prefer targeting people over technical systems because it is faster and requires less effort.

---

## Why Humans Are Targeted
Humans provide access to:
- Email accounts
- Corporate systems
- Sensitive databases
- Internal credentials

Common attacker goals:
- Steal data (e.g. HR databases, customer records)
- Gain internal system access via compromised credentials
- Hijack sessions or escalate privileges
- Use social access as a foothold into deeper systems

---

## Social Engineering
A manipulation technique that exploits human psychology rather than technical vulnerabilities.

It relies on:
- Trust (appearing legitimate)
- Emotion (fear, urgency, curiosity)

### Common forms:
- Phishing emails (most common)
- Malware delivery via links, attachments, fake websites
- Impersonation (IT support, managers, vendors)
- Deepfake audio/video scams
- Physical attacks (USB drops, malicious QR codes, fake job offers)

---

## Key Attack Methods

### Phishing
Emails or messages designed to trick users into:
- Clicking malicious links
- Entering credentials into fake pages
- Downloading malicious files

---

### Malware Delivery
Delivered via:
- Fake software downloads
- Pirated software
- Malicious CAPTCHAs or SEO poisoning
- QR codes or attachments

---

### Impersonation
Attackers pose as:
- IT support
- Company executives
- External vendors

Goal is to trick users into:
- Resetting passwords
- Sharing sensitive data
- Approving fraudulent actions

---

### Deepfakes
AI-generated audio/video used to impersonate trusted individuals.

Used for:
- Fraudulent financial transfers
- Social engineering via video calls
- Authority spoofing

---

## SOC Role in Human-Focused Attacks

SOC analysts:
- Detect phishing campaigns and suspicious logins
- Investigate compromised accounts
- Respond to user-reported incidents
- Support awareness training and prevention efforts

---

## Mitigation Strategies

### Preventative Controls
- Email filtering / anti-phishing systems
- Antivirus / endpoint protection
- Security awareness training
- “Trust but verify” policies for sensitive requests

### Detection Controls
- Monitoring login activity
- Alerting on suspicious behaviour
- Investigating anomalies and user reports

---

## Key SOC Principle
Humans cannot be fully secured through technical controls alone — security requires a mix of:
- Technology (filters, antivirus, monitoring)
- Process (verification procedures)
- Training (awareness and simulation)

---

# Systems as Attack Vectors

## Core Idea
Systems are directly targeted when attackers exploit:
- Software vulnerabilities
- Misconfigurations
- Weak architecture or design
- Supply chain weaknesses

Unlike humans, systems can be attacked without interaction from a user.

---

## What a System Is
A system is any infrastructure that stores or processes data, such as:
- Servers (web, database, mail)
- Cloud platforms (M365, AWS, Azure)
- Workstations and laptops
- Network appliances and services

Compromising a system often impacts multiple users at once.

---

## Main System Attack Paths

### 1. Vulnerabilities
Security flaws in software that can be exploited.

Examples:
- Zero-days (unknown to vendor)
- Known CVEs awaiting patching
- Weak authentication or logic flaws

Response:
- Apply patches
- Restrict access during exposure window
- Monitor for exploitation attempts

---

### 2. Misconfigurations
Security issues caused by incorrect setup rather than code bugs.

Examples:
- Default or weak passwords
- Exposed admin panels or services
- Public cloud storage buckets
- Overly permissive access controls

Response:
- Harden configurations
- Apply least privilege
- Conduct audits and scans

---

### 3. Supply Chain Attacks
Compromise of trusted dependencies such as:
- Third-party libraries
- Software updates
- External services or APIs

Impact:
- Trusted software becomes malicious
- Large-scale downstream compromise

Response:
- Verify dependencies
- Sign and validate updates
- Monitor behaviour of third-party components

---

## Key System Threat Types

- Human-led system compromise (weak passwords, reuse, USB malware)
- Exploited software vulnerabilities
- Misconfigured infrastructure
- Compromised dependencies (supply chain attacks)

---

## SOC Role in System Security

SOC analysts:
- Detect exploitation attempts (logs, alerts, IDS/WAF)
- Investigate vulnerabilities in use
- Respond to active incidents
- Coordinate patching and containment

---

## Mitigation Strategies

### Preventative Controls
- Patch management
- Secure configuration baselines
- Network segmentation and access control
- Antivirus / endpoint protection

### Detection Controls
- SIEM monitoring
- Vulnerability scanning alerts
- Behavioural anomaly detection

---

## Key SOC Principle
System security failures are usually not random — they come from:
- Unpatched vulnerabilities
- Poor configuration
- Unsafe dependencies
- Weak operational discipline

---

## Core Takeaway
Humans and systems are not separate attack surfaces.

Attackers treat them as one combined pathway:
- Humans provide access
- Systems provide scale and impact

SOC defence requires visibility and response across both.
