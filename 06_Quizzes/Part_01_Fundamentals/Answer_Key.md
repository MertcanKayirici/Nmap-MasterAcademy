# Quiz 01 — Answer Key

> Review your answers and reinforce your understanding of the fundamental concepts covered in Quiz 01.

---

# Overview

This answer key provides:

- Correct Answer
- Explanation
- Related Course Chapters
- Recommended Lab (when applicable)

Use this document as a learning resource rather than simply checking your score.

---

## Question 1

**Correct Answer:** **B**

### Explanation

Nmap is primarily used for **network discovery** and **security auditing**. It helps identify hosts, open ports, running services, and operating systems within authorized environments.

### References

- Course 01 — Introduction
- Lab 02 — Basic Host Discovery

---

## Question 2

**Correct Answer:** **B**

### Explanation

TCP is a **connection-oriented** protocol that establishes a reliable communication session before transmitting data.

### References

- Course 04 — TCP

---

## Question 3

**Correct Answer:** **B**

### Explanation

UDP is a **connectionless** protocol. It does not establish a session before sending data, making it faster but less reliable than TCP.

### References

- Course 05 — UDP

---

## Question 4

**Correct Answer:** **B**

### Explanation

A network port is a logical communication endpoint used by applications and services to exchange data over a network.

### References

- Course 03 — Ports

---

## Question 5

**Correct Answer:** **C**

### Explanation

Port **80/TCP** is the default port commonly used by HTTP web servers.

### References

- Course 03 — Ports

---

## Question 6

**Correct Answer:** **D**

### Explanation

HTTPS uses **443/TCP** to provide encrypted web communication using TLS.

### References

- Course 03 — Ports

---

## Question 7

**Correct Answer:** **B**

### Explanation

SSH (Secure Shell) commonly listens on **TCP port 22** for secure remote administration.

### References

- Course 03 — Ports

---

## Question 8

**Correct Answer:** **C**

### Explanation

Host Discovery determines whether a target host is reachable before more detailed scanning begins.

### References

- Course 06 — Host Discovery
- Lab 02 — Basic Host Discovery

---

## Question 9

**Correct Answer:** **A**

### Explanation

Port scanning identifies which ports are open, closed, or filtered on a target system.

### References

- Course 07 — Port Scanning
- Lab 03 — Basic Port Scanning

---

## Question 10

**Correct Answer:** **B**

### Explanation

Service Detection identifies the application or service running on an open port and may determine its version.

### References

- Course 08 — Service Detection
- Lab 06 — Service Detection

---

## Question 11

**Correct Answer:** **B**

### Explanation

DNS translates human-readable domain names into IP addresses.

### References

- Course 14 — DNS Resolution

---

## Question 12

**Correct Answer:** **C**

### Explanation

The Internet Layer of the TCP/IP model is responsible for routing packets between networks.

### References

- Course 02 — Network Basics

---

## Question 13

**Correct Answer:** **B**

### Explanation

Many Nmap scan techniques rely on the behavior of TCP and UDP. Understanding these protocols helps interpret scan results correctly.

### References

- Course 04 — TCP
- Course 05 — UDP

---

## Question 14

**Correct Answer:** **B**

### Explanation

TCP provides reliable, ordered, and error-checked communication between hosts.

### References

- Course 04 — TCP

---

## Question 15

**Correct Answer:** **C**

### Explanation

UDP is lightweight and connectionless, making it suitable for applications where speed is more important than guaranteed delivery.

### References

- Course 05 — UDP

---

## Question 16

**Correct Answer:** **False**

### Explanation

Nmap supports scanning a wide variety of operating systems, including Linux, Windows, macOS, and many network devices.

---

## Question 17

**Correct Answer:** **True**

### Explanation

An open port generally indicates that an application or service is actively listening for incoming connections.

---

## Question 18

**Correct Answer:** **True**

### Explanation

TCP includes mechanisms such as acknowledgments and retransmissions to help ensure reliable packet delivery.

### References

- Course 04 — TCP

---

## Question 19

**Correct Answer:** **False**

### Explanation

UDP does not establish a connection and therefore does not use a three-way handshake.

### References

- Course 05 — UDP

---

## Question 20

**Correct Answer:** **True**

### Explanation

A strong understanding of networking fundamentals improves the accuracy of scan interpretation and troubleshooting.

---

## Question 21

**Correct Answer:** **B**

### Explanation

Ports **80** and **443** typically indicate that web services are available on the target.

---

## Question 22

**Correct Answer:** **B**

### Explanation

"Host is up" indicates that the target responded to Nmap's host discovery probes.

---

## Question 23

**Correct Answer:** **C**

### Explanation

Port **22/TCP** is commonly associated with the SSH service.

---

## Question 24

**Correct Answer:** **B**

### Explanation

Before performing detailed scans, it is good practice to determine which hosts are active within the authorized scope.

### References

- Lab 02 — Basic Host Discovery

---

## Question 25

**Correct Answer:** **B**

### Explanation

Host discovery helps avoid unnecessary scans against unreachable systems and improves assessment efficiency.

---

# Score Interpretation

| Score | Performance |
|--------|-------------|
| 23–25 | Excellent |
| 19–22 | Good |
| 15–18 | Fair |
| Below 15 | Review the Fundamentals section before continuing. |

---

# Next Step

If you scored **75% or higher**, continue with:

➡ **Quiz 02 — Scanning and Enumeration**

Otherwise, review the following resources:

- Course 01–08
- Labs 01–06

Then attempt this quiz again to strengthen your understanding.