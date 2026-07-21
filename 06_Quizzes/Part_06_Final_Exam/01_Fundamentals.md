# Final Exam — Part 01: Fundamentals

> This section evaluates your understanding of networking fundamentals, TCP/IP, ports, host discovery, and core Nmap concepts.

---

# Overview

Topics covered:

- Networking Fundamentals
- OSI Model
- TCP/IP
- Ports
- TCP vs UDP
- Host Discovery
- Scan Types
- Basic Nmap Usage

---

# Instructions

- Questions: 20
- Suggested Time: 25 Minutes

Choose the best answer for each question.

---

# Multiple Choice

## Question 1

What is the primary purpose of Nmap?

A. Develop web applications

B. Discover hosts and analyze network services

C. Encrypt network traffic

D. Monitor CPU performance

---

## Question 2

Which protocol guarantees reliable, ordered data delivery?

A. UDP

B. ICMP

C. TCP

D. ARP

---

## Question 3

Which protocol is primarily used by the `ping` command?

A. TCP

B. UDP

C. ICMP

D. HTTP

---

## Question 4

What does an open TCP port indicate?

A. The service is accepting connections.

B. The host is offline.

C. The firewall is disabled.

D. The operating system is unknown.

---

## Question 5

Which Nmap option performs a SYN scan?

A. -sT

B. -sS

C. -sU

D. -sn

---

## Question 6

What is the purpose of host discovery?

A. Identify live hosts before detailed scanning.

B. Detect operating systems.

C. Enumerate DNS records.

D. Capture packets.

---

## Question 7

Which scan type requires a full TCP connection?

A. SYN Scan

B. Connect Scan

C. UDP Scan

D. ACK Scan

---

## Question 8

What is the default protocol scanned by Nmap if no scan type is specified?

A. UDP

B. TCP

C. ICMP

D. SCTP

---

## Question 9

Why is UDP scanning generally slower than TCP scanning?

A. UDP requires encryption.

B. Many UDP services do not respond unless necessary.

C. UDP always retransmits packets.

D. UDP requires authentication.

---

## Question 10

Why should scans remain within the authorized scope?

A. To improve scan speed.

B. To comply with legal and ethical requirements.

C. To reduce RAM usage.

D. To enable OS detection.

---

# True / False

## Question 11

TCP provides connection-oriented communication.

- True
- False

---

## Question 12

UDP guarantees packet delivery.

- True
- False

---

## Question 13

Host discovery should generally be performed before full port scanning.

- True
- False

---

## Question 14

An open port always indicates a vulnerability.

- True
- False

---

## Question 15

Nmap can perform host discovery without scanning ports.

- True
- False

---

# Output Analysis

## Question 16

```
Host is up (0.0021s latency).
```

What can be concluded?

A. The target is reachable.

B. The firewall is disabled.

C. All ports are open.

D. The operating system is Linux.

---

## Question 17

```
80/tcp open http
443/tcp open https
```

Which statement is most accurate?

A. The host appears to provide web services.

B. FTP is running.

C. DNS is unavailable.

D. SSH is disabled.

---

## Question 18

```
Not shown: 997 closed tcp ports
22/tcp open ssh
80/tcp open http
443/tcp open https
```

What does this result indicate?

A. Three TCP ports are open, while the remaining scanned ports are closed.

B. Only port 22 is open.

C. The host is unreachable.

D. UDP services are unavailable.

---

# Scenario-Based

## Question 19

You are assessing a new subnet with hundreds of hosts.

What is the most efficient first step?

A. Perform host discovery to identify active systems.

B. Run an aggressive scan against every IP immediately.

C. Scan only port 80.

D. Skip reconnaissance.

---

## Question 20

A colleague immediately starts vulnerability-focused scans without identifying active hosts.

What is the best recommendation?

A. Perform host discovery first to reduce unnecessary scanning and focus on reachable systems.

B. Continue scanning every address regardless of response.

C. Disable host discovery permanently.

D. Avoid documenting the assessment.

---

# End of Part 01

Continue to:

➡ **02_Scanning.md**