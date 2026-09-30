# Module 2: Network Operations

## Network Protocols

A **network protocol** is a set of rules describing the order of delivery and structure of data used by two or more devices — essentially a common language enabling devices worldwide to communicate. Some protocols have known vulnerabilities threat actors exploit (e.g., abusing DNS to redirect traffic from a legitimate site to a malicious one). Port numbers for many protocols are assigned by **IANA (Internet Assigned Numbers Authority)**.

Protocols fall into three main categories: **communication, management, and security** protocols.

### 1. Communication Protocols
Govern the exchange of information in network transmission, including recovery of data lost in transit.

| Protocol | Full Form | Purpose | Port(s) | TCP/IP Layer |
|---|---|---|---|---|
| **TCP** | Transmission Control Protocol | Connection-based, reliable data streaming. Uses a **three-way handshake**: SYN → SYN/ACK → ACK | — | Transport |
| **UDP** | User Datagram Protocol | Connectionless, less reliable (e.g., DNS requests to local servers) | — | Transport |
| **HTTP** | Hypertext Transfer Protocol | Client–website server communication; considered insecure | 80 | Application |
| **DNS** | Domain Name System | Translates domain names to IP addresses; usually UDP, switches to TCP for large replies | 53 | Application |
| **ARP** | Address Resolution Protocol | Translates IP addresses (in packets) into MAC addresses, since MAC is permanent but may be unknown | — | Network Access |
| **POP3** | Post Office Protocol (version 3) | Retrieves email from a mail server | 110 (plaintext) / 995 (SSL/TLS) | Application |
| **IMAP** | Internet Message Access Protocol | Manages incoming email; keeps content on the server so it's accessible from multiple devices | 143 (unencrypted) / 993 (TLS) | Application |
| **SMTP** | Simple Mail Transfer Protocol | Transmits/routes email from sender to recipient, using MTA (Message Transfer Agent) software + DNS lookups | 25 (unencrypted) / 587 (TLS) | Application |

> **TCP three-way handshake:** device sends SYN (Synchronize) → server responds SYN/ACK (Synchronize/Acknowledge) → device sends final ACK (Acknowledge) → connection established.

### 2. Management Protocols
Used for monitoring/managing network activity — error reporting and performance optimization.

| Protocol | Full Form | Purpose | Port(s) | TCP/IP Layer |
|---|---|---|---|---|
| **SNMP** | Simple Network Management Protocol | Monitors/manages network devices; can reset passwords or change baseline configs | — | Application |
| **ICMP** | Internet Control Message Protocol | Reports data transmission errors between devices; basis of the `ping` command for troubleshooting connectivity/latency | — | Internet |
| **DHCP** | Dynamic Host Configuration Protocol | Assigns unique IP addresses to devices (working with the router); also provides DNS server/gateway info | Server: UDP 67 / Client: UDP 68 | Application |
| **Telnet** | (not an acronym — from "teletype network") | Connects to a remote system via command line; sends everything in **clear text** (insecure) | 23 | Application |

### 3. Security Protocols
Use encryption to ensure data is sent/received securely.

| Protocol | Full Form | Purpose | Port | TCP/IP Layer |
|---|---|---|---|---|
| **HTTPS** | Hypertext Transfer Protocol Secure | Secure version of HTTP using SSL/TLS (Secure Sockets Layer/Transport Layer Security) encryption | 443 | Application |
| **SFTP** | Secure File Transfer Protocol | Secure file transfer, built on SSH; uses AES (Advanced Encryption Standard) and other encryption | 22 (via SSH) | Application |
| **SSH** | Secure Shell | Secure connection to a remote system; replaces insecure protocols like Telnet | 22 | Application |

> Note: these encryption protocols secure the *data*, but do **not** conceal the source/destination IP address of the traffic.

## Network Address Translation (NAT)

Devices on a local network use **private IP addresses** to communicate with each other, but need to share a single **public IP address** to communicate with the internet. The router swaps the private source IP for its public IP on outgoing traffic, and reverses this for incoming responses. This process — **NAT (Network Address Translation)** — generally requires a router/firewall specifically configured for it. NAT operates at the internet layer (layer 2) and transport layer (layer 3) of the TCP/IP model.

| | Private IP | Public IP |
|---|---|---|
| **Assigned by** | Router | ISP (Internet Service Provider) and IANA |
| **Uniqueness** | Unique only within the private network | Unique across the global internet |
| **Cost** | Free | Costs to lease |
| **Ranges** | 10.0.0.0–10.255.255.255, 172.16.0.0–172.31.255.255, 192.168.0.0–192.168.255.255 | 1.0.0.0–9.255.255.255, 11.0.0.0–126.255.255.255, 128.0.0.0–172.15.255.255, 172.32.0.0–192.167.255.255, 192.169.0.0–233.255.255.255 |

## Wireless Protocols (Wi-Fi Security)

**IEEE 802.11 (Wi-Fi)** — standards for wireless LAN (Local Area Network) communication, maintained by the **IEEE (Institute of Electrical and Electronics Engineers)**. Secured through a series of evolving wireless protocols:

| Protocol | Full Form | Notes |
|---|---|---|
| **WEP** | Wired Equivalent Privacy | Earliest; encryption can be broken by attackers — now considered **high-risk** |
| **WPA** | Wi-Fi Protected Access | Improved on WEP using **TKIP (Temporal Key Integrity Protocol)** and larger keys; still vulnerable to **KRACK (Key Reinstallation Attack)** |
| **WPA2** | Wi-Fi Protected Access 2 | Uses **AES (Advanced Encryption Standard)** + **CCMP (Counter Mode Cipher Block Chain Message Authentication Code Protocol)** (replacing TKIP); today's security standard for Wi-Fi — but still vulnerable to KRACK |
| **WPA3** | Wi-Fi Protected Access 3 | Fixes the KRACK vulnerability; uses **SAE (Simultaneous Authentication of Equals)** and stronger encryption (128-bit, with 192-bit optional in Enterprise mode) |

**WPA2 modes:**
- **Personal** — best for home networks; simpler/faster setup
- **Enterprise** — best for business networks; more complex setup but offers individualized, centralized access control

## Firewalls

Devices that inspect and filter network traffic before it enters the private network.

**By form factor:**
- **Hardware firewalls** — physical devices inspecting packets before network entry
- **Software firewalls** — installed programs performing the same role, but add processing load

**By operation:**
- **Stateless** — operate on predefined rules only, don't track packet info — less secure
- **Stateful** — actively monitor and track traffic, proactively filtering suspicious activity
- **NGFW (Next-Generation Firewall)** — most advanced; adds **deep packet inspection** and intrusion prevention, with optional extras like malware sandboxing, network antivirus, and URL/DNS filtering

## Virtual Private Networks (VPNs)

**VPN = Virtual Private Network**

- Change your public IP and hide your virtual location, keeping data private on public networks
- Prevent ISPs (Internet Service Providers)/attackers from linking your internet activity to your physical location/identity
- **Encapsulation** — VPN wraps sensitive data inside other data packets that routers can read, while your actual data stays encrypted
- Creates an **encrypted tunnel** between your device and the VPN server, unhackable without the cryptographic key

**SD-WAN (Software-Defined Wide Area Network)** — a virtual WAN (Wide Area Network) service securely connecting users to applications across multiple locations/large distances. Organizations increasingly combine VPN + SD-WAN for network security.

### VPN Types
- **Remote access VPN** — connects an individual's personal device to a VPN server; encrypts their traffic
- **Site-to-site VPN** — used by enterprises to extend their network to other locations/networks (e.g., multiple offices); more complex to configure/manage than remote access VPNs

### VPN Protocols
| Protocol | Full Form | Notes |
|---|---|---|
| **WireGuard** | (a proper name, not an acronym) | Newer, high-speed, simpler setup; fewer lines of code = faster; supports both site-to-site and client-server connections |
| **IPSec** | Internet Protocol Security | Older, more complex; most VPN providers use it to encrypt/authenticate packets; used for site-to-site connections |

## Proxy Servers

Enhance network security by filtering traffic and hiding internal network details — using NAT (Network Address Translation) to act as a barrier between internal clients and external threats.

- A proxy server sits between the internet and the internal network, forwarding client requests
- Has its own public IP, hiding internal (private) IPs from external actors
- Determines if connection requests are safe, blocks unsafe sites, and can cache frequent data to reduce load
- Protects internal servers from having their IPs exposed externally

### Types of Proxy Servers
- **Forward proxy** — regulates/restricts internal users' outgoing internet access, hiding their IPs
- **Reverse proxy** — accepts/vets external traffic before forwarding it to internal servers, shielding them from direct exposure
- **Email proxy** — filters spam and verifies sender addresses to reduce phishing risk

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 3 — Connect and Protect: Networks and Network Security*
