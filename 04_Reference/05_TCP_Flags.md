# TCP Flags

> Quick Reference for Network Engineers, Penetration Testers, SOC Analysts, and Nmap Users.

---

# Overview

TCP uses control bits, commonly known as **TCP Flags**, to establish, manage, and terminate network connections.

Each TCP packet contains one or more flags that define its purpose during communication.

Understanding TCP flags is essential for:

- Packet analysis
- Wireshark investigations
- Nmap scan interpretation
- Firewall analysis
- Intrusion Detection Systems (IDS)
- Penetration testing

---

# TCP Header Location

```text
TCP Header

+----------------------------------------------------+
| Source Port | Destination Port                     |
+----------------------------------------------------+
| Sequence Number                                   |
+----------------------------------------------------+
| Acknowledgment Number                             |
+----------------------------------------------------+
| Header Length | Flags | Window Size               |
+----------------------------------------------------+
| Checksum | Urgent Pointer                         |
+----------------------------------------------------+
```

---

# Common TCP Flags

| Flag | Full Name | Purpose |
|------|-----------|---------|
| SYN | Synchronize | Starts a connection |
| ACK | Acknowledgment | Confirms received data |
| FIN | Finish | Gracefully closes a connection |
| RST | Reset | Immediately terminates a connection |
| PSH | Push | Delivers data immediately |
| URG | Urgent | Marks urgent data |
| ECE | ECN Echo | Congestion notification |
| CWR | Congestion Window Reduced | Confirms congestion handling |

---

# SYN

Purpose:

- Initiates a TCP connection.
- Starts the Three-Way Handshake.

Example:

```text
Client ───── SYN ─────► Server
```

Common Uses:

- Opening TCP sessions
- Nmap SYN Scan (-sS)

---

# ACK

Purpose:

- Confirms successful packet reception.
- Maintains established connections.

Example:

```text
Client ◄──── ACK ───── Server
```

Almost every packet after connection establishment contains the ACK flag.

---

# FIN

Purpose:

- Gracefully closes a TCP session.
- Allows remaining data to be transmitted before termination.

Example:

```text
Client ───── FIN ─────► Server
```

---

# RST

Purpose:

- Immediately terminates a connection.
- Indicates an unexpected or invalid connection state.

Example:

```text
Server ───── RST ─────► Client
```

Common causes:

- Closed port
- Firewall rejection
- Application crash

---

# PSH

Purpose:

- Requests immediate delivery of buffered data.
- Commonly used in interactive applications.

Examples:

- SSH
- Telnet
- Remote Desktop

---

# URG

Purpose:

- Indicates urgent data.
- Uses the Urgent Pointer field.

Today this flag is rarely used.

---

# ECE

Purpose:

- Indicates network congestion.
- Used with Explicit Congestion Notification (ECN).

---

# CWR

Purpose:

- Sent after receiving an ECE packet.
- Confirms congestion handling.

---

# Typical Connection

```text
Client

SYN ─────────────►

◄──────── SYN ACK

ACK ─────────────►

Connection Established
```

---

# Connection Termination

```text
Client

FIN ─────────────►

◄──────── ACK

◄──────── FIN

ACK ─────────────►

Connection Closed
```

---

# TCP Flags Used by Nmap

| Scan | Primary Flag |
|------|--------------|
| SYN Scan | SYN |
| Connect Scan | SYN / ACK |
| FIN Scan | FIN |
| NULL Scan | No Flags |
| Xmas Scan | FIN + PSH + URG |
| ACK Scan | ACK |
| Window Scan | ACK |
| Maimon Scan | FIN + ACK |

---

# Common Flag Combinations

| Flags | Meaning |
|--------|---------|
| SYN | Connection Request |
| SYN + ACK | Connection Accepted |
| ACK | Data Acknowledgment |
| FIN + ACK | Graceful Close |
| RST | Immediate Reset |
| PSH + ACK | Immediate Data Delivery |
| FIN + PSH + URG | Xmas Scan Packet |

---

# Wireshark Examples

Typical Display Filters

```text
tcp.flags.syn == 1
```

```text
tcp.flags.ack == 1
```

```text
tcp.flags.fin == 1
```

```text
tcp.flags.reset == 1
```

```text
tcp.flags.push == 1
```

---

# Security Considerations

Attackers frequently manipulate TCP flags for:

- Firewall evasion
- Port scanning
- Fingerprinting
- IDS evasion
- Reconnaissance

Security devices inspect TCP flags to detect suspicious traffic.

---

# Key Takeaways

- SYN starts connections.
- ACK acknowledges packets.
- FIN gracefully closes connections.
- RST immediately resets connections.
- PSH requests immediate delivery.
- URG marks urgent data.
- ECE and CWR support congestion control.
- Nmap heavily relies on TCP flags for advanced scan techniques.

---

# Related References

- TCP vs UDP
- Three-Way Handshake
- Common Network Services
- Port Scanning
- Nmap Scan Types