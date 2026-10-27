# Module 2: Network Monitoring and Analysis

## Network Monitoring

Monitoring a network's traffic maintains situational awareness and helps detect suspicious activity. Ordinary events (sending an email, streaming video, visiting a website) all generate network traffic/data.

| Term | Meaning |
|---|---|
| **Network traffic** | The amount of data moving across a network |
| **Network data** | The data transmitted between devices on a network |

Network communications reveal useful details — source/destination IPs, data volume, timestamps, etc. — which help build a **baseline**: a reference point for normal/expected behavior. Knowing the baseline makes abnormal behavior easier to spot.

### Monitoring Network Components

| Component | What It Reveals |
|---|---|
| **Flow analysis** | Movement of communications — packets, protocols, ports. Watch for mismatches, e.g., HTTPS traffic using port 8088 instead of its standard port 443 — a sign of **command and control (C2)**, the techniques attackers use to maintain contact with a compromised system |
| **Packet payload information** | The actual transmitted data (often encrypted). Monitoring payloads can reveal sensitive data leaving the network — a possible **data exfiltration** indicator |
| **Temporal patterns** | Time-based activity patterns. Traffic spikes outside normal business hours (off-baseline) warrant investigation |

Through monitoring, organizations can catch intrusions early and secure components before damage occurs.

## Protecting the Network

A **network operations center (NOC)** monitors network *performance* and responds to disruptions (e.g., outages). This differs from a **SOC**, which focuses on *security* detection and response.

Security analysts watch for **indicators of compromise (IoC)** — signs of a potential security incident.

### Common Network Monitoring Tools

| Tool | Role |
|---|---|
| **IDS** | Monitors and alerts on intrusions, often by inspecting packet payload content for malware/phishing patterns |
| **Network protocol analyzers (packet sniffers)** | Capture and analyze network traffic in detail (e.g., tcpdump, Wireshark) via packet captures |

## Data Exfiltration Attacks

**Data exfiltration** is the unauthorized transmission of data out of a system — a large volume of outbound traffic from a host is a classic IoC.

### An Attacker's Path to Exfiltration

1. Gain **initial access** — often via phishing/social engineering
2. **Lateral movement (pivoting)** — explore the network, expand access, locate valuable assets (proprietary code, PII, financials)
3. **Collect and package** the data — often shrinking its size to evade detection/bypass controls
4. **Exfiltrate** the data to the attacker's destination (e.g., emailing it out via the compromised account)

### Defending Against It

- Prevent initial access — MFA against phishing
- Continuous monitoring — flag unusual activity like logins from unfamiliar IPs
- Maintain an asset inventory with appropriate controls
- Watch for unusual data-collection indicators (large internal transfers, large external uploads, unexpected file writes) using SIEM alerts; respond by, e.g., blocking the attacker's IP via firewall rules

## Network Traffic and Packet Structure

A **data packet** is the basic unit of information traveling between devices. Packets have three parts:

| Part | Role |
|---|---|
| **Header** | Routing info — source/destination IP, packet length, protocol, ID numbers. May include multiple headers (Ethernet, IP, TCP, etc.) |
| **Payload** | The actual data being delivered |
| **Footer (trailer)** | Error-checking info, used by protocols like Ethernet. Most protocols (e.g., IP) don't use one |

## Network Protocol Analyzers

Tools like **tcpdump**, **Wireshark**, and **TShark** capture/analyze traffic — used both to investigate suspicious activity and to troubleshoot performance (bandwidth, slowdowns). They can also be misused by attackers to intercept sensitive data like login credentials.

### How They Work

1. Packets are collected via the **Network Interface Card (NIC)**. By default a NIC only listens to traffic addressed to it — it must be switched into **promiscuous mode** (wired) or **monitor mode** (wireless) to see all visible traffic. The analyzer must also sit in the right network segment to actually reach that traffic.
2. The analyzer converts the raw binary capture into a human-readable format for analysts.

> Promiscuous mode exposes the capturing device to risk too, since it can also see sensitive data like passwords in the clear.

### Capturing Packets (p-cap)

**Packet sniffing** = capturing and inspecting data packets. A **packet capture (p-cap)** is the resulting file. Intercepting private communications without authorization is illegal in many places.

| Format | Notes |
|---|---|
| **Libpcap** | Default for Unix-like systems (Linux, macOS); used by tcpdump |
| **WinPcap** | Older Windows library, largely obsolete |
| **Npcap** | Modern Windows library, built by the Nmap project |
| **PCAPng** | Modern "next-generation" format — captures packets and stores data simultaneously |

## Internet Protocol (IP)

**IP** is the set of standards for routing and addressing packets across a network — the foundation of internet communication. Two versions are in use: **IPv4** and **IPv6**.

### IPv4 Header Fields (13 total)

| Field | Purpose |
|---|---|
| Version | Identifies the IP version (IPv4) |
| Internet Header Length (IHL) | Length of the header, including Options |
| Type of Service (ToS) | Delivery priority info |
| Total Length | Full packet length (header + data) |
| Identification | Unique ID for fragments of a packet, for reassembly |
| Flags | Fragmentation info — whether fragmented, more fragments coming |
| Fragment Offset | Correct sequence order of fragments |
| Time to Live (TTL) | Limits how long a packet circulates before being dropped |
| Protocol | Protocol used for the data portion |
| Header Checksum | Error-checking value for the header |
| Source Address | Sender's address |
| Destination Address | Receiver's address |
| Options | Optional — can apply security options |

### IPv6 Header Fields (8 total)

| Field | Purpose |
|---|---|
| Version | Identifies IPv6 |
| Traffic Class | Priority/class info (IPv4's ToS equivalent) |
| Flow Label | Identifies packets belonging to the same flow (sequence from one source) |
| Payload Length | Length of the data portion |
| Next Header | Type of header that follows (e.g., TCP) |
| Hop Limit | Limits travel distance before discard (IPv4's TTL equivalent) |
| Source Address | Sender's address |
| Destination Address | Receiver's address |

IPv6 adoption is growing mainly because of its much larger address space.

## Packet Capture with Wireshark

**Wireshark** is an open-source, GUI-based network protocol analyzer — easier to visualize captures with than a CLI tool.

### Display Filters

Used to isolate relevant packets out of large captures — filterable by protocol, IP, port, or virtually any packet property.

| Operator | Symbol | Abbreviation |
|---|---|---|
| Equal | `==` | `eq` |
| Not equal | `!=` | `ne` |
| Greater than | `>` | `gt` |
| Less than | `<` | `lt` |
| Greater than or equal | `>=` | `ge` |
| Less than or equal | `<=` | `le` |

Filters can be combined with `and`/`or`, and grouped with parentheses for complex queries.

- **`contains`** — matches an exact text string, e.g.: `http contains "moved"`
- **`matches`** — matches a regular expression (regex) pattern

**Common filter examples:**
```
dns                          # filter by protocol
ip.addr == 172.21.224.2      # filter by any matching IP
ip.src == 10.10.10.10        # filter by source IP
ip.dst == 4.4.4.4             # filter by destination IP
eth.addr == 00:70:f4:23:18:c4 # filter by MAC address
udp.port == 53                # filter by UDP port
tcp.port == 25                # filter by TCP port
```

Other protocol filters: `http`, `ftp`, `ssh`, `arp`, `telnet`, `icmp`.

**Following streams:** Wireshark can reassemble a full **stream/conversation** (an exchange between two devices over a protocol) into a readable format — useful for reviewing, e.g., a full HTTP request/response exchange.

## Packet Capture with tcpdump

**tcpdump** is a command-line network protocol analyzer, pre-installed on most Linux distributions and available on other Unix-based systems. Requires admin/sudo privileges to capture traffic. Encrypted traffic may need decryption (via the right private keys) before it's readable.

### Basic Syntax

```
sudo tcpdump [-i interface] [option(s)] [expression(s)]
```
- `-i` specifies the interface to capture from (`-i any` captures from all interfaces)
- `-D` lists available interfaces

### Key Options (Flags)

| Flag | Meaning | Example |
|---|---|---|
| `-w` | Write/save captured packets to a file | `sudo tcpdump -i any -w packetcapture.pcap` |
| `-r` | Read from a saved capture file | `sudo tcpdump -r packetcapture.pcap` |
| `-v` / `-vv` / `-vvv` | Verbose output — more detail with each added `v` | `sudo tcpdump -r packetcapture.pcap -v` |
| `-c` | Capture only a set number of packets | `sudo tcpdump -i any -c 3` |
| `-n` / `-nn` | Disable name resolution (`-n` = no hostname resolution, `-nn` = no hostname *or* port resolution) — best practice, since resolving an attacker's hostname via reverse DNS can tip them off that they're being investigated | `sudo tcpdump -r packetcapture.pcap -v -n` |

> Short options (`-i`) can be written with or without a space before their value; long options use a double hyphen (`--interface`). Options are case-sensitive.

### Filter Expressions

Used to isolate specific traffic, e.g. `ip6` for IPv6-only traffic. Combine with boolean operators (`and`, `or`, `not`):

```
sudo tcpdump -r packetcapture.pcap -n 'ip and port 80'
```

Quotes ensure the full expression executes together; parentheses group/prioritize expressions:
```
ip and (port 80 or port 443)
```

### Interpreting Output

Each captured packet prints as one line, in order:
1. **Timestamp** (hours:minutes:seconds.fraction)
2. **Source IP**
3. **Source port**
4. **Destination IP**
5. **Destination port**

...followed by TCP connection details (flags, sequence numbers), plus any extra detail enabled by `-v`.

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 6 — Sound the Alarm: Detection and Response*
