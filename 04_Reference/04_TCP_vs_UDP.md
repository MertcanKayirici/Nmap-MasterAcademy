# TCP vs UDP

> Quick Reference for Network Engineers, Penetration Testers, SOC Analysts, and Nmap Users.

---

# Overview

TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) are the two primary transport layer protocols in the TCP/IP suite.

Although both transport application data across networks, they differ significantly in reliability, speed, connection management, and intended use cases.

Understanding these differences is essential for network troubleshooting, penetration testing, firewall analysis, and Nmap scanning.

---

# Quick Comparison

| Feature | TCP | UDP |
|----------|-----|-----|
| Connection | Connection-Oriented | Connectionless |
| Reliability | Reliable | Best Effort |
| Packet Ordering | Guaranteed | Not Guaranteed |
| Error Checking | Yes | Basic Checksum |
| Retransmission | Yes | No |
| Flow Control | Yes | No |
| Congestion Control | Yes | No |
| Speed | Slower | Faster |
| Header Size | 20–60 Bytes | 8 Bytes |
| Broadcast Support | No | Yes |
| Streaming | Excellent | Limited |
| Typical Usage | Web, SSH, Email | DNS, VoIP, Streaming |

---

# TCP Communication

```text
Client
   │
SYN
   ▼
Server
   ▲
SYN ACK
   │
ACK
   ▼
Connection Established
```

---

# UDP Communication

```text
Client
   │
   ▼
UDP Packet
   ▼
Server
```

No connection setup.

---

# TCP Characteristics

- Reliable delivery
- Ordered packets
- Error recovery
- Retransmission
- Flow control
- Congestion control
- Connection-oriented

---

# UDP Characteristics

- Fast transmission
- Low overhead
- No retransmission
- No ordering
- No congestion control
- Connectionless

---

# Common TCP Services

| Port | Service |
|------|---------|
| 20/21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 80 | HTTP |
| 110 | POP3 |
| 143 | IMAP |
| 443 | HTTPS |
| 445 | SMB |
| 3389 | RDP |

---

# Common UDP Services

| Port | Service |
|------|---------|
| 53 | DNS |
| 67 | DHCP Server |
| 68 | DHCP Client |
| 69 | TFTP |
| 123 | NTP |
| 161 | SNMP |
| 162 | SNMP Trap |
| 500 | IKE |
| 514 | Syslog |
| 5060 | SIP |

---

# Nmap Scanning

TCP Scan

```bash
nmap -sS target
```

TCP Connect Scan

```bash
nmap -sT target
```

UDP Scan

```bash
nmap -sU target
```

TCP + UDP

```bash
nmap -sS -sU target
```

---

# Advantages

## TCP

- Reliable
- Ordered delivery
- Error recovery
- Suitable for critical applications

## UDP

- Fast
- Lightweight
- Low latency
- Ideal for real-time communication

---

# Disadvantages

## TCP

- Slower
- Higher overhead
- Connection setup required

## UDP

- Packet loss possible
- No ordering
- No retransmission

---

# When to Use

Use TCP when:

- Reliability is important
- File transfers
- Web applications
- Remote administration
- Database connections

Use UDP when:

- Speed matters
- Live streaming
- DNS queries
- Voice communication
- Online gaming

---

# Security Considerations

TCP

- SYN Flood
- Session Hijacking
- TCP Reset Attacks

UDP

- UDP Flood
- Amplification Attacks
- Reflection Attacks

---

# Summary

TCP prioritizes reliability, ordering, and guaranteed delivery, making it ideal for applications where data integrity is essential.

UDP prioritizes speed and low latency by eliminating connection setup and retransmissions, making it well suited for real-time applications where occasional packet loss is acceptable.

Understanding when each protocol is used helps analysts interpret Nmap scan results, troubleshoot network issues, and identify services more effectively.

---

# Header Comparison

## TCP Header

| Field | Purpose |
|--------|---------|
| Source Port | Sender port |
| Destination Port | Receiver port |
| Sequence Number | Packet ordering |
| Acknowledgment Number | Confirms received data |
| Data Offset | Header length |
| Flags | SYN, ACK, FIN, RST, PSH, URG |
| Window Size | Flow control |
| Checksum | Error detection |
| Urgent Pointer | Urgent data indicator |
| Options | MSS, Window Scaling, SACK, etc. |

---

## UDP Header

| Field | Purpose |
|--------|---------|
| Source Port | Sender port |
| Destination Port | Receiver port |
| Length | Datagram length |
| Checksum | Error detection |

UDP headers are significantly smaller than TCP headers, reducing overhead.

---

# Reliability Comparison

| Capability | TCP | UDP |
|------------|-----|-----|
| Guarantees Delivery | ✅ | ❌ |
| Packet Ordering | ✅ | ❌ |
| Duplicate Detection | ✅ | ❌ |
| Retransmission | ✅ | ❌ |
| Error Recovery | ✅ | ❌ |
| Low Latency | ❌ | ✅ |

---

# Performance Comparison

| Metric | TCP | UDP |
|--------|-----|-----|
| Speed | Medium | Very High |
| Reliability | Excellent | Low |
| Overhead | High | Very Low |
| Latency | Higher | Lower |
| Bandwidth Efficiency | Medium | High |

---

# Real-World Examples

## TCP Applications

- HTTP
- HTTPS
- SSH
- FTP
- SFTP
- SMB
- LDAP
- RDP
- SMTP
- IMAP
- POP3
- MySQL
- PostgreSQL

TCP is preferred whenever reliable delivery is required.

---

## UDP Applications

- DNS
- DHCP
- NTP
- SNMP
- SIP
- RTP
- TFTP
- Online Gaming
- Live Streaming
- Voice over IP (VoIP)

UDP is preferred whenever low latency is more important than perfect reliability.

---

# Nmap Perspective

TCP scanning is generally:

- Faster
- More accurate
- Easier to fingerprint
- More reliable

Example:

```bash
nmap -sS 192.168.1.10
```

---

UDP scanning is generally:

- Slower
- Less reliable
- More prone to filtered responses
- Requires additional verification

Example:

```bash
nmap -sU 192.168.1.10
```

---

# Firewall Behavior

## TCP

Firewalls commonly inspect:

- Connection state
- TCP Flags
- Session tracking
- Sequence numbers

Stateful firewalls are primarily designed around TCP connections.

---

## UDP

Since UDP has no connection state:

- Firewalls often rely on timeout values.
- Responses may be blocked more aggressively.
- UDP scanning often reports **open|filtered** instead of **open**.

---

# Packet Flow Comparison

## TCP

```text
Client
   │
   ├── SYN ─────────────►
   │◄──────────── SYN-ACK
   ├── ACK ─────────────►
   │
   ├── DATA ────────────►
   │◄──────────── ACK
   │
   ├── FIN ─────────────►
   │◄──────────── ACK
```

---

## UDP

```text
Client
   │
   ├── DATA ───────────►
   │
   (No ACK Required)
```

---

# Choosing Between TCP and UDP

Choose **TCP** when:

- Data integrity is critical.
- Every packet must arrive.
- Order must be preserved.
- The application can tolerate additional latency.

Choose **UDP** when:

- Low latency is critical.
- Small packet loss is acceptable.
- High throughput is required.
- Real-time communication is the priority.

---

# Key Takeaways

- TCP prioritizes reliability and accuracy.
- UDP prioritizes speed and efficiency.
- TCP uses a three-way handshake; UDP does not.
- TCP provides retransmission and ordering; UDP does not.
- Most enterprise services use TCP.
- Many real-time services use UDP.
- Nmap supports scanning both protocols using dedicated scan types.

---

# Related References

- TCP Flags
- Three-Way Handshake
- Top 100 Ports
- Top 1000 Ports
- Common Network Services
- Host Discovery
- Port Scanning