# Lab 27 — Hack The Box Advanced Enumeration

> Perform a structured enumeration of a Hack The Box machine using Nmap and service-specific NSE scripts.

---

# Overview

Finding open ports is only the beginning of an assessment.

The next step is to understand:

- What services are running?
- Which technologies are being used?
- What information can be collected safely?
- Which services require further investigation?

Professional penetration testers spend significantly more time on enumeration than on exploitation.

This lab focuses entirely on building that methodology.

---

# Rules of Engagement

- Work only within the assigned HTB machine.
- Do not attack systems outside the VPN.
- Document every command.
- Record every observation.
- Do not assume vulnerabilities without evidence.

---

# Learning Objectives

After completing this lab, you will be able to:

- Perform advanced service enumeration.
- Select appropriate NSE scripts.
- Build technology profiles.
- Prioritize services for investigation.
- Produce an enumeration report.

---

# Difficulty

⭐⭐⭐⭐☆

---

# Estimated Time

90–120 Minutes

---

# Scenario

You have completed an initial scan.

Discovered services:

```text
22/tcp   OpenSSH
80/tcp   Apache
139/tcp  NetBIOS
445/tcp  SMB
```

Your objective is to collect as much information as possible before considering any further actions.

---

# Enumeration Workflow

```
Open Ports

↓

Identify Services

↓

Run Service-Specific NSE Scripts

↓

Collect Information

↓

Build Technology Profile

↓

Prioritize Investigation
```

---

# Phase 1 — SSH Enumeration

```bash
nmap --script ssh-hostkey -p22 TARGET_IP
```

Document:

- RSA key
- ECDSA key
- ED25519 key

Questions:

- Which key algorithms are supported?
- Does the SSH banner reveal version information?

---

# Phase 2 — HTTP Enumeration

```bash
nmap --script http-title,http-headers,http-methods TARGET_IP
```

Document:

- Title
- Server header
- Allowed methods
- Redirects

---

# Phase 3 — SSL Enumeration (If HTTPS Exists)

```bash
nmap --script ssl-cert,ssl-enum-ciphers -p443 TARGET_IP
```

Record:

- Certificate subject
- Issuer
- Expiration
- TLS versions
- Cipher suites

---

# Phase 4 — SMB Enumeration

```bash
nmap --script smb-os-discovery TARGET_IP
```

```bash
nmap --script smb-protocols TARGET_IP
```

```bash
nmap --script smb-security-mode TARGET_IP
```

```bash
nmap --script smb-enum-shares TARGET_IP
```

Document:

- Hostname
- Domain
- Shares
- SMB versions
- Authentication mode

---

# Phase 5 — Version Detection

```bash
nmap -sV TARGET_IP
```

Create a table:

| Service | Product | Version |
|----------|----------|---------|
| SSH | | |
| HTTP | | |
| SMB | | |

---

# Phase 6 — Aggressive Scan

```bash
nmap -A TARGET_IP
```

Review:

- Service versions
- OS detection
- NSE output
- Traceroute

Compare the output with the manual enumeration performed earlier.

---

# Technology Profile

Complete:

| Category | Finding |
|----------|----------|
| Operating System | |
| Web Server | |
| SSH Version | |
| SMB Version | |
| Technologies | |

---

# Prioritization Matrix

Rank discovered services according to the amount of useful information they provide.

| Priority | Service | Reason |
|----------|----------|--------|
| High | | |
| Medium | | |
| Low | | |

Remember that prioritization depends on the assessment goals and available evidence.

---

# Assessment Checklist

☐ Full TCP scan completed

☐ Service detection completed

☐ SSH enumeration completed

☐ HTTP enumeration completed

☐ SMB enumeration completed

☐ Technology profile created

☐ Findings documented

---

# Decision Tree

```
Services Found

↓

Run Relevant NSE Scripts

↓

Collect Technical Information

↓

Compare Results

↓

Prioritize Services

↓

Prepare Next Assessment Phase
```

---

# Thinking Like a Pentester

Instead of asking:

> "Can I exploit this service?"

Ask:

- What additional information can I collect?
- Does the service reveal software versions?
- Are there configuration details worth documenting?
- Which service provides the clearest understanding of the target?

Enumeration reduces uncertainty and supports informed decision-making.

---

# Reporting Template

## Executive Summary

## Open Ports

## Service Versions

## SSH Findings

## HTTP Findings

## SMB Findings

## Technology Profile

## Recommendations

---

# Challenge

Perform a complete enumeration of an HTB machine and prepare:

- Service inventory
- Technology profile
- Enumeration notes
- Prioritization matrix
- Assessment report

---

# Bonus Challenge

Create a reusable Nmap command sequence that performs:

- Service Detection
- OS Detection
- Default NSE Scripts
- SSH Enumeration
- HTTP Enumeration
- SMB Enumeration

Save all results using:

```bash
-oA htb_enumeration
```

---

# Key Takeaways

- Enumeration is the foundation of effective security assessments.
- Service-specific NSE scripts provide significantly more context than basic port scans.
- Organizing findings into a technology profile helps prioritize further investigation.
- A disciplined, evidence-based approach leads to more accurate assessments.

---

# Next Lab

➡ **Lab 28 — TryHackMe Enumeration Workflow**