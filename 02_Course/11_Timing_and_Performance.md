# Nmap Master Academy

# Course 11

# Timing and Performance Optimization

---

## Course Information

**Course Number:** 11

**Difficulty:** Intermediate → Advanced

**Estimated Reading Time:** 90–120 Minutes

**Prerequisites**

- Course 01–10

---

# Table of Contents

1. Why Scan Performance Matters
2. Timing Templates (-T0 ~ -T5)
3. Host Parallelism
4. Probe Parallelism
5. RTT Timeout Options
6. Rate Limiting
7. Packet Retries
8. Scan Delay
9. Host Timeout
10. Performance Optimization Strategies
11. Real-World Examples
12. Best Practices
13. Summary

---

# 1. Why Scan Performance Matters

The default Nmap configuration is designed to work reliably in most environments.

However, default settings are not always optimal.

Sometimes you need:

- Faster scans
- Less network traffic
- Reduced detection
- Better accuracy
- Improved performance over slow links

Timing and performance options allow you to customize how aggressively Nmap scans a target.

---

# 2. Timing Templates (-T0 ~ -T5)

The easiest way to adjust scanning speed is with Timing Templates.

Command:

```bash
nmap -T4 target
```

Available templates:

| Template | Name | Description |
|----------|------|-------------|
| -T0 | Paranoid | Extremely slow, designed to evade IDS. |
| -T1 | Sneaky | Very slow scanning. |
| -T2 | Polite | Reduces bandwidth usage. |
| -T3 | Normal | Default timing. |
| -T4 | Aggressive | Faster scans on reliable networks. |
| -T5 | Insane | Maximum speed, increased risk of packet loss. |

---

## Recommended Usage

| Environment | Template |
|-------------|----------|
| Production | -T2 |
| Corporate LAN | -T3 |
| Internal Pentest | -T4 |
| Lab | -T5 |
| IDS Evasion | -T0 |

---

# 3. Host Parallelism

Nmap can scan multiple hosts simultaneously.

Instead of scanning one host at a time:

```text
Host 1

↓

Host 2

↓

Host 3
```

Nmap may scan them in parallel:

```text
Host1  ←

Host2  ←

Host3  ←

Host4  ←
```

More parallelism generally results in faster scans.

---

# 4. Probe Parallelism

Nmap can also send multiple probes to a single host at the same time.

Example:

```
Port 22

Port 80

Port 443

Port 3306

↓

Parallel Probes
```

This significantly reduces scan duration.

---

# 5. RTT Timeout Options

Network latency affects scan performance.

Important options include:

```bash
--initial-rtt-timeout
```

```bash
--max-rtt-timeout
```

```bash
--min-rtt-timeout
```

Example:

```bash
nmap --max-rtt-timeout 300ms target
```

Reducing RTT values can speed up scans on stable networks.

---

# 6. Rate Limiting

Some firewalls intentionally slow responses.

Nmap provides options to control packet transmission rates.

Example:

```bash
--min-rate 500
```

Minimum of 500 packets per second.

Example:

```bash
--max-rate 1000
```

Maximum of 1000 packets per second.

---

# 7. Packet Retries

When a packet receives no response, Nmap retransmits it.

Default behavior balances speed and accuracy.

Option:

```bash
--max-retries 2
```

Lower values:

✓ Faster

Higher values:

✓ Better accuracy

---

# 8. Scan Delay

Some IDS/IPS solutions detect rapid packet transmission.

Adding delays between probes can reduce detection.

Example:

```bash
--scan-delay 500ms
```

or

```bash
--scan-delay 2s
```

---

# 9. Host Timeout

Very slow hosts may waste scanning time.

Host Timeout allows Nmap to stop scanning after a specified duration.

Example:

```bash
--host-timeout 5m
```

Meaning:

Stop scanning a host after five minutes.

---

# 10. Performance Optimization Strategies

Small Network

```bash
nmap -T4 target
```

Large Enterprise

```bash
nmap -T4 --min-rate 1000 target
```

Slow WAN

```bash
nmap -T2 --max-retries 5 target
```

Stealth Assessment

```bash
nmap -T1 --scan-delay 1s target
```

---

# 11. Real-World Examples

Fast SYN Scan

```bash
sudo nmap -sS -T4 target
```

Aggressive Scan

```bash
sudo nmap -A -T4 target
```

Slow Scan

```bash
sudo nmap -T1 target
```

High Packet Rate

```bash
sudo nmap --min-rate 5000 target
```

---

# 12. Best Practices

✓ Use -T3 or -T4 for most assessments.

✓ Avoid -T5 on unstable networks.

✓ Increase retries on high-latency links.

✓ Reduce scan rate when testing production systems.

✓ Monitor packet loss during long scans.

✓ Balance speed with accuracy.

---

# Summary

Timing and Performance options allow Nmap to adapt to different network conditions.

Choosing the appropriate timing template and tuning packet transmission settings can dramatically improve scan efficiency while minimizing unnecessary traffic.

Understanding these options is essential for professional penetration testing and large-scale network assessments.

---

# Key Takeaways

✓ Timing Templates simplify performance tuning.

✓ RTT settings control response waiting times.

✓ Packet rate options affect scan speed.

✓ Retries improve reliability.

✓ Scan delays help reduce detection.

✓ Optimization depends on the assessment environment.

---

# Next Course

## Course 12

# Output Formats and Reporting