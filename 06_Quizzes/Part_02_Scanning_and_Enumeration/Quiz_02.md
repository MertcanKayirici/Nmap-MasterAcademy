# Quiz 02 — Scanning and Enumeration

> Evaluate your understanding of Nmap scanning techniques, service detection, operating system detection, and scan interpretation.

---

# Overview

This quiz focuses on practical scanning and enumeration techniques used during authorized network assessments.

Topics include:

- Port Scanning
- Service Detection
- OS Detection
- Aggressive Scan
- Output Formats
- Enumeration Workflow

---

# Instructions

- **Total Questions:** 25
- **Passing Score:** 75%
- **Time Limit:** 35 Minutes

Read each question carefully and choose the best answer.

---

# Multiple Choice Questions

## Question 1

What is the primary goal of port scanning?

A. Encrypt traffic

B. Identify open ports on a target

C. Disable services

D. Recover passwords

---

## Question 2

Service Detection primarily attempts to identify:

A. MAC addresses

B. Network cables

C. Running services and versions

D. Firewall vendors

---

## Question 3

Operating System Detection attempts to identify:

A. BIOS version

B. Installed software

C. The target operating system

D. User accounts

---

## Question 4

What information can be obtained from a successful service detection scan?

A. File contents

B. Application name and version

C. User passwords

D. Registry settings

---

## Question 5

Why is version detection important?

A. It reduces network speed.

B. It helps identify the software running on open ports.

C. It changes firewall rules.

D. It hides scan traffic.

---

## Question 6

Why is OS Detection useful?

A. It identifies possible platform-specific configurations.

B. It automatically exploits systems.

C. It removes vulnerabilities.

D. It disables services.

---

## Question 7

Which stage usually follows Host Discovery?

A. Password auditing

B. Port Scanning

C. Report writing

D. Malware analysis

---

## Question 8

What is the purpose of Aggressive Scan?

A. Encrypt scan results

B. Combine several detection techniques into one scan

C. Close ports

D. Remove services

---

## Question 9

Why should scan results be documented?

A. To consume disk space

B. To support analysis and reporting

C. To increase network traffic

D. To slow the scan

---

## Question 10

Why are output formats important?

A. They help organize and analyze scan results.

B. They improve network speed.

C. They close open ports.

D. They modify scan behavior.

---

## Question 11

Which output format is generally the easiest to automate?

A. XML

B. Normal Output

C. Console Only

D. Screenshot

---

## Question 12

Why is XML commonly used?

A. It is structured and machine-readable.

B. It encrypts scan traffic.

C. It hides results.

D. It reduces scan duration.

---

## Question 13

Which activity belongs to enumeration?

A. Installing software

B. Gathering detailed information about discovered services

C. Encrypting traffic

D. Creating backups

---

## Question 14

Why should open ports be investigated further?

A. They may reveal available services and technologies.

B. They slow the network.

C. They disable DNS.

D. They always indicate malware.

---

## Question 15

Which statement best describes enumeration?

A. Random guessing

B. Structured information gathering

C. Password cracking

D. File recovery

---

# True / False

## Question 16

Enumeration begins only after identifying active hosts.

- True
- False

---

## Question 17

OS Detection always returns 100% accurate results.

- True
- False

---

## Question 18

Service Detection may identify application versions.

- True
- False

---

## Question 19

Saving scan results is considered good practice.

- True
- False

---

## Question 20

Enumeration is a one-time process that never requires verification.

- True
- False

---

# Output Analysis

## Question 21

A scan reports:

```
22/tcp open ssh
80/tcp open http
443/tcp open https
```

Which conclusion is most reasonable?

A. The system likely provides remote administration and web services.

B. The host is offline.

C. DNS is unavailable.

D. The operating system has crashed.

---

## Question 22

A scan reports:

```
Service Info:
OS: Linux
```

What does this indicate?

A. Nmap identified characteristics consistent with a Linux-based system.

B. Windows is installed.

C. The scan failed.

D. SSH is disabled.

---

## Question 23

A scan reports:

```
PORT     STATE    SERVICE
445/tcp  open     microsoft-ds
```

Which type of environment is commonly associated with this service?

A. Web hosting

B. Windows file sharing

C. DNS infrastructure

D. Email servers

---

# Scenario-Based Questions

## Question 24

You have completed Host Discovery and identified several active systems.

What should be your next step?

A. Ignore the hosts.

B. Begin structured port scanning and service enumeration.

C. Shut down the network.

D. Skip documentation.

---

## Question 25

During an assessment, your team wants consistent and reusable scan results for future reporting.

Which practice is most appropriate?

A. Record only screenshots.

B. Save structured scan outputs for later analysis.

C. Delete scan results immediately.

D. Memorize the findings.