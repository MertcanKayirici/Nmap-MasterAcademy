# Nmap Master Academy

# Course 01

# Introduction to Nmap

---

## Course Information

**Course Number:** 01

**Difficulty:** Beginner

**Estimated Reading Time:** 30–45 Minutes

**Prerequisites:** None

---

# Table of Contents

1. What is Nmap?
2. History of Nmap
3. Why Learn Nmap?
4. Features
5. Common Use Cases
6. How Nmap Works
7. Nmap Architecture
8. Installing Nmap
9. Running Your First Scan
10. Understanding the Output
11. Legal and Ethical Considerations
12. Summary

---

# 1. What is Nmap?

Nmap (Network Mapper) is an open-source network scanning and security auditing tool used to discover hosts, identify open ports, detect running services, determine operating systems, and gather information about devices connected to a network.

Originally developed for Linux, Nmap now supports Windows, macOS, and many UNIX-based operating systems.

Today, it is considered one of the most important tools in cybersecurity.

---

## Simple Definition

Think of Nmap as a doctor performing a health check on a computer network.

Instead of checking blood pressure or heart rate, Nmap checks:

- Which devices are online
- Which ports are open
- Which services are running
- Which operating system is installed
- Whether security configurations appear correct

---

# 2. History of Nmap

Nmap was created in 1997 by **Gordon Lyon**, better known by his pseudonym **Fyodor**.

Since its first release, it has evolved into one of the world's most widely used network security tools.

Major milestones include:

- 1997 — Initial release
- 2003 — Service Version Detection
- 2004 — Operating System Fingerprinting improvements
- 2007 — Nmap Scripting Engine (NSE)
- Present — Continuous updates with support for modern protocols and operating systems

---

# 3. Why Learn Nmap?

Nmap is a foundational skill for:

- Penetration Testers
- Security Analysts
- Blue Team Engineers
- Network Administrators
- SOC Analysts
- Incident Responders
- Cybersecurity Students

Without Nmap, it is difficult to understand what systems exist on a network before assessing or defending them.

---

# 4. Key Features

Nmap can perform many different tasks, including:

- Host discovery
- Port scanning
- Service detection
- Version detection
- Operating system detection
- Firewall analysis
- Network inventory
- Vulnerability discovery (using NSE)
- Script automation
- IPv6 scanning
- Performance tuning

---

# 5. Common Use Cases

Nmap is commonly used for:

## Network Inventory

Discover all active devices on a network.

---

## Security Audits

Identify exposed services and unnecessary open ports.

---

## Penetration Testing

Gather information before exploitation.

---

## Troubleshooting

Verify whether services are reachable.

---

## Compliance

Ensure only approved services are accessible.

---

# 6. How Nmap Works

Nmap communicates with target systems by sending carefully crafted network packets and analyzing the responses.

Simplified workflow:

```text
Target
   ▲
   │ Response
   │
Nmap
   │
   ▼
Probe Packet
```

The type of response determines whether:

- the host is online
- the port is open
- the service is running
- filtering is present

---

# 7. Nmap Architecture

```text
                 User
                  │
                  ▼
          Nmap Command Line
                  │
                  ▼
        Scan Engine & Scheduler
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
 Host Discovery  Port Scan  NSE
        │         │         │
        └─────────┼─────────┘
                  ▼
        Result Processing
                  │
                  ▼
          Output Generator
```

---

# 8. Installing Nmap

### Windows

Download the installer from the official Nmap website and follow the installation wizard.

---

### Linux

Example (Debian-based systems):

```bash
sudo apt update
sudo apt install nmap
```

---

### macOS

Example using Homebrew:

```bash
brew install nmap
```

---

# 9. Running Your First Scan

```bash
nmap scanme.nmap.org
```

Expected process:

```text
Target
    │
    ▼
Host Discovery
    │
    ▼
Port Scan
    │
    ▼
Results
```

---

# 10. Understanding the Output

Example:

```text
PORT    STATE SERVICE

22/tcp  open  ssh

80/tcp  open  http

443/tcp open  https
```

Meaning:

| Column | Description |
|---------|-------------|
| PORT | Network port |
| STATE | Current port state |
| SERVICE | Detected service |

---

# 11. Legal and Ethical Considerations

Nmap is a legitimate security tool.

However, scanning systems without authorization may violate:

- Organizational policies
- Terms of service
- Local laws
- National cybersecurity regulations

Always obtain permission before scanning any network you do not own or administer.

---

# 12. Summary

After completing this course, you should understand:

- What Nmap is
- Why it is important
- Where it is used
- How it works
- How to install it
- How to perform your first scan
- How to interpret basic results

The following course will introduce the networking concepts required to understand Nmap in greater depth.

---

# Key Takeaways

✓ Nmap is the industry-standard network scanner.

✓ It is used by both defenders and attackers.

✓ It gathers information by sending and analyzing network packets.

✓ Ethical use requires proper authorization.

✓ Understanding networking fundamentals is essential before mastering advanced Nmap techniques.

---

# Next Course

## Course 02

**Network Basics**