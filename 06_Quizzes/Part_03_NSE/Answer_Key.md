# Quiz 03 — Answer Key

> Review your answers and strengthen your understanding of the Nmap Scripting Engine (NSE), Lua, and script development concepts.

---

# Overview

This answer key includes:

- Correct Answer
- Explanation
- Related Course Chapters
- Related NSE Lessons
- Related Labs (where applicable)

Review each explanation carefully before moving to the next section.

---

## Question 1

**Correct Answer:** **B**

### Explanation

The Nmap Scripting Engine (NSE) extends Nmap by providing powerful automation and information gathering capabilities through reusable scripts.

### References

- NSE Part 01 — Introduction
- NSE Part 02 — Architecture

---

## Question 2

**Correct Answer:** **C**

### Explanation

NSE scripts are written in **Lua**, a lightweight and efficient scripting language chosen for its simplicity and performance.

### References

- NSE Part 04 — Introduction to Lua

---

## Question 3

**Correct Answer:** **B**

### Explanation

The **safe** category contains scripts that are generally considered appropriate for routine information gathering without causing significant impact.

### References

- NSE Part 03 — Safe Scripts

---

## Question 4

**Correct Answer:** **A**

### Explanation

Discovery scripts help identify additional information about hosts and services during authorized assessments.

### References

- NSE Part 03 — Discovery Scripts

---

## Question 5

**Correct Answer:** **B**

### Explanation

The **auth** category includes scripts related to authentication mechanisms and authentication-oriented information gathering.

### References

- NSE Part 03 — Auth Scripts

---

## Question 6

**Correct Answer:** **A**

### Explanation

Script categories organize NSE scripts according to their intended purpose, helping analysts choose appropriate scripts for different assessment scenarios.

---

## Question 7

**Correct Answer:** **B**

### Explanation

`hostrule` and `portrule` determine when an NSE script should execute.

### References

- NSE Part 04 — Portrule and Hostrule

---

## Question 8

**Correct Answer:** **C**

### Explanation

The `action()` function contains the primary logic executed when the script's conditions are satisfied.

### References

- NSE Part 04 — Action Function

---

## Question 9

**Correct Answer:** **A**

### Explanation

Script arguments allow users to customize script behavior without modifying the source code.

### References

- NSE Part 04 — Arguments

---

## Question 10

**Correct Answer:** **A**

### Explanation

Custom scripts allow organizations to automate tasks specific to their own infrastructure or assessment requirements.

### References

- NSE Part 05 — Final Project

---

## Question 11

**Correct Answer:** **B**

### Explanation

Lua is a lightweight scripting language designed for embedding into applications such as Nmap.

---

## Question 12

**Correct Answer:** **A**

### Explanation

NSE libraries provide reusable functions that simplify script development and reduce duplicated code.

### References

- NSE Part 04 — NSE Libraries

---

## Question 13

**Correct Answer:** **A**

### Explanation

Well-formatted output improves readability and makes reports easier to understand.

---

## Question 14

**Correct Answer:** **A**

### Explanation

New scripts should always be tested in authorized laboratory environments before being used during assessments.

### References

- NSE Part 05 — Setting Up Lab

---

## Question 15

**Correct Answer:** **A**

### Explanation

Proper error handling improves script stability and helps prevent unexpected failures.

### References

- NSE Part 04 — Error Handling
- NSE Part 05 — Error Handling Lab

---

## Question 16

**Correct Answer:** **True**

### Explanation

Lua is the programming language used by the Nmap Scripting Engine.

---

## Question 17

**Correct Answer:** **False**

### Explanation

Scripts execute only when their defined `hostrule` or `portrule` conditions are satisfied.

---

## Question 18

**Correct Answer:** **True**

### Explanation

Testing helps identify bugs and verify expected behavior before deployment.

---

## Question 19

**Correct Answer:** **True**

### Explanation

Libraries promote modular development and reduce duplicated code.

---

## Question 20

**Correct Answer:** **True**

### Explanation

Readable output simplifies analysis and improves reporting quality.

---

## Question 21

**Correct Answer:** **A**

### Explanation

The script retrieved the title of the web page served by the target.

### References

- Lab 12 — HTTP Scripts

---

## Question 22

**Correct Answer:** **A**

### Explanation

The SMB script gathered information indicating the target appears to be running Windows Server 2022.

### References

- Lab 13 — SMB Scripts

---

## Question 23

**Correct Answer:** **A**

### Explanation

Script failures should be investigated by reviewing the script, supplied arguments, permissions, and testing environment.

---

## Question 24

**Correct Answer:** **A**

### Explanation

HTTP-related NSE scripts provide structured information about web servers and web applications.

### References

- Lab 12 — HTTP Scripts

---

## Question 25

**Correct Answer:** **A**

### Explanation

When no existing script meets a specific requirement, developing a custom NSE script is an appropriate solution.

### References

- NSE Part 05 — Final Project

---

## Question 26

**Correct Answer:** **A**

### Explanation

Unexpected behavior should be investigated through debugging and controlled testing.

### References

- NSE Part 05 — Debugging Lab

---

## Question 27

**Correct Answer:** **A**

### Explanation

A `portrule` allows a script to execute only against services that meet specified conditions, such as HTTP.

### References

- NSE Part 04 — Portrule and Hostrule

---

## Question 28

**Correct Answer:** **A**

### Explanation

Modular code is easier to maintain, extend, debug, and reuse across multiple projects.

---

## Question 29

**Correct Answer:** **A**

### Explanation

Improving output formatting enhances readability without changing the functionality of the script.

### References

- NSE Part 05 — Output Formatting

---

## Question 30

**Correct Answer:** **A**

### Explanation

The Nmap Scripting Engine extends Nmap by providing flexible, reusable automation for information gathering and assessment tasks.

---

# Score Interpretation

| Score | Performance |
|--------|-------------|
| 27–30 | Excellent |
| 23–26 | Good |
| 18–22 | Fair |
| Below 18 | Review Recommended |

---

# Next Step

If you achieved **75% or higher**, continue with:

➡ **Quiz 04 — Real-World Assessments**

Otherwise, review:

- NSE Part 01–05
- Labs 11–18

before attempting the quiz again.