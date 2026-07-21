# Nmap Master Academy

# Course 08

# Service Detection

---

## Course Information

**Course Number:** 08

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

---

# Table of Contents

1. What is Service Detection?
2. Why Service Detection Matters
3. How Service Detection Works
4. Version Detection (-sV)
5. Banner Grabbing
6. Probe Database
7. Version Intensity
8. Service Fingerprinting
9. Unknown Services
10. Accuracy and Limitations
11. Real-World Examples
12. Best Practices
13. Summary

---

# 1. What is Service Detection?

Finding an open port is only the beginning.

For example,

```text
80/tcp open
```

This tells us that port 80 is open.

But:

- Is it Apache?
- Is it Nginx?
- Is it IIS?
- Which version?
- Is it vulnerable?

Service Detection answers these questions.

---

# Example

Without Service Detection

```text
80/tcp open
```

With Service Detection

```text
80/tcp open

Apache httpd

Version 2.4.58
```

Notice how much more useful the second result is.

---

# 2. Why Service Detection Matters

Security professionals need more than open ports.

They need to know:

- Software name
- Version
- Vendor
- Protocol
- Possible vulnerabilities

Knowing that a server runs:

```
Apache 2.2
```

is far more valuable than simply knowing:

```
Port 80 is open.
```

---

# 3. How Service Detection Works

Nmap performs Service Detection by sending carefully crafted probes to open ports.

```
Open Port

↓

Probe

↓

Response

↓

Fingerprint Analysis

↓

Detected Service
```

Unlike Host Discovery,

the target application actively responds.

---

## Example

```
GET /

↓

Apache

↓

HTTP Header

↓

Apache/2.4.58
```

Nmap compares this response against its internal fingerprint database.

---

# 4. Version Detection (-sV)

The most commonly used option is:

```bash
nmap -sV target
```

Example

```bash
nmap -sV 192.168.1.20
```

Output

```text
PORT     STATE SERVICE VERSION

22/tcp   open  ssh     OpenSSH 9.6

80/tcp   open  http    Apache 2.4.58

3306/tcp open  mysql   MySQL 8.0
```

---

## Combining With SYN Scan

```bash
sudo nmap -sS -sV target
```

This is one of the most frequently used combinations in penetration testing.

---

# 5. Banner Grabbing

Many services identify themselves automatically.

Example

```
SSH-2.0-OpenSSH_9.6
```

or

```
220 FTP Server Ready
```

These identification strings are called banners.

Nmap analyzes these banners whenever possible.

---

# Active vs Passive Banner Grabbing

| Method | Description |
|----------|-------------|
| Passive | Read the banner without sending additional protocol-specific requests. |
| Active | Send protocol-specific probes to trigger informative responses. |

Nmap primarily uses active probing during version detection.

---

# 6. Probe Database

Nmap includes a large database of protocol probes.

Each probe is designed for a particular protocol or service.

Example probes include:

- HTTP
- HTTPS
- FTP
- SMTP
- SSH
- POP3
- IMAP
- DNS
- SMB
- MySQL
- PostgreSQL
- Redis

Each response is compared against thousands of known fingerprints.

---

# Probe Process

```
Open Port

↓

HTTP Probe

↓

Response

↓

Database Match

↓

Apache
```

---

# 7. Version Intensity

Not every scan uses the same number of probes.

Nmap allows you to control how aggressively it attempts service detection.

Levels range from:

```
0

↓

9
```

---

## Default

```bash
nmap -sV
```

Uses the default intensity.

---

## Low Intensity

```bash
nmap -sV --version-light
```

Advantages

✓ Faster

✓ Less traffic

Disadvantages

✗ Lower accuracy

---

## High Intensity

```bash
nmap -sV --version-all
```

Advantages

✓ Highest accuracy

✓ More fingerprints tested

Disadvantages

✗ Slower

✗ Generates more traffic

---

## Manual Intensity

```bash
nmap -sV --version-intensity 7
```

Valid values:

```
0

↓

9
```

Higher values mean more probes.

---

# 8. Service Fingerprinting

Sometimes a service does not reveal its identity directly.

Nmap then compares multiple characteristics such as:

- Response format
- Packet size
- Timing
- Protocol behavior
- Error messages

to determine the most likely service.

This process is called fingerprinting.

---

# 9. Unknown Services

Occasionally, Nmap cannot identify a service.

Example

```text
8080/tcp open unknown
```

Possible reasons:

- Custom software
- Proprietary applications
- New software versions
- Modified banners

Unknown does not mean the port is unimportant.

Further investigation may be required.

---

# 10. Accuracy and Limitations

Service Detection is highly accurate but not perfect.

Challenges include:

- Firewalls
- Reverse proxies
- Banner obfuscation
- Load balancers
- Custom services
- Encrypted protocols

Always verify critical findings.

---

# 11. Real-World Examples

Basic version detection

```bash
nmap -sV target
```

Aggressive version detection

```bash
nmap -sV --version-all target
```

Fast version detection

```bash
nmap -sV --version-light target
```

Custom intensity

```bash
nmap -sV --version-intensity 5 target
```

---

# Best Practices

✓ Always combine Service Detection with Port Scanning.

✓ Verify unusual results manually.

✓ Use high intensity only when necessary.

✓ Remember that hidden banners do not guarantee security.

✓ Combine Service Detection with NSE for deeper analysis.

---

# Summary

Service Detection transforms a list of open ports into meaningful information about the target system.

By identifying services and software versions, Nmap provides the foundation for vulnerability assessment, security auditing, and penetration testing.

Understanding Service Detection is essential before moving on to Operating System Detection and the Nmap Scripting Engine.

---

# Key Takeaways

✓ Open ports are only the starting point.

✓ Service Detection identifies applications.

✓ Version Detection uses the -sV option.

✓ Nmap relies on probes and fingerprint matching.

✓ Fingerprinting improves identification accuracy.

✓ Unknown services require further investigation.

---

# Next Course

## Course 09

# Operating System Detection