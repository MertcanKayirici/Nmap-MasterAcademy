# Lab 22 — Linux Server Assessment

> Perform a structured assessment of a Linux server using Nmap to identify operating system characteristics, exposed services, and infrastructure roles.

---

# Overview

Linux servers power a large portion of modern infrastructure, including:

- Web Servers
- Database Servers
- DNS Servers
- Mail Servers
- Reverse Proxies
- Containers
- Virtualization Hosts
- Storage Servers

Unlike Windows environments, Linux systems often expose different combinations of services depending on their purpose.

The goal of this lab is to identify those services and build a complete infrastructure profile using Nmap.

This assessment focuses exclusively on reconnaissance and documentation.

---

# Learning Objectives

After completing this lab, you will be able to:

- Identify Linux-based services.
- Estimate the operating system.
- Enumerate SSH.
- Detect web services.
- Identify infrastructure roles.
- Build a structured assessment report.

---

# Difficulty

⭐⭐⭐⭐☆

---

# Estimated Time

90–120 Minutes

---

# Prerequisites

- Parts 01–03 completed
- Basic Linux networking knowledge
- Linux server target

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| LINUX-SRV01 | 192.168.56.40 | Linux Server |

---

# Scenario

A Linux server has recently been deployed.

Your objectives are:

- Identify exposed services.
- Determine the server's role.
- Analyze SSH configuration.
- Enumerate web services.
- Document infrastructure information.

No configuration changes or exploitation are authorized.

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

SSH Enumeration

↓

Web Enumeration

↓

Infrastructure Analysis

↓

Documentation
```

---

# Phase 1 — Verify Connectivity

```bash
ping -c 4 192.168.56.40
```

Document:

- Reachability
- Average latency
- Packet loss

---

# Phase 2 — Initial Port Scan

```bash
nmap 192.168.56.40
```

Typical Linux services may include:

```text
22     SSH
80     HTTP
111    RPCBind
443    HTTPS
2049   NFS
3306   MySQL
5432   PostgreSQL
6379   Redis
8080   HTTP Alternate
9000   Application Service
```

---

# Phase 3 — Full TCP Scan

```bash
nmap -p- 192.168.56.40
```

Questions:

- Are any services using non-standard ports?
- Are management interfaces exposed?

---

# Phase 4 — Service Detection

```bash
nmap -sV 192.168.56.40
```

Record:

- Service
- Version
- Vendor

Example:

```text
OpenSSH 9.x

Apache httpd

nginx

MySQL
```

---

# Phase 5 — Operating System Detection

```bash
nmap -O 192.168.56.40
```

Document:

- Estimated OS
- Kernel family
- Confidence

---

# Phase 6 — SSH Enumeration

Run:

```bash
nmap --script ssh-hostkey -p22 192.168.56.40
```

Document:

- RSA key
- ECDSA key
- ED25519 key

Questions:

- Which host keys are available?
- Are multiple algorithms supported?

---

# Phase 7 — Web Enumeration

If HTTP is available:

```bash
nmap --script http-title,http-headers,http-methods 192.168.56.40
```

If HTTPS is available:

```bash
nmap --script ssl-cert,ssl-enum-ciphers -p443 192.168.56.40
```

Document:

- Page title
- Server banner
- HTTP methods
- TLS versions
- Certificate details

---

# Phase 8 — Infrastructure Role Identification

Based on discovered services, determine the most likely server role.

Examples:

| Services | Possible Role |
|----------|---------------|
| 22,80,443 | Web Server |
| 22,3306 | Database Server |
| 22,2049 | File Server |
| 22,53 | DNS Server |
| 22,25 | Mail Server |

Remember that these are hypotheses based on observed services and should be confirmed through authorized administrative processes.

---

# Phase 9 — Default NSE Enumeration

Run:

```bash
nmap -sC -sV 192.168.56.40
```

Review:

- SSH keys
- HTTP information
- SSL details
- Additional service data

---

# Linux Infrastructure Inventory

| Category | Finding |
|----------|----------|
| Hostname | |
| Operating System | |
| SSH Version | |
| Web Server | |
| Database | |
| Open Ports | |
| Server Role | |
| Notes | |

---

# Common Linux Services

| Port | Service | Typical Purpose |
|------|----------|-----------------|
| 22 | SSH | Remote Administration |
| 80 | HTTP | Web Hosting |
| 443 | HTTPS | Secure Web Hosting |
| 111 | RPCBind | RPC Service Mapping |
| 2049 | NFS | Network File Sharing |
| 3306 | MySQL | Database |
| 5432 | PostgreSQL | Database |
| 6379 | Redis | In-Memory Data Store |
| 8080 | HTTP Alternate | Web Applications |

---

# Decision Tree

```
Linux Host

↓

Detect Services

↓

Identify Server Role

↓

Enumerate SSH

↓

Enumerate Web Services

↓

Analyze Infrastructure

↓

Create Report
```

---

# Thinking Like an Analyst

Suppose the scan reports:

```text
22
80
443
3306
```

Questions:

- Is this an application server?
- Does the service combination match the expected architecture?
- Which service is likely the primary function of the host?

---

Another Example

```text
22
2049
111
```

Questions:

- Could this be a network file server?
- Is RPCBind expected?
- Which clients might depend on this service?

---

# Reporting Template

## Executive Summary

## Scope

## Methodology

## Operating System

## Open Services

## SSH Findings

## Web Findings

## Infrastructure Role

## Recommendations

---

# Challenge

Perform a complete Linux server assessment and document:

- Operating system estimate
- Open ports
- Service versions
- SSH details
- Web technologies (if applicable)
- Likely server role
- Infrastructure summary

---

# Bonus Challenge

Create a single Nmap command that performs:

- Service Detection
- OS Detection
- Default NSE Scripts
- SSH Enumeration
- HTTP Enumeration
- SSL Enumeration (if available)

Save the output as:

```bash
-oA linux_assessment
```

---

# Key Takeaways

- Linux servers often expose service combinations that reveal their infrastructure role.
- SSH enumeration provides valuable identification information.
- HTTP and HTTPS services can be analyzed using dedicated NSE scripts.
- Service combinations help build a technical profile of the host, but conclusions should be validated.
- A structured workflow improves repeatability, documentation, and operational consistency.

---

# Next Lab

➡ **Lab 23 — Database Server Assessment**

In the next lab, you will assess database servers by identifying database services, detecting versions, and documenting database-related infrastructure using Nmap and NSE.