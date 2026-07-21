# Lab 25 — Full Infrastructure Assessment (Capstone)

> Conduct a complete enterprise infrastructure assessment using Nmap and the Nmap Scripting Engine (NSE), from host discovery to professional reporting.

---

# Overview

This capstone lab combines every major concept covered throughout the Nmap Master Academy.

Unlike previous labs, which focused on individual technologies or environments, this assessment simulates a complete enterprise network.

You will perform a structured reconnaissance process, identify hosts, classify services, analyze operating systems, execute relevant NSE scripts, organize findings, and prepare a professional assessment report.

The objective is to demonstrate a repeatable methodology rather than simply execute commands.

No exploitation is performed.

---

# Learning Objectives

After completing this lab, you will be able to:

- Plan an infrastructure assessment.
- Discover live hosts.
- Build an enterprise asset inventory.
- Identify operating systems.
- Detect running services.
- Select appropriate NSE scripts.
- Analyze collected information.
- Classify server roles.
- Document findings professionally.
- Produce a final assessment report.

---

# Difficulty

⭐⭐⭐⭐⭐

Capstone

---

# Estimated Time

3–5 Hours

---

# Prerequisites

- Complete Parts 01–04
- Familiarity with NSE
- Basic networking knowledge
- Authorized assessment environment

---

# Enterprise Scenario

You have joined the infrastructure team of a medium-sized company.

The organization has no current network documentation.

Management requests a complete infrastructure inventory.

Only reconnaissance is authorized.

Your objectives are to:

- Identify every reachable host.
- Determine server roles.
- Enumerate exposed services.
- Build an infrastructure inventory.
- Produce recommendations.

---

# Network Diagram

```
                    Internet
                         │
                 ┌──────────────┐
                 │ Firewall     │
                 └──────────────┘
                         │
                ┌─────────────────┐
                │ DMZ             │
                │                 │
                │ WEB01           │
                │ MAIL01          │
                │ VPN01           │
                └─────────────────┘
                         │
        ┌────────────────────────────────┐
        │ Internal Network               │
        │                                │
        │ DC01                           │
        │ FILE01                         │
        │ DB01                           │
        │ APP01                          │
        │ LINUX01                        │
        │ CLIENT01                       │
        │ CLIENT02                       │
        └────────────────────────────────┘
```

---

# Assessment Workflow

```
Planning

↓

Host Discovery

↓

Asset Inventory

↓

Port Scanning

↓

Service Detection

↓

OS Detection

↓

NSE Enumeration

↓

Infrastructure Analysis

↓

Risk Review

↓

Reporting
```

---

# Phase 1 — Planning

Before scanning:

Answer:

- What is the assessment scope?
- Which network ranges are included?
- Which systems are expected?
- What authorization has been provided?

Document the answers.

---

# Phase 2 — Host Discovery

```bash
nmap -sn 192.168.10.0/24
```

Record:

- Live hosts
- Response times
- Address ranges

---

# Phase 3 — Asset Inventory

For every discovered system create:

| IP | Hostname | Role | Status |
|----|----------|------|--------|

---

# Phase 4 — Initial Port Scan

```bash
nmap target
```

Repeat for every host.

---

# Phase 5 — Full Port Scan

```bash
nmap -p- target
```

Record:

- Open ports
- Filtered ports
- Closed ports

---

# Phase 6 — Service Detection

```bash
nmap -sV target
```

Document:

- Service
- Version
- Vendor

---

# Phase 7 — Operating System Detection

```bash
nmap -O target
```

Document:

- Operating system
- Confidence
- Device type

---

# Phase 8 — NSE Enumeration

Use scripts appropriate for the discovered services.

Examples:

HTTP

```bash
http-title
http-headers
http-methods
```

SMB

```bash
smb-os-discovery
smb-protocols
smb-security-mode
```

SSL

```bash
ssl-cert
ssl-enum-ciphers
```

Database

```bash
mysql-info
pgsql-info
ms-sql-info
```

Document every result.

---

# Phase 9 — Infrastructure Classification

Identify:

- Domain Controllers
- Web Servers
- Linux Servers
- Database Servers
- Mail Servers
- DNS Servers
- VPN Gateways
- File Servers

Explain why you assigned each role.

---

# Phase 10 — Technology Inventory

Complete:

| Host | OS | Services | Technologies |
|------|----|-----------|--------------|

---

# Phase 11 — Network Observations

Answer:

- Which operating systems dominate?
- Which services are most common?
- Which hosts provide infrastructure services?
- Which hosts appear Internet-facing?

Support every conclusion using the collected evidence.

---

# Phase 12 — Exposure Review

Review every host.

Questions:

- Are administrative services exposed?
- Are legacy protocols present?
- Are unnecessary services running?
- Does the configuration appear consistent with the host's role?

Document observations without making unsupported assumptions.

---

# Phase 13 — Assessment Checklist

☐ Scope confirmed

☐ Host discovery completed

☐ Asset inventory created

☐ Port scans completed

☐ Service detection completed

☐ OS detection completed

☐ NSE enumeration completed

☐ Infrastructure roles identified

☐ Documentation completed

☐ Final report prepared

---

# Phase 14 — Executive Report

Prepare a report containing:

## Executive Summary

## Scope

## Methodology

## Network Overview

## Asset Inventory

## Operating Systems

## Service Inventory

## Technology Stack

## Host Profiles

## Infrastructure Roles

## Observations

## Recommendations

## Conclusion

---

# Decision Tree

```
Assessment Begins

↓

Discover Hosts

↓

Scan Services

↓

Detect Versions

↓

Run NSE

↓

Classify Systems

↓

Review Exposure

↓

Create Report

↓

Assessment Complete
```

---

# Thinking Like an Infrastructure Analyst

Rather than asking:

> "Which ports are open?"

Ask:

- What is the purpose of this host?
- Does the service combination match its expected role?
- Which infrastructure components depend on it?
- Does the observed configuration align with organizational expectations?
- Which findings should be communicated to administrators for review?

---

# Deliverables

By the end of this lab you should produce:

- Asset Inventory
- Service Inventory
- Technology Inventory
- Host Profiles
- Infrastructure Classification
- Assessment Checklist
- Executive Summary
- Technical Report

---

# Final Challenge

Perform a complete assessment of the entire environment using the workflow developed throughout this course.

Your final report should allow another administrator to understand:

- The infrastructure
- The services
- The server roles
- The technologies in use

without needing to repeat your assessment.

---

# Course Completion

Congratulations!

You have completed:

✅ Part 01 — Basic Scanning

✅ Part 02 — Enumeration

✅ Part 03 — NSE

✅ Part 04 — Real World Assessments

You now possess a structured methodology for using Nmap in authorized network discovery, service enumeration, infrastructure documentation, and assessment workflows.

The next parts of the academy will build on these skills by applying them to intentionally vulnerable environments and large-scale automation.

---

# Next Part

➡ **Part 05 — CTF and Hack The Box**