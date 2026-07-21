# Lab 26 — Hack The Box Basic Enumeration

> Learn how to perform a structured initial reconnaissance against a Hack The Box target using Nmap.

---

# Overview

Hack The Box machines are intentionally vulnerable systems designed for educational purposes.

Although each machine is different, the reconnaissance process should remain consistent.

This lab introduces a repeatable workflow for gathering information before any exploitation attempts.

---

# Learning Objectives

After completing this lab, you will be able to:

- Verify target reachability.
- Perform initial port scans.
- Detect running services.
- Identify operating systems.
- Build an enumeration checklist.

---

# Difficulty

⭐⭐⭐☆☆

---

# Estimated Time

60–90 Minutes

---

# Scenario

You receive a Hack The Box machine IP.

Example:

```

10.129.45.17

```

No additional information is provided.

Your task is to identify the services running on the host and prepare an enumeration plan.

---

# Assessment Workflow

```

Target Received

↓

Host Verification

↓

Port Scan

↓

Version Detection

↓

OS Detection

↓

NSE

↓

Documentation

```

---

# Phase 1 — Verify Connectivity

```bash
ping -c 4 TARGET_IP
```

Document:

- Reachability
- Packet loss
- Latency

---

# Phase 2 — Initial Port Scan

```bash
nmap TARGET_IP
```

Questions:

- Which ports are open?
- Which services are immediately visible?

---

# Phase 3 — Full TCP Scan

```bash
nmap -p- TARGET_IP
```

Why?

Many HTB machines intentionally expose services on uncommon ports.

---

# Phase 4 — Service Detection

```bash
nmap -sV TARGET_IP
```

Document:

- Product
- Version
- Vendor

---

# Phase 5 — Operating System Detection

```bash
nmap -O TARGET_IP
```

Record:

- Estimated OS
- Confidence

---

# Phase 6 — Default NSE Scripts

```bash
nmap -sC -sV TARGET_IP
```

Review:

- HTTP titles
- SSH keys
- SMB information
- SSL certificates

---

# Enumeration Notes

Complete:

| Category | Finding |
|----------|----------|
| Operating System | |
| Open Ports | |
| Services | |
| Versions | |
| Interesting Findings | |

---

# Planning the Next Phase

Before continuing, ask:

- Which service should be investigated first?
- Which NSE scripts are appropriate?
- Are multiple services related?
- Which service appears most important?

---

# Assessment Checklist

☐ Host reachable

☑ Initial scan completed

☑ Full TCP scan completed

☑ Version detection completed

☑ OS detection completed

☑ NSE enumeration completed

☑ Findings documented

---

# Decision Tree

```

Machine Received

↓

Port Scan

↓

Version Detection

↓

NSE

↓

Identify Interesting Services

↓

Plan Next Enumeration

```

---

# Thinking Like a Pentester

Rather than asking:

> "Which exploit should I use?"

Ask:

- What services exist?
- What technologies are running?
- What additional information is needed before moving forward?
- Which enumeration step provides the greatest value?

Good reconnaissance reduces guesswork later in the assessment.

---

# Reporting Template

## Target

## Scope

## Scan Commands

## Open Ports

## Service Versions

## Operating System

## Enumeration Results

## Initial Observations

## Recommended Next Steps

---

# Challenge

Perform a complete initial assessment of a Hack The Box machine.

Produce:

- Port inventory
- Service inventory
- Technology profile
- Enumeration report

---

# Key Takeaways

- A structured methodology is more valuable than memorizing commands.
- Full port scans often reveal services hidden on uncommon ports.
- Service detection and NSE provide context that simple port scans cannot.
- Thorough documentation improves later stages of an assessment.

---

# Next Lab

➡ **Lab 27 — Hack The Box Advanced Enumeration**