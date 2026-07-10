# Detecting Web Attacks

## Client-Side Attacks
- Target the **user's browser or device** rather than the web server.
- Often rely on:
  - User interaction
  - Browser vulnerabilities
  - Third-party scripts/plugins
- Difficult to detect from server logs because activity occurs on the client.
- Better visibility requires:
  - Browser security controls
  - Endpoint Detection & Response (EDR)

### Common Client-Side Attacks
| Attack | Description |
|---------|-------------|
| Cross-Site Scripting (XSS) | Injects malicious JavaScript into trusted webpages to steal cookies, sessions, or execute code in the victim's browser. |
| Cross-Site Request Forgery (CSRF) | Tricks a logged-in user's browser into sending unauthorized requests. |
| Clickjacking | Invisible elements trick users into clicking unintended actions. |

---

# Server-Side Attacks

- Exploit vulnerabilities within:
  - Web servers
  - Application code
  - Backend services
  - Databases
- Easier to investigate because requests generate:
  - Server logs
  - Network traffic
  - Security monitoring events

### Common Server-Side Attacks

| Attack | Description |
|---------|-------------|
| Brute Force | Automated login attempts using many username/password combinations. |
| SQL Injection (SQLi) | Manipulates SQL queries to read, modify, or delete database contents. Usually prevented with parameterized queries. |
| Command Injection | Executes operating system commands through vulnerable application input. |

---

# Web Server Access Logs

Every HTTP request can leave forensic evidence.

## Common Log Fields

| Field | Indicators of Suspicious Activity |
|--------|----------------------------------|
| Client IP | Known malicious IPs or unexpected geographic locations |
| Timestamp | High request frequency or unusual access times |
| Requested Resource | Sensitive files or hidden directories |
| HTTP Status Code | Numerous 404 errors, redirects, or failures |
| Response Size | Abnormally large or small responses |
| Referrer | Unexpected referring pages |
| User-Agent | Automated tools (sqlmap, wpscan, Hydra, etc.) or outdated browsers |

---

# Typical Web Attack Chain

1. Directory fuzzing
   - Searches for hidden directories/files.
   - Multiple requests with many 404 responses.
   - Successful discoveries often return **200 OK**.

2. Brute-force login
   - Rapid repeated POST requests.
   - Successful login may return:
     - **302 Redirect**
     - Redirect to authenticated pages.

3. SQL Injection
   - Injects SQL payloads into parameters.
   - Common payloads:
     ```
     ' OR '1'='1
     ```
     ```
     1' OR 'a'='a
     ```

---

# Limitations of Access Logs

Access logs often **do not record**:

- POST request bodies
- Submitted usernames/passwords
- Uploaded files
- Full request payloads

Visibility depends on:

- Server software
- Logging configuration
- Log format

---

# Network Traffic Analysis

Packet captures provide much deeper visibility than logs.

Can reveal:

- Full HTTP headers
- POST body data
- Cookies
- File uploads/downloads
- Complete requests and responses

Useful when server logs lack detail.

### Encryption Considerations

Encrypted protocols (HTTPS/TLS) hide payload contents unless traffic can be decrypted.

---

# Detecting Attacks in Wireshark

Useful display filters:

```
http
```

```
ip.dst == <server_ip>
```

```
http.user_agent
```

Useful investigation techniques:

- Follow HTTP Stream
- Inspect POST bodies
- View submitted credentials
- Examine SQL injection payloads
- Recover returned database data

---

# Indicators of Common Web Attacks

## Directory Fuzzing

Look for:

- Large number of GET requests
- Many 404 responses
- Automated User-Agent strings
- Discovery of valid pages (200 responses)

---

## Brute Force

Indicators:

- Repeated POST requests
- Same endpoint
- Many failed logins
- One eventual success
- HTTP 302 redirect after successful authentication

---

## SQL Injection

Indicators:

- SQL operators in URLs or POST data
- Quotes (`'`)
- Boolean logic (`OR`)
- UNION statements
- Database error messages
- Unexpected database responses

Common payloads:

```
' OR '1'='1
```

```
UNION SELECT ...
```

---

# Web Application Firewalls (WAF)

A WAF sits between users and web applications.

Functions:

- Inspects incoming requests
- Filters malicious traffic
- Can decrypt HTTPS traffic
- Blocks attacks before they reach the web server

---

# Common WAF Rule Types

### Block Attack Patterns

Examples:

- SQLi payloads
- XSS payloads
- Known exploit signatures

---

### Block Known Malicious Sources

Uses:

- IP reputation
- Threat intelligence
- Geo-blocking

---

### Custom Rules

Example:

```
IF User-Agent contains "sqlmap"
THEN BLOCK
```

Can also create rules for:

- Specific URLs
- Allowed HTTP methods
- Custom application behaviour

---

### Rate Limiting

Protects against:

- Brute-force attacks
- Credential stuffing
- Bots
- DoS attempts

Example:

- Maximum 5 login attempts per minute per IP

---

# CAPTCHA / Challenge Responses

Instead of blocking immediately, WAFs can:

- Present CAPTCHA challenges
- Verify human users
- Reduce false positives
- Slow automated attacks

---

# Threat Intelligence Integration

Modern WAFs automatically update with:

- Malicious IP addresses
- Botnet indicators
- Known malicious User-Agents
- OWASP Top 10 protections
- CVE signatures
- Threat actor intelligence

---

# Detection Workflow

```
Web Request
      │
      ▼
Access Log + Packet Capture
      │
      ▼
Identify:
• User-Agent
• Source IP
• Request Frequency
• HTTP Methods
• Status Codes
• SQL Payloads
• POST Data
      │
      ▼
Determine:
• Directory Fuzzing
• Brute Force
• SQL Injection
• Command Injection
      │
      ▼
Mitigate:
• WAF Rules
• Rate Limits
• CAPTCHA
• IP Blocking
• Threat Intelligence
```

## Key Takeaways

- Client-side attacks are difficult to detect using server-side monitoring alone.
- Server-side attacks leave evidence in logs and network traffic.
- Access logs show request metadata but often omit POST bodies.
- Packet captures provide full visibility into HTTP requests and responses.
- Common attack sequence:
  1. Directory fuzzing
  2. Brute-force login
  3. SQL injection
- Indicators include unusual User-Agents, repeated requests, HTTP status codes, and SQL payloads.
- WAFs inspect, filter, and block malicious traffic using signatures, custom rules, rate limiting, CAPTCHA, and threat intelligence.
