# Part 03 — Nmap Scripting Engine (NSE)

> Learn how to automate reconnaissance, service enumeration, and security checks using the Nmap Scripting Engine.

---

# Overview

The Nmap Scripting Engine (NSE) is one of Nmap's most powerful features.

While traditional Nmap scans identify hosts, ports, and services, NSE extends Nmap by allowing scripts to interact with discovered services and collect significantly more information.

NSE scripts can:

- Gather additional information
- Enumerate services
- Detect security misconfigurations
- Identify supported protocols
- Retrieve certificates
- Query DNS servers
- Test authentication
- Perform safe vulnerability checks

Understanding NSE transforms Nmap from a port scanner into a flexible network reconnaissance framework.

---

# Learning Objectives

After completing this section, you will be able to:

- Execute default NSE scripts
- Select scripts by category
- Use protocol-specific scripts
- Interpret script output
- Perform safe vulnerability checks
- Execute custom scripts
- Understand how NSE integrates into reconnaissance workflows

---

# Learning Path

```text
Default Scripts
        │
        ▼
HTTP Enumeration
        │
        ▼
SMB Enumeration
        │
        ▼
FTP Enumeration
        │
        ▼
SSL/TLS Enumeration
        │
        ▼
DNS Enumeration
        │
        ▼
Vulnerability Detection
        │
        ▼
Custom NSE Scripts
```

---

# Labs Included

## Lab 11 — Default Scripts

Learn how to use the default NSE script set.

---

## Lab 12 — HTTP Scripts

Enumerate web servers using HTTP-related NSE scripts.

---

## Lab 13 — SMB Scripts

Collect information from SMB services.

---

## Lab 14 — FTP Scripts

Analyze FTP servers and authentication settings.

---

## Lab 15 — SSL Scripts

Inspect SSL/TLS configurations and certificates.

---

## Lab 16 — DNS Scripts

Enumerate DNS infrastructure and records.

---

## Lab 17 — Vulnerability Scripts

Use safe vulnerability detection scripts.

---

## Lab 18 — Custom Script Test

Execute and customize NSE scripts while understanding their role in automation.

---

# Estimated Completion Time

Approximately **8–10 Hours**

---

# Recommended Practice Targets

- Metasploitable 2
- Metasploitable 3
- OWASP Broken Web Apps
- DVWA
- Ubuntu Server
- Windows Server Evaluation

---

# Next Step

Continue with **Lab 11 — Default Scripts**.