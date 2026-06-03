# Nmap: The Basics

Overview
--------
Nmap is used for network discovery and security auditing. It identifies live hosts, open ports, services, and potential operating systems on a network.

TARGET SPECIFICATION
--------------------
IP range:
192.168.0.1-10

Subnet:
192.168.0.1/24  (equivalent to 192.168.0.0–255)

Hostname:
example.thm

HOST DISCOVERY
--------------
-sL  -> List targets only (no scan)
-sn  -> Ping scan (host discovery only)

PORT SCANNING
--------------
-sT  -> TCP connect scan (full 3-way handshake)
-sS  -> SYN scan (half-open, faster and less noisy)
-sU  -> UDP scan

PORT SELECTION
--------------
-F        -> Fast scan (top 100 ports)
-p-       -> All ports (1–65535)
-p10-1024 -> Port range
-p 22     -> Specific port

Default scan:
- Top 1000 TCP ports

SERVICE & OS DETECTION
-----------------------
-sV  -> Service/version detection
-O   -> OS detection
-A   -> Aggressive scan (OS + version + traceroute + scripts)

FORCING SCANS
-------------
-Pn  -> Treat hosts as online (skip host discovery)

TIMING & PERFORMANCE
--------------------
-T0  -> Paranoid (very slow)
-T1  -> Sneaky
-T2  -> Polite
-T3  -> Normal (default)
-T4  -> Aggressive
-T5  -> Insane (fast, noisy)

Rate control:
--min-rate <n>
--max-rate <n>

Parallelism:
--min-parallelism <n>
--max-parallelism <n>

Timeout:
--host-timeout <time>

VERBOSITY & DEBUGGING
---------------------
-v        -> Verbose output
-vv / -v4 -> Increased verbosity
-d        -> Debug output
-d9       -> Maximum debugging

Output can be increased during scan by pressing 'v' or 'd'

OUTPUT OPTIONS
--------------
-oN <file>  -> Normal output
-oX <file>  -> XML output
-oG <file>  -> Grepable output
-oA <base>  -> All formats combined

COMMON USE CASE EXAMPLES
------------------------
`nmap -sn 192.168.0.1/24`
-> Discover live hosts

`nmap -sS -p 1-1000 192.168.0.1`
-> SYN scan of common ports

`nmap -sV -O 192.168.0.1`
-> Detect services and OS

`nmap -A 192.168.0.1`
-> Full aggressive scan

`nmap -Pn 192.168.0.1`
-> Scan even if host appears offline

SUMMARY TABLE
-------------
-sL  -> List targets
-sn  -> Host discovery only
-sT  -> TCP connect scan
-sS  -> SYN scan
-sU  -> UDP scan
-F   -> Fast scan (100 ports)
-p-  -> All ports
-Pn  -> Skip host discovery

-sV  -> Service/version detection
-O   -> OS detection
-A   -> Full aggressive scan

-T0–T5 -> Timing templates
-v / -d -> Verbosity & debugging

-oN / -oX / -oG / -oA -> Output formats
