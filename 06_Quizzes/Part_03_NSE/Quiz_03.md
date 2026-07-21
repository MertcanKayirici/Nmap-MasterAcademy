# Quiz 03 — Nmap Scripting Engine (NSE)

> Assess your understanding of the Nmap Scripting Engine (NSE), script categories, Lua fundamentals, and practical script usage.

---

# Overview

This quiz evaluates your understanding of the Nmap Scripting Engine and its role in authorized network assessments.

Topics include:

- NSE Architecture
- Script Categories
- Lua Fundamentals
- Script Selection
- Script Arguments
- Output Interpretation
- Custom Script Development

---

# Instructions

- **Total Questions:** 30
- **Passing Score:** 75%
- **Time Limit:** 40 Minutes

Choose the best answer for each question.

---

# Multiple Choice Questions

## Question 1

What is the primary purpose of the Nmap Scripting Engine?

A. Encrypt network traffic

B. Extend Nmap with automation and information gathering capabilities

C. Replace operating system detection

D. Compress scan results

---

## Question 2

NSE scripts are primarily written in which programming language?

A. Python

B. Bash

C. Lua

D. C#

---

## Question 3

Which NSE category is intended for scripts that are generally safe to run?

A. brute

B. safe

C. intrusive

D. exploit

---

## Question 4

Which category commonly contains service discovery scripts?

A. discovery

B. malware

C. brute

D. auth

---

## Question 5

Which category is associated with authentication-related tasks?

A. default

B. auth

C. broadcast

D. version

---

## Question 6

Why are NSE categories important?

A. They organize scripts by purpose and expected behavior.

B. They improve CPU performance.

C. They change IP addresses.

D. They encrypt scan traffic.

---

## Question 7

What determines whether an NSE script executes against a host or port?

A. Firewall rules

B. portrule or hostrule

C. DNS settings

D. Routing tables

---

## Question 8

Which function contains the primary logic of an NSE script?

A. setup()

B. execute()

C. action()

D. process()

---

## Question 9

Why are script arguments useful?

A. They allow scripts to receive configurable input.

B. They increase scan speed.

C. They disable logging.

D. They replace Lua variables.

---

## Question 10

What is one benefit of writing custom NSE scripts?

A. Tailoring automation for specific assessment needs.

B. Increasing internet speed.

C. Replacing the operating system.

D. Disabling services.

---

## Question 11

Which statement best describes Lua?

A. A database engine

B. A lightweight scripting language

C. A packet capture protocol

D. A network service

---

## Question 12

What is the purpose of NSE libraries?

A. They provide reusable functionality for scripts.

B. They replace Nmap.

C. They store scan reports.

D. They encrypt scan results.

---

## Question 13

Why is output formatting important in NSE scripts?

A. It improves readability and reporting.

B. It changes network routing.

C. It hides scan traffic.

D. It blocks open ports.

---

## Question 14

What should be done after developing a custom script?

A. Test it in an authorized lab environment.

B. Publish it immediately.

C. Delete the source code.

D. Ignore the output.

---

## Question 15

Why is error handling important in NSE development?

A. It improves reliability and stability.

B. It closes network ports.

C. It disables Nmap.

D. It increases bandwidth.

---

# True / False

## Question 16

Lua is the scripting language used by NSE.

- True
- False

---

## Question 17

Every NSE script runs against every port automatically.

- True
- False

---

## Question 18

Custom scripts should be tested before production use.

- True
- False

---

## Question 19

NSE libraries help reduce code duplication.

- True
- False

---

## Question 20

Readable output is important for reporting.

- True
- False

---

# Output Analysis

## Question 21

A scan reports:

```
| http-title:
|   Welcome to Apache2 Default Page
```

What information was obtained?

A. The web page title.

B. The operating system.

C. Firewall rules.

D. User credentials.

---

## Question 22

A scan reports:

```
| smb-os-discovery:
|   Windows Server 2022
```

What can be concluded?

A. The script identified characteristics of a Windows Server system.

B. SSH is unavailable.

C. DNS failed.

D. The host is offline.

---

## Question 23

A script returns:

```
Script execution failed.
```

What is the most appropriate next step?

A. Review the script, arguments, and environment.

B. Ignore the result.

C. Assume the target is vulnerable.

D. Delete the output.

---

# Scenario-Based Questions

## Question 24

You need general information about a newly discovered web server.

Which approach is most appropriate?

A. Use relevant HTTP-related NSE scripts.

B. Skip enumeration.

C. Guess the software version.

D. Disable logging.

---

## Question 25

Your organization has developed an internal service that is not supported by existing NSE scripts.

What is the best solution?

A. Develop a custom NSE script.

B. Stop the assessment.

C. Replace Nmap.

D. Disable the service.

---

## Question 26

During testing, your script produces inconsistent results.

What should you do first?

A. Review the code and test in a controlled environment.

B. Publish the script.

C. Ignore the issue.

D. Delete the project.

---

## Question 27

You want your script to run only against HTTP services.

Which mechanism should control this behavior?

A. portrule

B. DNS

C. Firewall

D. Routing

---

## Question 28

Why is modular code encouraged in NSE development?

A. It improves readability, reuse, and maintenance.

B. It increases network latency.

C. It replaces Lua.

D. It guarantees faster scans.

---

## Question 29

A script successfully retrieves service information but displays poorly formatted output.

What should be improved?

A. Output formatting.

B. IP addressing.

C. Network routing.

D. TCP handshakes.

---

## Question 30

What is the ultimate goal of NSE?

A. Extend Nmap with flexible automation and information gathering capabilities.

B. Replace operating systems.

C. Encrypt the internet.

D. Block all network traffic.

---

# End of Quiz

Review your answers using **Answer_Key.md** before continuing to the next section.