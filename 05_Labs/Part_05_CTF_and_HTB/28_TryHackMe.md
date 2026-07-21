# Lab 28 — TryHackMe Enumeration Workflow

> Learn how to apply a structured Nmap reconnaissance workflow in TryHackMe rooms to identify technologies, collect service information, and prepare for further investigation.

---

# Overview

TryHackMe provides guided learning environments covering various cybersecurity topics.

Unlike many CTF platforms, TryHackMe often focuses on understanding concepts rather than simply finding flags.

This lab demonstrates how to use Nmap effectively within those learning environments while maintaining a professional assessment methodology.

---

# Rules of Engagement

- Work only inside the assigned TryHackMe room.
- Follow the room instructions and scope.
- Document every command executed.
- Verify findings before drawing conclusions.
- Avoid making assumptions without supporting evidence.

---

# Learning Objectives

After completing this lab, you will be able to:

- Build a repeatable reconnaissance workflow.
- Perform structured service enumeration.
- Select appropriate NSE scripts.
- Identify technologies used by the target.
- Produce organized enumeration notes.

---

# Difficulty

⭐⭐⭐☆☆

---

# Estimated Time

60–90 Minutes

---

# Scenario

You have joined a TryHackMe room.

Target IP:

```text
10.10.150.20
```

No additional information is available.

Your task is to identify the technologies running on the target and document your findings.

---

# Workflow

```
Target IP

↓

Host Verification

↓

Full Port Scan

↓

Service Detection

↓

OS Detection

↓

NSE Enumeration

↓

Technology Identification

↓

Documentation
```

---

# Phase 1 — Verify Connectivity

```bash
ping -c 4 TARGET_IP
```

Record:

- Reachability
- Packet loss
- Average latency

---

# Phase 2 — Initial Scan

```bash
nmap TARGET_IP
```

Document:

- Open ports
- Initial observations

---

# Phase 3 — Full TCP Scan

```bash
nmap -p- TARGET_IP
```

Questions:

- Are non-standard ports in use?
- Are additional services discovered?

---

# Phase 4 — Service Detection

```bash
nmap -sV TARGET_IP
```

Document:

- Product
- Vendor
- Version

---

# Phase 5 — Operating System Detection

```bash
nmap -O TARGET_IP
```

Record:

- Estimated operating system
- Confidence level

---

# Phase 6 — Service-Specific NSE Scripts

Choose scripts based on discovered services.

### HTTP

```bash
nmap --script http-title,http-headers,http-methods TARGET_IP
```

### SMB

```bash
nmap --script smb-os-discovery,smb-security-mode TARGET_IP
```

### FTP

```bash
nmap --script ftp-anon,ftp-syst TARGET_IP
```

### SSH

```bash
nmap --script ssh-hostkey TARGET_IP
```

### SSL

```bash
nmap --script ssl-cert,ssl-enum-ciphers TARGET_IP
```

---

# Phase 7 — Technology Profile

Complete the following table.

| Category | Finding |
|----------|----------|
| Operating System | |
| Web Server | |
| SSH | |
| Database | |
| File Sharing | |
| Interesting Services | |

---

# Phase 8 — Enumeration Summary

Summarize:

- Which services appear most important?
- Which technologies are identified?
- Which services require further investigation?

Support every conclusion with collected evidence.

---

# Assessment Checklist

☐ Host verified

☐ Full TCP scan completed

☐ Service detection completed

☐ OS detection completed

☐ Service-specific NSE scripts executed

☐ Technology profile created

☐ Findings documented

---

# Decision Tree

```
Receive Target

↓

Discover Ports

↓

Identify Services

↓

Choose NSE Scripts

↓

Collect Information

↓

Build Technology Profile

↓

Prepare Investigation Plan
```

---

# Thinking Like a Security Analyst

Avoid asking:

> "What is the answer for this room?"

Instead ask:

- What technologies are running?
- What evidence supports my conclusions?
- Which services deserve additional attention?
- Have I documented everything necessary?

Good analysts focus on evidence rather than shortcuts.

---

# Reporting Template

## Target Information

## Scan Commands

## Open Ports

## Service Versions

## Operating System

## NSE Results

## Technology Profile

## Observations

## Recommended Next Steps

---

# Challenge

Complete a full reconnaissance workflow for a TryHackMe room and prepare:

- Port inventory
- Technology profile
- Enumeration notes
- Assessment report

---

# Bonus Challenge

Create a reusable Nmap command sequence that includes:

- Full TCP Scan
- Service Detection
- OS Detection
- Default NSE Scripts
- Service-Specific NSE Scripts

Save the output using:

```bash
-oA tryhackme_assessment
```

---

# Key Takeaways

- TryHackMe rooms are ideal for practicing structured reconnaissance.
- Nmap should be used methodically rather than relying on a single command.
- Service-specific NSE scripts provide valuable context.
- Clear documentation improves both learning and repeatability.
- Evidence-based analysis is more valuable than guessing.

---

# Next Lab

➡ **Lab 29 — CTF Reconnaissance Methodology**