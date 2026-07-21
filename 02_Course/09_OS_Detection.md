# Nmap Master Academy

# Course 09

# Operating System Detection

---

## Course Information

**Course Number:** 09

**Difficulty:** Intermediate → Advanced

**Estimated Reading Time:** 90–120 Minutes

**Prerequisites**

- Course 01 – Introduction
- Course 02 – Network Basics
- Course 03 – Ports
- Course 04 – TCP
- Course 05 – UDP
- Course 06 – Host Discovery
- Course 07 – Port Scanning
- Course 08 – Service Detection

---

# Table of Contents

1. What is Operating System Detection?
2. Why OS Detection Matters
3. How Nmap Detects Operating Systems
4. TCP/IP Fingerprinting
5. Active Fingerprinting
6. OS Detection (-O)
7. OS Guessing
8. Device Type Detection
9. Accuracy and Limitations
10. Firewall Effects
11. Real-World Examples
12. Best Practices
13. Summary

---

# 1. What is Operating System Detection?

After discovering a host and identifying its services, one important question remains:

**Which operating system is running?**

Operating System Detection attempts to answer that question by analyzing how the target responds to specially crafted network packets.

Unlike service detection, which identifies applications, OS Detection identifies the underlying operating system.

---

## Examples

```
Linux

Windows

FreeBSD

OpenBSD

macOS

Cisco IOS

Juniper JunOS

Android

Embedded Linux
```

---

# 2. Why OS Detection Matters

Knowing the operating system provides valuable information for security assessments.

Examples include:

- Identifying platform-specific vulnerabilities
- Selecting appropriate exploits
- Understanding default services
- Recognizing network devices
- Improving attack planning

For example,

```
Apache 2.4

↓

Linux
```

requires different security considerations than

```
Apache 2.4

↓

Windows Server
```

---

# 3. How Nmap Detects Operating Systems

Nmap sends a series of specially crafted packets to the target.

The operating system responds according to its TCP/IP implementation.

Nmap analyzes these responses and compares them against its fingerprint database.

```text
Target

↓

Special Probe Packets

↓

TCP/IP Responses

↓

Fingerprint Analysis

↓

Operating System Guess
```

Unlike banner grabbing, OS Detection does not rely on application responses.

---

# 4. TCP/IP Fingerprinting

Every operating system implements the TCP/IP stack slightly differently.

Nmap analyzes characteristics such as:

- TCP Window Size
- Initial Sequence Numbers (ISN)
- TCP Options
- IP Identification (IP ID)
- Don't Fragment (DF) flag
- Time To Live (TTL)
- ICMP responses

These values create a unique fingerprint.

---

## Example

```
TTL = 64

Window Size = 64240

TCP Options

↓

Likely Linux
```

```
TTL = 128

Window Size = 65535

↓

Likely Windows
```

These values are indicators, not guarantees.

---

# 5. Active Fingerprinting

Nmap uses **Active Fingerprinting**.

This means it actively sends probe packets and analyzes the responses.

```text
Nmap

↓

Probe

↓

Target

↓

Response

↓

Fingerprint Match
```

Unlike passive fingerprinting, active fingerprinting requires interaction with the target.

---

# 6. OS Detection (-O)

The basic command is:

```bash
sudo nmap -O target
```

Example:

```bash
sudo nmap -O 192.168.1.20
```

Sample output:

```text
OS details:

Linux 6.x

Network Distance: 1 hop
```

---

## Combining With Service Detection

```bash
sudo nmap -sS -sV -O target
```

This command combines:

- Port Scanning
- Service Detection
- Operating System Detection

It is commonly used during reconnaissance.

---

# 7. OS Guessing

Sometimes Nmap cannot identify the exact operating system.

Instead, it provides the closest matches.

Example:

```text
Aggressive OS guesses:

Linux 5.15 (96%)

Linux 6.1 (94%)

Ubuntu Linux (92%)
```

These percentages represent confidence levels based on fingerprint similarity.

---

# 8. Device Type Detection

OS Detection can also identify the type of device.

Examples:

```
General Purpose

Router

Switch

Firewall

Printer

VoIP Phone

Game Console

Access Point
```

Example output:

```text
Device type:

Router
```

This helps understand the role of the target within the network.

---

# 9. Accuracy and Limitations

OS Detection is highly effective but not always exact.

Factors that reduce accuracy include:

- Firewalls
- NAT devices
- Packet filtering
- Load balancers
- Virtual machines
- Custom TCP/IP stacks

If too few ports are available, Nmap may not have enough data to make a reliable guess.

---

# 10. Firewall Effects

Firewalls can interfere with OS Detection.

For example:

```text
Probe

↓

Firewall

↓

Dropped
```

or

```text
Probe

↓

Firewall

↓

Modified Response
```

This may lead to inaccurate results or prevent OS Detection entirely.

---

# 11. Real-World Examples

Basic OS Detection:

```bash
sudo nmap -O target
```

Combined scan:

```bash
sudo nmap -sS -sV -O target
```

Aggressive scan (includes OS Detection):

```bash
sudo nmap -A target
```

---

# Best Practices

✓ Ensure at least one open and one closed TCP port are available for best results.

✓ Combine OS Detection with Service Detection.

✓ Treat confidence percentages as estimates.

✓ Verify important findings using additional methods.

✓ Use OS Detection only on systems you are authorized to assess.

---

# Summary

Operating System Detection enables Nmap to identify the probable operating system of a target by analyzing TCP/IP behavior.

By comparing packet responses against its fingerprint database, Nmap can often determine not only the operating system but also the device type.

OS Detection complements Port Scanning and Service Detection, providing a more complete understanding of the target environment.

---

# Key Takeaways

✓ OS Detection identifies the target's operating system.

✓ Nmap uses active TCP/IP fingerprinting.

✓ The `-O` option enables OS Detection.

✓ Confidence values represent probability, not certainty.

✓ Firewalls and packet filtering can reduce accuracy.

✓ Combining `-sS`, `-sV`, and `-O` provides comprehensive reconnaissance.

---

# Next Course

## Course 10

# Nmap Scripting Engine (NSE)