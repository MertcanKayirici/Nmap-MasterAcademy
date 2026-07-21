# Lab 18 — Custom Script Test

> Learn how to execute individual NSE scripts, use script arguments, explore NSE documentation, and build customized scanning workflows.

---

# Overview

Throughout this section, you have learned how to use default, HTTP, SMB, FTP, SSL, DNS, and vulnerability scripts.

In real-world environments, professionals rarely execute every available script.

Instead, they:

- Select scripts relevant to the target.
- Read script documentation.
- Configure script arguments.
- Combine multiple scripts into efficient workflows.
- Analyze and document the results.

This lab focuses on building that professional workflow.

---

# Learning Objectives

After completing this lab, you will be able to:

- Execute individual NSE scripts.
- Search for available scripts.
- Read NSE documentation.
- Use script arguments.
- Combine multiple scripts.
- Build customized scan profiles.
- Select scripts based on discovered services.

---

# Difficulty

⭐⭐⭐⭐☆ Advanced

---

# Estimated Time

60–90 Minutes

---

# Prerequisites

- Labs 11–17 completed
- Familiarity with common network services
- Authorized testing environment

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| Target Server | 192.168.56.20 | Multi-Service Host |

---

# Scenario

You receive a target containing several services:

```text
22/tcp open ssh

80/tcp open http

443/tcp open https

445/tcp open microsoft-ds
```

Rather than running every available NSE script, you must build an efficient enumeration strategy.

---

# Step 1 — List All Installed Scripts

Run:

```bash
ls /usr/share/nmap/scripts/
```

Observe:

- Script names
- Categories
- Service-specific naming conventions

---

# Step 2 — Search for HTTP Scripts

Run:

```bash
ls /usr/share/nmap/scripts/http*
```

Notice the large number of HTTP-related scripts available.

Questions:

- Which scripts appear related to discovery?
- Which appear related to authentication?
- Which appear related to vulnerabilities?

---

# Step 3 — Search for SMB Scripts

Run:

```bash
ls /usr/share/nmap/scripts/smb*
```

Identify scripts related to:

- Shares
- Users
- Protocols
- Security
- Vulnerabilities

---

# Step 4 — Read Script Documentation

Example:

```bash
nmap --script-help http-title
```

Example Output

```text
http-title

Categories:

default

safe

Author:

Nmap Project

Description:

Retrieves the title of a web page.
```

Always read documentation before using unfamiliar scripts.

---

# Step 5 — Execute a Single Script

Run:

```bash
nmap --script http-title target
```

This executes only one NSE script.

---

# Step 6 — Execute Multiple Scripts

Run:

```bash
nmap --script "http-title,http-headers,http-methods" target
```

Only the selected scripts are executed.

---

# Step 7 — Execute an Entire Category

Run:

```bash
nmap --script default target
```

or

```bash
nmap -sC target
```

---

# Step 8 — Use Wildcards

Example:

```bash
nmap --script http* target
```

Another Example

```bash
nmap --script smb* target
```

Wildcards simplify running groups of related scripts.

---

# Step 9 — Use Script Arguments

Some scripts accept additional parameters.

Example:

```bash
nmap --script http-title \
--script-args http.useragent="Mozilla/5.0" target
```

Another Example

```bash
nmap --script dns-brute \
--script-args dns-brute.domain=example.com target
```

Script arguments customize script behavior.

---

# Step 10 — Save the Results

Run:

```bash
nmap -sV \
--script http-title,http-headers \
-oA web_enum \
target
```

This saves the scan in Normal, XML, and Grepable formats.

---

# Building a Workflow

A professional assessment often follows this sequence:

```text
Host Discovery
        │
        ▼
Port Scan
        │
        ▼
Service Detection
        │
        ▼
Script Selection
        │
        ▼
Execute Relevant NSE Scripts
        │
        ▼
Analyze Results
        │
        ▼
Document Findings
```

---

# Example Workflows

## Web Server

```bash
nmap -sV \
--script http-title,http-headers,http-methods \
target
```

---

## Windows Server

```bash
nmap -sV \
--script smb-os-discovery,smb-enum-shares,smb-protocols \
-p445 target
```

---

## HTTPS Server

```bash
nmap -sV \
--script ssl-cert,ssl-enum-ciphers \
-p443 target
```

---

## DNS Server

```bash
nmap -sV \
--script dns-recursion,dns-nsid \
-p53 target
```

---

# NSE Script Deep Dive

## Command

```text
nmap --script-help
```

Purpose

Displays:

- Description
- Categories
- Author
- Usage
- Script arguments
- Examples
- References

Reading script documentation is considered a best practice before using unfamiliar NSE scripts.

---

# Decision Tree

```text
Service Detected
        │
        ▼
Identify Service Type
        │
        ▼
Select Relevant NSE Category
        │
        ▼
Read Script Documentation
        │
        ▼
Run Appropriate Script(s)
        │
        ▼
Analyze Output
        │
        ▼
Document Findings
```

---

# Thinking Like an Analyst

Suppose your scan discovers:

```text
22 SSH

80 HTTP

445 SMB
```

Instead of running every script, ask:

- Which services are present?
- Which scripts are relevant?
- Which scripts provide the highest value?
- Which scripts are unnecessary?

---

Another Example

You discover:

```text
443 HTTPS
```

Rather than executing all scripts, you might begin with:

- ssl-cert
- ssl-enum-ciphers

Then decide whether additional investigation is necessary.

---

# Common Mistakes

## Running Every Script

Executing every script increases scan time and may generate unnecessary traffic.

Select only those that match your objectives.

---

## Ignoring Documentation

Always review the script description and supported arguments before use.

---

## Forgetting Script Arguments

Many NSE scripts become significantly more useful when configured with appropriate arguments.

---

## Not Saving Results

Always save scan output for future analysis and reporting.

---

# Challenge

A target exposes:

```text
22 SSH

80 HTTP

443 HTTPS

445 SMB
```

Create an enumeration plan that includes:

- Appropriate scripts
- Scan order
- Output format
- Documentation strategy

Explain why each selected script is relevant.

---

# Bonus Challenge

Choose five unfamiliar NSE scripts.

For each script, document:

- Purpose
- Category
- Typical use case
- Required arguments (if any)
- Related scripts

---

# Key Takeaways

- Effective NSE usage depends on selecting the right scripts, not running every script.
- Reading script documentation improves accuracy and efficiency.
- Script arguments allow you to customize behavior for different environments.
- Combining service detection with carefully chosen NSE scripts creates efficient and repeatable workflows.
- Professional assessments emphasize planning, interpretation, and documentation as much as command execution.

---

# Part Summary

Congratulations!

You have completed **Part 03 — Nmap Scripting Engine (NSE)**.

You can now:

- Understand the NSE architecture.
- Execute default and service-specific scripts.
- Interpret script output.
- Analyze HTTP, SMB, FTP, SSL/TLS, and DNS services.
- Perform safe vulnerability detection.
- Build customized NSE workflows.
- Select scripts based on assessment objectives.
- Document results using professional practices.

You are now prepared to apply NSE in larger network assessments.

---

# Next Part

➡ **Part 04 — Real World Assessments**

In the next section, you will apply everything learned so far to realistic environments, including:

- Internal Networks
- Web Servers
- Windows Servers
- Linux Servers
- Database Servers
- DMZ Environments
- Full Network Assessments

These labs simulate real-world reconnaissance workflows and integrate host discovery, service enumeration, NSE scripting, and reporting into complete assessment scenarios.