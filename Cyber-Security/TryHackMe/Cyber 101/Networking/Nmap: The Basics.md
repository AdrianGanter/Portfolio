# Nmap: The Basics

Overview
--------
Nmap is a network scanning tool used to discover live hosts, open ports, running services, and operating system information across a network.

TARGET SPECIFICATION
--------------------
- IP range: 192.168.0.1-10
- Subnet: 192.168.0.1/24 (equivalent to 192.168.0.0–255)
- Hostname: example.thm

HOST DISCOVERY
--------------
- -sL  -> List targets only (no scan performed)
- -sn  -> Ping scan (host discovery only)

PORT SCANNING
--------------
- -sT  -> TCP connect scan (full 3-way handshake)
- -sS  -> SYN scan (half-open, faster and quieter)
- -sU  -> UDP scan

PORT SELECTION
--------------
- -F        -> Fast scan (top 100 ports)
- -p-       -> Scan all ports (1–65535)
- -p1-1024   -> Well-known ports
- -p 22      -> Specific port

DEFAULT BEHAVIOUR
------------------
- By default, Nmap scans the top 1000 most common TCP ports

FORCING SCANS
-------------
- -Pn  -> Treat all hosts as online (skip host discovery)

SERVICE & OS DETECTION
-----------------------
- -sV  -> Service and version detection
- -O   -> OS detection
- -A   -> Aggressive scan (OS + version + scripts + traceroute)

TIMING & PERFORMANCE
--------------------
- -T0  -> Paranoid (very slow, stealthy)
- -T1  -> Sneaky
- -T2  -> Polite
- -T3  -> Normal (default)
- -T4  -> Aggressive (faster scans)
- -T5  -> Insane (very fast, noisy)

Rate Control:
- --min-rate <n>  -> Minimum packets per second
- --max-rate <n>  -> Maximum packets per second

Parallelism:
- --min-parallelism <n>  -> Minimum concurrent probes
- --max-parallelism <n>  -> Maximum concurrent probes

Timeout:
- --host-timeout <time>  -> Maximum time to wait per host

OUTPUT OPTIONS
--------------
- -oN <file>  -> Normal output (human-readable)
- -oX <file>  -> XML output
- -oG <file>  -> Grepable output
- -oA <base>  -> Output in all formats

VERBOSITY & DEBUGGING
---------------------
- -v   -> Verbose output
- -vv  -> Higher verbosity
- -v4  -> Maximum verbosity (explicit level)

- -d   -> Debug output
- -d9  -> Maximum debugging detail

Real-time control:
- Press 'v' to increase verbosity during scan
- Press 'd' to increase debugging during scan

COMMON SCENARIOS
----------------
`nmap -sn 192.168.0.1/24`
  -> Discover live hosts

`nmap -sS 192.168.0.1`
  -> Basic SYN scan

`nmap -sV 192.168.0.1`
  -> Detect service versions

`nmap -O 192.168.0.1`
  -> OS detection

`nmap -A 192.168.0.1`
  -> Full aggressive scan (OS + services + scripts + traceroute)

`nmap -p- 192.168.0.1`
  -> Scan all ports

`nmap -Pn 192.168.0.1`
  -> Scan even if host appears down

COMBINED EXAMPLE
----------------
- nmap -sS -sV -O -p- -T4 192.168.0.1
  -> Full detailed scan with OS, services, and all ports

SUMMARY FLAGS
-------------
- -sL  -> List scan
- -sn  -> Host discovery only
- -sT  -> TCP connect scan
- -sS  -> SYN scan
- -sU  -> UDP scan
- -F   -> Fast scan (100 ports)
- -p-  -> All ports
- -Pn  -> Skip host discovery
- -sV  -> Service/version detection
- -O   -> OS detection
- -A   -> Aggressive scan
- -T0–T5 -> Timing templates
- -v / -d -> Verbosity & debugging
- -oN / -oX / -oG / -oA -> Output formats
