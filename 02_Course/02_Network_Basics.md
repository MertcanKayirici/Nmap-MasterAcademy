# Nmap Master Academy

# Course 02

# Network Basics

---

## Course Information

**Course Number:** 02

**Difficulty:** Beginner

**Estimated Reading Time:** 60–90 Minutes

**Prerequisites:** Course 01 – Introduction to Nmap

---

# Table of Contents

1. Why Networking Matters
2. Computer Networks
3. Types of Networks
4. The OSI Model
5. The TCP/IP Model
6. Data Encapsulation
7. IP Addresses
8. MAC Addresses
9. ARP
10. DNS
11. Routers and Switches
12. Packets, Frames and Segments
13. Ports and Sockets
14. Summary

---

# 1. Why Networking Matters

Nmap is fundamentally a networking tool.

It does not exploit systems, crack passwords, or modify files. Instead, it communicates with remote devices using network protocols and analyzes their responses.

Without understanding how computer networks operate, it is difficult to understand why Nmap behaves the way it does.

Every Nmap scan is simply a conversation between two computers.

```text
Your Computer
      │
      │ Packets
      ▼
Target System
      ▲
      │ Responses
      │
```

Understanding these packets is the foundation of network scanning.

---

# 2. Computer Networks

A computer network is a collection of devices connected together to exchange information.

Examples include:

- Home Wi-Fi
- Office Networks
- University Networks
- Data Centers
- Cloud Infrastructure
- The Internet

Common network devices include:

- Computers
- Servers
- Smartphones
- Routers
- Switches
- Printers
- Firewalls
- IoT Devices

---

# 3. Types of Networks

## LAN (Local Area Network)

A LAN connects devices within a limited geographic area.

Examples:

- Home network
- School laboratory
- Office floor

Advantages

- High speed
- Low latency
- Easy management

---

## WAN (Wide Area Network)

A WAN connects multiple LANs over large distances.

Example:

```text
Office A
     │
Internet
     │
Office B
```

The Internet itself is the largest WAN.

---

## MAN (Metropolitan Area Network)

A MAN covers a city or metropolitan area.

Example:

A university connecting multiple campuses within one city.

---

## PAN (Personal Area Network)

A PAN connects personal devices.

Examples:

- Bluetooth headset
- Smartwatch
- Wireless keyboard

---

# 4. The OSI Model

The OSI Model divides network communication into seven layers.

```text
+---------------------------+
| 7. Application            |
+---------------------------+
| 6. Presentation           |
+---------------------------+
| 5. Session                |
+---------------------------+
| 4. Transport              |
+---------------------------+
| 3. Network                |
+---------------------------+
| 2. Data Link              |
+---------------------------+
| 1. Physical               |
+---------------------------+
```

Each layer has a specific responsibility.

---

## Layer 7 – Application

Responsible for communication between applications.

Examples:

- HTTP
- HTTPS
- FTP
- DNS
- SMTP

---

## Layer 6 – Presentation

Responsible for:

- Encryption
- Compression
- Data formatting

Examples:

- TLS
- SSL
- JPEG
- UTF-8

---

## Layer 5 – Session

Responsible for:

- Session establishment
- Session maintenance
- Session termination

---

## Layer 4 – Transport

Responsible for reliable communication.

Protocols:

- TCP
- UDP

This is one of the most important layers for Nmap.

---

## Layer 3 – Network

Responsible for logical addressing.

Protocols:

- IPv4
- IPv6
- ICMP

Routers operate here.

---

## Layer 2 – Data Link

Responsible for communication inside a local network.

Examples:

- Ethernet
- Wi-Fi

MAC addresses belong here.

---

## Layer 1 – Physical

Responsible for transmitting electrical or optical signals.

Examples:

- Copper cables
- Fiber optics
- Radio signals

---

# 5. The TCP/IP Model

Modern networks primarily use the TCP/IP model.

```text
Application

Transport

Internet

Network Access
```

Comparison

| OSI | TCP/IP |
|------|---------|
| Application | Application |
| Presentation | Application |
| Session | Application |
| Transport | Transport |
| Network | Internet |
| Data Link | Network Access |
| Physical | Network Access |

---

# 6. Data Encapsulation

When data travels across a network, each layer adds its own header.

```text
Application Data
      │
      ▼
TCP Header
      │
      ▼
IP Header
      │
      ▼
Ethernet Header
      │
      ▼
Bits on the Wire
```

The receiving device removes these headers in reverse order.

---

# 7. IP Addresses

An IP address uniquely identifies a device on a network.

Example IPv4

```text
192.168.1.10
```

Example IPv6

```text
2001:db8::1
```

Types:

- Public
- Private
- Static
- Dynamic

---

## Private IPv4 Ranges

| Range | CIDR |
|--------|------|
| 10.0.0.0 | /8 |
| 172.16.0.0 | /12 |
| 192.168.0.0 | /16 |

These addresses are not routable on the public Internet.

---

# 8. MAC Addresses

Every network interface has a unique hardware address.

Example

```text
00:1A:2B:3C:4D:5E
```

Characteristics

- Layer 2 identifier
- Assigned to network interfaces
- Used inside local networks

Nmap uses MAC addresses during ARP discovery.

---

# 9. ARP (Address Resolution Protocol)

ARP maps an IP address to a MAC address.

Example:

```text
Who has 192.168.1.10?

↓

192.168.1.10 is at

00:1A:2B:3C:4D:5E
```

This process enables devices on the same LAN to communicate.

---

# 10. DNS (Domain Name System)

DNS translates human-readable names into IP addresses.

Example

```text
google.com

↓

142.250.x.x
```

Without DNS, users would have to remember IP addresses instead of names.

---

# 11. Routers and Switches

## Switch

- Operates at Layer 2
- Uses MAC addresses
- Connects devices within a LAN

---

## Router

- Operates at Layer 3
- Uses IP addresses
- Connects different networks

---

# 12. Packets, Frames and Segments

These terms describe data units at different layers.

| Layer | Unit |
|--------|------|
| Application | Data |
| Transport | Segment (TCP) / Datagram (UDP) |
| Network | Packet |
| Data Link | Frame |
| Physical | Bits |

---

# 13. Ports and Sockets

A port identifies a specific service running on a device.

Examples

| Port | Service |
|------|----------|
| 22 | SSH |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |

A socket is the combination of:

```text
IP Address

+

Port Number
```

Example

```text
192.168.1.20:443
```

This uniquely identifies one communication endpoint.

---

# Summary

You have learned:

- Why networking is essential for Nmap
- Types of computer networks
- The OSI model
- The TCP/IP model
- Encapsulation
- IP addressing
- MAC addressing
- ARP
- DNS
- Routers
- Switches
- Packets
- Frames
- Segments
- Ports
- Sockets

These concepts form the foundation for understanding how Nmap discovers hosts, scans ports, and identifies services.

---

# Key Takeaways

✓ Nmap communicates using standard network protocols.

✓ Every scan consists of network packets.

✓ TCP/IP is the foundation of modern networking.

✓ IP addresses identify hosts.

✓ MAC addresses identify network interfaces.

✓ Ports identify applications.

✓ Understanding networking fundamentals makes Nmap output much easier to interpret.

---

# Next Course

## Course 03

**Ports**