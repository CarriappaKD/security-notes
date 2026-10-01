# Module 3: Secure Against Network Intrusions

Every network has inherent vulnerabilities and can become a target. Attackers use methods like malware, spoofing, packet sniffing, and packet flooding to infiltrate systems — successful attacks can cause leakage of valuable/confidential information, resulting in financial and reputational damage. Security analysts must stay alert to potential vulnerabilities and act quickly to mitigate them.

## Network Interception Attacks

Attacks that work by intercepting network traffic (packet sniffing) to steal information or interfere with the transmission — e.g., inserting malicious code or altering the message in transit.

## Backdoor Attacks

**Backdoors** are weaknesses intentionally left by programmers or admins that bypass normal access control — originally meant to help with troubleshooting/admin tasks. Attackers can also install backdoors after compromising a system to maintain **persistent access**.

Damage a backdoor can enable:
- Installing malware
- Performing a DoS attack
- Stealing private information
- Changing security settings to leave the system further exposed

## Denial of Service (DoS) Attacks

| Term | Definition |
|---|---|
| **DoS (Denial of Service)** | Floods a network/server with traffic to disrupt normal operations, making it unavailable to legitimate users |
| **DDoS (Distributed Denial of Service)** | A DoS attack using multiple devices from various locations to flood the target, increasing the likelihood of overwhelming it |

### Network-Level DoS Attack Types

| Attack | How It Works |
|---|---|
| **SYN Flood** | Exploits the TCP handshake by flooding a server with SYN requests, exceeding available ports until the server is overwhelmed |
| **ICMP Flood** | Repeatedly sends ICMP packets, forcing the server to respond in kind — consuming bandwidth both ways until it crashes |
| **Ping of Death** | Sends an oversized ICMP packet (>64 KB) to a vulnerable system, overloading and crashing it |

## Network Protocol Analyzers (Packet Sniffers)

Tools designed to capture and analyze data traffic within a network — commonly used as investigative tools to monitor networks and identify suspicious activity.

**Common analyzers:**
- SolarWinds NetFlow Traffic Analyzer
- ManageEngine OpManager
- Azure Network Watcher
- Wireshark
- tcpdump

### tcpdump

A command-line network protocol analyzer — popular, lightweight (low memory/CPU usage), built on the open-source **libpcap** library. It's text-based: all commands run in the terminal, and it prints packet info directly to the terminal in a human-readable format.

**Information from a packet capture:**
- **Timestamp** — hours, minutes, seconds, fractions of a second
- **Source IP** — the packet's origin
- **Source port** — where the packet originated
- **Destination IP** — where the packet is headed
- **Destination port** — the destination port number

**Uses for protocol analyzers:**
- Establishing a baseline for normal network traffic/utilization
- Detecting and identifying malicious traffic
- Creating customized alerts for network issues or security threats
- Locating unauthorized instant messaging traffic or wireless access points

> ⚠️ The same tools used defensively can also be used maliciously — attackers use protocol analyzers to capture sensitive data like usernames and passwords.

## Malicious Packet Sniffing

Using software tools to capture/analyze data packets in transit, which may contain names, financial details, credit card numbers, etc.

| Type | Description |
|---|---|
| **Passive sniffing** | Reads packets in transit without altering them — like a postal worker reading mail |
| **Active sniffing** | Manipulates packets in transit — redirecting or changing content, like a neighbor intercepting and altering mail |

**Preventing malicious packet sniffing:**
- **Use a VPN** — encrypts data so it's unreadable even if intercepted
- **Use HTTPS** — ensures secure, encrypted communication with websites
- **Avoid unprotected Wi-Fi** — public networks often lack encryption

> **NIC (Network Interface Card)** — hardware connecting a device to a network. Normally, it only accepts packets addressed to its own MAC address. In **promiscuous mode**, however, a NIC accepts *all* traffic on the network — even packets not addressed to it — which is how packet sniffing tools work.

## IP Spoofing

Attacker alters a packet's source IP address to impersonate an authorized system, allowing them to bypass firewall rules and gain unauthorized network access. Firewalls can be configured to reject unauthorized/suspicious IP traffic as a defense.

### Common IP Spoofing Attacks

| Attack | Description | Key Defense |
|---|---|---|
| **On-path attack** (a.k.a. meddler-in-the-middle) | Attacker positions themselves between two communicating devices, intercepts data, and impersonates one device after learning its IP/MAC address | Encrypt data in transit (e.g., TLS) |
| **Replay attack** | Attacker intercepts a packet and delays or retransmits it later to impersonate an authorized user or cause connection issues | — |
| **Smurf attack** | Combines DDoS + IP spoofing — attacker sniffs a user's IP and floods it with packets; once the spoofed packet hits the broadcast address, it's sent to every device/server on the network | Advanced firewall (NGFW) that detects unusual traffic/oversized broadcasts |

### Protecting Against IP Spoofing
- **Encryption** — prevents attackers from reading data in transit
- **Firewall configuration** — reject incoming internet traffic if the sender's IP matches the private network's IP range

> No single strategy stops every attack type — **layered defense** (multiple overlapping strategies) is the practical approach.

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 3 — Connect and Protect: Networks and Network Security*
