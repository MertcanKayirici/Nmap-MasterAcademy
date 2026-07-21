# Nmap Master Academy

# Course 06

# Host Discovery

---

## Course Information

**Course Number:** 06

**Difficulty:** Intermediate

**Estimated Reading Time:** 90–120 Minutes

**Prerequisites**

- Course 01 – Introduction
- Course 02 – Network Basics
- Course 03 – Ports
- Course 04 – TCP
- Course 05 – UDP

---

# Table of Contents

1. What is Host Discovery?
2. Why Host Discovery Matters
3. Discovery Workflow
4. ARP Discovery
5. ICMP Discovery
6. TCP SYN Discovery
7. TCP ACK Discovery
8. UDP Discovery
9. SCTP Discovery
10. Disabling Host Discovery (-Pn)
11. Ping Scan (-sn)
12. Host Discovery Options
13. Choosing the Right Method
14. Real-World Examples
15. Best Practices
16. Summary

---

# 1. What is Host Discovery?

Host Discovery is the process of determining whether a target device is online before performing more detailed scans.

Instead of immediately scanning every port on every IP address, Nmap first checks whether the host is reachable.

Example:

```text
Network

↓

192.168.1.1

192.168.1.2

192.168.1.3

192.168.1.4

↓

Which systems are actually online?
```

Host Discovery answers this question.

---

# Why Is This Important?

Imagine scanning an entire /24 network.

```text
256 IP Addresses
```

If only 15 hosts are online, scanning all 256 hosts wastes time.

Host Discovery allows Nmap to focus only on active systems.

Benefits include:

- Faster scans
- Reduced network traffic
- Better accuracy
- Lower detection risk

---

# 2. Discovery Workflow

A simplified Nmap scan looks like this:

```text
Target List
      │
      ▼
Host Discovery
      │
      ▼
Live Hosts
      │
      ▼
Port Scan
      │
      ▼
Service Detection
      │
      ▼
OS Detection
      │
      ▼
Reporting
```

Host Discovery is usually the first active step.

---

# 3. Default Host Discovery

When no special options are provided, Nmap performs host discovery automatically.

Example:

```bash
nmap 192.168.1.10
```

Internally, Nmap chooses appropriate discovery methods depending on:

- Local network
- Remote network
- User privileges
- Target type

---

# 4. ARP Discovery

When scanning devices on the same local network, Nmap prefers ARP requests.

Why?

ARP is fast and highly reliable on Ethernet networks.

Example:

```text
Who has

192.168.1.20?

↓

192.168.1.20

is at

00:11:22:33:44:55
```

If the target responds, it is considered online.

Command:

```bash
nmap -PR 192.168.1.0/24
```

---

## Advantages

✓ Extremely fast

✓ Very reliable

✓ Works even if ICMP is blocked

---

## Limitations

Only works on the local Layer-2 network.

---

# 5. ICMP Discovery

ICMP is the classic "ping."

Example:

```text
Echo Request

↓

Target

↓

Echo Reply
```

Command:

```bash
nmap -PE 192.168.1.20
```

---

## Other ICMP Types

Nmap can also use:

```text
Timestamp Request

Address Mask Request
```

Commands:

```bash
-PP

-PM
```

---

# Advantages

Simple

Widely supported

Easy to interpret

---

# Limitations

Many organizations block ICMP.

Blocked ICMP does **not** necessarily mean the host is offline.

---

# 6. TCP SYN Discovery

Instead of sending ICMP packets, Nmap can send a TCP SYN packet to a specific port.

Example:

```text
SYN

↓

Port 80

↓

SYN-ACK

↓

Host Online
```

Command:

```bash
nmap -PS80 192.168.1.20
```

Multiple ports:

```bash
nmap -PS22,80,443
```

---

# Why Use SYN Discovery?

Many firewalls block ICMP but allow web traffic.

A SYN probe may succeed even when ping fails.

---

# 7. TCP ACK Discovery

ACK discovery works similarly but sends ACK packets.

Example:

```text
ACK

↓

Target

↓

RST

↓

Host Online
```

Command:

```bash
nmap -PA80
```

This method is useful in some filtered environments.

---

# 8. UDP Discovery

UDP probes can also determine whether a host exists.

Command:

```bash
nmap -PU53
```

Example:

```text
UDP Packet

↓

DNS Server

↓

UDP Reply

↓

Host Online
```

Because UDP responses are inconsistent, this method is generally slower.

---

# 9. SCTP Discovery

Nmap also supports SCTP discovery.

Command:

```bash
nmap -PY80
```

Although SCTP is uncommon, it is used in some telecommunications environments.

---

# 10. Disabling Host Discovery

Sometimes a firewall blocks all discovery probes.

You still want to scan the target.

Use:

```bash
nmap -Pn
```

Meaning:

```text
Assume

Target

is Online
```

Nmap skips host discovery and proceeds directly to port scanning.

---

# Advantages

Useful against restrictive firewalls.

---

# Disadvantages

Much slower.

Offline systems will still be scanned.

---

# 11. Ping Scan

If you only want to discover hosts without scanning ports:

```bash
nmap -sn 192.168.1.0/24
```

Example output:

```text
Nmap scan report for

192.168.1.10

Host is up.

Nmap scan report for

192.168.1.21

Host is up.
```

No port scan is performed.

---

# 12. Host Discovery Options

| Option | Description |
|---------|-------------|
| -sn | Ping scan only |
| -Pn | Skip host discovery |
| -PR | ARP discovery |
| -PE | ICMP Echo Request |
| -PP | ICMP Timestamp |
| -PM | ICMP Address Mask |
| -PS | TCP SYN discovery |
| -PA | TCP ACK discovery |
| -PU | UDP discovery |
| -PY | SCTP INIT discovery |

---

# 13. Choosing the Right Method

| Environment | Recommended Method |
|--------------|--------------------|
| Local LAN | ARP |
| Internet | ICMP |
| ICMP Blocked | TCP SYN |
| Web Server | TCP SYN 80/443 |
| Firewall Testing | TCP ACK |
| DNS Server | UDP 53 |
| Unknown Network | Combine Methods |

---

# 14. Real-World Examples

Discover live hosts:

```bash
nmap -sn 10.10.10.0/24
```

Skip discovery:

```bash
nmap -Pn 10.10.10.15
```

Use TCP SYN:

```bash
nmap -PS22,80,443 10.10.10.15
```

Use ARP:

```bash
nmap -PR 192.168.1.0/24
```

Use UDP:

```bash
nmap -PU53 192.168.1.20
```

---

# 15. Best Practices

✓ Use ARP on local networks.

✓ Do not rely solely on ICMP.

✓ Use -Pn only when necessary.

✓ Select ports likely to be open for TCP discovery.

✓ Combine discovery methods when scanning unknown environments.

---

# Summary

Host Discovery identifies which systems are online before more detailed scanning begins.

Different discovery methods are suited to different environments.

Choosing the correct technique improves scan speed, accuracy, and efficiency.

---

# Key Takeaways

✓ Host Discovery reduces unnecessary scanning.

✓ ARP is best for local networks.

✓ ICMP is simple but often filtered.

✓ TCP SYN discovery is effective against ICMP restrictions.

✓ -Pn skips discovery entirely.

✓ -sn performs discovery without scanning ports.

---

# Next Course

## Course 07

**Port Scanning**