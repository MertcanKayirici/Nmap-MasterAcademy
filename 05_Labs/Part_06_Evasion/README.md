# Part 06 — Evasion

> Learn how Nmap's evasion and scan optimization features work, when they may be appropriate in authorized assessments, and how to interpret their results.

---

# Overview

Modern networks frequently include devices such as:

- Firewalls
- Intrusion Detection Systems (IDS)
- Intrusion Prevention Systems (IPS)
- Network Monitoring Solutions
- Web Application Firewalls (WAF)

These systems may influence how scan traffic is handled or observed.

Nmap includes several features that can change the characteristics of scan traffic. Understanding these options helps security professionals interpret scan results and evaluate network behavior during authorized testing.

This section focuses on understanding these capabilities, not on bypassing security controls.

---

# Learning Objectives

After completing this section, you will be able to:

- Explain how different network security devices affect scans.
- Understand common Nmap traffic modification options.
- Compare scan results under different conditions.
- Recognize limitations of scan techniques.
- Document observations from authorized assessments.

---

# Labs Included

| Lab | Topic |
|------|------|
| 31 | Firewall Behavior |
| 32 | IDS Observation |
| 33 | Decoy Scans |
| 34 | Packet Fragmentation |

---

# Recommended Workflow

```
Baseline Scan

↓

Modify Scan Characteristics

↓

Compare Results

↓

Analyze Differences

↓

Document Findings
```

---

# Ethical Reminder

All techniques demonstrated in this section must only be used in environments where you have explicit authorization.

The purpose of this section is to understand network behavior and improve assessment methodology.

---

# Estimated Time

6–8 Hours

---

# Next Part

➡ **Part 07 — Automation**