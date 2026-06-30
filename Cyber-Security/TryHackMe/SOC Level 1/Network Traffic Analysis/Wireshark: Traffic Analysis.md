# Wireshark: Traffic Analysis

## Overview

Network packet analysis focuses on identifying anomalies and extracting meaningful signals from large capture datasets. The workflow combines statistical overview, protocol dissection, and targeted filtering to isolate malicious or unusual activity.

---

## Initial Reconnaissance (Before Filtering)

Start by using Wireshark’s built-in statistics views to establish baseline behaviour:

- Protocol Hierarchy (distribution of traffic types)
- Conversations (endpoint-to-endpoint flows)
- Endpoints (hosts, MACs, IPs, ports)
- DNS statistics (query patterns, anomalies)
- HTTP statistics (methods, response codes)
- IPv4 / IPv6 breakdown

This stage is used to identify dominant hosts, unusual protocols, and traffic spikes before applying filters.

---

## Core Filtering Concepts

### Capture vs Display Filters

- Capture filters: reduce what is recorded (applied before capture)
- Display filters: analyse full dataset after capture (preferred for investigations)

---

## High-Value Filter Cheat Sheet (Low Hanging Fruit)

### Global / Broad Discovery

- `tcp`
- `udp`
- `arp`
- `dns`
- `http`
- `http2`
- `icmp`
- `kerberos`
- `nbns`
- `dhcporbootp`
- `ftp`
- `tls`

---

## TCP Scan & Recon Detection

### TCP Flag Analysis

- SYN only:
  - `tcp.flags.syn == 1`
  - `tcp.flags == 2`

- ACK only:
  - `tcp.flags.ack == 1`
  - `tcp.flags == 16`

- SYN + ACK:
  - `tcp.flags.syn == 1 and tcp.flags.ack == 1`
  - `tcp.flags == 18`

- RST:
  - `tcp.flags.reset == 1`
  - `tcp.flags == 4`

- FIN:
  - `tcp.flags.fin == 1`
  - `tcp.flags == 1`

---

### Nmap Scan Detection Patterns

- TCP Connect scan:
  - `tcp.flags.syn == 1 and tcp.flags.ack == 0 and tcp.window_size > 1024`

- SYN scan:
  - `tcp.flags.syn == 1 and tcp.flags.ack == 0 and tcp.window_size <= 1024`

- UDP scan response (closed ports):
  - `icmp.type == 3 and icmp.code == 3`

---

## ARP Analysis (MITM / Poisoning Detection)

- All ARP traffic:
  - `arp`

- Requests:
  - `arp.opcode == 1`

- Replies:
  - `arp.opcode == 2`

- Suspicious indicators:
  - Duplicate IP detection:
    - `arp.duplicate-address-detected`
  - Null MAC anomalies:
    - `arp.dst.hw_mac == 00:00:00:00:00:00`

---

## DHCP / NetBIOS / Kerberos Host Discovery

### DHCP

- All DHCP:
  - `dhcporbootp`

- Request types:
  - `dhcp.option.dhcp == 3`
- ACK:
  - `dhcp.option.dhcp == 5`
- NAK:
  - `dhcp.option.dhcp == 6`

- Hostname discovery:
  - `dhcp.option.hostname contains ""`

---

### NetBIOS

- `nbns`
- `nbns.name contains ""`

---

### Kerberos

- `kerberos`
- User extraction:
  - `kerberos.CNameString contains ""`
- Exclude machine accounts:
  - `kerberos.CNameString and !(kerberos.CNameString contains "$")`
- Domain filtering:
  - `kerberos.realm contains ""`

---

## DNS Tunnelling / Exfiltration Detection

- `dns`

- Known tunnelling patterns:
  - `dns contains "dnscat"`
  - `dns contains "dns2tcp"`

- Suspicious long queries:
  - `dns.qry.name.len > 15 and !mdns`

---

## ICMP Tunnelling Detection

- `icmp`

- Suspicious payload size:
  - `data.len > 64 and icmp`

- ICMP error-based analysis:
  - `icmp.type == 3`

---

## HTTP Analysis

### Request filtering

- `http.request`
- `http.request.method == "GET"`
- `http.request.method == "POST"`

### Response codes

- `http.response.code == 200`
- `http.response.code == 401`
- `http.response.code == 403`
- `http.response.code == 404`
- `http.response.code == 500`

### URI-based filtering

- `http.request.uri contains ""`
- `http.request.full_uri contains ""`

### User-Agent analysis

- `http.user_agent`
- Suspicious tooling:
  - `(http.user_agent contains "sqlmap") or (http.user_agent contains "Nmap") or (http.user_agent contains "Nikto") or (http.user_agent contains "Wfuzz")`

---

## FTP Cleartext Analysis

- `ftp`

### Authentication tracking

- Login success:
  - `ftp.response.code == 230`

- Failed login:
  - `ftp.response.code == 530`

### Credential capture

- Username:
  - `ftp.request.command == "USER"`

- Password:
  - `ftp.request.command == "PASS"`

- Password brute-force indicators:
  - `(ftp.response.code == 530)`

---

## HTTPS / TLS Analysis

- `tls`
- `http.request`
- TLS handshake stages:
  - Client Hello:
    - `tls.handshake.type == 1`
  - Server Hello:
    - `tls.handshake.type == 2`

- SSDP noise filtering:
  - `!ssdp`

---

## Credential Extraction (Wireshark Feature)

- Tools → Credentials viewer
- Extracts:
  - HTTP Basic Auth
  - FTP / SMTP / IMAP credentials (if present in cleartext)

---

## Firewall Rule Generation

Wireshark can generate ACL rules from packet context:

- iptables (Linux)
- Cisco IOS
- Windows Firewall
- pf / ipfw

Example outputs:
- deny source IP rules
- allow MAC address rules

---

## Practical Workflow Summary

1. Start with statistics (protocols + conversations)
2. Identify abnormal endpoints (ARP/DHCP/NetBIOS/Kerberos)
3. Detect scanning behaviour (TCP flags, SYN/ACK patterns)
4. Analyse application layer (HTTP, FTP, DNS)
5. Hunt tunnelling (ICMP/DNS anomalies)
6. Extract credentials if present
7. Correlate findings across protocols
8. Generate containment rules if required

---

## Key Takeaways

- TCP flag combinations are primary indicators of scanning behaviour.
- ARP anomalies are strong indicators of MITM activity.
- DNS and ICMP are common covert channels for tunnelling.
- HTTP and FTP are primary sources of cleartext credential exposure.
- TLS analysis requires handshake inspection rather than payload visibility.
- Effective analysis depends on layering protocol filters with behavioural patterns rather than isolated packet inspection.
