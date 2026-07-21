# Nmap Master Academy

# Course 12

# Output Formats and Reporting

---

## Course Information

**Course Number:** 12

**Difficulty:** Intermediate

**Estimated Reading Time:** 90–120 Minutes

**Prerequisites**

- Course 01–11

---

# Table of Contents

1. Why Save Scan Results?
2. Normal Output (-oN)
3. XML Output (-oX)
4. Grepable Output (-oG)
5. Script Kiddie Output (-oS)
6. All Formats (-oA)
7. Verbose Output (-v)
8. Debugging Output (-d)
9. Logging Best Practices
10. Parsing Scan Results
11. Reporting Workflow
12. Best Practices
13. Summary

---

# 1. Why Save Scan Results?

Running a scan is only part of the assessment.

The results should also be:

- Saved
- Reviewed
- Shared
- Compared
- Archived

Saving scan results allows security professionals to reproduce findings and generate reports.

---

# Example

Without saving:

```bash
nmap target
```

Results disappear after the terminal closes.

With output:

```bash
nmap -oN scan.txt target
```

The scan can be reviewed later.

---

# 2. Normal Output (-oN)

Normal Output saves results in a human-readable format.

Command

```bash
nmap -oN scan.txt target
```

Example

```text
PORT     STATE SERVICE

22/tcp   open  ssh

80/tcp   open  http
```

This is the most commonly used output format.

---

## Advantages

✓ Easy to read

✓ Suitable for reports

✓ Good for documentation

---

## Disadvantages

✗ Difficult to parse automatically

---

# 3. XML Output (-oX)

XML is designed for automation.

Command

```bash
nmap -oX scan.xml target
```

Example

```xml
<host>

<ports>

<port protocol="tcp" portid="80">

<state state="open"/>

</port>

</ports>

</host>
```

XML is supported by many third-party tools.

---

## Common Uses

- Automation
- Dashboards
- SIEM Integration
- Vulnerability Scanners
- Reporting Platforms

---

# 4. Grepable Output (-oG)

Grepable Output is optimized for command-line processing.

Command

```bash
nmap -oG scan.gnmap target
```

Example

```text
Host: 192.168.1.20

Ports: 22/open/tcp//ssh///
```

Although still supported, XML is generally preferred for automation.

---

# 5. Script Kiddie Output (-oS)

Script Kiddie Output produces humorous text formatting.

Command

```bash
nmap -oS funny.txt target
```

Example

```text
Interesting ports on target
```

This format exists primarily for historical and entertainment purposes and is rarely used in professional environments.

---

# 6. All Formats (-oA)

Save all major output formats simultaneously.

Command

```bash
nmap -oA audit target
```

Generated files:

```text
audit.nmap

audit.xml

audit.gnmap
```

This is one of the most useful options for penetration testers.

---

# 7. Verbose Output (-v)

Verbose mode displays additional information while scanning.

Command

```bash
nmap -v target
```

Increase verbosity further:

```bash
nmap -vv target
```

Verbose mode displays:

- Scan progress
- Hosts completed
- Timing information
- Additional status messages

---

# 8. Debugging Output (-d)

Debug mode provides detailed diagnostic information.

Command

```bash
nmap -d target
```

Higher levels:

```bash
nmap -d2 target

nmap -d5 target

nmap -d9 target
```

Debugging is useful for troubleshooting unexpected scan behavior.

---

# 9. Logging Best Practices

Always include:

- Scan date
- Target information
- Scan options
- Nmap version
- Analyst name (if applicable)

Maintain organized directories for scan results.

Example:

```text
Scans/

├── Internal/

├── External/

├── XML/

├── Reports/

└── Archives/
```

---

# 10. Parsing Scan Results

Many tools can process XML output automatically.

Examples include:

- Security dashboards
- Asset management systems
- Vulnerability management platforms
- Custom scripts

Python example:

```python
import xml.etree.ElementTree as ET

tree = ET.parse("scan.xml")
```

PowerShell example:

```powershell
[xml]$scan = Get-Content scan.xml
```

---

# 11. Reporting Workflow

Typical workflow:

```text
Run Scan

↓

Save Results

↓

Review Findings

↓

Validate Results

↓

Generate Report

↓

Archive Results
```

Good reporting is just as important as accurate scanning.

---

# 12. Best Practices

✓ Save every important scan.

✓ Prefer -oA for professional assessments.

✓ Store XML files for automation.

✓ Keep reports organized.

✓ Protect sensitive scan results.

✓ Remove obsolete reports securely.

---

# Summary

Nmap provides multiple output formats to support both human-readable documentation and automated analysis.

Choosing the correct format improves collaboration, reporting, and long-term record keeping.

Professional penetration testers almost always save scan results for future analysis.

---

# Key Takeaways

✓ -oN creates readable reports.

✓ -oX generates XML for automation.

✓ -oG provides grepable output.

✓ -oA saves all major formats.

✓ Verbose and Debug modes assist during scanning.

✓ Good reporting practices improve assessment quality.

---

# Next Course

## Course 13

# Firewall and IDS Evasion