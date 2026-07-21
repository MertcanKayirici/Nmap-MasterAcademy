# Lab 11 — Default Scripts

> Learn how to use Nmap's default NSE scripts to automatically gather valuable information from network services.

---

# Overview

The Nmap Scripting Engine (NSE) extends Nmap beyond traditional port scanning by allowing scripts to interact with discovered services.

Instead of simply reporting that a port is open, NSE can retrieve banners, enumerate services, inspect SSL certificates, identify SSH host keys, obtain HTTP titles, and perform many other safe information-gathering tasks.

The default script set provides an excellent starting point because it focuses on scripts that are considered safe and broadly useful.

In this lab, you will learn how to execute default scripts, understand their output, and determine how the collected information guides the next stage of an assessment.

---

# Learning Objectives

After completing this lab, you will be able to:

- Understand the purpose of NSE.
- Execute default scripts.
- Understand the relationship between `-sC` and `--script default`.
- Interpret common NSE output.
- Combine service detection with NSE.
- Identify valuable information returned by scripts.

---

# Difficulty

⭐⭐⭐☆☆ Intermediate

---

# Estimated Time

45–60 Minutes

---

# Prerequisites

- Part 01 completed
- Part 02 completed

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| Target Machine | 192.168.56.20 | Target |

---

# What is the Nmap Scripting Engine?

The Nmap Scripting Engine (NSE) is an automation framework built into Nmap.

Scripts can communicate directly with network services to collect additional information beyond what a traditional scan provides.

Examples include:

- Retrieving HTTP page titles
- Displaying SSL certificates
- Listing SSH host keys
- Identifying SMB information
- Checking FTP configuration
- Performing safe security checks

---

# What Are Default Scripts?

Default scripts are a curated collection of NSE scripts designed to provide useful information while minimizing unnecessary risk and network impact.

They are intended for general reconnaissance and are appropriate for most authorized assessments.

---

# Step 1 — Execute Default Scripts

Run:

```bash
nmap -sC 192.168.56.20
```

Explanation

The `-sC` option runs the default script category.

---

# Step 2 — Equivalent Command

Run:

```bash
nmap --script default 192.168.56.20
```

Both commands execute the same set of default scripts.

---

# Step 3 — Combine with Version Detection

Run:

```bash
nmap -sC -sV 192.168.56.20
```

This command provides:

- Open ports
- Service names
- Version information
- Default NSE script results

This combination is commonly used during initial enumeration.

---

# Understanding Script Output

Example

```text
PORT   STATE SERVICE

22/tcp open ssh

| ssh-hostkey:
|   3072 RSA
|   256 ECDSA
|   256 ED25519
```

The script reports the public host keys presented by the SSH server.

These keys help identify the server and detect changes over time.

---

Another Example

```text
80/tcp open http

| http-title:

Apache2 Ubuntu Default Page
```

The script retrieves the title of the web page.

This can reveal:

- Default installations
- Internal applications
- Device interfaces
- Login portals

---

Another Example

```text
443/tcp open https

| ssl-cert:

Subject:

CN=example.local
```

The certificate may reveal:

- Hostnames
- Organization names
- Expiration dates
- Certificate authorities

---

# Common Default Scripts

| Script | Purpose |
|---------|---------|
| ssh-hostkey | Retrieve SSH host keys |
| http-title | Retrieve web page title |
| http-server-header | Display HTTP server banner |
| ssl-cert | Display SSL certificate |
| smb-os-discovery | Identify SMB information |
| ftp-anon | Check anonymous FTP access |

---

# Listing Available Default Scripts

Display all installed NSE scripts:

```bash
ls /usr/share/nmap/scripts/
```

Search for HTTP scripts:

```bash
ls /usr/share/nmap/scripts/http*
```

Search for SSH scripts:

```bash
ls /usr/share/nmap/scripts/ssh*
```

---

# Understanding Script Categories

NSE scripts are grouped into categories.

Examples include:

- default
- safe
- auth
- discovery
- version
- vuln
- brute
- intrusive
- malware
- exploit

Future labs will explore these categories in detail.

---

# Output Analysis

Suppose the scan reports:

```text
http-title:

Admin Login
```

Questions to ask:

- Is this an administrative interface?
- Is authentication required?
- Is HTTPS available?
- Should web enumeration continue?

---

Another Example

```text
ftp-anon:

Anonymous FTP login allowed
```

Questions:

- Is anonymous access expected?
- What files are exposed?
- Does this present unnecessary risk?

---

# Common Mistakes

## Running Scripts Without Understanding Them

Always read the script description before use.

Not every script is appropriate for every environment.

---

## Ignoring Script Output

Many valuable findings appear below the port list.

Do not stop reading after identifying open ports.

---

## Assuming Every Script Is Safe

While the default category is designed to be safe, other categories may perform intrusive actions.

Understand a script before executing it.

---

# Challenge

Run:

```bash
nmap -sC -sV 192.168.56.20
```

Answer:

- Which scripts executed?
- Which script returned the most useful information?
- Did any script identify additional host information?

---

# Bonus Challenge

List all installed NSE scripts:

```bash
ls /usr/share/nmap/scripts/
```

Estimate:

- How many scripts are installed?
- Which categories appear most frequently?
- Which scripts seem related to HTTP?

---

# Key Takeaways

- NSE extends Nmap far beyond traditional port scanning.
- Default scripts provide valuable information with minimal risk.
- `-sC` and `--script default` are equivalent.
- Script output often reveals details unavailable through port scanning alone.
- Understanding script results is just as important as running the scripts.

---

# Next Lab

➡ **Lab 12 — HTTP Scripts**

In the next lab, you will use HTTP-specific NSE scripts to enumerate web servers, identify technologies, retrieve headers, inspect page titles, and gather information from web applications.