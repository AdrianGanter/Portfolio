# IDS Fundamentals

## Overview

An **Intrusion Detection System (IDS)** monitors network or host activity for signs of malicious behaviour and generates alerts when suspicious activity is detected.

### IDS vs Firewall

| Firewall | IDS |
|-----------|-----------|
| Prevents or blocks unwanted traffic | Detects suspicious or malicious activity |
| Acts as a gatekeeper at the network boundary | Monitors activity inside the network |
| Can deny connections | Generates alerts only |
| Preventive control | Detective control |

**Key Point:** An IDS does **not** stop an attack; it identifies and alerts on potential threats.

---

# Types of IDS

## Deployment Modes

### Host Intrusion Detection System (HIDS)

- Installed on individual endpoints or servers
- Monitors activity on a specific host
- Provides detailed host-level visibility
- Can be resource-intensive in large environments

### Network Intrusion Detection System (NIDS)

- Monitors traffic across the network
- Detects suspicious activity affecting multiple hosts
- Provides centralized visibility
- Commonly deployed at strategic network locations

---

## Detection Methods

### Signature-Based IDS

- Detects threats using known attack signatures
- Fast and efficient for known threats
- Relies on an up-to-date rule database
- Cannot detect unknown or zero-day attacks

### Anomaly-Based IDS

- Learns normal network behaviour (baseline)
- Detects deviations from expected behaviour
- Can identify unknown or zero-day attacks
- May generate higher false positives

### Hybrid IDS

- Combines signature-based and anomaly-based detection
- Detects both known and unknown threats
- Provides broader detection coverage

---

# Snort IDS

## Overview

**Snort** is a widely used open-source IDS that supports:

- Signature-based detection
- Anomaly-based detection
- Custom rule creation
- Real-time traffic monitoring
- PCAP analysis

Snort allows security teams to use built-in detection rules or create custom rules tailored to their environment.

---

# Snort Operating Modes

## Packet Sniffer Mode

- Captures and displays network packets
- No intrusion detection performed
- Useful for troubleshooting and traffic analysis

## Packet Logging Mode

- Captures and stores traffic in PCAP format
- Useful for forensic investigations
- Enables later analysis of network activity

## NIDS Mode

- Primary IDS functionality
- Monitors traffic in real time
- Applies rules to identify malicious activity
- Generates alerts when rules are triggered

---

# Snort File Structure

### Main Directory

```bash
/etc/snort
```

Important files:

| File | Purpose |
|--------|---------|
| snort.lua | Main configuration file |
| rules/ | Contains detection rules |
| local.rules | Custom rule file |
| *.pcap | Packet capture files for analysis |

---

# Snort Rule Structure

Example rule:

```bash
alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)
```

## Rule Components

<img width="1140" height="279" alt="image" src="https://github.com/user-attachments/assets/af9cf187-0259-4d6d-adac-e3e906d6d823" />

| Component | Description |
|------------|------------|
| alert | Action to perform |
| icmp | Protocol to monitor |
| any any | Source IP and port |
| -> | Traffic direction |
| 127.0.0.1 any | Destination IP and port |
| msg | Alert message |
| sid | Unique Signature ID |
| rev | Rule revision number |

---

# Practical Exercise 1 - Creating a Custom Rule

### Objective

Create a custom Snort rule to detect ICMP traffic directed at the loopback address.

### Rule Added

```bash
alert icmp any any -> 127.0.0.1 any (msg:"Loopback Ping Detected"; sid:10003; rev:1;)
```

### Edited Rule File

```bash
sudo nano /etc/snort/rules/local.rules
```

### Started Snort

```bash
sudo snort -q -l /var/log/snort -i lo -A alert_fast -c /etc/snort/snort.lua
```

### Generated Test Traffic

```bash
ping 127.0.0.1
```

### Result

- Snort successfully detected ICMP traffic.
- Generated alert:
  - **"Loopback Ping Detected"**
- Verified the custom rule was functioning correctly.

---

# Practical Exercise 2 - PCAP Analysis

### Objective

Investigate historical network traffic using Snort and a supplied PCAP file.

### Command Used

```bash
sudo snort -q -l /var/log/snort -r Intro_to_IDS.pcap -A alert_fast -c /etc/snort/snort.lua
```

### Findings

#### SSH Connection Attempt

- Source IP:
  
```text
10.11.90.211
```

- Detected by Snort using an SSH detection rule.

#### Additional Detection

```text
Ping Detected
```

#### SSH Detection Rule SID

```text
1000002
```
<img width="1910" height="967" alt="image" src="https://github.com/user-attachments/assets/3d3d6c2d-dc38-4f04-ba8a-61ddf2ca0ff1" />

---

# Key Takeaways

- IDS solutions detect malicious activity but do not prevent attacks.
- HIDS monitors individual hosts, while NIDS monitors network traffic.
- Signature-based IDS detects known threats; anomaly-based IDS identifies unusual behaviour.
- Snort is a powerful open-source IDS capable of real-time monitoring and forensic analysis.
- Custom Snort rules can be created to detect specific network activity.
- Snort can analyse both live traffic and historical PCAP files.
- Practical experience included:
  - Creating and testing a custom ICMP detection rule.
  - Running Snort in NIDS mode.
  - Analysing a PCAP file for forensic investigation.
  - Identifying SSH activity and validating Snort alerts.
