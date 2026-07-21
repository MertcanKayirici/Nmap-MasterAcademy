# Lab 20 — Web Server Assessment

> Perform a structured assessment of a web server using Nmap and the Nmap Scripting Engine (NSE).

---

# Overview

Web servers are among the most frequently assessed systems in modern IT environments.

A web server may host:

- Corporate websites
- Internal applications
- APIs
- Administrative portals
- Customer-facing services

The objective of this lab is to identify exposed services, collect technical information, enumerate web technologies, and document observations using a structured methodology.

This assessment focuses on reconnaissance and information gathering rather than exploitation.

---

# Learning Objectives

After completing this lab, you will be able to:

- Identify HTTP and HTTPS services.
- Detect web server software.
- Retrieve HTTP headers.
- Inspect SSL/TLS certificates.
- Enumerate supported HTTP methods.
- Gather information using HTTP-related NSE scripts.
- Produce a structured assessment report.

---

# Difficulty

⭐⭐⭐⭐☆

---

# Estimated Time

90–120 Minutes

---

# Prerequisites

- Parts 01–03 completed
- Basic understanding of HTTP and HTTPS
- Target with an active web server

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| WEB01 | 192.168.56.20 | Web Server |

---

# Scenario

A newly deployed web server has been added to the network.

Your task is to:

- Identify running services.
- Determine server software.
- Enumerate HTTP features.
- Collect SSL/TLS information.
- Document the results.

No further testing is authorized.

---

# Assessment Workflow

```
Host Discovery

↓

Port Scan

↓

Service Detection

↓

HTTP Enumeration

↓

SSL Enumeration

↓

Analysis

↓

Documentation
```

---

# Phase 1 — Host Verification

Run:

```bash
ping -c 4 192.168.56.20
```

Confirm:

- Host is reachable.
- Round-trip time.
- Packet loss.

---

# Phase 2 — Initial Port Scan

```bash
nmap 192.168.56.20
```

Example

```text
80/tcp open http

443/tcp open https
```

---

# Phase 3 — Full Port Scan

```bash
nmap -p- 192.168.56.20
```

Questions:

- Are additional services exposed?
- Are management ports accessible?

---

# Phase 4 — Service Detection

```bash
nmap -sV 192.168.56.20
```

Example

```text
Apache httpd 2.4.57

OpenSSL
```

Document:

- Service
- Version
- Vendor

---

# Phase 5 — HTTP Enumeration

Retrieve page title:

```bash
nmap --script http-title 192.168.56.20
```

Retrieve headers:

```bash
nmap --script http-headers 192.168.56.20
```

Retrieve server banner:

```bash
nmap --script http-server-header 192.168.56.20
```

Enumerate methods:

```bash
nmap --script http-methods 192.168.56.20
```

Check robots.txt:

```bash
nmap --script http-robots.txt 192.168.56.20
```

---

# Phase 6 — HTTPS Enumeration

Retrieve certificate:

```bash
nmap --script ssl-cert -p443 192.168.56.20
```

Enumerate ciphers:

```bash
nmap --script ssl-enum-ciphers -p443 192.168.56.20
```

Review:

- Certificate subject
- Issuer
- Validity period
- Supported TLS versions

---

# Phase 7 — Default NSE Scripts

Run:

```bash
nmap -sC -sV 192.168.56.20
```

Review all additional information returned by the default scripts.

---

# Phase 8 — Organize Findings

Complete the table below.

| Category | Finding |
|----------|----------|
| Web Server | |
| Version | |
| HTTP Methods | |
| Page Title | |
| Server Header | |
| SSL Certificate | |
| TLS Versions | |
| Interesting Observations | |

---

# Building a Technology Profile

Based on the collected information, answer:

- Which web server software is running?
- Which operating system is likely in use?
- Is encryption enabled?
- Which HTTP methods are supported?
- Are default pages present?
- Are administrative interfaces visible?

---

# Decision Tree

```
HTTP Service Found

↓

Identify Server

↓

Enumerate Headers

↓

Enumerate Methods

↓

Inspect Certificate

↓

Analyze Configuration

↓

Document Findings
```

---

# Reporting Template

## Executive Summary

## Scope

## Methodology

## Open Ports

## Web Technologies

## HTTP Findings

## HTTPS Findings

## Observations

## Recommendations

---

# Challenge

Perform a complete assessment of the web server and create:

- Service inventory
- Web technology profile
- SSL/TLS summary
- HTTP analysis
- Final report

---

# Bonus Challenge

Create a single Nmap command that performs:

- Version detection
- Default scripts
- HTTP title retrieval
- HTTP headers
- HTTP methods
- SSL certificate retrieval

Save the output in all formats using:

```bash
-oA web_assessment
```

---

# Key Takeaways

- Web server assessments require more than identifying open ports.
- HTTP-related NSE scripts provide valuable insight into web technologies.
- SSL/TLS inspection complements HTTP enumeration.
- Structured documentation is as important as technical discovery.
- A repeatable workflow improves consistency and reporting quality.

---

# Next Lab

➡ **Lab 21 — Windows Server Assessment**

In the next lab, you will perform a comprehensive assessment of a Windows server, including SMB enumeration, operating system detection, service analysis, and Active Directory-related observations.