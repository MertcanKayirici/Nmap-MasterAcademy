# Nmap Master Academy

# Course 05

# UDP (User Datagram Protocol)

---

## Course Information

**Course Number:** 05

**Difficulty:** Beginner → Intermediate

**Estimated Reading Time:** 60–90 Minutes

**Prerequisites**

- Course 01 – Introduction
- Course 02 – Network Basics
- Course 03 – Ports
- Course 04 – TCP

---

# Table of Contents

1. What is UDP?
2. Why UDP Exists
3. TCP vs UDP
4. UDP Header
5. How UDP Communication Works
6. UDP Characteristics
7. Common UDP Services
8. Advantages and Disadvantages
9. Why UDP Scanning is Difficult
10. UDP in Nmap
11. Real-World Examples
12. Summary

---

# 1. What is UDP?

UDP (User Datagram Protocol) is a transport-layer protocol designed for fast, connectionless communication.

Unlike TCP, UDP does not establish a connection before sending data.

It simply sends packets to the destination without waiting for confirmation.

---

## Real-World Analogy

Imagine sending a postcard.

You place it in a mailbox.

You do not know:

- if it arrived
- when it arrived
- whether it was lost

UDP works in a similar way.

---

# 2. Why UDP Exists

TCP provides reliability.

However, reliability introduces overhead.

Some applications require speed rather than guaranteed delivery.

Examples include:

- Video streaming
- Voice calls
- Online gaming
- DNS queries

For these applications, losing one packet is usually better than waiting for retransmission.

---

# 3. TCP vs UDP

| Feature | TCP | UDP |
|----------|-----|-----|
| Connection | Yes | No |
| Reliable | Yes | No |
| Handshake | Yes | No |
| Ordering | Yes | No |
| Retransmission | Yes | No |
| Speed | Slower | Faster |
| Header Size | Larger | Smaller |

---

# 4. UDP Header

The UDP header is very small.

```text
+----------------------------------+
| Source Port | Destination Port   |
+----------------------------------+
| Length      | Checksum           |
+----------------------------------+
| Data                          |
+----------------------------------+
```

Header fields:

| Field | Description |
|--------|-------------|
| Source Port | Sender port |
| Destination Port | Receiver port |
| Length | Packet length |
| Checksum | Error detection |

Unlike TCP, there are:

- No sequence numbers
- No acknowledgments
- No flags
- No window size

---

# 5. How UDP Communication Works

UDP communication is straightforward.

```text
Client

    │

UDP Packet

    ▼

Server
```

The server may:

- reply
- ignore the packet
- discard the packet

There is no built-in mechanism to verify delivery.

---

# 6. UDP Characteristics

UDP is:

✓ Connectionless

✓ Fast

✓ Lightweight

✓ Low Overhead

✓ Unreliable

✓ Message-Oriented

Because UDP does not establish a session, communication begins immediately.

---

# 7. Common UDP Services

Many important Internet services rely on UDP.

| Port | Service |
|------|----------|
| 53 | DNS |
| 67 | DHCP Server |
| 68 | DHCP Client |
| 69 | TFTP |
| 123 | NTP |
| 161 | SNMP |
| 162 | SNMP Trap |
| 500 | ISAKMP |
| 514 | Syslog |
| 520 | RIP |

These services are commonly encountered during security assessments.

---

# 8. Advantages of UDP

Advantages include:

- Lower latency
- Faster communication
- Smaller packets
- Lower CPU usage
- Suitable for real-time applications

---

# 9. Disadvantages of UDP

UDP does not provide:

- Reliability
- Ordering
- Error recovery
- Congestion control
- Flow control

Applications must implement these features themselves if needed.

---

# 10. Why UDP Scanning is Difficult

UDP scanning is fundamentally different from TCP scanning.

With TCP:

```text
SYN

↓

SYN-ACK

↓

Open Port
```

With UDP:

```text
UDP Packet

↓

(No Response)
```

No response does **not** necessarily mean the port is open.

It may indicate:

- The port is open.
- A firewall silently dropped the packet.
- The application ignored the request.

---

## ICMP Responses

If a UDP port is closed, the target often returns an ICMP "Port Unreachable" message.

```text
UDP Packet

↓

ICMP Port Unreachable

↓

Closed Port
```

If no ICMP message is received, Nmap usually reports the port as:

```text
open|filtered
```

This means the scanner cannot determine whether the port is truly open or simply filtered.

---

# 11. UDP in Nmap

UDP scanning uses:

```bash
nmap -sU <target>
```

Example:

```bash
nmap -sU 192.168.1.10
```

Possible results:

| State | Meaning |
|--------|---------|
| open | Service responded |
| closed | ICMP Port Unreachable received |
| filtered | Firewall blocked traffic |
| open\|filtered | No definitive response |

Because UDP often receives no reply, scans are typically slower than TCP scans.

---

## Why UDP Scans Are Slow

Nmap must wait for possible responses.

Example workflow:

```text
Send UDP Packet

↓

Wait

↓

No Response

↓

Retry

↓

Wait Again

↓

Timeout
```

This waiting period increases scan duration.

---

# 12. Real-World Example

Suppose a DNS server is running on port 53.

```bash
nmap -sU -p 53 192.168.1.20
```

Possible output:

```text
53/udp open domain
```

Now consider an unused UDP port:

```bash
nmap -sU -p 9999 192.168.1.20
```

Possible output:

```text
9999/udp closed
```

Finally, if a firewall silently drops packets:

```text
9999/udp open|filtered
```

This is one of the most common UDP scan results.

---

# Best Practices

✓ Scan only required UDP ports.

✓ Combine UDP scans with service detection when appropriate.

✓ Be patient—UDP scans are slower by design.

✓ Interpret "open|filtered" carefully.

✓ Remember that lack of response is not proof of an open port.

---

# Summary

In this course, you learned:

- What UDP is
- Why UDP exists
- Differences between TCP and UDP
- UDP header structure
- Connectionless communication
- Common UDP services
- Advantages and disadvantages
- Why UDP scanning is challenging
- How Nmap performs UDP scans
- Why "open|filtered" is common

Understanding UDP behavior is essential for interpreting UDP scan results accurately.

---

# Key Takeaways

✓ UDP is connectionless.

✓ UDP prioritizes speed over reliability.

✓ No handshake is required.

✓ No response does not always mean an open port.

✓ ICMP messages play a key role in UDP scanning.

✓ UDP scans are generally slower than TCP scans.

---

# Next Course

## Course 06

**Host Discovery**