# Module 1: Network Architecture

## What Is a Network?

A **network** is a collection of connected devices. Devices can communicate over either physical or wireless connections.

| Type | Scope |
|---|---|
| **LAN** (Local Area Network) | A small, confined area — home, office, or school |
| **WAN** (Wide Area Network) | A large geographical region — a city, state, or entire country |

## Network Devices

| Device | Function | Security Note |
|---|---|---|
| **Hub** | Broadcasts information to *every* connected device | Vulnerable to eavesdropping since all traffic is broadcast |
| **Switch** | Sends data only to the intended recipient, using a MAC address table matching devices to port numbers | More secure than a hub — traffic isn't broadcast everywhere |
| **Router** | Connects networks and directs traffic based on the destination's IP address | — |
| **Modem** | Connects a router to the internet, enabling internet access for a LAN | — |
| **Wireless Access Point** | Sends/receives digital signals over radio waves, creating a wireless network | — |
| **Firewall** | Monitors traffic to/from the network | First line of defense |
| **Server** | Provides information/services to devices (called *clients*) | Common examples: DNS server, file server, mail server |

## Virtualization Tools

**Software-based network operations** — offered by cloud service providers, these perform the same functions as physical hubs/switches/routers/modems, but via software instead of dedicated hardware. Benefits: **flexibility, scalability, cost savings, simplified management.**

## Network Diagrams

Maps showing devices on a network and how they connect. Security analysts use them to develop and refine network security strategies by:
- **Spotting unauthorized devices** — a possible sign of a breach
- **Identifying critical assets** — devices holding sensitive data or critical functions, for prioritized protection
- **Analyzing traffic flow** — revealing potential choke points or interception risks
- **Pinpointing single points of failure** — devices/connections that could take down a large part of the network if compromised
- **Assessing firewall placement** — confirming firewalls are protecting the right areas
- **Detecting misconfigurations** — e.g., a server directly exposed to the internet with no firewall

## Cloud Networks

**Cloud computing** — using remote servers/applications hosted on the internet, removing the need for local physical devices. Data/resources live in remote data centers rather than on-site.

### Key Areas for Cloud Security

- **IAM (Identity and Access Management)** — verifying who accesses what, with strong authentication and regular access reviews
- **Data encryption** — both in transit and at rest
- **Network security controls** — firewalls, IDS/IPS, and VPNs designed for cloud environments
- **Regular audits and monitoring** — continuously watching for suspicious activity
- **Compliance and governance** — aligning cloud practices with regulations/data protection laws
- **Employee training** — reducing human error as a breach vector

### Cloud Service Providers (CSPs)

A **CSP** owns large global data centers housing millions of servers, offering three main service categories:

| Service Model | What You Get | Who Manages What |
|---|---|---|
| **SaaS** (Software as a Service) | Ready-to-use software, hosted and managed remotely | Provider manages everything; you just use the app |
| **IaaS** (Infrastructure as a Service) | Virtual computing resources (servers, storage, networks) via API/console | You manage OS, applications, and data; provider manages hardware |
| **PaaS** (Platform as a Service) | A complete environment for developing/running/managing applications | Provider manages infrastructure; you focus purely on writing code |

**Hybrid cloud environment** — when an organization uses both a CSP's services *and* its own on-premise computers/networks/storage.

**Software-Defined Networks (SDNs)** — made up of virtual network devices and services; just as CSPs provide virtual computers, SDNs provide virtual switches, routers, firewalls, etc.

> Cloud computing and SDNs appeal to businesses for three main reasons: **reliability, decreased cost, and increased scalability.**

## Network Communication Basics

- **Data packet** — the basic unit of information transferred across a network; contains origin, destination, and content. Structure: header (IP + MAC addresses), protocol number, message body, footer.
- **Bandwidth** — amount of data a device receives per second (data quantity ÷ time)
- **Speed** — the rate at which data packets are received/downloaded

> Irregularities in bandwidth or speed can be a sign of a potential attack — worth monitoring as a security metric.

## The TCP/IP Model

- **TCP (Transmission Control Protocol)** — enables two devices to establish a connection and stream data
- **IP (Internet Protocol)** — defines standards for routing/addressing data packets between devices
- **Port numbers** — software-based locations organizing data transmission/reception (e.g., port 25 = email, port 443 = secure internet communication, port 20 = large file transfers)

### The Four TCP/IP Layers

| Layer | Also Called | Function | Example |
|---|---|---|---|
| **4. Application** | — | High-level protocols, user interface, session control | DNS lookups, HTTP/HTTPS web traffic |
| **3. Transport** | — | Host-to-host delivery, sequencing, error checking (TCP/UDP) | UDP streaming live video where speed > reliability |
| **2. Internet** | Network layer | Packages data into IP datagrams and routes across networks | IPv4/IPv6 routing packets across the internet |
| **1. Network Access** | Data link layer | Interfaces with physical media and local hardware addressing | A Wi-Fi card sending frames to a local access point |

**Protocols at the Internet layer:**
- **IP** — sends packets to the correct destination, relying on TCP/UDP for final delivery
- **ICMP** — shares error info/status updates (dropped packets, connectivity issues, redirected packets) — useful for troubleshooting

**Protocols at the Transport layer:**
- **TCP** — connection-based, reliable delivery; contains the destination port number in its header
- **UDP** — connectionless, no guaranteed delivery; used for real-time/performance-sensitive apps like video streaming

**Common Application layer protocols:** HTTP, SMTP, SSH, FTP, DNS

## The OSI Model (7 Layers)

A standardized concept describing the seven layers computers use to communicate over a network.

| Layer | Name | Function | Example |
|---|---|---|---|
| **7** | Application | Direct interface for user-facing network services | HTTP loading a webpage |
| **6** | Presentation | Translates, encrypts, compresses data for the application layer | SSL/TLS encrypting credit card info during checkout |
| **5** | Session | Opens, manages, and closes communication sessions (auth, reconnection, checkpoints) | NetBIOS or RPC maintaining a login session |
| **4** | Transport | Delivers data between devices; handles speed, flow, segmentation | TCP guaranteeing a file download arrives complete |
| **3** | Network | Logical addressing and routing packets across networks | IP routing a packet from your router to a server |
| **2** | Data Link | Node-to-node delivery and error correction via physical (MAC) addresses; home to switches and NICs | Ethernet/Wi-Fi using MAC addresses on a local network |
| **1** | Physical | Transmits raw binary bits over physical media | Ethernet cables, fiber optic cables, radio waves |

> **Segmentation** — dividing a large data transmission into smaller pieces for easier transport; these segments are reassembled at the destination.

**Note on layer mapping:** the TCP/IP model's 4 layers essentially group the OSI model's 7 layers — TCP/IP's Application layer = OSI layers 5–7; TCP/IP's Transport layer = OSI layer 4; TCP/IP's Internet layer = OSI layer 3; TCP/IP's Network Access layer = OSI layers 1–2.

## IP Addresses and MAC Addresses

- **IP address** — a unique identifier for a device's location on the internet.
  - **IPv4** — four sets of 1–3 digit numbers separated by decimals
  - **IPv6** — uses 32 characters, built to accommodate far more devices
  - **Public IP** — assigned by the ISP, tied to geographic location; shared by all devices on a network for outward-facing traffic
  - **Private IP** — used for communication between devices on the same local network; not visible externally

- **MAC address** — a unique alphanumeric identifier assigned to each physical device on a network. Switches use MAC addresses (via a MAC address table) to direct packets to the correct device.

## Network Layer Operations

The network layer organizes addressing and delivery of packets from host to destination. Each packet's header includes the destination IP address, source IP address, packet size, and the protocol used for the data portion.

> A packet is also called an **IP packet** (TCP) or a **datagram** (UDP).

### IPv4 Packet Format

An IPv4 packet = **header** + **data**. Max packet size: 65,535 bytes. Header size: 20–60 bytes (first 20 bytes fixed; remaining 0–40 bytes are the options field).

**The 13 IPv4 header fields:**

| Field | Purpose |
|---|---|
| **Version (VER)** | Tells receiving devices which protocol the packet uses |
| **IP Header Length (HLEN/IHL)** | Indicates where the header ends and data begins |
| **Type of Service (ToS)** | Lets routers prioritize packets for quality of service |
| **Total Length** | Total length of the entire packet (header + data) |
| **Identification** | Unique ID for reassembling fragmented packets |
| **Flags** | Indicates if the packet is fragmented and if more fragments are coming |
| **Fragmentation Offset** | Tells routers where a fragment belongs in the original packet |
| **Time to Live (TTL)** | Counter decremented at each router hop; packet is discarded (with an ICMP error sent back) when it hits zero — prevents infinite forwarding |
| **Protocol** | Tells the receiving device which protocol handles the data portion |
| **Header Checksum** | Detects header corruption in transit; corrupted packets are discarded |
| **Source IP Address** | IPv4 address of the sending device |
| **Destination IP Address** | IPv4 address of the destination device |
| **Options** | Allows security options to be applied (when HLEN > 5) |

## Questions / Things to Revisit

- 

---
*Notes based on Google Cybersecurity Professional Certificate, Course 3 — Connect and Protect: Networks and Network Security*
