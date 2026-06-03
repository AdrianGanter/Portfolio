# Networking Essentials

---

## 1. Core Concepts
- **IP**: Logical address of a host (IPv4 32-bit, IPv6 128-bit).  
- **MAC**: 48-bit hardware address; first 24 bits = vendor OUI.  
- **ICMP**: Ping & traceroute; disable inbound echo to reduce recon.  
- **ARP**: Resolves IP → MAC; protect with **Dynamic ARP Inspection**.  
- **DHCP**: 4-step handshake (Discover → Offer → Request → ACK) that hands out IPs; prevent rogue servers with **DHCP snooping**.

---

## 2. OSI 7-Layer Security Lens
| Layer | Threat Surface | Defensive Primitives | Tools/Logs |
|---|---|---|---|
| 7 – Application | Malicious payloads, credential stuffing, API abuse | WAF, secure coding, SAST/DAST, MFA | HTTP logs, SIEM alerts |
| 6 – Presentation | Downgrade attacks (TLS-strip) | Enforce TLS 1.2+ (HSTS), cert pinning | SSL Labs grade, cert transparency |
| 5 – Session | Session hijack, fixation | Secure cookies, short TTL, SameSite=Lax | Cookie flags, session replay logs |
| 4 – Transport | Port scan, SYN flood, MITM | Segmentation, ACLs, IDS/IPS, TCP reset limits | NetFlow, Zeek conn.log |
| 3 – Network | IP spoofing, route hijack, smurf | uRPF, BGP RPKI, ICMP rate-limit | Router ACLs, BGPmon |
| 2 – Data Link | ARP spoofing, MAC flooding | Dynamic ARP Inspection, port security | switch CAM tables, ARP logs |
| 1 – Physical | Rogue AP, taps, EMI | Locked cabinets, 802.1X on switch ports | badge logs, RF spectrum analyzer |

---

## 3. TCP vs UDP
| Protocol | Characteristic | Use-Case | Security Note |
|---|---|---|---|
| **TCP** | Connection-oriented, reliable, 3-way handshake | HTTP(S), SSH, SMTP | SYN flood → SYN cookies, idle-timeout |
| **UDP** | Connectionless, fast, no flow control | DNS, VoIP, DHCP | UDP flood → rate-limit, stateless ACL |

---

## 4. Ports
| Port | Service | Security Tip |
|---|---|---|
| 21/20 | FTP | Replace with SFTP/FTPS |
| 22 | SSH | Key-only, fail2ban |
| 53 | DNS | DNSSEC + DoH/DoT |
| 80 | HTTP | Redirect to 443 + HSTS |
| 443 | HTTPS | TLS 1.2+, disable weak ciphers |
| 3389 | RDP | Restrict by IP, VPN only |
| 445 | SMB | Block from Internet |

---

## 5. Network Topologies & LAN Segmentation
- **Star** – Central switch; single point of failure but easy to manage.  
- **Bus** – Cheap; collisions & single break kills the segment.  
- **Ring** – Token-based; cable cut = entire ring down.

**Subnetting**  
- Network: `192.168.1.0/24`  
- Gateway: `.1` or `.254`  
- Hosts: `.1-254` (minus network & broadcast).  
- **VLANs** isolate departments; use **ACLs** between VLANs.

---

## 6. Routing & Path Selection
- **OSPF** – Link-state; fast convergence; large networks.  
- **RIP** – Distance-vector; hop-count ≤ 15; small/simple.  
- **uRPF** prevents IP spoofing.  
- **BGP RPKI** validates route origins.

---

## 7. Monitoring & Incident Response

### Live host sweep
`nmap -sn 192.168.1.0/24`

### Banner grab
`nc -nv 10.0.0.10 80`

### DNS tunnel check
`dig +short tunnel.evil.com`

### Port scan detection
`tcpdump -i eth0 'tcp[tcpflags] & (tcp-syn) != 0'`

### Rogue DHCP
`dhcpdump -i eth0`


---

## 8. NAT & Firewall Zones
- **DNAT** = Port-forward external → internal.  
- **SNAT** = Masquerade outbound traffic.  
- **Zones**: Green (internal), Orange (DMZ), Red (Internet).  
  – Default **deny-inbound**, allow **related/established**.

---

## 9. Secure Network Mindset
- Encrypt **in transit** (TLS 1.2+).  
- Authenticate **endpoints** (802.1X, certs).  
- Log **everything** (NetFlow, syslog).  
- Inspect **every layer** (WAF, IDS, endpoint AV).

---

## 10. End-to-End Web Request Flow
1. Browser → DNS lookup → WAF → Load Balancer  
2. Load Balancer → Web Server (static or dynamic)  
3. Web App → Database → Rendered HTML → Client  

**Security Stack**: CDN → WAF → LB → App → DB → Logging.

---
