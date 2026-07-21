# Lab 01 — Lab Environment

> Build a safe and isolated laboratory environment for learning and practicing Nmap.

---

# Overview

Before performing any network scan, it is essential to prepare a controlled laboratory environment.

Scanning random systems on the Internet without authorization is unethical and may be illegal. A dedicated lab allows you to safely experiment with Nmap features, understand scan results, and practice without affecting production systems.

In this lab, you will prepare the virtual machines and network configuration that will be used throughout the Nmap Master Academy.

---

# Learning Objectives

After completing this lab, you will be able to:

- Understand why a lab environment is necessary.
- Install Kali Linux.
- Install one or more vulnerable target machines.
- Configure virtual networking.
- Verify connectivity between machines.
- Install and verify Nmap.
- Perform your first connectivity test.

---

# Difficulty

⭐☆☆☆☆ Beginner

---

# Estimated Time

30–60 Minutes

---

# Prerequisites

- Basic computer knowledge
- VirtualBox or VMware installed
- At least 8 GB RAM (16 GB recommended)
- Approximately 40 GB free disk space

---

# Recommended Lab Setup

## Attacker Machine

| Component | Value |
|----------|-------|
| Operating System | Kali Linux |
| Role | Attacker |
| IP Address | 192.168.56.10 |

---

## Target Machine

Choose one or more vulnerable machines:

- Metasploitable 2
- Metasploitable 3
- OWASP Broken Web Apps
- DVWA
- Ubuntu Server
- Windows Server Evaluation

Example:

| Machine | Purpose |
|----------|----------|
| Metasploitable2 | General Practice |
| Ubuntu Server | Linux Enumeration |
| Windows Server | Windows Enumeration |

---

# Network Topology

```text
                Host Computer
                      │
         ----------------------------
         │                          │
     Kali Linux              Target Machine
   192.168.56.10           192.168.56.20
```

All machines should be connected to the same virtual network.

---

# Choosing a Network Mode

## Host-Only

Recommended for beginners.

Advantages:

- Completely isolated
- Safe
- Internet access not required

---

## NAT

Suitable when Internet access is required.

Advantages:

- Easy configuration
- Internet connectivity

Limitations:

- Some network discovery techniques may not work as expected.

---

## Bridged

Connects virtual machines directly to the physical network.

Advantages:

- Realistic environment

Use with caution and only in authorized environments.

---

# Verify IP Addresses

On Kali:

```bash
ip addr
```

or

```bash
hostname -I
```

Expected Example:

```text
192.168.56.10
```

---

On Linux Target:

```bash
ip addr
```

---

On Windows Target:

```cmd
ipconfig
```

---

# Verify Connectivity

Ping the target:

```bash
ping 192.168.56.20
```

Expected Output:

```text
64 bytes from 192.168.56.20
```

If the target responds, the virtual network is configured correctly.

---

# Verify Nmap Installation

Check the installed version:

```bash
nmap --version
```

Example:

```text
Nmap version 7.99
```

---

# First Scan

Perform a basic host discovery:

```bash
nmap -sn 192.168.56.20
```

Expected Result:

```text
Host is up.
```

---

# Save Scan Results

Save the output for future comparison.

```bash
nmap -sn 192.168.56.20 -oN lab01.txt
```

---

# Troubleshooting

## Target Does Not Respond

Possible causes:

- Incorrect IP address
- Firewall enabled
- Different virtual networks
- Target machine powered off

---

## Nmap Not Found

Verify installation:

```bash
which nmap
```

If necessary:

```bash
sudo apt install nmap
```

---

## No Network Connectivity

Check:

- VirtualBox network adapter
- VMware network settings
- Firewall rules
- IP configuration

---

# Lab Checklist

Before continuing, ensure that:

- Kali Linux is running.
- Target machine is running.
- Both machines are on the same network.
- Ping is successful.
- Nmap is installed.
- Basic scan completes successfully.

---

# Challenge

Prepare a second target machine.

Verify that both targets appear during host discovery.

Example:

```bash
nmap -sn 192.168.56.0/24
```

How many live hosts are detected?

---

# Bonus Challenge

Add a Windows virtual machine to your lab.

Verify communication between:

- Kali Linux
- Linux Target
- Windows Target

---

# Key Takeaways

- Always perform scans in an authorized environment.
- Proper network configuration is essential.
- Verify connectivity before scanning.
- Ensure Nmap is installed and functioning.
- A well-prepared lab saves time during future exercises.

---

# Next Lab

➡ **Lab 02 — Basic Host Discovery**

In the next lab, you will learn how to discover live hosts using different Nmap host discovery techniques before performing any port scan.