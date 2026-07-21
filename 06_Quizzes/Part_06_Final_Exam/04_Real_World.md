# Final Exam — Part 04: Real-World Assessments

> This section evaluates your ability to analyze real-world infrastructures, interpret scan results, classify systems, and produce evidence-based assessment findings.

---

# Overview

Topics covered:

- Infrastructure Assessment
- Internal Networks
- DMZ
- Windows Servers
- Linux Servers
- Web Servers
- Database Servers
- Documentation
- Reporting
- Assessment Methodology

---

# Instructions

- Questions: 20
- Suggested Time: 25 Minutes

Choose the best answer for each question.

---

# Multiple Choice

## Question 1

What is the primary goal of an infrastructure assessment?

A. Modify production systems

B. Understand the environment and document observed services

C. Increase bandwidth

D. Replace vulnerability management

---

## Question 2

Why is maintaining an asset inventory important?

A. It provides a structured overview of discovered systems and services.

B. It improves internet speed.

C. It replaces Nmap output.

D. It disables unused ports.

---

## Question 3

Which environment typically hosts publicly accessible services?

A. Internal LAN

B. DMZ

C. Management VLAN

D. Backup Network

---

## Question 4

Why should database servers receive special attention?

A. They often store sensitive or business-critical information.

B. They always use Linux.

C. They replace DNS servers.

D. They improve routing.

---

## Question 5

What is the purpose of evidence-based reporting?

A. Ensure findings are supported by collected observations.

B. Reduce documentation.

C. Increase scan speed.

D. Hide assessment details.

---

## Question 6

Why should web servers be enumerated?

A. To identify technologies and exposed services.

B. To disable HTTPS.

C. To replace service detection.

D. To modify web applications.

---

## Question 7

What is the benefit of classifying discovered systems?

A. It helps prioritize analysis and reporting.

B. It changes IP addresses.

C. It reduces latency.

D. It disables logging.

---

## Question 8

What is the purpose of documenting operating systems?

A. Understand infrastructure diversity and administration methods.

B. Increase network throughput.

C. Improve DNS performance.

D. Replace service detection.

---

## Question 9

Why should assessment notes be preserved?

A. They support reporting, audits, and future reviews.

B. They replace scan results.

C. They improve scan speed.

D. They reduce bandwidth.

---

## Question 10

Which report is most appropriate for executive management?

A. Executive Summary

B. XML Output

C. Raw Console Log

D. Packet Capture

---

# True / False

## Question 11

A discovered host should always be considered critical.

- True
- False

---

## Question 12

Infrastructure documentation should include observed services.

- True
- False

---

## Question 13

Professional assessments should remain within the approved scope.

- True
- False

---

## Question 14

Evidence is more valuable than assumptions.

- True
- False

---

## Question 15

Raw scan results should be retained.

- True
- False

---

# Output Analysis

## Question 16

```
22/tcp open ssh
80/tcp open http
3306/tcp open mysql
```

What does this most likely indicate?

A. A host providing remote administration, web, and database services.

B. A firewall failure.

C. A DNS server.

D. A wireless controller.

---

## Question 17

```
445/tcp open microsoft-ds
3389/tcp open ms-wbt-server
```

Which operating system family is most likely?

A. Linux

B. Windows

C. BSD

D. macOS

---

## Question 18

```
PORT    STATE SERVICE
443/tcp open  https
```

What can be concluded?

A. The host is providing an encrypted web service.

B. FTP is running.

C. SMTP is available.

D. DNS is misconfigured.

---

# Scenario-Based

## Question 19

You discover an undocumented web server inside the DMZ.

What should you do first?

A. Document the host, identify its technologies, and include it in the assessment report.

B. Shut the server down.

C. Ignore it because it is undocumented.

D. Delete the scan results.

---

## Question 20

During an assessment, two scans produce slightly different results.

What is the most professional response?

A. Verify the findings through additional evidence before reporting.

B. Choose one result randomly.

C. Ignore both scans.

D. Report both as confirmed findings.

---

# End of Part 04

Continue to:

➡ **05_Automation.md**