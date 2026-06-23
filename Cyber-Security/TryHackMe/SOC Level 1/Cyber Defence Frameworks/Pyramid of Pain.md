# Pyramid of Pain – Summary & Key Takeaways

## Overview

The Pyramid of Pain is a threat hunting and detection framework that ranks Indicators of Compromise (IOCs) based on how difficult they are for an attacker to change. The higher up the pyramid defenders can detect and respond, the more disruption and "pain" is caused to the adversary.

A key takeaway is that while basic indicators such as hashes and IP addresses are useful, they are relatively easy for attackers to replace. More mature security operations focus on identifying attacker behaviour, tools, and techniques rather than relying solely on simple indicators.

---

## Pyramid Levels

### 1. Hash Values (Trivial)

Hashes are unique identifiers generated from files using algorithms such as MD5, SHA-1, and SHA-256.

**What I learned:**

* Security teams use hashes to identify known malicious files.
* Platforms such as VirusTotal can be used to investigate file hashes.
* Even a minor change to a file creates a completely different hash value.
* Because hashes are easy for attackers to modify, they sit at the bottom of the pyramid.

---

### 2. IP Addresses (Easy)

IP addresses identify systems communicating across a network.

**What I learned:**

* Malicious IPs can be blocked through firewalls and security controls.
* IP addresses can help identify attacker infrastructure and command-and-control activity.
* Attackers can easily rotate IP addresses or use techniques such as Fast Flux to avoid detection.
* IP blocking is useful but often only a temporary solution.

---

### 3. Domain Names (Simple)

Attackers frequently use domains for phishing campaigns, malware delivery, and command-and-control communication.

**What I learned:**

* Domains are slightly more difficult for attackers to replace than IP addresses.
* DNS logs, proxy logs, and web logs can help identify malicious domains.
* Attackers may use techniques such as:

  * Punycode attacks to impersonate legitimate websites.
  * URL shortening services to disguise malicious destinations.
* Monitoring suspicious domain activity can improve detection capabilities.

---

### 4. Host Artifacts (Annoying)

Host artifacts are traces left behind on systems during malicious activity.

**Examples:**

* Registry modifications
* Suspicious processes
* Dropped files
* Persistence mechanisms

**What I learned:**

* Host artifacts provide valuable evidence of attacker activity.
* Detecting these indicators forces attackers to alter their tools or techniques.
* Endpoint monitoring and EDR solutions are commonly used to identify host-based indicators.

---

### 5. Network Artifacts (Annoying)

Network artifacts are observable behaviours within network traffic.

**Examples:**

* User-Agent strings
* HTTP requests
* DNS requests
* Command-and-control traffic patterns

**What I learned:**

* Network traffic can reveal attacker behaviours even when malware changes.
* Packet captures (PCAPs), IDS alerts, and network monitoring tools can be used to identify these indicators.
* Detecting network artifacts can significantly disrupt attacker operations.

---

### 6. Tools (Challenging)

Tools are the malware, frameworks, payloads, and utilities attackers use to conduct operations.

**What I learned:**

* Detecting attacker tools is much more effective than detecting individual indicators.
* Security teams can use:

  * YARA rules
  * Antivirus signatures
  * Threat intelligence feeds
  * Fuzzy hashing (SSDeep)
* Fuzzy hashing allows analysts to identify similar malware variants even when traditional hashes differ.

---

### 7. TTPs – Tactics, Techniques & Procedures (Tough)

TTPs represent the behaviours and methodologies attackers use throughout an intrusion.

**Examples:**

* Phishing
* Credential theft
* Lateral movement
* Persistence
* Data exfiltration

**What I learned:**

* TTPs align closely with the MITRE ATT&CK framework.
* Detecting TTPs is the most effective defensive approach because attackers cannot easily change how they operate.
* Successful detection at this level often forces attackers to redesign their entire attack chain or abandon the target.

---

## Key Takeaways

* The Pyramid of Pain demonstrates that not all indicators provide equal defensive value.
* Hashes, IPs, and domains are useful starting points but are relatively easy for attackers to replace.
* Host artifacts, network artifacts, tools, and TTPs provide stronger detection opportunities.
* The most effective SOC detections focus on attacker behaviour rather than individual indicators.
* Understanding where a detection sits within the Pyramid of Pain helps prioritise detection engineering and threat hunting efforts.
