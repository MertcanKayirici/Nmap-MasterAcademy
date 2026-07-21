# Nmap Master Academy

# Course 20

# Real-World Workflows

---

## Course Information

**Course Number:** 20

**Difficulty:** Advanced

**Estimated Reading Time:** 180–240 Minutes

**Prerequisites**

- Course 01–19

---

# Table of Contents

1. Introduction
2. Professional Assessment Workflow
3. Internal Network Assessment
4. External Penetration Test
5. Web Server Assessment
6. Active Directory Environment
7. Cloud Environment Assessment
8. Vulnerability Verification
9. Reporting Workflow
10. Common Mistakes
11. Professional Tips
12. Summary

---

# 1. Introduction

Real penetration tests rarely consist of a single Nmap command.

Instead, professionals follow structured workflows that collect information gradually while minimizing unnecessary traffic and maximizing accuracy.

Each phase builds on the results of the previous one.

---

# 2. Professional Assessment Workflow

A typical workflow:

```text
Authorization

↓

Define Scope

↓

Identify Targets

↓

Host Discovery

↓

Port Scanning

↓

Service Detection

↓

Operating System Detection

↓

NSE Enumeration

↓

Validate Findings

↓

Risk Analysis

↓

Reporting
```

Skipping steps often results in incomplete or inaccurate assessments.

---

# 3. Internal Network Assessment

Scenario:

```
Corporate LAN

↓

192.168.10.0/24
```

### Step 1 — Discover Hosts

```bash
nmap -sn 192.168.10.0/24
```

---

### Step 2 — Scan Open Ports

```bash
sudo nmap -sS 192.168.10.15
```

---

### Step 3 — Detect Services

```bash
sudo nmap -sV 192.168.10.15
```

---

### Step 4 — Detect Operating System

```bash
sudo nmap -O 192.168.10.15
```

---

### Step 5 — Run Default NSE Scripts

```bash
sudo nmap -sC 192.168.10.15
```

---

### Step 6 — Save Results

```bash
sudo nmap -oA workstation01 192.168.10.15
```

---

# Internal Assessment Workflow

```text
Host Discovery

↓

Port Scan

↓

Service Detection

↓

OS Detection

↓

NSE

↓

Report
```

---

# 4. External Penetration Test

Scenario

```
Public IP

↓

203.0.113.25
```

External assessments require a more cautious approach.

---

### Initial Scan

```bash
sudo nmap -Pn -sS -T2 target
```

---

### Version Detection

```bash
sudo nmap -sV target
```

---

### HTTP Enumeration

```bash
sudo nmap --script=http-title,http-headers target
```

---

### SSL Analysis

```bash
sudo nmap --script ssl-cert target
```

---

### Save Output

```bash
sudo nmap -oA external_scan target
```

---

# 5. Web Server Assessment

Typical workflow:

```text
HTTP

↓

HTTPS

↓

Version Detection

↓

HTTP Headers

↓

TLS Certificate

↓

Supported Methods

↓

Reporting
```

Example commands:

```bash
nmap -p80,443 -sV target
```

```bash
nmap --script=http-title target
```

```bash
nmap --script=http-methods target
```

```bash
nmap --script=http-headers target
```

```bash
nmap --script ssl-cert target
```

---

# 6. Active Directory Environment

Typical targets include:

- Domain Controllers
- File Servers
- DNS Servers
- Member Servers
- Workstations

Useful ports:

| Port | Service |
|-------|----------|
|53|DNS|
|88|Kerberos|
|135|RPC|
|139|NetBIOS|
|389|LDAP|
|445|SMB|
|636|LDAPS|
|3268|Global Catalog|

Useful commands:

```bash
nmap -p53,88,389,445 target
```

```bash
nmap --script smb-os-discovery target
```

```bash
nmap --script smb-enum-shares target
```

---

# 7. Cloud Environment Assessment

Cloud environments introduce additional considerations.

Possible obstacles:

- Security Groups
- Network ACLs
- Load Balancers
- Reverse Proxies
- Managed Firewalls

Recommended workflow:

```text
Host Discovery

↓

Port Scan

↓

Version Detection

↓

TLS Inspection

↓

NSE

↓

Validation
```

---

# 8. Vulnerability Verification

Never assume a vulnerability exists based solely on a service version.

Instead:

```
Open Port

↓

Version Detection

↓

NSE

↓

Manual Verification

↓

Evidence

↓

Report
```

Verification reduces false positives.

---

# 9. Reporting Workflow

Professional reports should include:

## Scope

What was tested.

---

## Methodology

Which techniques were used.

---

## Findings

Open ports

Services

Operating Systems

Scripts

Evidence

---

## Risk Analysis

Critical

High

Medium

Low

Informational

---

## Recommendations

Examples:

- Disable unnecessary services
- Apply security updates
- Restrict firewall rules
- Enable stronger authentication

---

# Example Assessment Timeline

```text
08:30

Scope Review

↓

08:45

Host Discovery

↓

09:00

Port Scan

↓

09:20

Version Detection

↓

09:45

NSE

↓

10:30

Validation

↓

11:00

Report Writing
```

---

# 10. Common Mistakes

Avoid:

✗ Running aggressive scans immediately

✗ Ignoring UDP

✗ Forgetting IPv6

✗ Assuming filtered means secure

✗ Trusting version detection blindly

✗ Failing to document commands

✗ Forgetting to save scan results

---

# 11. Professional Tips

✓ Start with lightweight scans.

✓ Build information gradually.

✓ Keep scan logs.

✓ Validate important findings.

✓ Document everything.

✓ Protect collected data.

✓ Always follow the agreed assessment scope.

---

# Summary

Professional Nmap usage is based on structured workflows rather than isolated commands.

By combining host discovery, port scanning, service detection, operating system identification, NSE, validation, and reporting, security professionals can perform reliable and repeatable assessments.

The techniques presented throughout this academy provide a solid foundation for conducting network reconnaissance in a responsible and methodical manner.

---

# Final Key Takeaways

✓ Follow a structured workflow.

✓ Start simple and expand gradually.

✓ Validate all important findings.

✓ Save and protect scan results.

✓ Choose scan techniques based on objectives.

✓ Combine multiple Nmap features for comprehensive assessments.

✓ Always operate within the authorized scope.

---

# Congratulations!

You have successfully completed the **Nmap Master Academy**.

You now understand:

- Host Discovery
- Port Scanning
- Service Detection
- Operating System Detection
- Nmap Scripting Engine (NSE)
- Timing and Optimization
- Output and Reporting
- DNS Resolution
- IPv4 & IPv6 Scanning
- Scan Strategies
- Troubleshooting
- Professional Workflows

You are now prepared to use Nmap effectively in security assessments, penetration testing, and network administration while following professional methodologies and ethical practices.

---

# What's Next?

After mastering Nmap, consider exploring:

- Wireshark (Packet Analysis)
- NetExec (SMB and Active Directory Enumeration)
- Burp Suite (Web Application Security)
- Gobuster / FFUF (Content Discovery)
- SQLMap (SQL Injection Testing)
- Metasploit Framework (Exploitation)
- CrackMapExec Alternatives
- Nessus / OpenVAS (Vulnerability Assessment)