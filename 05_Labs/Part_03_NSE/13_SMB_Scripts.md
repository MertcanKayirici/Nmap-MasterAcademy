# Lab 13 — SMB Scripts

> Learn how to enumerate SMB services using Nmap NSE scripts and identify valuable information exposed by Windows file-sharing services.

---

# Overview

Server Message Block (SMB) is one of the most important network protocols in Windows environments.

SMB provides services such as:

- File Sharing
- Printer Sharing
- Remote Administration
- Authentication
- Named Pipes

Because SMB often exposes valuable information, it is one of the first services examined during an authorized security assessment.

Nmap includes many NSE scripts that safely enumerate SMB services without exploiting them.

---

# Learning Objectives

After completing this lab, you will be able to:

- Identify SMB services.
- Discover SMB shares.
- Detect SMB protocol versions.
- Retrieve operating system information.
- Enumerate SMB security settings.
- Interpret SMB enumeration results.

---

# Difficulty

⭐⭐⭐☆☆ Intermediate

---

# Estimated Time

45–60 Minutes

---

# Prerequisites

- Lab 11 completed
- Basic understanding of SMB
- Windows or Samba target

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| Windows Server | 192.168.56.20 | Target |

---

# Scenario

A Windows server exposes port **445/TCP**.

Your task is to identify:

- SMB version
- Operating system
- Computer name
- Domain or workgroup
- Available shares
- Security configuration

---

# What is SMB?

SMB (Server Message Block) is a protocol used primarily by Microsoft Windows systems for sharing files, printers, and other network resources.

Common ports:

| Port | Protocol |
|------|----------|
| 139 | NetBIOS Session Service |
| 445 | Direct SMB |

---

# Step 1 — Detect SMB Service

Run:

```bash
nmap -sV -p445 192.168.56.20
```

Example Output

```text
445/tcp open microsoft-ds
```

---

# Step 2 — OS Discovery

Run:

```bash
nmap --script smb-os-discovery -p445 192.168.56.20
```

Example Output

```text
Computer name:

WIN-SERVER

OS:

Windows Server 2022

Workgroup:

WORKGROUP
```

---

# Step 3 — Enumerate SMB Shares

Run:

```bash
nmap --script smb-enum-shares -p445 192.168.56.20
```

Example Output

```text
ADMIN$

IPC$

Public

Users
```

Questions:

- Which shares are expected?
- Are any publicly accessible?
- Are unnecessary shares exposed?

---

# Step 4 — Enumerate Users (When Permitted)

Run:

```bash
nmap --script smb-enum-users -p445 192.168.56.20
```

Depending on the target configuration, this may reveal account information.

---

# Step 5 — Determine SMB Protocol Version

Run:

```bash
nmap --script smb-protocols -p445 192.168.56.20
```

Example Output

```text
SMBv2

SMBv3
```

Questions:

- Is SMBv1 enabled?
- Which protocol versions are supported?

---

# Step 6 — Enumerate SMB Security Mode

Run:

```bash
nmap --script smb-security-mode -p445 192.168.56.20
```

Example Output

```text
Message signing:

Enabled

Required:

False
```

Consider:

- Is message signing enforced?
- Does the configuration align with organizational policy?

---

# Running Multiple SMB Scripts

Run:

```bash
nmap --script "smb-os-discovery,smb-enum-shares,smb-protocols,smb-security-mode" -p445 192.168.56.20
```

This gathers multiple pieces of SMB information in a single scan.

---

# Understanding the Results

Example

```text
Computer Name:

DC01
```

Possible interpretation:

- Domain Controller naming convention
- Enterprise Windows environment
- Additional directory services may exist

---

Example

```text
SMBv1 Supported
```

Questions:

- Is legacy protocol support required?
- Has it been intentionally retained for compatibility?
- Should it be reviewed by administrators?

---

# Common SMB Scripts

| Script | Purpose |
|---------|---------|
| smb-os-discovery | OS information |
| smb-enum-shares | List shared folders |
| smb-enum-users | Enumerate users |
| smb-protocols | Supported SMB versions |
| smb-security-mode | Security settings |
| smb2-time | Server time |
| smb2-capabilities | SMBv2/v3 capabilities |

---

# NSE Script Deep Dive

## Script

```text
smb-os-discovery.nse
```

Category

```text
default
discovery
safe
```

Purpose

Retrieves operating system and SMB-related host information.

Typical Uses

- Asset inventory
- Operating system identification
- Domain discovery

Limitations

- Depends on server configuration.
- Some information may be restricted.

Related Scripts

- smb-protocols
- smb-security-mode
- smb-enum-shares

---

# Thinking Like an Analyst

Suppose you discover:

```text
Shares

Public

Finance

Backups
```

Questions:

- Are these shares expected?
- Are permissions appropriate?
- Which shares should administrators review?

---

Another example:

```text
Computer Name:

DC01
```

Questions:

- Could this be a domain controller?
- What additional directory services might be available?
- Should LDAP or Kerberos be enumerated next?

---

# Common Mistakes

## Assuming Every Share Is Public

Many shares require authentication.

Always verify access according to authorized testing procedures.

---

## Ignoring SMB Version Information

Understanding supported SMB versions helps identify compatibility and security considerations.

---

## Running Every SMB Script Automatically

Select scripts that match your assessment objectives and authorization.

---

# Challenge

Run the following:

```bash
nmap --script "smb-os-discovery,smb-enum-shares,smb-protocols" -p445 target
```

Document:

- Operating system
- Computer name
- Supported SMB versions
- Shared resources

---

# Bonus Challenge

List all SMB-related NSE scripts:

```bash
ls /usr/share/nmap/scripts/smb*
```

Answer:

- How many SMB scripts are installed?
- Which scripts focus on discovery?
- Which scripts appear related to authentication?
- Which scripts appear to check security configuration?

---

# Key Takeaways

- SMB provides valuable information about Windows systems.
- NSE scripts can safely enumerate shares, protocol versions, and host details.
- Understanding SMB configuration is important for system administration and authorized security assessments.
- Enumeration results should guide the next stage of analysis.

---

# Next Lab

➡ **Lab 14 — FTP Scripts**

In the next lab, you will enumerate FTP servers, inspect authentication settings, identify supported features, and analyze FTP-related configuration using dedicated NSE scripts.