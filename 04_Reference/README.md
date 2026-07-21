# Reference

> Quick reference documentation for networking concepts, TCP/IP fundamentals, and Nmap-related topics.

---

# Overview

The **Reference** section is designed as a fast and practical knowledge base.

Unlike the **Course** section, which focuses on teaching concepts step by step, this directory provides concise reference material that can be used during daily work, labs, Capture The Flag (CTF) challenges, penetration tests, security assessments, or exam preparation.

The goal is to help readers quickly recall important information without reading an entire lesson again.

---

# Why This Section Exists

During penetration testing and network analysis, professionals often need immediate access to information such as:

- Common service ports
- TCP vs UDP differences
- TCP Flags
- Three-Way Handshake
- Packet flow
- Frequently used network services

Searching through lengthy documentation every time is inefficient.

This section solves that problem by collecting the most commonly referenced networking topics into one place.

Think of it as a networking handbook that you can open whenever you need a quick answer.

---

# Course vs Reference

One of the most common questions is:

> "Why are these topics included again if they already exist in the Course?"

The answer is simple.

## Course

The **Course** directory is intended for learning.

Topics are explained in depth, starting from the basics and gradually moving toward more advanced concepts.

Readers are expected to spend time understanding the material.

Example:

```
What is TCP?

↓

How does TCP work?

↓

How does TCP establish a connection?

↓

How does Nmap use TCP?
```

---

## Reference

The **Reference** directory is intended for quick consultation.

Instead of lengthy explanations, it focuses on concise summaries, comparison tables, diagrams, packet flows, port lists, and commonly used information.

It is designed for situations where the reader already understands the concept but needs a rapid reminder.

Example:

```
Need to remember:

• Which ports use UDP?
• What does the SYN flag do?
• What is the difference between TCP and UDP?
• Which scan uses FIN?
```

Open the reference, find the answer, continue working.

---

# When Should You Use This Section?

This section is especially useful during:

- Penetration testing
- Network troubleshooting
- CTF competitions
- Security assessments
- Incident response
- Packet analysis
- Wireshark investigations
- Nmap scanning
- Practical labs
- Technical interviews
- Exam preparation

---

# Learning Recommendation

For the best learning experience:

1. Study the topic in the **Course** section.
2. Practice the topic in a lab environment.
3. Return to this **Reference** section whenever you need a quick reminder.

This approach helps reinforce knowledge through both detailed learning and repeated review.

---

# Directory Structure

```
Reference/
│
├── 01_Top_100_Ports.md
├── 02_Top_1000_Ports.md
├── 03_Common_Network_Services.md
├── 04_TCP_vs_UDP.md
├── 05_TCP_Flags.md
├── 06_Three_Way_Handshake.md
└── 07_ASCII_Diagrams.md
```

---

# File Descriptions

## 01 — Top 100 Ports

Provides a quick reference for the 100 most commonly encountered ports, including protocol information and associated services.

---

## 02 — Top 1000 Ports

Contains a broader list of the most frequently scanned ports, commonly used during reconnaissance and security assessments.

---

## 03 — Common Network Services

Explains widely used network services, their purposes, typical ports, and where they are commonly encountered.

Examples include:

- HTTP
- HTTPS
- SSH
- FTP
- DNS
- SMTP
- LDAP
- SMB
- MySQL
- Redis

and many more.

---

## 04 — TCP vs UDP

A side-by-side comparison of the two transport layer protocols.

Topics include:

- Reliability
- Speed
- Header structure
- Packet flow
- Nmap scanning
- Advantages and disadvantages
- Typical use cases

---

## 05 — TCP Flags

Explains every TCP control flag used in packet communication.

Includes:

- SYN
- ACK
- FIN
- RST
- PSH
- URG
- ECE
- CWR

Also covers how Nmap uses these flags during advanced scans.

---

## 06 — Three-Way Handshake

Illustrates the complete TCP connection establishment process.

Includes:

- SYN
- SYN-ACK
- ACK
- Sequence numbers
- Connection lifecycle
- Nmap SYN Scan behavior

---

## 07 — ASCII Diagrams

A collection of text-based diagrams that visualize networking concepts directly inside the terminal or Markdown viewer.

Includes diagrams for:

- TCP
- UDP
- TCP Flags
- Three-Way Handshake
- Four-Way Termination
- Packet flow
- Nmap workflow
- TCP/IP stack

---

# Who Is This For?

This section is intended for:

- Students
- Network Engineers
- System Administrators
- SOC Analysts
- Blue Team Members
- Red Team Members
- Penetration Testers
- Bug Bounty Hunters
- Security Researchers
- Anyone learning Nmap and networking

---

# Design Principles

Every reference document follows the same philosophy:

- Easy to read
- Consistent formatting
- Practical examples
- Clear comparison tables
- Terminal-friendly ASCII diagrams
- Concise explanations
- Professional documentation style

---

# Final Notes

The **Reference** directory is not meant to replace the **Course**.

Instead, it complements it.

The **Course** teaches concepts in depth, while the **Reference** provides quick access to essential information when speed and convenience matter.

Together, they create a learning experience that supports both structured study and real-world usage.