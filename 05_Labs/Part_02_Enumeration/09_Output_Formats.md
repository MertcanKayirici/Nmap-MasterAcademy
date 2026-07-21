# Lab 09 — Output Formats

> Learn how to save, export, and reuse Nmap scan results using different output formats.

---

# Overview

Running a scan is only part of the assessment process.

The collected information is often needed later for:

- Documentation
- Reporting
- Automation
- Comparison
- Vulnerability Assessment
- Incident Response

Nmap supports multiple output formats, each designed for different workflows.

Understanding when to use each format is an essential skill for security professionals.

---

# Learning Objectives

After completing this lab, you will be able to:

- Save scan results
- Understand every output format
- Generate reports
- Create machine-readable output
- Export multiple formats simultaneously
- Choose the correct format for different scenarios

---

# Difficulty

⭐⭐☆☆☆

---

# Estimated Time

30–45 Minutes

---

# Prerequisites

- Previous Enumeration labs completed

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| Target Machine | 192.168.56.20 | Target |

---

# Scenario

You have completed a successful enumeration.

Now you must deliver your findings to:

- another security analyst
- a system administrator
- an automated tool
- a reporting platform

Different consumers require different output formats.

---

# Why Save Scan Results?

Saving results allows you to:

- Review findings later
- Compare scans over time
- Share results
- Import into other tools
- Create professional reports

Never rely only on terminal output.

---

# Output Formats

Nmap supports several output formats.

| Option | Format | Intended Use |
|---------|--------|--------------|
| -oN | Normal | Human-readable reports |
| -oX | XML | Automation and integrations |
| -oG | Grepable | Simple text parsing (legacy) |
| -oA | All Formats | Generate multiple outputs simultaneously |

---

# Step 1 — Normal Output

Run

```bash
nmap -sV -oN scan.txt 192.168.56.20
```

Explanation

Creates a plain-text report similar to what you see in the terminal.

Advantages

- Easy to read
- Easy to archive
- Suitable for documentation

---

# Step 2 — XML Output

Run

```bash
nmap -sV -oX scan.xml 192.168.56.20
```

Explanation

Stores results as structured XML.

Advantages

- Machine-readable
- Easy to import
- Widely supported

Common Uses

- Security dashboards
- Vulnerability scanners
- Custom scripts
- CI/CD pipelines

---

# Step 3 — Grepable Output

Run

```bash
nmap -sV -oG scan.gnmap 192.168.56.20
```

Explanation

Produces simplified text intended for quick parsing.

Example

```text
Host: 192.168.56.20

Ports:

22/open/tcp//ssh//

80/open/tcp//http//
```

Although still available, this format is considered legacy.

XML is recommended for new automation projects.

---

# Step 4 — All Formats

Run

```bash
nmap -sV -oA enumeration 192.168.56.20
```

Generated Files

```
enumeration.nmap

enumeration.xml

enumeration.gnmap
```

This is one of the most commonly used options during professional assessments.

---

# Comparing the Formats

| Format | Human Readable | Machine Readable | Automation | Reporting |
|----------|---------------|-----------------|------------|-----------|
| Normal | ✅ | ❌ | ❌ | ✅ |
| XML | ❌ | ✅ | ✅ | Limited |
| Grepable | Partial | Partial | Legacy | ❌ |
| All | ✅ | ✅ | ✅ | ✅ |

---

# Viewing Saved Results

Display a saved report

```bash
cat scan.txt
```

Search for open ports

```bash
grep open scan.txt
```

Count open ports

```bash
grep open scan.txt | wc -l
```

Search XML

```bash
grep ssh scan.xml
```

---

# Organizing Scan Results

Example directory

```
Scans/

├── Internal/

├── External/

├── Weekly/

├── Monthly/

└── Reports/
```

Using a consistent directory structure makes historical comparisons much easier.

---

# Best Practices

- Save every important scan.
- Use descriptive filenames.
- Include dates when appropriate.
- Store raw scan data separately from reports.
- Keep original files unchanged.

Example

```
2026-07-20_Internal_Enumeration.xml
```

---

# Common Mistakes

## Forgetting to Save Results

Once the terminal is closed, unsaved information may be lost.

---

## Overwriting Existing Files

Running

```bash
-oN scan.txt
```

again replaces the previous file.

Use unique filenames whenever possible.

---

## Using XML for Manual Reading

XML is designed for software, not humans.

Use Normal Output when reading results directly.

---

# Challenge

Perform an enumeration scan and save the results in:

- Normal format
- XML format
- All formats

Verify that every file has been created successfully.

---

# Bonus Challenge

Create a folder named:

```
Nmap_Scans
```

Inside it, save:

```
internal_scan.nmap

internal_scan.xml

internal_scan.gnmap
```

Organize your scan results as if preparing documentation for a professional assessment.

---

# Key Takeaways

- Saving scan results is an essential part of every assessment.
- Different output formats serve different purposes.
- XML is the preferred format for automation.
- Normal Output is ideal for documentation.
- The `-oA` option is a convenient way to generate multiple formats simultaneously.

---

# Next Lab

➡ **Lab 10 — Full Enumeration**

In the next lab, you will combine everything learned throughout this section into a complete reconnaissance workflow against a target system.