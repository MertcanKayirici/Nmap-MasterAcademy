# Nmap Master Academy

# Course 04

# TCP (Transmission Control Protocol)

---

## Course Information

**Course Number:** 04

**Difficulty:** Beginner → Intermediate

**Estimated Reading Time:** 90–120 Minutes

**Prerequisites**

- Course 01 – Introduction
- Course 02 – Network Basics
- Course 03 – Ports

---

# Table of Contents

1. What is TCP?
2. Why TCP Exists
3. TCP Characteristics
4. TCP Header
5. TCP Flags
6. Three-Way Handshake
7. Four-Way Termination
8. TCP Connection States
9. Flow Control
10. Congestion Control
11. Retransmission
12. TCP Sessions
13. TCP vs UDP
14. Why TCP Matters for Nmap
15. Summary

---

# 1. What is TCP?

TCP (Transmission Control Protocol) is a transport-layer protocol that provides reliable, ordered, and error-checked communication between two devices.

Unlike UDP, TCP guarantees that data arrives:

- Completely
- In the correct order
- Without duplication

It is one of the core protocols of the Internet.

---

## Real-World Analogy

Imagine sending a package through a courier service.

The courier:

- Confirms delivery
- Ensures nothing is missing
- Resends the package if necessary

TCP behaves in a similar way.

---

# 2. Why TCP Exists

Networks are unreliable.

Packets may:

- Be lost
- Arrive out of order
- Become corrupted
- Be duplicated

TCP solves these problems by introducing mechanisms such as:

- Sequence Numbers
- Acknowledgments
- Retransmissions
- Flow Control
- Congestion Control

---

# 3. TCP Characteristics

TCP is:

✓ Connection-Oriented

✓ Reliable

✓ Ordered

✓ Full-Duplex

✓ Error Checked

✓ Stream Based

Unlike UDP, communication begins by establishing a connection.

---

# 4. TCP Header

Every TCP packet contains a header.

Simplified structure:

```text
+------------------------------------------------------+
| Source Port          | Destination Port              |
+------------------------------------------------------+
| Sequence Number                                   |
+------------------------------------------------------+
| Acknowledgment Number                             |
+------------------------------------------------------+
| Header Length | Flags | Window Size                |
+------------------------------------------------------+
| Checksum | Urgent Pointer                          |
+------------------------------------------------------+
| Options (Optional)                                |
+------------------------------------------------------+
| Data                                              |
+------------------------------------------------------+
```

Important fields:

| Field | Purpose |
|--------|----------|
| Source Port | Sender application |
| Destination Port | Receiver application |
| Sequence Number | Packet ordering |
| Acknowledgment | Confirmation |
| Window Size | Flow control |
| Flags | Connection control |
| Checksum | Error detection |

---

# 5. TCP Flags

TCP uses control flags to manage connections.

The most common flags are:

| Flag | Name | Purpose |
|------|------|----------|
| SYN | Synchronize | Start a connection |
| ACK | Acknowledge | Confirm receipt |
| FIN | Finish | Gracefully close a connection |
| RST | Reset | Immediately terminate |
| PSH | Push | Deliver data immediately |
| URG | Urgent | Urgent data |
| ECE | ECN Echo | Congestion notification |
| CWR | Congestion Window Reduced | Congestion response |

---

## SYN

Starts a TCP connection.

Example:

```text
Client

↓

SYN

↓

Server
```

---

## ACK

Acknowledges received packets.

```text
Server

↓

ACK

↓

Client
```

---

## FIN

Gracefully ends a connection.

---

## RST

Immediately aborts the connection.

Nmap often receives RST packets from closed ports.

---

# 6. Three-Way Handshake

Before exchanging data, TCP establishes a connection.

```
Client                      Server

SYN  ---------------------->

     <-------------------  SYN + ACK

ACK  ---------------------->

Connection Established
```

Step 1

Client sends SYN.

Step 2

Server replies with SYN-ACK.

Step 3

Client sends ACK.

Only after these three steps can data be transmitted.

---

# Why Is This Important?

The famous Nmap SYN Scan (-sS) intentionally avoids completing this handshake.

Instead:

```
Client                   Server

SYN -------------------->

      <--------------- SYN-ACK

RST -------------------->

Connection Closed
```

This technique makes the scan faster and often less visible in logs.

---

# 7. Four-Way Termination

Closing a TCP connection usually requires four steps.

```
Client                     Server

FIN ---------------------->

      <---------------- ACK

      <---------------- FIN

ACK ---------------------->
```

The connection is then terminated cleanly.

---

# 8. TCP Connection States

During its lifetime, a TCP connection passes through several states.

Common states include:

```text
LISTEN

↓

SYN_SENT

↓

SYN_RECEIVED

↓

ESTABLISHED

↓

FIN_WAIT

↓

TIME_WAIT

↓

CLOSED
```

Nmap interacts with several of these states during scanning.

---

# 9. Flow Control

Flow Control prevents the sender from overwhelming the receiver.

TCP uses the Window Size field.

Example:

```
Receiver

"I can receive 4096 bytes."

↓

Sender

Sends no more than 4096 bytes before waiting.
```

---

# 10. Congestion Control

Networks can become congested.

TCP automatically adjusts its transmission rate.

Common algorithms include:

- Slow Start
- Congestion Avoidance
- Fast Retransmit
- Fast Recovery

Although Nmap transfers relatively little data, congestion can still influence scan speed.

---

# 11. Retransmission

If an acknowledgment is not received within a timeout period, TCP retransmits the packet.

```
Packet

↓

Lost

↓

Timeout

↓

Packet Sent Again
```

This mechanism improves reliability but may also slow communication.

---

# 12. TCP Sessions

A TCP session is uniquely identified by four values.

```
Source IP

Source Port

Destination IP

Destination Port
```

Example:

```
192.168.1.10:52341

↓

192.168.1.20:443
```

This combination uniquely identifies a connection.

---

# 13. TCP vs UDP

| Feature | TCP | UDP |
|----------|-----|-----|
| Reliable | ✓ | ✗ |
| Connection | Yes | No |
| Ordering | Yes | No |
| Speed | Slower | Faster |
| Retransmission | Yes | No |
| Handshake | Yes | No |
| Streaming | Yes | Limited |

---

# 14. Why TCP Matters for Nmap

Most Nmap scan types rely on TCP behavior.

Examples include:

- SYN Scan
- Connect Scan
- ACK Scan
- FIN Scan
- NULL Scan
- Xmas Scan
- Window Scan
- Maimon Scan

Understanding TCP allows you to interpret scan results instead of simply memorizing commands.

For example:

A SYN-ACK response often indicates an open port.

A RST response usually indicates a closed port.

No response may suggest filtering by a firewall.

---

# Summary

In this course, you learned:

- What TCP is
- Why it exists
- TCP characteristics
- TCP header fields
- TCP flags
- Three-way handshake
- Four-way termination
- Connection states
- Flow control
- Congestion control
- Retransmission
- TCP sessions
- Why TCP is essential for Nmap

A solid understanding of TCP is one of the most important prerequisites for mastering network scanning.

---

# Key Takeaways

✓ TCP is reliable and connection-oriented.

✓ Every TCP connection begins with a three-way handshake.

✓ TCP flags control communication.

✓ SYN and ACK packets play a central role in Nmap scanning.

✓ Nmap leverages TCP behavior to determine whether ports are open, closed, or filtered.

✓ Understanding TCP makes advanced scan types much easier to learn.

---

# Next Course

## Course 05

**UDP**