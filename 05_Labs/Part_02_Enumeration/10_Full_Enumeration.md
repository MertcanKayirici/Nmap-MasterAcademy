# Lab 10 — Full Enumeration

> Perform a complete enumeration workflow using everything learned throughout Part 02.

---

# Overview

In previous labs, you learned how to:

- Detect live hosts
- Discover open ports
- Identify services
- Detect operating systems
- Perform aggressive scans
- Export scan results

Real-world reconnaissance rarely consists of a single command.

Instead, analysts follow a structured workflow that gradually collects information while validating each finding.

In this lab, you will perform a complete enumeration from start to finish and produce a professional report.

---

# Learning Objectives

After completing this lab, you will be able to:

- Build an enumeration workflow
- Collect information methodically
- Analyze scan results
- Validate findings
- Produce structured documentation
- Prepare targets for further assessment

---

# Difficulty

⭐⭐⭐☆☆ Intermediate

---

# Estimated Time

60–90 Minutes

---

# Prerequisites

- Part 01 completed
- Labs 06–09 completed

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Analyst |
| Target Machine | 192.168.56.20 | Target |

---

# Scenario

A new server has been deployed inside your organization's internal network.

The security team has received only one piece of information:

```
Target IP

192.168.56.20
```

Your task is to gather as much information as possible using Nmap before any vulnerability assessment begins.

No credentials are available.

No documentation exists.

Only network reconnaissance is authorized.

---

# Mission Objectives

Determine:

- Is the host alive?
- Which ports are open?
- Which services are running?
- Which versions are installed?
- Which operating system is likely?
- Which NSE scripts provide useful information?
- What should be investigated next?

---

# Phase 1 — Verify Host Availability

Run

```bash
nmap -sn 192.168.56.20
```

Questions

- Is the host reachable?
- How quickly did it respond?

---

# Phase 2 — Discover Open Ports

Run

```bash
nmap 192.168.56.20
```

Record:

- Open ports
- Closed ports
- Filtered ports

---

# Phase 3 — Full TCP Scan

Run

```bash
nmap -p- 192.168.56.20
```

Questions

- Were additional ports discovered?
- Were any uncommon services found?

---

# Phase 4 — Service Detection

Run

```bash
nmap -sV 192.168.56.20
```

Document:

- Service names
- Versions
- Interesting findings

---

# Phase 5 — Operating System Detection

Run

```bash
sudo nmap -O 192.168.56.20
```

Document:

- Operating system
- Device type
- Detection confidence

---

# Phase 6 — Aggressive Scan

Run

```bash
sudo nmap -A 192.168.56.20
```

Review:

- NSE Results
- Traceroute
- Additional banners
- Hostnames
- Certificates (if present)

---

# Phase 7 — Save Results

Generate every format.

```bash
sudo nmap -A -oA FullEnumeration 192.168.56.20
```

Verify

```
FullEnumeration.nmap

FullEnumeration.xml

FullEnumeration.gnmap
```

---

# Phase 8 — Analyze Findings

Complete the following table.

| Category | Finding |
|----------|----------|
| Live Host | |
| Open Ports | |
| Services | |
| Versions | |
| Operating System | |
| Device Type | |
| Interesting NSE Results | |
| Additional Notes | |

---

# Phase 9 — Build an Enumeration Summary

Prepare a short report.

Example

```
Target:

192.168.56.20

Summary

Host is reachable.

Five TCP ports are open.

SSH is running on OpenSSH 9.2.

Apache HTTP Server 2.4.57 was detected.

The operating system appears to be Ubuntu Linux.

No unexpected services were identified.

Further assessment should focus on the web server.
```

---

# Thinking Like a Security Analyst

Do not stop after collecting information.

Ask questions.

Example

```
Apache

↓

Is HTTPS available?

↓

What web application is hosted?

↓

Are default pages exposed?

↓

Should directory enumeration be performed?
```

Another example

```
SSH

↓

Password authentication?

↓

Public keys?

↓

Administrative access?

↓

Expected service?
```

Enumeration is a continuous process of asking informed questions.

---

# Common Mistakes

## Running Every Scan Immediately

Good analysts collect information progressively.

Each result should influence the next step.

---

## Ignoring Inconsistent Results

Different scans may produce different findings.

Always investigate unexpected behavior.

---

## Collecting Without Interpreting

Data alone has little value.

The goal is to understand the target.

---

# Final Challenge

Without using additional tools, answer:

- Which operating system is most likely?
- Which service appears most valuable?
- Which port deserves further investigation?
- Which additional Nmap command would you execute next?
- Why?

---

# Bonus Challenge

Repeat the entire workflow against a different virtual machine.

Compare:

- Number of open ports
- Services
- Operating systems
- Scan duration
- NSE output

Write a one-page comparison report.

---

# Part Summary

Congratulations!

You have completed **Part 02 — Enumeration**.

You can now:

✓ Discover hosts

✓ Identify open ports

✓ Detect services

✓ Identify software versions

✓ Estimate operating systems

✓ Perform aggressive scans

✓ Export professional reports

✓ Build a structured reconnaissance workflow

These skills provide the foundation for vulnerability assessment and penetration testing.

---

# Next Part

➡ **Part 03 — NSE (Nmap Scripting Engine)**

In the next section, you will move beyond information gathering and begin using the Nmap Scripting Engine to automate service enumeration, information collection, and security checks.