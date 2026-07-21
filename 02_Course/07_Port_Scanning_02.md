# Nmap Master Academy

# Course 07

# Port Scanning

## Part 2 – Advanced TCP & UDP Scans

---

## Course Information

**Course Number:** 07

**Part:** 2 of 4

**Difficulty:** Intermediate → Advanced

**Estimated Reading Time:** 60–90 Minutes

**Prerequisites**

- Course 07 – Part 1

---

# Table of Contents

7. UDP Scan (-sU)

8. TCP ACK Scan (-sA)

9. TCP Window Scan (-sW)

10. Scan Comparison

11. Best Practices

12. Summary

---

# 7. UDP Scan (-sU)

Unlike TCP scanning, UDP scanning does not rely on a connection handshake.

Instead, Nmap sends UDP datagrams and analyzes the target's response.

Command:

```bash
sudo nmap -sU 192.168.1.20
```

---

## How UDP Scan Works

```text
Nmap

 │

 │ UDP Packet

 ▼

Target

 │

 ├── UDP Reply
 │
 │      ↓
 │    Port Open
 │
 ├── ICMP Port Unreachable
 │
 │      ↓
 │    Port Closed
 │
 └── No Response
        ↓
   open|filtered
```

---

## Response Interpretation

| Response | Interpretation |
|----------|----------------|
| UDP Response | Open |
| ICMP Port Unreachable | Closed |
| ICMP Administratively Prohibited | Filtered |
| No Response | Open or Filtered |

---

## Why UDP Scans Are Slow

Unlike TCP, UDP provides no acknowledgment mechanism.

If no reply is received, Nmap must wait until the timeout expires before deciding how to classify the port.

```text
Send UDP Probe

↓

Wait

↓

No Response

↓

Retry

↓

Wait

↓

Timeout

↓

open|filtered
```

This waiting period makes UDP scanning significantly slower than TCP scanning.

---

## Advantages

✓ Discovers UDP services

✓ Essential for internal network assessments

✓ Detects DNS, SNMP, DHCP, NTP and other UDP-based services

✓ Complements TCP scans

---

## Disadvantages

✗ Slow

✗ Difficult to interpret

✗ Firewalls frequently drop UDP packets silently

✗ Many ports return no response

---

## Common UDP Services

| Port | Service |
|------|----------|
|53|DNS|
|67|DHCP Server|
|68|DHCP Client|
|69|TFTP|
|123|NTP|
|161|SNMP|
|162|SNMP Trap|
|500|ISAKMP|
|514|Syslog|

---

## Example

```bash
sudo nmap -sU -p53 192.168.1.20
```

Possible output

```text
53/udp open domain
```

---

# 8. TCP ACK Scan (-sA)

Unlike SYN Scan, ACK Scan is **not** intended to identify open ports.

Its primary purpose is to determine whether a firewall is filtering packets.

Command

```bash
sudo nmap -sA 192.168.1.20
```

---

## Packet Flow

```text
Nmap

ACK

↓

Firewall

↓

Allowed

↓

Target

↓

RST

↓

Unfiltered
```

---

## Response Interpretation

| Response | Meaning |
|----------|----------|
| RST | Unfiltered |
| No Response | Filtered |
| ICMP Error | Filtered |

---

## Advantages

✓ Excellent for firewall analysis

✓ Determines whether packet filtering exists

✓ Helps understand security policies

---

## Disadvantages

✗ Cannot determine open ports

✗ Limited use outside firewall reconnaissance

---

## Example

```bash
sudo nmap -sA 192.168.1.20
```

Possible output

```text
PORT    STATE       SERVICE

80/tcp  unfiltered  http
```

---

# 9. TCP Window Scan (-sW)

Window Scan is an extension of ACK Scan.

Instead of examining only the RST response, Nmap also evaluates the TCP Window Size returned by the target.

Command

```bash
sudo nmap -sW 192.168.1.20
```

---

## Packet Flow

```text
ACK

↓

RST

↓

Window Size

↓

Analysis
```

---

## Window Size Analysis

Some operating systems respond differently depending on whether the port is open or closed.

```text
Window > 0

↓

Likely Open
```

```text
Window = 0

↓

Likely Closed
```

Modern operating systems often use identical window sizes for all responses, making this technique less effective today.

---

## Advantages

✓ Useful against some legacy operating systems

✓ Provides additional information beyond ACK Scan

---

## Disadvantages

✗ OS dependent

✗ Unreliable on modern systems

✗ Rarely used during routine assessments

---

# Scan Comparison

| Feature | UDP | ACK | Window |
|---------|-----|------|---------|
| Detects Open Ports | Sometimes | No | Sometimes |
| Firewall Analysis | Limited | Excellent | Excellent |
| Fast | No | Yes | Yes |
| Uses TCP | No | Yes | Yes |
| Uses UDP | Yes | No | No |

---

# Best Practices

✓ Use UDP Scan for well-known UDP services.

✓ Combine UDP Scan with Service Detection.

✓ Use ACK Scan to evaluate firewall rules.

✓ Treat Window Scan as a supplemental technique.

✓ Interpret "open|filtered" results cautiously.

---

# Summary

This part introduced three specialized scan techniques.

UDP Scan focuses on discovering UDP-based services.

ACK Scan evaluates packet filtering.

Window Scan extends ACK Scan by analyzing TCP window sizes on supported operating systems.

Understanding the purpose of each scan helps you choose the most effective technique during reconnaissance.

---

# Key Takeaways

✓ UDP scanning relies heavily on ICMP responses.

✓ ACK Scan is designed for firewall analysis.

✓ Window Scan depends on TCP Window Size behavior.

✓ Modern systems reduce the effectiveness of Window Scan.

✓ Each scan type serves a different reconnaissance objective.

---

# Next Part

## Part 3 – Stealth Scan Techniques

- TCP FIN Scan (-sF)
- TCP NULL Scan (-sN)
- TCP Xmas Scan (-sX)
- TCP Maimon Scan (-sM)