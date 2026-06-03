# TCPDUMP NOTES

Tool Overview
-------------
tcpdump is a command-line packet analysis tool used to capture and inspect network traffic in real time or from saved capture files.

Basic Capture
-------------
sudo tcpdump -i any
sudo tcpdump -i eth0
ip a s / ip address show   -> view interfaces

Capturing Packets to File
-------------------------
tcpdump -i any -w capture.pcap
- Writes raw packet data to a .pcap file for later analysis

Reading Captured Files
----------------------
tcpdump -r capture.pcap
- Reads packets from a saved file instead of live capture

Limit Packet Count
------------------
tcpdump -c 50
- Stops capture after 50 packets

Disable Name Resolution
-----------------------
tcpdump -n
- Do NOT resolve IP addresses to hostnames

tcpdump -nn
- Disable IP resolution AND port/protocol name resolution (faster, cleaner output)

Verbosity Levels
----------------
tcpdump -v
tcpdump -vv
tcpdump -vvv
- Increases detail shown in packet output (TTL, headers, options, etc.)

Example Combined Command
------------------------
sudo tcpdump -i any -c 50 -nn

FILTERING TRAFFIC

Host Filtering
--------------
tcpdump host 1.1.1.1
tcpdump src host 1.1.1.1
tcpdump dst host example.com

Port Filtering
--------------
tcpdump port 53        -> DNS traffic
tcpdump src port 80
tcpdump dst port 443

Protocol Filtering
------------------
tcpdump tcp
tcpdump udp
tcpdump icmp
tcpdump ip / ip6

Logical Operators
-----------------
and  -> both conditions must match
or   -> either condition matches
not  -> exclude condition

Examples:
tcpdump host 1.1.1.1 and tcp
tcpdump udp or icmp
tcpdump not tcp

PRACTICAL EXAMPLES
------------------
tcpdump -i any tcp port 22
- Capture SSH traffic

tcpdump -i wlan0 udp port 123
- Capture NTP traffic

tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap
- Capture HTTPS traffic for a specific host and save it

READING CAPTURE FILES (EXAMPLE)
------------------------------
tcpdump -r traffic.pcap -c 5 -n
- Read first 5 packets without DNS resolution

PACKET DISPLAY OPTIONS
----------------------
-q   -> quick output (minimal detail)
-e   -> include MAC addresses
-A   -> ASCII view of packet data
-xx  -> hex dump of packet data
-X   -> hex + ASCII output

BYTE-LEVEL FILTERING (pcap filters)
-----------------------------------
proto[expr:size]
- proto = protocol (ip, tcp, udp, ether, etc.)
- expr = byte offset (0 = first byte)
- size = number of bytes (1,2,4 optional)

Example concepts:
ether[0] & 1 != 0   -> multicast Ethernet traffic
ip[0] & 0xf != 5    -> IP packets with options

FILTER MODIFIERS
----------------
greater LENGTH -> packets larger than size
less LENGTH    -> packets smaller than size

BINARY OPERATORS
----------------
&  (AND) -> both bits must be 1
|  (OR)  -> either bit is 1
!  (NOT) -> inverts bit value

Example truth logic:
0 & 1 = 0
1 & 1 = 1
0 | 1 = 1
!1 = 0

SUMMARY
-------
tcpdump -i INTERFACE      -> capture on interface
tcpdump -w file.pcap      -> write capture to file
tcpdump -r file.pcap      -> read capture file
tcpdump -c COUNT          -> limit packets
tcpdump -n / -nn          -> disable DNS/port resolution
tcpdump -v/-vv/-vvv       -> verbosity levels
