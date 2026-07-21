# Lab 30 — Final Reconnaissance Capstone

> Conduct a complete reconnaissance assessment against an intentionally vulnerable target by combining every Nmap technique learned throughout this section.

---

# Overview

This capstone lab represents the final practical assessment of Part 05.

You will perform a complete reconnaissance workflow against an intentionally vulnerable machine similar to those found on:

- Hack The Box
- TryHackMe
- VulnHub
- CTF Platforms

Rather than solving the machine, your objective is to understand it.

Professional assessments begin with accurate reconnaissance—not exploitation.

---

# Rules of Engagement

- Stay within the authorized lab environment.
- Perform reconnaissance only.
- Do not modify the target.
- Record every command executed.
- Document all observations.
- Base conclusions on collected evidence.

---

# Learning Objectives

After completing this lab, you will be able to:

- Plan a reconnaissance assessment.
- Perform complete host enumeration.
- Build technology profiles.
- Identify infrastructure roles.
- Prioritize findings.
- Produce a professional reconnaissance report.

---

# Difficulty

⭐⭐⭐⭐⭐

Capstone

---

# Estimated Time

2–4 Hours

---

# Prerequisites

- Labs 26–29 completed
- Familiarity with NSE
- Basic networking knowledge

---

# Scenario

You receive access to a new target machine.

Information provided:

```text
Target IP:
10.10.10.100
```

No hostname.

No documentation.

No hints.

Everything must be discovered through reconnaissance.

---

# Reconnaissance Workflow

```
Receive Target

↓

Verify Connectivity

↓

Host Discovery

↓

Full Port Scan

↓

Service Detection

↓

OS Detection

↓

NSE Enumeration

↓

Technology Profiling

↓

Prioritization

↓

Final Report
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

# Phase 2 — Full TCP Scan

```bash
nmap -p- TARGET_IP
```

Document:

- Open ports
- Closed ports
- Filtered ports

---

# Phase 3 — Service Detection

```bash
nmap -sV TARGET_IP
```

Complete:

| Port | Service | Product | Version |
|------|----------|----------|---------|

---

# Phase 4 — Operating System Detection

```bash
nmap -O TARGET_IP
```

Document:

- Operating system
- Device type
- Confidence

---

# Phase 5 — Default NSE Enumeration

```bash
nmap -sC -sV TARGET_IP
```

Review:

- HTTP information
- SMB information
- SSL certificates
- SSH host keys
- Additional banners

---

# Phase 6 — Service-Specific Enumeration

Select appropriate NSE scripts based on discovered services.

Possible categories include:

- HTTP
- HTTPS
- FTP
- SSH
- SMB
- DNS
- Database
- SMTP

Document:

- Commands used
- Information collected
- Relevant observations

---

# Phase 7 — Technology Profile

Create the following inventory.

| Category | Finding |
|----------|----------|
| Operating System | |
| Web Server | |
| SSH | |
| SMB | |
| Database | |
| Programming Language | |
| Framework | |
| Interesting Technologies | |

---

# Phase 8 — Infrastructure Role

Based on collected evidence:

Determine whether the host is most likely acting as:

- Web Server
- Database Server
- Domain Controller
- Application Server
- File Server
- Mail Server
- VPN Gateway
- Development Server
- Other

Explain the evidence supporting your conclusion.

---

# Phase 9 — Prioritization Matrix

Rank discovered services.

| Priority | Service | Reason |
|----------|----------|--------|
| High | | |
| Medium | | |
| Low | | |

Priorities should reflect the value of further enumeration, not assumptions about vulnerabilities.

---

# Phase 10 — Assessment Checklist

☐ Host reachable

☐ Full TCP scan completed

☐ Version detection completed

☐ OS detection completed

☐ NSE scripts executed

☐ Technology profile created

☐ Infrastructure role identified

☐ Priorities documented

☐ Final report completed

---

# Phase 11 — Executive Report

Prepare a professional report including:

## Executive Summary

## Scope

## Methodology

## Commands Executed

## Open Ports

## Service Inventory

## Operating System

## Technology Profile

## Infrastructure Assessment

## Observations

## Recommendations

## Conclusion

---

# Decision Tree

```
Target Received

↓

Identify Services

↓

Detect Versions

↓

Run NSE Scripts

↓

Analyze Technologies

↓

Determine Host Role

↓

Prioritize Findings

↓

Prepare Report
```

---

# Thinking Like a Professional

Instead of asking:

> "How do I get the flag?"

Ask:

- What services are available?
- Which technologies are present?
- Which findings require additional investigation?
- Have I documented all collected evidence?
- Can another analyst reproduce my assessment?

Professional reconnaissance is repeatable, evidence-based, and well documented.

---

# Deliverables

At the end of this lab you should produce:

- Asset Profile
- Port Inventory
- Service Inventory
- Technology Profile
- Infrastructure Assessment
- Prioritization Matrix
- Reconnaissance Notes
- Executive Report

---

# Final Challenge

Perform a complete reconnaissance assessment from start to finish without using any predefined walkthroughs.

The final report should allow another analyst to understand:

- The target
- The exposed services
- The technologies in use
- The host's probable role
- The recommended next investigation steps

---

# Congratulations!

You have successfully completed:

✅ Hack The Box Basic Enumeration

✅ Advanced Enumeration

✅ TryHackMe Workflow

✅ CTF Reconnaissance

✅ Final Reconnaissance Capstone

You now possess a structured methodology for using Nmap in educational platforms while maintaining professional reconnaissance standards.

---

# Next Part

➡ **Part 06 — Evasion**