# Lab 04 — TCP vs UDP Scan

> Compare TCP and UDP scanning techniques and understand why their results differ.

---

# Overview

Not all network services use the same transport protocol.

Some services communicate over **TCP**, while others rely on **UDP**. Because these protocols behave differently, Nmap uses different scanning techniques for each.

In this lab, you will compare TCP and UDP scans against the same target and analyze how protocol behavior affects scan speed, accuracy, and output.

---

# Learning Objectives

After completing this lab, you will be able to:

- Perform TCP scans
- Perform UDP scans
- Compare scan duration
- Compare scan results
- Identify TCP and UDP services
- Understand why UDP scanning is slower
- Interpret UDP scan results

---

# Difficulty

⭐⭐☆☆☆

---

# Estimated Time

35–50 Minutes

---

# Prerequisites

- Lab 01 completed
- Lab 02 completed
- Lab 03 completed

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Attacker |
| Target Machine | 192.168.56.20 | Victim |

---

# Scenario

You have identified a target host.

Now you need to determine:

- Which TCP services are running?
- Which UDP services are running?
- Which protocol produces faster results?
- Why are the scan results different?

---

# Step 1 — TCP SYN Scan

Run

```bash
sudo nmap -sS 192.168.56.20
```

Explanation

- Performs a TCP SYN Scan.
- Requires root privileges.
- Fast and stealthy.
- Most commonly used TCP scan.

Expected Output

```text
22/tcp open ssh
80/tcp open http
```

---

# Step 2 — TCP Connect Scan

Run

```bash
nmap -sT 192.168.56.20
```

Explanation

Uses the operating system's TCP stack to complete the full connection.

Useful when raw packet privileges are unavailable.

---

# Step 3 — UDP Scan

Run

```bash
sudo nmap -sU 192.168.56.20
```

Explanation

Scans UDP services.

Expected Output

```text
53/udp open domain
161/udp open snmp
```

Depending on the target, you may also see:

```text
open|filtered
```

---

# Step 4 — Scan Common UDP Ports

Run

```bash
sudo nmap -sU --top-ports 20 192.168.56.20
```

Explanation

Scanning all 65,535 UDP ports is slow.

Using the most common UDP ports is usually much faster.

---

# Step 5 — Compare Results

Record your observations.

| Feature | TCP | UDP |
|----------|-----|-----|
| Scan Speed | | |
| Number of Open Ports | | |
| Response Time | | |
| Accuracy | | |
| Reliability | | |

---

# Understanding UDP Results

Unlike TCP, UDP does not establish a connection.

Because of this:

- No SYN
- No ACK
- No connection establishment

If a UDP service does not respond, Nmap often cannot determine whether the port is open or simply filtered.

This is why UDP scans frequently display:

```text
open|filtered
```

---

# Comparing Commands

TCP SYN Scan

```bash
sudo nmap -sS target
```

TCP Connect Scan

```bash
nmap -sT target
```

UDP Scan

```bash
sudo nmap -sU target
```

TCP + UDP

```bash
sudo nmap -sS -sU target
```

---

# Output Analysis

Example

```text
22/tcp open ssh
```

Meaning

SSH is accepting TCP connections.

---

Example

```text
53/udp open domain
```

Meaning

A DNS service is listening over UDP.

---

Example

```text
161/udp open snmp
```

Meaning

The SNMP service is available.

---

Example

```text
69/udp open|filtered tftp
```

Meaning

Nmap cannot determine whether the port is open or filtered.

---

# Common Mistakes

## Forgetting sudo

Many TCP SYN and UDP scans require elevated privileges.

---

## Expecting UDP to be Fast

UDP scans are often significantly slower than TCP scans.

---

## Assuming open|filtered Means Open

It does not.

Further investigation is required.

---

# Challenge

Answer the following:

- Which scan finished first?
- How many TCP ports were open?
- How many UDP ports were open?
- Which protocol returned more information?

---

# Bonus Challenge

Run:

```bash
sudo nmap -sS -sU 192.168.56.20
```

Compare the combined scan with the individual scans.

Questions

- Which ports appeared only in TCP?
- Which ports appeared only in UDP?
- Why?

---

# Key Takeaways

- TCP scans are generally faster and more reliable.
- UDP scans are slower and may produce ambiguous results.
- Different services use different transport protocols.
- Both TCP and UDP scans are important during reconnaissance.
- Nmap supports scanning both protocols individually or together.

---

# Next Lab

➡ **Lab 05 — Service Enumeration**

In the next lab, you will identify services and application versions running on open ports using Nmap's version detection capabilities.