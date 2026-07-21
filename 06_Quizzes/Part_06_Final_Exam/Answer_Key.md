# Final Examination — Answer Key

> This document provides the correct answers, explanations, and references for all questions included in the Nmap Master Academy Final Examination.

---

# Overview

This answer key covers:

- Part 01 — Fundamentals
- Part 02 — Scanning & Enumeration
- Part 03 — Nmap Scripting Engine (NSE)
- Part 04 — Real-World Assessments
- Part 05 — Automation

For each question you will find:

- Correct Answer
- Explanation
- Related Course Chapters
- Related Labs
- Related Reference Material (where applicable)

---

# Part 01 — Fundamentals

## Question 1

**Correct Answer:** B

### Explanation

Nmap is primarily used to discover hosts and analyze network services within an authorized environment.

### References

- Course 01 — Introduction to Nmap
- Lab 01 — Basic Host Discovery

---

## Question 2

**Correct Answer:** C

### Explanation

TCP provides reliable, ordered, connection-oriented communication through acknowledgments and retransmissions.

### References

- Course 02 — TCP/IP Fundamentals
- Reference — TCP vs UDP

---

## Question 3

**Correct Answer:** C

### Explanation

The `ping` command primarily uses the Internet Control Message Protocol (ICMP) to determine whether a host is reachable.

### References

- Course 03 — Host Discovery

---

## Question 4

**Correct Answer:** A

### Explanation

An open TCP port indicates that an application is actively listening for incoming connections on that port.

### References

- Course 04 — Ports and Services
- Lab 02 — Port Scanning

---

## Question 5

**Correct Answer:** B

### Explanation

The `-sS` option performs a TCP SYN (half-open) scan, one of Nmap's most commonly used scan types.

### References

- Course 05 — Scan Types
- Lab 03 — SYN Scan

---

## Question 6

**Correct Answer:** A

### Explanation

Host discovery identifies which systems are online before performing more detailed scanning.

### References

- Course 03 — Host Discovery
- Lab 01 — Ping Sweep

---

## Question 7

**Correct Answer:** B

### Explanation

A TCP Connect Scan (`-sT`) completes the full TCP three-way handshake before closing the connection.

### References

- Course 05 — Connect Scan

---

## Question 8

**Correct Answer:** B

### Explanation

When no scan type is specified, Nmap performs TCP scanning by default (subject to privileges and platform).

### References

- Course 05 — Default Scan Behavior

---

## Question 9

**Correct Answer:** B

### Explanation

UDP scanning is generally slower because many UDP services do not respond unless they receive valid application-specific requests.

### References

- Course 06 — UDP Scanning
- Reference — TCP vs UDP

---

## Question 10

**Correct Answer:** B

### Explanation

Security assessments must remain within the authorized scope to comply with legal, ethical, and organizational requirements.

### References

- Course 01 — Ethics and Authorization

---

## Question 11

**Correct Answer:** True

### Explanation

TCP is a connection-oriented protocol that establishes a session before transmitting data.

---

## Question 12

**Correct Answer:** False

### Explanation

UDP is connectionless and does not guarantee packet delivery, ordering, or retransmission.

---

## Question 13

**Correct Answer:** True

### Explanation

Host discovery reduces unnecessary scanning by identifying reachable systems before performing detailed assessments.

---

## Question 14

**Correct Answer:** False

### Explanation

An open port only indicates that a service is listening; it does not automatically indicate a security vulnerability.

---

## Question 15

**Correct Answer:** True

### Explanation

Nmap can perform host discovery independently of port scanning using options such as `-sn`.

---

## Question 16

**Correct Answer:** A

### Explanation

The output confirms that the target responded successfully and is reachable on the network.

### References

- Lab 01 — Host Discovery

---

## Question 17

**Correct Answer:** A

### Explanation

Ports 80 (HTTP) and 443 (HTTPS) indicate that the target is providing web services.

### References

- Lab 02 — Service Identification

---

## Question 18

**Correct Answer:** A

### Explanation

The scan found three open TCP ports while the remaining scanned TCP ports were closed.

### References

- Lab 02 — Interpreting Scan Results

---

## Question 19

**Correct Answer:** A

### Explanation

For large networks, performing host discovery first identifies active systems and avoids wasting time scanning inactive hosts.

### References

- Lab 01 — Large Network Host Discovery

---

## Question 20

**Correct Answer:** A

### Explanation

Professional assessment methodology begins with host discovery before vulnerability-focused or service-specific scanning.

### References

- Course 03 — Host Discovery
- Lab 25 — Assessment Methodology


---

# Part 02 — Scanning & Enumeration

## Question 21

**Correct Answer:** B

### Explanation

The `-sV` option performs service version detection, allowing Nmap to identify the software and version running on open ports.

### References

- Course 07 — Service Version Detection
- Lab 05 — Service Enumeration

---

## Question 22

**Correct Answer:** B

### Explanation

The `-O` option enables operating system detection by analyzing network responses and comparing them with Nmap's fingerprint database.

### References

- Course 08 — OS Detection
- Lab 06 — Operating System Detection

---

## Question 23

**Correct Answer:** A

### Explanation

The `-A` option enables several advanced features simultaneously, including OS detection, version detection, default NSE scripts, and traceroute.

### References

- Course 09 — Aggressive Scan
- Lab 07 — Aggressive Scanning

---

## Question 24

**Correct Answer:** D

### Explanation

Timing template **T5** is the fastest available template. It should only be used in stable and authorized environments because it can increase packet loss and reduce accuracy.

### References

- Course 10 — Timing Templates
- Lab 08 — Performance Optimization

---

## Question 25

**Correct Answer:** A

### Explanation

Aggressive timing templates may overload slower networks or devices, causing missed responses and less reliable scan results.

### References

- Course 10 — Timing Templates

---

## Question 26

**Correct Answer:** A

### Explanation

XML output is structured and machine-readable, making it the preferred format for automation, parsing, and report generation.

### References

- Course 12 — Output Formats
- Lab 36 — Python Automation

---

## Question 27

**Correct Answer:** A

### Explanation

Service enumeration gathers additional information about running services, including banners, versions, and supported protocols.

### References

- Course 07 — Service Detection
- Lab 05 — Service Enumeration

---

## Question 28

**Correct Answer:** A

### Explanation

Version detection helps identify software versions that may require updates or further security assessment.

### References

- Course 07 — Version Detection

---

## Question 29

**Correct Answer:** A

### Explanation

Scanning only required ports reduces scan duration and focuses the assessment on relevant services.

### References

- Lab 04 — Targeted Port Scanning

---

## Question 30

**Correct Answer:** B

### Explanation

A SYN Scan (`-sS`) performs a half-open TCP handshake, making it more efficient than a full TCP Connect Scan in many environments.

### References

- Course 05 — TCP Scan Types
- Lab 03 — SYN Scan

---

## Question 31

**Correct Answer:** True

### Explanation

Version detection communicates with the target service to identify software information.

---

## Question 32

**Correct Answer:** False

### Explanation

Operating system detection is probabilistic and depends on available responses, network conditions, and fingerprint accuracy.

---

## Question 33

**Correct Answer:** True

### Explanation

Many UDP services do not respond unless they receive valid requests, which often results in the `open|filtered` state.

---

## Question 34

**Correct Answer:** True

### Explanation

XML output is widely used for integration with automation frameworks and reporting tools.

---

## Question 35

**Correct Answer:** True

### Explanation

Timing templates should always be selected according to the assessment environment to balance speed and reliability.

---

## Question 36

**Correct Answer:** A

### Explanation

The output shows that Nmap successfully identified service names and versions running on the target.

### References

- Lab 05 — Service Enumeration

---

## Question 37

**Correct Answer:** A

### Explanation

This information was produced through operating system detection, indicating the detected device type and probable operating system.

### References

- Course 08 — OS Detection

---

## Question 38

**Correct Answer:** A

### Explanation

The `open|filtered` state indicates that Nmap cannot determine whether the UDP port is open or filtered because no definitive response was received.

### References

- Course 06 — UDP Scanning

---

## Question 39

**Correct Answer:** A

### Explanation

A structured workflow begins with host discovery, followed by port scanning, service detection, and finally documentation and reporting.

### References

- Lab 25 — Complete Infrastructure Assessment

---

## Question 40

**Correct Answer:** A

### Explanation

Outdated service versions should be documented and recommended for further investigation or remediation according to organizational policies.

### References

- Lab 25 — Assessment Reporting

---

# Part 03 — Nmap Scripting Engine (NSE)

## Question 41

**Correct Answer:** B

### Explanation

The Nmap Scripting Engine (NSE) extends Nmap by adding automation capabilities, advanced service interaction, and custom scripting support.

### References

- NSE Part 01 — Introduction
- NSE Part 02 — Architecture

---

## Question 42

**Correct Answer:** B

### Explanation

NSE scripts are written in **Lua**, a lightweight scripting language designed for embedding into applications.

### References

- NSE Part 04 — Introduction to Lua

---

## Question 43

**Correct Answer:** B

### Explanation

The `portrule` function determines whether a script should execute against a specific port or service.

### References

- NSE Part 04 — Portrule

---

## Question 44

**Correct Answer:** C

### Explanation

The `hostrule` function determines whether an NSE script should execute once for an entire host.

### References

- NSE Part 04 — Hostrule

---

## Question 45

**Correct Answer:** A

### Explanation

The `action()` function contains the primary logic executed after the rule conditions have been satisfied.

### References

- NSE Part 04 — Action Function

---

## Question 46

**Correct Answer:** A

### Explanation

NSE libraries provide reusable functions that simplify development, reduce duplicated code, and improve script maintainability.

### References

- NSE Part 04 — NSE Libraries

---

## Question 47

**Correct Answer:** B

### Explanation

The **safe** category contains scripts intended for routine information gathering with minimal impact on the target.

### References

- NSE Part 03 — Script Categories

---

## Question 48

**Correct Answer:** A

### Explanation

Testing scripts in a controlled laboratory environment helps verify expected behavior and reduce the risk of unexpected results during authorized assessments.

### References

- NSE Part 05 — Script Testing

---

## Question 49

**Correct Answer:** A

### Explanation

Script arguments allow users to customize script behavior without modifying the script source code.

### References

- NSE Part 04 — Script Arguments

---

## Question 50

**Correct Answer:** A

### Explanation

Readable output improves analysis, reporting, and troubleshooting while making script results easier to interpret.

### References

- NSE Part 05 — Output Formatting

---

## Question 51

**Correct Answer:** True

### Explanation

Lua is a lightweight embedded scripting language selected for NSE because of its simplicity and performance.

---

## Question 52

**Correct Answer:** False

### Explanation

NSE scripts execute only when their defined `hostrule` or `portrule` conditions evaluate to true.

---

## Question 53

**Correct Answer:** True

### Explanation

Proper error handling improves script stability, reliability, and user experience.

---

## Question 54

**Correct Answer:** True

### Explanation

Script categories organize scripts according to their intended purpose, making script selection easier.

---

## Question 55

**Correct Answer:** True

### Explanation

Documentation improves maintainability and helps other users understand script functionality and usage.

---

## Question 56

**Correct Answer:** A

### Explanation

The `http-title` script retrieved the HTML title of the web page served by the target.

### References

- Lab 12 — HTTP NSE Scripts

---

## Question 57

**Correct Answer:** A

### Explanation

The `smb-os-discovery` script gathered operating system information using SMB-related responses from the target.

### References

- Lab 13 — SMB NSE Scripts

---

## Question 58

**Correct Answer:** A

### Explanation

The message indicates that Nmap completed execution of all selected NSE scripts. It does not imply that vulnerabilities were found.

### References

- NSE Part 02 — Execution Flow

---

## Question 59

**Correct Answer:** A

### Explanation

When existing scripts do not meet organizational requirements, developing a custom NSE script is the recommended solution.

### References

- NSE Part 05 — Custom Script Development

---

## Question 60

**Correct Answer:** A

### Explanation

Unexpected input should be handled through validation, exception handling, and proper error management to improve script robustness.

### References

- NSE Part 05 — Error Handling
- Lab 18 — Custom Script Development

---

# Part 04 — Real-World Assessments

## Question 61

**Correct Answer:** B

### Explanation

The primary objective of an infrastructure assessment is to understand the environment, identify systems and services, and accurately document the observed findings.

### References

- Lab 19 — Internal Network Assessment
- Lab 25 — Complete Infrastructure Assessment

---

## Question 62

**Correct Answer:** A

### Explanation

An asset inventory provides a structured overview of discovered hosts, operating systems, services, and technologies, serving as the foundation for reporting.

### References

- Lab 25 — Assessment Documentation

---

## Question 63

**Correct Answer:** B

### Explanation

A DMZ (Demilitarized Zone) is designed to host publicly accessible services while separating them from the internal network.

### References

- Lab 24 — DMZ Assessment

---

## Question 64

**Correct Answer:** A

### Explanation

Database servers frequently contain sensitive or business-critical information and should receive special attention during infrastructure assessments.

### References

- Lab 23 — Database Server Assessment

---

## Question 65

**Correct Answer:** A

### Explanation

Evidence-based reporting ensures that every conclusion is supported by observed data rather than assumptions.

### References

- Course 12 — Reporting
- Lab 25 — Assessment Reporting

---

## Question 66

**Correct Answer:** A

### Explanation

Web server enumeration identifies technologies, services, software versions, and other useful information for documentation and further analysis.

### References

- Lab 20 — Web Server Assessment

---

## Question 67

**Correct Answer:** A

### Explanation

Classifying discovered systems helps prioritize analysis, understand infrastructure roles, and improve reporting.

### References

- Lab 25 — Infrastructure Classification

---

## Question 68

**Correct Answer:** A

### Explanation

Documenting operating systems provides insight into infrastructure diversity, administration methods, and technology distribution.

### References

- Lab 22 — Linux Assessment
- Lab 21 — Windows Assessment

---

## Question 69

**Correct Answer:** A

### Explanation

Assessment notes support future reviews, audits, troubleshooting, and report generation.

### References

- Lab 25 — Documentation

---

## Question 70

**Correct Answer:** A

### Explanation

An Executive Summary communicates key findings in a concise, business-oriented format suitable for management.

### References

- Course 12 — Reporting

---

## Question 71

**Correct Answer:** False

### Explanation

Not every discovered host is equally important. Criticality depends on business function, exposure, and organizational context.

---

## Question 72

**Correct Answer:** True

### Explanation

Professional documentation should include observed services, operating systems, and other verified information.

---

## Question 73

**Correct Answer:** True

### Explanation

Security assessments must always remain within the approved scope and authorization.

---

## Question 74

**Correct Answer:** True

### Explanation

Professional assessments should always rely on evidence rather than assumptions.

---

## Question 75

**Correct Answer:** True

### Explanation

Raw scan results provide supporting evidence and should be preserved for verification and future reference.

---

## Question 76

**Correct Answer:** A

### Explanation

The combination of SSH, HTTP, and MySQL services suggests that the host provides remote administration, web services, and database functionality.

### References

- Lab 25 — Infrastructure Analysis

---

## Question 77

**Correct Answer:** B

### Explanation

Ports 445 (SMB) and 3389 (Remote Desktop Protocol) are commonly associated with Microsoft Windows systems.

### References

- Lab 21 — Windows Server Assessment

---

## Question 78

**Correct Answer:** A

### Explanation

Port 443 indicates an HTTPS service, meaning the host is providing encrypted web communication.

### References

- Lab 20 — Web Server Assessment

---

## Question 79

**Correct Answer:** A

### Explanation

Unexpected systems should be documented, identified, and included in the assessment report for further review. Evidence should always be collected before drawing conclusions.

### References

- Lab 24 — DMZ Assessment
- Lab 25 — Assessment Reporting

---

## Question 80

**Correct Answer:** A

### Explanation

When scan results differ, additional verification should be performed before documenting conclusions. Repeatability and evidence are essential components of professional assessments.

### References

- Lab 25 — Assessment Methodology

---

# Part 05 — Automation

## Question 81

**Correct Answer:** B

### Explanation

Automation improves consistency, scalability, and efficiency by reducing repetitive manual work while ensuring standardized assessment workflows.

### References

- Course 20 — Automation
- Lab 36 — Python Automation
- Lab 37 — Enterprise Assessment Workflow

---

## Question 82

**Correct Answer:** A

### Explanation

Reusable scan profiles ensure assessments are performed consistently across multiple engagements and simplify recurring security evaluations.

### References

- Lab 37 — Scan Profiles

---

## Question 83

**Correct Answer:** B

### Explanation

Python is commonly used for advanced Nmap automation because it provides excellent support for process execution, XML parsing, reporting, and workflow orchestration.

### References

- Lab 36 — Python Automation

---

## Question 84

**Correct Answer:** A

### Explanation

Bash scripting automates repetitive command-line tasks, making it ideal for executing Nmap commands, looping through targets, and managing assessment workflows.

### References

- Lab 35 — Bash Automation

---

## Question 85

**Correct Answer:** A

### Explanation

Raw scan results should always be preserved because they serve as supporting evidence, allow verification of findings, and enable future analysis.

### References

- Lab 37 — Reporting Workflow

---

## Question 86

**Correct Answer:** A

### Explanation

XML is the preferred output format for automation because it is structured, machine-readable, and easily parsed by scripts and reporting tools.

### References

- Course 12 — Output Formats
- Lab 36 — XML Processing

---

## Question 87

**Correct Answer:** A

### Explanation

Separating scanning, parsing, and reporting into individual modules improves maintainability, scalability, testing, and code reuse.

### References

- Lab 37 — Modular Automation Design

---

## Question 88

**Correct Answer:** A

### Explanation

Logging records execution details, errors, and progress, making troubleshooting, auditing, and verification significantly easier.

### References

- Lab 37 — Logging and Reporting

---

## Question 89

**Correct Answer:** A

### Explanation

Timestamped output directories preserve historical assessment data and prevent previous results from being overwritten.

### References

- Lab 37 — Project Organization

---

## Question 90

**Correct Answer:** A

### Explanation

Modular design allows large automation projects to remain maintainable, reusable, and easier to extend over time.

### References

- Lab 37 — Modular Architecture

---

## Question 91

**Correct Answer:** True

### Explanation

Automation workflows should always include proper error handling to ensure reliable execution and graceful recovery from failures.

---

## Question 92

**Correct Answer:** True

### Explanation

Python can execute external programs such as Nmap using modules like `subprocess`, making it suitable for automation workflows.

---

## Question 93

**Correct Answer:** False

### Explanation

Automation assists professionals but does not replace human judgment, analysis, or decision-making during security assessments.

---

## Question 94

**Correct Answer:** True

### Explanation

A consistent directory structure improves organization, collaboration, maintenance, and long-term project scalability.

---

## Question 95

**Correct Answer:** True

### Explanation

Assessment logs provide valuable evidence for troubleshooting, auditing, and reviewing completed assessments and should therefore be retained.

---

## Question 96

**Correct Answer:** A

### Explanation

Organizing logs, reports, results, and target files into separate directories improves project management and simplifies navigation.

### References

- Lab 37 — Enterprise Project Structure

---

## Question 97

**Correct Answer:** A

### Explanation

Separating functionality into `scanner.py`, `parser.py`, and `reporter.py` demonstrates the software engineering principle of separation of responsibilities (separation of concerns).

### References

- Lab 37 — Modular Automation Design

---

## Question 98

**Correct Answer:** A

### Explanation

Timestamped assessment directories ensure that every assessment is stored independently, preserving historical data and preventing accidental overwrites.

### References

- Lab 37 — Result Management

---

## Question 99

**Correct Answer:** A

### Explanation

Recurring infrastructure assessments are best handled through reusable automation workflows that include standardized scan profiles, logging, parsing, and reporting.

### References

- Lab 37 — Enterprise Assessment Workflow

---

## Question 100

**Correct Answer:** A

### Explanation

A well-designed automation workflow should log unreachable targets, continue processing the remaining systems, and include all issues in the final report rather than terminating the entire assessment.

### References

- Lab 37 — Error Handling
- Lab 37 — Enterprise Reporting

---

# Final Score Interpretation

| Score | Result |
|--------|--------|
| 90–100 | Outstanding |
| 80–89 | Excellent |
| 75–79 | Passed |
| 60–74 | Needs Improvement |
| Below 60 | Review Required |

---

# Recommendations

If your score is below **75%**, review the following before retaking the examination:

- Course Chapters
- NSE Lessons
- Reference Materials
- Hands-on Labs
- Section Quizzes

---

# Congratulations

Congratulations on completing the **Nmap Master Academy Final Examination**.

By reaching this stage, you have demonstrated knowledge of:

- Networking Fundamentals
- Host Discovery
- Port Scanning
- Service Enumeration
- Operating System Detection
- Nmap Scripting Engine (NSE)
- Infrastructure Assessment
- Enterprise Reporting
- Automation Workflows
- Professional Assessment Methodology

Continue practicing in authorized environments, contribute to the cybersecurity community, and keep expanding your knowledge through continuous learning.
