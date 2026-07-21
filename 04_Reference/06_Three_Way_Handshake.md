# Three-Way Handshake

> Quick Reference for Network Engineers, Penetration Testers, SOC Analysts, and Nmap Users.

---

# Overview

The TCP Three-Way Handshake is the process used to establish a reliable connection between a client and a server before any application data is transmitted.

This mechanism synchronizes sequence numbers, confirms that both hosts are reachable, and prepares both sides for reliable communication.

---

# Purpose

The Three-Way Handshake is responsible for:

- Establishing a TCP connection
- Synchronizing sequence numbers
- Confirming bidirectional communication
- Negotiating connection parameters
- Preparing both hosts for reliable data transfer

---

# The Three Steps

## Step 1 — SYN

The client initiates the connection by sending a TCP packet with the **SYN** flag set.

```text
Client -------------------- SYN --------------------► Server
```

Purpose:

- Request a new TCP connection.
- Advertise the client's initial sequence number.

---

## Step 2 — SYN-ACK

The server acknowledges the client's request and responds with both the **SYN** and **ACK** flags.

```text
Client ◄---------------- SYN-ACK ------------------- Server
```

Purpose:

- Confirm receipt of the client's SYN.
- Send the server's own initial sequence number.

---

## Step 3 — ACK

The client acknowledges the server's response.

```text
Client -------------------- ACK --------------------► Server
```

Purpose:

- Confirm receipt of the server's SYN.
- Complete the connection establishment.

---

# Complete Flow

```text
Client                                      Server

   SYN ------------------------------->

       <----------------------- SYN-ACK

   ACK ------------------------------->

============ Connection Established ============
```

---

# Sequence Number Example

```text
Client ISN = 1000

Client ---- SYN (Seq=1000) ----------->

Server ISN = 5000

Server <-- SYN ACK (Seq=5000 Ack=1001)

Client ---- ACK (Seq=1001 Ack=5001) -->
```

---

# Why Three Steps?

Three messages are required to ensure:

- Both hosts are online.
- Both hosts can send data.
- Both hosts can receive data.
- Sequence numbers are synchronized.
- Duplicate or delayed packets are avoided.

---

# After the Handshake

Once the handshake completes:

- Data transfer begins.
- ACK is present on nearly every TCP segment.
- Reliability mechanisms become active.
- Flow control and congestion control are enforced.

---

# Connection Termination

TCP closes connections using a separate **Four-Way Handshake**.

```text
Client

FIN ---------------------------->

        <---------------- ACK

        <---------------- FIN

ACK ---------------------------->

Connection Closed
```

---

# Wireshark Example

Typical packet order:

```text
1  SYN
2  SYN, ACK
3  ACK
4  Application Data
5  ACK
```

Useful display filter:

```text
tcp.flags.syn == 1
```

---

# Nmap Perspective

Nmap uses the TCP handshake differently depending on the scan type.

## SYN Scan

```bash
nmap -sS target
```

- Sends a SYN packet.
- Receives SYN-ACK if the port is open.
- Sends RST instead of completing the handshake.
- Faster and stealthier than a full connection.

---

## TCP Connect Scan

```bash
nmap -sT target
```

- Completes the full three-way handshake.
- Uses the operating system's networking stack.
- Easier to detect by security devices.

---

# Common Problems

The handshake may fail because of:

- Firewall rules
- Closed ports
- Network congestion
- Packet loss
- Incorrect routing
- Host unavailable

---

# Security Considerations

The handshake is commonly abused in network attacks.

Examples include:

- SYN Flood attacks
- Half-open connection attacks
- TCP spoofing
- Session hijacking attempts

Firewalls and IDS/IPS solutions often monitor handshake behavior to detect anomalies.

---

# Key Takeaways

- TCP requires a Three-Way Handshake before data transmission.
- The handshake uses the SYN, SYN-ACK, and ACK flags.
- It establishes a reliable bidirectional connection.
- Sequence numbers are synchronized during the process.
- Nmap SYN scans intentionally avoid completing the handshake.
- TCP Connect scans perform the full handshake.

---

# Related References

- TCP vs UDP
- TCP Flags
- Port Scanning
- Nmap Scan Types
- Common Network Services