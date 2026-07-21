02_Course# Nmap Master Academy

# Course 07

# Port Scanning

## Part 4 – Advanced Scan Techniques

---

## Course Information

**Course Number:** 07

**Part:** 4 of 4

**Difficulty:** Intermediate → Advanced

**Estimated Reading Time:** 60–90 Minutes

**Prerequisites**

- Course 07 – Part 1
- Course 07 – Part 2
- Course 07 – Part 3

---

# Table of Contents

14. Idle Scan (-sI)

15. SCTP Scan

16. IP Protocol Scan (-sO)

17. Scan Selection Guide

18. Scan Comparison Matrix

19. Best Practices

20. Summary

---

# 14. Idle Scan (-sI)

Idle Scan is one of the most stealthy scan techniques supported by Nmap.

Instead of sending packets directly from the attacker's IP address, Nmap performs the scan through an idle "zombie" host.

The target believes the packets originated from the zombie.

---

## Requirements

The zombie host should:

- Be online
- Be mostly idle
- Use predictable IP ID values

---

## Workflow

```text
Attacker

│

├──────────────► Zombie

│                 │

│                 ▼

│          IP ID Analysis

│                 │

▼                 ▼

Target ◄──────── Zombie
```

---

## Packet Flow

```text
Attacker

↓

Probe Zombie

↓

Record IP ID

↓

Spoof SYN to Target

↓

Target replies to Zombie

↓

Zombie sends RST

↓

Probe Zombie Again

↓

Compare IP ID
```

---

## Interpretation

If the zombie's IP ID increased unexpectedly,

the target most likely responded,

indicating an open port.

---

## Command

```bash
sudo nmap -sI 192.168.1.15 192.168.1.20
```

Where:

```
192.168.1.15

↓

Zombie Host

192.168.1.20

↓

Target
```

---

## Advantages

✓ Extremely stealthy

✓ Hides the attacker's IP

✓ Useful for firewall research

---

## Disadvantages

✗ Difficult to find a suitable zombie

✗ Rarely practical today

✗ Modern operating systems randomize IP IDs

---

# 15. SCTP Scan

SCTP (Stream Control Transmission Protocol) is primarily used in telecommunications and signaling systems.

Although less common than TCP or UDP, Nmap supports SCTP scanning.

---

## SCTP INIT Scan

Command

```bash
sudo nmap -sY target
```

Workflow

```text
INIT

↓

Target

↓

INIT ACK

↓

Open
```

---

## SCTP COOKIE-ECHO Scan

Command

```bash
sudo nmap -sZ target
```

This scan helps identify SCTP services while minimizing connection establishment.

---

## Common SCTP Applications

- SS7 Networks

- SIGTRAN

- LTE Infrastructure

- Telecommunications

---

# 16. IP Protocol Scan (-sO)

Most scans focus on ports.

IP Protocol Scan determines which Layer 3 protocols are supported.

Command

```bash
sudo nmap -sO target
```

---

## Common Protocol Numbers

| Protocol | Number |
|-----------|--------|
| ICMP | 1 |
| IGMP | 2 |
| TCP | 6 |
| UDP | 17 |
| GRE | 47 |
| ESP | 50 |
| AH | 51 |
| OSPF | 89 |

---

## Example Output

```text
PROTOCOL STATE

1 open icmp

6 open tcp

17 open udp
```

---

# When Should You Use IP Protocol Scan?

Useful when:

- Auditing routers

- Assessing firewalls

- Examining VPN appliances

- Network infrastructure assessments

---

# 17. Scan Selection Guide

Choosing the appropriate scan depends on your objective.

| Situation | Recommended Scan |
|------------|------------------|
| General Enumeration | SYN Scan |
| No Root Privileges | Connect Scan |
| UDP Services | UDP Scan |
| Firewall Analysis | ACK Scan |
| Legacy Firewall Testing | FIN / NULL / Xmas |
| Anonymous Scanning | Idle Scan |
| Telecom Assessment | SCTP Scan |
| Protocol Discovery | IP Protocol Scan |

---

# 18. Scan Comparison Matrix

| Scan | Speed | Stealth | Reliability | Privileges |
|------|-------|----------|-------------|------------|
| Connect | Medium | Low | High | No |
| SYN | High | High | High | Yes |
| UDP | Low | Medium | Medium | Yes |
| ACK | High | Medium | Medium | Yes |
| Window | High | Medium | Low | Yes |
| FIN | High | High | Medium | Yes |
| NULL | High | High | Medium | Yes |
| Xmas | High | High | Medium | Yes |
| Maimon | High | Medium | Low | Yes |
| Idle | Very Low | Very High | Medium | Yes |
| SCTP | Medium | Medium | Medium | Yes |
| IP Protocol | Medium | Medium | High | Yes |

---

# Which Scan Should I Choose?

```
Need normal port scan?

        │

        ▼

Use SYN Scan

        │

No Root?

        │

        ▼

Connect Scan

        │

UDP Services?

        │

        ▼

UDP Scan

        │

Firewall Analysis?

        │

        ▼

ACK Scan

        │

Need Maximum Stealth?

        │

        ▼

Idle Scan
```

---

# Best Practices

✓ Begin with Host Discovery.

✓ Use SYN Scan whenever possible.

✓ Scan only required ports.

✓ Combine Service Detection after Port Scanning.

✓ Verify unusual results.

✓ Scan responsibly.

✓ Obtain authorization before testing.

---

# Common Mistakes

✗ Assuming filtered means closed.

✗ Ignoring UDP services.

✗ Scanning every port unnecessarily.

✗ Forgetting firewall effects.

✗ Relying on a single scan type.

---

# Summary

Port Scanning is the foundation of network reconnaissance.

Throughout this course you learned:

- Connect Scan

- SYN Scan

- UDP Scan

- ACK Scan

- Window Scan

- FIN Scan

- NULL Scan

- Xmas Scan

- Maimon Scan

- Idle Scan

- SCTP Scan

- IP Protocol Scan

You also learned how to interpret port states, compare scan types, and choose the appropriate scanning technique for different environments.

Mastering these techniques enables security professionals to perform efficient and accurate reconnaissance while understanding the strengths and limitations of each scan.

---

# Key Takeaways

✓ Every scan type has a specific purpose.

✓ SYN Scan is the preferred general-purpose scan.

✓ UDP scanning requires careful interpretation.

✓ ACK and Window Scans are useful for firewall analysis.

✓ FIN, NULL, and Xmas are stealth techniques.

✓ Idle Scan provides exceptional anonymity.

✓ Always choose the scan based on the assessment objective.

---

# Course Complete

Congratulations!

You have completed **Course 07 – Port Scanning**.

---

# Next Course

## Course 08

# Service Detection (-sV)