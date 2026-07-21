# Lab 08 — Aggressive Scan

> Learn how to perform comprehensive reconnaissance using Nmap's Aggressive Scan mode and understand every feature it enables.

---

# Overview

During reconnaissance, running multiple Nmap commands individually can become time-consuming.

Instead, Nmap provides the **Aggressive Scan** option (`-A`), which combines several advanced detection techniques into a single command.

An Aggressive Scan can identify:

- Operating System
- Service Versions
- Default NSE Script Results
- Network Path (Traceroute)

Although convenient, aggressive scanning generates more traffic and takes longer to complete than basic scans.

Understanding exactly what happens during an Aggressive Scan is essential for deciding when—and when not—to use it.

---

# Learning Objectives

After completing this lab, you will be able to:

- Perform an Aggressive Scan.
- Understand every feature enabled by `-A`.
- Analyze combined scan results.
- Recognize when aggressive scanning is appropriate.
- Understand the performance trade-offs.
- Plan follow-up enumeration steps.

---

# Difficulty

⭐⭐⭐☆☆ Intermediate

---

# Estimated Time

45–60 Minutes

---

# Prerequisites

- Lab 06 completed.
- Lab 07 completed.
- A reachable target with multiple open ports.

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| Target Machine | 192.168.56.20 | Target |

---

# Scenario

You have already discovered:

- Live hosts
- Open ports
- Running services
- Possible operating system

Instead of executing several separate commands, you want to collect as much information as possible with a single scan.

---

# What Does -A Actually Do?

The following command:

```bash
sudo nmap -A 192.168.56.20
```

internally enables several features.

| Feature | Equivalent Option |
|----------|------------------|
| OS Detection | `-O` |
| Version Detection | `-sV` |
| Default NSE Scripts | `-sC` |
| Traceroute | `--traceroute` |

Think of `-A` as a shortcut that combines these features into one scan.

---

# Step 1 — Run an Aggressive Scan

Execute:

```bash
sudo nmap -A 192.168.56.20
```

Allow the scan to finish before analyzing the output.

---

# Step 2 — Review Service Detection

Example

```text
22/tcp open ssh OpenSSH 9.2
```

Questions

- Which service was detected?
- Which version is running?
- Does the version appear current?

---

# Step 3 — Review OS Detection

Example

```text
Running: Linux 6.X
```

Questions

- Is the OS estimate reasonable?
- Does it match the detected services?

---

# Step 4 — Review NSE Script Results

Example

```text
http-title:

Apache2 Ubuntu Default Page
```

Example

```text
ssh-hostkey:

RSA
ECDSA
ED25519
```

Questions

- What additional information did the scripts reveal?
- Which findings deserve further investigation?

---

# Step 5 — Review Traceroute

Example

```text
TRACEROUTE

1 192.168.56.20
```

Traceroute helps estimate the network path between the scanner and the target.

In local virtual labs, the path is usually very short.

---

# Understanding the Output

A typical Aggressive Scan report contains several sections:

```text
PORTS

↓

SERVICES

↓

VERSIONS

↓

OS DETAILS

↓

NSE RESULTS

↓

TRACEROUTE
```

Each section provides different information about the target.

---

# Advantages of Aggressive Scan

- Collects multiple types of information at once.
- Reduces the number of separate commands.
- Produces comprehensive reconnaissance results.
- Excellent for laboratory environments.
- Useful during authorized internal assessments.

---

# Limitations

Aggressive Scan:

- Takes longer.
- Generates more packets.
- Produces more network noise.
- May trigger monitoring or security systems.

Because of these characteristics, it is not always the best choice.

---

# Comparing Common Commands

| Command | Information Collected |
|----------|----------------------|
| `nmap target` | Open Ports |
| `nmap -sV target` | Services |
| `nmap -O target` | Operating System |
| `nmap -sC target` | Default NSE Scripts |
| `nmap -A target` | Combined Enumeration |

---

# Thinking Like an Analyst

Suppose the scan reports:

```text
22/tcp open ssh

80/tcp open http

3306/tcp open mysql
```

Instead of stopping here, ask:

- Is the database intended to be network-accessible?
- Does the web application connect to the database?
- Are the services expected for this type of server?
- Which service should be examined first?

Aggressive Scan provides information.

Your job is to turn that information into meaningful conclusions.

---

# Common Mistakes

## Using -A for Every Scan

Aggressive scanning is powerful, but it is not always necessary.

Use simpler scans when only basic information is required.

---

## Ignoring NSE Results

Many beginners focus only on open ports.

The NSE output often contains the most valuable information.

---

## Forgetting Performance Impact

Aggressive scans consume more time and generate more network traffic than basic scans.

---

# Challenge

Run an Aggressive Scan and answer:

1. Which operating system was detected?
2. Which services were identified?
3. Which NSE script result was the most interesting?
4. How many hops were shown in the traceroute?

---

# Bonus Challenge

Instead of using:

```bash
sudo nmap -A target
```

Run the equivalent commands separately:

```bash
sudo nmap -O target
```

```bash
sudo nmap -sV target
```

```bash
sudo nmap -sC target
```

```bash
sudo nmap --traceroute target
```

Compare the outputs.

Which approach do you prefer, and why?

---

# Key Takeaways

- `-A` combines multiple advanced Nmap features into one scan.
- It provides a comprehensive overview of the target.
- Aggressive scans balance convenience against increased scan time and network activity.
- The value of an Aggressive Scan comes from correctly interpreting all of its output—not just the list of open ports.

---

# Next Lab

➡ **Lab 09 — Output Formats**

In the next lab, you will learn how to save, export, and reuse scan results in multiple formats for reporting, automation, and future analysis.