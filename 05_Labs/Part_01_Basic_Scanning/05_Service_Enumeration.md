# Lab 05 — Service Enumeration

> Learn how to identify running services and application versions using Nmap.

---

# Overview

Discovering open ports is only the beginning of a network assessment.

The next step is determining **which services** are running on those ports and, if possible, **which versions** of those services are installed.

Service enumeration helps identify:

- Running applications
- Service versions
- Potential vulnerabilities
- Misconfigurations
- Operating system characteristics

Nmap performs service detection by communicating with the target service and comparing the responses against its built-in service fingerprint database.

---

# Learning Objectives

After completing this lab, you will be able to:

- Detect running services
- Identify application versions
- Understand service fingerprinting
- Compare different version detection modes
- Perform aggressive service detection
- Save enumeration results

---

# Difficulty

⭐⭐☆☆☆

---

# Estimated Time

30–45 Minutes

---

# Prerequisites

- Lab 01 completed
- Lab 02 completed
- Lab 03 completed
- Lab 04 completed

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Attacker |
| Target Machine | 192.168.56.20 | Victim |

---

# Scenario

You have already identified the target's open ports.

Now your task is to determine:

- Which services are running?
- Which software versions are installed?
- Which services might require additional investigation?

---

# Why Service Enumeration Matters

Knowing that port **80** is open is useful.

Knowing that it is running:

```
Apache HTTP Server 2.4.57
```

is much more valuable.

Version information allows administrators and security professionals to:

- Verify software inventory
- Identify outdated software
- Search for known vulnerabilities
- Prioritize remediation efforts

---

# Step 1 — Basic Version Detection

Run

```bash
nmap -sV 192.168.56.20
```

Explanation

The `-sV` option enables service and version detection.

Example Output

```text
PORT     STATE SERVICE VERSION

21/tcp   open  ftp     vsftpd 2.3.4

22/tcp   open  ssh     OpenSSH 8.9

80/tcp   open  http    Apache httpd 2.4.57
```

---

# Step 2 — Light Version Detection

Run

```bash
nmap -sV --version-light 192.168.56.20
```

Explanation

Performs fewer probes.

Advantages

- Faster
- Less network traffic

Disadvantages

- Less accurate

---

# Step 3 — Aggressive Version Detection

Run

```bash
nmap -sV --version-all 192.168.56.20
```

Explanation

Uses additional probes to improve identification accuracy.

Advantages

- Better detection
- More detailed fingerprints

Disadvantages

- Longer scan time

---

# Step 4 — Aggressive Scan

Run

```bash
nmap -A 192.168.56.20
```

Explanation

The `-A` option enables:

- Service Detection
- OS Detection
- Default NSE Scripts
- Traceroute

This is a convenient option for comprehensive reconnaissance.

---

# Step 5 — Save Results

Normal Output

```bash
nmap -sV -oN service_scan.txt 192.168.56.20
```

XML Output

```bash
nmap -sV -oX service_scan.xml 192.168.56.20
```

All Formats

```bash
nmap -sV -oA service_scan 192.168.56.20
```

This creates:

```
service_scan.nmap

service_scan.xml

service_scan.gnmap
```

---

# Understanding the Output

Example

```text
22/tcp

open

ssh

OpenSSH 9.2
```

Meaning

Port

```
22
```

is open.

The detected service is

```
SSH
```

The application appears to be

```
OpenSSH 9.2
```

---

Another Example

```text
3306/tcp

open

mysql

MySQL 8.0
```

Meaning

A MySQL database server is accessible on the network.

---

# Comparing Commands

| Command | Purpose |
|----------|----------|
| `-sV` | Standard Version Detection |
| `--version-light` | Faster Detection |
| `--version-all` | Maximum Accuracy |
| `-A` | Aggressive Scan |

---

# Common Mistakes

## Assuming Port Number Equals Service

Example

Port

```
80
```

does not always mean HTTP.

Services can run on non-standard ports.

Always verify using version detection.

---

## Running Aggressive Scan Everywhere

The `-A` option generates more network traffic.

Use it only when appropriate.

---

## Forgetting to Save Results

Enumeration results are valuable for reporting and future analysis.

Always save important scans.

---

# Challenge

Answer the following questions.

1. Which services are running?

2. Which service versions were identified?

3. Which command provides the most detailed version information?

4. Which command is the fastest?

---

# Bonus Challenge

Run all three commands.

```bash
nmap -sV target
```

```bash
nmap -sV --version-light target
```

```bash
nmap -sV --version-all target
```

Compare:

- Scan duration
- Number of detected services
- Version accuracy

Which method would you choose during a large-scale assessment?

---

# Key Takeaways

- Open ports do not automatically reveal the running application.
- Version detection identifies software and application versions.
- Accurate service information improves vulnerability assessment.
- Different detection modes balance speed and accuracy.
- Saving scan results is an important part of professional workflows.

---

# Part Summary

Congratulations!

You have completed **Part 01 — Basic Scanning**.

You can now:

- Prepare a laboratory environment.
- Discover live hosts.
- Perform TCP port scans.
- Compare TCP and UDP scanning.
- Enumerate running services.

These skills form the foundation for more advanced reconnaissance techniques.

---

# Next Part

➡ **Part 02 — Enumeration**

In the next section, you will move beyond basic scanning and begin comprehensive enumeration using advanced Nmap features, operating system detection, aggressive scans, and structured output.