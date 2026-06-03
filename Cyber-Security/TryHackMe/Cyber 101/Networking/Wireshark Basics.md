### Wireshark for Incident Response & Threat Hunting 

#### Core UI Sections
| Pane | Purpose | Pro-Tip |
|---|---|---|
| Packet List (top) | Row-per-packet summary | Colorize → `View ▸ Coloring Rules` |
| Packet Details (middle) | Dissected headers & payloads | Right-click ▸ “Apply as Column” for IOCs |
| Packet Bytes (bottom) | Raw hex/ASCII view | `Ctrl+Shift+X` → export bytes as file |

#### Expert Info Cheat-Sheet
| Severity | Color | Typical Use-Case | Example IOC |
|---|---|---|---|
| **Chat** (Blue) | Normal flow | Baseline traffic | DNS query/response |
| **Note** (Cyan) | App-level events | HTTP 404, SMTP 550 | Track phishing domains |
| **Warn** (Yellow) | Anomaly flags | TCP retransmission storm | Possible DoS |
| **Error** (Red) | Malformed | Bad checksum, illegal TCP flags | Likely injection or fuzzing |

Quick open: `Analyze ▸ Expert Information` or bottom-left status bar icon.

#### Display Filters for Common Attacks
| Attack Pattern | Filter | Notes |
|---|---|---|
| **Port Scan** | `tcp.flags.syn == 1 and tcp.flags.ack == 0` | Count distinct dst ports |
| **Brute Force** | `tcp.analysis.retransmission and tcp.dstport == 22` | Excessive SSH retries |
| **DNS Tunnel** | `dns.qry.name contains "base64"` or `dns.len > 100` | Large TXT queries |
| **ARP Spoof** | `arp.duplicate-address-detected or arp.duplicate-address-frame` | Look for gratuitous ARP storms |
| **Beaconing** | `frame.time_delta < 1 and ip.dst == C2_IP and tcp.len == 0` | Regular outbound keep-alive |
| **Clear-text Credentials** | `http.request or ftp or pop or telnet` | Follow stream (`Ctrl+Alt+Shift+T`) |
| **File Exfil** | `tcp.payload contains "filename=" or http.file_data` | Save objects (`File ▸ Export Objects`) |

#### Built-in Statistics & IO Graphs
| Menu Path | Insight | Usage |
|---|---|---|
| `Statistics ▸ Conversations` | Top talkers & throughput | Spot C2 or data-hogging host |
| `Statistics ▸ Endpoints` | MAC/IP/port counts | Identify pivot points |
| `Statistics ▸ Protocol Hierarchy` | Unexpected protocols (e.g., IRC) | Baseline drift |
| `Statistics ▸ IO Graphs` | Traffic spikes | Correlate with SIEM alerts |

Example IO Graph filter: `tcp.analysis.bytes_in_flight` to visualize window-size attacks.

#### TLS Decryption Workflow
1. Obtain server private key or SSLKEYLOGFILE from browser.  
2. `Edit ▸ Preferences ▸ Protocols ▸ TLS ▸ (a) RSA keys list` or `(b) Pre-Master-Secret log`.  
3. Re-open capture → decrypted `http2`/`http` streams appear.

#### Packet Carving & IOC Export
- Export HTTP objects: `File ▸ Export Objects ▸ HTTP`.  
- Export raw bytes: right-click field ▸ “Export Selected Packet Bytes” → malware sample.  
- Extract strings: `Tools ▸ Firewall ACL Rules` → generate blocklists.

#### Hotkeys & Productivity
| Key | Action |
|---|---|
| `Ctrl+F` | Search packet bytes/regex |
| `Ctrl+M` | Mark/unmark packet |
| `Ctrl+Alt+Shift+T` | Follow TCP stream |
| `Ctrl+Shift+P` | Apply previous display filter |
| `Ctrl+Shift+X` | Export bytes |

#### Quick Triage Checklist
1. Load capture → sort by “Time since beginning”.  
2. Check Expert Info for red/yellow flags.  
3. Run `Statistics ▸ Conversations` → sort by Bytes → inspect top flows.  
4. Apply port-scan filter → pivot to src IP.  
5. Follow stream → extract payload → hash → VT lookup.  
6. Document IOCs: IPs, domains, hashes, user-agents.

> Wireshark is not signature-based; always corroborate suspicious traffic with endpoint logs and threat-intel feeds.
