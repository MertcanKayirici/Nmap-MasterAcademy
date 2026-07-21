# Lab 19 — Internal Network Assessment

> Perform a structured assessment of an internal network using Nmap.

---

# Overview

Internal network assessments are one of the most common tasks performed by system administrators and security professionals.

Unlike Internet-facing systems, internal environments often contain many devices with different operating systems, services, and roles.

The objective of this lab is to discover hosts, identify services, and document the internal infrastructure.

---

# Learning Objectives

After completing this lab, you will be able to:

- Discover live hosts
- Identify critical systems
- Detect open ports
- Perform service detection
- Enumerate services
- Organize findings into a report

---

# Difficulty

⭐⭐⭐⭐☆

---

# Estimated Time

90 Minutes

---

# Scenario

You have been assigned to review an internal corporate subnet.

Known Information:

```
Network:

192.168.10.0/24

No asset inventory is available.
```

Your task is to build one.

---

# Lab Environment

| Device | Expected Role |
|---------|---------------|
| DC01 | Domain Controller |
| WEB01 | Web Server |
| FILE01 | File Server |
| DB01 | Database Server |
| CLIENT01 | Windows Workstation |
| CLIENT02 | Linux Workstation |

---

# Phase 1 — Host Discovery

Run:

```bash
nmap -sn 192.168.10.0/24
```

Questions:

- How many hosts responded?
- Which IP addresses are active?

---

# Phase 2 — Initial Port Scan

Choose one host.

Run:

```bash
nmap 192.168.10.15
```

Document:

- Open ports
- Closed ports
- Filtered ports

---

# Phase 3 — Full Port Scan

```bash
nmap -p- 192.168.10.15
```

Why?

Many enterprise services use non-standard ports.

---

# Phase 4 — Service Detection

```bash
nmap -sV 192.168.10.15
```

Record:

- Service
- Version
- Vendor

---

# Phase 5 — Operating System Detection

```bash
nmap -O 192.168.10.15
```

Estimate:

- Operating System
- Confidence
- Device Type

---

# Phase 6 — NSE Enumeration

```bash
nmap -sC -sV 192.168.10.15
```

Review:

- HTTP titles
- SSL certificates
- SMB information
- SSH host keys

---

# Phase 7 — Build an Asset Inventory

| IP | Hostname | OS | Services | Notes |
|----|----------|----|----------|------|
| | | | | |

Complete this table for every discovered host.

---

# Phase 8 — Risk Review

For each host ask:

- Is this expected?
- Which services are unnecessary?
- Are legacy protocols present?
- Are administrative interfaces exposed?

---

# Reporting Template

## Executive Summary

## Scope

## Methodology

## Hosts Discovered

## Open Services

## Interesting Findings

## Recommendations

---

# Decision Tree

```
Host Found

↓

Port Scan

↓

Services Found

↓

Version Detection

↓

NSE

↓

Document

↓

Next Host
```

---

# Challenge

Assess every host inside the subnet.

Produce:

- Asset inventory
- Service inventory
- Network observations
- Recommendations

---

# Key Takeaways

- Internal assessments require systematic enumeration.
- Asset inventory is often the first deliverable.
- Every discovered service should be documented.
- Consistency is critical in large environments.

---

# Next Lab

➡ **Lab 20 — Web Server Assessment**