# Nmap Master Academy

# Course 16

# Scan Strategies

---

## Course Information

**Course Number:** 16

**Difficulty:** Advanced

**Estimated Reading Time:** 120–150 Minutes

**Prerequisites**

- Course 01–15

---

# Table of Contents

1. What is a Scan Strategy?
2. Why Scan Strategy Matters
3. Reconnaissance Workflow
4. Selecting Targets
5. Host Discovery Strategy
6. Port Scanning Strategy
7. Service Enumeration Strategy
8. Operating System Detection Strategy
9. NSE Strategy
10. Firewall Considerations
11. Internal vs External Assessments
12. Stealth vs Speed
13. Real-World Scan Strategies
14. Common Mistakes
15. Best Practices
16. Summary

---

# 1. What is a Scan Strategy?

A scan strategy is a structured approach to gathering information from a target network.

Instead of running random commands, security professionals follow a logical sequence of steps to maximize information while minimizing unnecessary traffic.

---

# Why Not Scan Everything?

Poor strategy:

```bash
sudo nmap -A -p- target
```

Advantages

✓ Easy

Disadvantages

✗ Slow

✗ Noisy

✗ Easily detected

✗ May impact production systems

Professional assessments require planning before scanning begins.

---

# 2. Why Scan Strategy Matters

An effective strategy helps:

- Reduce scan time
- Minimize network traffic
- Avoid unnecessary detection
- Improve result accuracy
- Focus on relevant systems

Scanning is not about sending more packets—it is about sending the right packets.

---

# 3. Reconnaissance Workflow

A typical Nmap assessment follows this sequence:

```text
Define Scope

↓

Identify Targets

↓

Host Discovery

↓

Port Scanning

↓

Service Detection

↓

Operating System Detection

↓

NSE Enumeration

↓

Result Validation

↓

Reporting
```

Each stage builds upon the previous one.

---

# 4. Selecting Targets

Targets may include:

- Single host
- IP range
- Subnet
- Domain
- Target list file

Examples:

```bash
nmap 192.168.1.10
```

```bash
nmap 192.168.1.0/24
```

```bash
nmap -iL targets.txt
```

Always verify that the targets are within the authorized assessment scope.

---

# 5. Host Discovery Strategy

Before scanning ports, determine which hosts are online.

Example:

```bash
nmap -sn 192.168.1.0/24
```

Benefits:

✓ Faster subsequent scans

✓ Reduced unnecessary traffic

✓ Better resource utilization

---

# 6. Port Scanning Strategy

Choose the scan type based on the assessment.

Internal network:

```bash
sudo nmap -sS
```

External assessment:

```bash
sudo nmap -sS -T2
```

Firewall analysis:

```bash
sudo nmap -sA
```

UDP services:

```bash
sudo nmap -sU
```

Use only the techniques appropriate for the environment.

---

# 7. Service Enumeration Strategy

After identifying open ports, determine the services running on them.

Command:

```bash
sudo nmap -sV target
```

Service information provides:

- Software name
- Version
- Protocol details

This information supports vulnerability analysis.

---

# 8. Operating System Detection Strategy

Determine the target operating system when appropriate.

Command:

```bash
sudo nmap -O target
```

Combine with Service Detection for a more complete profile.

---

# 9. NSE Strategy

Use NSE selectively.

Quick assessment:

```bash
nmap -sC target
```

Specific script:

```bash
nmap --script=http-title target
```

Vulnerability checks:

```bash
nmap --script=vuln target
```

Avoid running intrusive scripts unless authorized.

---

# 10. Firewall Considerations

A firewall may:

- Drop packets
- Reject packets
- Modify responses
- Rate-limit traffic

Adapt the scan strategy accordingly.

Examples:

```bash
-T2
```

```bash
--scan-delay
```

```bash
--max-retries
```

---

# 11. Internal vs External Assessments

Internal Network

Advantages:

- Lower latency
- More reliable responses
- Faster scans

Recommended:

```bash
sudo nmap -sS -T4
```

---

External Network

Challenges:

- Firewalls
- NAT
- Packet filtering
- Higher latency

Recommended:

```bash
sudo nmap -sS -T3
```

---

# 12. Stealth vs Speed

Fast Scan

Advantages

✓ Faster completion

✓ Less analyst time

Disadvantages

✗ Easier detection

---

Stealth Scan

Advantages

✓ Lower visibility

✓ Reduced IDS alerts

Disadvantages

✗ Longer duration

Choosing the right balance depends on the assessment objectives.

---

# 13. Real-World Scan Strategies

## Small Office

```bash
nmap -sn 192.168.1.0/24

↓

nmap -sS -sV

↓

nmap -O

↓

nmap -sC
```

---

## Enterprise Network

```bash
Host Discovery

↓

Top 1000 Ports

↓

Service Detection

↓

NSE

↓

Focused Full Port Scan

↓

Reporting
```

---

## Web Server Assessment

```bash
Host Discovery

↓

80/443 Scan

↓

Version Detection

↓

HTTP NSE Scripts

↓

SSL Analysis

↓

Reporting
```

---

# 14. Common Mistakes

✗ Skipping host discovery

✗ Running aggressive scans immediately

✗ Ignoring UDP services

✗ Scanning every port without necessity

✗ Assuming filtered means secure

✗ Forgetting to save results

---

# 15. Best Practices

✓ Define assessment objectives.

✓ Choose the appropriate scan type.

✓ Start with lightweight scans.

✓ Validate unusual findings.

✓ Save scan results.

✓ Respect rate limits.

✓ Obtain proper authorization.

---

# Summary

Effective scanning is not about using every Nmap option.

It is about selecting the right techniques for the environment, minimizing unnecessary traffic, and collecting reliable information.

A structured scan strategy improves efficiency, accuracy, and professionalism.

---

# Key Takeaways

✓ Always follow a structured workflow.

✓ Begin with Host Discovery.

✓ Match scan types to the environment.

✓ Balance speed and stealth.

✓ Use NSE selectively.

✓ Validate findings before reporting.

---

# Next Course

## Course 17

# Scan Optimization