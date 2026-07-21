# Lab 07 — OS Detection

> Learn how Nmap identifies operating systems using TCP/IP fingerprinting and analyze the confidence of its results.

---

# Overview

Knowing which operating system is running on a target host provides valuable context for system administration, troubleshooting, and security assessments.

Different operating systems implement the TCP/IP protocol stack in slightly different ways. Nmap analyzes these differences by sending a series of probes and comparing the responses against its extensive OS fingerprint database.

Operating system detection is not always exact. Firewalls, network devices, virtualization, and custom configurations may affect the results. Therefore, OS detection should always be treated as an informed estimation rather than absolute truth.

---

# Learning Objectives

After completing this lab, you will be able to:

- Perform operating system detection.
- Understand TCP/IP fingerprinting.
- Interpret confidence levels.
- Recognize common operating systems.
- Understand why detection may fail.
- Combine OS detection with service detection.

---

# Difficulty

⭐⭐⭐☆☆ Intermediate

---

# Estimated Time

45–60 Minutes

---

# Prerequisites

- Part 01 completed.
- Lab 06 completed.
- A reachable target with at least one open and one closed TCP port.

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| Target Machine | 192.168.56.20 | Target |

---

# Scenario

You have identified a live host and discovered several open ports.

Before continuing your assessment, you want to answer questions such as:

- Is the target running Windows or Linux?
- Is it a server or a workstation?
- Which operating system family is most likely?
- How confident is Nmap in its prediction?

---

# What is OS Detection?

Operating System Detection is the process of estimating the target's operating system by analyzing network behavior.

Instead of reading system files or logging into the machine, Nmap observes how the target responds to specially crafted packets.

These responses create a unique fingerprint.

---

# How Nmap Detects Operating Systems

Nmap sends multiple probes that evaluate characteristics such as:

- TCP Window Size
- TCP Initial Sequence Numbers
- IP Identification Values
- TCP Options
- TTL Values
- ICMP Responses

The collected fingerprint is compared against the Nmap OS database.

---

# Step 1 — Basic OS Detection

Run:

```bash
sudo nmap -O 192.168.56.20
```

Explanation

The `-O` option enables operating system detection.

Example Output

```text
Running: Linux 6.X

OS CPE: cpe:/o:linux:linux_kernel:6

OS details:
Linux 6.1 - 6.6
```

---

# Step 2 — Verbose OS Detection

Run:

```bash
sudo nmap -O -v 192.168.56.20
```

Explanation

Verbose mode provides additional information about the detection process.

Useful when troubleshooting uncertain results.

---

# Step 3 — Aggressive OS Detection

Run:

```bash
sudo nmap -A 192.168.56.20
```

The `-A` option combines:

- OS Detection
- Version Detection
- Default NSE Scripts
- Traceroute

This is one of the most commonly used reconnaissance commands.

---

# Understanding the Output

Example

```text
Running: Microsoft Windows 11
```

Meaning

Nmap believes the target is running Windows 11.

---

Example

```text
Running: Linux 6.X
```

Meaning

The system is likely using a modern Linux kernel.

---

Example

```text
Device type: general purpose
```

Possible values include:

- General Purpose
- Router
- Firewall
- Printer
- Switch
- VoIP Device
- Storage Appliance

---

# Accuracy and Confidence

Sometimes Nmap displays:

```text
OS details:

Linux 5.15 - 6.6
```

This does not mean the exact version is known.

Instead, it represents the closest matching fingerprints in the database.

Always verify important findings using multiple sources.

---

# Why Detection Can Fail

OS detection may produce inaccurate or inconclusive results if:

- Firewalls filter packets.
- Too few ports are available.
- All scanned ports are filtered.
- The target uses uncommon network stacks.
- Network devices modify packets.

---

# Improving Detection Accuracy

Recommendations:

- Scan a host with both open and closed TCP ports.
- Use root privileges.
- Avoid scanning through multiple network devices.
- Combine OS detection with service detection.

---

# Combining Service and OS Detection

Run:

```bash
sudo nmap -O -sV 192.168.56.20
```

This command collects:

- Operating system information.
- Service versions.
- Additional context for analysis.

---

# Common Mistakes

## Assuming the Result Is Always Correct

OS detection is based on probability, not certainty.

---

## Ignoring Confidence

Always evaluate how closely the detected fingerprint matches known systems.

---

## Using OS Detection Alone

The best assessments combine:

- Host Discovery
- Port Scanning
- Service Detection
- OS Detection

---

# Challenge

Run OS detection against your target.

Answer the following:

1. Which operating system was detected?
2. Was a device type identified?
3. How confident do the results appear?
4. Which open ports support the OS estimate?

---

# Bonus Challenge

Compare the outputs of:

```bash
sudo nmap -O target
```

and

```bash
sudo nmap -A target
```

Questions:

- Which command provides more information?
- Which takes longer?
- When would each command be appropriate?

---

# Key Takeaways

- OS detection estimates the target's operating system using TCP/IP fingerprinting.
- Results are based on probability rather than certainty.
- Detection accuracy depends on network conditions and available responses.
- Combining OS detection with service detection provides a more complete understanding of the target.

---

# Next Lab

➡ **Lab 08 — Aggressive Scan**

In the next lab, you will combine multiple Nmap detection techniques into a single comprehensive reconnaissance scan using the `-A` option.