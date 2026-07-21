# Lab 16 — DNS Scripts

> Learn how to enumerate DNS services using Nmap NSE scripts and analyze DNS infrastructure, records, and server information.

---

# Overview

The Domain Name System (DNS) translates human-readable domain names into IP addresses.

Almost every network relies on DNS for communication.

DNS servers may provide valuable information about:

- Domain names
- Name servers
- Mail servers
- Reverse lookups
- Supported DNS features
- Server software

Nmap provides several NSE scripts that help administrators and security professionals inspect DNS services during authorized assessments.

---

# Learning Objectives

After completing this lab, you will be able to:

- Detect DNS services.
- Query DNS servers.
- Retrieve DNS records.
- Understand reverse lookups.
- Analyze DNS infrastructure.
- Interpret DNS-related findings.

---

# Difficulty

⭐⭐⭐☆☆ Intermediate

---

# Estimated Time

45–60 Minutes

---

# Prerequisites

- Lab 11 completed
- Target with a DNS service
- Basic understanding of DNS

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| DNS Server | 192.168.56.53 | Target |

---

# Scenario

A previous scan identified:

```text
53/tcp open domain
53/udp open domain
```

Your task is to determine:

- Which DNS server is running?
- Which records are available?
- Which name servers are configured?
- Which DNS features are supported?

---

# What is DNS?

DNS translates names into IP addresses.

Example:

```
example.com

↓

93.184.216.34
```

Common DNS record types include:

| Record | Purpose |
|---------|----------|
| A | IPv4 Address |
| AAAA | IPv6 Address |
| MX | Mail Server |
| NS | Name Server |
| TXT | Text Record |
| CNAME | Alias |
| PTR | Reverse Lookup |

---

# Step 1 — Identify the DNS Service

Run:

```bash
nmap -sV -p53 192.168.56.53
```

Example Output

```text
53/tcp open domain

ISC BIND 9.18
```

---

# Step 2 — Retrieve DNS Information

Run:

```bash
nmap --script dns-recursion -p53 192.168.56.53
```

This checks whether recursive queries are supported.

---

# Step 3 — Reverse DNS Lookup

Run:

```bash
nmap --script dns-brute example.local
```

This script attempts to discover common subdomains.

---

# Step 4 — Query Name Servers

Run:

```bash
nmap --script dns-nsid -p53 192.168.56.53
```

Example Output

```text
Server Identifier

ns1.example.local
```

---

# Step 5 — Execute Multiple DNS Scripts

Run:

```bash
nmap --script "dns-recursion,dns-nsid" -p53 192.168.56.53
```

This combines multiple DNS checks into a single scan.

---

# Understanding the Results

Example

```text
Recursion

Enabled
```

Possible interpretation:

- The server accepts recursive queries.
- This behavior should be reviewed against the intended role of the server.

---

Example

```text
Name Server

ns1.example.local
```

Possible interpretation:

- Internal DNS naming convention
- Infrastructure naming information
- Useful for inventory and documentation

---

# Common DNS Scripts

| Script | Purpose |
|---------|---------|
| dns-recursion | Check recursive query support |
| dns-nsid | Retrieve DNS server identifier |
| dns-brute | Discover common subdomains |
| dns-service-discovery | Identify DNS-related services |

---

# NSE Script Deep Dive

## Script

```text
dns-recursion.nse
```

Category

```text
safe
discovery
```

Purpose

Determines whether the DNS server performs recursive queries.

Typical Uses

- DNS configuration review
- Infrastructure assessment
- Operational verification

Limitations

- Requires a reachable DNS server.
- Results depend on server configuration.

Related Scripts

- dns-nsid
- dns-brute

---

# Related Services

DNS often operates alongside:

- DHCP
- LDAP
- Kerberos
- Active Directory
- Mail Servers

Understanding these relationships helps place DNS findings into a broader infrastructure context.

---

# Thinking Like an Analyst

Suppose the scan reports:

```text
Server Identifier

ns1.internal.local
```

Questions:

- Is this an internal naming convention?
- Does the identifier match organizational documentation?
- Are there additional DNS servers?

---

Another Example

```text
Recursion

Enabled
```

Questions:

- Is recursion expected on this server?
- Should this behavior be restricted?
- Does the server's role justify this configuration?

---

# Common Mistakes

## Assuming Every DNS Server Should Behave the Same

Authoritative and recursive DNS servers often have different configurations.

---

## Ignoring DNS Metadata

Server identifiers and record information can help document infrastructure.

---

## Forgetting UDP

DNS primarily uses UDP, but TCP is also used for larger responses and zone transfers.

---

# Challenge

Run:

```bash
nmap --script "dns-recursion,dns-nsid" -p53 target
```

Document:

- DNS software
- Server identifier
- Recursion status
- Interesting findings

---

# Bonus Challenge

List DNS-related NSE scripts:

```bash
ls /usr/share/nmap/scripts/dns*
```

Answer:

- Which scripts retrieve server information?
- Which scripts enumerate records?
- Which scripts relate to discovery?

---

# Key Takeaways

- DNS enumeration helps understand network infrastructure.
- NSE scripts can safely retrieve server information and configuration details.
- DNS findings should always be interpreted in the context of the server's intended role.
- DNS is a foundational service that often provides valuable operational insight.

---

# Next Lab

➡ **Lab 17 — Vulnerability Scripts**

In the next lab, you will use NSE's `vuln` category to perform safe vulnerability detection and understand how Nmap assists in identifying potential security issues.