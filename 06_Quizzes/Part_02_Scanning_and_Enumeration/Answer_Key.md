# Quiz 02 — Answer Key

> Review your answers and reinforce your understanding of Nmap scanning and enumeration techniques.

---

# Overview

This answer key includes:

- Correct Answer
- Explanation
- Related Course Chapters
- Related Labs (where applicable)

Review the explanations carefully, especially for any questions you answered incorrectly.

---

## Question 1

**Correct Answer:** **B**

### Explanation

Port scanning identifies which ports on a target are open, closed, or filtered. It is one of the primary functions of Nmap.

### References

- Course 07 — Port Scanning
- Lab 03 — Basic Port Scanning

---

## Question 2

**Correct Answer:** **C**

### Explanation

Service Detection attempts to identify the application running on an open port and, when possible, determine its version.

### References

- Course 08 — Service Detection
- Lab 06 — Service Detection

---

## Question 3

**Correct Answer:** **C**

### Explanation

Operating System Detection analyzes characteristics of network responses to estimate the target operating system.

### References

- Course 09 — OS Detection
- Lab 07 — OS Detection

---

## Question 4

**Correct Answer:** **B**

### Explanation

Version detection helps identify the software and version associated with an open service.

### References

- Course 08 — Service Detection

---

## Question 5

**Correct Answer:** **B**

### Explanation

Knowing the software version helps administrators understand which technologies are deployed and maintain accurate inventories.

### References

- Course 08 — Service Detection

---

## Question 6

**Correct Answer:** **A**

### Explanation

OS Detection provides insight into the platform being assessed, which helps with documentation and infrastructure analysis.

### References

- Course 09 — OS Detection

---

## Question 7

**Correct Answer:** **B**

### Explanation

After identifying active hosts, the next logical step is to determine which ports are open.

### References

- Course 06 — Host Discovery
- Course 07 — Port Scanning

---

## Question 8

**Correct Answer:** **B**

### Explanation

Aggressive Scan combines several detection features, such as OS detection, version detection, script scanning, and traceroute.

### References

- Course 16 — Scan Strategies
- Lab 08 — Aggressive Scan

---

## Question 9

**Correct Answer:** **B**

### Explanation

Proper documentation supports reporting, auditing, and future comparison of scan results.

### References

- Course 12 — Output and Reporting

---

## Question 10

**Correct Answer:** **A**

### Explanation

Different output formats make it easier to archive, parse, and report scan results.

### References

- Course 12 — Output and Reporting
- Lab 09 — Output Formats

---

## Question 11

**Correct Answer:** **A**

### Explanation

XML is structured, machine-readable, and widely supported by automation tools.

### References

- Course 12 — Output and Reporting

---

## Question 12

**Correct Answer:** **A**

### Explanation

XML output is commonly used because it is easy to parse programmatically and integrate into reporting workflows.

### References

- Course 12 — Output and Reporting

---

## Question 13

**Correct Answer:** **B**

### Explanation

Enumeration involves collecting detailed information about discovered services, hosts, and infrastructure.

### References

- Lab 10 — Full Enumeration

---

## Question 14

**Correct Answer:** **A**

### Explanation

Open ports often reveal valuable information about available services and technologies within the authorized environment.

### References

- Course 08 — Service Detection

---

## Question 15

**Correct Answer:** **B**

### Explanation

Enumeration is a structured process of gathering detailed information after discovering reachable systems.

### References

- Lab 10 — Full Enumeration

---

## Question 16

**Correct Answer:** **True**

### Explanation

Enumeration normally begins after identifying active hosts during Host Discovery.

---

## Question 17

**Correct Answer:** **False**

### Explanation

OS Detection provides an estimate and may not always be completely accurate.

---

## Question 18

**Correct Answer:** **True**

### Explanation

Service Detection often identifies both the application name and version.

---

## Question 19

**Correct Answer:** **True**

### Explanation

Saving scan results is considered a professional best practice for documentation and reporting.

---

## Question 20

**Correct Answer:** **False**

### Explanation

Enumeration frequently involves validating and confirming collected information.

---

## Question 21

**Correct Answer:** **A**

### Explanation

SSH, HTTP, and HTTPS commonly indicate a system providing remote administration and web services.

---

## Question 22

**Correct Answer:** **A**

### Explanation

OS Detection identified characteristics commonly associated with a Linux operating system.

---

## Question 23

**Correct Answer:** **B**

### Explanation

Port 445 is commonly associated with Microsoft's SMB protocol, which provides file and printer sharing.

---

## Question 24

**Correct Answer:** **B**

### Explanation

After Host Discovery, the next step is structured port scanning followed by service enumeration.

### References

- Lab 03 — Basic Port Scanning
- Lab 06 — Service Detection

---

## Question 25

**Correct Answer:** **B**

### Explanation

Saving structured scan outputs improves reporting, future analysis, and automation.

### References

- Course 12 — Output and Reporting
- Lab 09 — Output Formats

---

# Score Interpretation

| Score | Performance |
|--------|-------------|
| 23–25 | Excellent |
| 19–22 | Good |
| 15–18 | Fair |
| Below 15 | Review the Enumeration section before continuing. |

---

# Next Step

If you achieved a score of **75% or higher**, continue with:

➡ **Quiz 03 — Nmap Scripting Engine (NSE)**

Otherwise, review the following materials before attempting the quiz again:

- Course 07 — Port Scanning
- Course 08 — Service Detection
- Course 09 — OS Detection
- Course 12 — Output and Reporting
- Labs 06–10