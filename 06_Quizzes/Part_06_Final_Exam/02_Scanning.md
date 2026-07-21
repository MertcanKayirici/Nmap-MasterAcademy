# Final Exam — Part 02: Scanning & Enumeration

> This section evaluates your ability to perform and interpret port scanning, service enumeration, operating system detection, and scan optimization.

---

# Overview

Topics covered:

- TCP Scanning
- UDP Scanning
- Service Detection
- Version Detection
- OS Detection
- Timing Templates
- Scan Performance
- Output Formats

---

# Instructions

- Questions: 20
- Suggested Time: 25 Minutes

Choose the best answer for each question.

---

# Multiple Choice

## Question 1

Which Nmap option enables service version detection?

A. -O

B. -sV

C. -A

D. -sn

---

## Question 2

Which option attempts operating system detection?

A. -sV

B. -O

C. -Pn

D. -PR

---

## Question 3

What is the purpose of the `-A` option?

A. Perform aggressive scan including OS detection, version detection, default scripts, and traceroute.

B. Scan only UDP ports.

C. Disable host discovery.

D. Scan all IP addresses.

---

## Question 4

Which timing template is the fastest?

A. T0

B. T2

C. T4

D. T5

---

## Question 5

Why should aggressive timing templates be used carefully?

A. They may increase network load and reduce scan reliability.

B. They improve encryption.

C. They disable logging.

D. They prevent service detection.

---

## Question 6

Which output format is most suitable for machine processing?

A. XML

B. Normal Output

C. Grepable Output

D. Interactive Console

---

## Question 7

What is service enumeration?

A. Identifying running services and collecting information about them.

B. Changing service ports.

C. Encrypting traffic.

D. Creating firewall rules.

---

## Question 8

Why is version detection valuable?

A. It identifies software versions that may require further investigation.

B. It increases bandwidth.

C. It closes open ports.

D. It modifies services.

---

## Question 9

What is the purpose of scanning specific ports instead of all ports?

A. Reduce scan duration when only selected services are relevant.

B. Disable OS detection.

C. Improve DNS resolution.

D. Replace host discovery.

---

## Question 10

Which scan is generally preferred for stealthier TCP reconnaissance?

A. Connect Scan

B. SYN Scan

C. UDP Scan

D. Idle Scan

---

# True / False

## Question 11

Version detection requires communication with the target service.

- True
- False

---

## Question 12

Operating system detection is always 100% accurate.

- True
- False

---

## Question 13

UDP scanning may produce many open|filtered results.

- True
- False

---

## Question 14

XML output is commonly used by automation tools.

- True
- False

---

## Question 15

Timing templates should be selected according to the assessment environment.

- True
- False

---

# Output Analysis

## Question 16

```
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 9.6
80/tcp  open  http    Apache httpd 2.4.62
```

Which conclusion is most appropriate?

A. Service versions have been successfully identified.

B. The operating system has been confirmed.

C. UDP services are unavailable.

D. The host is offline.

---

## Question 17

```
Device type: general purpose
Running: Linux
OS details: Linux 6.x
```

What feature produced this information?

A. OS Detection

B. Version Detection

C. Host Discovery

D. DNS Resolution

---

## Question 18

```
PORT      STATE         SERVICE
53/udp    open|filtered domain
```

What does `open|filtered` indicate?

A. Nmap cannot confidently distinguish between an open port and packet filtering.

B. The port is confirmed closed.

C. DNS is disabled.

D. The operating system is Windows.

---

# Scenario-Based

## Question 19

You are assessing a large production network.

What is the most appropriate workflow?

A. Host discovery → Port scanning → Service detection → Reporting.

B. OS Detection → Reporting → Host discovery.

C. Vulnerability scanning before host discovery.

D. Random scan order.

---

## Question 20

A scan identifies several outdated service versions.

What should you do?

A. Document the findings and recommend further investigation or remediation.

B. Modify the target systems immediately.

C. Ignore version information.

D. Delete the scan results.

---

# End of Part 02

Continue to:

➡ **03_NSE.md**