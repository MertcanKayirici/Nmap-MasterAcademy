# Lab 31 — Firewall Behavior Analysis

> Compare scan results against a firewall-protected environment and analyze how filtering influences Nmap output.

---

# Overview

Firewalls control network traffic according to predefined security policies.

During an authorized assessment, understanding how a firewall affects scan results is often more important than simply identifying open ports.

This lab focuses on observing firewall behavior and interpreting Nmap results.

---

# Learning Objectives

After completing this lab, you will be able to:

- Identify filtered ports.
- Distinguish between open, closed, and filtered states.
- Compare scans performed under different firewall rules.
- Document firewall observations.

---

# Difficulty

⭐⭐⭐⭐☆

---

# Estimated Time

90–120 Minutes

---

# Lab Environment

| Machine | Role |
|----------|------|
| Kali Linux | Scanner |
| Linux Server | Target |
| Firewall | Network Filtering Device |

---

# Scenario

You are conducting an authorized assessment against a server protected by a firewall.

Your goal is to understand how filtering affects scan results.

---

# Workflow

```
Baseline Scan

↓

Identify Filtered Ports

↓

Compare Results

↓

Analyze Firewall Behavior

↓

Document Findings
```

---

# Phase 1 — Baseline Scan

```bash
nmap TARGET_IP
```

Document:

- Open ports
- Closed ports
- Filtered ports

---

# Phase 2 — SYN Scan

```bash
nmap -sS TARGET_IP
```

Compare the output with the baseline scan.

Questions:

- Did the reported port states change?
- Were any ports reported as filtered?

---

# Phase 3 — ACK Scan

```bash
nmap -sA TARGET_IP
```

Observe how the firewall responds.

Record:

- Unfiltered ports
- Filtered ports

Remember that an ACK scan is commonly used to help analyze filtering behavior. It does not determine whether a port is open in the same way as SYN or Connect scans.

---

# Phase 4 — Compare Results

Create a comparison table.

| Scan Type | Open | Closed | Filtered |
|-----------|------|---------|----------|
| Default | | | |
| SYN | | | |
| ACK | | | |

---

# Phase 5 — Analysis

Answer:

- Which ports appear filtered?
- Which scan provided the most useful information?
- What conclusions can be supported by the collected evidence?

Avoid drawing conclusions that are not supported by the scan results.

---

# Assessment Checklist

☐ Baseline scan completed

☐ SYN scan completed

☐ ACK scan completed

☐ Results compared

☐ Observations documented

---

# Decision Tree

```
Run Scan

↓

Observe Port States

↓

Compare Results

↓

Analyze Filtering

↓

Document Findings
```

---

# Reporting Template

## Scope

## Methodology

## Baseline Results

## Comparison

## Firewall Observations

## Conclusions

---

# Challenge

Perform each scan against the same target and compare how firewall filtering influences the reported results.

---

# Key Takeaways

- Firewalls can affect how Nmap interprets port states.
- Filtered ports provide information about network policy, not just service availability.
- Comparing multiple scan types improves understanding of network behavior.
- Careful interpretation is essential during authorized assessments.

---

# Next Lab

➡ **Lab 32 — IDS Observation**