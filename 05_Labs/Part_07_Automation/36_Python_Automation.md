# Lab 35 — Bash Automation

> Build reusable Bash scripts that automate common Nmap assessment workflows in authorized environments.

---

# Overview

Bash scripting is one of the fastest ways to automate repetitive Nmap tasks.

Instead of manually executing the same commands multiple times, a script can:

- Scan multiple hosts
- Save outputs consistently
- Reduce human error
- Standardize assessments

This lab introduces practical Bash automation techniques for Nmap.

---

# Learning Objectives

After completing this lab, you will be able to:

- Execute Nmap from Bash.
- Automate repeated scans.
- Organize scan output.
- Handle multiple targets.
- Produce repeatable results.

---

# Difficulty

⭐⭐⭐☆☆

---

# Estimated Time

90 Minutes

---

# Scenario

Your organization performs weekly infrastructure inventories.

Instead of manually scanning each server, you are asked to build a reusable Bash workflow.

---

# Workflow

```
Read Target List

↓

Execute Scan

↓

Save Results

↓

Repeat

↓

Generate Summary
```

---

# Phase 1 — Create a Target List

Example:

```text
192.168.1.10
192.168.1.20
192.168.1.30
```

Store the list in:

```text
targets.txt
```

---

# Phase 2 — Basic Automation Script

Example:

```bash
#!/bin/bash

while read target
do
    nmap "$target"
done < targets.txt
```

Explain:

- `while read`
- Loop execution
- Variable expansion
- Input redirection

---

# Phase 3 — Save Results

Example:

```bash
nmap -oA scan_results/$target "$target"
```

Document:

- Output files
- Naming convention
- Directory structure

---

# Phase 4 — Error Handling

Consider:

- Empty lines
- Unreachable hosts
- Missing files
- Interrupted scans

How should the script respond?

---

# Phase 5 — Organize Reports

Example directory:

```text
Assessment/

targets.txt

scan_results/

logs/

reports/
```

---

# Assessment Checklist

☐ Target list prepared

☐ Script created

☐ Output saved

☐ Errors handled

☐ Results documented

---

# Decision Tree

```
Load Targets

↓

Run Scan

↓

Save Output

↓

Repeat

↓

Generate Report
```

---

# Reporting Template

## Scope

## Target List

## Script Description

## Scan Results

## Observations

---

# Challenge

Create a Bash script that scans multiple authorized hosts and stores the results using a consistent naming structure.

---

# Key Takeaways

- Bash is well suited for repetitive command-line automation.
- Consistent output organization improves later analysis.
- Simple scripts can significantly reduce manual effort.

---

# Next Lab

➡ **Lab 36 — Python Automation**