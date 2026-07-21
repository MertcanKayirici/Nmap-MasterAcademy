# ASCII Diagrams

> Quick ASCII reference diagrams for networking, TCP/IP, and Nmap.

---

# OSI Model

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

---

# TCP/IP Model

```text
+---------------------------+
| Application               |
+---------------------------+
| Transport                 |
+---------------------------+
| Internet                  |
+---------------------------+
| Network Access            |
+---------------------------+
```

---

# TCP Three-Way Handshake

```text
Client                           Server

SYN ---------------------------->

      <---------------- SYN ACK

ACK ---------------------------->

========= Connection Established =========
```

---

# TCP Four-Way Termination

```text
Client                           Server

FIN ---------------------------->

      <---------------- ACK

      <---------------- FIN

ACK ---------------------------->

========== Connection Closed ==========
```

---

# TCP Data Transfer

```text
Client                           Server

DATA --------------------------->

      <---------------- ACK

DATA --------------------------->

      <---------------- ACK
```

---

# UDP Communication

```text
Client                           Server

DATA --------------------------->
```

No connection.

No acknowledgment.

No retransmission.

---

# TCP vs UDP

```text
TCP

Connect
   │
Handshake
   │
Reliable
   │
Ordered
   │
ACK
   │
Retransmission

UDP

Send
 │
Done
 │
Fast
 │
Lightweight
 │
No ACK
 │
No Retransmission
```

---

# TCP Flags

```text
SYN  -> Start Connection

ACK  -> Acknowledge Data

FIN  -> Graceful Close

RST  -> Immediate Reset

PSH  -> Deliver Immediately

URG  -> Urgent Data

ECE  -> Congestion Notification

CWR  -> Congestion Response
```

---

# Nmap SYN Scan

```text
Scanner                     Target

SYN ------------------------>

      <--------------- SYN ACK

RST ------------------------>

Port Open
```

---

# Nmap Connect Scan

```text
Scanner                     Target

SYN ------------------------>

      <--------------- SYN ACK

ACK ------------------------>

Connection Established

FIN ------------------------>

Connection Closed
```

---

# Closed Port

```text
Scanner                     Target

SYN ------------------------>

      <---------------- RST
```

---

# Filtered Port

```text
Scanner                     Firewall

SYN ------------------------>

      X

No Response
```

---

# TCP Header

```text
+------------------------------------------------------+
| Source Port | Destination Port                       |
+------------------------------------------------------+
| Sequence Number                                     |
+------------------------------------------------------+
| Acknowledgment Number                               |
+------------------------------------------------------+
| Offset | Flags | Window                             |
+------------------------------------------------------+
| Checksum | Urgent Pointer                           |
+------------------------------------------------------+
| Options                                              |
+------------------------------------------------------+
```

---

# UDP Header

```text
+--------------------------------------+
| Source Port | Destination Port       |
+--------------------------------------+
| Length      | Checksum               |
+--------------------------------------+
```

---

# Packet Flow

```text
Application

↓

TCP / UDP

↓

IP

↓

Ethernet

↓

Physical Network

↓

Destination
```

---

# Nmap Workflow

```text
Target

↓

Host Discovery

↓

Port Scan

↓

Service Detection

↓

OS Detection

↓

NSE Scripts

↓

Report
```

---

# Common Port States

```text
OPEN

Scanner <------ Service


CLOSED

Scanner <------ RST


FILTERED

Scanner ----X---- Firewall


OPEN|FILTERED

Scanner ------ ?

No definitive response
```

---

# Scan Progress

```text
Discovery

↓

Scan

↓

Detect

↓

Analyze

↓

Report
```

---

# Related References

- TCP vs UDP
- TCP Flags
- Three-Way Handshake
- Common Network Services
- Top 100 Ports
- Top 1000 Ports