# NetworkMiner

## Overview

NetworkMiner is an open-source **Network Forensic Analysis Tool (NFAT)** used to quickly analyse PCAP files and extract useful information without manually inspecting every packet.

It complements Wireshark by providing a fast overview of captured traffic before performing deeper packet analysis.

Typical workflow:

> Capture traffic → Analyse with NetworkMiner → Investigate further with Wireshark

---

# What NetworkMiner Can Do

- Identify hosts and operating systems
- Map network sessions
- View DNS activity
- Extract files and images
- Recover credentials and password hashes
- Recover emails and messages
- Extract HTTP parameters
- Search for keywords in cleartext
- Detect basic anomalies

---

# Useful Tabs

### Hosts

Quickly identify:

- IP & MAC addresses
- Operating systems
- Hostnames
- Open ports
- Packet counts

### Sessions

View conversations between hosts, including:

- Client & Server
- Ports
- Protocol
- Frame number

### DNS

Review DNS queries and responses to identify suspicious domains or communications.

### Credentials

Automatically extracts credentials such as:

- NTLM hashes
- Kerberos hashes
- HTTP, FTP, SMTP and IMAP credentials
- Cookies

### Files & Images

Recover transferred files, documents, executables and images directly from the PCAP.

### Parameters

Extract HTTP parameters such as usernames, IDs and search terms.

### Messages

Recover emails, chats and attachments.

### Anomalies

Highlights basic detections such as:

- EternalBlue exploitation
- Spoofing attempts

---

# Version Differences

### NetworkMiner 2.7

Best for:

- Duplicate MAC address detection
- Improved parameter extraction
- Better host correlation

### NetworkMiner 1.6

Best for:

- Frame-level analysis
- More detailed packet information
- Viewing extracted cleartext data

Both versions have strengths, so it's useful to know when each provides more insight.

---

# Practical Skills

During the exercises I practised:

- Identifying operating systems from PCAPs
- Finding hosts sharing the same MAC address
- Reviewing packet and byte counts between hosts
- Identifying web server banners
- Recovering usernames and NTLM password hashes
- Extracting transferred files and images
- Identifying email senders, recipients and subjects
- Finding DNS queries and responses
- Detecting TLS anomalies
- Locating useful artefacts without inspecting every packet manually

---

# Investigation Workflow

When opening a PCAP:

1. Hosts
2. Sessions
3. DNS
4. Credentials
5. Files
6. Messages
7. Anomalies

Then switch to **Wireshark** if detailed packet analysis is required.

---

# Key Takeaways

- NetworkMiner is excellent for quickly triaging PCAP files.
- It automatically extracts hosts, credentials, files and other useful artefacts.
- Version 2.7 focuses on better host correlation, while Version 1.6 provides more detailed packet and frame views.
- Use NetworkMiner to find the **low hanging fruit**, then use Wireshark for in-depth investigation.
