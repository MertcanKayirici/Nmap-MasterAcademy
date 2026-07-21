# Lab 02 — Basic Host Discovery

> Learn how to identify live hosts before performing any port scan.

---

# Overview

Before scanning ports or identifying services, it is important to determine which hosts are actually online.

Scanning inactive systems wastes time and resources. Nmap provides several host discovery techniques that allow you to quickly identify reachable devices on a network.

In this lab, you will explore the most commonly used host discovery methods and learn when to use each one.

---

# Learning Objectives

After completing this lab, you will be able to:

- Understand what Host Discovery is.
- Discover live hosts on a local network.
- Compare different discovery techniques.
- Interpret Nmap host discovery results.
- Recognize when ICMP is blocked.
- Use alternative discovery methods.

---

# Difficulty

⭐☆☆☆☆ Beginner

---

# Estimated Time

30–45 Minutes

---

# Prerequisites

- Lab 01 completed
- Kali Linux
- At least one target machine
- Basic networking knowledge

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Attacker |
| Target | 192.168.56.20 | Victim |

---

# Scenario

You have connected to an unfamiliar network.

You do not know:

- Which devices are online.
- Which IP addresses are active.
- Which hosts should be scanned.

Your first task is to identify active systems before beginning further enumeration.

---

# What is Host Discovery?

Host Discovery is the process of identifying which systems on a network are currently online.

Instead of immediately scanning every port, Nmap first determines whether a host is reachable.

Benefits include:

- Faster scans
- Reduced network traffic
- Lower chance of detection
- Better resource utilization

---

# Step 1 — Scan a Single Host

Run:

```bash
nmap -sn 192.168.56.20
```

Explanation:

- `-sn` performs host discovery only.
- No port scan is performed.

Expected Output:

```text
Host is up.

Nmap done:
1 IP address (1 host up)
```

---

# Step 2 — Scan an Entire Subnet

Run:

```bash
nmap -sn 192.168.56.0/24
```

Explanation:

- Scans every address in the subnet.
- Reports only live hosts.

Example Output:

```text
Host: 192.168.56.1
Host: 192.168.56.10
Host: 192.168.56.20
```

---

# Step 3 — Disable Host Discovery

Sometimes a firewall blocks ICMP packets.

Run:

```bash
nmap -Pn 192.168.56.20
```

Explanation:

`-Pn`

Assumes the host is online and skips the discovery phase.

Use this option when:

- ICMP is blocked.
- Firewalls ignore ping requests.
- The target is known to exist.

---

# Step 4 — ARP Discovery

Run:

```bash
sudo nmap -PR 192.168.56.0/24
```

Explanation:

ARP discovery works only on local Ethernet networks.

Advantages:

- Extremely fast
- Highly accurate
- Preferred on LAN environments

---

# Step 5 — Compare Results

| Method | Speed | Reliability | Best Use Case |
|---------|-------|------------|---------------|
| -sn | Fast | High | General discovery |
| -Pn | Medium | Medium | ICMP blocked |
| -PR | Very Fast | Very High | Local LAN |

---

# Understanding the Output

Typical Output:

```text
Host is up (0.0010s latency).
```

Meaning:

- The host responded.
- Network latency is displayed.
- The system is reachable.

---

# Common Mistakes

## Using -Pn unnecessarily

`-Pn` forces Nmap to assume every host is alive.

This increases scan time.

---

## Scanning the wrong subnet

Example:

```text
192.168.0.0/24
```

instead of

```text
192.168.56.0/24
```

Always verify your IP address first.

---

## Firewall Blocking ICMP

If no hosts are found:

- Verify the target is powered on.
- Check firewall settings.
- Try `-Pn`.

---

# Challenge

Perform a host discovery scan against your subnet.

Questions:

- How many hosts are online?
- Which IP belongs to Kali?
- Which IP belongs to the target?

---

# Bonus Challenge

Add another virtual machine.

Run:

```bash
nmap -sn 192.168.56.0/24
```

How many hosts are now detected?

Can you identify each machine?

---

# Key Takeaways

- Host Discovery should usually be the first step.
- `-sn` performs discovery without port scanning.
- `-Pn` skips host discovery.
- `-PR` is the preferred method on local Ethernet networks.
- Identifying live hosts reduces scan time and improves efficiency.

---

# Next Lab

➡ **Lab 03 — Basic Port Scanning**

In the next lab, you will scan the discovered host for open TCP ports and learn how to interpret Nmap's port scan results.