# Nmap Master Academy

# Course 10

# Nmap Scripting Engine (NSE)

---

## Course Information

**Course Number:** 10

**Difficulty:** Advanced

**Estimated Reading Time:** 180–240 Minutes

**Prerequisites**

- Course 01 – Introduction
- Course 02 – Network Basics
- Course 03 – Ports
- Course 04 – TCP
- Course 05 – UDP
- Course 06 – Host Discovery
- Course 07 – Port Scanning
- Course 08 – Service Detection
- Course 09 – Operating System Detection

---

# Table of Contents

1. What is NSE?
2. Why NSE Matters
3. How NSE Works
4. NSE Architecture
5. Script Categories
6. Using Scripts
7. Script Arguments
8. Finding Scripts
9. Common NSE Scripts
10. Vulnerability Detection
11. Authentication Scripts
12. Discovery Scripts
13. Safe vs Intrusive Scripts
14. Writing Custom Scripts
15. NSE Best Practices
16. Summary

---

# 1. What is NSE?

The Nmap Scripting Engine (NSE) extends Nmap beyond simple port scanning.

Instead of only identifying hosts and services, NSE allows Nmap to perform automated tasks such as:

- Service enumeration
- Vulnerability detection
- Authentication testing
- Information gathering
- Configuration auditing
- Protocol interaction

NSE transforms Nmap into a powerful automation platform for network reconnaissance and security assessments.

---

## Example

Basic Scan

```bash
nmap 192.168.1.20
```

Output

```
22/tcp open ssh
80/tcp open http
```

Using NSE

```bash
nmap --script=http-title 192.168.1.20
```

Output

```
80/tcp open http

Title: Welcome to Apache
```

The script provides additional information that a normal scan would not reveal.

---

# 2. Why NSE Matters

Without NSE, Nmap mainly answers:

- Is the host alive?
- Which ports are open?
- Which services are running?

With NSE, it can answer:

- Is the service vulnerable?
- Does anonymous FTP login work?
- Which SSL ciphers are supported?
- Is SMB misconfigured?
- Which HTTP methods are enabled?
- Does the server expose sensitive information?

This makes NSE one of Nmap's most powerful features.

---

# 3. How NSE Works

NSE executes Lua scripts after or during the scanning process.

```
Host Discovery

↓

Port Scanning

↓

Service Detection

↓

NSE Scripts

↓

Results
```

Each script performs a specific task and returns structured information.

---

# 4. NSE Architecture

NSE consists of several components:

```
Nmap

↓

NSE Engine

↓

Lua Runtime

↓

Script Database

↓

Network Libraries

↓

Target
```

Scripts are written in the Lua programming language and use Nmap's internal libraries to interact with network services.

---

# 5. Script Categories

NSE organizes scripts into categories.

The most common categories include:

| Category | Purpose |
|----------|---------|
| safe | Safe information gathering |
| default | Scripts executed with `-sC` |
| discovery | Service and host discovery |
| version | Improve version detection |
| vuln | Vulnerability detection |
| auth | Authentication testing |
| brute | Password brute forcing |
| malware | Malware detection |
| exploit | Exploitation-related scripts |
| intrusive | Scripts that may affect the target |
| dos | Denial-of-service testing |
| external | Uses external services |

Each category helps users choose scripts appropriate for their assessment.

---

# 6. Running NSE Scripts

Run a single script:

```bash
nmap --script=http-title target
```

Run multiple scripts:

```bash
nmap --script=http-title,http-headers target
```

Run all scripts in a category:

```bash
nmap --script=vuln target
```

Run default scripts:

```bash
nmap -sC target
```

---

# 7. Script Arguments

Some scripts require additional parameters.

Example:

```bash
nmap --script http-brute \
--script-args userdb=users.txt,passdb=passwords.txt target
```

Arguments allow scripts to customize their behavior.

---

# 8. Finding Scripts

Nmap includes hundreds of scripts.

Useful commands:

```bash
ls /usr/share/nmap/scripts/
```

Search by keyword:

```bash
ls /usr/share/nmap/scripts | grep smb
```

Update script database:

```bash
sudo nmap --script-updatedb
```

Display script help:

```bash
nmap --script-help http-title
```

---

# 9. Common NSE Scripts

| Script | Purpose |
|---------|---------|
| http-title | Retrieves webpage titles |
| http-headers | Displays HTTP headers |
| http-methods | Lists supported HTTP methods |
| ssl-cert | Retrieves SSL certificates |
| smb-os-discovery | Detects SMB OS information |
| smb-enum-shares | Enumerates SMB shares |
| ftp-anon | Checks anonymous FTP access |
| ssh-hostkey | Displays SSH host keys |
| dns-brute | DNS subdomain enumeration |

---

# 10. Vulnerability Detection

NSE can identify known vulnerabilities.

Example:

```bash
nmap --script vuln target
```

Possible checks include:

- Heartbleed
- SMB vulnerabilities
- HTTP vulnerabilities
- SSL weaknesses
- Misconfigurations

Remember:

NSE reports potential issues—it does not guarantee exploitation.

---

# 11. Authentication Scripts

Authentication-related scripts test login configurations.

Examples include:

- ftp-anon
- http-auth
- smb-enum-users
- ssh-auth-methods

These scripts help identify weak or insecure authentication mechanisms.

---

# 12. Discovery Scripts

Discovery scripts collect additional information.

Examples:

- DNS records
- SSL certificates
- SMB shares
- SNMP data
- HTTP information

These scripts are commonly used during reconnaissance.

---

# 13. Safe vs Intrusive Scripts

Safe scripts:

- Read-only
- Low risk
- Suitable for production systems

Intrusive scripts:

- May modify system state
- Generate more traffic
- Could trigger security alerts

Always understand a script before executing it.

---

# 14. Writing Custom Scripts

NSE scripts are written in Lua.

A typical script includes:

- Description
- Categories
- Rule
- Action function

Example:

```lua
description = [[
Example NSE Script
]]

categories = {"safe"}

action = function(host)
    return "Hello NSE"
end
```

Custom scripts allow organizations to automate specialized tasks.

---

# 15. Best Practices

✓ Use `-sC` for quick default checks.

✓ Read script documentation before execution.

✓ Prefer safe scripts during initial reconnaissance.

✓ Limit intrusive scripts to authorized environments.

✓ Keep the NSE database updated.

✓ Combine NSE with Service Detection for better results.

---

# Summary

The Nmap Scripting Engine significantly expands Nmap's capabilities.

By using Lua-based scripts, NSE enables automated reconnaissance, vulnerability detection, service enumeration, and security auditing.

Understanding NSE is essential for advanced penetration testing and network security assessments.

---

# Key Takeaways

✓ NSE extends Nmap through Lua scripts.

✓ Scripts automate reconnaissance and security testing.

✓ Categories help organize scripts by purpose.

✓ `-sC` executes default scripts.

✓ `--script` runs specific scripts or categories.

✓ Custom scripts can automate specialized tasks.

---

# Next Course

## Course 11

# Timing and Performance Optimization