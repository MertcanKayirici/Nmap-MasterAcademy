# Lab 32 — IDS Observation

> Observe how different Nmap scan techniques may be interpreted by an Intrusion Detection System (IDS) during an authorized security assessment.

---

# Overview

Intrusion Detection Systems (IDS) monitor network traffic for patterns that may indicate suspicious or unauthorized activity.

Unlike firewalls, which actively allow or block traffic, IDS solutions primarily observe, log, and generate alerts for further analysis.

Understanding how scan techniques appear to network monitoring systems helps security professionals:

- Validate monitoring capabilities
- Interpret assessment results
- Improve detection engineering
- Produce accurate assessment reports

This lab focuses on observation and comparison rather than avoiding detection.

---

# Learning Objectives

After completing this lab, you will be able to:

- Understand the role of an IDS.
- Compare scan behaviors.
- Analyze scan results.
- Observe differences between scan types.
- Document monitoring observations.

---

# Difficulty

⭐⭐⭐⭐☆

---

# Estimated Time

90–120 Minutes

---

# Prerequisites

- Parts 01–05 completed
- Basic networking knowledge
- Authorized lab environment
- Basic understanding of IDS concepts

---

# Lab Environment

| Machine | Role |
|----------|------|
| Kali Linux | Scanner |
| Linux Server | Target |
| IDS Sensor | Monitoring Device |

---

# Scenario

Your organization has recently deployed an IDS sensor.

Your task is to perform several authorized scans and compare how they appear from a network monitoring perspective.

No attempt should be made to disable, bypass, or interfere with the monitoring system.

---

# Assessment Workflow

```
Baseline Scan

↓

Alternative Scan Types

↓

Compare Results

↓

Analyze IDS Observations

↓

Document Findings
```

---

# Phase 1 — Baseline Scan

```bash
nmap TARGET_IP
```

Record:

- Open ports
- Closed ports
- Filtered ports
- Scan duration

---

# Phase 2 — SYN Scan

```bash
nmap -sS TARGET_IP
```

Observe:

- Scan duration
- Differences from baseline
- Reported port states

---

# Phase 3 — Connect Scan

```bash
nmap -sT TARGET_IP
```

Questions:

- Does the output differ?
- Are the same services identified?

---

# Phase 4 — UDP Scan

```bash
nmap -sU TARGET_IP
```

Document:

- UDP services
- Scan duration
- Ports reported as open, closed, or open|filtered

---

# Phase 5 — Service Detection

```bash
nmap -sV TARGET_IP
```

Record:

- Product names
- Versions
- Additional service information

---

# Phase 6 — Compare Results

Create the following table.

| Scan Type | Open Ports | Notes |
|-----------|------------|-------|
| Default | | |
| SYN | | |
| Connect | | |
| UDP | | |
| Service Detection | | |

---

# Phase 7 — Observation Analysis

Answer the following questions:

- Which scan provided the most information?
- Which scan required the most time?
- Which scan produced the clearest service identification?
- Were any differences observed between scan types?

Support every answer using collected evidence.

---

# IDS Observation Notes

Record:

- Time of scan
- Scan type
- Target
- Observed behavior
- Analyst comments

---

# Assessment Checklist

☐ Baseline scan completed

☐ SYN scan completed

☐ Connect scan completed

☐ UDP scan completed

☐ Service detection completed

☐ Results compared

☐ Documentation completed

---

# Decision Tree

```
Run Scan

↓

Collect Results

↓

Compare Outputs

↓

Analyze Differences

↓

Document Findings
```

---

# Thinking Like a Defender

Instead of asking:

> "Can this scan avoid detection?"

Ask:

- What network behavior does this scan produce?
- Which scan provides the most useful information?
- How might monitoring systems interpret this traffic?
- How should these observations be documented?

Understanding network visibility is an important part of defensive security and authorized assessments.

---

# Reporting Template

## Scope

## Methodology

## Scan Types

## Service Inventory

## Comparison

## Observations

## Conclusions

---

# Challenge

Perform every scan in the lab and compare:

- Scan duration
- Services discovered
- Port states
- Information collected

Prepare a structured comparison report.

---

# Bonus Challenge

Create a reusable Nmap workflow that performs:

- Default Scan
- SYN Scan
- UDP Scan
- Service Detection

Save the output as:

```bash
-oA ids_observation
```

---

# Key Takeaways

- Different scan techniques provide different perspectives on a target.
- Comparing scan outputs improves understanding of network behavior.
- IDS solutions monitor traffic patterns and support defensive visibility.
- Accurate documentation is an essential part of every authorized assessment.
- Evidence-based analysis is more valuable than assumptions.

---

# Next Lab

➡ **Lab 33 — Decoy Scans**