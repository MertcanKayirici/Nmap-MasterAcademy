# Quiz 04 — Real-World Assessments

> Assess your ability to apply Nmap methodologies in realistic infrastructure assessment scenarios.

---

# Overview

This quiz evaluates your understanding of structured reconnaissance and infrastructure analysis in authorized environments.

Topics include:

- Internal Networks
- Web Servers
- Windows Servers
- Linux Servers
- Database Servers
- DMZ Assessments
- Reporting
- Assessment Methodology

---

# Instructions

- **Total Questions:** 30
- **Passing Score:** 75%
- **Time Limit:** 45 Minutes

Choose the most appropriate answer for each question.

---

# Multiple Choice Questions

## Question 1

What is the primary objective of an internal network assessment?

A. Delete unnecessary services

B. Understand the infrastructure and identify exposed services

C. Install software updates

D. Configure firewalls

---

## Question 2

Why is asset inventory important during an assessment?

A. It slows the assessment.

B. It documents discovered systems and technologies.

C. It replaces reporting.

D. It identifies passwords.

---

## Question 3

Which service is commonly associated with a web server?

A. SSH

B. HTTP

C. DNS

D. NTP

---

## Question 4

Why should web servers be enumerated?

A. To understand available technologies and exposed services.

B. To increase bandwidth.

C. To disable HTTP.

D. To remove SSL certificates.

---

## Question 5

Which service is commonly associated with Windows file sharing?

A. FTP

B. SMB

C. SMTP

D. DNS

---

## Question 6

Why are Linux servers frequently identified through SSH?

A. SSH is commonly enabled for administration.

B. Linux requires HTTP.

C. SSH only works on Linux.

D. SSH identifies databases.

---

## Question 7

What is the purpose of a DMZ?

A. Store backups only

B. Isolate publicly accessible services from the internal network

C. Replace firewalls

D. Disable routing

---

## Question 8

Why should database servers be documented separately?

A. They often contain critical business data.

B. They improve Wi-Fi coverage.

C. They reduce scan duration.

D. They replace DNS servers.

---

## Question 9

Which document summarizes assessment findings?

A. Inventory Report

B. Executive Report

C. Installation Guide

D. Backup Log

---

## Question 10

What should be preserved after an assessment?

A. Raw scan results

B. Temporary files only

C. Browser history

D. Screenshots only

---

# True / False

## Question 11

Assessment documentation is as important as scanning.

- True
- False

---

## Question 12

Infrastructure inventories should include discovered technologies.

- True
- False

---

## Question 13

A DMZ usually contains publicly accessible services.

- True
- False

---

## Question 14

Every discovered host should automatically be considered critical.

- True
- False

---

## Question 15

Professional reports should be evidence-based.

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

Which conclusion is most appropriate?

A. The host likely provides remote administration, web services, and database functionality.

B. The host is offline.

C. DNS is unavailable.

D. Windows Update failed.

---

## Question 17

```
443/tcp open https
```

What does this suggest?

A. An encrypted web service is available.

B. DNS failed.

C. SMTP is running.

D. SMB is unavailable.

---

## Question 18

```
445/tcp open microsoft-ds
3389/tcp open ms-wbt-server
```

Which platform is most likely being assessed?

A. Linux

B. Windows

C. macOS

D. Embedded Device

---

# Scenario-Based Questions

## Question 19

You discover multiple web servers during an assessment.

What should you do next?

A. Document technologies and continue structured enumeration.

B. Stop scanning.

C. Assume they are identical.

D. Ignore HTTPS.

---

## Question 20

A database server is discovered.

Which action is most appropriate?

A. Record the observed service and include it in the infrastructure inventory.

B. Delete the database.

C. Disable the server.

D. Ignore it.

---

## Question 21

Several Windows servers expose SMB services.

Why should they be documented?

A. They may provide important infrastructure roles.

B. They reduce scan speed.

C. They disable routing.

D. They automatically indicate vulnerabilities.

---

## Question 22

You identify both Linux and Windows systems.

Why is this information valuable?

A. It helps understand infrastructure diversity.

B. It improves internet speed.

C. It disables firewalls.

D. It changes IP addresses.

---

## Question 23

A scan reveals an unexpected web server in the DMZ.

What should be included in the report?

A. Its observed services and role.

B. User passwords.

C. Source code.

D. Firewall configuration changes.

---

## Question 24

Why should raw scan outputs be archived?

A. They support future verification and reporting.

B. They increase scan speed.

C. They replace inventories.

D. They remove false positives.

---

## Question 25

Management requests a summary instead of detailed technical output.

Which report is most appropriate?

A. Executive Summary

B. XML Output

C. Raw Log

D. Console Output

---

## Question 26

During documentation you notice inconsistent service names.

What should you do?

A. Verify findings before reporting.

B. Ignore inconsistencies.

C. Delete the report.

D. Repeat the assessment without documentation.

---

## Question 27

A host exposes SSH, HTTP, HTTPS, and MySQL.

What is the best approach?

A. Document all observed services and continue systematic analysis.

B. Disconnect the server.

C. Skip reporting.

D. Guess the operating system.

---

## Question 28

Why is infrastructure classification useful?

A. It helps understand the purpose of discovered systems.

B. It hides services.

C. It replaces Nmap.

D. It increases bandwidth.

---

## Question 29

Why should every finding be supported by evidence?

A. Professional reports require traceable observations.

B. It makes reports shorter.

C. It speeds up scanning.

D. It improves DNS.

---

## Question 30

What is the primary goal of a professional infrastructure assessment?

A. Produce structured, accurate, and well-documented findings.

B. Generate the largest possible scan.

C. Hide scan results.

D. Skip documentation.

---

# End of Quiz

Review your answers using **Answer_Key.md** before continuing.