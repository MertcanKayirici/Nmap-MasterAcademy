# Quiz 01 — Fundamentals

> Assess your understanding of networking fundamentals and the basic concepts required to use Nmap effectively.

---

# Overview

This quiz covers the core concepts introduced in the Fundamentals section of the Nmap Master Academy.

Topics include:

- Introduction to Nmap
- Network Basics
- Ports
- TCP
- UDP
- Host Discovery
- Basic Port Scanning
- Service Detection

---

# Instructions

- **Total Questions:** 25
- **Passing Score:** 75%
- **Time Limit:** 30 Minutes

Read each question carefully and choose the best answer.

---

# Multiple Choice Questions

## Question 1

What is the primary purpose of Nmap?

A. Password recovery

B. Network discovery and security auditing

C. File encryption

D. Malware analysis

---

## Question 2

Which protocol provides reliable, connection-oriented communication?

A. UDP

B. TCP

C. ICMP

D. ARP

---

## Question 3

Which protocol is connectionless?

A. TCP

B. UDP

C. SSH

D. FTP

---

## Question 4

What is a network port?

A. A physical cable

B. A software communication endpoint

C. A network switch

D. A firewall rule

---

## Question 5

Which port is commonly associated with HTTP?

A. 22

B. 53

C. 80

D. 443

---

## Question 6

Which port is commonly associated with HTTPS?

A. 21

B. 80

C. 110

D. 443

---

## Question 7

Which service commonly uses port 22?

A. FTP

B. SSH

C. SMTP

D. SMB

---

## Question 8

What does Host Discovery attempt to determine?

A. Operating system version

B. Open ports

C. Whether a host is reachable

D. Running services

---

## Question 9

Which scan is primarily used to identify open ports?

A. Port Scan

B. Ping Scan

C. DNS Query

D. ARP Cache

---

## Question 10

What does Service Detection attempt to identify?

A. Firewall rules

B. Application names and versions

C. Network topology

D. MAC addresses

---

## Question 11

Which protocol is primarily responsible for translating domain names into IP addresses?

A. DHCP

B. DNS

C. SMTP

D. FTP

---

## Question 12

Which layer of the TCP/IP model is responsible for routing packets?

A. Application Layer

B. Transport Layer

C. Internet Layer

D. Link Layer

---

## Question 13

Why is understanding TCP and UDP important when using Nmap?

A. It improves typing speed.

B. Different scan techniques depend on protocol behavior.

C. It changes IP addresses.

D. It disables firewalls.

---

## Question 14

Which statement best describes TCP?

A. Fast but unreliable

B. Reliable and connection-oriented

C. Broadcast only

D. Used exclusively for DNS

---

## Question 15

Which statement best describes UDP?

A. Reliable and connection-oriented

B. Requires a three-way handshake

C. Lightweight and connectionless

D. Encrypts traffic automatically

---

# True / False

## Question 16

Nmap can only scan Linux systems.

- True
- False

---

## Question 17

An open port usually indicates that a service is listening.

- True
- False

---

## Question 18

TCP always guarantees packet delivery.

- True
- False

---

## Question 19

UDP performs a three-way handshake before sending data.

- True
- False

---

## Question 20

Understanding networking fundamentals improves scan interpretation.

- True
- False

---

# Output Analysis

## Question 21

A scan reports:

```
80/tcp open http
443/tcp open https
```

What can be concluded?

A. The host is powered off.

B. The host is likely running web services.

C. The firewall is blocking all traffic.

D. DNS is unavailable.

---

## Question 22

A scan reports:

```
Host is up.
```

What does this indicate?

A. The operating system has been identified.

B. The host responded to discovery probes.

C. All ports are open.

D. Service detection has completed.

---

## Question 23

A scan reports:

```
22/tcp open ssh
```

Which service is likely available?

A. DNS

B. FTP

C. SSH

D. SMTP

---

# Scenario-Based Questions

## Question 24

You have been authorized to assess a small office network.

Before identifying services, what should you determine first?

A. Open every firewall port.

B. Discover which hosts are online.

C. Remove antivirus software.

D. Guess the operating systems.

---

## Question 25

A colleague immediately starts service detection without verifying whether the target hosts are reachable.

What is the best recommendation?

A. Continue as planned.

B. Perform host discovery first to identify active systems.

C. Disable the network firewall.

D. Skip documentation.

---

# End of Quiz

After completing all questions, review your answers using **Answer_Key.md**.

Good luck!