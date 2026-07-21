# Lab 03 — Basic Port Scanning

> Learn how to discover open ports using Nmap and understand what the results mean.

---

# Overview

Once a live host has been identified, the next step is to discover which network ports are open.

Open ports reveal which services are available on a system and often provide the first clues about the target's purpose. Identifying these ports is a fundamental step in network administration, security assessments, and penetration testing.

In this lab, you will perform several basic port scans and learn how to interpret the results.

---

# Learning Objectives

After completing this lab, you will be able to:

- Perform a basic port scan.
- Scan specific ports.
- Scan all TCP ports.
- Use the Fast Scan option.
- Use the Top Ports option.
- Interpret common port states.
- Understand why some ports appear filtered.

---

# Difficulty

⭐⭐☆☆☆ Beginner

---

# Estimated Time

30–45 Minutes

---

# Prerequisites

- Lab 01 completed
- Lab 02 completed
- Target machine is online

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Attacker |
| Target Machine | 192.168.56.20 | Victim |

---

# Scenario

You have successfully identified a live host.

Now you need to answer the following questions:

- Which ports are open?
- Which services are exposed?
- Are any important services available?

---

# What is Port Scanning?

A port scan is the process of determining which network ports on a target system are open, closed, or filtered.

Open ports often indicate running services such as:

- SSH
- HTTP
- HTTPS
- FTP
- SMB

Understanding which ports are accessible helps identify the services available on the target.

---

# Step 1 — Default Scan

Run:

```bash
nmap 192.168.56.20
```

Explanation

By default, Nmap scans the **1,000 most common TCP ports**.

Expected Output

```text
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
80/tcp   open  http
```

---

# Step 2 — Scan Specific Ports

Run

```bash
nmap -p 22,80,443 192.168.56.20
```

Explanation

Only the specified ports are scanned.

Use this when you only care about certain services.

---

# Step 3 — Scan a Port Range

Run

```bash
nmap -p 1-1000 192.168.56.20
```

Explanation

Scans ports 1 through 1000.

Useful for targeted assessments.

---

# Step 4 — Scan All TCP Ports

Run

```bash
nmap -p- 192.168.56.20
```

Explanation

Scans all 65,535 TCP ports.

Advantages

- Finds uncommon services.
- More comprehensive.

Disadvantages

- Takes longer.

---

# Step 5 — Fast Scan

Run

```bash
nmap -F 192.168.56.20
```

Explanation

Scans fewer ports than the default scan.

Useful for quick reconnaissance.

---

# Step 6 — Scan Top Ports

Run

```bash
nmap --top-ports 100 192.168.56.20
```

Explanation

Scans the 100 most frequently used ports.

You can change the number:

```bash
nmap --top-ports 50 target
```

```bash
nmap --top-ports 1000 target
```

---

# Understanding Port States

| State | Meaning |
|--------|---------|
| Open | A service is actively listening. |
| Closed | No service is listening, but the host responded. |
| Filtered | A firewall or filtering device prevented Nmap from determining the state. |
| Unfiltered | The port is reachable, but its state cannot be determined. |
| Open\|Filtered | Nmap cannot determine whether the port is open or filtered. |
| Closed\|Filtered | Rare state where Nmap cannot distinguish between closed and filtered. |

---

# Comparing Scan Types

| Command | Description |
|----------|-------------|
| nmap target | Default scan |
| nmap -F target | Fast scan |
| nmap -p- target | Full TCP scan |
| nmap -p 80 target | Single port |
| nmap -p 20-100 target | Port range |
| nmap --top-ports 100 target | Most common ports |

---

# Output Analysis

Example

```text
22/tcp open ssh
```

Meaning

- Port 22 is open.
- The SSH service is listening.
- Remote administration may be possible.

---

Example

```text
80/tcp closed http
```

Meaning

- Port exists.
- No HTTP service is running.

---

Example

```text
445/tcp filtered microsoft-ds
```

Meaning

- A firewall or filtering device blocked the scan.

---

# Common Mistakes

## Forgetting the Target

Incorrect

```bash
nmap
```

Correct

```bash
nmap 192.168.56.20
```

---

## Confusing Closed with Filtered

Closed

The host responded.

Filtered

The host did not provide enough information.

---

## Running Full Scans Unnecessarily

A full scan is slower.

Use it only when needed.

---

# Challenge

Answer the following:

- How many ports are open?
- Which service is running on port 22?
- Is port 80 open?
- Which command scans every TCP port?

---

# Bonus Challenge

Compare the results of:

```bash
nmap target
```

and

```bash
nmap -F target
```

Questions

- Which scan is faster?
- Which scan finds more ports?
- Why?

---

# Key Takeaways

- Port scanning is the foundation of enumeration.
- Default scans cover the 1,000 most common TCP ports.
- Full scans inspect every TCP port.
- Fast scans trade completeness for speed.
- Understanding port states is essential before moving to service detection.

---

# Next Lab

➡ **Lab 04 — TCP vs UDP Scan**

In the next lab, you will compare TCP and UDP scanning techniques and learn why UDP scanning behaves differently from TCP scanning.