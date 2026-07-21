# Final Exam — Part 03: Nmap Scripting Engine (NSE)

> This section evaluates your understanding of the Nmap Scripting Engine (NSE), Lua fundamentals, script categories, and custom script development.

---

# Overview

Topics covered:

- NSE Architecture
- Script Categories
- Lua Basics
- portrule
- hostrule
- action()
- Script Arguments
- NSE Libraries
- Error Handling
- Custom Script Development

---

# Instructions

- Questions: 20
- Suggested Time: 25 Minutes

Choose the best answer for each question.

---

# Multiple Choice

## Question 1

What is the primary purpose of the Nmap Scripting Engine (NSE)?

A. Replace Nmap's scanning engine

B. Extend Nmap with automation and advanced service interaction

C. Encrypt scan traffic

D. Perform packet capture

---

## Question 2

Which programming language is used to write NSE scripts?

A. Python

B. Lua

C. Bash

D. Go

---

## Question 3

Which function determines whether a script should run against a specific port?

A. action()

B. portrule

C. hostrule

D. main()

---

## Question 4

Which function determines whether a script should execute for an entire host?

A. action()

B. portrule

C. hostrule

D. execute()

---

## Question 5

What is the purpose of the `action()` function?

A. Perform the primary logic of the script

B. Detect the operating system

C. Start host discovery

D. Define scan timing

---

## Question 6

Why are NSE libraries useful?

A. They provide reusable functions and simplify script development.

B. They increase bandwidth.

C. They replace Lua.

D. They disable debugging.

---

## Question 7

Which script category is generally considered appropriate for routine information gathering?

A. intrusive

B. safe

C. exploit

D. malware

---

## Question 8

Why should custom NSE scripts be tested in a lab before production use?

A. To verify functionality and reduce unexpected behavior.

B. To improve internet speed.

C. To modify operating systems.

D. To disable logging.

---

## Question 9

What is the benefit of script arguments?

A. They allow users to customize script behavior without modifying the source code.

B. They increase scan speed automatically.

C. They replace libraries.

D. They prevent errors.

---

## Question 10

Why is proper output formatting important?

A. It improves readability and reporting.

B. It hides scan activity.

C. It disables XML output.

D. It increases OS detection accuracy.

---

# True / False

## Question 11

Lua is an embedded scripting language.

- True
- False

---

## Question 12

Every NSE script runs against every detected service.

- True
- False

---

## Question 13

Proper error handling improves script reliability.

- True
- False

---

## Question 14

Script categories help organize scripts by purpose.

- True
- False

---

## Question 15

Custom scripts should be documented.

- True
- False

---

# Output Analysis

## Question 16

```
| http-title:
|   Welcome to Internal Portal
```

What information was collected?

A. The title of the web page.

B. The operating system version.

C. The DNS configuration.

D. The SSH banner.

---

## Question 17

```
| smb-os-discovery:
|   Windows Server 2022
```

What can be concluded?

A. The script identified the operating system through SMB-related information.

B. Linux was detected.

C. The firewall is disabled.

D. FTP is running.

---

## Question 18

```
NSE: Script execution completed.
```

What does this indicate?

A. Script execution has finished successfully from Nmap's perspective.

B. A vulnerability was confirmed.

C. The host is offline.

D. The scan was interrupted.

---

# Scenario-Based

## Question 19

Your organization requires collecting a proprietary service banner that no existing NSE script supports.

What is the best solution?

A. Develop a custom NSE script following Nmap scripting guidelines.

B. Modify the operating system.

C. Disable service detection.

D. Ignore the requirement.

---

## Question 20

During testing, an NSE script occasionally fails because a service returns unexpected data.

What is the most appropriate improvement?

A. Add input validation and error handling to make the script more robust.

B. Remove logging.

C. Disable the script.

D. Ignore the failures.

---

# End of Part 03

Continue to:

➡ **04_Real_World.md**