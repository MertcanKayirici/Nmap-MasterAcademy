# Lab 14 — FTP Scripts

> Learn how to enumerate FTP servers using Nmap NSE scripts and analyze authentication, server configuration, and available capabilities.

---

# Overview

File Transfer Protocol (FTP) is one of the oldest Internet protocols and is still used in many environments for transferring files.

Although many organizations have migrated to more secure alternatives such as SFTP or FTPS, FTP servers continue to exist in internal networks, embedded devices, legacy systems, and laboratory environments.

Nmap's NSE includes several scripts that can safely gather information from FTP servers without modifying their configuration.

---

# Learning Objectives

After completing this lab, you will be able to:

- Identify FTP services.
- Test anonymous authentication.
- Retrieve FTP banners.
- Enumerate FTP capabilities.
- Analyze FTP configuration.
- Determine appropriate follow-up actions.

---

# Difficulty

⭐⭐⭐☆☆ Intermediate

---

# Estimated Time

45–60 Minutes

---

# Prerequisites

- Lab 11 completed
- Basic understanding of FTP
- Target with an FTP service

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| FTP Server | 192.168.56.20 | Target |

---

# Scenario

A previous scan identified:

```text
21/tcp open ftp
```

Your objective is to determine:

- Which FTP software is running?
- Is anonymous login available?
- Which authentication methods are supported?
- What additional information can be collected?

---

# What is FTP?

FTP is a protocol used to transfer files between systems.

Common ports:

| Port | Purpose |
|------|----------|
| 21 | Control Channel |
| 20 | Data Channel (Active Mode) |

Many modern servers use passive mode for data transfers.

---

# Step 1 — Identify the FTP Service

Run:

```bash
nmap -sV -p21 192.168.56.20
```

Example Output

```text
21/tcp open ftp

vsftpd 3.0.5
```

Questions:

- Which FTP server software is detected?
- Does the version appear current?

---

# Step 2 — Test Anonymous Login

Run:

```bash
nmap --script ftp-anon -p21 192.168.56.20
```

Example Output

```text
Anonymous FTP login allowed
```

or

```text
Anonymous FTP login not allowed
```

Questions:

- Is anonymous access expected?
- Does it align with organizational policy?

---

# Step 3 — Retrieve FTP Banner

Run:

```bash
nmap --script banner -p21 192.168.56.20
```

Example Output

```text
220 vsFTPd 3.0.5 ready
```

The banner may reveal:

- Server software
- Version
- Hostname
- Welcome message

---

# Step 4 — Enumerate FTP Capabilities

Run:

```bash
nmap --script ftp-syst -p21 192.168.56.20
```

Example Output

```text
UNIX Type: L8
```

This may provide clues about the underlying operating system.

---

# Step 5 — Execute Multiple FTP Scripts

Run:

```bash
nmap --script "ftp-anon,ftp-syst,banner" -p21 192.168.56.20
```

This combines several FTP-related checks into one scan.

---

# Understanding the Results

Example

```text
Anonymous FTP login allowed
```

Possible interpretation:

- Public file repository
- Software distribution server
- Legacy configuration
- Administrative review may be appropriate

---

Example

```text
UNIX Type: L8
```

Possible interpretation:

- Unix-like operating system
- Linux or BSD family
- Combine with OS detection for additional context

---

# Common FTP Scripts

| Script | Purpose |
|---------|---------|
| ftp-anon | Check anonymous login |
| ftp-syst | Retrieve system type |
| ftp-bounce | Check FTP bounce support |
| ftp-libopie | Detect OPIE support |
| ftp-proftpd-backdoor | Identify specific ProFTPD backdoor (legacy environments) |
| banner | Retrieve service banner |

---

# NSE Script Deep Dive

## Script

```text
ftp-anon.nse
```

Category

```text
default
auth
safe
```

Purpose

Checks whether anonymous authentication is permitted.

Typical Uses

- Validate FTP configuration
- Identify publicly accessible repositories
- Confirm anonymous access settings

Limitations

- Does not enumerate files unless permitted.
- Results depend on server configuration.

Related Scripts

- ftp-syst
- banner
- ftp-bounce

---

# Related Services

FTP servers are often deployed alongside:

- SSH (22)
- HTTP (80)
- HTTPS (443)
- SMB (445)
- NFS (2049)

These services may provide complementary methods for transferring or accessing files.

---

# Thinking Like an Analyst

Suppose the scan reports:

```text
Anonymous FTP login allowed
```

Questions:

- Is this intentional?
- Is the server intended for public distribution?
- Should administrators verify exposed content?

---

Another Example

```text
220 Welcome to Backup Server
```

Questions:

- Does the banner reveal the server's role?
- Is unnecessary information being disclosed?
- Could the banner be simplified?

---

# Common Mistakes

## Assuming Anonymous Access Is Always a Security Issue

Some organizations intentionally provide anonymous FTP for software downloads or public resources.

Always interpret findings within the system's intended purpose.

---

## Ignoring Banner Information

Service banners often provide valuable context about server software and configuration.

---

## Treating FTP as an Isolated Service

Consider how FTP relates to other services running on the same host.

---

# Challenge

Run:

```bash
nmap --script "ftp-anon,ftp-syst,banner" -p21 target
```

Document:

- FTP software
- Banner
- Anonymous login status
- System type

---

# Bonus Challenge

List all FTP-related NSE scripts:

```bash
ls /usr/share/nmap/scripts/ftp*
```

Answer:

- How many FTP scripts are installed?
- Which scripts relate to authentication?
- Which scripts gather system information?
- Which scripts appear to perform configuration checks?

---

# Key Takeaways

- FTP enumeration provides insight into authentication, configuration, and server identity.
- Anonymous access should always be evaluated in the context of the system's intended purpose.
- Service banners and system responses often reveal useful operational details.
- Combining multiple FTP scripts produces a more complete picture of the service.

---

# Next Lab

➡ **Lab 15 — SSL Scripts**

In the next lab, you will inspect SSL/TLS certificates, supported protocol versions, and encryption settings using dedicated NSE scripts.