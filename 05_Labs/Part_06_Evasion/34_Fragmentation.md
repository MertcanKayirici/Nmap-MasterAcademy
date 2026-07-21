# Lab 34 — Packet Fragmentation Analysis

> Explore how packet fragmentation affects Nmap scan traffic and compare scan observations in an authorized laboratory environment.

---

# Overview

Network packets are normally transmitted as complete units.

Nmap provides options that modify how scan packets are transmitted, including packet fragmentation.

Understanding fragmentation helps security professionals:

- Observe how scan traffic changes.
- Compare scan behavior.
- Better understand network devices.
- Improve assessment documentation.

This lab focuses on observation rather than attempting to bypass security controls.

---

# Learning Objectives

After completing this lab, you will be able to:

- Explain packet fragmentation.
- Compare fragmented and non-fragmented scans.
- Analyze scan results.
- Document observed differences.
- Understand limitations of fragmentation.

---

# Difficulty

⭐⭐⭐⭐☆

---

# Estimated Time

60–90 Minutes

---

# Prerequisites

- Labs 31–33 completed
- Authorized laboratory environment
- Basic understanding of IP networking

---

# Lab Environment

| Machine | Role |
|----------|------|
| Kali Linux | Scanner |
| Linux Server | Target |
| Monitoring System | Packet Capture & Logging |

---

# Scenario

Your security team wants to understand whether modifying packet structure affects scan observations within an authorized testing environment.

Your objective is to compare a standard scan with a fragmented scan and document the observed differences.

---

# Workflow

```
Standard Scan

↓

Fragmented Scan

↓

Compare Results

↓

Analyze Differences

↓

Document Findings
```

---

# Phase 1 — Standard Scan

Run a normal scan.

```bash
nmap TARGET_IP
```

Record:

- Open ports
- Closed ports
- Filtered ports
- Scan duration

---

# Phase 2 — Fragmented Scan

Run a fragmented scan.

```bash
nmap -f TARGET_IP
```

Document:

- Scan duration
- Reported ports
- Observed differences

Remember:

Fragmentation modifies packet transmission characteristics but does not guarantee different scan results.

---

# Phase 3 — Service Detection Comparison

Run service detection.

```bash
nmap -sV TARGET_IP
```

Compare:

- Service versions
- Product names
- Banners

---

# Phase 4 — Result Comparison

| Scan Type | Open Ports | Service Detection | Notes |
|-----------|------------|-------------------|------|
| Standard | | | |
| Fragmented | | | |

---

# Phase 5 — Analysis

Answer:

- Were the same ports identified?
- Did scan duration change?
- Were there observable differences?
- Which conclusions are supported by the collected evidence?

Avoid unsupported assumptions.

---

# Assessment Checklist

☐ Standard scan completed

☐ Fragmented scan completed

☐ Service detection completed

☐ Results compared

☐ Documentation completed

---

# Decision Tree

```
Standard Scan

↓

Fragmented Scan

↓

Compare Results

↓

Analyze Observations

↓

Prepare Report
```

---

# Blue Team Perspective

Consider the assessment from the defender's perspective.

Questions:

- Which monitoring systems could record fragmented traffic?
- Would packet captures provide additional context?
- Which network devices may reassemble fragmented packets?
- What evidence should analysts collect before drawing conclusions?

---

# Reporting Template

## Scope

## Methodology

## Standard Scan Results

## Fragmented Scan Results

## Comparison

## Observations

## Conclusions

---

# Challenge

Perform both scan types in an authorized lab environment.

Prepare:

- Port inventory
- Service inventory
- Comparison table
- Observation notes
- Final report

---

# Evasion Summary

Throughout this section you explored how changes to scan behavior can influence observations during an authorized assessment.

```
Baseline Scan
        │
        ▼
Firewall Analysis
        │
        ▼
IDS Observation
        │
        ▼
Decoy Scan Comparison
        │
        ▼
Packet Fragmentation
        │
        ▼
Compare Results
        │
        ▼
Document Findings
```

The emphasis has been on understanding network behavior, comparing results, and documenting observations rather than attempting to evade security controls.

---

# Key Takeaways

- Packet fragmentation changes how scan traffic is transmitted.
- Comparing scan configurations improves understanding of network behavior.
- Observations should always be supported by evidence.
- Documentation is an essential part of every professional assessment.
- Authorized laboratory environments provide a safe place to study scan characteristics.

---

# Congratulations!

You have completed:

✅ Firewall Behavior Analysis

✅ IDS Observation

✅ Understanding Decoy Scans

✅ Packet Fragmentation Analysis

You now understand how Nmap scan characteristics can influence observations in monitored environments and how to analyze those observations professionally.

---

# Next Part

➡ **Part 07 — Automation**