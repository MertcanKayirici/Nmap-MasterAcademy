# Nmap Master Academy

# Course 18

# Troubleshooting Nmap Scans

---

## Course Information

**Course Number:** 18

**Difficulty:** Advanced

**Estimated Reading Time:** 90–120 Minutes

**Prerequisites**

- Course 01–17

---

# Table of Contents

1. Introduction
2. Understanding Scan Failures
3. Host Appears Down
4. All Ports Are Filtered
5. No Open Ports Found
6. Service Detection Problems
7. OS Detection Problems
8. DNS Resolution Problems
9. Firewall and IDS Issues
10. IPv6 Scanning Issues
11. Timing Problems
12. Debugging Techniques
13. Common Error Messages
14. Troubleshooting Workflow
15. Best Practices
16. Summary

---

# 1. Introduction

Even experienced penetration testers encounter scan failures.

A failed scan does not necessarily indicate that the target is offline.

Problems may be caused by:

- Firewalls
- IDS/IPS
- Packet filtering
- Routing issues
- Incorrect commands
- DNS failures
- Network latency
- Operating system behavior

Understanding how to troubleshoot these situations is an essential Nmap skill.

---

# 2. Understanding Scan Failures

When a scan does not produce the expected results, avoid making assumptions.

Instead, investigate systematically.

Typical troubleshooting process:

```text
Check Connectivity

↓

Verify Target

↓

Review Command

↓

Analyze Responses

↓

Enable Debugging

↓

Adjust Scan Options

↓

Retry
```

---

# 3. Host Appears Down

Example message:

```text
Note: Host seems down.
```

Possible causes:

- ICMP blocked
- Firewall filtering
- Incorrect IP address
- Host is offline
- VPN disconnected

Try:

```bash
nmap -Pn target
```

This skips host discovery and assumes the host is online.

---

## Verify Connectivity

Check basic connectivity first.

Linux:

```bash
ping target
```

or

```bash
traceroute target
```

Windows:

```powershell
ping target

tracert target
```

---

# 4. All Ports Are Filtered

Example:

```text
PORT

STATE

filtered
```

Possible causes:

- Firewall
- ACL
- IDS
- Security appliance
- Cloud security group

Try:

```bash
sudo nmap -sA target
```

ACK Scan helps determine whether packet filtering is present.

---

# 5. No Open Ports Found

Possible reasons:

- Wrong target
- Firewall
- Host offline
- Services stopped
- Incorrect scan type

Try scanning all ports.

```bash
sudo nmap -p- target
```

Or verify common ports.

```bash
sudo nmap -F target
```

---

# 6. Service Detection Problems

Sometimes:

```text
80/tcp

open

unknown
```

Possible reasons:

- Custom application
- Hidden banner
- Reverse proxy
- Encrypted service

Increase version detection.

```bash
sudo nmap -sV --version-all target
```

---

# 7. OS Detection Problems

Example:

```text
No exact OS matches.
```

Possible causes:

- Too few open ports
- Firewall interference
- Packet modification
- NAT devices

Try:

```bash
sudo nmap -O --osscan-guess target
```

---

# 8. DNS Resolution Problems

Symptoms:

- Slow scans
- Incorrect hostnames
- No hostname returned

Solutions:

Disable DNS

```bash
nmap -n target
```

Specify DNS servers

```bash
nmap --dns-servers 8.8.8.8 target
```

---

# 9. Firewall and IDS Issues

Firewalls may:

- Drop packets
- Reject packets
- Modify responses

Possible solutions:

Slow scanning

```bash
-T2
```

Delay packets

```bash
--scan-delay 1s
```

Reduce rate

```bash
--max-rate 100
```

---

# 10. IPv6 Scanning Issues

Common problems:

- Missing IPv6 routing
- Disabled IPv6
- Link-local addresses
- Neighbor Discovery failures

Verify IPv6 connectivity before scanning.

Linux:

```bash
ping6 target
```

---

# 11. Timing Problems

Symptoms:

- Extremely slow scans
- Frequent retransmissions
- Timeout errors

Possible solutions:

```bash
-T4
```

Reduce retries

```bash
--max-retries 2
```

Adjust RTT

```bash
--max-rtt-timeout 300ms
```

---

# 12. Debugging Techniques

Verbose mode

```bash
nmap -v target
```

More verbose

```bash
nmap -vv target
```

Debug mode

```bash
nmap -d target
```

Higher debug level

```bash
nmap -d9 target
```

Packet tracing

```bash
nmap --packet-trace target
```

Reason reporting

```bash
nmap --reason target
```

These options help identify why Nmap reached a particular conclusion.

---

# 13. Common Error Messages

| Message | Meaning | Possible Solution |
|----------|---------|-------------------|
| Host seems down | Host discovery failed | Use `-Pn` |
| All ports filtered | Firewall filtering | Try `-sA` |
| Unknown service | Banner unavailable | Use `-sV --version-all` |
| No exact OS matches | Insufficient fingerprint | Use `--osscan-guess` |
| Failed to resolve | DNS failure | Check DNS or use `-n` |
| Permission denied | Insufficient privileges | Run with sudo |

---

# 14. Troubleshooting Workflow

```text
Scan Failed

↓

Verify Target

↓

Check Connectivity

↓

Verify DNS

↓

Enable Verbose Mode

↓

Enable Debug Mode

↓

Analyze Packet Trace

↓

Modify Scan Options

↓

Retry Scan
```

---

# 15. Best Practices

✓ Verify the target before scanning.

✓ Read Nmap output carefully.

✓ Use verbose and debug modes when troubleshooting.

✓ Test changes one option at a time.

✓ Keep Nmap updated.

✓ Document recurring issues and solutions.

---

# Summary

Troubleshooting is an essential skill for effective network reconnaissance.

Rather than assuming that scan failures indicate unreachable systems, analysts should systematically verify connectivity, examine responses, and adjust scanning parameters.

A structured troubleshooting process improves both the accuracy and efficiency of security assessments.

---

# Key Takeaways

✓ Most scan failures have identifiable causes.

✓ Debugging options provide valuable diagnostic information.

✓ Firewalls and filtering frequently affect results.

✓ Timing adjustments can improve reliability.

✓ Always verify assumptions before changing scan strategies.

---

# Next Course

## Course 19

# Nmap Best Practices