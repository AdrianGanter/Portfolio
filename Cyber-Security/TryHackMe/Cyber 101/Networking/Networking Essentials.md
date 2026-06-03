### Networking Essentials for Cyber Security – Deep Quick-Ref

#### OSI 7-Layer Security Lens
| Layer | Threat Surface | Defensive Primitives | Tools/Logs |
|---|---|---|---|
| 7 – Application | Malicious payloads, credential stuffing, API abuse | WAF, secure coding, SAST/DAST, MFA | HTTP logs, SIEM alerts |
| 6 – Presentation | Downgrade attacks (TLS-strip) | Enforce TLS 1.2+ (HSTS), cert pinning | SSL Labs grade, cert transparency |
| 5 – Session | Session hijack, fixation | Secure cookies, short TTL, SameSite=Lax | Cookie flags, session replay logs |
| 4 – Transport | Port scan, SYN flood, MITM | Segmentation, ACLs, IDS/IPS, TCP reset limits | NetFlow, Zeek conn.log |
| 3 – Network | IP spoofing, route hijack, smurf | uRPF, BGP RPKI, ICMP rate-limit | Router ACLs, BGPmon |
| 2 – Data Link | ARP spoofing, MAC flooding | Dynamic ARP Inspection, port security | switch CAM tables, ARP logs |
| 1 – Physical | Rogue AP, taps, EMI | Locked cabinets, 802.1X on switch ports | badge logs, RF spectrum analyzer |

#### Private vs. Public IPv4
- **RFC 1918 ranges** are unreachable from the Internet → NAT hides internal topology.  
- **Ingress/Egress monitoring**: log every connection that leaves or enters the NAT gateway.

#### Core Protocols – Security Notes
| Protocol | Port(s) | Security Facts | One-Liner |
|---|---|---|---|
| **ICMP** | — | Recon (ping sweep, TTL fingerprint), DoS (ping flood) | Block inbound echo but allow Time-Exceeded for PMTU. |
| **DNS** | 53/UDP+TCP | Cache poisoning, tunneling, recon (sub-domain brute) | DNSSEC + DoH/DoT, sink-hole malicious domains. |
| **HTTP** | 80 | Plain-text credentials, session cookies | Redirect 80→443, HSTS preload. |
| **HTTPS** | 443 | TLS inspection bypass, weak ciphers | Qualys SSL Labs audit, disable TLS <1.2, rotate certs. |
| **FTP** | 21 (+ 20 data) | Credentials & payload in clear text | Replace with SFTP/FTPS. |
| **SSH** | 22 | Brute-force, key misuse, tunneling | Key-only auth, fail2ban, `AllowUsers`, change port ≠ security. |
| **SMTP/SMTPS** | 25, 587/465 | Spoofing, phishing, open relay | SPF+DKIM+DMARC, STARTTLS enforcement. |
| **POP3/IMAP** | 110/143 vs 995/993 | Passwords in clear on legacy ports | Disable plaintext ports; enforce SSL/TLS. |
| **TELNET** | 23 | **Never use** – no encryption | Drop at firewall. |
| **DHCP** | 67/68 | Rogue DHCP server, IP exhaustion | DHCP snooping on switches, static leases for servers. |

#### Network Monitoring & Response
- **Port Scan Detection**: sudden SYN packets → trigger “port scan” alert in SIEM.  
- **ARP Watch**: compare CAM ↔ ARP tables; alert on mismatch.  
- **BGP Hijack**: use BGPmon or RIPE RPKI validator for route-origin validation.  
- **Packet Capture**: capture on span/tap port, filter with BPF:  
  `tcpdump -i eth0 'tcp[tcpflags] & (tcp-syn) != 0 and dst port 3389'`

#### NAT & Firewall Cheat-Sheet
- **DNAT (Port-Forward)**: maps public:port → private:port.  
- **SNAT (Masquerade)**: hides private source behind public IP.  
- **Firewall Zones**:  
  - **Green** (internal), **Orange** (DMZ), **Red** (Internet).  
  - Default deny inbound, allow related/established.

#### Incident Response One-Liners

# Find live hosts on /24
`nmap -sn 192.168.1.0/24 | grep "Nmap scan report"`

# Quick banner grab
`nc -nv 10.0.0.10 80`

# DNS tunnel check
`dig +short tunnel.evil.com`

# Check for rogue DHCP
`dhcpdump -i eth0`

# Trace path with path-MTU discovery
`traceroute -F 1500 8.8.8.8`


#### Key Take-Away
Secure networks **never trust traffic by default**: encrypt in transit, authenticate endpoints, log everything, and inspect at every layer.
