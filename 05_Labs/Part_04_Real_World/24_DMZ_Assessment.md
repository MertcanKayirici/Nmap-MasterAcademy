# Lab 24 — DMZ Assessment

> Perform a structured assessment of a Demilitarized Zone (DMZ) by identifying exposed services, understanding network segmentation, and documenting publicly accessible infrastructure.

---

# Overview

A Demilitarized Zone (DMZ) is a network segment positioned between an organization's internal network and the Internet.

Its purpose is to expose selected services to external users while protecting the internal network.

Typical DMZ systems include:

- Web Servers
- Reverse Proxies
- Mail Servers
- VPN Gateways
- DNS Servers
- Load Balancers
- Web Application Firewalls (WAF)

This lab focuses on identifying systems within a DMZ and understanding their roles through structured reconnaissance.

No exploitation is performed.

---

# Learning Objectives

After completing this lab, you will be able to:

- Identify public-facing hosts.
- Enumerate exposed services.
- Recognize common DMZ architectures.
- Identify server roles.
- Build a DMZ asset inventory.
- Produce a professional assessment report.

---

# Difficulty

⭐⭐⭐⭐⭐

---

# Estimated Time

2–3 Hours

---

# Prerequisites

- Parts 01–03 completed
- Previous Real World labs completed
- Understanding of basic network segmentation

---

# Lab Environment

| Host | IP Address | Role |
|------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| WEB01 | 192.168.56.20 | Public Web Server |
| MAIL01 | 192.168.56.21 | Mail Server |
| DNS01 | 192.168.56.22 | Public DNS |
| VPN01 | 192.168.56.23 | VPN Gateway |
| FW01 | 192.168.56.1 | Firewall |

---

# Scenario

Your organization requests an inventory of systems deployed inside the DMZ.

Your objectives are:

- Identify every reachable host.
- Determine each server's role.
- Enumerate exposed services.
- Document findings.
- Produce recommendations.

No authentication attempts or exploitation are authorized.

---

# Understanding a DMZ

Example architecture:

```
                 Internet
                     │
             ┌────────────┐
             │ Firewall   │
             └────────────┘
                     │
          ┌────────────────────┐
          │        DMZ         │
          │                    │
          │ WEB01              │
          │ MAIL01             │
          │ DNS01              │
          │ VPN01              │
          └────────────────────┘
                     │
             ┌────────────┐
             │ Internal   │
             │ Network    │
             └────────────┘
```

The DMZ acts as a buffer between external users and internal resources.

---

# Assessment Workflow

```
Host Discovery

↓

Host Classification

↓

Port Scan

↓

Service Detection

↓

NSE Enumeration

↓

Infrastructure Analysis

↓

Asset Inventory

↓

Reporting
```

---

# Phase 1 — Discover Live Hosts

```bash
nmap -sn 192.168.56.0/24
```

Document:

- Live hosts
- IP addresses
- Response times

---

# Phase 2 — Scan Every Host

Example:

```bash
nmap 192.168.56.20
```

Repeat for every discovered system.

Document:

- Open ports
- Closed ports
- Filtered ports

---

# Phase 3 — Full TCP Scan

```bash
nmap -p- 192.168.56.20
```

Questions:

- Are management ports exposed?
- Are uncommon services present?

---

# Phase 4 — Service Detection

```bash
nmap -sV 192.168.56.20
```

Record:

- Service
- Vendor
- Version

---

# Phase 5 — Execute Default Scripts

```bash
nmap -sC -sV 192.168.56.20
```

Review:

- HTTP information
- SSL certificates
- SSH host keys
- Service banners

Repeat for each host.

---

# Phase 6 — Identify Server Roles

Example observations:

| Services | Possible Role |
|----------|---------------|
| 80,443 | Web Server |
| 25,587,993 | Mail Server |
| 53 | DNS Server |
| 443,1194,500,4500 | VPN Gateway |
| 80,443,8080 | Reverse Proxy |

Remember that service combinations suggest a role but do not confirm it. Validate assumptions with authorized documentation whenever possible.

---

# Phase 7 — Asset Inventory

| Host | Role | OS | Services | Notes |
|------|------|----|----------|------|
| WEB01 | | | | |
| MAIL01 | | | | |
| DNS01 | | | | |
| VPN01 | | | | |

---

# Phase 8 — Exposure Review

For each host ask:

- Which services are Internet-facing?
- Are administrative interfaces exposed?
- Are unnecessary services visible?
- Does the observed role match the exposed services?

---

# Assessment Checklist

☐ Host discovery completed

☐ Full TCP scan completed

☐ Service detection completed

☐ NSE enumeration completed

☐ Asset inventory prepared

☐ Server roles identified

☐ Findings documented

☐ Recommendations prepared

---

# Decision Tree

```
Host Found

↓

Identify Services

↓

Determine Role

↓

Run Relevant NSE Scripts

↓

Analyze Exposure

↓

Document Findings

↓

Continue With Next Host
```

---

# Thinking Like an Analyst

Suppose the scan reveals:

```text
80
443
22
```

Questions:

- Is SSH expected on a public web server?
- Should administrative access be restricted?
- Are additional web services exposed?

---

Another Example

```text
25
465
587
993
```

Questions:

- Does this appear to be a mail server?
- Are secure mail protocols available?
- Which additional mail-related services might exist?

---

# Reporting Template

## Executive Summary

## Scope

## Methodology

## Discovered Hosts

## Service Inventory

## Infrastructure Roles

## Public Exposure Summary

## Observations

## Recommendations

---

# Challenge

Assess every host within the DMZ.

Produce:

- Asset inventory
- Service inventory
- Infrastructure map
- Exposure summary
- Final assessment report

---

# Bonus Challenge

Create a reusable Nmap workflow that performs:

- Host Discovery
- Full TCP Scan
- Service Detection
- OS Detection
- Default NSE Scripts
- Output Saving

Save the results using:

```bash
-oA dmz_assessment
```

---

# Key Takeaways

- DMZ assessments focus on understanding exposed infrastructure rather than individual hosts alone.
- Host roles can often be inferred from service combinations.
- Asset inventories provide valuable operational visibility.
- Public-facing systems should be documented carefully and reviewed regularly.
- A structured workflow improves consistency across large environments.

---

# Next Lab

➡ **Lab 25 — Full Infrastructure Assessment**

In the final lab of this section, you will combine every technique learned throughout the course into a complete enterprise-style infrastructure assessment, from host discovery to reporting.