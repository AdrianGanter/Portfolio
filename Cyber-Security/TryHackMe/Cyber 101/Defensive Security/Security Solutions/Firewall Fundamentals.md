# Firewall Fundamentals

## Overview
A firewall is a security control that monitors and filters incoming and outgoing network traffic based on defined rules. Its primary purpose is to prevent unauthorized access while allowing legitimate communications.

---

## Firewall Types

### Stateless Firewall
- Operates at OSI Layers 3 and 4
- Filters packets against predefined rules
- Does not track connection state
- Fast and efficient but less context-aware

### Stateful Firewall
- Operates at OSI Layers 3 and 4
- Maintains a state table of active connections
- Makes decisions based on connection history
- More secure than stateless filtering

### Proxy Firewall
- Operates at OSI Layer 7
- Acts as an intermediary between users and external services
- Inspects packet contents and application traffic
- Provides content filtering and hides internal IP addresses

### Next-Generation Firewall (NGFW)
- Operates across OSI Layers 3–7
- Performs deep packet inspection (DPI)
- Includes Intrusion Prevention System (IPS) capabilities
- Supports SSL/TLS inspection and threat intelligence integration
- Detects suspicious behaviour through heuristic analysis

---

## Firewall Rules

Firewall rules are used to control network traffic based on specific criteria.

### Core Rule Components
- **Source Address** – Originating IP address
- **Destination Address** – Target IP address
- **Port** – Service port being used
- **Protocol** – TCP, UDP, etc.
- **Action** – Allow, Deny, or Forward
- **Direction** – Inbound or Outbound

### Rule Actions

#### Allow
Permits matching traffic.

#### Deny
Blocks matching traffic.

#### Forward
Redirects traffic to another host or network segment.

### Rule Direction

#### Inbound Rules
- Apply to incoming traffic
- Example: Allow HTTP traffic to a web server

#### Outbound Rules
- Apply to outgoing traffic
- Example: Block outbound SMTP traffic from endpoints

#### Forward Rules
- Redirect traffic to another destination
- Commonly used for web servers and internal services

---

## Windows Defender Firewall

### Key Features
- Built-in Windows firewall solution
- Supports inbound and outbound filtering
- Allows creation of custom firewall rules
- Supports different profiles for trusted and untrusted networks

### Network Profiles

#### Private
- Used for trusted environments such as home networks

#### Public
- Used for untrusted networks such as cafés, airports, and public Wi-Fi

### Practical Exercise

Investigated existing Windows Defender Firewall rules and identified:

| Finding | Result |
|----------|----------|
| Rule blocking inbound SSH traffic | Core Op |
| Rule allowing SSH from a specific IP | Infra Team |
| Allowed IP Address | 192.168.13.7 |

<img width="1895" height="1006" alt="image" src="https://github.com/user-attachments/assets/e36460d5-e6d1-4d7d-b35b-632db9ddf908" />

### Custom Rule Demonstration
Created an outbound firewall rule to block:
- TCP Port 80 (HTTP)
- TCP Port 443 (HTTPS)

Result:
- Web browsing traffic was successfully blocked, confirming rule functionality.

---

## Linux Firewalls

### Netfilter
Core Linux firewall framework responsible for:
- Packet filtering
- Network Address Translation (NAT)
- Connection tracking

### Common Firewall Utilities

| Utility | Purpose |
|----------|----------|
| iptables | Traditional Linux firewall management |
| nftables | Modern replacement for iptables |
| firewalld | Zone-based firewall management |
| ufw | Simplified firewall management interface |

---

## UFW (Uncomplicated Firewall)

### Check Firewall Status
```bash
sudo ufw status
```

### Enable Firewall
```bash
sudo ufw enable
```

### Allow All Outbound Traffic
```bash
sudo ufw default allow outgoing
```

### Deny Incoming SSH Connections
```bash
sudo ufw deny 22/tcp
```

### Display Active Rules
```bash
sudo ufw status numbered
```

### Delete a Rule
```bash
sudo ufw delete <rule_number>
```

### Deny All Outbound Traffic by Default
```bash
ufw default deny outgoing
```

---

## Key Takeaways
- Firewalls inspect and control network traffic using predefined rules.
- Stateless firewalls evaluate packets independently, while stateful firewalls track connection history.
- Proxy firewalls inspect application-layer traffic and provide content filtering.
- NGFWs provide advanced security features including IPS, deep packet inspection, and behavioural analysis.
- Windows Defender Firewall supports profile-based filtering and custom rule creation.
- Linux firewall management is built on the Netfilter framework.
- nftables is the successor to iptables.
- UFW provides a simplified interface for managing Linux firewall rules.
