# Lab 21 — Windows Server Assessment

> Perform a structured assessment of a Windows server using Nmap to identify exposed services, operating system details, and Windows-specific infrastructure components.

---

# Overview

Windows servers are commonly used to provide critical enterprise services such as:

- Active Directory
- DNS
- DHCP
- File Sharing
- Remote Desktop Services
- Certificate Services
- IIS Web Hosting

A proper assessment begins by identifying exposed services, determining the server's role, and collecting technical information that can assist administrators in understanding the system.

This lab focuses entirely on reconnaissance and documentation.

---

# Learning Objectives

After completing this lab, you will be able to:

- Detect Windows-specific services.
- Identify the operating system.
- Enumerate SMB services.
- Recognize Active Directory indicators.
- Identify remote management services.
- Produce a structured infrastructure report.

---

# Difficulty

⭐⭐⭐⭐☆

---

# Estimated Time

90–120 Minutes

---

# Prerequisites

- Parts 01–03 completed
- Basic knowledge of Windows networking
- Windows Server target

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| WIN-SRV01 | 192.168.56.30 | Windows Server |

---

# Scenario

A newly deployed Windows server has been added to the corporate network.

Your objectives are:

- Identify exposed services.
- Determine the server role.
- Enumerate SMB.
- Detect management interfaces.
- Document infrastructure information.

No exploitation is authorized.

---

# Assessment Workflow

```
Host Discovery

↓

Port Scan

↓

Service Detection

↓

OS Detection

↓

SMB Enumeration

↓

Windows Service Analysis

↓

Documentation
```

---

# Phase 1 — Verify Connectivity

```bash
ping -c 4 192.168.56.30
```

Record:

- Latency
- Packet loss
- Reachability

---

# Phase 2 — Initial Port Scan

```bash
nmap 192.168.56.30
```

Typical Windows services may include:

```text
53    DNS
88    Kerberos
135   RPC
139   NetBIOS
389   LDAP
445   SMB
464   Kerberos Password Change
593   RPC over HTTP
636   LDAPS
3268  Global Catalog
3389  RDP
5985  WinRM
5986  WinRM HTTPS
```

---

# Phase 3 — Full TCP Scan

```bash
nmap -p- 192.168.56.30
```

Questions:

- Are administrative ports exposed?
- Are unexpected services present?

---

# Phase 4 — Service Detection

```bash
nmap -sV 192.168.56.30
```

Document:

- Service
- Version
- Vendor
- Port

---

# Phase 5 — Operating System Detection

```bash
nmap -O 192.168.56.30
```

Record:

- Estimated OS
- Confidence
- Device type

---

# Phase 6 — SMB Enumeration

```bash
nmap --script smb-os-discovery -p445 192.168.56.30
```

```bash
nmap --script smb-protocols -p445 192.168.56.30
```

```bash
nmap --script smb-security-mode -p445 192.168.56.30
```

```bash
nmap --script smb-enum-shares -p445 192.168.56.30
```

Document:

- Computer name
- Domain/Workgroup
- SMB versions
- Shares
- Security mode

---

# Phase 7 — Detect Remote Management Services

Review results for:

- RDP (3389)
- WinRM (5985/5986)
- RPC (135)
- SMB (445)

Questions:

- Which remote administration methods are available?
- Are they expected for this server role?

---

# Phase 8 — Active Directory Indicators

If the following services are present:

```text
53
88
389
445
3268
```

Consider:

- Could this be a Domain Controller?
- Is the server providing directory services?
- Which enterprise services appear to be installed?

---

# Phase 9 — Default NSE Enumeration

```bash
nmap -sC -sV 192.168.56.30
```

Review:

- Hostname
- SSL certificates
- SMB information
- Additional service details

---

# Infrastructure Inventory

| Category | Finding |
|----------|----------|
| Hostname | |
| Operating System | |
| Domain | |
| Computer Name | |
| SMB Version | |
| Remote Management | |
| Open Ports | |
| Installed Services | |

---

# Windows Service Reference

| Port | Service | Typical Purpose |
|------|----------|-----------------|
| 53 | DNS | Name Resolution |
| 88 | Kerberos | Authentication |
| 135 | RPC | Remote Procedure Calls |
| 139 | NetBIOS | Legacy SMB Support |
| 389 | LDAP | Directory Services |
| 445 | SMB | File Sharing |
| 636 | LDAPS | Secure LDAP |
| 3268 | Global Catalog | Active Directory |
| 3389 | RDP | Remote Desktop |
| 5985 | WinRM | Remote Management |

---

# Decision Tree

```
Windows Host

↓

Detect Services

↓

Identify Server Role

↓

Enumerate SMB

↓

Review Management Services

↓

Analyze Findings

↓

Create Report
```

---

# Thinking Like an Analyst

Suppose the scan reveals:

```text
53
88
389
445
3268
```

Questions:

- Is this likely a Domain Controller?
- Which directory services are available?
- Which authentication mechanisms are present?

---

Another Example

```text
3389

5985
```

Questions:

- Which remote administration protocols are enabled?
- Are both required for the server's role?
- Should administrators verify their exposure?

---

# Reporting Template

## Executive Summary

## Scope

## Methodology

## Operating System

## Open Services

## SMB Findings

## Active Directory Indicators

## Remote Management

## Recommendations

---

# Challenge

Perform a complete assessment and document:

- Windows version
- Server role
- SMB configuration
- Active Directory indicators
- Remote administration services
- Infrastructure summary

---

# Bonus Challenge

Create a single Nmap command that performs:

- Service Detection
- OS Detection
- Default NSE Scripts
- SMB Enumeration

Save the output as:

```bash
-oA windows_assessment
```

---

# Key Takeaways

- Windows servers expose characteristic service combinations that help identify their role.
- SMB enumeration provides valuable information about the system and its configuration.
- Active Directory-related services can often be recognized through their network ports.
- Remote management interfaces should be documented and reviewed as part of every assessment.
- A structured workflow improves both consistency and reporting quality.

---

# Next Lab

➡ **Lab 22 — Linux Server Assessment**

In the next lab, you will assess a Linux server by identifying common services such as SSH, Apache/Nginx, databases, and other Unix-based components while building a comprehensive infrastructure profile.