# Lab 29 — CTF Reconnaissance Methodology

> Learn how to perform structured reconnaissance during Capture The Flag (CTF) challenges using Nmap and a repeatable enumeration methodology.

---

# Overview

Capture The Flag (CTF) challenges are designed to improve technical skills by simulating realistic systems and scenarios.

Although each challenge is unique, the reconnaissance methodology should remain consistent.

Rather than immediately searching for vulnerabilities, successful participants first develop a clear understanding of the target.

This lab demonstrates a professional reconnaissance workflow that can be applied across various CTF platforms.

---

# Rules of Engagement

- Stay within the provided challenge scope.
- Document every command executed.
- Record every observation.
- Base conclusions on evidence.
- Avoid skipping enumeration steps.

---

# Learning Objectives

After completing this lab, you will be able to:

- Build a structured reconnaissance methodology.
- Identify high-value services.
- Select appropriate NSE scripts.
- Create a technology profile.
- Prioritize enumeration targets.
- Produce professional reconnaissance notes.

---

# Difficulty

⭐⭐⭐⭐☆

---

# Estimated Time

90–120 Minutes

---

# Scenario

You receive the following target:

```text
10.10.10.50
```

No description.

No hints.

No documentation.

Everything must be discovered through reconnaissance.

---

# Reconnaissance Workflow

```
Receive Target

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

Technology Profile

↓

Prioritize Services

↓

Prepare Investigation Plan
```

---

# Phase 1 — Verify Connectivity

```bash
ping -c 4 TARGET_IP
```

Record:

- Reachability
- Latency
- Packet loss

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

- Are services listening on uncommon ports?
- Are administrative services exposed?

---

# Phase 4 — Service Detection

```bash
nmap -sV TARGET_IP
```

Create:

| Port | Service | Product | Version |
|------|----------|----------|---------|

---

# Phase 5 — Operating System Detection

```bash
nmap -O TARGET_IP
```

Document:

- Operating system
- Device type
- Confidence

---

# Phase 6 — Service-Specific Enumeration

Choose NSE scripts based on discovered services.

### HTTP

```bash
http-title

http-headers

http-methods
```

### SMB

```bash
smb-os-discovery

smb-security-mode

smb-enum-shares
```

### FTP

```bash
ftp-anon

ftp-syst
```

### SSH

```bash
ssh-hostkey
```

### DNS

```bash
dns-recursion

dns-service-discovery
```

### SSL

```bash
ssl-cert

ssl-enum-ciphers
```

---

# Phase 7 — Technology Profile

Complete:

| Category | Finding |
|----------|----------|
| Operating System | |
| Web Server | |
| SSH | |
| Database | |
| File Sharing | |
| Other Technologies | |

---

# Phase 8 — Prioritization

Rank services according to the value of additional enumeration.

| Priority | Service | Reason |
|----------|----------|--------|
| High | | |
| Medium | | |
| Low | | |

Remember that priorities depend on collected evidence, not assumptions.

---

# Phase 9 — Reconnaissance Notes

Create a structured summary.

## Open Ports

## Services

## Versions

## Operating System

## Interesting Findings

## Questions for Further Investigation

---

# Assessment Checklist

☐ Host reachable

☐ Full TCP scan completed

☐ Version detection completed

☐ OS detection completed

☐ NSE enumeration completed

☐ Technology profile completed

☐ Priorities identified

☐ Documentation completed

---

# Decision Tree

```
Target

↓

Discover Ports

↓

Identify Services

↓

Select NSE Scripts

↓

Collect Evidence

↓

Create Technology Profile

↓

Prioritize Investigation

↓

Prepare Next Phase
```

---

# Thinking Like a CTF Player

Instead of asking:

> "Which exploit should I try?"

Ask:

- What technologies are present?
- Which services expose the most information?
- Which findings deserve additional investigation?
- Have I documented everything before moving forward?

Strong reconnaissance often determines the success of the rest of the challenge.

---

# Reporting Template

## Target

## Scan Methodology

## Open Ports

## Service Inventory

## Operating System

## Technology Profile

## Enumeration Results

## Observations

## Next Investigation Steps

---

# Challenge

Perform a complete reconnaissance assessment against a CTF target.

Prepare:

- Port inventory
- Service inventory
- Technology profile
- Enumeration notes
- Prioritized investigation plan

---

# Bonus Challenge

Design a reusable reconnaissance workflow using Nmap that includes:

- Full TCP Scan
- Service Detection
- OS Detection
- Default NSE Scripts
- Service-Specific NSE Scripts
- Structured Output

Save the results as:

```bash
-oA ctf_recon
```

---

# Key Takeaways

- Successful CTF players rely on structured reconnaissance rather than guesswork.
- Service-specific NSE scripts provide valuable information for understanding a target.
- A technology profile helps organize findings and guide further investigation.
- Documentation reduces repeated work and improves analysis.
- Evidence-based decision-making is essential throughout the assessment.

---

# Next Lab

➡ **Lab 30 — Final Capstone Challenge**