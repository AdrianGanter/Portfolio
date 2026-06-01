# Gobuster: Fundamentals

## Overview

Gobuster is an open-source offensive security tool written in Go (Golang) used for enumeration through brute-force techniques. It assists security professionals in discovering hidden resources that may not be visible through normal browsing.

Common use cases include:

- Web directory enumeration
- File discovery
- Subdomain enumeration
- Virtual host (vHost) discovery
- Cloud storage bucket enumeration (AWS S3 / Google Cloud Storage)

Gobuster is commonly used during the Reconnaissance and Enumeration phases of a security assessment.

---

## Key Concepts

### Enumeration

Enumeration is the process of systematically identifying and listing resources that exist on a target system.

Examples:

- Discovering hidden web directories
- Identifying subdomains
- Finding virtual hosts
- Enumerating cloud storage buckets

The goal is to uncover attack surface that may not be publicly exposed.

### Brute Force

Brute forcing involves testing many possible values until a valid result is found.

Gobuster uses wordlists to automate this process by sending requests based on predefined entries.

Example:

If a wordlist contains:

admin
backup
images

Gobuster will test:

/admin
/backup
/images

and report any valid findings.

---

## Common Gobuster Modes

### Directory Enumeration

Used to discover hidden directories and files on web servers.

```bash
gobuster dir -u http://target.com -w wordlist.txt
```

### DNS Enumeration

Used to discover subdomains.

```bash
gobuster dns -d target.com -w wordlist.txt
```

### Virtual Host Enumeration

Used to identify hidden virtual hosts configured on a web server.

```bash
gobuster vhost -u http://target-ip -w wordlist.txt
```

---

## Common Flags

| Flag | Purpose |
|--------|---------|
| `-u` | Target URL |
| `-w` | Wordlist path |
| `-t` | Number of concurrent threads |
| `--delay` | Delay between requests |
| `-o` | Save output to a file |
| `--debug` | Troubleshooting and verbose diagnostics |

---

## Example Command

```bash
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/small.txt -t 64
```

This command:

- Targets a web application
- Uses the `small.txt` wordlist
- Tests potential directories and files
- Utilizes 64 concurrent threads to improve speed

---

## SOC Analyst Relevance

Understanding Gobuster helps analysts:

- Recognize enumeration activity in web server logs
- Identify brute-force directory discovery attempts
- Investigate suspicious scanning behaviour
- Understand attacker reconnaissance techniques
- Improve detection engineering and threat hunting capabilities

Common indicators include:

- High volumes of HTTP requests
- Sequential requests to non-existent paths
- Requests matching common wordlist entries
- Increased 404 responses from a single source

---

## Key Takeaway

Gobuster is a powerful enumeration tool used to identify hidden resources through wordlist-driven brute forcing. Understanding how it operates enables security professionals to both perform assessments and detect reconnaissance activity within enterprise environments.

---

## Practical 1

Enumerate directories of www.offensivetools.thm (10.49.146.52)

```gobuster dir -u http://10.49.146.52 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt```

Directory that stands out: /secret

Digging deeper..

```gobuster dir -u http://10.49.146.52/secret -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt```

Found: /content /uploads 

Look for a .js file

```gobuster dir -u http://10.49.146.52/secret/content -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x .js```

Found: /flag.js

```curl http://10.49.146.52/secret/content/flag.js```

Flag: THM{ReconWasASuccess}

---

