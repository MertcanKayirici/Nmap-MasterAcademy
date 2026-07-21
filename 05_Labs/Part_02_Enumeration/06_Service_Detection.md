# Lab 06 — Service Detection

> Learn how to identify, analyze, and interpret network services discovered during an Nmap scan.

---

# Overview

Open ports alone provide limited information about a target.

For example, discovering that **port 22** is open tells you very little. However, learning that the port is running **OpenSSH 9.2 on Ubuntu Linux** immediately provides valuable insight into the system.

Service detection is the process of identifying the applications listening on open ports. Nmap accomplishes this by sending carefully crafted probes and comparing the responses against its service fingerprint database.

Understanding the detected services allows administrators and security professionals to determine the role of a system, identify outdated software, and plan the next stage of an assessment.

---

# Learning Objectives

After completing this lab, you will be able to:

- Perform service detection using Nmap.
- Interpret service banners.
- Identify application versions.
- Recognize common network services.
- Understand the security implications of exposed services.
- Decide the next enumeration step based on detected services.

---

# Difficulty

⭐⭐☆☆☆

---

# Estimated Time

45–60 Minutes

---

# Prerequisites

- Part 01 completed.
- Basic understanding of TCP ports.
- A target machine with multiple running services.

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Attacker |
| Target Machine | 192.168.56.20 | Target |

---

# Scenario

A host has already been identified.

Your objective is no longer to find open ports—you already know they exist.

Instead, your task is to answer questions such as:

- Which services are running?
- Which software is being used?
- Which versions are installed?
- Which services deserve further investigation?

---

# What is Service Detection?

Service Detection is the process of identifying the application listening behind an open port.

Example

Without service detection:

```text
80/tcp open
```

With service detection:

```text
80/tcp open http Apache httpd 2.4.57
```

The second result provides much more useful information.

---

# Why Version Information Matters

Knowing that a web server exists is useful.

Knowing exactly which software and version is running is even more valuable.

Example:

```text
Apache httpd 2.4.57
```

This information can be used to:

- Verify software inventory
- Identify outdated software
- Search for public vulnerabilities
- Prioritize security updates

---

# Step 1 — Detect Services

Run:

```bash
nmap -sV 192.168.56.20
```

Example Output

```text
PORT     STATE SERVICE VERSION

21/tcp   open  ftp     vsftpd 2.3.4

22/tcp   open  ssh     OpenSSH 9.2

80/tcp   open  http    Apache httpd 2.4.57
```

---

# Output Analysis

## FTP

```text
21/tcp open ftp vsftpd 2.3.4
```

Questions to ask:

- Is anonymous login enabled?
- Which FTP implementation is used?
- Is the version outdated?
- Should FTP be exposed?

---

## SSH

```text
22/tcp open ssh OpenSSH 9.2
```

Questions to ask:

- Is password authentication enabled?
- Is key authentication available?
- Is the version current?
- Is remote administration expected?

---

## HTTP

```text
80/tcp open http Apache httpd 2.4.57
```

Questions to ask:

- Which web server is running?
- Is HTTPS available?
- Does the server expose default pages?
- Is directory enumeration appropriate?
- Which technologies might the website use?

---

# Step 2 — Increase Detection Intensity

Run:

```bash
nmap -sV --version-all 192.168.56.20
```

Explanation

Nmap sends additional probes to improve detection accuracy.

Advantages

- Better identification
- More reliable fingerprints

Disadvantages

- Longer scan time
- Increased network traffic

---

# Step 3 — Faster Detection

Run:

```bash
nmap -sV --version-light 192.168.56.20
```

Use this option when scanning many hosts quickly.

---

# Recognizing Common Services

| Port | Typical Service | Purpose |
|------|-----------------|----------|
| 21 | FTP | File Transfer |
| 22 | SSH | Secure Remote Access |
| 25 | SMTP | Email |
| 53 | DNS | Name Resolution |
| 80 | HTTP | Web Server |
| 110 | POP3 | Email Retrieval |
| 143 | IMAP | Email |
| 443 | HTTPS | Secure Web |
| 445 | SMB | Windows File Sharing |
| 3306 | MySQL | Database |
| 3389 | RDP | Remote Desktop |

---

# Thinking Like an Analyst

Enumeration is not about collecting information.

It is about deciding what to investigate next.

Example:

```text
22/tcp open ssh
```

Possible next steps:

- Check supported authentication methods.
- Verify SSH configuration.
- Identify the operating system.
- Look for weak credentials (only in authorized environments).

---

Another example:

```text
80/tcp open http Apache
```

Possible next steps:

- Visit the website.
- Check response headers.
- Identify technologies.
- Search for hidden directories.
- Determine whether HTTPS is available.

---

# Common Mistakes

## Assuming the Port Defines the Service

Applications can run on non-standard ports.

Always rely on service detection rather than port numbers alone.

---

## Ignoring Version Information

The version number may reveal:

- Unsupported software
- Missing updates
- Configuration differences

---

## Treating Enumeration as Finished

Finding the service is only the beginning.

Each detected service opens the door to further investigation.

---

# Challenge

Perform service detection on your target and answer:

1. Which services were detected?

2. Which application versions were identified?

3. Which service would you investigate first?

4. Why?

---

# Bonus Challenge

Run the following commands and compare the results:

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
- Detected services
- Version accuracy
- Amount of information collected

---

# Key Takeaways

- Service detection reveals the applications behind open ports.
- Version detection provides valuable context for further analysis.
- Enumeration is a decision-making process, not just data collection.
- Every detected service should be evaluated for its purpose and potential security impact.

---

# Next Lab

➡ **Lab 07 — OS Detection**

In the next lab, you will determine the operating system of the target by analyzing TCP/IP fingerprinting and other characteristics observed by Nmap.