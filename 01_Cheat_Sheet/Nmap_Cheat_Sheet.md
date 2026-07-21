# Nmap Master Academy

## Nmap Cheat Sheet

**Version:** 1.0

**Document Type:** Quick Reference Guide

**Language:** English

**Difficulty Level:** Beginner • Intermediate • Advanced

**Compatible With:** Nmap 7.x+

---

### Description

This cheat sheet provides a concise reference to the most commonly used Nmap commands, scan techniques, options, and best practices. It is designed for cybersecurity students, penetration testers, system administrators, and security professionals who need a fast and reliable reference during assessments or while learning Nmap.

---

**Master Academy**

Professional Cybersecurity Documentation Series

---

# 1. Basic Syntax

The following commands demonstrate the most common ways to execute an Nmap scan. They serve as the foundation for almost every scanning task.

| Command | Description |
|----------|-------------|
| `nmap <target>` | Scan the top 1000 TCP ports of the target. |
| `nmap 192.168.1.10` | Scan a single IPv4 address. |
| `nmap scanme.nmap.org` | Scan a hostname or domain name. |
| `nmap target1 target2` | Scan multiple targets in a single command. |
| `nmap 192.168.1.0/24` | Scan every host within a subnet using CIDR notation. |
| `nmap -iL targets.txt` | Read scan targets from a text file. |
| `nmap --exclude 192.168.1.5 192.168.1.0/24` | Exclude one or more hosts from the scan. |
| `nmap --exclude-file exclude.txt 192.168.1.0/24` | Exclude hosts listed in a file. |

---

### Syntax

```bash
nmap [Scan Type(s)] [Options] <Target Specification>
```

---

### General Structure

```text
nmap [SCAN TYPE] [DISCOVERY OPTIONS] [PORT OPTIONS] [OUTPUT OPTIONS] TARGET
```

---

### Example Commands

```bash
# Scan a single host
nmap 192.168.1.10

# Scan multiple hosts
nmap 192.168.1.10 192.168.1.20

# Scan an entire subnet
nmap 192.168.1.0/24

# Scan targets from a file
nmap -iL targets.txt

# Exclude a host
nmap --exclude 192.168.1.5 192.168.1.0/24
```

---

### Notes

- Targets can be specified using IP addresses, hostnames, CIDR ranges, or input files.
- Unless otherwise specified, Nmap scans the top 1000 most common TCP ports.
- Many scan types require elevated (root/administrator) privileges.
- Combine multiple options to customize scan behavior.

---

# 2. Target Specification

Target specification defines which hosts or networks Nmap will scan. Targets can be individual hosts, IP ranges, subnets, hostnames, IPv6 addresses, or lists stored in files.

---

## Single Host

| Command | Description |
|----------|-------------|
| `nmap 192.168.1.10` | Scan a single IPv4 host. |
| `nmap scanme.nmap.org` | Scan a hostname. |
| `nmap localhost` | Scan the local machine. |

---

## Multiple Hosts

| Command | Description |
|----------|-------------|
| `nmap 192.168.1.10 192.168.1.20` | Scan multiple hosts. |
| `nmap host1 host2 host3` | Scan multiple hostnames. |

---

## IP Range

| Command | Description |
|----------|-------------|
| `nmap 192.168.1.1-50` | Scan hosts from .1 to .50. |
| `nmap 10.0.0.10-100` | Scan a custom IP range. |

---

## CIDR Notation

| Command | Description |
|----------|-------------|
| `nmap 192.168.1.0/24` | Scan a Class C subnet (256 addresses). |
| `nmap 10.0.0.0/16` | Scan a larger network. |
| `nmap 172.16.0.0/12` | Scan an enterprise network range. |

---

## Input File

| Command | Description |
|----------|-------------|
| `nmap -iL targets.txt` | Read targets from a text file. |

Example **targets.txt**

```text
192.168.1.10
192.168.1.20
scanme.nmap.org
example.com
```

---

## Excluding Targets

| Command | Description |
|----------|-------------|
| `nmap --exclude 192.168.1.15 192.168.1.0/24` | Exclude specific hosts. |
| `nmap --exclude-file exclude.txt 192.168.1.0/24` | Exclude hosts listed in a file. |

Example **exclude.txt**

```text
192.168.1.5
192.168.1.8
192.168.1.100
```

---

## IPv6 Targets

| Command | Description |
|----------|-------------|
| `nmap -6 fe80::1` | Scan a single IPv6 host. |
| `nmap -6 2001:db8::/64` | Scan an IPv6 network. |

---

## Random Targets

| Command | Description |
|----------|-------------|
| `nmap -iR 10` | Scan 10 random Internet hosts. |
| `nmap -iR 100 --exclude 192.168.1.1` | Exclude specific addresses while scanning random hosts. |

---

## Target Specification Summary

| Target Type | Example |
|--------------|---------|
| Single IP | `192.168.1.10` |
| Hostname | `scanme.nmap.org` |
| Multiple Hosts | `192.168.1.10 192.168.1.20` |
| IP Range | `192.168.1.1-50` |
| CIDR | `192.168.1.0/24` |
| IPv6 | `-6 2001:db8::/64` |
| File Input | `-iL targets.txt` |
| Exclude Hosts | `--exclude`, `--exclude-file` |
| Random Targets | `-iR 50` |

---

## Best Practices

- Prefer CIDR notation when scanning entire networks.
- Use input files (`-iL`) for large target lists.
- Exclude critical systems when they should not be scanned.
- Verify that hostnames resolve correctly before scanning.
- Use IPv6 mode (`-6`) only when the target network supports IPv6.

---

## Notes

- Nmap supports IPv4 and IPv6 targets.
- Multiple target specification methods can be combined.
- Host discovery behavior depends on the selected scan options.
- Always ensure you have authorization before scanning any network.

---

# 3. Host Discovery

Host Discovery is the process of determining whether a target host is online before performing a port scan. Nmap supports multiple discovery techniques depending on the target environment and network restrictions.

---

## Common Host Discovery Commands

| Command | Description |
|----------|-------------|
| `-sn` | Perform host discovery only (disable port scanning). |
| `-Pn` | Skip host discovery and treat all targets as online. |
| `-PE` | Send ICMP Echo Request probes. |
| `-PP` | Send ICMP Timestamp Request probes. |
| `-PM` | Send ICMP Address Mask Request probes. |
| `-PS` | Send TCP SYN probes to discover hosts. |
| `-PA` | Send TCP ACK probes to discover hosts. |
| `-PU` | Send UDP probes to discover hosts. |
| `-PY` | Send SCTP INIT probes. |
| `-PR` | Perform ARP discovery on local networks. |

---

## ARP Discovery

| Command | Description |
|----------|-------------|
| `nmap -PR 192.168.1.0/24` | Discover hosts using ARP requests. |

**Notes**

- Used automatically on local Ethernet networks.
- Fastest and most reliable method on LANs.
- Does not rely on ICMP.

---

## ICMP Discovery

| Command | Description |
|----------|-------------|
| `-PE` | ICMP Echo Request |
| `-PP` | ICMP Timestamp Request |
| `-PM` | ICMP Address Mask Request |

Example

```bash
nmap -PE 192.168.1.0/24
```

---

## TCP Discovery

| Command | Description |
|----------|-------------|
| `-PS22` | SYN Ping on port 22 |
| `-PS80,443` | SYN Ping on multiple ports |
| `-PA80` | ACK Ping |
| `-PA22,80,443` | ACK Ping on multiple ports |

Example

```bash
nmap -PS80,443 192.168.1.0/24
```

---

## UDP Discovery

| Command | Description |
|----------|-------------|
| `-PU53` | UDP Ping on port 53 |
| `-PU161` | UDP Ping on SNMP port |

Example

```bash
nmap -PU53 192.168.1.0/24
```

---

## SCTP Discovery

| Command | Description |
|----------|-------------|
| `-PY` | SCTP INIT Ping |

Example

```bash
nmap -PY 192.168.1.0/24
```

---

## Disable Host Discovery

| Command | Description |
|----------|-------------|
| `-Pn` | Assume every host is online and skip host discovery. |

Example

```bash
nmap -Pn 192.168.1.10
```

**Use Cases**

- ICMP is blocked by a firewall.
- The target drops discovery probes.
- You already know the target is online.

---

## Host Discovery Comparison

| Method | Speed | Reliability | Typical Usage |
|--------|------:|------------:|---------------|
| ARP | Very High | Excellent | Local networks |
| ICMP | High | Good | Internal networks |
| TCP SYN | Medium | Excellent | Firewall bypass |
| TCP ACK | Medium | Good | Filtered networks |
| UDP | Low | Moderate | UDP-based services |
| SCTP | Low | Limited | SCTP environments |

---

## Example Commands

```bash
# Host discovery only
nmap -sn 192.168.1.0/24

# Skip host discovery
nmap -Pn 192.168.1.10

# ICMP Echo discovery
nmap -PE 192.168.1.0/24

# TCP SYN discovery
nmap -PS80,443 192.168.1.0/24

# TCP ACK discovery
nmap -PA80 192.168.1.0/24

# UDP discovery
nmap -PU53 192.168.1.0/24

# ARP discovery
nmap -PR 192.168.1.0/24
```

---

## Best Practices

- Use **ARP discovery (`-PR`)** on local Ethernet networks whenever possible.
- Use **TCP SYN discovery (`-PS`)** when ICMP traffic is filtered.
- Use **`-Pn`** only when you know the target is online or host discovery is being blocked.
- Combine discovery methods for improved reliability in complex environments.
- Avoid unnecessary `-Pn` scans on large networks, as they can significantly increase scan time.

---

## Notes

- Host discovery determines whether a target appears to be online before port scanning.
- Different networks may respond differently to ICMP, TCP, UDP, or ARP probes.
- Firewalls and IDS/IPS devices can affect discovery results.
- Host discovery can be customized using one or more probe types.

---

# 4. Port Specification

Port specification controls which ports Nmap scans on the target system. By default, Nmap scans the 1000 most common TCP ports, but you can customize the scan to include specific ports, ranges, protocols, or all available ports.

---

## Common Port Selection Options

| Command | Description |
|----------|-------------|
| `-p 80` | Scan a single port. |
| `-p 22,80,443` | Scan multiple ports. |
| `-p 1-1000` | Scan a port range. |
| `-p-` | Scan all 65535 TCP ports. |
| `--top-ports 100` | Scan the 100 most common ports. |
| `-F` | Fast scan (top 100 ports). |

---

## Port Ranges

| Command | Description |
|----------|-------------|
| `-p 1-1024` | Scan well-known ports. |
| `-p 1025-49151` | Scan registered ports. |
| `-p 49152-65535` | Scan dynamic/private ports. |

---

## Mixed Port Lists

| Command | Description |
|----------|-------------|
| `-p 22,80,443,8080` | Scan selected ports. |
| `-p 21-25,80,443,3306` | Combine ranges and individual ports. |

---

## TCP and UDP Port Selection

| Command | Description |
|----------|-------------|
| `-p T:80,443` | Scan TCP ports only. |
| `-p U:53,161` | Scan UDP ports only. |
| `-p T:22,80,U:53,161` | Scan TCP and UDP ports simultaneously. |

---

## Excluding Ports

| Command | Description |
|----------|-------------|
| `--exclude-ports 80` | Exclude port 80. |
| `--exclude-ports 22,80,443` | Exclude multiple ports. |
| `--exclude-ports 1-1024` | Exclude a port range. |

---

## Port Selection Examples

```bash
# Scan port 80
nmap -p 80 192.168.1.10

# Scan SSH, HTTP and HTTPS
nmap -p 22,80,443 192.168.1.10

# Scan ports 1-1000
nmap -p 1-1000 192.168.1.10

# Scan all TCP ports
nmap -p- 192.168.1.10

# Scan top 100 ports
nmap --top-ports 100 192.168.1.10

# Fast scan
nmap -F 192.168.1.10

# Scan TCP and UDP together
nmap -sS -sU -p T:22,80,U:53 192.168.1.10
```

---

## Port Categories

| Range | Category | Description |
|--------|----------|-------------|
| 0-1023 | Well-Known Ports | Standard Internet services. |
| 1024-49151 | Registered Ports | Vendor and application services. |
| 49152-65535 | Dynamic / Private Ports | Temporary or ephemeral ports. |

---

## Quick Reference

| Option | Function |
|---------|----------|
| `-p` | Specify ports to scan. |
| `-p-` | Scan every TCP port. |
| `-F` | Fast scan. |
| `--top-ports` | Scan the most common ports. |
| `--exclude-ports` | Exclude ports from scanning. |

---

## Best Practices

- Scan only the ports you need whenever possible.
- Use `--top-ports` for quick reconnaissance.
- Use `-p-` during penetration tests when a complete assessment is required.
- Combine TCP and UDP scans when comprehensive coverage is needed.
- Save scan results for later analysis.

---

## Notes

- Nmap scans the top 1000 TCP ports by default.
- UDP scanning requires the `-sU` scan type.
- Scanning all ports (`-p-`) takes significantly longer than scanning common ports.
- Firewalls may hide open ports by marking them as filtered.

---

# 5. Scan Types

Nmap supports multiple scan techniques, each designed for different environments and objectives. Selecting the appropriate scan type depends on factors such as speed, stealth, firewall behavior, privileges, and the information you want to collect.

---

## Common Scan Types

| Scan Type | Option | Description |
|-----------|--------|-------------|
| TCP SYN Scan | `-sS` | Performs a half-open TCP scan without completing the handshake. Default choice for privileged users. |
| TCP Connect Scan | `-sT` | Completes the full TCP three-way handshake. Used when raw packet privileges are unavailable. |
| UDP Scan | `-sU` | Scans UDP services. Slower than TCP scans. |
| TCP ACK Scan | `-sA` | Determines firewall filtering rules rather than open ports. |
| TCP Window Scan | `-sW` | Similar to ACK scan but uses TCP window size to identify open ports on some systems. |
| TCP Maimon Scan | `-sM` | Uses FIN/ACK packets. Effective only against certain TCP implementations. |
| TCP NULL Scan | `-sN` | Sends packets without TCP flags. Useful for bypassing simple packet filters. |
| TCP FIN Scan | `-sF` | Sends FIN packets instead of SYN packets. |
| TCP Xmas Scan | `-sX` | Sends FIN, PSH and URG flags together. |
| IP Protocol Scan | `-sO` | Identifies supported IP protocols instead of TCP/UDP ports. |
| Idle Scan | `-sI` | Performs a stealth scan using a zombie host. |
| SCTP INIT Scan | `-sY` | Scans SCTP services using INIT packets. |
| SCTP COOKIE-ECHO Scan | `-sZ` | Uses SCTP COOKIE-ECHO packets for scanning. |

---

## TCP SYN Scan (`-sS`)

```bash
nmap -sS 192.168.1.10
```

**Purpose**

- Fast
- Stealthy
- Most commonly used TCP scan

**Requirements**

- Root/Administrator privileges

---

## TCP Connect Scan (`-sT`)

```bash
nmap -sT 192.168.1.10
```

**Purpose**

- Uses the operating system's TCP stack.
- Completes the full TCP handshake.
- Useful without elevated privileges.

---

## UDP Scan (`-sU`)

```bash
nmap -sU 192.168.1.10
```

**Purpose**

- Detect UDP services.
- Commonly used for DNS, SNMP, DHCP, NTP and TFTP.

---

## ACK Scan (`-sA`)

```bash
nmap -sA 192.168.1.10
```

**Purpose**

- Detect firewall rules.
- Distinguish filtered from unfiltered ports.
- Does **not** determine whether a port is open.

---

## NULL Scan (`-sN`)

```bash
nmap -sN 192.168.1.10
```

Sends packets without any TCP flags.

---

## FIN Scan (`-sF`)

```bash
nmap -sF 192.168.1.10
```

Uses FIN packets instead of SYN packets.

---

## Xmas Scan (`-sX`)

```bash
nmap -sX 192.168.1.10
```

Sets the FIN, PSH and URG flags simultaneously.

---

## Window Scan (`-sW`)

```bash
nmap -sW 192.168.1.10
```

Uses TCP Window size differences on some operating systems.

---

## Maimon Scan (`-sM`)

```bash
nmap -sM 192.168.1.10
```

Uses FIN/ACK packets to identify open ports on some systems.

---

## Idle Scan (`-sI`)

```bash
nmap -sI zombie_host target
```

A stealth scanning technique that uses a third-party zombie host to hide the attacker's IP address.

---

## IP Protocol Scan (`-sO`)

```bash
nmap -sO 192.168.1.10
```

Detects supported IP protocols such as TCP, UDP, ICMP, GRE and ESP.

---

## SCTP INIT Scan (`-sY`)

```bash
nmap -sY 192.168.1.10
```

Discovers SCTP services using INIT packets.

---

## SCTP COOKIE-ECHO Scan (`-sZ`)

```bash
nmap -sZ 192.168.1.10
```

Uses SCTP COOKIE-ECHO packets to identify SCTP services.

---

## Scan Type Comparison

| Scan | Speed | Stealth | Root Required | Detect Open Ports |
|------|------:|--------:|--------------:|------------------:|
| SYN (`-sS`) | High | High | Yes | Yes |
| Connect (`-sT`) | Medium | Low | No | Yes |
| UDP (`-sU`) | Low | Medium | Yes | Yes |
| ACK (`-sA`) | High | Medium | Yes | No |
| Window (`-sW`) | High | Medium | Yes | Limited |
| FIN (`-sF`) | Medium | High | Yes | Limited |
| NULL (`-sN`) | Medium | High | Yes | Limited |
| Xmas (`-sX`) | Medium | High | Yes | Limited |
| Idle (`-sI`) | Low | Very High | Yes | Yes |
| IP Protocol (`-sO`) | Medium | Medium | Yes | Protocol Discovery |

---

## Best Practices

- Use **`-sS`** for most TCP reconnaissance tasks.
- Use **`-sT`** when raw packet privileges are unavailable.
- Combine **`-sU`** with TCP scans for complete service discovery.
- Use **`-sA`** to analyze firewall filtering.
- Reserve **Idle Scan (`-sI`)** for advanced scenarios due to its setup requirements.

---

## Notes

- Different scan types generate different network traffic and may trigger security devices differently.
- No single scan type is ideal for every environment.
- Combining scan techniques often provides more complete results.

---

# 6. Service & Version Detection

Service and Version Detection enables Nmap to identify the application or service running on an open port. It performs probe-based fingerprinting to determine software names, versions, and additional information.

---

## Common Version Detection Options

| Command | Description |
|----------|-------------|
| `-sV` | Detect service versions. |
| `--version-light` | Perform a light version detection scan. |
| `--version-all` | Try every available probe for maximum accuracy. |
| `--version-intensity <0-9>` | Set the version detection intensity level. |

---

## Basic Version Detection

```bash
nmap -sV 192.168.1.10
```

Scans open ports and attempts to identify the running services and software versions.

---

## Version Detection Intensity

| Level | Description |
|-------:|-------------|
| 0 | Use only the most common probes (fastest). |
| 1-3 | Low intensity scanning. |
| 4-6 | Balanced speed and accuracy. |
| 7-8 | Aggressive version detection. |
| 9 | Use all available probes (slowest, most accurate). |

Example

```bash
nmap -sV --version-intensity 5 192.168.1.10
```

---

## Light Version Detection

```bash
nmap -sV --version-light 192.168.1.10
```

**Advantages**

- Faster scanning
- Less network traffic
- Good for large environments

---

## Maximum Version Detection

```bash
nmap -sV --version-all 192.168.1.10
```

**Advantages**

- Highest detection accuracy
- Uses every available service probe

**Disadvantages**

- Slower
- Generates more network traffic

---

## Combining with Other Scan Types

```bash
# SYN Scan + Version Detection
nmap -sS -sV 192.168.1.10

# Default Scripts + Version Detection
nmap -sC -sV 192.168.1.10

# Aggressive Scan
nmap -A 192.168.1.10
```

---

## Example Output

```text
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 9.2
80/tcp   open  http    Apache httpd 2.4.57
3306/tcp open  mysql   MySQL 8.0.36
```

---

## Service Detection Workflow

```text
Open Port
     │
     ▼
Send Service Probes
     │
     ▼
Receive Response
     │
     ▼
Compare with Nmap Signature Database
     │
     ▼
Identify Service and Version
```

---

## Commonly Detected Services

| Port | Service |
|------|---------|
| 21 | FTP |
| 22 | SSH |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 143 | IMAP |
| 443 | HTTPS |
| 445 | SMB |
| 3306 | MySQL |
| 3389 | RDP |
| 5432 | PostgreSQL |

---

## Best Practices

- Use `-sV` during reconnaissance to identify running services.
- Combine `-sV` with `-sC` for richer information.
- Increase version intensity only when additional accuracy is required.
- Save scan results for future analysis and reporting.

---

## Notes

- Version detection works only on open ports.
- Some services intentionally hide or modify version information.
- Firewalls and intrusion prevention systems may interfere with version detection.
- Higher intensity scans improve accuracy but increase scan duration. 

---

# 7. Operating System Detection

Operating System Detection enables Nmap to identify the target's operating system by analyzing TCP/IP stack behavior. Nmap compares collected network fingerprints against its extensive OS fingerprint database to estimate the operating system, version, device type, and network distance.

---

## Common OS Detection Options

| Command | Description |
|----------|-------------|
| `-O` | Enable operating system detection. |
| `--osscan-limit` | Attempt OS detection only on promising targets. |
| `--osscan-guess` | Guess the OS when an exact match cannot be determined. |

---

## Basic OS Detection

```bash
nmap -O 192.168.1.10
```

Attempts to determine the operating system of the target host.

---

## OS Detection with Service Detection

```bash
nmap -O -sV 192.168.1.10
```

Performs operating system detection together with service version detection.

---

## Aggressive Scan

```bash
nmap -A 192.168.1.10
```

Enables:

- OS Detection
- Version Detection
- Default NSE Scripts
- Traceroute

---

## Limit OS Detection

```bash
nmap --osscan-limit -O 192.168.1.10
```

Only performs OS detection on hosts that have at least one open and one closed TCP port.

**Advantages**

- Faster scanning
- Fewer unnecessary probes
- Reduced network traffic

---

## Aggressive OS Guessing

```bash
nmap --osscan-guess -O 192.168.1.10
```

Attempts to identify the operating system even when confidence is low.

Useful when:

- Fingerprints are incomplete.
- Firewalls modify responses.
- The target does not perfectly match known signatures.

---

## Example Output

```text
OS details:
Linux 6.x
Device type: general purpose
Running: Linux 6.X
OS CPE:
cpe:/o:linux:linux_kernel:6
Network Distance: 1 hop
```

---

## Detection Process

```text
Target Host
      │
      ▼
TCP/IP Probes
      │
      ▼
Analyze Responses
      │
      ▼
Compare with Nmap Fingerprint Database
      │
      ▼
Estimated Operating System
```

---

## Information Identified

| Information | Example |
|--------------|---------|
| Operating System | Windows 11 |
| Linux Distribution | Ubuntu 24.04 |
| Kernel Version | Linux 6.x |
| Device Type | Router |
| Vendor | Cisco |
| Network Distance | 2 hops |
| Accuracy | 98% |

---

## Supported Device Types

| Device |
|---------|
| Desktop |
| Laptop |
| Server |
| Router |
| Switch |
| Firewall |
| Printer |
| VoIP Phone |
| NAS |
| IoT Device |
| Game Console |
| Smartphone |

---

## Best Practices

- Use `-O` after identifying open ports.
- Combine `-O` with `-sV` for better fingerprint accuracy.
- Use `--osscan-limit` when scanning large networks.
- Treat OS detection as an estimate rather than an absolute result.
- Verify critical findings with additional enumeration techniques.

---

## Limitations

- Firewalls may alter TCP/IP responses.
- NAT devices can affect fingerprint accuracy.
- Some operating systems intentionally disguise their network behavior.
- Closed ports are often required for reliable fingerprinting.

---

## Notes

- OS detection requires root/Administrator privileges on most systems.
- Detection accuracy depends on the quality of the target's responses.
- New operating systems may not immediately exist in the Nmap fingerprint database.
- Results are confidence-based estimates rather than guarantees.

---

# 8. Nmap Scripting Engine (NSE)

The Nmap Scripting Engine (NSE) extends Nmap's capabilities beyond basic port scanning. NSE scripts can perform service detection, vulnerability discovery, brute-force testing, malware detection, configuration auditing, information gathering, and many other security-related tasks.

---

## Common NSE Options

| Command | Description |
|----------|-------------|
| `-sC` | Run the default NSE scripts. |
| `--script=<script>` | Execute a specific NSE script. |
| `--script=<category>` | Execute all scripts in a category. |
| `--script-args` | Pass arguments to NSE scripts. |
| `--script-help` | Display script documentation. |
| `--script-updatedb` | Update the local NSE script database. |

---

## Default Scripts

```bash
nmap -sC 192.168.1.10
```

Runs the default collection of safe and commonly useful scripts.

Default scripts typically perform:

- Basic service enumeration
- SSL certificate inspection
- HTTP title detection
- SMB information gathering
- SSH host key collection

---

## Running a Specific Script

```bash
nmap --script=http-title 192.168.1.10
```

Example output

```text
PORT   STATE SERVICE
80/tcp open  http

| http-title:
| Login Portal
```

---

## Running Multiple Scripts

```bash
nmap --script=http-title,http-headers,http-server-header 192.168.1.10
```

Multiple scripts are separated using commas.

---

## Running a Script Category

```bash
nmap --script=vuln 192.168.1.10
```

Executes every script belonging to the **vuln** category.

---

## Passing Script Arguments

```bash
nmap --script ftp-anon --script-args ftp-anon.maxlist=20 192.168.1.10
```

Some scripts accept custom parameters that modify their behavior.

---

## Display Script Documentation

```bash
nmap --script-help http-title
```

Displays:

- Description
- Categories
- Usage
- Arguments
- Author
- Output examples

---

## Update the Script Database

```bash
nmap --script-updatedb
```

Updates the local NSE database after adding new scripts.

---

# Common NSE Categories

| Category | Purpose |
|----------|---------|
| `auth` | Authentication checks |
| `broadcast` | Broadcast discovery |
| `brute` | Brute-force authentication |
| `default` | Default safe scripts |
| `discovery` | Information gathering |
| `dos` | Denial-of-Service testing |
| `exploit` | Exploitation checks |
| `external` | Uses third-party resources |
| `fuzzer` | Fuzz testing |
| `intrusive` | Potentially disruptive scripts |
| `malware` | Malware detection |
| `safe` | Safe for production environments |
| `version` | Service version enhancement |
| `vuln` | Vulnerability detection |

---

## Popular NSE Scripts

| Script | Purpose |
|---------|---------|
| `http-title` | Retrieve webpage title |
| `http-headers` | Display HTTP headers |
| `http-enum` | Enumerate web content |
| `ssl-cert` | Retrieve SSL certificate |
| `ssh-hostkey` | Collect SSH host keys |
| `ftp-anon` | Check anonymous FTP access |
| `smb-os-discovery` | Identify Windows systems |
| `smb-enum-shares` | Enumerate SMB shares |
| `mysql-info` | Gather MySQL information |
| `dns-brute` | DNS subdomain brute force |
| `whois-domain` | Perform WHOIS lookup |
| `banner` | Retrieve service banners |

---

## Example Commands

### Default Enumeration

```bash
nmap -sC 192.168.1.10
```

---

### Version Detection + Default Scripts

```bash
nmap -sV -sC 192.168.1.10
```

---

### Vulnerability Scan

```bash
nmap --script vuln 192.168.1.10
```

---

### HTTP Enumeration

```bash
nmap --script http-enum 192.168.1.10
```

---

### SMB Enumeration

```bash
nmap --script smb-enum-shares,smb-os-discovery 192.168.1.10
```

---

### SSL Certificate Information

```bash
nmap --script ssl-cert 192.168.1.10
```

---

## Script Execution Workflow

```text
Open Port
     │
     ▼
Load Selected Script(s)
     │
     ▼
Send Protocol-Specific Requests
     │
     ▼
Analyze Responses
     │
     ▼
Generate Structured Output
```

---

## Best Practices

- Start with **`-sC`** during reconnaissance.
- Combine **`-sV`** with NSE for more accurate results.
- Review script documentation before using advanced scripts.
- Use intrusive or exploit-related scripts only in authorized environments.
- Keep the NSE database updated to access the latest scripts.

---

## Notes

- NSE is written in the Lua programming language.
- Nmap includes hundreds of built-in scripts.
- Some scripts require authentication credentials or additional arguments.
- Script execution time depends on the selected scripts and target responsiveness.
- Certain scripts may generate significant network traffic or trigger security monitoring systems.

---

# 9. Timing & Performance

Timing and Performance options allow you to control how aggressively Nmap sends probes, retries failed requests, manages parallelism, and handles timeouts. Proper tuning can significantly reduce scan time while balancing accuracy and network impact.

---

## Timing Templates

| Option | Name | Description |
|--------|------|-------------|
| `-T0` | Paranoid | Extremely slow. Designed to avoid IDS detection. |
| `-T1` | Sneaky | Very slow with reduced network footprint. |
| `-T2` | Polite | Slows scanning to reduce bandwidth usage. |
| `-T3` | Normal | Default timing template. |
| `-T4` | Aggressive | Faster scanning on reliable networks. |
| `-T5` | Insane | Fastest timing. Suitable only for very reliable networks. |

---

## Timing Template Examples

```bash
# Default timing
nmap -T3 192.168.1.10

# Aggressive scan
nmap -T4 192.168.1.10

# Maximum speed
nmap -T5 192.168.1.10
```

---

## Packet Rate Control

| Option | Description |
|----------|-------------|
| `--min-rate <num>` | Minimum packets sent per second. |
| `--max-rate <num>` | Maximum packets sent per second. |

Examples

```bash
nmap --min-rate 500 192.168.1.10

nmap --max-rate 1000 192.168.1.10
```

---

## Parallelism Control

| Option | Description |
|----------|-------------|
| `--min-parallelism <num>` | Minimum number of parallel probes. |
| `--max-parallelism <num>` | Maximum number of parallel probes. |

Example

```bash
nmap --min-parallelism 20 192.168.1.0/24
```

---

## Retry Control

| Option | Description |
|----------|-------------|
| `--max-retries <num>` | Maximum retransmission attempts. |

Example

```bash
nmap --max-retries 2 192.168.1.10
```

Lower values increase speed but may reduce accuracy.

---

## Host Timeout

| Option | Description |
|----------|-------------|
| `--host-timeout <time>` | Stop scanning a host after the specified time. |

Examples

```bash
nmap --host-timeout 30s 192.168.1.10

nmap --host-timeout 5m 192.168.1.0/24
```

---

## Scan Delay

| Option | Description |
|----------|-------------|
| `--scan-delay <time>` | Delay between probes sent to the same host. |
| `--max-scan-delay <time>` | Maximum allowed delay between probes. |

Example

```bash
nmap --scan-delay 100ms 192.168.1.10
```

---

## RTT Timeout Options

| Option | Description |
|----------|-------------|
| `--initial-rtt-timeout` | Initial response timeout. |
| `--min-rtt-timeout` | Minimum RTT timeout. |
| `--max-rtt-timeout` | Maximum RTT timeout. |

Example

```bash
nmap --initial-rtt-timeout 500ms
```

---

## Host Group Size

| Option | Description |
|----------|-------------|
| `--min-hostgroup <num>` | Minimum hosts scanned together. |
| `--max-hostgroup <num>` | Maximum hosts scanned together. |

Example

```bash
nmap --min-hostgroup 64
```

Useful for improving performance during large network scans.

---

## Performance Examples

### Fast Internal Network Scan

```bash
nmap -T4 --min-rate 1000 192.168.1.0/24
```

---

### Slow Stealth Scan

```bash
nmap -T1 --scan-delay 1s 192.168.1.10
```

---

### Reliable Internet Scan

```bash
nmap -T3 --max-retries 5
```

---

### Large Enterprise Network

```bash
nmap -T4 \
--min-rate 2000 \
--min-hostgroup 128 \
192.168.0.0/16
```

---

## Timing Comparison

| Template | Speed | Noise | Typical Usage |
|-----------|------:|------:|---------------|
| T0 | Very Low | Very Low | IDS Evasion |
| T1 | Low | Low | Stealth Reconnaissance |
| T2 | Medium-Low | Low | Shared Networks |
| T3 | Medium | Medium | General Purpose |
| T4 | High | High | Penetration Testing |
| T5 | Very High | Very High | Lab Environments |

---

## Best Practices

- Use **`-T3`** unless you have a reason to change it.
- Use **`-T4`** for most penetration testing engagements on reliable networks.
- Avoid **`-T5`** on unstable or high-latency networks.
- Increase packet rates only after verifying network capacity.
- Reduce retries only when occasional missed responses are acceptable.
- Use host timeouts to prevent a few slow hosts from delaying an entire scan.

---

## Notes

- Faster scans generate more network traffic.
- Aggressive timing increases the likelihood of detection by IDS/IPS devices.
- Network latency and packet loss significantly influence scan performance.
- Performance tuning should always balance speed, accuracy, and reliability.

---

# 10. Firewall & IDS Evasion

Nmap includes several options that modify how packets are generated and transmitted. These options are primarily intended for compatibility testing, network analysis, and authorized security assessments where different packet characteristics need to be evaluated.

> **Important:** These features should only be used during authorized security assessments or in lab environments.

---

## Common Evasion-Related Options

| Option | Description |
|---------|-------------|
| `-f` | Fragment IP packets into smaller pieces. |
| `--mtu <size>` | Specify a custom MTU for fragmented packets. |
| `-D <decoys>` | Include decoy source addresses in scan traffic. |
| `-S <IP>` | Specify a custom source IP address. |
| `--spoof-mac <MAC>` | Specify or randomize the source MAC address. |
| `--source-port <port>` | Use a specific source port. |
| `--data-length <num>` | Append random data to probe packets. |
| `--badsum` | Send packets with an invalid TCP/UDP checksum. |

---

## Packet Fragmentation

Fragmentation divides packets into smaller IP fragments.

**Related Options**

| Option | Description |
|---------|-------------|
| `-f` | Fragment packets. |
| `-ff` | Use smaller packet fragments. |
| `--mtu` | Define a custom fragment size. |

---

## Decoy Scanning

Decoy mode generates traffic that appears to originate from multiple source addresses.

**Option**

| Option | Description |
|---------|-------------|
| `-D` | Add decoy source addresses to the scan. |

---

## Source Address Selection

Nmap can transmit packets using a specified source address.

| Option | Description |
|---------|-------------|
| `-S` | Specify the source IP address. |

**Note**

The selected address should be valid for the network environment.

---

## MAC Address Selection

Control the source MAC address used on local networks.

| Option | Description |
|---------|-------------|
| `--spoof-mac <MAC>` | Use a specific MAC address. |
| `--spoof-mac 0` | Generate a random MAC address. |
| `--spoof-mac <Vendor>` | Generate a MAC address matching a vendor. |

---

## Source Port Selection

Specify the TCP or UDP source port used by Nmap.

| Option | Description |
|---------|-------------|
| `--source-port <port>` | Set the source port for outgoing probes. |

---

## Random Payload Data

Add random bytes to probe packets.

| Option | Description |
|---------|-------------|
| `--data-length <bytes>` | Append random payload data. |

---

## Invalid Checksums

Generate packets with intentionally invalid checksums.

| Option | Description |
|---------|-------------|
| `--badsum` | Send packets with invalid checksums. |

Useful for observing how network devices and operating systems validate traffic.

---

## Feature Comparison

| Feature | Primary Purpose |
|----------|-----------------|
| Fragmentation | Packet fragmentation testing |
| Custom MTU | Fragment size control |
| Decoys | Traffic source simulation |
| Source IP | Source address testing |
| MAC Selection | Layer 2 address testing |
| Source Port | Source port selection |
| Data Length | Packet size variation |
| Bad Checksum | Protocol validation testing |

---

## Compatibility Notes

- Some options require root or Administrator privileges.
- Certain features only apply on local Ethernet networks.
- Intermediate devices such as routers and firewalls may modify or discard specially crafted packets.
- Results can vary depending on operating systems, network infrastructure, and security devices.

---

## Best Practices

- Use these options only in environments where you have explicit authorization.
- Test one option at a time to understand its effect on scan results.
- Compare results with standard scans when troubleshooting network behavior.
- Record the options used in assessment reports to ensure reproducibility.

---

## Notes

- Packet manipulation options do not guarantee different scan results.
- Security appliances may inspect, normalize, or reject modified packets.
- Network conditions and device configurations influence how probes are handled.
- Always verify findings using multiple assessment techniques when appropriate.

---

# 11. DNS Resolution

DNS Resolution determines how Nmap translates IP addresses into hostnames and resolves hostnames into IP addresses. Adjusting DNS behavior can improve scan speed, reduce unnecessary queries, or use specific DNS servers during an assessment.

---

## Common DNS Options

| Option | Description |
|---------|-------------|
| `-n` | Never perform DNS resolution. |
| `-R` | Always resolve DNS names. |
| `--system-dns` | Use the operating system's DNS resolver. |
| `--dns-servers <server[,server]>` | Specify one or more DNS servers. |
| `--resolve-all` | Resolve all IP addresses associated with a hostname. |

---

## Disable DNS Resolution

```bash
nmap -n 192.168.1.0/24
```

**Advantages**

- Faster scanning
- Fewer DNS requests
- Reduces unnecessary network traffic

Recommended for:

- Internal penetration tests
- Large network scans
- Performance-focused reconnaissance

---

## Force DNS Resolution

```bash
nmap -R 192.168.1.10
```

Always attempts reverse DNS lookups, even when scanning IP addresses.

Useful when:

- Hostnames are required in reports
- Asset identification is important

---

## Use System DNS Resolver

```bash
nmap --system-dns scanme.nmap.org
```

Uses the operating system's configured DNS resolver instead of Nmap's default resolver.

---

## Specify DNS Servers

```bash
nmap --dns-servers 8.8.8.8 scanme.nmap.org
```

Multiple DNS servers

```bash
nmap --dns-servers 8.8.8.8,1.1.1.1 example.com
```

Allows you to query specific DNS servers during hostname resolution.

---

## Resolve All Addresses

```bash
nmap --resolve-all example.com
```

Scans every IP address returned by DNS instead of selecting only one.

Useful for:

- Load-balanced services
- Multi-homed servers
- CDN environments

---

## DNS Resolution Examples

### Fast Network Scan

```bash
nmap -n 192.168.1.0/24
```

---

### Scan with Hostname Resolution

```bash
nmap -R 192.168.1.0/24
```

---

### Custom DNS Server

```bash
nmap --dns-servers 1.1.1.1 target.com
```

---

### Resolve Every Address

```bash
nmap --resolve-all target.com
```

---

## DNS Option Comparison

| Option | Speed | Hostnames | Typical Usage |
|---------|------:|----------:|---------------|
| `-n` | Very High | No | Large scans |
| `-R` | Lower | Yes | Reporting |
| `--system-dns` | Medium | Yes | Use OS configuration |
| `--dns-servers` | Medium | Yes | Custom DNS infrastructure |
| `--resolve-all` | Lower | Yes | Multi-IP targets |

---

## Best Practices

- Use **`-n`** during large scans to reduce scan time.
- Enable hostname resolution only when it adds value to the assessment.
- Use trusted DNS servers when consistency is important.
- Include hostnames in reports when they aid asset identification.
- Be aware that DNS lookups can increase total scan duration.

---

## Notes

- DNS resolution is independent of port scanning.
- Reverse DNS records may be missing or inaccurate.
- Large-scale hostname resolution can noticeably increase scan time.
- Results depend on the DNS infrastructure and record availability.

---

# 12. Output Formats

Nmap provides multiple output formats for reporting, automation, integration, and later analysis. Scan results can be saved in human-readable text, XML, grepable format, or multiple formats simultaneously.

---

## Common Output Options

| Option | Description |
|---------|-------------|
| `-oN <file>` | Save output in normal (human-readable) format. |
| `-oX <file>` | Save output as XML. |
| `-oG <file>` | Save output in grepable format. *(Deprecated)* |
| `-oS <file>` | Save output in Script Kiddie format. |
| `-oA <name>` | Save output in Normal, XML, and Grepable formats simultaneously. |

---

## Normal Output

```bash
nmap -oN scan.txt 192.168.1.10
```

Produces a readable report suitable for documentation.

Example

```text
Nmap scan report for 192.168.1.10

PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
```

---

## XML Output

```bash
nmap -oX scan.xml 192.168.1.10
```

XML output is commonly used by:

- Security tools
- Automation frameworks
- CI/CD pipelines
- Report generators
- Vulnerability management platforms

---

## Grepable Output

```bash
nmap -oG scan.gnmap 192.168.1.10
```

Designed for quick parsing using command-line tools.

Example

```text
Host: 192.168.1.10
Ports: 22/open/tcp//ssh///
```

> **Note:** Grepable output is deprecated. XML output is recommended for new automation workflows.

---

## Script Kiddie Output

```bash
nmap -oS funny.txt 192.168.1.10
```

A novelty format that changes the capitalization style of the output.

Not recommended for professional reporting.

---

## All Output Formats

```bash
nmap -oA scan_results 192.168.1.10
```

Creates three files automatically:

```text
scan_results.nmap
scan_results.xml
scan_results.gnmap
```

This is one of the most commonly used options during professional assessments.

---

## Verbose Output

| Option | Description |
|---------|-------------|
| `-v` | Increase verbosity. |
| `-vv` | Higher verbosity level. |

Example

```bash
nmap -v 192.168.1.10
```

Useful for monitoring scan progress.

---

## Debug Output

| Option | Description |
|---------|-------------|
| `-d` | Enable debugging output. |
| `-dd` | More detailed debugging. |
| `-d9` | Maximum debugging level. |

Example

```bash
nmap -d 192.168.1.10
```

Debug output is primarily intended for troubleshooting.

---

## Resume an Interrupted Scan

```bash
nmap --resume scan_results.nmap
```

Continues a previously interrupted scan using the normal output file.

---

## Output Comparison

| Format | Human Readable | Machine Readable | Typical Usage |
|---------|:--------------:|:----------------:|---------------|
| Normal (`-oN`) | ✅ | ❌ | Reports |
| XML (`-oX`) | ⚠️ | ✅ | Automation |
| Grepable (`-oG`) | ⚠️ | ✅ | Legacy scripts |
| Script Kiddie (`-oS`) | ⚠️ | ❌ | Demonstration |
| All (`-oA`) | ✅ | ✅ | Professional assessments |

---

## Example Commands

### Save Normal Output

```bash
nmap -oN report.txt target
```

---

### Save XML Output

```bash
nmap -oX report.xml target
```

---

### Save All Formats

```bash
nmap -oA full_scan target
```

---

### Verbose Scan

```bash
nmap -v -oA scan target
```

---

### Debugging Scan

```bash
nmap -d -oN debug.txt target
```

---

## Best Practices

- Use **`-oA`** during penetration tests to preserve results in multiple formats.
- Prefer **XML (`-oX`)** for automation and tool integration.
- Store scan reports using descriptive filenames and timestamps.
- Enable verbose mode for long-running scans.
- Use debug mode only when troubleshooting scan behavior.

---

## Notes

- Existing output files may be overwritten unless renamed.
- XML output is widely supported by third-party security tools.
- Grepable output remains available for compatibility but is no longer recommended for new workflows.
- Saving scan results ensures findings can be reviewed without repeating the scan.

---

# 13. Port States

Nmap classifies each scanned port into one of several states based on the responses received during the scan. A port state reflects what Nmap can determine about the port at the time of the scan—not necessarily the port's permanent condition.

---

## The Six Port States

| State | Description |
|--------|-------------|
| `open` | An application is actively accepting connections on this port. |
| `closed` | The port is reachable but no service is listening. |
| `filtered` | Nmap cannot determine whether the port is open because packet filtering prevents probes from reaching the target or responses from returning. |
| `unfiltered` | The port is reachable, but Nmap cannot determine whether it is open or closed. Typically seen during ACK scans. |
| `open\|filtered` | Nmap cannot distinguish between an open and a filtered port. |
| `closed\|filtered` | Nmap cannot determine whether the port is closed or filtered. Rarely encountered. |

---

# Open

```text
22/tcp open ssh
80/tcp open http
443/tcp open https
```

### Meaning

- A service is listening.
- The port accepts connections.
- Enumeration can continue.

Common Next Steps

- Version Detection (`-sV`)
- NSE Scripts (`-sC`)
- Vulnerability Assessment

---

# Closed

```text
23/tcp closed telnet
```

### Meaning

- Host is reachable.
- No service is listening.
- The operating system responded.

Important

A closed port proves the target is alive.

---

# Filtered

```text
445/tcp filtered microsoft-ds
```

### Meaning

Nmap received no useful response because:

- Firewall blocked packets
- ACL blocked traffic
- IDS/IPS interfered
- Packet filtering occurred

Possible Causes

- Corporate firewall
- Cloud Security Group
- Router ACL
- Host Firewall

---

# Unfiltered

```text
80/tcp unfiltered http
```

### Meaning

- Port is reachable.
- ACK probes reached the target.
- Nmap cannot determine whether the port is open.

Usually appears with:

```bash
-sA
```

---

# Open|Filtered

```text
161/udp open|filtered snmp
```

### Meaning

Nmap cannot distinguish between:

- Open
- Filtered

Common during:

- UDP Scan
- FIN Scan
- NULL Scan
- Xmas Scan

Reason

Some services simply do not respond when open.

---

# Closed|Filtered

```text
123/udp closed|filtered ntp
```

### Meaning

Nmap cannot determine whether:

- the port is closed
- or filtering prevented an accurate result

This state is uncommon.

---

# State Comparison

| State | Host Reachable | Service Running | Firewall Possible |
|---------|:-------------:|:---------------:|:-----------------:|
| Open | ✅ | ✅ | Possible |
| Closed | ✅ | ❌ | Usually No |
| Filtered | Unknown | Unknown | ✅ |
| Unfiltered | ✅ | Unknown | No Filtering Detected |
| Open\|Filtered | Unknown | Unknown | Possible |
| Closed\|Filtered | Unknown | Unknown | Possible |

---

# Decision Flow

```text
Probe Sent
      │
      ▼
Response Received?
      │
 ┌────┴────┐
 │         │
Yes        No
 │         │
 ▼         ▼
Open?   Filtered?
 │         │
 ▼         ▼
Open   Filtered
 │
 ▼
Closed
```

---

# Typical Scan Results

## SYN Scan

| Result | Meaning |
|---------|---------|
| SYN/ACK | Open |
| RST | Closed |
| No Response | Filtered |

---

## UDP Scan

| Result | Meaning |
|---------|---------|
| UDP Response | Open |
| ICMP Port Unreachable | Closed |
| No Response | Open or Filtered |

---

## ACK Scan

| Result | Meaning |
|---------|---------|
| RST | Unfiltered |
| No Response | Filtered |

---

# Practical Interpretation

| State | Recommended Action |
|---------|-------------------|
| Open | Enumerate the service |
| Closed | Usually no further action |
| Filtered | Investigate filtering devices |
| Unfiltered | Perform SYN or Connect Scan |
| Open\|Filtered | Verify with additional scan types |
| Closed\|Filtered | Use complementary techniques |

---

# Best Practices

- Never assume **Filtered** means the host is offline.
- Verify **Open|Filtered** ports using additional scan techniques.
- Use multiple scan types when results are ambiguous.
- Combine port state information with service detection and NSE scripts.
- Record port states in assessment reports for future comparison.

---

# Notes

- Port states describe Nmap's observations at the time of scanning.
- Firewalls, IDS/IPS devices, and network latency can affect state detection.
- Different scan types may report different states for the same port.
- A single scan does not always provide definitive results.

---

# 14. TCP Flags

TCP Flags are control bits in the TCP header that manage the state and behavior of TCP connections. Nmap relies on different flag combinations to perform various scan techniques and analyze how target systems respond.

---

## TCP Header Flags

| Flag | Full Name | Purpose |
|------|-----------|---------|
| `SYN` | Synchronize | Initiates a TCP connection. |
| `ACK` | Acknowledgment | Acknowledges received data. |
| `FIN` | Finish | Gracefully closes a TCP connection. |
| `RST` | Reset | Immediately terminates a TCP connection. |
| `PSH` | Push | Delivers buffered data immediately to the application. |
| `URG` | Urgent | Indicates urgent data is present. |
| `ECE` | ECN Echo | Used for Explicit Congestion Notification. |
| `CWR` | Congestion Window Reduced | Indicates congestion handling. |

---

# SYN Flag

```
Client                      Server

SYN ------------------------>

```

Purpose

- Starts a TCP connection.
- Used during the TCP Three-Way Handshake.
- Primary flag used by SYN Scans (`-sS`).

---

# ACK Flag

```
Client                      Server

<------------------------ ACK
```

Purpose

- Confirms receipt of data.
- Indicates an established connection.
- Used by ACK Scan (`-sA`).

---

# FIN Flag

```
Client                      Server

FIN ------------------------>
```

Purpose

- Gracefully closes a TCP connection.
- Used in FIN Scan (`-sF`).

---

# RST Flag

```
Client                      Server

RST ------------------------>
```

Purpose

- Immediately terminates a TCP connection.
- Indicates closed ports during many scan types.

---

# PSH Flag

Purpose

- Pushes buffered data immediately to the receiving application.
- Common during interactive sessions.

Example

```
PSH + ACK
```

---

# URG Flag

Purpose

- Marks urgent data.
- Rarely used by modern applications.

---

# ECE Flag

Purpose

- Indicates network congestion.
- Part of Explicit Congestion Notification (ECN).

---

# CWR Flag

Purpose

- Acknowledges congestion handling.
- Works together with ECE.

---

# Flag Combinations Used by Nmap

| Scan | Flags Sent |
|-------|------------|
| SYN Scan (`-sS`) | SYN |
| Connect Scan (`-sT`) | Complete Handshake |
| FIN Scan (`-sF`) | FIN |
| NULL Scan (`-sN`) | No Flags |
| Xmas Scan (`-sX`) | FIN + PSH + URG |
| ACK Scan (`-sA`) | ACK |
| Window Scan (`-sW`) | ACK |

---

# TCP Flag Visualization

```
TCP HEADER

+----------------------------------------------------+
| URG | ACK | PSH | RST | SYN | FIN | ECE | CWR |
+----------------------------------------------------+
```

---

# TCP Three-Way Handshake

```
Client                              Server

SYN ------------------------------->

          <---------------------- SYN/ACK

ACK ------------------------------->
```

Connection Established

---

# Connection Termination

```
Client                              Server

FIN ------------------------------->

          <---------------------- ACK

          <---------------------- FIN

ACK ------------------------------->
```

Connection Closed

---

# Scan Response Examples

## Open Port

```
Scanner               Target

SYN ------------------>

       <----------- SYN/ACK

RST ------------------>
```

Nmap sends a RST instead of completing the connection.

---

## Closed Port

```
Scanner               Target

SYN ------------------>

       <------------- RST
```

The target immediately rejects the connection.

---

## Filtered Port

```
Scanner               Target

SYN ------------------>

       (No Response)
```

Usually indicates packet filtering.

---

# Flag Summary

| Flag | Opens Connection | Closes Connection | Used by Nmap |
|------|:----------------:|:-----------------:|:------------:|
| SYN | ✅ | ❌ | ✅ |
| ACK | ❌ | ❌ | ✅ |
| FIN | ❌ | ✅ | ✅ |
| RST | ❌ | Immediate | ✅ |
| PSH | ❌ | ❌ | Partial |
| URG | ❌ | ❌ | Partial |
| ECE | ❌ | ❌ | Rare |
| CWR | ❌ | ❌ | Rare |

---

# Best Practices

- Understand the purpose of each TCP flag before interpreting scan results.
- Relate TCP flag behavior to the scan type being performed.
- Remember that operating systems may implement TCP differently.
- Use packet captures (e.g., Wireshark) to observe TCP flags during scans.

---

# Notes

- TCP flags control connection establishment, data transfer, and termination.
- Many Nmap scan types differ only in the TCP flags they transmit.
- Firewalls and intrusion prevention systems may inspect or modify TCP flag behavior.
- Understanding TCP flags is essential for interpreting advanced Nmap scan results.

---

# 15. TCP Three-Way Handshake

The TCP Three-Way Handshake is the process used to establish a reliable TCP connection between a client and a server. Nmap relies on this mechanism to determine whether ports are open, closed, or filtered during many scan types.

---

## Overview

A TCP connection is established in three steps:

1. Client sends a **SYN** packet.
2. Server replies with **SYN/ACK**.
3. Client responds with **ACK**.

Once these three packets are exchanged, the TCP connection is established.

---

# Step 1 — SYN

```
Client                              Server

SYN ------------------------------->
```

### Purpose

- Requests a new TCP connection.
- Synchronizes sequence numbers.
- Begins the handshake process.

---

# Step 2 — SYN/ACK

```
Client                              Server

          <---------------------- SYN/ACK
```

### Purpose

- Confirms receipt of the SYN packet.
- Acknowledges the client's request.
- Sends the server's own SYN request.

---

# Step 3 — ACK

```
Client                              Server

ACK ------------------------------->
```

### Purpose

- Acknowledges the server's SYN.
- Completes the handshake.
- The connection is now established.

---

# Complete Handshake

```text
Client                              Server

SYN ------------------------------->

          <---------------------- SYN/ACK

ACK ------------------------------->
```

```
Connection Established
```

---

# TCP Data Transfer

Once the handshake completes:

```text
Client  <=========================>  Server

        Reliable TCP Communication
```

Both systems can now exchange application data.

---

# Connection Termination

A normal TCP connection is closed using a four-step exchange.

```text
Client                              Server

FIN ------------------------------->

          <---------------------- ACK

          <---------------------- FIN

ACK ------------------------------->
```

```
Connection Closed
```

---

# How SYN Scan Works (`-sS`)

A SYN Scan intentionally **does not complete** the TCP handshake.

```
Scanner                             Target

SYN ------------------------------->

          <---------------------- SYN/ACK

RST ------------------------------->
```

### Result

- Connection is never fully established.
- Faster than a full TCP Connect Scan.
- Generates less application-layer activity.
- Commonly referred to as a **Half-Open Scan**.

---

# How Connect Scan Works (`-sT`)

A TCP Connect Scan completes the entire handshake using the operating system's networking stack.

```text
Scanner                             Target

SYN ------------------------------->

          <---------------------- SYN/ACK

ACK ------------------------------->

Connection Established
```

The connection is then closed normally.

---

# Closed Port Example

```text
Scanner                             Target

SYN ------------------------------->

          <---------------------- RST
```

### Interpretation

The target is reachable, but no service is listening on the port.

---

# Filtered Port Example

```text
Scanner                             Target

SYN ------------------------------->

        (No Response)
```

or

```text
Scanner                             Target

SYN ------------------------------->

          <------ ICMP Unreachable
```

### Interpretation

A firewall or filtering device prevents the connection from being evaluated.

---

# Handshake Comparison

| Step | SYN Scan (`-sS`) | Connect Scan (`-sT`) |
|------|:----------------:|:--------------------:|
| SYN | ✅ | ✅ |
| SYN/ACK | ✅ | ✅ |
| ACK | ❌ | ✅ |
| Connection Established | ❌ | ✅ |
| RST Sent | ✅ | Usually after connection closes |

---

# Response Interpretation

| Target Response | Meaning |
|-----------------|---------|
| SYN/ACK | Port is open |
| RST | Port is closed |
| No Response | Port may be filtered |
| ICMP Unreachable | Filtering detected |

---

# Relationship to Scan Types

| Scan Type | Uses TCP Handshake |
|------------|:------------------:|
| `-sS` SYN Scan | Partial |
| `-sT` Connect Scan | Complete |
| `-sA` ACK Scan | No |
| `-sF` FIN Scan | No |
| `-sN` NULL Scan | No |
| `-sX` Xmas Scan | No |
| `-sU` UDP Scan | Not Applicable |

---

# Why SYN Scan Is Faster

A SYN Scan avoids completing the TCP connection, which provides several advantages:

- Fewer packets exchanged.
- Lower resource usage on the target.
- Reduced scan duration.
- Less application-level logging on many services.

---

# Best Practices

- Use **SYN Scan (`-sS`)** whenever raw packet privileges are available.
- Use **Connect Scan (`-sT`)** when administrative privileges are unavailable.
- Understand the handshake before interpreting Nmap scan results.
- Combine packet captures with Nmap scans to observe handshake behavior in real time.

---

# Notes

- Every TCP connection begins with a Three-Way Handshake.
- SYN Scans intentionally stop before the connection is established.
- TCP Connect Scans use the operating system's networking stack.
- Understanding the handshake is essential for interpreting SYN, ACK, FIN, NULL, and Xmas scans.

---

# 16. UDP Communication

Unlike TCP, UDP (User Datagram Protocol) is a connectionless transport protocol. It does not establish a session before transmitting data, making it faster but less reliable. Because there is no handshake, UDP scanning behaves differently from TCP scanning and often requires more time to produce reliable results.

---

# TCP vs UDP

| Feature | TCP | UDP |
|----------|-----|-----|
| Connection | Connection-Oriented | Connectionless |
| Handshake | Yes | No |
| Reliability | High | Low |
| Error Recovery | Yes | No |
| Packet Ordering | Guaranteed | Not Guaranteed |
| Speed | Slower | Faster |
| Typical Usage | Web, SSH, FTP | DNS, SNMP, VoIP, Streaming |

---

# UDP Communication

Unlike TCP:

```
Client ------------------------> Server
          UDP Packet
```

No connection is established.

No acknowledgement is required.

---

# UDP Scan

```bash
nmap -sU 192.168.1.10
```

Scans UDP ports instead of TCP ports.

---

# Common UDP Services

| Port | Service |
|------|---------|
| 53 | DNS |
| 67 | DHCP Server |
| 68 | DHCP Client |
| 69 | TFTP |
| 123 | NTP |
| 137 | NetBIOS Name Service |
| 138 | NetBIOS Datagram |
| 161 | SNMP |
| 162 | SNMP Trap |
| 500 | ISAKMP / IKE |
| 514 | Syslog |
| 520 | RIP |

---

# UDP Scan Workflow

```
Scanner                     Target

UDP Packet ----------------------->

           ?
```

Possible responses determine the port state.

---

# Open UDP Port

```
Scanner                     Target

UDP Packet ----------------------->

          <---------------- UDP Response
```

Interpretation

- Service is running.
- Port is open.

---

# Closed UDP Port

```
Scanner                     Target

UDP Packet ----------------------->

          <------ ICMP Port Unreachable
```

Interpretation

- Host is reachable.
- No service is listening.

---

# Open|Filtered Port

```
Scanner                     Target

UDP Packet ----------------------->

          (No Response)
```

Interpretation

Nmap cannot determine whether:

- the service is open and silently ignored the probe, or
- a firewall filtered the packet.

This is the most common UDP scan result.

---

# Why UDP Scans Are Slow

UDP services often do **not** respond unless they receive a valid application-specific request.

As a result:

- Multiple retries may be required.
- Timeouts are generally longer.
- Packet loss is harder to distinguish from filtering.

---

# Typical UDP States

| Response | Port State |
|-----------|------------|
| UDP Reply | Open |
| ICMP Port Unreachable | Closed |
| No Response | Open\|Filtered |
| ICMP Filtering Message | Filtered |

---

# Example Scan

```bash
nmap -sU 192.168.1.10
```

Example Output

```text
PORT      STATE         SERVICE

53/udp    open          domain
67/udp    closed        dhcp
161/udp   open|filtered snmp
123/udp   open          ntp
```

---

# TCP vs UDP Scanning

| Feature | TCP Scan | UDP Scan |
|----------|----------|----------|
| Speed | Fast | Slow |
| Reliability | High | Moderate |
| Handshake | Yes | No |
| Open Detection | Easy | More Difficult |
| Firewall Effects | Moderate | Significant |

---

# Combining TCP and UDP

A comprehensive assessment often scans both protocols.

Example

```bash
nmap -sS -sU target
```

Specify ports

```bash
nmap -sS -sU -p T:22,80,443,U:53,161 target
```

---

# Best Practices

- Scan only required UDP ports when possible.
- Expect longer scan durations compared to TCP.
- Verify important UDP findings with additional enumeration.
- Combine UDP scans with service version detection when appropriate.
- Save scan results for later comparison.

---

# Notes

- UDP is connectionless and does not use a handshake.
- Many UDP services intentionally remain silent unless they receive valid protocol requests.
- Firewalls frequently affect UDP scan accuracy.
- The `open|filtered` state is common and should be interpreted carefully.

---

# 17. ICMP Reference

The Internet Control Message Protocol (ICMP) is used for network diagnostics, error reporting, and operational communication between network devices. Nmap uses several ICMP message types during host discovery and UDP scanning.

---

# What is ICMP?

Unlike TCP and UDP, ICMP does **not** transport application data.

It is primarily used for:

- Network diagnostics
- Error reporting
- Reachability testing
- Route information

Common tools using ICMP include:

- Ping
- Traceroute
- Nmap Host Discovery

---

# Common ICMP Message Types

| Type | Name | Purpose |
|------:|------|---------|
| 0 | Echo Reply | Response to Ping |
| 3 | Destination Unreachable | Target or service unavailable |
| 5 | Redirect | Better route available |
| 8 | Echo Request | Ping request |
| 11 | Time Exceeded | TTL expired |
| 12 | Parameter Problem | Invalid packet header |
| 13 | Timestamp Request | Time synchronization request |
| 14 | Timestamp Reply | Response to timestamp request |

---

# Echo Request (Type 8)

```
Scanner ---------------------->

        ICMP Echo Request
```

Purpose

- Tests whether a host is reachable.
- Commonly known as a Ping request.

Nmap Option

```bash
nmap -PE target
```

---

# Echo Reply (Type 0)

```
Scanner <----------------------

        ICMP Echo Reply
```

Interpretation

- Host is online.
- Network path is functioning.
- The target responded successfully.

---

# Destination Unreachable (Type 3)

One of the most important ICMP messages for Nmap.

Common Codes

| Code | Meaning |
|------|---------|
| 0 | Network Unreachable |
| 1 | Host Unreachable |
| 2 | Protocol Unreachable |
| 3 | Port Unreachable |
| 9 | Network Administratively Prohibited |
| 10 | Host Administratively Prohibited |
| 13 | Communication Administratively Prohibited |

Example

```
Scanner ---------------------->

UDP Packet

        <------------ ICMP Port Unreachable
```

Interpretation

UDP port is **Closed**.

---

# Redirect (Type 5)

```
Router

Redirect Message
```

Purpose

Informs a host that a better gateway exists.

Rarely used during Nmap scans.

---

# Time Exceeded (Type 11)

```
Router

TTL Expired
```

Purpose

Occurs when the packet's TTL reaches zero.

Used by:

- Traceroute
- Path analysis

---

# Timestamp Request (Type 13)

```
Scanner ---------------------->

Timestamp Request
```

Nmap Option

```bash
nmap -PP target
```

Some systems respond even when Echo Requests are blocked.

---

# Timestamp Reply (Type 14)

```
Scanner <----------------------

Timestamp Reply
```

Confirms the host is reachable.

---

# ICMP in Host Discovery

| Option | ICMP Probe |
|----------|------------|
| `-PE` | Echo Request |
| `-PP` | Timestamp Request |
| `-PM` | Address Mask Request |

Example

```bash
nmap -sn -PE 192.168.1.0/24
```

---

# ICMP in UDP Scanning

UDP scans rely heavily on ICMP responses.

```
UDP Probe
      │
      ▼

ICMP Port Unreachable
      │
      ▼

Closed Port
```

No ICMP response usually results in:

```
Open|Filtered
```

---

# ICMP Response Interpretation

| ICMP Message | Meaning |
|--------------|---------|
| Echo Reply | Host is online |
| Port Unreachable | UDP port closed |
| Host Unreachable | Target unreachable |
| Network Unreachable | Network unavailable |
| TTL Exceeded | Hop limit reached |
| No Response | Possible filtering |

---

# ICMP Workflow

```
Scanner
    │
    ▼
ICMP Echo Request
    │
    ▼
Target Host
    │
    ├──────── Echo Reply
    │
    ├──────── Destination Unreachable
    │
    ├──────── Time Exceeded
    │
    └──────── No Response
```

---

# Common ICMP Types Used by Nmap

| Type | Used By |
|------:|---------|
| Echo Request | Host Discovery |
| Echo Reply | Host Discovery |
| Timestamp | Host Discovery |
| Destination Unreachable | UDP Scan |
| Time Exceeded | Traceroute |

---

# Best Practices

- Use ICMP discovery on networks where Echo Requests are permitted.
- Do not assume a host is offline if it does not reply to ICMP Echo Requests.
- Combine ICMP probes with TCP or ARP discovery for more reliable host detection.
- Remember that many firewalls block ICMP traffic by default.
- Interpret ICMP responses together with other scan results.

---

# Notes

- ICMP is a network-layer protocol and does not use ports.
- Many network devices prioritize or rate-limit ICMP traffic.
- Different ICMP messages provide different diagnostic information.
- Nmap combines ICMP with other probe types to improve host discovery accuracy.

---

# 18. Common Ports Reference

Network services communicate through port numbers. Knowing the most common ports and their associated protocols is essential for interpreting Nmap scan results, identifying exposed services, and planning further enumeration.

---

# Well-Known Port Ranges

| Range | Name | Description |
|--------|------|-------------|
| 0–1023 | Well-Known Ports | Standard Internet services |
| 1024–49151 | Registered Ports | Vendor and application services |
| 49152–65535 | Dynamic / Private Ports | Ephemeral or temporary ports |

---

# Common TCP Ports

| Port | Service | Description |
|------:|---------|-------------|
| 20 | FTP Data | FTP data transfer |
| 21 | FTP | File Transfer Protocol |
| 22 | SSH | Secure Shell |
| 23 | Telnet | Remote terminal |
| 25 | SMTP | Mail transfer |
| 49 | TACACS+ | Network device authentication |
| 53 | DNS | Domain Name System |
| 80 | HTTP | Web server |
| 88 | Kerberos | Authentication |
| 110 | POP3 | Email retrieval |
| 111 | RPCbind | Remote Procedure Call |
| 119 | NNTP | Network News Transfer |
| 135 | MS RPC | Windows RPC Endpoint Mapper |
| 139 | NetBIOS Session | Windows file sharing |
| 143 | IMAP | Email retrieval |
| 179 | BGP | Border Gateway Protocol |
| 389 | LDAP | Directory services |
| 427 | SLP | Service Location Protocol |
| 443 | HTTPS | Secure web services |
| 445 | SMB | Windows file sharing |
| 465 | SMTPS | Secure SMTP |
| 514 | Syslog | System logging (TCP deployments) |
| 515 | LPD | Line Printer Daemon |
| 548 | AFP | Apple Filing Protocol |
| 554 | RTSP | Streaming media |
| 587 | SMTP Submission | Authenticated email submission |
| 631 | IPP | Internet Printing Protocol |
| 636 | LDAPS | Secure LDAP |
| 873 | Rsync | File synchronization |
| 989 | FTPS Data | Secure FTP data |
| 990 | FTPS Control | Secure FTP control |
| 993 | IMAPS | Secure IMAP |
| 995 | POP3S | Secure POP3 |
| 1025 | Microsoft RPC | Dynamic RPC |
| 1080 | SOCKS | Proxy service |
| 1433 | Microsoft SQL Server | Database server |
| 1521 | Oracle Database | Oracle listener |
| 1723 | PPTP | VPN |
| 1883 | MQTT | IoT messaging |
| 2049 | NFS | Network File System |
| 2375 | Docker API | Unencrypted Docker daemon |
| 2376 | Docker API TLS | Encrypted Docker daemon |
| 3128 | Squid Proxy | HTTP proxy |
| 3306 | MySQL | Database |
| 3389 | RDP | Remote Desktop |
| 3690 | Subversion | SVN |
| 4369 | Erlang Port Mapper | Erlang distribution |
| 4444 | Metasploit Handler | Common testing port |
| 5000 | UPnP / Web Apps | Application services |
| 5060 | SIP | Voice over IP |
| 5061 | SIP TLS | Secure VoIP |
| 5432 | PostgreSQL | Database |
| 5601 | Kibana | Dashboard |
| 5672 | RabbitMQ | Message broker |
| 5900 | VNC | Remote desktop |
| 5985 | WinRM HTTP | Windows Remote Management |
| 5986 | WinRM HTTPS | Secure WinRM |
| 6379 | Redis | In-memory database |
| 6443 | Kubernetes API | Cluster management |
| 6667 | IRC | Internet Relay Chat |
| 7001 | WebLogic | Oracle middleware |
| 8000 | HTTP Alternate | Web applications |
| 8080 | HTTP Proxy | Alternate HTTP |
| 8081 | HTTP Alternate | Web applications |
| 8443 | HTTPS Alternate | Secure web applications |
| 8888 | HTTP Alternate | Development services |
| 9000 | SonarQube / PHP-FPM | Application services |
| 9090 | Prometheus | Monitoring |
| 9200 | Elasticsearch | Search engine |
| 9300 | Elasticsearch Cluster | Node communication |
| 9418 | Git | Git protocol |
| 10000 | Webmin | System administration |
| 11211 | Memcached | Caching |
| 27017 | MongoDB | NoSQL database |

---

# Common UDP Ports

| Port | Service | Description |
|------:|---------|-------------|
| 53 | DNS | Domain Name System |
| 67 | DHCP Server | Dynamic Host Configuration |
| 68 | DHCP Client | DHCP client |
| 69 | TFTP | Trivial File Transfer |
| 123 | NTP | Network Time Protocol |
| 137 | NetBIOS Name | Windows networking |
| 138 | NetBIOS Datagram | Windows networking |
| 161 | SNMP | Network management |
| 162 | SNMP Trap | SNMP notifications |
| 500 | ISAKMP/IKE | IPsec VPN |
| 514 | Syslog | Logging |
| 520 | RIP | Routing Information Protocol |
| 1701 | L2TP | VPN |
| 1812 | RADIUS Authentication | AAA |
| 1813 | RADIUS Accounting | AAA |
| 1900 | SSDP | UPnP discovery |
| 4500 | IPsec NAT-T | VPN |
| 5353 | mDNS | Multicast DNS |
| 5355 | LLMNR | Local name resolution |

---

# Frequently Encountered During Pentests

| Port | Service | Common Enumeration |
|------:|---------|-------------------|
| 21 | FTP | Anonymous login, banners |
| 22 | SSH | Host keys, authentication |
| 80 | HTTP | Directories, headers, technologies |
| 443 | HTTPS | TLS configuration, certificates |
| 445 | SMB | Shares, users, OS detection |
| 3306 | MySQL | Version, authentication |
| 3389 | RDP | Encryption, NLA |
| 5432 | PostgreSQL | Version, authentication |
| 5900 | VNC | Authentication |
| 6379 | Redis | Anonymous access |
| 9200 | Elasticsearch | Cluster information |
| 27017 | MongoDB | Authentication status |

---

# Port Number Mnemonics

| Port | Easy Reminder |
|------:|---------------|
| 22 | SSH |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 143 | IMAP |
| 443 | HTTPS |
| 445 | SMB |
| 3306 | MySQL |
| 3389 | RDP |

---

# Best Practices

- Memorize the most frequently encountered service ports.
- Always verify the actual service using **Version Detection (`-sV`)**, as services can run on non-standard ports.
- Do not assume a service solely from its port number.
- Use port information together with service banners and NSE scripts for accurate identification.

---

# Notes

- Services can be configured to use non-default ports.
- Port numbers provide clues but do not definitively identify the running service.
- Version detection and banner analysis are recommended for confirmation.
- Modern environments frequently host multiple services on alternate ports.

---

# 19. IPv4 & CIDR Quick Reference

IPv4 addresses identify devices on a network using a 32-bit address space. CIDR (Classless Inter-Domain Routing) notation specifies how many bits represent the network portion of an address, allowing flexible subnet definitions.

---

# IPv4 Address Structure

An IPv4 address consists of four octets.

Example

```text
192.168.1.10
```

Binary Representation

```text
11000000.10101000.00000001.00001010
```

Each octet contains **8 bits**.

```
8 + 8 + 8 + 8 = 32 Bits
```

---

# IPv4 Address Classes (Historical)

| Class | First Octet | Default Mask | CIDR |
|--------|------------:|-------------|------|
| A | 1–126 | 255.0.0.0 | /8 |
| B | 128–191 | 255.255.0.0 | /16 |
| C | 192–223 | 255.255.255.0 | /24 |
| D | 224–239 | Multicast | — |
| E | 240–255 | Reserved | — |

---

# Private IPv4 Ranges

| Network | CIDR |
|----------|------|
| 10.0.0.0 | /8 |
| 172.16.0.0 | /12 |
| 192.168.0.0 | /16 |

These ranges are not routable on the public Internet.

---

# Loopback

| Address | Purpose |
|----------|---------|
| 127.0.0.1 | Localhost |
| 127.0.0.0/8 | Loopback Network |

---

# APIPA

| Network | Description |
|----------|-------------|
| 169.254.0.0/16 | Automatic Private IP Addressing |

Assigned automatically when DHCP is unavailable.

---

# CIDR Reference

| CIDR | Subnet Mask | Total Addresses | Usable Hosts |
|------|-------------|----------------:|-------------:|
| /8 | 255.0.0.0 | 16,777,216 | 16,777,214 |
| /12 | 255.240.0.0 | 1,048,576 | 1,048,574 |
| /16 | 255.255.0.0 | 65,536 | 65,534 |
| /20 | 255.255.240.0 | 4,096 | 4,094 |
| /22 | 255.255.252.0 | 1,024 | 1,022 |
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 8 | 6 |
| /30 | 255.255.255.252 | 4 | 2 |
| /31 | 255.255.255.254 | 2 | Point-to-Point |
| /32 | 255.255.255.255 | 1 | Single Host |

---

# CIDR Examples

```text
192.168.1.0/24
```

Scans

```
192.168.1.0
        │
        ▼
254 Usable Hosts
```

---

```text
10.0.0.0/8
```

Large enterprise network

```
16 Million Addresses
```

---

```text
172.16.0.0/12
```

Private enterprise network

---

# Nmap Target Examples

Scan one host

```bash
nmap 192.168.1.10
```

---

Scan an entire subnet

```bash
nmap 192.168.1.0/24
```

---

Scan a larger network

```bash
nmap 10.0.0.0/16
```

---

Scan a custom range

```bash
nmap 192.168.1.1-100
```

---

Scan multiple targets

```bash
nmap 192.168.1.10 192.168.1.20
```

---

Read targets from a file

```bash
nmap -iL targets.txt
```

---

# CIDR Visualization

```text
192.168.1.0/24

Network Bits              Host Bits

192.168.1.00000000

████████ ████████ ████████ ░░░░░░░░

      /24
```

---

# Broadcast Address

Example

```
Network

192.168.1.0/24
```

Broadcast

```
192.168.1.255
```

Usable Hosts

```
192.168.1.1

↓

192.168.1.254
```

---

# Network Components

```
Network Address

↓

Usable Hosts

↓

Broadcast Address
```

---

# Common CIDRs Used in Practice

| CIDR | Typical Usage |
|------|---------------|
| /8 | Very large enterprise networks |
| /16 | Large organizations |
| /24 | Standard LAN |
| /28 | Small office subnet |
| /30 | Router-to-router links |
| /32 | Single host |

---

# Best Practices

- Verify the network range before launching large scans.
- Use the smallest practical CIDR block to reduce unnecessary traffic.
- Remember that `/32` represents a single host.
- Confirm subnet boundaries when scanning enterprise environments.
- Use input files (`-iL`) for large collections of unrelated targets.

---

# Notes

- CIDR notation replaces traditional class-based addressing.
- Smaller prefix lengths represent larger networks.
- Larger prefix lengths represent fewer usable hosts.
- Understanding CIDR is essential for efficient network scanning.

---

# 20. IPv6 Quick Reference

IPv6 (Internet Protocol Version 6) is the successor to IPv4 and provides a vastly larger address space. It uses 128-bit addresses, supports modern networking features, and eliminates many limitations of IPv4.

Nmap fully supports IPv6 scanning through the `-6` option.

---

# IPv6 Address Structure

IPv6 addresses contain **128 bits**.

Format:

```text
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```

Eight groups of four hexadecimal digits.

```
8 Groups

↓

4 Hex Digits

↓

16 Bits per Group

↓

128 Bits Total
```

---

# Hexadecimal Characters

IPv6 uses hexadecimal notation.

| Decimal | Hex |
|----------|-----|
| 10 | A |
| 11 | B |
| 12 | C |
| 13 | D |
| 14 | E |
| 15 | F |

Example

```
2001:DB8::1
```

---

# IPv6 Address Compression

Leading zeros may be omitted.

Example

```
Original

2001:0db8:0000:0000:0000:0000:0000:0001

↓

Compressed

2001:db8::1
```

---

# Double Colon Rule

A double colon (`::`) replaces one consecutive sequence of zero groups.

Valid

```
2001:db8::1
```

Invalid

```
2001::db8::1
```

A double colon may appear **only once** in an IPv6 address.

---

# Common IPv6 Address Types

| Prefix | Type | Description |
|--------|------|-------------|
| 2000::/3 | Global Unicast | Public Internet addresses |
| FC00::/7 | Unique Local | Private addressing |
| FE80::/10 | Link-Local | Local network communication |
| FF00::/8 | Multicast | One-to-many communication |
| ::1 | Loopback | Localhost |
| :: | Unspecified | No assigned address |

---

# Global Unicast

Example

```text
2001:4860:4860::8888
```

Used for Internet-routable communication.

---

# Link-Local

Example

```text
fe80::1234:abcd:5678:9abc
```

Characteristics

- Automatically assigned
- Valid only on the local network
- Cannot be routed across the Internet

---

# Unique Local Address (ULA)

Example

```text
fd12:3456:789a::1
```

Comparable to IPv4 private address ranges.

---

# Multicast

Example

```text
ff02::1
```

Used instead of broadcast.

Common multicast addresses

| Address | Purpose |
|----------|---------|
| ff02::1 | All Nodes |
| ff02::2 | All Routers |

---

# Loopback

```
::1
```

Equivalent to

```
127.0.0.1
```

---

# IPv4 vs IPv6

| Feature | IPv4 | IPv6 |
|----------|------|------|
| Address Length | 32 Bits | 128 Bits |
| Notation | Decimal | Hexadecimal |
| Broadcast | Yes | No |
| Multicast | Limited | Native |
| NAT | Common | Usually unnecessary |
| Address Space | ~4.3 Billion | 2¹²⁸ |

---

# IPv6 Prefix Lengths

| Prefix | Typical Usage |
|---------|---------------|
| /32 | ISP allocation |
| /48 | Organization |
| /56 | Small business |
| /64 | Standard LAN |
| /128 | Single host |

Most LAN networks use:

```
/64
```

---

# Nmap IPv6 Scanning

Scan a host

```bash
nmap -6 2001:db8::10
```

---

Scan a subnet

```bash
nmap -6 2001:db8:abcd::/64
```

---

Service detection

```bash
nmap -6 -sV 2001:db8::20
```

---

OS detection

```bash
nmap -6 -O 2001:db8::20
```

---

SYN Scan

```bash
nmap -6 -sS 2001:db8::20
```

---

Version + OS Detection

```bash
nmap -6 -A 2001:db8::20
```

---

# Example Output

```text
PORT      STATE SERVICE

22/tcp    open  ssh

80/tcp    open  http

443/tcp   open  https
```

---

# IPv6 Address Visualization

```
2001:0db8:85a3:0000:0000:8a2e:0370:7334

│──── Network Prefix ────││──── Interface ID ────│
```

Typical LAN

```
Network Prefix (/64)

↓

Interface Identifier (/64)
```

---

# Important Notes for Nmap

- Always specify `-6` when scanning IPv6 targets.
- IPv6 scanning requires IPv6 connectivity.
- Link-local addresses often require an interface specification (e.g., `%eth0` or `%ens33`).
- Many enterprise environments expose services only over IPv6.
- IPv6 firewalls may behave differently from IPv4 firewalls.

---

# Best Practices

- Verify IPv6 connectivity before scanning.
- Prefer Global Unicast addresses for remote assessments.
- Use Link-Local addresses only within the same network segment.
- Include IPv6 in security assessments whenever available.
- Test both IPv4 and IPv6 services, as configurations may differ.

---

# Notes

- IPv6 uses 128-bit hexadecimal addresses.
- There is no broadcast in IPv6; multicast replaces broadcast functionality.
- `/64` is the standard subnet size for most LANs.
- Nmap supports IPv6 scanning with the `-6` option across most scan types.

---

# 21. Output Files & Report Formats

Nmap can save scan results in multiple output formats. Choosing the correct format makes reporting, automation, parsing, and future analysis much easier.

---

# Why Save Scan Results?

Saving scan results allows you to:

- Compare scans over time
- Create reports
- Import results into other tools
- Parse results automatically
- Keep evidence during penetration tests

---

# Output Options

| Option | Format | Human Readable | Machine Readable |
|---------|--------|:--------------:|:----------------:|
| `-oN` | Normal | ✅ | ❌ |
| `-oX` | XML | ❌ | ✅ |
| `-oG` | Grepable | Partial | ✅ |
| `-oA` | All Formats | ✅ | ✅ |
| `-oS` | Script Kiddie *(Deprecated)* | ✅ | ❌ |

---

# Normal Output (`-oN`)

Saves the same output shown in the terminal.

Example

```bash
nmap -oN scan.txt target
```

Example Output

```text
Nmap scan report for 192.168.1.10

22/tcp open ssh

80/tcp open http

443/tcp open https
```

Recommended for:

- Documentation
- Human review
- Reports

---

# XML Output (`-oX`)

Stores scan results in XML format.

```bash
nmap -oX scan.xml target
```

Example

```xml
<host>

    <address addr="192.168.1.10"/>

    <ports>

        <port portid="22"/>

    </ports>

</host>
```

Recommended for:

- Automation
- Parsing
- Integration with other security tools

---

# Grepable Output (`-oG`)

Produces simplified text that is easy to search.

```bash
nmap -oG scan.grep target
```

Example

```text
Host: 192.168.1.10

Ports: 22/open/tcp//ssh///
```

Useful for

```bash
grep
awk
sed
```

> **Note:** Grepable output is considered **deprecated**. XML output is preferred for modern automation.

---

# All Formats (`-oA`)

Produces all major output formats simultaneously.

```bash
nmap -oA audit target
```

Generated Files

```text
audit.nmap

audit.xml

audit.gnmap
```

This is the most commonly recommended option during professional assessments.

---

# Append Timestamp

Useful for keeping historical scans.

Example

```bash
nmap -oA scan-2026-07-19 target
```

---

# Verbose Output

```bash
nmap -v target
```

More detailed progress information.

Very Verbose

```bash
nmap -vv target
```

---

# Debug Output

```bash
nmap -d target
```

Higher debug level

```bash
nmap -d2 target

nmap -d5 target

nmap -d9 target
```

Useful for troubleshooting scan behavior.

---

# Resume Interrupted Scan

```bash
nmap --resume audit.nmap
```

Continues an interrupted scan.

---

# Reading XML Reports

Many tools support importing XML files.

Examples include:

- SIEM platforms
- Vulnerability scanners
- Asset management tools
- Custom scripts
- Reporting dashboards

---

# Typical Workflow

```text
Run Scan

↓

Save Results

↓

Review Output

↓

Import XML

↓

Generate Report

↓

Archive Results
```

---

# File Naming Best Practices

Good Examples

```text
corp-lan.nmap

corp-lan.xml

dmz-scan.nmap

external-2026-07-19.xml
```

Avoid

```text
scan1.txt

test.txt

newscan.txt

temp.xml
```

---

# Output Comparison

| Format | Advantages | Best For |
|---------|------------|----------|
| Normal | Easy to read | Documentation |
| XML | Structured | Automation |
| GNMAP | Searchable | Legacy scripts |
| All | Complete | Professional assessments |

---

# Combining Output with Other Options

Version Detection

```bash
nmap -sV -oA services target
```

Aggressive Scan

```bash
nmap -A -oA aggressive target
```

UDP Scan

```bash
nmap -sU -oA udp target
```

OS Detection

```bash
nmap -O -oA osdetect target
```

---

# Best Practices

- Prefer `-oA` during penetration tests.
- Store scan results in organized directories.
- Include timestamps in filenames.
- Keep XML reports for automation.
- Archive important scans for future comparison.

---

# Notes

- XML is the preferred format for automation and third-party tools.
- Normal output is ideal for human-readable documentation.
- `-oA` generates `.nmap`, `.xml`, and `.gnmap` files simultaneously.
- Grepable output (`.gnmap`) is retained mainly for backward compatibility.

---

# 22. Exit Codes & Scan Results Interpretation

Nmap returns an exit code when it finishes execution. Exit codes allow shell scripts, automation frameworks, and security tools to determine whether the scan completed successfully or encountered an error.

---

# What is an Exit Code?

An exit code is an integer returned by a program when it terminates.

Example

```bash
echo $?
```

Linux and macOS display the exit status of the previously executed command.

---

# Standard Nmap Exit Codes

| Exit Code | Meaning |
|-----------|---------|
| 0 | Scan completed successfully |
| 1 | Fatal error occurred |
| 2 | Incorrect command-line usage |

---

# Exit Code 0

```
0
```

Meaning

- Scan completed successfully.
- Results were generated.
- No fatal errors occurred.

Example

```bash
nmap -sS 192.168.1.10
```

Result

```
Exit Code = 0
```

---

# Exit Code 1

```
1
```

Meaning

A fatal runtime error occurred.

Possible causes

- Insufficient privileges
- Invalid network interface
- Packet capture failure
- DNS resolution failure
- Unable to access required resources

Example

```bash
nmap -sS target
```

Without administrator/root privileges:

```
You requested a scan type which requires root privileges.
```

Exit Code

```
1
```

---

# Exit Code 2

```
2
```

Meaning

Command-line syntax is incorrect.

Example

```bash
nmap --unknown-option
```

Output

```
Illegal option
```

Exit Code

```
2
```

---

# Checking Exit Codes in Bash

```bash
nmap target

echo $?
```

Example

```text
0
```

---

# Using Exit Codes in Shell Scripts

```bash
if [ $? -eq 0 ]; then
    echo "Scan Successful"
else
    echo "Scan Failed"
fi
```

---

# Common Scan States

| State | Meaning |
|--------|---------|
| open | Service is accepting connections |
| closed | Port is reachable but no service is listening |
| filtered | Firewall prevents determination |
| unfiltered | Port is reachable but scan type cannot determine openness |
| open\|filtered | Cannot distinguish between open and filtered |
| closed\|filtered | Cannot distinguish between closed and filtered |

---

# Understanding Port States

## Open

```
22/tcp open ssh
```

Interpretation

- Service is running.
- Further enumeration is recommended.

---

## Closed

```
22/tcp closed ssh
```

Interpretation

- Host is reachable.
- No service is listening.

---

## Filtered

```
22/tcp filtered ssh
```

Interpretation

A firewall or filtering device blocks the probe.

---

## Open|Filtered

```
161/udp open|filtered snmp
```

Interpretation

Usually seen during UDP scans.

Nmap cannot determine whether:

- the service is open, or
- packets are being filtered.

---

## Closed|Filtered

Less common.

Usually associated with specialized scan techniques.

---

# Typical Nmap Output

```text
PORT     STATE SERVICE

22/tcp   open  ssh

80/tcp   open  http

111/tcp  filtered rpcbind

443/tcp  open  https
```

Interpretation

- SSH available
- HTTP available
- RPC filtered
- HTTPS available

---

# Host Status Interpretation

```
Host is up
```

Meaning

Target responded to discovery probes.

---

```
Host seems down
```

Meaning

Target did not respond.

Possible reasons

- Powered off
- Firewall
- ICMP blocked
- Incorrect address

Override

```bash
nmap -Pn target
```

---

# Common Warning Messages

### Failed DNS Resolution

```text
Failed to resolve given hostname.
```

Cause

- Incorrect hostname
- DNS issue

---

### Permission Error

```text
You requested a scan type which requires root privileges.
```

Cause

Administrative privileges required.

---

### Network Unreachable

```text
Network is unreachable
```

Cause

No route exists to the target network.

---

### Host Timeout

```text
Host timeout
```

Cause

- Slow network
- Heavy filtering
- High latency

---

# Troubleshooting Checklist

✓ Verify the target address.

✓ Confirm network connectivity.

✓ Check firewall rules.

✓ Use appropriate privileges.

✓ Reduce scan speed if necessary.

✓ Verify DNS resolution.

✓ Confirm interface selection.

---

# Automation Example

```bash
nmap -oA scan target

if [ $? -eq 0 ]
then
    echo "Report generated successfully."
else
    echo "Scan failed."
fi
```

---

# Best Practices

- Always verify exit codes in automation scripts.
- Do not rely solely on a single port state.
- Investigate filtered ports using additional scan techniques.
- Save scan results before troubleshooting.
- Review warning messages carefully.

---

# Notes

- Exit code **0** indicates successful execution, not necessarily that open ports were found.
- Exit code **1** indicates a runtime failure.
- Exit code **2** indicates invalid command-line usage.
- Correct interpretation of port states is essential for accurate security assessments.

---

# 23. Nmap One-Liners Cheat Sheet

This section provides a collection of practical Nmap commands for common reconnaissance, enumeration, and auditing tasks. These examples are intended as quick references during security assessments.

---

# Basic Scans

Scan a single host

```bash
nmap 192.168.1.10
```

---

Scan multiple hosts

```bash
nmap 192.168.1.10 192.168.1.20
```

---

Scan an entire subnet

```bash
nmap 192.168.1.0/24
```

---

Scan targets from a file

```bash
nmap -iL targets.txt
```

---

Exclude specific hosts

```bash
nmap 192.168.1.0/24 --exclude 192.168.1.1
```

---

# Host Discovery

Ping sweep

```bash
nmap -sn 192.168.1.0/24
```

---

Disable host discovery

```bash
nmap -Pn target
```

---

ARP discovery

```bash
nmap -PR 192.168.1.0/24
```

---

ICMP Echo

```bash
nmap -PE target
```

---

Timestamp Request

```bash
nmap -PP target
```

---

# Port Scanning

Top 100 ports

```bash
nmap --top-ports 100 target
```

---

Top 1000 ports

```bash
nmap target
```

---

All TCP ports

```bash
nmap -p- target
```

---

Specific ports

```bash
nmap -p 22,80,443 target
```

---

Port range

```bash
nmap -p 1-1024 target
```

---

Fast scan

```bash
nmap -F target
```

---

# Scan Types

SYN Scan

```bash
nmap -sS target
```

---

TCP Connect Scan

```bash
nmap -sT target
```

---

UDP Scan

```bash
nmap -sU target
```

---

ACK Scan

```bash
nmap -sA target
```

---

FIN Scan

```bash
nmap -sF target
```

---

NULL Scan

```bash
nmap -sN target
```

---

Xmas Scan

```bash
nmap -sX target
```

---

# Service Enumeration

Version detection

```bash
nmap -sV target
```

---

Aggressive version detection

```bash
nmap -sV --version-all target
```

---

OS Detection

```bash
nmap -O target
```

---

Aggressive Scan

```bash
nmap -A target
```

---

Default NSE Scripts

```bash
nmap -sC target
```

---

Version + Scripts

```bash
nmap -sC -sV target
```

---

# NSE Examples

HTTP title

```bash
nmap --script http-title target
```

---

HTTP headers

```bash
nmap --script http-headers target
```

---

SMB shares

```bash
nmap --script smb-enum-shares target
```

---

SMB users

```bash
nmap --script smb-enum-users target
```

---

FTP anonymous login

```bash
nmap --script ftp-anon target
```

---

SSH host keys

```bash
nmap --script ssh-hostkey target
```

---

DNS information

```bash
nmap --script dns-recursion target
```

---

SNMP information

```bash
nmap --script snmp-info target
```

---

Vulnerability scan

```bash
nmap --script vuln target
```

---

Safe scripts

```bash
nmap --script safe target
```

---

# Performance

Timing Template 4

```bash
nmap -T4 target
```

---

Timing Template 5

```bash
nmap -T5 target
```

---

Minimum rate

```bash
nmap --min-rate 1000 target
```

---

Maximum retries

```bash
nmap --max-retries 2 target
```

---

Host timeout

```bash
nmap --host-timeout 5m target
```

---

# Firewall Evasion

Fragment packets

```bash
nmap -f target
```

---

Randomize host order

```bash
nmap --randomize-hosts target
```

---

Decoy scan

```bash
nmap -D RND:10 target
```

---

Spoof MAC address

```bash
nmap --spoof-mac 0 target
```

---

Source port

```bash
nmap --source-port 53 target
```

---

# Output

Normal output

```bash
nmap -oN scan.txt target
```

---

XML output

```bash
nmap -oX scan.xml target
```

---

All formats

```bash
nmap -oA audit target
```

---

Verbose

```bash
nmap -v target
```

---

Debug

```bash
nmap -d target
```

---

# IPv6

Basic IPv6 scan

```bash
nmap -6 target
```

---

Version detection

```bash
nmap -6 -sV target
```

---

OS detection

```bash
nmap -6 -O target
```

---

Aggressive scan

```bash
nmap -6 -A target
```

---

# Common Combinations

Quick TCP scan

```bash
nmap -T4 -F target
```

---

Full TCP scan

```bash
nmap -p- -T4 target
```

---

Full enumeration

```bash
nmap -A -T4 target
```

---

Stealth scan

```bash
nmap -sS -Pn target
```

---

Web server enumeration

```bash
nmap -p80,443 -sC -sV target
```

---

Database discovery

```bash
nmap -p1433,3306,5432,1521 target
```

---

Windows host enumeration

```bash
nmap -p135,139,445 -sC -sV target
```

---

UDP Top Services

```bash
nmap -sU --top-ports 20 target
```

---

Save complete assessment

```bash
nmap -A -T4 -oA assessment target
```

---

# Best Practices

- Start with host discovery before launching full scans.
- Use `-sS` when raw packet privileges are available.
- Combine `-sC` and `-sV` for efficient service enumeration.
- Save results using `-oA` for documentation and automation.
- Adjust timing templates based on network stability and assessment scope.
- Verify findings with additional tools when necessary.

---

# Notes

- These one-liners are intended as quick references for common scenarios.
- Modify timing, port selection, and script usage according to the assessment environment.
- Always ensure you have authorization before scanning networks or systems you do not own or administer.

---

# 24. Scan Type Comparison Matrix

Nmap provides multiple scan techniques, each designed for different environments and objectives. Understanding their differences helps you select the most effective scan while balancing speed, stealth, accuracy, and privilege requirements.

---

# Scan Type Overview

| Option | Scan Name | Protocol |
|----------|-----------|----------|
| `-sS` | SYN Scan | TCP |
| `-sT` | TCP Connect Scan | TCP |
| `-sU` | UDP Scan | UDP |
| `-sA` | ACK Scan | TCP |
| `-sW` | Window Scan | TCP |
| `-sM` | Maimon Scan | TCP |
| `-sF` | FIN Scan | TCP |
| `-sN` | NULL Scan | TCP |
| `-sX` | Xmas Scan | TCP |
| `-sI` | Idle Scan | TCP |
| `-sY` | SCTP INIT Scan | SCTP |
| `-sZ` | SCTP COOKIE-ECHO Scan | SCTP |

---

# Feature Comparison

| Scan | Fast | Stealth | Root Required | Firewall Detection | OS Support |
|------|:----:|:-------:|:-------------:|:------------------:|:----------:|
| SYN (`-sS`) | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ✅ | Moderate | Excellent |
| Connect (`-sT`) | ⭐⭐⭐ | ⭐ | ❌ | Limited | Excellent |
| UDP (`-sU`) | ⭐ | ⭐⭐ | ✅ | Moderate | Excellent |
| ACK (`-sA`) | ⭐⭐⭐⭐ | ⭐⭐⭐ | ✅ | Excellent | Excellent |
| FIN (`-sF`) | ⭐⭐⭐ | ⭐⭐⭐⭐ | ✅ | Limited | UNIX-like |
| NULL (`-sN`) | ⭐⭐⭐ | ⭐⭐⭐⭐ | ✅ | Limited | UNIX-like |
| Xmas (`-sX`) | ⭐⭐⭐ | ⭐⭐⭐⭐ | ✅ | Limited | UNIX-like |
| Window (`-sW`) | ⭐⭐⭐ | ⭐⭐⭐ | ✅ | Limited | OS-dependent |
| Maimon (`-sM`) | ⭐⭐ | ⭐⭐⭐ | ✅ | Limited | UNIX-like |
| Idle (`-sI`) | ⭐⭐ | ⭐⭐⭐⭐⭐ | ✅ | Excellent | Depends on Zombie |
| SCTP INIT (`-sY`) | ⭐⭐⭐ | ⭐⭐⭐ | ✅ | Moderate | SCTP Hosts |
| SCTP COOKIE (`-sZ`) | ⭐⭐ | ⭐⭐⭐⭐ | ✅ | Moderate | SCTP Hosts |

---

# Detection Accuracy

| Scan Type | Open | Closed | Filtered |
|------------|:----:|:------:|:--------:|
| SYN | Excellent | Excellent | Good |
| Connect | Excellent | Excellent | Good |
| UDP | Moderate | Good | Moderate |
| ACK | No | No | Excellent |
| FIN | Moderate | Moderate | Moderate |
| NULL | Moderate | Moderate | Moderate |
| Xmas | Moderate | Moderate | Moderate |
| Idle | Excellent | Excellent | Good |

---

# Packet Behavior

| Scan | TCP Handshake |
|------|---------------|
| SYN | Partial |
| Connect | Complete |
| UDP | None |
| ACK | ACK Only |
| FIN | FIN Only |
| NULL | No Flags |
| Xmas | FIN + PSH + URG |
| Idle | Uses Zombie Host |

---

# Typical Responses

| Scan | Open Port | Closed Port |
|------|-----------|-------------|
| SYN | SYN/ACK | RST |
| Connect | Connection Established | RST |
| UDP | UDP Reply | ICMP Port Unreachable |
| ACK | RST | RST |
| FIN | No Response | RST |
| NULL | No Response | RST |
| Xmas | No Response | RST |

---

# Firewall Detection Capability

| Scan | Can Detect Filtering? |
|------|:---------------------:|
| SYN | Yes |
| Connect | Limited |
| ACK | Excellent |
| UDP | Good |
| FIN | Limited |
| NULL | Limited |
| Xmas | Limited |
| Idle | Moderate |

---

# Stealth Comparison

```
Most Stealthy

↓

Idle Scan

↓

FIN / NULL / Xmas

↓

SYN Scan

↓

ACK Scan

↓

UDP Scan

↓

Connect Scan

↓

Most Detectable
```

---

# Speed Comparison

```
Fastest

↓

SYN Scan

↓

ACK Scan

↓

Connect Scan

↓

FIN / NULL / Xmas

↓

Idle Scan

↓

UDP Scan

↓

Slowest
```

---

# Privilege Requirements

| Scan | Administrator / Root Required |
|------|:-----------------------------:|
| SYN | Yes |
| Connect | No |
| UDP | Usually |
| ACK | Yes |
| FIN | Yes |
| NULL | Yes |
| Xmas | Yes |
| Idle | Yes |

---

# Recommended Use Cases

| Scenario | Recommended Scan |
|-----------|------------------|
| Quick reconnaissance | `-sS` |
| No administrator privileges | `-sT` |
| Firewall analysis | `-sA` |
| UDP service discovery | `-sU` |
| Stealth assessment | `-sS` |
| Advanced stealth | `-sI` |
| Legacy UNIX firewall testing | `-sF`, `-sN`, `-sX` |
| SCTP environments | `-sY`, `-sZ` |

---

# Decision Guide

```text
Need the fastest TCP scan?

        │
        ▼

Use SYN Scan (-sS)

──────────────────────────

No administrator privileges?

        │
        ▼

Use Connect Scan (-sT)

──────────────────────────

Need UDP services?

        │
        ▼

Use UDP Scan (-sU)

──────────────────────────

Testing firewall rules?

        │
        ▼

Use ACK Scan (-sA)

──────────────────────────

Need maximum stealth?

        │
        ▼

Use Idle Scan (-sI)
```

---

# Best Practices

- Use **SYN Scan (`-sS`)** as the default TCP scan whenever possible.
- Choose **TCP Connect (`-sT`)** only when raw packet privileges are unavailable.
- Limit **UDP scans (`-sU`)** to relevant ports to reduce scan time.
- Use **ACK scans (`-sA`)** to analyze firewall filtering rather than port openness.
- Validate unusual results using multiple scan techniques.

---

# Notes

- No single scan type is ideal for every situation.
- SYN Scan provides the best balance of speed, accuracy, and stealth.
- UDP scans require patience and careful interpretation.
- Idle Scans offer exceptional stealth but depend on finding a suitable zombie host.
- FIN, NULL, and Xmas scans are less effective against many modern Windows systems and stateful firewalls.

---
