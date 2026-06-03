### Recon & Threat-Intel Fundamentals (Quick-Ref)

#### Core Search Operators
| Goal | Google Example |
|---|---|
| Exact phrase | `"passive reconnaissance"` |
| Domain-only | `site:tryhackme.com success stories` |
| Omit noise | `pyramids -tourism` |
| File discovery | `filetype:ppt cyber security` |

#### Essential Services & One-liners
| Service | Purpose | Quick Command |
|---|---|---|
| **Shodan** | Internet-facing devices | `apache country:"US" port:"80"` |
| **Censys** | Host & certificate inventory | `services.http.response.headers.server: nginx` |
| **VirusTotal** | Multi-AV file/URL scan | `curl -X POST --form file=@malware.exe https://www.virustotal.com/vtapi/v2/file/scan?apikey=YOUR_KEY` |
| **HIBP** | Breach lookup | `curl https://haveibeenpwned.com/api/v3/breachedaccount/user@example.com` |
| **CVE Details** | Vulnerability ID lookup | `https://nvd.nist.gov/vuln/detail/CVE-2024-29988` |
| **Exploit-DB** | Proof-of-concept search | `searchsploit apache 2.4` |
| **GitHub** | PoC & tools | `CVE-2024-29988 poc` |

#### Docs & Manuals
- Linux: `man <command>` (e.g., `man ip`)
- Windows: `ipconfig /?` or `https://learn.microsoft.com/`
- Product manuals: `filetype:pdf <product> manual`

#### OSINT Mindset
- People: LinkedIn job titles, Facebook schools → possible security-question answers.
- Reduce exposure: unique aliases, minimal public PII.
