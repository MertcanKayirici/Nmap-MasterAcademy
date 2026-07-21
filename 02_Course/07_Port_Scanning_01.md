# Nmap Master Academy

# Course 07

# Port Scanning

---

## Course Information

**Course Number:** 07

**Difficulty:** Intermediate → Advanced

**Estimated Reading Time:** 120–180 Minutes

**Prerequisites**

- Course 01 – Introduction
- Course 02 – Network Basics
- Course 03 – Ports
- Course 04 – TCP
- Course 05 – UDP
- Course 06 – Host Discovery

---

# Table of Contents

1. What is Port Scanning?
2. Why Port Scanning Matters
3. The Port Scanning Process
4. Understanding Port States
5. TCP Connect Scan (-sT)
6. TCP SYN Scan (-sS)
7. UDP Scan (-sU)
8. TCP ACK Scan (-sA)
9. TCP Window Scan (-sW)
10. TCP FIN Scan (-sF)
11. TCP NULL Scan (-sN)
12. TCP Xmas Scan (-sX)
13. TCP Maimon Scan (-sM)
14. Idle Scan (-sI)
15. SCTP Scans
16. IP Protocol Scan (-sO)
17. Choosing the Right Scan
18. Best Practices
19. Summary

---

# 1. What is Port Scanning?

Port scanning is the process of determining which network ports are accessible on a target system.

The goal is to identify:

- Running services
- Accessible applications
- Exposed attack surfaces
- Security misconfigurations

Every service reachable over a network listens on one or more ports.

---

## Example

Suppose a server has the following services:

```text
22/tcp   SSH

80/tcp   HTTP

443/tcp  HTTPS

3306/tcp MySQL
```

A port scan allows us to discover these services without logging into the system.

---

# 2. Why Port Scanning Matters

Port scanning is one of the first steps in almost every penetration test.

It helps answer questions such as:

- Which services are exposed?
- Which applications are accessible?
- Are unnecessary ports open?
- Which services may contain vulnerabilities?

Without port scanning, it is difficult to understand the attack surface of a target.

---

# 3. The Port Scanning Process

A simplified Nmap workflow looks like this:

```text
Target

↓

Host Discovery

↓

Send Probe Packet

↓

Receive Response

↓

Analyze Response

↓

Determine Port State

↓

Generate Report
```

Each scan type uses different probe packets and interprets responses differently.

---

# 4. Understanding Port States

Nmap reports six primary port states.

| State | Meaning |
|--------|---------|
| open | A service is actively accepting connections. |
| closed | The host is reachable, but no service is listening on the port. |
| filtered | A firewall or packet filter prevented Nmap from determining the port state. |
| unfiltered | The port is reachable, but its exact state cannot be determined. |
| open\|filtered | Nmap cannot distinguish whether the port is open or filtered. |
| closed\|filtered | Nmap cannot distinguish whether the port is closed or filtered (rare). |

---

## Open

```text
Nmap

↓

SYN

↓

Target

↓

SYN-ACK
```

Result:

```
open
```

---

## Closed

```text
Nmap

↓

SYN

↓

Target

↓

RST
```

Result:

```
closed
```

---

## Filtered

```text
Nmap

↓

SYN

↓

Firewall

↓

Blocked
```

Result:

```
filtered
```

---

# 5. TCP Connect Scan (-sT)

TCP Connect Scan uses the operating system's networking API to establish a full TCP connection.

Command:

```bash
nmap -sT 192.168.1.10
```

Connection flow:

```text
Client              Server

SYN  ------------->

      <----------- SYN-ACK

ACK  ------------->

Connection Established
```

After the connection is established, Nmap immediately closes it.

---

## Advantages

✓ Works without administrative privileges.

✓ Highly reliable.

✓ Supported on almost every operating system.

---

## Disadvantages

✗ Easily logged by servers.

✗ Generates more network traffic.

✗ Slower than SYN scanning.

---

# 6. TCP SYN Scan (-sS)

Also known as:

Half-Open Scan

Stealth Scan

This is Nmap's default scan for privileged users.

Command:

```bash
sudo nmap -sS 192.168.1.10
```

Workflow:

```text
Client               Server

SYN  ------------->

      <----------- SYN-ACK

RST  ------------->
```

Unlike Connect Scan, the TCP handshake is never completed.

---

## Advantages

✓ Faster.

✓ Generates less traffic.

✓ Often less visible in logs.

✓ Preferred by penetration testers.

---

## Disadvantages

Requires raw packet privileges.

---

# SYN Scan Response Interpretation

| Response | Result |
|----------|--------|
| SYN-ACK | Open |
| RST | Closed |
| No Response | Filtered |
| ICMP Error | Filtered |

---

# Comparison

| Feature | Connect | SYN |
|---------|---------|-----|
| Completes Handshake | Yes | No |
| Privileges Required | No | Yes |
| Speed | Medium | Fast |
| Logging | High | Lower |

---

# Coming Next

The following sections will explain:

- UDP Scan (-sU)
- ACK Scan (-sA)
- Window Scan (-sW)
- FIN Scan (-sF)
- NULL Scan (-sN)
- Xmas Scan (-sX)
- Maimon Scan (-sM)
- Idle Scan (-sI)
- SCTP Scans
- IP Protocol Scan (-sO)

Each scan type will include:

- Theory
- Packet flow diagrams
- Advantages
- Disadvantages
- Detection methods
- Typical use cases
- Nmap commands
- Sample outputs
- Best practices

---

# Summary

Port scanning is the core capability of Nmap.

Different scan types exist because networks, firewalls, and operating systems respond differently to network probes.

Understanding how each scan works allows security professionals to choose the most effective technique for a given environment.

---

# Key Takeaways

✓ Port scanning identifies accessible services.

✓ SYN Scan is the preferred TCP scanning method.

✓ Connect Scan establishes a full TCP connection.

✓ Port states provide valuable information about target systems.

✓ Choosing the correct scan type improves accuracy and efficiency.

---

# Next Lesson

## UDP Scan (-sU)