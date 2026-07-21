# Common Network Services

> A Professional Reference Guide for Nmap Users, Penetration Testers, Network Engineers, SOC Analysts, and Security Professionals.

---

# Introduction

Knowing **port numbers** is only part of network reconnaissance.

A penetration tester, system administrator, or SOC analyst must also understand the **services** running behind those ports.

For example:

- Port **22** usually indicates SSH.
- Port **80** generally hosts HTTP.
- Port **443** commonly serves HTTPS.
- Port **445** often exposes SMB.
- Port **3389** usually represents Remote Desktop.

However, identifying a port is only the first step.

Understanding:

- what the service does,
- how it communicates,
- common software,
- security weaknesses,
- detection techniques,
- and Nmap enumeration methods

is what separates beginners from experienced professionals.

This reference introduces the most common services encountered during penetration tests and enterprise network assessments.

---

# Service Anatomy

Almost every network service follows the same basic communication model.

```text
             Client

                │

        Service Request

                │

                ▼

        Network Protocol

                │

                ▼

        Listening Service

                │

        Authentication

                │

        Business Logic

                │

                ▼

          Operating System

                │

                ▼

            Resources

 Database

 Files

 Memory

 Hardware
```

During an Nmap scan, the scanner attempts to determine:

- Is the port open?
- Which service is listening?
- Which software is running?
- What version is installed?
- Which operating system is hosting it?
- Are there known vulnerabilities?
- Can NSE scripts collect additional information?

---

# Service Categories

Enterprise environments generally contain services belonging to several categories.

| Category | Examples |
|-----------|----------|
| Web Services | HTTP, HTTPS |
| Remote Administration | SSH, RDP, WinRM, VNC |
| File Sharing | SMB, NFS, FTP, SFTP |
| Email | SMTP, POP3, IMAP |
| Databases | MySQL, PostgreSQL, MSSQL, Oracle |
| Authentication | LDAP, Kerberos, Active Directory |
| Infrastructure | DNS, DHCP, NTP |
| Monitoring | SNMP, Syslog |
| Virtualization | VMware, Hyper-V |
| Containers | Docker API, Kubernetes |
| Messaging | MQTT, AMQP, Kafka |
| Backup | rsync, Backup Servers |
| Security | VPN, PKI, IDS, IPS, SIEM |

---

# Service Recognition Workflow

Experienced penetration testers rarely identify services by port number alone.

Instead, they combine multiple sources of information.

```text
Open Port

     │

     ▼

Service Detection (-sV)

     │

     ▼

Version Detection

     │

     ▼

Banner Grabbing

     │

     ▼

NSE Enumeration

     │

     ▼

Fingerprint Analysis

     │

     ▼

Attack Surface Mapping
```

---

# Common Nmap Commands

Basic Service Detection

```bash
nmap -sV target
```

Aggressive Detection

```bash
nmap -A target
```

Default Scripts

```bash
nmap -sC -sV target
```

Version Intensity

```bash
nmap -sV --version-intensity 9 target
```

Operating System Detection

```bash
nmap -O target
```

Service Enumeration

```bash
nmap -sV -Pn target
```

---

# Why Service Detection Matters

Finding an open port is useful.

Understanding **what is behind that port** is far more valuable.

For example:

| Port | Service | Possible Risk |
|-------|----------|---------------|
| 22 | SSH | Weak credentials |
| 80 | HTTP | Directory traversal |
| 443 | HTTPS | Web vulnerabilities |
| 445 | SMB | Lateral movement |
| 3306 | MySQL | Database compromise |
| 3389 | RDP | Remote desktop attacks |
| 5432 | PostgreSQL | Database exposure |
| 6379 | Redis | Unauthenticated access |
| 9200 | Elasticsearch | Information disclosure |

---

# What You'll Learn

This guide explains each common service from both defensive and offensive perspectives.

Every chapter includes:

- Purpose
- Default Ports
- Protocol
- Common Software
- Architecture
- Authentication
- Typical Enterprise Usage
- Nmap Detection
- NSE Scripts
- Banner Examples
- Enumeration Techniques
- Security Risks
- Blue Team Perspective
- Red Team Perspective
- Best Practices
- Summary

---

# Chapters

## Part I — Web Services

1. HTTP
2. HTTPS

---

## Part II — Remote Administration

3. SSH
4. Telnet
5. RDP
6. VNC
7. WinRM

---

## Part III — File Transfer & File Sharing

8. FTP
9. FTPS
10. SFTP
11. SMB
12. NFS
13. rsync

---

## Part IV — Core Network Infrastructure

14. DNS
15. DHCP
16. RPC

---

## Part V — Identity & Authentication

17. LDAP
18. Kerberos

---

## Part VI — Email Services

19. SMTP
20. POP3
21. IMAP

---

## Part VII — Voice over IP (VoIP)

22. SIP
23. RTP

---

## Part VIII — Database Services

24. MySQL
25. PostgreSQL
26. Microsoft SQL Server
27. Oracle Database
28. MongoDB
29. Redis
30. Elasticsearch

---

## Part IX — Containers & Orchestration

31. Docker Remote API
32. Kubernetes API Server

---

## Part X — Messaging & Streaming

33. MQTT
34. AMQP
35. Apache Kafka

---

## Part XI — Development Services

36. Git

---

## Part XII — Enterprise Infrastructure

37. VMware Services
38. Printing Services
39. VPN Technologies
40. PKI Services

---

## Part XIII — Security Platforms

41. SIEM Platforms
42. IDS / IPS

---

## Topics Covered

- Common Ports Reference
- Service Identification
- Banner Grabbing
- Version Detection
- NSE Script Selection
- Service Fingerprinting
- Common Misconfigurations
- Blue Team Checklist
- Red Team Checklist
- Enterprise Best Practices
- Quick Reference Tables

---

# Chapter 1 — HTTP (Hypertext Transfer Protocol)

## Overview

**HTTP (Hypertext Transfer Protocol)** is the foundation of the World Wide Web.

It defines how clients and servers exchange requests and responses over a network.

Nearly every web application, REST API, management interface, IoT dashboard, or cloud service communicates using HTTP or HTTPS.

Because of its widespread use, HTTP is one of the most important services that penetration testers and defenders must understand.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Hypertext Transfer Protocol |
| Default Port | TCP 80 |
| Protocol | TCP |
| Layer | Application Layer |
| RFC | RFC 9110 |
| Encryption | None |
| Stateful | No |
| Common Alternative | HTTPS (TCP 443) |

---

# Primary Purpose

HTTP allows a client to request resources from a web server.

Examples include:

- HTML pages
- Images
- CSS files
- JavaScript
- APIs
- JSON responses
- XML documents
- File downloads
- Web applications

---

# Communication Model

```text
Browser

    │

HTTP Request

    ▼

Web Server

    │

Application

    │

Database

    │

HTTP Response

    ▼

Browser
```

---

# Request Lifecycle

```text
Client

    │

TCP Connection

    ▼

HTTP Request

GET /index.html

    ▼

Web Server

    ▼

Application Logic

    ▼

Database

    ▼

HTTP Response

200 OK

HTML

JSON

Image

File
```

---

# HTTP Methods

| Method | Purpose | Safe | Idempotent |
|----------|----------|------|------------|
| GET | Retrieve data | Yes | Yes |
| POST | Create data | No | No |
| PUT | Replace resource | No | Yes |
| PATCH | Partial update | No | No |
| DELETE | Delete resource | No | Yes |
| HEAD | Retrieve headers only | Yes | Yes |
| OPTIONS | Supported methods | Yes | Yes |
| TRACE | Diagnostic | Yes | Yes |
| CONNECT | Proxy tunnel | No | No |

---

# Common HTTP Status Codes

## Informational

| Code | Meaning |
|------|---------|
|100|Continue|
|101|Switching Protocols|

---

## Success

| Code | Meaning |
|------|---------|
|200|OK|
|201|Created|
|202|Accepted|
|204|No Content|

---

## Redirection

| Code | Meaning |
|------|---------|
|301|Moved Permanently|
|302|Found|
|304|Not Modified|
|307|Temporary Redirect|
|308|Permanent Redirect|

---

## Client Errors

| Code | Meaning |
|------|---------|
|400|Bad Request|
|401|Unauthorized|
|403|Forbidden|
|404|Not Found|
|405|Method Not Allowed|
|408|Request Timeout|
|429|Too Many Requests|

---

## Server Errors

| Code | Meaning |
|------|---------|
|500|Internal Server Error|
|501|Not Implemented|
|502|Bad Gateway|
|503|Service Unavailable|
|504|Gateway Timeout|

---

# HTTP Request Example

```http
GET /login HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Accept: */*
Connection: close
```

---

# HTTP Response Example

```http
HTTP/1.1 200 OK

Server: nginx

Content-Type: text/html

Content-Length: 1543

<html>

...

</html>
```

---

# Common Web Servers

| Software | Platform |
|-----------|----------|
| Apache HTTP Server | Linux / Windows |
| Nginx | Linux |
| Microsoft IIS | Windows |
| LiteSpeed | Linux |
| Caddy | Linux |
| OpenLiteSpeed | Linux |
| Cherokee | Linux |

---

# Enterprise Usage

HTTP is commonly used for:

- Internal web applications
- REST APIs
- Administration panels
- Monitoring dashboards
- Intranet portals
- Documentation systems
- Ticket systems
- CI/CD dashboards
- Container management
- Cloud services

---

# Typical Architecture

```text
Internet

     │

Firewall

     │

Load Balancer

     │

Reverse Proxy

     │

Web Server

     │

Application

     │

Database
```

---

# HTTP Headers

Frequently encountered headers include:

| Header | Purpose |
|----------|----------|
| Host | Requested hostname |
| User-Agent | Client software |
| Accept | Accepted content |
| Cookie | Session information |
| Authorization | Credentials |
| Referer | Previous page |
| Origin | Request origin |
| Cache-Control | Cache behavior |
| Content-Type | Data type |
| Content-Length | Response size |
| Server | Server software |
| Location | Redirect destination |

---

# Nmap Detection

Basic Scan

```bash
nmap -p80 target
```

Version Detection

```bash
nmap -sV -p80 target
```

Default Scripts

```bash
nmap -sC -sV -p80 target
```

Aggressive Scan

```bash
nmap -A -p80 target
```

---

# Useful NSE Scripts

Discover HTTP Title

```bash
nmap --script http-title -p80 target
```

Enumerate Headers

```bash
nmap --script http-headers -p80 target
```

Detect Robots.txt

```bash
nmap --script http-robots.txt -p80 target
```

List HTTP Methods

```bash
nmap --script http-methods -p80 target
```

Retrieve Server Banner

```bash
nmap --script banner -p80 target
```

Enumerate Default Pages

```bash
nmap --script http-enum -p80 target
```

---

# Banner Examples

Apache

```text
Server: Apache/2.4.58
```

Nginx

```text
Server: nginx/1.27.0
```

Microsoft IIS

```text
Server: Microsoft-IIS/10.0
```

LiteSpeed

```text
Server: LiteSpeed
```

---

# Information That Can Be Collected

During reconnaissance, HTTP services may reveal:

- Server software
- Version number
- Framework
- Programming language
- Operating system hints
- Directory structure
- Login pages
- Admin panels
- APIs
- Cookies
- Security headers
- Session tokens
- Technologies in use

---

# Summary

HTTP is one of the most frequently encountered services during network reconnaissance and penetration testing. It powers web applications, APIs, dashboards, and countless enterprise services. Effective HTTP enumeration can reveal valuable information about server software, application frameworks, exposed endpoints, authentication mechanisms, and potential attack surfaces, making it a foundational skill for both offensive and defensive security professionals.

---

# Chapter 2 — HTTPS (Hypertext Transfer Protocol Secure)

## Overview

**HTTPS (Hypertext Transfer Protocol Secure)** is the encrypted version of HTTP.

Instead of sending data in plain text, HTTPS encrypts all communication using the **Transport Layer Security (TLS)** protocol.

Today, HTTPS is the standard communication protocol for almost every modern website, cloud service, API, banking application, and enterprise management portal.

For penetration testers, HTTPS often represents one of the largest attack surfaces because most enterprise applications are web-based.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Hypertext Transfer Protocol Secure |
| Default Port | TCP 443 |
| Transport | TCP |
| Encryption | TLS |
| Application Layer | Yes |
| RFC | RFC 2818 |
| Successor to SSL | TLS |

---

# Why HTTPS Exists

Traditional HTTP sends every packet in plaintext.

Anyone positioned between the client and server can potentially read:

- Usernames
- Passwords
- Cookies
- API Keys
- Session Tokens
- Sensitive Documents

HTTPS encrypts this communication.

---

# HTTP vs HTTPS

| HTTP | HTTPS |
|-------|--------|
| Plaintext | Encrypted |
| Port 80 | Port 443 |
| No Certificates | Uses X.509 Certificates |
| Easy Packet Inspection | Encrypted Traffic |
| No Identity Verification | Server Authentication |
| Vulnerable to MITM | Resistant to MITM |

---

# Typical Communication Flow

```text
Browser

     │

TCP 443

     ▼

TLS Handshake

     ▼

Certificate Validation

     ▼

Encrypted Tunnel

     ▼

HTTP Requests

     ▼

Web Server
```

---

# HTTPS Request Lifecycle

```text
Client

     │

TCP Connection

     ▼

TLS Handshake

     ▼

Certificate Exchange

     ▼

Key Negotiation

     ▼

Encrypted HTTP Request

     ▼

Web Server

     ▼

Encrypted Response
```

---

# TLS Handshake (Simplified)

```text
Client

    │

Client Hello

    ▼

Server Hello

    ▼

Certificate

    ▼

Key Exchange

    ▼

Session Keys Created

    ▼

Encrypted Communication
```

---

# TLS Provides

- Confidentiality
- Authentication
- Integrity
- Secure Key Exchange

---

# Common TLS Versions

| Version | Status |
|----------|--------|
| SSL 2.0 | Obsolete |
| SSL 3.0 | Obsolete |
| TLS 1.0 | Deprecated |
| TLS 1.1 | Deprecated |
| TLS 1.2 | Widely Supported |
| TLS 1.3 | Recommended |

---

# Common Certificate Fields

| Field | Description |
|---------|-------------|
| CN | Common Name |
| SAN | Subject Alternative Name |
| Issuer | Certificate Authority |
| Subject | Certificate Owner |
| Valid From | Start Date |
| Valid To | Expiration Date |
| Signature Algorithm | Signing Algorithm |
| Public Key | Server Public Key |

---

# Enterprise Usage

HTTPS protects:

- Banking systems
- E-commerce
- Cloud services
- VPN portals
- Web APIs
- Identity providers
- Corporate dashboards
- SIEM interfaces
- Kubernetes dashboards
- VMware management
- Git servers

---

# Common Web Servers

| Software | Operating System |
|-----------|------------------|
| Apache HTTPS | Linux / Windows |
| Nginx | Linux |
| Microsoft IIS | Windows |
| Caddy | Linux |
| LiteSpeed | Linux |
| HAProxy | Linux |
| Traefik | Linux |

---

# Typical Enterprise Architecture

```text
Internet

      │

Firewall

      │

Load Balancer

      │

WAF

      │

Reverse Proxy

      │

HTTPS Web Server

      │

Application

      │

Database
```

---

# Nmap Detection

Basic Scan

```bash
nmap -p443 target
```

Version Detection

```bash
nmap -sV -p443 target
```

Aggressive Scan

```bash
nmap -A -p443 target
```

SSL Detection

```bash
nmap -sV --script ssl-cert target
```

---

# Useful NSE Scripts

Retrieve Certificate

```bash
nmap --script ssl-cert -p443 target
```

Enumerate TLS Ciphers

```bash
nmap --script ssl-enum-ciphers -p443 target
```

Check Heartbleed

```bash
nmap --script ssl-heartbleed -p443 target
```

Check Known SSL Vulnerabilities

```bash
nmap --script ssl-known-key -p443 target
```

Enumerate HTTP Headers

```bash
nmap --script http-headers -p443 target
```

Retrieve Web Title

```bash
nmap --script http-title -p443 target
```

---

# Certificate Example

```text
Subject: CN=www.example.com

Issuer: DigiCert Global CA

Valid From:
2026-01-01

Valid Until:
2027-01-01

TLS Version:
TLS 1.3
```

---

# Common Findings During Enumeration

Penetration testers often discover:

- Expired certificates
- Self-signed certificates
- Weak cipher suites
- Deprecated TLS versions
- Missing HSTS
- Default web pages
- Exposed admin panels
- API documentation
- Login portals
- Misconfigured reverse proxies

---

# Blue Team Perspective

Recommendations

- Disable SSL and TLS 1.0/1.1.
- Enable TLS 1.3 where possible.
- Use certificates from trusted CAs.
- Rotate certificates before expiration.
- Enable HSTS.
- Disable weak cipher suites.
- Monitor certificate expiration.
- Keep web servers updated.

---

# Red Team Perspective

Interesting Targets

- Login portals
- VPN gateways
- Reverse proxies
- Web APIs
- Jenkins
- GitLab
- Grafana
- Kibana
- Kubernetes Dashboard
- VMware vCenter
- Admin panels

Useful Enumeration

```bash
nmap -sV \
--script ssl-cert,ssl-enum-ciphers,http-title,http-headers \
-p443 target
```

Information That May Be Revealed

- Certificate details
- Server software
- TLS version
- Cipher suites
- Supported HTTP methods
- Security headers
- Reverse proxy information
- Web technologies

---

# Security Risks

Common HTTPS weaknesses include:

- Expired certificates
- Weak cipher suites
- Legacy TLS support
- Certificate misconfiguration
- Self-signed certificates
- Sensitive information disclosure
- Improper redirect handling
- Missing security headers

---

# Best Practices

- Use TLS 1.3 whenever possible.
- Disable obsolete SSL/TLS versions.
- Implement HSTS.
- Enable OCSP Stapling.
- Use strong cipher suites.
- Rotate certificates automatically.
- Protect private keys.
- Perform regular TLS audits.

---

# Summary

HTTPS is the standard protocol for secure web communication. It combines HTTP with TLS to provide confidentiality, integrity, and authentication for modern web applications. During reconnaissance, HTTPS services often reveal valuable information through certificates, supported TLS versions, server headers, and application fingerprints. Proper TLS configuration and regular security assessments are essential to protect enterprise web infrastructure.

---

# Chapter 3 — SSH (Secure Shell)

## Overview

**SSH (Secure Shell)** is the industry standard protocol for secure remote administration of Linux, UNIX, network devices, cloud servers, and embedded systems.

It replaces insecure protocols such as **Telnet**, **rlogin**, and **rsh** by encrypting the entire communication session.

SSH is one of the first services investigated during penetration tests because it frequently provides administrative access to critical systems.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Secure Shell |
| Default Port | TCP 22 |
| Transport | TCP |
| Encryption | Yes |
| Authentication | Password / Public Key / Certificate |
| RFC | RFC 4251 |
| Application Layer | Yes |

---

# Primary Purpose

SSH provides secure remote access to systems.

Typical uses include:

- Remote administration
- File transfer (SCP)
- Secure file synchronization (SFTP)
- Port forwarding
- Remote command execution
- Secure tunneling
- Git operations
- Infrastructure automation

---

# Communication Model

```text
Administrator

      │

 SSH Connection

      ▼

SSH Server

      │

Authentication

      ▼

Secure Shell

      │

Operating System

      ▼

Resources
```

---

# SSH Authentication Methods

| Method | Description |
|----------|-------------|
| Password | Username and password authentication |
| Public Key | RSA, ECDSA, Ed25519 keys |
| Keyboard Interactive | PAM-based authentication |
| Certificate | SSH Certificates |
| Multi-Factor Authentication | Password + OTP or Hardware Token |

---

# Common SSH Implementations

| Software | Platform |
|-----------|----------|
| OpenSSH | Linux, BSD, macOS |
| Dropbear | Embedded Linux |
| Bitvise SSH Server | Windows |
| Tectia SSH | Enterprise |
| OpenSSH for Windows | Windows |

---

# Enterprise Usage

SSH is widely used for:

- Linux server administration
- Network switch management
- Router configuration
- Cloud infrastructure
- Kubernetes nodes
- Docker hosts
- Git servers
- Backup automation
- DevOps pipelines
- CI/CD systems

---

# Typical Architecture

```text
Administrator

      │

SSH Client

      ▼

Firewall

      ▼

SSH Server

      │

Linux

UNIX

Network Device

Cloud Instance
```

---

# SSH Session Flow

```text
TCP Connection

      │

Protocol Negotiation

      ▼

Key Exchange

      ▼

Server Authentication

      ▼

User Authentication

      ▼

Encrypted Session

      ▼

Remote Shell
```

---

# Common Encryption Algorithms

### Key Exchange

- Diffie-Hellman
- ECDH
- Curve25519

### Host Keys

- RSA
- ECDSA
- Ed25519

### Encryption

- AES-128
- AES-256
- ChaCha20-Poly1305

### Integrity

- HMAC-SHA2
- Poly1305

---

# Nmap Detection

Basic Scan

```bash
nmap -p22 target
```

Version Detection

```bash
nmap -sV -p22 target
```

Aggressive Scan

```bash
nmap -A -p22 target
```

OS Detection

```bash
nmap -O target
```

---

# Useful NSE Scripts

Retrieve Host Keys

```bash
nmap --script ssh-hostkey -p22 target
```

Supported Algorithms

```bash
nmap --script ssh2-enum-algos -p22 target
```

Brute Force (Authorized Testing Only)

```bash
nmap --script ssh-brute -p22 target
```

Retrieve Banner

```bash
nmap --script banner -p22 target
```

---

# Example Banner

```text
SSH-2.0-OpenSSH_9.8
```

Example

```text
SSH-2.0-dropbear_2025.87
```

---

# Information That Can Be Collected

SSH enumeration may reveal:

- SSH implementation
- Software version
- Supported algorithms
- Public host keys
- Authentication methods
- Operating system hints
- Weak cryptographic settings
- Legacy protocol support

---

# Blue Team Perspective

Recommendations

- Disable password authentication where possible.
- Use SSH keys instead of passwords.
- Enable MFA.
- Restrict root login.
- Disable SSH protocol version 1.
- Rotate host keys periodically.
- Limit administrator IP addresses.
- Enable logging and auditing.

---

# Red Team Perspective

Interesting Targets

- Linux servers
- Cloud instances
- Network appliances
- Hypervisors
- Backup servers
- Git servers
- NAS devices
- IoT systems

Useful Enumeration

```bash
nmap -sV \
--script ssh-hostkey,ssh2-enum-algos,banner \
-p22 target
```

Potential Findings

- Outdated OpenSSH versions
- Weak host keys
- Deprecated algorithms
- Password authentication enabled
- Root login permitted
- Vendor-specific SSH implementations

---

# Security Risks

Common SSH weaknesses include:

- Weak passwords
- Default credentials
- Outdated OpenSSH versions
- Root login enabled
- Password authentication enabled
- Weak cryptographic algorithms
- Poor key management
- Lack of MFA

---

# Best Practices

- Use Ed25519 or modern RSA keys.
- Disable password authentication when possible.
- Disable direct root login.
- Restrict SSH with firewalls.
- Enable Fail2Ban or similar protection.
- Keep OpenSSH updated.
- Audit SSH logs regularly.
- Rotate keys on a defined schedule.

---

# Real-World Examples

| Device | Typical SSH Usage |
|----------|------------------|
| Linux Server | Remote administration |
| Cisco Switch | CLI management |
| MikroTik Router | Configuration |
| VMware ESXi | Maintenance |
| Raspberry Pi | Remote access |
| Git Server | Repository management |
| NAS Appliance | Storage administration |
| AWS EC2 | Cloud administration |

---

# Summary

SSH is one of the most critical protocols in modern IT infrastructure. It enables secure remote administration, encrypted file transfers, and infrastructure automation across servers, cloud platforms, network devices, and development environments. During reconnaissance, SSH enumeration can reveal software versions, supported cryptographic algorithms, authentication methods, and potential security weaknesses. Proper hardening—including key-based authentication, multi-factor authentication, and regular updates—is essential to protect administrative access.

---

# Chapter 4 — FTP (File Transfer Protocol)

## Overview

**FTP (File Transfer Protocol)** is one of the oldest Internet protocols and was designed to transfer files between computers over a TCP/IP network.

Although it is still encountered in legacy environments, FTP is considered **insecure** because it transmits authentication credentials and data in plaintext.

Modern organizations typically replace FTP with **SFTP** or **FTPS**, but FTP remains common in embedded devices, legacy enterprise systems, industrial environments, and older file servers.

For penetration testers, FTP is often an excellent source of information disclosure due to anonymous access, weak credentials, or exposed files.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | File Transfer Protocol |
| Default Control Port | TCP 21 |
| Default Data Port | TCP 20 (Active Mode) |
| Transport | TCP |
| Encryption | No |
| RFC | RFC 959 |
| Application Layer | Yes |

---

# Primary Purpose

FTP allows users to:

- Upload files
- Download files
- Rename files
- Delete files
- Create directories
- Browse directories
- Synchronize data

---

# FTP Architecture

```text
FTP Client

      │

TCP 21 (Control)

      ▼

FTP Server

      │

Authentication

      │

File Operations

      ▼

Storage
```

Unlike many protocols, FTP commonly uses **two separate TCP connections**.

---

# FTP Communication Channels

| Channel | Default Port | Purpose |
|----------|--------------|----------|
| Control | TCP 21 | Commands and authentication |
| Data | TCP 20 (Active) | File transfer |

---

# FTP Modes

## Active Mode

```text
Client

     │
     │ TCP 21
     ▼

FTP Server

     │
     │ TCP 20
     ▼

Client Data Port
```

The server initiates the data connection.

---

## Passive Mode

```text
Client

     │
     │ TCP 21
     ▼

FTP Server

     │
     │ Random High Port
     ▼

Client Connects
```

Passive mode is the preferred option because it works better with NAT and firewalls.

---

# Common FTP Commands

| Command | Description |
|----------|-------------|
| USER | Specify username |
| PASS | Specify password |
| LIST | List directory contents |
| PWD | Print current directory |
| CWD | Change working directory |
| RETR | Download file |
| STOR | Upload file |
| DELE | Delete file |
| MKD | Create directory |
| RMD | Remove directory |
| QUIT | Close session |

---

# Common FTP Servers

| Software | Platform |
|-----------|----------|
| vsftpd | Linux |
| ProFTPD | Linux |
| Pure-FTPd | Linux |
| FileZilla Server | Windows |
| Microsoft IIS FTP | Windows |
| Gene6 FTP Server | Windows |

---

# Enterprise Usage

FTP may still be found in:

- Legacy applications
- Manufacturing systems
- Embedded devices
- Network appliances
- Firmware repositories
- Backup servers
- File distribution systems
- Laboratory equipment

---

# Anonymous FTP

Many FTP servers allow anonymous access.

Example login:

```text
Username: anonymous

Password: anonymous@example.com
```

Anonymous access may expose:

- Public downloads
- Software packages
- Documentation
- Configuration files
- Backup archives

Poorly configured servers may unintentionally expose sensitive data.

---

# Nmap Detection

Basic Scan

```bash
nmap -p21 target
```

Version Detection

```bash
nmap -sV -p21 target
```

Aggressive Scan

```bash
nmap -A -p21 target
```

Default Scripts

```bash
nmap -sC -sV -p21 target
```

---

# Useful NSE Scripts

Anonymous Login Check

```bash
nmap --script ftp-anon -p21 target
```

FTP Banner

```bash
nmap --script banner -p21 target
```

FTP Commands

```bash
nmap --script ftp-syst -p21 target
```

FTP Bounce Detection

```bash
nmap --script ftp-bounce -p21 target
```

Brute Force (Authorized Testing Only)

```bash
nmap --script ftp-brute -p21 target
```

---

# Example Banner

```text
220 (vsFTPd 3.0.5)
```

Example

```text
220 Microsoft FTP Service
```

---

# Information That Can Be Collected

FTP enumeration may reveal:

- Server software
- Version number
- Anonymous access
- Writable directories
- File listings
- Backup archives
- Configuration files
- Firmware images
- Usernames
- Operating system information

---

# Blue Team Perspective

Recommendations

- Disable anonymous FTP unless absolutely necessary.
- Replace FTP with SFTP or FTPS.
- Restrict access using firewalls.
- Enable detailed logging.
- Use strong authentication.
- Remove obsolete FTP services.
- Limit write permissions.
- Regularly review shared directories.

---

# Red Team Perspective

Interesting Targets

- Anonymous file shares
- Backup archives
- Database exports
- Configuration files
- Firmware images
- Software repositories
- User home directories
- Legacy file servers

Useful Enumeration

```bash
nmap -sV \
--script ftp-anon,ftp-syst,banner \
-p21 target
```

Potential Findings

- Anonymous login enabled
- Weak credentials
- Writable directories
- Sensitive documents
- Backup files
- Database dumps
- Legacy applications

---

# Security Risks

Common FTP weaknesses include:

- Plaintext credentials
- Anonymous access
- Weak passwords
- Writable directories
- File disclosure
- FTP Bounce attacks
- Lack of encryption
- Legacy software vulnerabilities

---

# Best Practices

- Migrate to SFTP or FTPS.
- Disable anonymous access.
- Enforce strong passwords.
- Restrict directory permissions.
- Encrypt sensitive transfers.
- Patch FTP server software.
- Monitor authentication logs.
- Remove unused FTP services.

---

# Real-World Examples

| Device | Typical FTP Usage |
|----------|------------------|
| NAS Appliance | File sharing |
| Printer | Firmware updates |
| Router | Configuration backup |
| Industrial Controller | Firmware distribution |
| Legacy Windows Server | File repository |
| Linux Server | Software distribution |
| Embedded Device | Maintenance |

---

# Summary

FTP remains one of the most frequently discovered legacy services during internal and external network assessments. While it provides reliable file transfer capabilities, its lack of native encryption makes it unsuitable for modern secure environments. During reconnaissance, FTP servers often expose valuable information such as anonymous file shares, software versions, backup archives, and configuration files. Security teams should migrate to encrypted alternatives such as **SFTP** or **FTPS**, restrict access to trusted users, and continuously monitor FTP activity for unauthorized access.

---

# Chapter 5 — FTPS (FTP Secure)

## Overview

**FTPS (FTP Secure)** is an extension of the traditional **File Transfer Protocol (FTP)** that adds **SSL/TLS encryption** to protect authentication credentials and file transfers.

Unlike standard FTP, FTPS encrypts the communication channel, significantly reducing the risk of credential theft and data interception.

Many enterprises continue to use FTPS because it integrates easily with existing FTP infrastructure while providing secure communications.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | File Transfer Protocol Secure |
| Default Control Port | TCP 990 (Implicit FTPS) |
| Alternative | TCP 21 (Explicit FTPS) |
| Transport | TCP |
| Encryption | TLS |
| Authentication | Username / Password / Certificate |
| Application Layer | Yes |

---

# FTP vs FTPS

| FTP | FTPS |
|------|-------|
| Plaintext | Encrypted |
| No Certificate | X.509 Certificate |
| Port 21 | Port 990 or Explicit TLS |
| Weak Security | Stronger Security |
| Credentials Visible | Credentials Encrypted |

---

# Explicit vs Implicit FTPS

## Explicit FTPS

The connection starts as standard FTP and is upgraded to TLS using the **AUTH TLS** command.

```text
Client

    │

TCP 21

    ▼

FTP Server

    │

AUTH TLS

    ▼

Encrypted Session
```

---

## Implicit FTPS

Encryption begins immediately after the TCP connection is established.

```text
Client

    │

TCP 990

    ▼

TLS Handshake

    ▼

Encrypted FTP Session
```

---

# Communication Workflow

```text
Client

     │

TCP Connection

     ▼

TLS Handshake

     ▼

Certificate Validation

     ▼

User Authentication

     ▼

Encrypted File Transfer
```

---

# Common FTPS Servers

| Software | Platform |
|-----------|----------|
| FileZilla Server | Windows |
| ProFTPD | Linux |
| vsftpd | Linux |
| Microsoft IIS FTP | Windows |
| Cerberus FTP Server | Windows |
| Titan FTP | Windows |

---

# Enterprise Usage

FTPS is commonly deployed for:

- Financial institutions
- Healthcare systems
- Government agencies
- Secure document exchange
- Software distribution
- Enterprise backup
- Partner file exchange
- Regulatory compliance

---

# Authentication

Most FTPS servers support:

- Username and password
- Active Directory integration
- LDAP authentication
- Client certificates
- Multi-factor authentication

---

# Typical Architecture

```text
Business Partner

        │

Encrypted FTPS

        ▼

Firewall

        ▼

FTPS Gateway

        ▼

Internal File Server

        ▼

Storage
```

---

# Nmap Detection

Basic Scan

```bash
nmap -p990 target
```

Version Detection

```bash
nmap -sV -p990 target
```

Default Script Scan

```bash
nmap -sC -sV -p990 target
```

Aggressive Scan

```bash
nmap -A -p990 target
```

---

# Useful NSE Scripts

Retrieve TLS Certificate

```bash
nmap --script ssl-cert -p990 target
```

Enumerate TLS Ciphers

```bash
nmap --script ssl-enum-ciphers -p990 target
```

FTP System Information

```bash
nmap --script ftp-syst -p990 target
```

Retrieve Banner

```bash
nmap --script banner -p990 target
```

---

# Example Banner

```text
220 FileZilla Server 1.9 Ready
```

Example TLS Information

```text
TLS Version:
TLS 1.3

Certificate:
Let's Encrypt
```

---

# Information That Can Be Collected

During enumeration, testers may identify:

- FTP software
- Software version
- TLS version
- Supported cipher suites
- Certificate details
- Authentication methods
- Banner information
- Passive mode configuration
- File permissions

---

# Blue Team Perspective

Recommendations

- Require TLS for every connection.
- Disable legacy SSL protocols.
- Use trusted certificates.
- Rotate certificates before expiration.
- Disable anonymous access.
- Restrict upload directories.
- Monitor file transfer activity.
- Enable audit logging.

---

# Red Team Perspective

Interesting Targets

- Secure file servers
- Document exchange portals
- Financial systems
- Backup repositories
- Government infrastructure
- Enterprise storage

Useful Enumeration

```bash
nmap -sV \
--script ssl-cert,ssl-enum-ciphers,ftp-syst,banner \
-p990 target
```

Potential Findings

- Expired certificates
- Weak TLS configuration
- Outdated FTP software
- Misconfigured permissions
- Information disclosure
- Anonymous access (rare but possible)

---

# Security Risks

Although FTPS is considerably safer than FTP, risks still include:

- Expired certificates
- Weak cipher suites
- TLS downgrade attacks
- Poor certificate management
- Weak authentication
- Excessive user permissions
- Misconfigured passive ports

---

# Best Practices

- Prefer TLS 1.2 or TLS 1.3.
- Disable SSL and deprecated TLS versions.
- Enforce strong password policies.
- Enable multi-factor authentication.
- Monitor certificate validity.
- Restrict network access.
- Regularly review permissions.
- Log all administrative actions.

---

# Real-World Examples

| Organization | Typical FTPS Usage |
|--------------|-------------------|
| Bank | Secure financial document transfer |
| Hospital | Patient record exchange |
| Government Agency | Confidential document delivery |
| Insurance Company | Claims processing |
| Software Vendor | Customer software downloads |
| Enterprise | Secure partner file exchange |

---

# Summary

FTPS extends the traditional FTP protocol by adding TLS encryption, providing confidentiality and integrity for file transfers. It is commonly found in organizations that require secure document exchange while maintaining compatibility with existing FTP workflows. During reconnaissance, FTPS enumeration can reveal certificate details, supported TLS versions, server software, and configuration weaknesses. Proper certificate management, modern TLS configurations, and strong authentication are essential for maintaining a secure FTPS environment.

---

# Chapter 6 — SFTP (SSH File Transfer Protocol)

## Overview

**SFTP (SSH File Transfer Protocol)** is a secure file transfer protocol that operates over the **SSH (Secure Shell)** protocol.

Despite its name, SFTP is **not an extension of FTP**.

Instead, it is an entirely different protocol that uses a single encrypted SSH connection for authentication, file management, and data transfer.

Because it leverages SSH, SFTP has become one of the most widely deployed secure file transfer solutions in Linux, UNIX, cloud, and enterprise environments.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | SSH File Transfer Protocol |
| Default Port | TCP 22 |
| Underlying Protocol | SSH |
| Transport | TCP |
| Encryption | Yes |
| Authentication | Password, Public Key, Certificate |
| Application Layer | Yes |

---

# SFTP vs FTP vs FTPS

| Feature | FTP | FTPS | SFTP |
|----------|-----|-------|------|
| Encryption | No | TLS | SSH |
| Default Port | 21 | 990 / 21 | 22 |
| Multiple Connections | Yes | Yes | No |
| Uses SSH | No | No | Yes |
| Certificate Required | No | Yes | No |
| Recommended | No | Yes | Yes |

---

# Primary Purpose

SFTP allows users to securely:

- Upload files
- Download files
- Rename files
- Delete files
- Create directories
- Remove directories
- Synchronize files
- Manage permissions

All communication is encrypted.

---

# Communication Model

```text
SFTP Client

      │

 SSH Connection

      ▼

SSH Server

      │

SFTP Subsystem

      ▼

Filesystem

      ▼

Storage
```

---

# Connection Workflow

```text
Client

    │

TCP 22

    ▼

SSH Handshake

    ▼

Key Exchange

    ▼

User Authentication

    ▼

Encrypted Session

    ▼

SFTP Operations
```

---

# Authentication Methods

Most SFTP servers support:

- Username and password
- SSH Public Keys
- Ed25519 Keys
- RSA Keys
- ECDSA Keys
- SSH Certificates
- Multi-Factor Authentication

---

# Common Implementations

| Software | Platform |
|-----------|----------|
| OpenSSH | Linux |
| Bitvise SSH Server | Windows |
| Rebex SFTP Server | Windows |
| Tectia SSH | Enterprise |
| OpenSSH for Windows | Windows |

---

# Enterprise Usage

SFTP is commonly used for:

- Secure backups
- Financial transactions
- Healthcare records
- Cloud automation
- CI/CD pipelines
- DevOps deployments
- Software distribution
- Enterprise file exchange
- Log collection

---

# Typical Architecture

```text
Business Partner

       │

Encrypted SSH

       ▼

Firewall

       ▼

SFTP Server

       │

Filesystem

       ▼

Storage
```

---

# Advantages

Compared to FTP and FTPS:

- Single TCP connection
- Strong encryption
- SSH authentication
- Easy firewall traversal
- Secure tunneling
- Better automation support

---

# Nmap Detection

Basic Scan

```bash
nmap -p22 target
```

Version Detection

```bash
nmap -sV -p22 target
```

Default Script Scan

```bash
nmap -sC -sV -p22 target
```

Aggressive Scan

```bash
nmap -A -p22 target
```

---

# Useful NSE Scripts

Retrieve Host Key

```bash
nmap --script ssh-hostkey -p22 target
```

Enumerate SSH Algorithms

```bash
nmap --script ssh2-enum-algos -p22 target
```

Retrieve Banner

```bash
nmap --script banner -p22 target
```

SSH Brute Force (Authorized Testing Only)

```bash
nmap --script ssh-brute -p22 target
```

---

# Example Banner

```text
SSH-2.0-OpenSSH_9.8
```

Example Host Key

```text
2048-bit RSA

256-bit ECDSA

256-bit Ed25519
```

---

# Information That Can Be Collected

Enumeration may reveal:

- SSH implementation
- SSH version
- Supported algorithms
- Host keys
- Authentication methods
- Operating system hints
- Vendor information
- Weak cryptographic algorithms

---

# Blue Team Perspective

Recommendations

- Prefer public key authentication.
- Disable password authentication where possible.
- Restrict user access.
- Disable direct root login.
- Enable multi-factor authentication.
- Keep OpenSSH updated.
- Monitor authentication logs.
- Rotate host keys periodically.

---

# Red Team Perspective

Interesting Targets

- Linux servers
- Backup servers
- NAS devices
- Cloud instances
- Git servers
- Development servers
- File repositories
- Automation platforms

Useful Enumeration

```bash
nmap -sV \
--script ssh-hostkey,ssh2-enum-algos,banner \
-p22 target
```

Potential Findings

- Weak host keys
- Password authentication enabled
- Outdated OpenSSH versions
- Legacy cryptographic algorithms
- Vendor-specific SSH implementations

---

# Security Risks

Although SFTP is highly secure, common weaknesses include:

- Weak passwords
- Poor SSH key management
- Password authentication enabled
- Root login enabled
- Outdated SSH software
- Weak encryption algorithms
- Shared administrator accounts

---

# Best Practices

- Use Ed25519 keys whenever possible.
- Disable SSH password authentication.
- Enforce least privilege.
- Rotate SSH keys regularly.
- Enable MFA.
- Restrict access by firewall.
- Monitor login attempts.
- Remove unused accounts.

---

# Real-World Examples

| Organization | Typical SFTP Usage |
|--------------|-------------------|
| Bank | Secure financial file exchange |
| Hospital | Medical record transfers |
| Cloud Provider | Automated deployments |
| Software Company | Artifact distribution |
| Government Agency | Confidential document exchange |
| Enterprise | Backup synchronization |

---

# Comparison with SCP

| Feature | SCP | SFTP |
|----------|-----|------|
| Uses SSH | Yes | Yes |
| Interactive File Management | No | Yes |
| Resume Transfers | Limited | Yes |
| Directory Browsing | No | Yes |
| Modern Recommendation | Legacy | Recommended |

---

# Summary

SFTP is the preferred protocol for secure file transfers in modern enterprise environments. By leveraging SSH, it provides encrypted communication, strong authentication, and simplified firewall traversal without relying on multiple TCP connections. During reconnaissance, SFTP services can reveal SSH versions, supported cryptographic algorithms, and authentication methods. Proper SSH hardening—including key-based authentication, modern encryption algorithms, and multi-factor authentication—ensures that SFTP remains one of the safest methods for transferring sensitive data.

---

# Chapter 7 — SMB (Server Message Block)

## Overview

**Server Message Block (SMB)** is a network protocol that enables systems to share files, printers, named pipes, and other resources over a network.

Originally developed by IBM and later expanded by Microsoft, SMB is one of the most commonly encountered protocols in Windows environments.

SMB is heavily used in:

- Microsoft Active Directory
- Windows File Servers
- Network Attached Storage (NAS)
- Domain Controllers
- Enterprise Workstations
- Print Servers

For penetration testers, SMB is one of the highest-value services because it frequently exposes usernames, shared folders, domain information, operating system details, and occasionally sensitive files.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Server Message Block |
| Default Port | TCP 445 |
| Legacy Port | TCP 139 (NetBIOS Session Service) |
| Transport | TCP |
| Encryption | SMB 3.x Supports Encryption |
| Application Layer | Yes |
| Primary Platform | Microsoft Windows |

---

# Primary Purpose

SMB provides shared access to:

- Files
- Directories
- Printers
- Named Pipes
- Network Drives
- IPC Communication

---

# SMB Architecture

```text
Client

     │

 SMB Request

     ▼

SMB Server

     │

Authentication

     │

Filesystem

     ▼

Shared Resources
```

---

# SMB Communication Workflow

```text
Client

     │

TCP 445

     ▼

SMB Negotiation

     ▼

Authentication

     ▼

Tree Connect

     ▼

File Operations

     ▼

Shared Folder
```

---

# SMB Versions

| Version | Status |
|----------|--------|
| SMB 1.0 | Obsolete (Insecure) |
| SMB 2.0 | Supported |
| SMB 2.1 | Supported |
| SMB 3.0 | Recommended |
| SMB 3.1.1 | Current Standard |

---

# Authentication Methods

SMB commonly supports:

- Local Windows Accounts
- Active Directory Accounts
- NTLM
- Kerberos
- Guest Access
- Anonymous Sessions (Rare)

---

# Common SMB Shares

| Share | Purpose |
|--------|----------|
| C$ | Administrative Share |
| ADMIN$ | Windows Administration |
| IPC$ | Interprocess Communication |
| NETLOGON | Domain Logon Scripts |
| SYSVOL | Group Policy Distribution |
| Users | User Data |
| Public | Shared Documents |

---

# Enterprise Usage

SMB is used for:

- File Servers
- Domain Controllers
- Network Storage
- Printer Sharing
- Windows Administration
- Backup Systems
- User Profiles
- Software Distribution
- Group Policy

---

# Typical Enterprise Architecture

```text
Employees

      │

SMB Client

      ▼

Windows File Server

      │

Active Directory

      ▼

Shared Storage
```

---

# Common SMB Servers

| Software | Platform |
|-----------|----------|
| Microsoft Windows Server | Windows |
| Samba | Linux |
| TrueNAS | BSD |
| Synology DSM | NAS |
| QNAP QTS | NAS |

---

# Nmap Detection

Basic Scan

```bash
nmap -p445 target
```

Version Detection

```bash
nmap -sV -p445 target
```

Default Scripts

```bash
nmap -sC -sV -p445 target
```

Aggressive Scan

```bash
nmap -A -p445 target
```

---

# Useful NSE Scripts

SMB Operating System Discovery

```bash
nmap --script smb-os-discovery -p445 target
```

List SMB Shares

```bash
nmap --script smb-enum-shares -p445 target
```

Enumerate SMB Users

```bash
nmap --script smb-enum-users -p445 target
```

Enumerate Security Mode

```bash
nmap --script smb-security-mode -p445 target
```

SMB Protocol Versions

```bash
nmap --script smb-protocols -p445 target
```

Vulnerability Detection

```bash
nmap --script smb-vuln* -p445 target
```

---

# Example Banner

```text
Microsoft Windows Server 2022
```

Example SMB Version

```text
SMB 3.1.1
```

---

# Information That Can Be Collected

SMB enumeration can reveal:

- Computer name
- Domain name
- Windows version
- SMB version
- Shared folders
- Logged-in users
- Domain SID
- Workgroup
- Printer shares
- Anonymous access
- Security settings

---

# Common Security Risks

Frequently observed SMB weaknesses include:

- SMBv1 enabled
- EternalBlue exposure
- Anonymous shares
- Weak NTLM authentication
- Guest access enabled
- Excessive share permissions
- Sensitive file exposure
- Pass-the-Hash attacks

---

# Blue Team Perspective

Recommendations

- Disable SMBv1.
- Require SMB signing where appropriate.
- Enable SMB encryption.
- Remove unnecessary shares.
- Restrict anonymous access.
- Apply Microsoft security updates.
- Monitor failed authentication attempts.
- Review share permissions regularly.

---

# Red Team Perspective

Interesting Targets

- Domain Controllers
- File Servers
- NAS Appliances
- Backup Servers
- Print Servers
- Workstations
- Administrative Shares
- SYSVOL
- NETLOGON

Useful Enumeration

```bash
nmap -sV \
--script smb-os-discovery,smb-enum-shares,smb-security-mode,smb-protocols \
-p445 target
```

Potential Findings

- Active Directory domain
- Windows build version
- Shared folders
- Anonymous access
- Domain information
- Backup files
- Login scripts
- Weak security settings

---

# Related Attacks

Historically significant attacks involving SMB include:

- EternalBlue (MS17-010)
- Pass-the-Hash
- NTLM Relay
- SMB Relay
- Anonymous Enumeration
- Lateral Movement
- Credential Harvesting

---

# Best Practices

- Disable SMBv1 permanently.
- Use SMB 3.1.1 whenever possible.
- Enable SMB encryption.
- Require Kerberos authentication.
- Restrict administrative shares.
- Enable detailed auditing.
- Implement network segmentation.
- Regularly audit shared folders.

---

# Real-World Examples

| Environment | SMB Usage |
|-------------|-----------|
| Active Directory | SYSVOL & NETLOGON |
| Corporate File Server | Department Shares |
| NAS Device | Shared Storage |
| Print Server | Printer Sharing |
| Backup Server | Backup Repository |
| Windows Workstation | Administrative Shares |

---

# Summary

SMB is one of the most valuable protocols encountered during enterprise security assessments. It enables file sharing, printer access, authentication, and administrative communication across Windows networks. Proper SMB enumeration can reveal operating system information, domain membership, available shares, authentication methods, and potential vulnerabilities. Because SMB is frequently targeted by attackers for lateral movement and privilege escalation, organizations should disable legacy protocols such as SMBv1, enforce modern authentication mechanisms, and continuously monitor SMB activity.

---

# Chapter 8 — DNS (Domain Name System)

## Overview

The **Domain Name System (DNS)** is one of the most critical services on the Internet and in enterprise networks.

DNS translates **human-readable domain names** into **IP addresses**, allowing users to access resources without remembering numerical addresses.

Without DNS, users would need to manually remember IP addresses for every website and service.

Because nearly every network application depends on DNS, it is one of the first services analyzed during reconnaissance and security assessments.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Domain Name System |
| Default Port | UDP 53 |
| Alternative Port | TCP 53 |
| Transport | UDP / TCP |
| Encryption | None (Traditional DNS) |
| Layer | Application Layer |
| RFC | RFC 1034 / RFC 1035 |

---

# Primary Purpose

DNS is responsible for:

- Name resolution
- Reverse lookups
- Mail server discovery
- Service discovery
- Load balancing
- Domain delegation
- Zone transfers

---

# DNS Resolution Process

```text
User

   │

www.example.com

   ▼

Local DNS Resolver

   │

Recursive Query

   ▼

Root DNS Server

   │

TLD Server (.com)

   ▼

Authoritative DNS

   │

IP Address

   ▼

Web Server
```

---

# DNS Hierarchy

```text
                .

                │

     Root Name Servers

                │

        Top-Level Domains

       (.com .org .net)

                │

      example.com

                │

Subdomains

www

mail

api

vpn
```

---

# Common DNS Record Types

| Record | Purpose |
|----------|----------|
| A | IPv4 Address |
| AAAA | IPv6 Address |
| CNAME | Alias |
| MX | Mail Server |
| NS | Name Server |
| TXT | Text Information |
| PTR | Reverse Lookup |
| SOA | Start of Authority |
| SRV | Service Discovery |
| CAA | Certificate Authority Authorization |

---

# Forward Lookup

```text
example.com

      │

DNS Query

      ▼

93.184.216.34
```

---

# Reverse Lookup

```text
93.184.216.34

      │

PTR Query

      ▼

example.com
```

---

# Recursive vs Iterative Queries

| Recursive | Iterative |
|------------|-----------|
| Resolver performs all lookups | Client performs additional lookups |
| Common for clients | Common between DNS servers |
| Simpler for users | More efficient for infrastructure |

---

# Enterprise Usage

DNS supports:

- Active Directory
- Email routing
- Cloud services
- VPN gateways
- Load balancers
- Kubernetes
- Service discovery
- Internal applications
- Microservices

---

# Typical Enterprise Architecture

```text
Client

   │

DNS Resolver

   ▼

Internal DNS

   │

Forwarder

   ▼

Internet DNS

   │

Authoritative Server

   ▼

Requested Service
```

---

# Common DNS Servers

| Software | Platform |
|-----------|----------|
| BIND | Linux |
| Microsoft DNS | Windows |
| PowerDNS | Linux |
| Unbound | Linux |
| CoreDNS | Kubernetes |
| Knot DNS | Linux |

---

# Nmap Detection

Basic Scan

```bash
nmap -p53 target
```

Version Detection

```bash
nmap -sV -p53 target
```

UDP Scan

```bash
nmap -sU -p53 target
```

Aggressive Scan

```bash
nmap -A -p53 target
```

---

# Useful NSE Scripts

Retrieve DNS Version

```bash
nmap --script dns-nsid -p53 target
```

Check Recursion

```bash
nmap --script dns-recursion -p53 target
```

Brute Force Subdomains

```bash
nmap --script dns-brute target
```

DNS Cache Snooping

```bash
nmap --script dns-cache-snoop target
```

---

# Example Responses

A Record

```text
example.com

93.184.216.34
```

MX Record

```text
mail.example.com
```

NS Record

```text
ns1.example.com

ns2.example.com
```

---

# Information That Can Be Collected

DNS enumeration may reveal:

- Domain names
- Internal subdomains
- Mail servers
- VPN gateways
- Cloud services
- Internal infrastructure
- Name servers
- Service records
- Technology stack
- Public IP addresses

---

# Zone Transfer (AXFR)

One of the most valuable DNS misconfigurations is an unrestricted **zone transfer**.

If allowed, it may disclose:

- Internal hosts
- Development systems
- Mail servers
- VPN endpoints
- Database servers
- Backup servers
- Network topology

Example:

```bash
dig axfr example.com @ns1.example.com
```

A properly configured DNS server should refuse unauthorized zone transfer requests.

---

# Blue Team Perspective

Recommendations

- Disable public zone transfers.
- Restrict recursive queries.
- Enable DNSSEC where appropriate.
- Monitor unusual DNS traffic.
- Separate internal and external DNS.
- Remove obsolete DNS records.
- Keep DNS software updated.
- Log DNS queries for security analysis.

---

# Red Team Perspective

Interesting Targets

- Domain Controllers
- Internal DNS servers
- Public authoritative servers
- VPN hostnames
- Exchange servers
- Cloud endpoints
- Kubernetes services
- Development environments

Useful Enumeration

```bash
nmap -sU -sV \
--script dns-brute,dns-recursion,dns-nsid \
-p53 target
```

Potential Findings

- Internal hostnames
- Recursive DNS enabled
- DNS version disclosure
- Public zone transfer
- Mail infrastructure
- Hidden subdomains
- Cloud resources

---

# Common Security Risks

Frequently observed DNS weaknesses include:

- Open recursion
- Zone transfer enabled
- DNS cache poisoning
- DNS spoofing
- Outdated DNS software
- Information disclosure
- Weak DNSSEC implementation
- DNS amplification attacks

---

# Best Practices

- Disable unauthorized AXFR.
- Restrict recursive queries.
- Deploy DNSSEC where practical.
- Monitor DNS logs.
- Separate internal and external DNS infrastructure.
- Patch DNS servers regularly.
- Limit version disclosure.
- Protect authoritative name servers.

---

# Real-World Examples

| Environment | DNS Usage |
|--------------|-----------|
| Active Directory | Domain Name Resolution |
| Kubernetes | Service Discovery |
| Microsoft Exchange | Mail Routing |
| Cloud Platform | Public DNS Records |
| Enterprise VPN | Gateway Resolution |
| Load Balancer | Application Distribution |

---

# Summary

DNS is a foundational network service that enables communication between users and Internet resources by translating domain names into IP addresses. It also supports email delivery, service discovery, cloud infrastructure, and Active Directory environments. During reconnaissance, DNS can reveal valuable information about an organization's infrastructure, including subdomains, mail servers, VPN gateways, and internal naming conventions. Proper DNS hardening—including restricting zone transfers, disabling unnecessary recursion, implementing DNSSEC, and monitoring DNS activity—is essential for maintaining a secure network.

---

# Chapter 9 — DHCP (Dynamic Host Configuration Protocol)

## Overview

**Dynamic Host Configuration Protocol (DHCP)** is a network management protocol that automatically assigns IP configuration information to devices connected to a network.

Without DHCP, administrators would have to manually configure every client with an IP address, subnet mask, default gateway, DNS servers, and other network settings.

DHCP greatly simplifies network administration and is found in virtually every enterprise, home, and cloud network.

During penetration testing, DHCP services may reveal network architecture, available IP ranges, gateway information, DNS servers, and sometimes unauthorized DHCP servers.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Dynamic Host Configuration Protocol |
| Default Server Port | UDP 67 |
| Default Client Port | UDP 68 |
| Transport | UDP |
| Encryption | No |
| RFC | RFC 2131 |
| Application Layer | Yes |

---

# Primary Purpose

DHCP automatically provides:

- IP Address
- Subnet Mask
- Default Gateway
- DNS Servers
- Domain Name
- Lease Time
- NTP Servers
- Additional Network Options

---

# DHCP Communication Workflow

```text
Client

   │

DHCPDISCOVER

   ▼

DHCP Server

   │

DHCPOFFER

   ▼

Client

   │

DHCPREQUEST

   ▼

DHCP Server

   │

DHCPACK

   ▼

Client Configured
```

This process is commonly known as the **DORA** process:

- Discover
- Offer
- Request
- Acknowledge

---

# DHCP Lease Process

```text
Device Boots

      │

Broadcast Discover

      ▼

Server Offers Address

      ▼

Client Requests Address

      ▼

Server Confirms Lease

      ▼

Device Joins Network
```

---

# Information Assigned by DHCP

| Configuration | Example |
|---------------|----------|
| IP Address | 192.168.1.50 |
| Subnet Mask | 255.255.255.0 |
| Gateway | 192.168.1.1 |
| DNS Server | 8.8.8.8 |
| Lease Time | 24 Hours |
| Domain Name | corp.local |

---

# Common DHCP Servers

| Software | Platform |
|-----------|----------|
| Windows DHCP Server | Windows Server |
| ISC DHCP Server | Linux |
| Kea DHCP | Linux |
| dnsmasq | Linux |
| MikroTik RouterOS | Router |
| Cisco IOS | Network Devices |
| pfSense | Firewall |

---

# Enterprise Usage

DHCP is commonly deployed in:

- Enterprise LANs
- Wireless Networks
- Branch Offices
- Universities
- Data Centers
- Cloud Environments
- Guest Networks
- Industrial Networks

---

# Typical Architecture

```text
DHCP Client

      │

Broadcast

      ▼

Switch

      │

DHCP Relay (Optional)

      ▼

DHCP Server

      │

IP Pool

      ▼

Network Configuration
```

---

# DHCP Relay Agent

Large enterprise networks often use **DHCP Relay Agents** to forward DHCP requests between different network segments.

```text
Client

    │

Broadcast

    ▼

Router (DHCP Relay)

    │

Forward

    ▼

Central DHCP Server
```

This enables centralized IP address management across multiple subnets.

---

# Nmap Detection

Basic UDP Scan

```bash
nmap -sU -p67 target
```

Version Detection

```bash
nmap -sU -sV -p67 target
```

Aggressive Scan

```bash
nmap -sU -A -p67 target
```

---

# Useful NSE Scripts

Broadcast DHCP Discovery

```bash
nmap --script broadcast-dhcp-discover
```

General Broadcast Discovery

```bash
nmap --script broadcast*
```

---

# Example DHCP Discovery Output

```text
Server Identifier:
192.168.1.1

Offered IP:
192.168.1.120

Subnet Mask:
255.255.255.0

Router:
192.168.1.1

DNS:
192.168.1.10
```

---

# Information That Can Be Collected

DHCP enumeration may reveal:

- DHCP server IP
- Gateway address
- DNS servers
- IP address range
- Lease duration
- Domain name
- Network topology
- DHCP options
- Vendor-specific options

---

# Blue Team Perspective

Recommendations

- Enable DHCP Snooping on managed switches.
- Authorize only trusted DHCP servers.
- Monitor lease activity.
- Segment guest networks.
- Restrict administrative access.
- Backup DHCP configurations.
- Audit DHCP logs regularly.
- Reserve critical IP addresses for infrastructure.

---

# Red Team Perspective

Interesting Targets

- Corporate DHCP Servers
- Guest Networks
- Wireless Networks
- Branch Offices
- Network Appliances
- Virtual Infrastructure
- Data Centers

Useful Enumeration

```bash
nmap --script broadcast-dhcp-discover
```

Potential Findings

- Internal addressing scheme
- Default gateway
- DNS infrastructure
- Internal domain name
- Network segmentation
- Rogue DHCP servers

---

# Common Security Risks

Frequently observed DHCP weaknesses include:

- Rogue DHCP servers
- DHCP starvation attacks
- Lack of DHCP Snooping
- Unauthorized network devices
- Weak network segmentation
- Information disclosure
- Poor lease management

---

# DHCP Security Features

Modern enterprise networks often implement:

- DHCP Snooping
- IP Source Guard
- Dynamic ARP Inspection (DAI)
- Port Security
- Network Access Control (NAC)
- 802.1X Authentication

These technologies work together to reduce the risk of rogue devices and network spoofing attacks.

---

# Best Practices

- Enable DHCP Snooping on access switches.
- Use authorized DHCP servers only.
- Monitor DHCP lease activity.
- Separate guest and corporate networks.
- Use static reservations for servers.
- Regularly audit DHCP scopes.
- Protect administrative interfaces.
- Integrate DHCP logs with SIEM platforms.

---

# Real-World Examples

| Environment | DHCP Usage |
|-------------|------------|
| Enterprise LAN | Automatic Client Configuration |
| Wi-Fi Network | IP Assignment for Wireless Devices |
| University Campus | Student Device Configuration |
| Cloud Environment | Virtual Machine Networking |
| Data Center | Dynamic Infrastructure |
| Guest Network | Temporary Address Allocation |

---

# Summary

DHCP automates the assignment of network configuration parameters, making it an essential service for modern networks. By dynamically providing IP addresses, gateways, DNS servers, and other settings, DHCP significantly reduces administrative overhead while improving scalability. During reconnaissance, DHCP responses can reveal valuable information about internal network architecture, addressing schemes, and infrastructure components. Organizations should protect DHCP services with features such as DHCP Snooping, Network Access Control (NAC), and continuous monitoring to prevent rogue servers and unauthorized network access.

---

# Chapter 10 — SMTP (Simple Mail Transfer Protocol)

## Overview

**Simple Mail Transfer Protocol (SMTP)** is the standard protocol used to **send and relay email messages** across networks.

SMTP is responsible for transferring emails between:

- Email clients and mail servers
- Mail servers and other mail servers
- Internal mail systems
- Cloud email services

Unlike **POP3** and **IMAP**, which retrieve emails, SMTP is designed exclusively for **sending and forwarding email messages**.

SMTP is one of the most common enterprise services and is frequently encountered during penetration testing because mail servers often reveal valuable information about an organization's infrastructure.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Simple Mail Transfer Protocol |
| Default Port | TCP 25 |
| Submission Port | TCP 587 |
| SMTPS Port | TCP 465 |
| Transport | TCP |
| Encryption | Optional (STARTTLS / TLS) |
| RFC | RFC 5321 |
| Application Layer | Yes |

---

# Primary Purpose

SMTP is responsible for:

- Sending emails
- Relaying emails
- Forwarding mail between servers
- Delivering outgoing messages
- Processing email queues
- Supporting email infrastructure

---

# SMTP Communication Workflow

```text
Mail Client

      │

SMTP Submission

      ▼

Mail Server

      │

SMTP Relay

      ▼

Destination Mail Server

      │

Mailbox

      ▼

Recipient
```

---

# Email Delivery Process

```text
User

    │

Compose Email

    ▼

SMTP Server

    │

DNS MX Lookup

    ▼

Recipient Mail Server

    │

Mailbox

    ▼

User Reads Email
```

---

# SMTP Commands

| Command | Purpose |
|----------|----------|
| HELO | Identify client |
| EHLO | Extended SMTP |
| MAIL FROM | Sender |
| RCPT TO | Recipient |
| DATA | Message body |
| RSET | Reset session |
| VRFY | Verify user |
| EXPN | Expand mailing list |
| NOOP | No operation |
| QUIT | Close connection |

---

# Common SMTP Response Codes

| Code | Meaning |
|------|---------|
| 220 | Service Ready |
| 221 | Closing Connection |
| 250 | OK |
| 354 | Start Mail Input |
| 421 | Service Not Available |
| 450 | Mailbox Busy |
| 451 | Temporary Error |
| 500 | Syntax Error |
| 530 | Authentication Required |
| 550 | Mailbox Unavailable |

---

# Enterprise Usage

SMTP is used in:

- Microsoft Exchange
- Office 365
- Google Workspace
- Postfix Servers
- Sendmail
- Exim
- Email Gateways
- Notification Systems
- Monitoring Platforms

---

# Common SMTP Servers

| Software | Platform |
|-----------|----------|
| Microsoft Exchange | Windows |
| Postfix | Linux |
| Exim | Linux |
| Sendmail | Linux |
| Haraka | Cross-platform |
| OpenSMTPD | BSD/Linux |

---

# Typical Architecture

```text
Mail Client

      │

SMTP

      ▼

Mail Gateway

      │

Spam Filter

      ▼

Mail Server

      │

Mailbox Database

      ▼

Recipients
```

---

# Authentication Methods

SMTP commonly supports:

- Username / Password
- LOGIN Authentication
- PLAIN Authentication
- CRAM-MD5
- OAuth
- STARTTLS Authentication

---

# Nmap Detection

Basic Scan

```bash
nmap -p25 target
```

Version Detection

```bash
nmap -sV -p25 target
```

Aggressive Scan

```bash
nmap -A -p25 target
```

Submission Port

```bash
nmap -p587 target
```

SMTPS

```bash
nmap -p465 target
```

---

# Useful NSE Scripts

SMTP Commands

```bash
nmap --script smtp-commands -p25 target
```

Open Relay Test

```bash
nmap --script smtp-open-relay -p25 target
```

SMTP Enumeration

```bash
nmap --script smtp-enum-users -p25 target
```

Retrieve Banner

```bash
nmap --script banner -p25 target
```

TLS Certificate

```bash
nmap --script ssl-cert -p465 target
```

---

# Example Banner

```text
220 mail.example.com ESMTP Postfix
```

Microsoft Exchange

```text
220 mail.corp.local Microsoft ESMTP
```

---

# Information That Can Be Collected

SMTP enumeration may reveal:

- Mail server software
- Software version
- Supported commands
- Authentication methods
- TLS support
- Internal hostnames
- Domain names
- User accounts
- Open relay configuration

---

# Blue Team Perspective

Recommendations

- Disable unnecessary SMTP commands.
- Require SMTP authentication.
- Enable STARTTLS or SMTPS.
- Disable open relay functionality.
- Restrict mail relay to trusted clients.
- Hide software version information.
- Enable logging and monitoring.
- Keep mail server software updated.

---

# Red Team Perspective

Interesting Targets

- Exchange Servers
- Internal Mail Servers
- Secure Mail Gateways
- Notification Servers
- Backup Mail Relays
- Cloud Email Gateways

Useful Enumeration

```bash
nmap -sV \
--script smtp-commands,smtp-enum-users,banner \
-p25 target
```

Potential Findings

- Open relay enabled
- User enumeration
- Internal domain names
- Software versions
- Authentication methods
- Mail routing information

---

# Common Security Risks

Frequently observed SMTP weaknesses include:

- Open relay configuration
- User enumeration
- Weak authentication
- Missing TLS encryption
- Information disclosure
- Outdated mail server software
- Misconfigured authentication
- Email spoofing

---

# Best Practices

- Disable open relay.
- Require authenticated mail submission.
- Enforce TLS for mail transport.
- Implement SPF, DKIM, and DMARC.
- Disable unnecessary SMTP commands.
- Restrict relay permissions.
- Monitor SMTP logs.
- Regularly update mail server software.

---

# Real-World Examples

| Environment | SMTP Usage |
|-------------|------------|
| Microsoft Exchange | Enterprise Email |
| Office 365 | Cloud Email |
| Google Workspace | Business Email |
| Monitoring Systems | Alert Notifications |
| Backup Systems | Status Reports |
| Web Applications | Transactional Email |

---

# Related Email Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| SMTP | Send Email | 25 / 587 / 465 |
| POP3 | Retrieve Email | 110 / 995 |
| IMAP | Synchronize Email | 143 / 993 |

---

# Summary

SMTP is the core protocol responsible for sending and relaying email across modern networks. It is widely deployed in enterprise environments, cloud platforms, and Internet-facing mail systems. During reconnaissance, SMTP services can reveal mail server software, authentication methods, supported commands, internal domains, and potential misconfigurations such as open mail relays or user enumeration. Proper hardening—including mandatory authentication, TLS encryption, SPF/DKIM/DMARC implementation, and continuous monitoring—is essential for securing enterprise email infrastructure.

---

# Chapter 11 — POP3 (Post Office Protocol Version 3)

## Overview

**Post Office Protocol Version 3 (POP3)** is an email retrieval protocol that allows clients to download messages from a mail server to a local device.

Unlike **IMAP**, which synchronizes mailboxes across multiple devices, POP3 typically downloads emails and optionally removes them from the server. This behavior makes POP3 simple and lightweight but less suitable for modern multi-device environments.

Although its usage has declined in favor of IMAP, POP3 is still found in legacy systems, embedded devices, and organizations with simple email infrastructures.

During security assessments, POP3 services may reveal authentication methods, server software, encryption support, and configuration weaknesses.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Post Office Protocol Version 3 |
| Default Port | TCP 110 |
| Secure Port | TCP 995 (POP3S) |
| Transport | TCP |
| Encryption | Optional (TLS/SSL) |
| RFC | RFC 1939 |
| Application Layer | Yes |

---

# Primary Purpose

POP3 enables users to:

- Download email messages
- Authenticate to a mailbox
- Delete messages from the server
- Read emails while offline
- Manage local email storage

---

# Communication Workflow

```text
Mail Client

      │

Connect

      ▼

POP3 Server

      │

Authenticate

      ▼

Mailbox

      │

Download Messages

      ▼

Local Computer
```

---

# Session Workflow

```text
Client

   │

USER

   ▼

PASS

   ▼

Authentication

   ▼

LIST

   ▼

RETR

   ▼

DELE (Optional)

   ▼

QUIT
```

---

# POP3 States

| State | Description |
|---------|-------------|
| Authorization | User authentication |
| Transaction | Read and manage messages |
| Update | Apply mailbox changes after logout |

---

# Common POP3 Commands

| Command | Description |
|----------|-------------|
| USER | Specify username |
| PASS | Specify password |
| STAT | Mailbox statistics |
| LIST | List available messages |
| RETR | Retrieve a message |
| TOP | Retrieve message headers |
| DELE | Delete a message |
| RSET | Reset deletion marks |
| QUIT | Close the session |

---

# Enterprise Usage

Although less common today, POP3 is still used in:

- Legacy mail systems
- Small businesses
- Embedded systems
- Industrial environments
- Offline email clients
- Archive servers

---

# Common POP3 Servers

| Software | Platform |
|-----------|----------|
| Dovecot | Linux |
| Courier Mail Server | Linux |
| Microsoft Exchange (Legacy Support) | Windows |
| Zimbra | Linux |
| hMailServer | Windows |

---

# Typical Architecture

```text
User

   │

POP3 Client

   ▼

Firewall

   ▼

Mail Server

   │

Mailbox

   ▼

Stored Messages
```

---

# POP3 vs IMAP

| Feature | POP3 | IMAP |
|----------|------|------|
| Downloads Messages | Yes | No |
| Synchronizes Devices | No | Yes |
| Server Storage | Minimal | Extensive |
| Offline Access | Excellent | Limited |
| Multi-Device Support | Poor | Excellent |

---

# Nmap Detection

Basic Scan

```bash
nmap -p110 target
```

Version Detection

```bash
nmap -sV -p110 target
```

Secure POP3

```bash
nmap -p995 target
```

Aggressive Scan

```bash
nmap -A -p110 target
```

---

# Useful NSE Scripts

Retrieve Banner

```bash
nmap --script banner -p110 target
```

Check SSL Certificate

```bash
nmap --script ssl-cert -p995 target
```

Enumerate SSL Ciphers

```bash
nmap --script ssl-enum-ciphers -p995 target
```

---

# Example Banner

```text
+OK Dovecot ready.
```

Microsoft Exchange

```text
+OK Microsoft Exchange POP3 Server Ready
```

---

# Information That Can Be Collected

POP3 enumeration may reveal:

- Mail server software
- Software version
- Supported authentication methods
- TLS availability
- Certificate information
- Internal hostnames
- Domain names
- Banner information

---

# Blue Team Perspective

Recommendations

- Prefer POP3S over plaintext POP3.
- Require TLS encryption.
- Disable plaintext authentication.
- Enforce strong passwords.
- Enable account lockout policies.
- Monitor authentication failures.
- Hide software version information.
- Keep mail server software updated.

---

# Red Team Perspective

Interesting Targets

- Legacy mail servers
- Internal email systems
- Backup mail servers
- Small business infrastructures
- Embedded email gateways

Useful Enumeration

```bash
nmap -sV \
--script banner,ssl-cert,ssl-enum-ciphers \
-p110,995 target
```

Potential Findings

- Plaintext authentication
- Weak TLS configuration
- Outdated mail software
- Certificate issues
- Internal domain names
- Information disclosure

---

# Common Security Risks

Frequently observed POP3 weaknesses include:

- Plaintext authentication
- Weak passwords
- Outdated TLS versions
- Expired certificates
- Legacy mail software
- Information disclosure
- Missing account lockout
- Brute-force attacks

---

# Best Practices

- Use POP3S whenever possible.
- Disable unencrypted authentication.
- Require TLS 1.2 or TLS 1.3.
- Enforce strong password policies.
- Monitor login attempts.
- Enable multi-factor authentication where supported.
- Patch mail servers regularly.
- Restrict external access when unnecessary.

---

# Real-World Examples

| Environment | POP3 Usage |
|-------------|------------|
| Small Business | Local Email Download |
| Legacy Exchange | Mail Retrieval |
| Embedded Devices | Alert Mailboxes |
| Archive Systems | Offline Storage |
| Industrial Networks | Notification Mailboxes |

---

# Related Email Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| SMTP | Send Email | 25 / 587 / 465 |
| POP3 | Download Email | 110 / 995 |
| IMAP | Synchronize Email | 143 / 993 |

---

# Summary

POP3 is a simple and reliable protocol for retrieving email messages from a mail server. While its popularity has decreased due to the widespread adoption of IMAP, it remains present in many legacy and specialized environments. During reconnaissance, POP3 services can expose server software, authentication methods, encryption capabilities, and configuration weaknesses. Organizations should prioritize encrypted POP3S connections, disable plaintext authentication, and maintain secure mail server configurations.

---

# Chapter 12 — IMAP (Internet Message Access Protocol)

## Overview

**Internet Message Access Protocol (IMAP)** is a standard email retrieval protocol that allows users to access and synchronize email messages directly from a mail server.

Unlike **POP3**, which typically downloads emails to a single device, IMAP keeps messages stored on the server and synchronizes changes across multiple devices. This makes IMAP the preferred protocol for modern email systems.

Today, IMAP is widely used by enterprises, cloud email providers, and mobile devices because it supports real-time synchronization and centralized mailbox management.

During penetration testing, IMAP services may reveal mail server software, authentication mechanisms, encryption support, and internal domain information.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Internet Message Access Protocol |
| Default Port | TCP 143 |
| Secure Port | TCP 993 (IMAPS) |
| Transport | TCP |
| Encryption | Optional (STARTTLS) / TLS |
| RFC | RFC 9051 (IMAP4rev2) |
| Application Layer | Yes |

---

# Primary Purpose

IMAP allows users to:

- Read email messages
- Synchronize mailboxes
- Create folders
- Delete messages
- Flag messages
- Search emails
- Access multiple mailboxes
- Synchronize across devices

---

# Communication Workflow

```text
Mail Client

      │

Connect

      ▼

IMAP Server

      │

Authentication

      ▼

Mailbox

      │

Synchronization

      ▼

Client Devices
```

---

# Synchronization Process

```text
Desktop

     │

Laptop

     │

Mobile Phone

     │

      ▼

IMAP Server

      │

Single Mailbox

      ▼

Synchronized Messages
```

Every connected device sees the same mailbox state.

---

# IMAP States

| State | Description |
|---------|-------------|
| Non-Authenticated | Initial connection |
| Authenticated | User logged in |
| Selected | Mailbox selected |
| Logout | Session terminated |

---

# Common IMAP Commands

| Command | Description |
|----------|-------------|
| LOGIN | Authenticate user |
| AUTHENTICATE | Secure authentication |
| LIST | List mailboxes |
| SELECT | Open mailbox |
| FETCH | Retrieve messages |
| SEARCH | Search mailbox |
| STORE | Modify message flags |
| COPY | Copy messages |
| EXPUNGE | Permanently delete messages |
| LOGOUT | Close session |

---

# Enterprise Usage

IMAP is commonly deployed in:

- Microsoft Exchange
- Microsoft 365
- Google Workspace
- Zimbra
- Dovecot
- Courier Mail Server
- Enterprise mail systems
- Cloud email platforms

---

# Common IMAP Servers

| Software | Platform |
|-----------|----------|
| Dovecot | Linux |
| Microsoft Exchange | Windows |
| Cyrus IMAP | Linux |
| Courier IMAP | Linux |
| Zimbra | Linux |
| hMailServer | Windows |

---

# Typical Architecture

```text
User Devices

   │

Desktop

Laptop

Mobile

   │

   ▼

IMAP Server

   │

Mailbox Storage

   ▼

Mail Database
```

---

# IMAP vs POP3

| Feature | IMAP | POP3 |
|----------|------|------|
| Synchronization | Yes | No |
| Multiple Devices | Yes | Limited |
| Server Storage | Yes | Optional |
| Folder Management | Yes | Limited |
| Offline Access | Partial | Excellent |
| Recommended | Yes | Legacy Environments |

---

# Nmap Detection

Basic Scan

```bash
nmap -p143 target
```

Version Detection

```bash
nmap -sV -p143 target
```

Secure IMAP

```bash
nmap -p993 target
```

Aggressive Scan

```bash
nmap -A -p143 target
```

---

# Useful NSE Scripts

Retrieve Banner

```bash
nmap --script banner -p143 target
```

Check SSL Certificate

```bash
nmap --script ssl-cert -p993 target
```

Enumerate TLS Ciphers

```bash
nmap --script ssl-enum-ciphers -p993 target
```

---

# Example Banner

```text
* OK Dovecot Ready.
```

Microsoft Exchange

```text
* OK Microsoft Exchange IMAP4 Service Ready
```

---

# Information That Can Be Collected

IMAP enumeration may reveal:

- Mail server software
- Software version
- Supported authentication methods
- TLS configuration
- Certificate information
- Internal domain names
- Banner information
- Server capabilities

---

# Blue Team Perspective

Recommendations

- Require IMAPS or STARTTLS.
- Disable plaintext authentication.
- Enforce strong password policies.
- Enable multi-factor authentication.
- Hide unnecessary banner information.
- Monitor authentication attempts.
- Regularly update mail server software.
- Restrict external access where appropriate.

---

# Red Team Perspective

Interesting Targets

- Enterprise mail servers
- Exchange servers
- Cloud email gateways
- Legacy email infrastructure
- Internal messaging systems

Useful Enumeration

```bash
nmap -sV \
--script banner,ssl-cert,ssl-enum-ciphers \
-p143,993 target
```

Potential Findings

- Weak TLS configuration
- Plaintext authentication
- Internal hostnames
- Certificate issues
- Software versions
- Supported authentication mechanisms

---

# Common Security Risks

Frequently observed IMAP weaknesses include:

- Unencrypted authentication
- Weak passwords
- Outdated TLS versions
- Information disclosure
- Expired certificates
- Legacy mail server software
- Brute-force attacks
- Poor account management

---

# Best Practices

- Require TLS for all client connections.
- Disable legacy authentication methods.
- Enforce strong password policies.
- Enable account lockout policies.
- Implement multi-factor authentication.
- Monitor authentication logs.
- Patch mail servers regularly.
- Protect administrative interfaces.

---

# Real-World Examples

| Environment | IMAP Usage |
|-------------|------------|
| Microsoft 365 | Enterprise Email |
| Google Workspace | Cloud Email |
| Corporate Exchange | Internal Messaging |
| Universities | Student Mail Services |
| Hosting Providers | Shared Email Platforms |

---

# Related Email Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| SMTP | Send Email | 25 / 587 / 465 |
| POP3 | Download Email | 110 / 995 |
| IMAP | Synchronize Email | 143 / 993 |

---

# Summary

IMAP is the modern standard for retrieving and synchronizing email messages across multiple devices. By storing emails on the server and maintaining consistent mailbox state, IMAP provides greater flexibility than POP3 for enterprise and cloud-based environments. During reconnaissance, IMAP services can reveal server software, supported authentication mechanisms, TLS configurations, and other valuable information. Organizations should enforce encrypted connections, disable legacy authentication methods, and continuously monitor mail infrastructure to reduce the risk of unauthorized access.

---

# Chapter 13 — LDAP (Lightweight Directory Access Protocol)

## Overview

**Lightweight Directory Access Protocol (LDAP)** is an application-layer protocol used to access, query, and manage directory services over IP networks.

LDAP stores structured information about users, computers, groups, organizational units, printers, applications, and other network resources.

In Microsoft environments, LDAP is one of the core technologies behind **Active Directory (AD)**, making it one of the most valuable services encountered during enterprise penetration testing.

Because LDAP contains identity information, improper configuration can expose usernames, email addresses, group memberships, organizational structures, and authentication details.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Lightweight Directory Access Protocol |
| Default Port | TCP/UDP 389 |
| Secure Port | TCP 636 (LDAPS) |
| Transport | TCP / UDP |
| Encryption | Optional (STARTTLS) / TLS |
| RFC | RFC 4511 |
| Application Layer | Yes |

---

# Primary Purpose

LDAP is designed to:

- Store directory information
- Authenticate users
- Query user accounts
- Manage groups
- Organize organizational units (OUs)
- Provide centralized identity management
- Support enterprise authentication

---

# LDAP Directory Structure

LDAP stores data in a hierarchical structure.

```text
DC=company,DC=com

│

├── OU=Users
│      ├── Alice
│      ├── Bob
│      └── Charlie
│
├── OU=Groups
│      ├── IT
│      ├── HR
│      └── Finance
│
└── OU=Servers
       ├── DC01
       ├── FILE01
       └── WEB01
```

---

# Distinguished Name (DN)

Each LDAP object has a unique identifier called a **Distinguished Name (DN).**

Example:

```text
CN=Alice Smith,
OU=Users,
DC=company,
DC=com
```

Components:

| Component | Meaning |
|-----------|----------|
| CN | Common Name |
| OU | Organizational Unit |
| DC | Domain Component |
| O | Organization |
| C | Country |

---

# LDAP Communication Workflow

```text
LDAP Client

      │

TCP 389

      ▼

LDAP Server

      │

Bind

      ▼

Authentication

      │

Directory Query

      ▼

Directory Response
```

---

# Authentication Methods

LDAP commonly supports:

- Anonymous Bind
- Simple Bind
- SASL
- Kerberos
- NTLM
- Certificate Authentication

---

# LDAP Operations

| Operation | Purpose |
|------------|----------|
| Bind | Authenticate |
| Search | Query directory |
| Compare | Compare attribute values |
| Add | Create object |
| Modify | Update object |
| Delete | Remove object |
| Modify DN | Rename or move object |
| Unbind | Close session |

---

# Enterprise Usage

LDAP is widely used in:

- Microsoft Active Directory
- OpenLDAP
- Identity Providers
- Single Sign-On (SSO)
- VPN Authentication
- Enterprise Applications
- Email Systems
- Network Authentication
- IAM Platforms

---

# Common LDAP Servers

| Software | Platform |
|-----------|----------|
| Microsoft Active Directory | Windows |
| OpenLDAP | Linux |
| Red Hat Directory Server | Linux |
| Apache Directory Server | Cross-platform |
| 389 Directory Server | Linux |

---

# Typical Enterprise Architecture

```text
User

    │

Authentication

    ▼

LDAP Server

    │

Directory Database

    ▼

Enterprise Resources

    │

Applications

VPN

Email

File Servers
```

---

# LDAP vs Active Directory

| LDAP | Active Directory |
|------|------------------|
| Protocol | Microsoft Directory Service |
| Standard | Product |
| Cross-platform | Primarily Windows |
| Used for Queries | Uses LDAP for Directory Access |

LDAP is the protocol, while **Active Directory** is Microsoft's directory service that uses LDAP for communication.

---

# Nmap Detection

Basic Scan

```bash
nmap -p389 target
```

Version Detection

```bash
nmap -sV -p389 target
```

Secure LDAP

```bash
nmap -p636 target
```

Aggressive Scan

```bash
nmap -A -p389 target
```

---

# Useful NSE Scripts

RootDSE Enumeration

```bash
nmap --script ldap-rootdse -p389 target
```

Search LDAP Entries

```bash
nmap --script ldap-search -p389 target
```

Retrieve Banner

```bash
nmap --script banner -p389 target
```

Check SSL Certificate

```bash
nmap --script ssl-cert -p636 target
```

---

# Example RootDSE Output

```text
defaultNamingContext:

DC=company,DC=com

dnsHostName:

DC01.company.com

supportedLDAPVersion:

3
```

---

# Information That Can Be Collected

LDAP enumeration may reveal:

- Domain name
- Forest name
- Domain Controller hostname
- Organizational Units
- User accounts
- Group names
- Service accounts
- Email addresses
- Password policies
- Domain functional level

---

# Blue Team Perspective

Recommendations

- Disable anonymous LDAP binds.
- Require LDAPS or STARTTLS.
- Restrict LDAP access using firewalls.
- Implement least privilege.
- Monitor LDAP queries.
- Protect service accounts.
- Enable auditing.
- Regularly review directory permissions.

---

# Red Team Perspective

Interesting Targets

- Domain Controllers
- Global Catalog Servers
- Active Directory
- Identity Providers
- LDAP Gateways
- Enterprise Applications

Useful Enumeration

```bash
nmap -sV \
--script ldap-rootdse,ldap-search,banner \
-p389 target
```

Potential Findings

- Domain naming context
- Organizational structure
- User accounts
- Service accounts
- Group memberships
- Domain Controller information
- Directory version
- Authentication methods

---

# Common Security Risks

Frequently observed LDAP weaknesses include:

- Anonymous bind enabled
- Information disclosure
- Weak access controls
- Insecure LDAP (without TLS)
- Misconfigured permissions
- Service account exposure
- Legacy authentication methods
- Excessive directory permissions

---

# Best Practices

- Enforce LDAPS whenever possible.
- Disable anonymous binds.
- Restrict directory queries.
- Monitor LDAP traffic.
- Protect privileged accounts.
- Rotate service account credentials.
- Enable comprehensive auditing.
- Keep directory services updated.

---

# Real-World Examples

| Environment | LDAP Usage |
|-------------|------------|
| Active Directory | User Authentication |
| Microsoft Exchange | Address Book |
| VPN Gateway | User Validation |
| Wi-Fi Authentication | Directory Lookup |
| Enterprise Applications | Single Sign-On |
| Identity Management | Centralized Directory |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| LDAP | Directory Access | 389 |
| LDAPS | Secure LDAP | 636 |
| Kerberos | Authentication | 88 |
| DNS | Name Resolution | 53 |

---

# Summary

LDAP is the foundation of centralized identity management in modern enterprise environments. It enables applications and services to authenticate users, retrieve directory information, and manage organizational resources efficiently. During reconnaissance, LDAP services often reveal valuable information about Active Directory domains, organizational structures, user accounts, and authentication mechanisms. Organizations should enforce encrypted LDAP communication (LDAPS), disable anonymous binds, apply least-privilege principles, and continuously monitor directory access to protect sensitive identity information.

---

# Chapter 14 — Kerberos

## Overview

**Kerberos** is a network authentication protocol that provides **secure, ticket-based authentication** for users and services within a trusted network.

Originally developed at the Massachusetts Institute of Technology (MIT), Kerberos has become the default authentication protocol for **Microsoft Active Directory** and is widely used in enterprise environments.

Unlike traditional password-based authentication, Kerberos minimizes password exposure by using **encrypted tickets** issued by a trusted authority known as the **Key Distribution Center (KDC)**.

For penetration testers, Kerberos is one of the most valuable services because it plays a central role in authentication, authorization, privilege escalation, and lateral movement within Active Directory environments.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Kerberos Network Authentication Protocol |
| Default Port | TCP/UDP 88 |
| Transport | TCP / UDP |
| Encryption | Yes |
| RFC | RFC 4120 |
| Application Layer | Yes |
| Primary Usage | Authentication |

---

# Primary Purpose

Kerberos provides:

- Secure authentication
- Single Sign-On (SSO)
- Mutual authentication
- Ticket-based access
- Credential protection
- Enterprise identity management

---

# Core Components

| Component | Description |
|-----------|-------------|
| Client | User requesting access |
| KDC | Key Distribution Center |
| Authentication Server (AS) | Verifies user identity |
| Ticket Granting Server (TGS) | Issues service tickets |
| Service Server | Provides requested service |

---

# Kerberos Architecture

```text
            Key Distribution Center

          ┌──────────────────────┐
          │ Authentication Server│
          │ Ticket Granting Srv  │
          └──────────┬───────────┘
                     │
          ┌──────────┴───────────┐
          │                      │
       Client              Service Server
```

---

# Authentication Workflow

```text
Client

   │

AS-REQ

   ▼

Authentication Server

   │

AS-REP (TGT)

   ▼

Client

   │

TGS-REQ

   ▼

Ticket Granting Server

   │

TGS-REP (Service Ticket)

   ▼

Service Server

   │

Access Granted
```

---

# Kerberos Tickets

## Ticket Granting Ticket (TGT)

Issued after successful authentication.

Purpose:

- Prove user identity
- Request service tickets
- Enable Single Sign-On

---

## Service Ticket (TGS Ticket)

Issued after presenting a valid TGT.

Purpose:

- Access network services
- Authenticate to servers
- Avoid sending passwords repeatedly

---

# Kerberos Encryption

Common encryption algorithms include:

- AES-128
- AES-256
- RC4-HMAC (Legacy)
- DES (Deprecated)

Modern Active Directory environments should use **AES-based encryption** whenever possible.

---

# Enterprise Usage

Kerberos is commonly used in:

- Active Directory
- Microsoft Exchange
- File Servers
- SQL Server
- SharePoint
- IIS Web Servers
- Remote Desktop Services
- Enterprise Applications

---

# Typical Enterprise Architecture

```text
User

   │

Login

   ▼

Domain Controller

(KDC)

   │

Ticket Issued

   ▼

Enterprise Services

   │

SMB

SQL

Exchange

IIS

LDAP
```

---

# Common Kerberos Messages

| Message | Purpose |
|----------|----------|
| AS-REQ | Authentication request |
| AS-REP | Authentication response |
| TGS-REQ | Service ticket request |
| TGS-REP | Service ticket response |
| AP-REQ | Access request |
| AP-REP | Mutual authentication |

---

# Nmap Detection

Basic Scan

```bash
nmap -p88 target
```

Version Detection

```bash
nmap -sV -p88 target
```

UDP Scan

```bash
nmap -sU -p88 target
```

Aggressive Scan

```bash
nmap -A -p88 target
```

---

# Useful NSE Scripts

Kerberos User Enumeration

```bash
nmap --script krb5-enum-users -p88 target
```

Retrieve Banner

```bash
nmap --script banner -p88 target
```

---

# Example Output

```text
88/tcp open kerberos-sec
Microsoft Windows Kerberos
```

---

# Information That Can Be Collected

Kerberos enumeration may reveal:

- Domain name
- Domain Controller hostname
- Valid usernames
- Authentication realm
- Kerberos version
- Service Principal Names (SPNs)
- Encryption types
- Domain information

---

# Blue Team Perspective

Recommendations

- Enforce AES encryption.
- Disable deprecated encryption algorithms.
- Require strong password policies.
- Protect privileged accounts.
- Rotate Kerberos service account passwords.
- Monitor authentication failures.
- Enable advanced auditing.
- Restrict administrative privileges.

---

# Red Team Perspective

Interesting Targets

- Domain Controllers
- Active Directory
- Exchange Servers
- SQL Servers
- IIS Servers
- Service Accounts
- Administrative Users

Useful Enumeration

```bash
nmap -sV \
--script krb5-enum-users,banner \
-p88 target
```

Potential Findings

- Valid usernames
- Domain realm
- Domain Controller information
- Kerberos configuration
- Service accounts
- Authentication mechanisms

---

# Common Kerberos Attacks

Understanding these attacks helps defenders recognize common attack paths.

| Attack | Description |
|---------|-------------|
| Kerberoasting | Extracting service tickets for offline password cracking |
| AS-REP Roasting | Requesting AS-REP messages from accounts without pre-authentication |
| Golden Ticket | Forged TGT using the KRBTGT account hash |
| Silver Ticket | Forged service ticket for a specific service |
| Pass-the-Ticket | Reusing stolen Kerberos tickets |
| Overpass-the-Hash | Using NTLM hashes to obtain Kerberos tickets |

---

# Common Security Risks

Frequently observed Kerberos weaknesses include:

- Weak service account passwords
- Legacy RC4 encryption
- Excessive administrative privileges
- Unconstrained delegation
- Misconfigured Service Principal Names
- Poor password hygiene
- Long-lived service accounts
- Weak auditing

---

# Best Practices

- Enforce AES encryption.
- Disable RC4 and DES where possible.
- Require pre-authentication for all users.
- Use strong passwords for service accounts.
- Rotate KRBTGT account passwords periodically.
- Implement tiered administration.
- Monitor abnormal Kerberos activity.
- Enable detailed security logging.

---

# Real-World Examples

| Environment | Kerberos Usage |
|-------------|----------------|
| Active Directory | User Authentication |
| Microsoft Exchange | Mail Authentication |
| SQL Server | Integrated Authentication |
| IIS | Windows Authentication |
| File Server | SMB Authentication |
| Remote Desktop | Domain Login |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Kerberos | Authentication | 88 |
| LDAP | Directory Services | 389 |
| DNS | Name Resolution | 53 |
| SMB | File Sharing | 445 |

---

# Summary

Kerberos is the primary authentication protocol used in modern Active Directory environments. By replacing repeated password transmissions with encrypted tickets, it provides secure, scalable, and efficient authentication across enterprise networks. During reconnaissance, Kerberos services can reveal domain information, authentication realms, service accounts, and user enumeration opportunities. Proper hardening—including modern encryption, strong service account management, comprehensive auditing, and least-privilege administration—is essential to defend against common Kerberos-based attacks such as Kerberoasting, AS-REP Roasting, and Pass-the-Ticket.

---

# Chapter 15 — RDP (Remote Desktop Protocol)

## Overview

**Remote Desktop Protocol (RDP)** is a proprietary protocol developed by Microsoft that enables users to remotely access and control Windows systems through a graphical interface.

Unlike SSH, which primarily provides a command-line interface, RDP offers a complete desktop experience, allowing administrators to interact with remote systems as if they were physically present.

RDP is extensively used in enterprise environments for system administration, technical support, remote work, and virtual desktop infrastructure (VDI).

Because RDP often provides direct administrative access to Windows systems, it is one of the most frequently targeted services during cyber attacks and penetration tests.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Remote Desktop Protocol |
| Default Port | TCP 3389 |
| Transport | TCP / UDP |
| Encryption | Yes (TLS) |
| Developer | Microsoft |
| Application Layer | Yes |
| Primary Platform | Windows |

---

# Primary Purpose

RDP enables users to:

- Remotely control computers
- Perform system administration
- Access graphical desktops
- Troubleshoot systems
- Manage servers
- Support remote employees
- Connect to virtual desktops

---

# Communication Workflow

```text
Administrator

      │

RDP Client

      │

TCP 3389

      ▼

RDP Server

      │

Authentication

      ▼

Windows Session

      │

Desktop Environment
```

---

# Session Establishment

```text
Client

   │

TCP Connection

   ▼

TLS Negotiation

   ▼

Authentication

   ▼

Session Creation

   ▼

Desktop Rendering

   ▼

Remote Control
```

---

# Authentication Methods

RDP commonly supports:

- Username and Password
- Active Directory Authentication
- Kerberos
- NTLM
- Smart Cards
- Network Level Authentication (NLA)
- Multi-Factor Authentication (MFA)

---

# Enterprise Usage

RDP is widely used for:

- Windows Server administration
- Help desk support
- Remote work
- Cloud virtual machines
- Virtual Desktop Infrastructure (VDI)
- Hyper-V management
- Azure Virtual Desktop
- Application servers

---

# Typical Enterprise Architecture

```text
Administrator

      │

VPN

      │

Firewall

      ▼

Remote Desktop Gateway

      ▼

Windows Server

      │

Applications

Databases

Services
```

---

# Common RDP Servers

| Software | Platform |
|-----------|----------|
| Microsoft Remote Desktop Services | Windows |
| Windows Server | Windows |
| Azure Virtual Desktop | Microsoft Azure |
| xrdp | Linux |
| FreeRDP Server | Cross-platform |

---

# Security Features

Modern RDP implementations support:

- TLS encryption
- Network Level Authentication (NLA)
- Credential Guard
- Remote Credential Guard
- Restricted Admin Mode
- Multi-Factor Authentication

---

# Nmap Detection

Basic Scan

```bash
nmap -p3389 target
```

Version Detection

```bash
nmap -sV -p3389 target
```

Aggressive Scan

```bash
nmap -A -p3389 target
```

Default Scripts

```bash
nmap -sC -sV -p3389 target
```

---

# Useful NSE Scripts

Retrieve RDP Information

```bash
nmap --script rdp-enum-encryption -p3389 target
```

Check NTLM Information

```bash
nmap --script rdp-ntlm-info -p3389 target
```

Retrieve Banner

```bash
nmap --script banner -p3389 target
```

---

# Example Output

```text
3389/tcp open ms-wbt-server
```

Example NTLM Information

```text
Computer Name:
DC01

DNS Domain:
corp.local

Product Version:
Windows Server 2022
```

---

# Information That Can Be Collected

RDP enumeration may reveal:

- Computer name
- Domain name
- Windows version
- Build number
- Authentication methods
- Encryption level
- NTLM information
- Server hostname
- DNS information

---

# Blue Team Perspective

Recommendations

- Enable Network Level Authentication (NLA).
- Require Multi-Factor Authentication.
- Restrict RDP access using firewalls.
- Use VPN or Remote Desktop Gateway.
- Disable unused RDP services.
- Monitor login attempts.
- Apply Microsoft security updates.
- Restrict administrative accounts.

---

# Red Team Perspective

Interesting Targets

- Domain Controllers
- File Servers
- Application Servers
- Administrative Workstations
- Jump Servers
- Azure Virtual Desktop
- Hyper-V Hosts

Useful Enumeration

```bash
nmap -sV \
--script rdp-enum-encryption,rdp-ntlm-info,banner \
-p3389 target
```

Potential Findings

- Windows build version
- Domain membership
- Computer hostname
- Weak encryption
- Missing NLA
- Authentication methods
- Internal DNS names

---

# Common Security Risks

Frequently observed RDP weaknesses include:

- Weak passwords
- Exposed RDP to the Internet
- Missing Multi-Factor Authentication
- Network Level Authentication disabled
- Outdated Windows systems
- Brute-force attacks
- Credential theft
- BlueKeep-vulnerable systems

---

# Best Practices

- Never expose RDP directly to the Internet.
- Require VPN or Remote Desktop Gateway.
- Enable Network Level Authentication.
- Enforce Multi-Factor Authentication.
- Apply security patches promptly.
- Restrict administrative access.
- Monitor failed login attempts.
- Enable account lockout policies.

---

# Real-World Examples

| Environment | RDP Usage |
|-------------|-----------|
| Windows Server | Remote Administration |
| Domain Controller | Administrative Access |
| Azure Virtual Desktop | Cloud Desktop |
| Hyper-V Host | Virtual Machine Management |
| Help Desk | Remote Technical Support |
| Enterprise Workstation | Remote Employee Access |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| RDP | Remote Desktop | 3389 |
| SSH | Secure Remote Shell | 22 |
| VNC | Remote Desktop | 5900 |
| WinRM | Remote Management | 5985 / 5986 |

---

# Summary

RDP is Microsoft's primary protocol for remote graphical administration and desktop access. It is widely deployed across enterprise Windows environments, making it a high-value target during security assessments. Proper enumeration can reveal operating system versions, domain information, encryption settings, and authentication mechanisms. Organizations should secure RDP by enabling Network Level Authentication, enforcing multi-factor authentication, restricting access through VPNs or Remote Desktop Gateways, and continuously monitoring remote access activity.

---

# Chapter 16 — Telnet

## Overview

**Telnet** is one of the earliest network protocols designed for remote command-line access to computers over TCP/IP networks.

Unlike SSH, Telnet **does not provide encryption**, meaning all transmitted data—including usernames, passwords, and commands—is sent in plaintext.

Although Telnet has largely been replaced by SSH in modern environments, it is still encountered in:

- Legacy enterprise systems
- Industrial Control Systems (ICS)
- Network appliances
- Embedded devices
- IoT devices
- Older UNIX systems
- Laboratory equipment

Because of its lack of encryption, Telnet is considered **insecure** and should not be used across untrusted networks.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Telnet |
| Default Port | TCP 23 |
| Transport | TCP |
| Encryption | No |
| RFC | RFC 854 |
| Application Layer | Yes |
| Status | Legacy / Insecure |

---

# Primary Purpose

Telnet allows users to:

- Access remote command-line interfaces
- Manage network devices
- Troubleshoot systems
- Execute commands remotely
- Configure embedded devices
- Test TCP services

---

# Communication Workflow

```text
Administrator

      │

TCP 23

      ▼

Telnet Server

      │

Username

Password

      ▼

Remote Shell

      │

Operating System
```

Everything exchanged between the client and server is transmitted without encryption.

---

# Session Establishment

```text
Client

   │

TCP Connection

   ▼

Login Prompt

   ▼

Username

   ▼

Password

   ▼

Authenticated Session

   ▼

Remote Command Execution
```

---

# Typical Enterprise Usage

Although uncommon today, Telnet may still be found in:

- Legacy routers
- Industrial PLCs
- Power management systems
- Medical equipment
- Embedded Linux devices
- Legacy UNIX servers
- Test laboratories

---

# Common Telnet Servers

| Software | Platform |
|-----------|----------|
| inetutils-telnetd | Linux |
| BusyBox Telnetd | Embedded Linux |
| Cisco IOS (Legacy) | Network Devices |
| Windows Telnet Server (Deprecated) | Windows |
| Solaris Telnet Service | UNIX |

---

# Typical Architecture

```text
Administrator

      │

Telnet Client

      ▼

Firewall

      ▼

Legacy Server

      │

Operating System

      ▼

Applications
```

---

# Why Telnet Is Insecure

Unlike SSH, Telnet provides:

- No encryption
- No integrity protection
- No server authentication
- No secure key exchange

An attacker monitoring the network can capture:

- Usernames
- Passwords
- Commands
- Configuration files
- Sensitive data

---

# Telnet vs SSH

| Feature | Telnet | SSH |
|----------|--------|-----|
| Encryption | No | Yes |
| Authentication Protection | No | Yes |
| Default Port | 23 | 22 |
| Secure File Transfer | No | Yes (SFTP/SCP) |
| Recommended | No | Yes |

---

# Nmap Detection

Basic Scan

```bash
nmap -p23 target
```

Version Detection

```bash
nmap -sV -p23 target
```

Aggressive Scan

```bash
nmap -A -p23 target
```

Default Scripts

```bash
nmap -sC -sV -p23 target
```

---

# Useful NSE Scripts

Retrieve Banner

```bash
nmap --script banner -p23 target
```

Enumerate Authentication

```bash
nmap --script telnet-encryption -p23 target
```

Version Detection

```bash
nmap -sV -p23 target
```

---

# Example Banner

```text
Welcome to Ubuntu Server

login:
```

Cisco Device

```text
User Access Verification

Username:
```

---

# Information That Can Be Collected

Telnet enumeration may reveal:

- Operating system
- Device vendor
- Software version
- Login banner
- Hostname
- Authentication prompt
- Network device model
- Legacy services

---

# Blue Team Perspective

Recommendations

- Replace Telnet with SSH.
- Disable Telnet services whenever possible.
- Restrict access using firewalls.
- Remove default credentials.
- Disable unnecessary remote administration.
- Monitor authentication attempts.
- Segment legacy devices.
- Keep embedded firmware updated.

---

# Red Team Perspective

Interesting Targets

- Legacy routers
- Industrial controllers
- Embedded devices
- IoT systems
- Medical equipment
- Network switches
- Laboratory devices

Useful Enumeration

```bash
nmap -sV \
--script banner,telnet-encryption \
-p23 target
```

Potential Findings

- Plaintext authentication
- Vendor identification
- Device model
- Default credentials
- Legacy operating systems
- Administrative interfaces

---

# Common Security Risks

Frequently observed Telnet weaknesses include:

- Plaintext credentials
- Default usernames and passwords
- Missing encryption
- Legacy operating systems
- Weak authentication
- Information disclosure
- Unpatched firmware
- Unauthorized remote access

---

# Best Practices

- Disable Telnet completely.
- Replace Telnet with SSH.
- Restrict remote administration.
- Enforce strong authentication.
- Remove default accounts.
- Segment legacy infrastructure.
- Monitor remote login activity.
- Upgrade unsupported devices.

---

# Real-World Examples

| Environment | Telnet Usage |
|-------------|--------------|
| Legacy Cisco Router | Remote CLI |
| Industrial PLC | Device Configuration |
| Embedded Linux Device | Maintenance |
| Legacy UNIX Server | Administration |
| Laboratory Equipment | Diagnostics |
| IoT Gateway | Initial Configuration |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Telnet | Remote CLI | 23 |
| SSH | Secure Remote CLI | 22 |
| RDP | Remote Desktop | 3389 |
| VNC | Remote Desktop | 5900 |

---

# Summary

Telnet was one of the earliest protocols for remote system administration, but its lack of encryption makes it unsuitable for modern networks. Because all credentials and session data are transmitted in plaintext, Telnet remains a significant security risk when exposed to untrusted networks. During reconnaissance, Telnet services can reveal device information, operating systems, vendor details, and authentication banners. Organizations should replace Telnet with SSH, disable unnecessary legacy services, and isolate devices that still require Telnet for operational reasons.

---

# Chapter 17 — VNC (Virtual Network Computing)

## Overview

**Virtual Network Computing (VNC)** is a cross-platform remote desktop protocol based on the **Remote Framebuffer (RFB)** protocol. It allows users to remotely view and control another computer's graphical desktop over a network.

Unlike Microsoft's **Remote Desktop Protocol (RDP)**, VNC is platform-independent and can be used between Windows, Linux, macOS, and various embedded systems.

VNC is commonly used for:

- Remote administration
- Technical support
- Laboratory environments
- Embedded devices
- Virtual machines
- Industrial control systems

Because many VNC deployments are poorly configured or lack strong authentication, they frequently become attractive targets during penetration tests.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Virtual Network Computing |
| Underlying Protocol | Remote Framebuffer (RFB) |
| Default Port | TCP 5900 |
| Additional Ports | TCP 5901–5909 |
| Transport | TCP |
| Encryption | Optional |
| Application Layer | Yes |

---

# Primary Purpose

VNC allows users to:

- View remote desktops
- Control remote systems
- Transfer keyboard input
- Transfer mouse input
- Perform remote maintenance
- Manage servers
- Access virtual machines

---

# Communication Workflow

```text
Administrator

      │

VNC Viewer

      │

TCP 5900

      ▼

VNC Server

      │

Authentication

      ▼

Remote Desktop

      │

Operating System
```

---

# Session Workflow

```text
Client

   │

TCP Connection

   ▼

RFB Negotiation

   ▼

Authentication

   ▼

Desktop Initialization

   ▼

Screen Updates

   ▼

User Interaction
```

---

# Common VNC Implementations

| Software | Platform |
|-----------|----------|
| RealVNC | Cross-platform |
| TightVNC | Windows/Linux |
| TigerVNC | Linux/Windows |
| UltraVNC | Windows |
| x11vnc | Linux |
| LibVNCServer | Cross-platform |

---

# Enterprise Usage

VNC is commonly found in:

- Linux servers
- Virtual machines
- Help desk environments
- Laboratory systems
- Industrial automation
- Embedded devices
- Raspberry Pi deployments
- Development workstations

---

# Typical Architecture

```text
Administrator

      │

VPN

      │

Firewall

      ▼

VNC Server

      │

Desktop Session

      ▼

Applications
```

---

# Authentication

Depending on the implementation, VNC may support:

- Password authentication
- Operating system authentication
- Active Directory integration
- Certificate authentication
- Multi-factor authentication (vendor-dependent)

Older VNC implementations often support only a simple password-based authentication mechanism.

---

# Display Numbers

Each VNC desktop is identified by a display number.

| Display | TCP Port |
|----------|----------|
| :0 | 5900 |
| :1 | 5901 |
| :2 | 5902 |
| :3 | 5903 |

---

# Nmap Detection

Basic Scan

```bash
nmap -p5900 target
```

Version Detection

```bash
nmap -sV -p5900 target
```

Aggressive Scan

```bash
nmap -A -p5900 target
```

Scan Multiple Displays

```bash
nmap -p5900-5905 target
```

---

# Useful NSE Scripts

Retrieve VNC Information

```bash
nmap --script vnc-info -p5900 target
```

Attempt Authentication (Authorized Testing Only)

```bash
nmap --script vnc-brute -p5900 target
```

Retrieve Banner

```bash
nmap --script banner -p5900 target
```

---

# Example Output

```text
5900/tcp open vnc
```

Example Enumeration

```text
Protocol: RFB 003.008

Desktop Name:

Windows Server

Authentication:

VNC Authentication
```

---

# Information That Can Be Collected

VNC enumeration may reveal:

- RFB protocol version
- Desktop name
- Authentication type
- Vendor information
- Operating system hints
- Desktop display number
- Encryption support
- Software version

---

# Blue Team Perspective

Recommendations

- Disable VNC if it is not required.
- Require strong authentication.
- Enable encrypted connections.
- Restrict VNC access through VPNs.
- Disable Internet exposure.
- Monitor connection attempts.
- Keep VNC software updated.
- Apply least-privilege principles.

---

# Red Team Perspective

Interesting Targets

- Development servers
- Virtual machines
- Engineering workstations
- Embedded Linux systems
- Raspberry Pi devices
- Industrial controllers
- Help desk systems

Useful Enumeration

```bash
nmap -sV \
--script vnc-info,banner \
-p5900 target
```

Potential Findings

- Weak authentication
- Desktop names
- Software versions
- Operating system information
- Missing encryption
- Internet-exposed remote desktop services

---

# Common Security Risks

Frequently observed VNC weaknesses include:

- Weak passwords
- No encryption
- Internet exposure
- Default credentials
- Outdated VNC software
- Shared administrator accounts
- Poor access controls
- Lack of logging

---

# Best Practices

- Never expose VNC directly to the Internet.
- Require VPN access.
- Enable encryption.
- Use strong passwords.
- Enable multi-factor authentication when supported.
- Monitor remote access logs.
- Update VNC software regularly.
- Restrict administrative access.

---

# Comparison with RDP

| Feature | VNC | RDP |
|----------|-----|-----|
| Cross-platform | Yes | Limited |
| Default Port | 5900 | 3389 |
| Remote Desktop | Yes | Yes |
| Native Encryption | Vendor-dependent | Yes |
| Performance | Moderate | High |
| Primary Platform | Cross-platform | Windows |

---

# Real-World Examples

| Environment | Typical VNC Usage |
|-------------|-------------------|
| Linux Workstation | Remote GUI Access |
| Raspberry Pi | Headless Administration |
| VMware Virtual Machine | Remote Desktop |
| Industrial HMI | Maintenance |
| Engineering Workstation | Remote Support |
| Embedded Device | Configuration |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| VNC | Remote Desktop | 5900 |
| RDP | Remote Desktop | 3389 |
| SSH | Secure Remote Shell | 22 |
| Telnet | Legacy Remote CLI | 23 |

---

# Summary

VNC is a flexible, cross-platform remote desktop protocol that enables graphical remote access to systems across Windows, Linux, macOS, and embedded environments. During reconnaissance, VNC services can reveal desktop names, authentication methods, protocol versions, and software information. Because many deployments rely on weak authentication or lack encryption, organizations should restrict VNC access through VPNs, enable secure authentication mechanisms, and regularly update VNC software to reduce the risk of unauthorized remote access.

---

# Chapter 18 — NTP (Network Time Protocol)

## Overview

**Network Time Protocol (NTP)** is a networking protocol designed to synchronize the clocks of computers, servers, network devices, and other systems across IP networks.

Accurate time synchronization is essential for authentication, logging, digital certificates, distributed systems, databases, and security monitoring.

Without synchronized time, security logs become unreliable, Kerberos authentication may fail, certificates may appear invalid, and forensic investigations become significantly more difficult.

Because of its critical role in infrastructure, NTP is commonly deployed in enterprise, cloud, industrial, and telecommunications environments.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Network Time Protocol |
| Default Port | UDP 123 |
| Transport | UDP |
| Encryption | Optional (NTS - Network Time Security) |
| RFC | RFC 5905 |
| Application Layer | Yes |
| Initial Release | 1985 |

---

# Primary Purpose

NTP synchronizes:

- System clocks
- Servers
- Workstations
- Network devices
- Firewalls
- Routers
- Domain Controllers
- Virtual machines
- Cloud infrastructure

---

# Why Time Synchronization Matters

Many enterprise services depend on accurate time.

Examples include:

- Kerberos authentication
- TLS certificate validation
- SIEM correlation
- Log analysis
- Active Directory
- Database replication
- Scheduled tasks
- Distributed applications

---

# NTP Architecture

```text
           Stratum 0

      Atomic Clock

            │

            ▼

       Stratum 1

 Primary Time Server

            │

            ▼

       Stratum 2

 Enterprise NTP

            │

            ▼

 Clients

 Servers

 Routers

 Firewalls
```

---

# Stratum Levels

| Stratum | Description |
|----------|-------------|
| 0 | Atomic Clock / GPS |
| 1 | Primary Time Server |
| 2 | Secondary Time Server |
| 3 | Internal Time Server |
| 4–15 | Client Synchronization |
| 16 | Unsynchronized |

Lower stratum values generally indicate a more accurate time source.

---

# Time Synchronization Workflow

```text
Client

   │

NTP Request

   ▼

NTP Server

   │

Timestamp Reply

   ▼

Offset Calculation

   ▼

Clock Adjustment

   ▼

Synchronized System
```

---

# Enterprise Usage

NTP is widely deployed in:

- Active Directory
- Cloud platforms
- Kubernetes clusters
- Virtualization environments
- Financial systems
- Industrial automation
- Monitoring systems
- Security appliances
- Database clusters

---

# Common NTP Servers

| Software | Platform |
|-----------|----------|
| ntpd | Linux |
| chronyd | Linux |
| Windows Time Service | Windows |
| OpenNTPD | BSD/Linux |
| systemd-timesyncd | Linux |

---

# Typical Enterprise Architecture

```text
GPS Clock

     │

Primary NTP Server

     │

Secondary NTP Server

     │

Domain Controllers

     │

Clients

Servers

Network Devices
```

---

# Nmap Detection

Basic UDP Scan

```bash
nmap -sU -p123 target
```

Version Detection

```bash
nmap -sU -sV -p123 target
```

Aggressive Scan

```bash
nmap -sU -A -p123 target
```

---

# Useful NSE Scripts

Retrieve NTP Information

```bash
nmap --script ntp-info -p123 target
```

Monitor List Check

```bash
nmap --script ntp-monlist -p123 target
```

Version Detection

```bash
nmap -sU -sV -p123 target
```

---

# Example Output

```text
123/udp open ntp
```

Example Enumeration

```text
Version: NTPv4

Stratum: 2

Reference Clock:

GPS
```

---

# Information That Can Be Collected

NTP enumeration may reveal:

- NTP version
- Stratum level
- Reference clock
- Server hostname
- Synchronization status
- Software version
- Time offset
- Operating system hints

---

# Blue Team Perspective

Recommendations

- Disable deprecated NTP features such as `monlist`.
- Restrict NTP queries to trusted networks.
- Keep NTP software updated.
- Use authenticated time sources where possible.
- Monitor unusual NTP traffic.
- Deploy redundant time servers.
- Synchronize all infrastructure components.
- Enable logging for time synchronization failures.

---

# Red Team Perspective

Interesting Targets

- Domain Controllers
- Time Servers
- Network Appliances
- Core Routers
- Firewalls
- Database Servers
- Monitoring Systems

Useful Enumeration

```bash
nmap -sU -sV \
--script ntp-info,ntp-monlist \
-p123 target
```

Potential Findings

- NTP version
- Stratum level
- Internal time hierarchy
- Legacy NTP implementation
- Monitor list enabled
- Software version
- Reference clock information

---

# Common Security Risks

Frequently observed NTP weaknesses include:

- NTP amplification attacks
- Monitor list information disclosure
- Outdated NTP software
- Unauthorized time servers
- Poor access controls
- Weak synchronization policies
- Time manipulation attacks
- Reflection attacks

---

# NTP Amplification Attacks

Historically, improperly configured NTP servers have been abused in **Distributed Denial-of-Service (DDoS)** attacks.

Attackers send small spoofed requests that generate significantly larger responses toward a victim.

```text
Attacker

    │

Spoofed Request

    ▼

Public NTP Server

    │

Large Response

    ▼

Victim
```

Proper configuration prevents this type of abuse.

---

# Best Practices

- Disable `monlist` support.
- Restrict public NTP access.
- Use internal NTP servers.
- Enable Network Time Security (NTS) where supported.
- Keep NTP implementations updated.
- Monitor synchronization status.
- Configure redundant time sources.
- Audit time synchronization regularly.

---

# Real-World Examples

| Environment | Typical NTP Usage |
|-------------|-------------------|
| Active Directory | Kerberos Synchronization |
| Financial Institution | Transaction Timestamping |
| Kubernetes Cluster | Node Synchronization |
| VMware Environment | Hypervisor Time |
| Database Cluster | Replication Timing |
| SIEM Platform | Log Correlation |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| NTP | Time Synchronization | 123 |
| DNS | Name Resolution | 53 |
| Kerberos | Authentication | 88 |
| LDAP | Directory Services | 389 |

---

# Summary

NTP is a foundational protocol responsible for maintaining accurate time across enterprise networks. Reliable time synchronization is essential for authentication, security monitoring, digital certificates, and distributed applications. During reconnaissance, NTP services can reveal software versions, stratum levels, synchronization status, and configuration details. Organizations should secure NTP by restricting access, disabling deprecated features, using authenticated time sources, and keeping time synchronization services updated.

---

# Chapter 19 — SNMP (Simple Network Management Protocol)

## Overview

**Simple Network Management Protocol (SNMP)** is an application-layer protocol used to monitor, manage, and configure network devices across IP networks.

SNMP enables administrators to collect operational information from routers, switches, firewalls, servers, printers, UPS devices, IoT systems, and many other network-connected devices.

Because SNMP often exposes valuable operational and configuration data, it is one of the most important protocols during infrastructure reconnaissance.

Improperly configured SNMP services may reveal device information, software versions, network topology, interface statistics, routing information, and sometimes even administrative credentials.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Simple Network Management Protocol |
| Default Port | UDP 161 |
| Trap Port | UDP 162 |
| Transport | UDP |
| Encryption | SNMPv3 Only |
| RFC | RFC 3411–3418 |
| Application Layer | Yes |

---

# Primary Purpose

SNMP is designed to:

- Monitor network devices
- Collect performance metrics
- Manage device configurations
- Detect failures
- Receive alerts
- Inventory network assets
- Automate monitoring

---

# SNMP Architecture

```text
          Network Management Station

                    │

            SNMP Requests

                    ▼

            Managed Devices

      ┌────────┬─────────┬────────┐
      │        │         │        │
   Router   Switch   Firewall   Server
```

---

# Core Components

| Component | Description |
|-----------|-------------|
| SNMP Manager | Central monitoring system |
| SNMP Agent | Software running on managed devices |
| Managed Device | Device being monitored |
| MIB | Management Information Base |
| OID | Object Identifier |

---

# Communication Workflow

```text
SNMP Manager

      │

GET Request

      ▼

SNMP Agent

      │

Retrieve OID

      ▼

Response

      ▼

Monitoring Dashboard
```

---

# SNMP Operations

| Operation | Purpose |
|-----------|----------|
| GET | Read a value |
| GETNEXT | Read next object |
| GETBULK | Retrieve multiple objects |
| SET | Modify configuration |
| RESPONSE | Reply from agent |
| TRAP | Unsolicited notification |
| INFORM | Confirmed notification |

---

# SNMP Versions

| Version | Security |
|----------|----------|
| SNMPv1 | Insecure |
| SNMPv2c | Community String Authentication |
| SNMPv3 | Authentication + Encryption |

SNMPv3 is the recommended version for modern enterprise environments.

---

# Management Information Base (MIB)

A **Management Information Base (MIB)** is a hierarchical database containing information about managed devices.

Example hierarchy:

```text
iso

└── org

    └── dod

        └── internet

            └── mgmt

                └── mib-2

                    ├── system
                    ├── interfaces
                    ├── ip
                    ├── tcp
                    └── udp
```

---

# Object Identifiers (OIDs)

Each managed object is identified by an **Object Identifier (OID).**

Example:

```text
1.3.6.1.2.1.1.5.0
```

This OID typically represents:

```text
System Name (sysName)
```

---

# Common Community Strings

Historically, many devices have been configured with default community strings such as:

- public
- private
- manager
- admin

These values should always be changed in production environments.

---

# Enterprise Usage

SNMP is commonly used in:

- Enterprise monitoring
- Network management
- Data centers
- ISPs
- Cloud infrastructure
- Industrial control systems
- VoIP infrastructure
- Security appliances
- Wireless controllers

---

# Common SNMP Implementations

| Software | Platform |
|-----------|----------|
| Net-SNMP | Linux |
| Windows SNMP Service | Windows |
| Cisco IOS SNMP | Network Devices |
| MikroTik RouterOS | Router |
| Juniper JunOS | Network Devices |
| VMware ESXi | Virtualization |

---

# Typical Enterprise Architecture

```text
               Monitoring Platform

         (PRTG / Zabbix / Nagios)

                    │

             SNMP Manager

                    │

     ┌──────────────┼──────────────┐

     ▼              ▼              ▼

 Router         Firewall       Switch

     ▼              ▼              ▼

 Servers      UPS Devices     Printers
```

---

# Nmap Detection

Basic UDP Scan

```bash
nmap -sU -p161 target
```

Version Detection

```bash
nmap -sU -sV -p161 target
```

Aggressive Scan

```bash
nmap -sU -A -p161 target
```

---

# Useful NSE Scripts

Retrieve System Information

```bash
nmap --script snmp-info -p161 target
```

Brute Force Community Strings (Authorized Testing Only)

```bash
nmap --script snmp-brute -p161 target
```

Retrieve Interfaces

```bash
nmap --script snmp-interfaces -p161 target
```

Retrieve Processes

```bash
nmap --script snmp-processes -p161 target
```

Retrieve Network Shares

```bash
nmap --script snmp-netstat -p161 target
```

---

# Example Output

```text
161/udp open snmp
```

Example Enumeration

```text
Hostname:

CORE-SW01

Contact:

Network Administrator

Location:

Data Center A

System Description:

Cisco IOS XE
```

---

# Information That Can Be Collected

SNMP enumeration may reveal:

- Hostname
- Device model
- Operating system
- Software version
- Contact information
- Device location
- Network interfaces
- Routing information
- Running processes
- Installed software
- Uptime
- CPU utilization
- Memory usage

---

# Blue Team Perspective

Recommendations

- Use SNMPv3 whenever possible.
- Disable SNMPv1 and SNMPv2c.
- Replace default community strings.
- Restrict SNMP access using ACLs.
- Monitor SNMP queries.
- Disable write access unless required.
- Audit SNMP configurations regularly.
- Limit exposure to trusted management networks.

---

# Red Team Perspective

Interesting Targets

- Core routers
- Layer 3 switches
- Firewalls
- Wireless controllers
- Domain Controllers
- VMware hosts
- UPS devices
- NAS appliances

Useful Enumeration

```bash
nmap -sU -sV \
--script snmp-info,snmp-interfaces,snmp-processes \
-p161 target
```

Potential Findings

- Default community strings
- Internal hostnames
- Device locations
- Software versions
- Network topology
- Running services
- Routing tables
- Hardware inventory

---

# Common Security Risks

Frequently observed SNMP weaknesses include:

- Default community strings
- SNMPv1 enabled
- SNMPv2c enabled
- Excessive read permissions
- Write access enabled
- Information disclosure
- Internet-exposed SNMP services
- Weak access controls

---

# Best Practices

- Deploy SNMPv3 with authentication and encryption.
- Disable legacy SNMP versions.
- Restrict access using firewalls and ACLs.
- Rotate authentication credentials regularly.
- Disable write access unless operationally required.
- Monitor SNMP logs for unusual activity.
- Segment management networks.
- Keep firmware and SNMP software updated.

---

# Real-World Examples

| Environment | Typical SNMP Usage |
|-------------|-------------------|
| Enterprise Network | Infrastructure Monitoring |
| ISP | Router Monitoring |
| Data Center | Server Health Monitoring |
| Hospital | Medical Device Monitoring |
| Manufacturing | Industrial Equipment Monitoring |
| Cloud Infrastructure | Performance Collection |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| SNMP | Network Management | 161 / 162 |
| SSH | Secure Administration | 22 |
| Syslog | Log Collection | 514 |
| NTP | Time Synchronization | 123 |

---

# Summary

SNMP is a critical protocol for monitoring and managing enterprise network infrastructure. It provides administrators with detailed operational information about devices, services, interfaces, and performance metrics. During reconnaissance, SNMP can reveal extensive information about an organization's infrastructure, including hardware inventory, software versions, routing details, and system statistics. Organizations should migrate to SNMPv3, eliminate default community strings, restrict management access, and continuously audit SNMP configurations to minimize the risk of information disclosure.

---

# Chapter 20 — Syslog

## Overview

**Syslog** is a standard protocol used for collecting, storing, and forwarding log messages generated by operating systems, network devices, security appliances, servers, and applications.

Virtually every enterprise environment relies on Syslog to centralize logs for monitoring, troubleshooting, compliance, incident response, and forensic investigations.

Unlike protocols such as SSH or HTTP, Syslog is **not used for remote management or data transfer**. Instead, it acts as a standardized mechanism for transmitting event information from devices to centralized logging servers.

Because Syslog often contains security events, authentication logs, firewall records, application errors, and system alerts, it plays a critical role in modern Security Operations Centers (SOC).

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | System Logging Protocol |
| Default Port | UDP 514 |
| Secure Port | TCP 6514 (Syslog over TLS) |
| Transport | UDP / TCP |
| Encryption | Optional (TLS) |
| RFC | RFC 5424 |
| Application Layer | Yes |

---

# Primary Purpose

Syslog is designed to:

- Collect system logs
- Centralize event records
- Forward security alerts
- Monitor infrastructure
- Support troubleshooting
- Enable forensic investigations
- Meet compliance requirements

---

# Communication Workflow

```text
Network Device

       │

 Log Message

       ▼

Syslog Server

       │

Store

Index

Analyze

       ▼

SIEM Platform

       │

Security Analysts
```

---

# Typical Enterprise Architecture

```text
             Firewall

                 │

             Router

                 │

      Windows Servers

                 │

       Linux Servers

                 │

      Security Appliances

                 │

          Syslog Server

                 │

              SIEM

                 │

        Security Team
```

---

# Log Generation Process

```text
System Event

      │

Log Generated

      │

Syslog Packet

      ▼

Network

      ▼

Central Log Server

      ▼

Database

      ▼

Analysis Dashboard
```

---

# Syslog Message Structure

Modern Syslog messages generally contain:

- Priority
- Timestamp
- Hostname
- Application name
- Process ID
- Message ID
- Event message

Example:

```text
<34>1 2026-07-20T14:25:13Z FW01 firewall 2312 ACCEPT Connection permitted from 10.10.5.12
```

---

# Facility Codes

Facility values indicate which subsystem generated the message.

| Facility | Description |
|----------|-------------|
| Kernel | Operating System Kernel |
| User | User-Level Processes |
| Mail | Mail Services |
| Daemon | Background Services |
| Auth | Authentication |
| Syslog | Logging Service |
| Local0–Local7 | Vendor-Specific Logs |

---

# Severity Levels

| Level | Description |
|-------|-------------|
| 0 | Emergency |
| 1 | Alert |
| 2 | Critical |
| 3 | Error |
| 4 | Warning |
| 5 | Notice |
| 6 | Informational |
| 7 | Debug |

Lower numbers indicate higher severity.

---

# Enterprise Usage

Syslog is widely deployed in:

- Security Operations Centers (SOC)
- Data Centers
- Financial Institutions
- Government Networks
- Healthcare Organizations
- Cloud Infrastructure
- Industrial Control Systems
- Internet Service Providers

---

# Common Syslog Servers

| Software | Platform |
|-----------|----------|
| rsyslog | Linux |
| syslog-ng | Linux |
| Graylog | Cross-platform |
| Kiwi Syslog Server | Windows |
| Splunk Forwarder | Cross-platform |
| Logstash | Cross-platform |

---

# Nmap Detection

Basic UDP Scan

```bash
nmap -sU -p514 target
```

TCP Scan

```bash
nmap -p514 target
```

Version Detection

```bash
nmap -sU -sV -p514 target
```

Aggressive Scan

```bash
nmap -sU -A -p514 target
```

---

# Useful NSE Scripts

Although there are no widely used dedicated NSE scripts specifically for Syslog enumeration, the following can assist in service identification:

Banner Detection

```bash
nmap --script banner -p514 target
```

Version Detection

```bash
nmap -sV -p514 target
```

Service Discovery

```bash
nmap -sC -sV -p514 target
```

---

# Example Output

```text
514/udp open syslog
```

Example Banner

```text
Syslog Server

RFC5424 Compatible
```

---

# Information That Can Be Collected

Limited enumeration may reveal:

- Syslog implementation
- Software version
- Open transport protocol
- Vendor information
- Logging service availability
- TLS support (if configured)

Unlike SNMP or HTTP, Syslog generally does not expose extensive information through simple network enumeration.

---

# Blue Team Perspective

Recommendations

- Centralize logs from all critical systems.
- Use Syslog over TLS (TCP 6514) whenever possible.
- Restrict access to Syslog servers.
- Synchronize systems using NTP.
- Retain logs according to compliance requirements.
- Monitor failed log delivery.
- Protect log integrity.
- Regularly back up log storage.

---

# Red Team Perspective

Interesting Targets

- SIEM Servers
- Central Log Servers
- SOC Infrastructure
- Security Appliances
- Firewalls
- IDS/IPS Systems
- Authentication Servers

Useful Enumeration

```bash
nmap -sU -sV \
-p514 target
```

Potential Findings

- Presence of centralized logging
- Syslog implementation
- Vendor identification
- Logging infrastructure
- Secure Syslog support

---

# Common Security Risks

Frequently observed Syslog weaknesses include:

- Plaintext log transmission
- Internet-exposed Syslog servers
- Missing TLS encryption
- Log tampering
- Excessive log retention
- Unauthorized log access
- Weak access controls
- Lack of integrity verification

---

# Syslog vs SIEM

| Feature | Syslog | SIEM |
|----------|---------|------|
| Collect Logs | Yes | Yes |
| Store Logs | Limited | Yes |
| Correlate Events | No | Yes |
| Threat Detection | No | Yes |
| Alerting | Limited | Advanced |
| Dashboard | No | Yes |

Syslog provides the log transport mechanism, while a SIEM platform consumes, analyzes, correlates, and visualizes those logs.

---

# Best Practices

- Deploy redundant Syslog servers.
- Use encrypted log transport.
- Restrict log access with least privilege.
- Validate log integrity.
- Forward logs to a SIEM platform.
- Monitor log collection failures.
- Archive logs securely.
- Perform regular log audits.

---

# Real-World Examples

| Environment | Typical Syslog Usage |
|-------------|----------------------|
| Cisco Router | Interface Events |
| Palo Alto Firewall | Security Logs |
| Linux Server | System Logs |
| Windows Server | Forwarded Events |
| VMware ESXi | Hypervisor Logs |
| Kubernetes Cluster | Node Logs |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Syslog | Log Collection | 514 / 6514 |
| SNMP | Network Monitoring | 161 |
| NTP | Time Synchronization | 123 |
| SSH | Secure Administration | 22 |

---

# Summary

Syslog is the industry-standard protocol for collecting and forwarding log messages across enterprise infrastructures. It forms the foundation of centralized logging and enables organizations to monitor system health, investigate incidents, and satisfy regulatory requirements. While Syslog itself exposes limited information during network reconnaissance, identifying a Syslog service can reveal the presence of centralized monitoring infrastructure. Organizations should secure Syslog communications with TLS, protect log integrity, restrict access, and integrate log data with SIEM platforms for comprehensive security monitoring.

---

# Chapter 21 — TFTP (Trivial File Transfer Protocol)

## Overview

**Trivial File Transfer Protocol (TFTP)** is a lightweight file transfer protocol designed for simple, connectionless file transfers over IP networks.

Unlike FTP, FTPS, or SFTP, TFTP provides **no authentication, no encryption, and no directory browsing capabilities**. Its simplicity makes it suitable for environments where devices need to quickly retrieve or upload small configuration or boot files.

TFTP is commonly found in:

- Network device firmware upgrades
- PXE (Preboot Execution Environment)
- Router and switch configuration backups
- VoIP phone provisioning
- Embedded systems
- Industrial devices

Although it remains useful in controlled environments, exposing TFTP to untrusted networks introduces significant security risks.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Trivial File Transfer Protocol |
| Default Port | UDP 69 |
| Transport | UDP |
| Encryption | No |
| Authentication | No |
| RFC | RFC 1350 |
| Application Layer | Yes |

---

# Primary Purpose

TFTP is designed to:

- Transfer small files
- Boot diskless systems
- Distribute firmware
- Backup network configurations
- Restore configurations
- Provision embedded devices
- Deliver PXE boot images

---

# Communication Workflow

```text
Client

    │

Read Request (RRQ)

or

Write Request (WRQ)

    ▼

TFTP Server

    │

Data Blocks

    ▼

Acknowledgements (ACK)

    ▼

Transfer Complete
```

Unlike FTP, TFTP uses a simple request-response model over UDP.

---

# Packet Types

| Opcode | Description |
|---------|-------------|
| RRQ | Read Request |
| WRQ | Write Request |
| DATA | File Data |
| ACK | Acknowledgement |
| ERROR | Error Message |

---

# File Transfer Process

```text
Client

   │

RRQ

   ▼

Server

   │

DATA Block 1

   ▼

ACK

   │

DATA Block 2

   ▼

ACK

   │

...

   ▼

Final Block

   ▼

Transfer Complete
```

---

# Enterprise Usage

TFTP is frequently used in:

- Cisco infrastructure
- PXE deployment servers
- Network appliances
- IP phone provisioning
- Embedded Linux systems
- Industrial control environments
- Firmware distribution servers

---

# Common TFTP Servers

| Software | Platform |
|-----------|----------|
| tftpd-hpa | Linux |
| atftpd | Linux |
| dnsmasq (TFTP Mode) | Linux |
| SolarWinds TFTP Server | Windows |
| Cisco IOS TFTP Service | Cisco Devices |

---

# Typical Enterprise Architecture

```text
               PXE Server

                   │

             TFTP Service

                   │

        ┌──────────┼──────────┐

        ▼          ▼          ▼

 Workstation   Switch     Router

        │

Boot Image

Configuration

Firmware
```

---

# Common Use Cases

Typical files transferred using TFTP include:

- Router configurations
- Switch configurations
- Firmware images
- Operating system images
- PXE boot files
- BIOS updates
- VoIP phone configuration files

---

# TFTP vs FTP

| Feature | TFTP | FTP |
|----------|------|-----|
| Transport | UDP | TCP |
| Authentication | No | Yes |
| Encryption | No | Optional (FTPS) |
| Directory Listing | No | Yes |
| File Management | Limited | Full |
| Complexity | Very Low | Moderate |

---

# Nmap Detection

Basic UDP Scan

```bash
nmap -sU -p69 target
```

Version Detection

```bash
nmap -sU -sV -p69 target
```

Aggressive Scan

```bash
nmap -sU -A -p69 target
```

---

# Useful NSE Scripts

Retrieve TFTP Information

```bash
nmap --script tftp-enum -p69 target
```

Version Detection

```bash
nmap -sU -sV -p69 target
```

Default Scripts

```bash
nmap -sC -sU -p69 target
```

---

# Example Output

```text
69/udp open tftp
```

Example Enumeration

```text
TFTP Server

Read Requests Allowed

Firmware Repository Available
```

---

# Information That Can Be Collected

TFTP enumeration may reveal:

- TFTP server presence
- Software implementation
- Firmware repository
- Configuration files
- Boot images
- Network device backups
- Accessible filenames
- Read/write permissions

---

# Blue Team Perspective

Recommendations

- Disable TFTP if not required.
- Restrict access to trusted management networks.
- Disable anonymous write access.
- Store sensitive configuration files securely.
- Monitor file transfer activity.
- Use secure alternatives where possible.
- Limit firewall exposure.
- Regularly audit accessible files.

---

# Red Team Perspective

Interesting Targets

- PXE servers
- Cisco configuration repositories
- VoIP provisioning servers
- Firmware repositories
- Industrial controllers
- Embedded Linux systems
- Network appliance management servers

Useful Enumeration

```bash
nmap -sU -sV \
--script tftp-enum \
-p69 target
```

Potential Findings

- Downloadable configuration files
- Firmware images
- Device backup files
- Network architecture information
- Default boot images
- Accessible provisioning files

---

# Common Security Risks

Frequently observed TFTP weaknesses include:

- No authentication
- No encryption
- Unauthorized file downloads
- Unauthorized file uploads
- Firmware disclosure
- Configuration leakage
- Weak access controls
- Internet exposure

---

# PXE Boot and TFTP

One of the most common enterprise uses of TFTP is **PXE booting**, where a computer downloads boot files from a TFTP server before an operating system is installed.

```text
Client

    │

DHCP Request

    ▼

DHCP Server

    │

PXE Information

    ▼

TFTP Server

    │

Boot Loader

    ▼

Operating System Installer
```

This process is widely used for automated operating system deployment in enterprise environments.

---

# Best Practices

- Restrict TFTP to isolated management networks.
- Disable write operations unless operationally necessary.
- Replace TFTP with secure alternatives where feasible.
- Monitor file access logs.
- Limit accessible directories.
- Protect firmware repositories.
- Apply the principle of least privilege.
- Regularly review server configurations.

---

# Real-World Examples

| Environment | Typical TFTP Usage |
|-------------|-------------------|
| Cisco Network | Configuration Backup |
| Enterprise PXE Server | OS Deployment |
| VoIP Infrastructure | Phone Provisioning |
| Industrial Controller | Firmware Updates |
| Embedded Device | Boot Image Distribution |
| Data Center | Network Device Recovery |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| TFTP | Lightweight File Transfer | 69 |
| FTP | File Transfer | 21 |
| FTPS | Secure FTP | 990 / 21 |
| SFTP | Secure File Transfer | 22 |
| DHCP | PXE Boot Support | 67 / 68 |

---

# Summary

TFTP is a simple, connectionless protocol designed for lightweight file transfers in trusted environments. It is commonly used for firmware distribution, PXE booting, and network device configuration management. However, because it lacks authentication and encryption, improperly secured TFTP servers can expose sensitive files and configuration data. During reconnaissance, discovering an accessible TFTP service may provide valuable information about an organization's infrastructure. Administrators should restrict TFTP access, disable unnecessary write capabilities, and migrate to secure alternatives whenever practical.

---

# Chapter 21 — TFTP (Trivial File Transfer Protocol)

## Overview

**Trivial File Transfer Protocol (TFTP)** is a lightweight file transfer protocol designed for simple, connectionless file transfers over IP networks.

Unlike FTP, FTPS, or SFTP, TFTP provides **no authentication, no encryption, and no directory browsing capabilities**. Its simplicity makes it suitable for environments where devices need to quickly retrieve or upload small configuration or boot files.

TFTP is commonly found in:

- Network device firmware upgrades
- PXE (Preboot Execution Environment)
- Router and switch configuration backups
- VoIP phone provisioning
- Embedded systems
- Industrial devices

Although it remains useful in controlled environments, exposing TFTP to untrusted networks introduces significant security risks.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Trivial File Transfer Protocol |
| Default Port | UDP 69 |
| Transport | UDP |
| Encryption | No |
| Authentication | No |
| RFC | RFC 1350 |
| Application Layer | Yes |

---

# Primary Purpose

TFTP is designed to:

- Transfer small files
- Boot diskless systems
- Distribute firmware
- Backup network configurations
- Restore configurations
- Provision embedded devices
- Deliver PXE boot images

---

# Communication Workflow

```text
Client

    │

Read Request (RRQ)

or

Write Request (WRQ)

    ▼

TFTP Server

    │

Data Blocks

    ▼

Acknowledgements (ACK)

    ▼

Transfer Complete
```

Unlike FTP, TFTP uses a simple request-response model over UDP.

---

# Packet Types

| Opcode | Description |
|---------|-------------|
| RRQ | Read Request |
| WRQ | Write Request |
| DATA | File Data |
| ACK | Acknowledgement |
| ERROR | Error Message |

---

# File Transfer Process

```text
Client

   │

RRQ

   ▼

Server

   │

DATA Block 1

   ▼

ACK

   │

DATA Block 2

   ▼

ACK

   │

...

   ▼

Final Block

   ▼

Transfer Complete
```

---

# Enterprise Usage

TFTP is frequently used in:

- Cisco infrastructure
- PXE deployment servers
- Network appliances
- IP phone provisioning
- Embedded Linux systems
- Industrial control environments
- Firmware distribution servers

---

# Common TFTP Servers

| Software | Platform |
|-----------|----------|
| tftpd-hpa | Linux |
| atftpd | Linux |
| dnsmasq (TFTP Mode) | Linux |
| SolarWinds TFTP Server | Windows |
| Cisco IOS TFTP Service | Cisco Devices |

---

# Typical Enterprise Architecture

```text
               PXE Server

                   │

             TFTP Service

                   │

        ┌──────────┼──────────┐

        ▼          ▼          ▼

 Workstation   Switch     Router

        │

Boot Image

Configuration

Firmware
```

---

# Common Use Cases

Typical files transferred using TFTP include:

- Router configurations
- Switch configurations
- Firmware images
- Operating system images
- PXE boot files
- BIOS updates
- VoIP phone configuration files

---

# TFTP vs FTP

| Feature | TFTP | FTP |
|----------|------|-----|
| Transport | UDP | TCP |
| Authentication | No | Yes |
| Encryption | No | Optional (FTPS) |
| Directory Listing | No | Yes |
| File Management | Limited | Full |
| Complexity | Very Low | Moderate |

---

# Nmap Detection

Basic UDP Scan

```bash
nmap -sU -p69 target
```

Version Detection

```bash
nmap -sU -sV -p69 target
```

Aggressive Scan

```bash
nmap -sU -A -p69 target
```

---

# Useful NSE Scripts

Retrieve TFTP Information

```bash
nmap --script tftp-enum -p69 target
```

Version Detection

```bash
nmap -sU -sV -p69 target
```

Default Scripts

```bash
nmap -sC -sU -p69 target
```

---

# Example Output

```text
69/udp open tftp
```

Example Enumeration

```text
TFTP Server

Read Requests Allowed

Firmware Repository Available
```

---

# Information That Can Be Collected

TFTP enumeration may reveal:

- TFTP server presence
- Software implementation
- Firmware repository
- Configuration files
- Boot images
- Network device backups
- Accessible filenames
- Read/write permissions

---

# Blue Team Perspective

Recommendations

- Disable TFTP if not required.
- Restrict access to trusted management networks.
- Disable anonymous write access.
- Store sensitive configuration files securely.
- Monitor file transfer activity.
- Use secure alternatives where possible.
- Limit firewall exposure.
- Regularly audit accessible files.

---

# Red Team Perspective

Interesting Targets

- PXE servers
- Cisco configuration repositories
- VoIP provisioning servers
- Firmware repositories
- Industrial controllers
- Embedded Linux systems
- Network appliance management servers

Useful Enumeration

```bash
nmap -sU -sV \
--script tftp-enum \
-p69 target
```

Potential Findings

- Downloadable configuration files
- Firmware images
- Device backup files
- Network architecture information
- Default boot images
- Accessible provisioning files

---

# Common Security Risks

Frequently observed TFTP weaknesses include:

- No authentication
- No encryption
- Unauthorized file downloads
- Unauthorized file uploads
- Firmware disclosure
- Configuration leakage
- Weak access controls
- Internet exposure

---

# PXE Boot and TFTP

One of the most common enterprise uses of TFTP is **PXE booting**, where a computer downloads boot files from a TFTP server before an operating system is installed.

```text
Client

    │

DHCP Request

    ▼

DHCP Server

    │

PXE Information

    ▼

TFTP Server

    │

Boot Loader

    ▼

Operating System Installer
```

This process is widely used for automated operating system deployment in enterprise environments.

---

# Best Practices

- Restrict TFTP to isolated management networks.
- Disable write operations unless operationally necessary.
- Replace TFTP with secure alternatives where feasible.
- Monitor file access logs.
- Limit accessible directories.
- Protect firmware repositories.
- Apply the principle of least privilege.
- Regularly review server configurations.

---

# Real-World Examples

| Environment | Typical TFTP Usage |
|-------------|-------------------|
| Cisco Network | Configuration Backup |
| Enterprise PXE Server | OS Deployment |
| VoIP Infrastructure | Phone Provisioning |
| Industrial Controller | Firmware Updates |
| Embedded Device | Boot Image Distribution |
| Data Center | Network Device Recovery |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| TFTP | Lightweight File Transfer | 69 |
| FTP | File Transfer | 21 |
| FTPS | Secure FTP | 990 / 21 |
| SFTP | Secure File Transfer | 22 |
| DHCP | PXE Boot Support | 67 / 68 |

---

# Summary

TFTP is a simple, connectionless protocol designed for lightweight file transfers in trusted environments. It is commonly used for firmware distribution, PXE booting, and network device configuration management. However, because it lacks authentication and encryption, improperly secured TFTP servers can expose sensitive files and configuration data. During reconnaissance, discovering an accessible TFTP service may provide valuable information about an organization's infrastructure. Administrators should restrict TFTP access, disable unnecessary write capabilities, and migrate to secure alternatives whenever practical.

---

# Chapter 23 — RTP (Real-time Transport Protocol)

## Overview

**Real-time Transport Protocol (RTP)** is an application-layer protocol designed to deliver real-time audio and video across IP networks.

Unlike SIP, which establishes and manages communication sessions, RTP is responsible for **transporting the actual multimedia data** between participants.

RTP is widely used in:

- Voice over IP (VoIP)
- Video conferencing
- Live streaming
- IP cameras
- Telemedicine
- Online gaming
- Video surveillance
- Unified communications

RTP is typically accompanied by **RTCP (Real-time Transport Control Protocol)**, which provides quality statistics, synchronization information, and feedback about media streams.

Because RTP usually carries sensitive voice or video traffic, securing these streams is an important consideration in enterprise environments.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Real-time Transport Protocol |
| RFC | RFC 3550 |
| Transport | UDP |
| Default Port | Dynamic (typically 16384–32767) |
| Encryption | Optional (SRTP) |
| Application Layer | Yes |

---

# Primary Purpose

RTP is designed to:

- Transport voice traffic
- Transport video streams
- Deliver real-time multimedia
- Minimize transmission latency
- Synchronize media playback
- Support interactive communication

---

# RTP Communication Workflow

```text
Caller

    │

SIP Signaling

    ▼

Call Established

    │

RTP Stream

    ▼

Receiver

    │

Voice

Video

Playback
```

SIP establishes the session.

RTP carries the media.

---

# RTP Packet Structure

A simplified RTP packet consists of:

```text
+------------------------------+

RTP Header

+------------------------------+

Payload (Audio / Video)

+------------------------------+
```

The header typically includes:

- Version
- Sequence Number
- Timestamp
- Synchronization Source (SSRC)
- Payload Type

---

# RTP Session Flow

```text
Caller

    │

INVITE (SIP)

    ▼

PBX

    │

200 OK

    ▼

ACK

    │

──────── RTP Audio ───────►

◄────── RTP Audio ─────────

    │

Conversation

    │

BYE
```

---

# Enterprise Usage

RTP is commonly deployed in:

- Enterprise PBX systems
- Cloud telephony
- Contact centers
- Video conferencing
- Security camera systems
- Remote learning platforms
- Live broadcasting
- Medical communication systems

---

# Common RTP Applications

| Software | Platform |
|-----------|----------|
| Asterisk | Linux |
| FreeSWITCH | Cross-platform |
| Cisco Unified Communications | Cisco |
| Zoom | Cross-platform |
| Microsoft Teams | Cross-platform |
| Jitsi Meet | Cross-platform |

---

# RTP vs RTCP

| Feature | RTP | RTCP |
|----------|-----|------|
| Audio Transport | Yes | No |
| Video Transport | Yes | No |
| Quality Reports | No | Yes |
| Synchronization | Limited | Yes |
| Statistics | No | Yes |
| Control Messages | No | Yes |

---

# RTP vs SIP

| Feature | RTP | SIP |
|----------|-----|-----|
| Session Establishment | No | Yes |
| Voice Transport | Yes | No |
| Video Transport | Yes | No |
| Authentication | No | Yes |
| Media Streaming | Yes | No |

---

# Dynamic Ports

Unlike many application protocols, RTP does **not** use a fixed port.

Common ranges include:

| Platform | Typical Port Range |
|-----------|-------------------|
| Asterisk | 10000–20000 |
| Cisco CUCM | Dynamic |
| Microsoft Teams | Dynamic |
| Linux PBX | Configurable |
| Enterprise Firewalls | Configurable |

This dynamic behavior can complicate firewall configuration and network monitoring.

---

# Nmap Detection

Since RTP uses dynamically negotiated UDP ports, discovering RTP streams directly with Nmap is often difficult.

Typical discovery focuses on the associated SIP service.

Example SIP Scan

```bash
nmap -sU -p5060 target
```

UDP Port Range Scan

```bash
nmap -sU -p10000-20000 target
```

Version Detection

```bash
nmap -sU -sV target
```

---

# Useful NSE Scripts

There are currently no commonly used dedicated NSE scripts for RTP enumeration.

Instead, security assessments typically enumerate:

- SIP servers
- PBX systems
- VoIP gateways
- Media servers

Relevant scripts include:

```bash
sip-methods
sip-enum-users
banner
```

---

# Example Output

Example UDP Scan

```text
10000/udp open unknown

10012/udp open unknown

10018/udp open unknown
```

When correlated with SIP infrastructure, these ports may represent active RTP streams.

---

# Information That Can Be Collected

Direct RTP enumeration is limited.

However, surrounding infrastructure may reveal:

- PBX software
- Dynamic media ports
- Codec negotiation
- Session duration
- Call endpoints
- Media gateway information
- Streaming services

---

# Common RTP Codecs

| Codec | Typical Usage |
|---------|--------------|
| G.711 | Enterprise Telephony |
| G.722 | HD Voice |
| G.729 | Low Bandwidth Voice |
| Opus | Modern VoIP |
| H.264 | Video |
| VP8 | Video Conferencing |

---

# Blue Team Perspective

Recommendations

- Encrypt media streams using SRTP.
- Restrict RTP traffic with firewall rules.
- Monitor abnormal UDP traffic.
- Separate voice traffic using VLANs.
- Disable unused codecs.
- Keep PBX software updated.
- Use secure SIP signaling with TLS.
- Monitor media quality and packet loss.

---

# Red Team Perspective

Interesting Targets

- PBX servers
- VoIP gateways
- Video conferencing platforms
- SIP infrastructure
- Session Border Controllers
- Contact center systems

Useful Enumeration

```bash
nmap -sU \
-p5060,10000-20000 \
target
```

Potential Findings

- Dynamic media ports
- VoIP infrastructure
- Active call sessions
- Media gateways
- Codec support
- Voice VLAN identification

---

# Common Security Risks

Frequently observed RTP weaknesses include:

- Unencrypted media streams
- Voice eavesdropping
- Packet injection
- RTP spoofing
- Denial-of-Service attacks
- Poor network segmentation
- Weak SIP security
- Codec downgrade attacks

---

# Secure RTP (SRTP)

**Secure Real-time Transport Protocol (SRTP)** extends RTP by adding:

- Encryption
- Message authentication
- Integrity protection
- Replay attack prevention

```text
Standard RTP

Audio

────────────►

Anyone on the network may capture packets.


Secure RTP (SRTP)

Encrypted Audio

────────────►

Only authorized endpoints can decrypt the media.
```

SRTP is recommended for all enterprise VoIP deployments.

---

# Best Practices

- Deploy SRTP for all media streams.
- Use SIP over TLS for signaling.
- Restrict RTP port ranges.
- Isolate voice networks using dedicated VLANs.
- Monitor abnormal UDP traffic.
- Keep VoIP infrastructure updated.
- Disable unnecessary codecs.
- Perform regular security assessments.

---

# Real-World Examples

| Environment | Typical RTP Usage |
|-------------|-------------------|
| Enterprise PBX | Voice Calls |
| Contact Center | Customer Conversations |
| Video Conference Platform | Video Streams |
| IP Camera | Live Video |
| Telemedicine | Secure Video Sessions |
| Online Education | Live Classroom Audio/Video |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| RTP | Audio/Video Transport | Dynamic |
| RTCP | RTP Control | Dynamic |
| SIP | Session Signaling | 5060 / 5061 |
| SRTP | Secure RTP | Dynamic |
| H.323 | Multimedia Communication | 1720 |

---

# Summary

RTP is the standard protocol for transporting real-time audio and video across IP networks. It works alongside signaling protocols such as SIP to deliver multimedia content with low latency. Although RTP itself exposes limited information during reconnaissance, identifying RTP traffic can reveal active VoIP or video infrastructure. Because standard RTP does not provide encryption, organizations should deploy SRTP, secure SIP signaling with TLS, segment voice networks, and continuously monitor media traffic for unauthorized activity.

---

# Chapter 24 — RTSP (Real-Time Streaming Protocol)

## Overview

**Real-Time Streaming Protocol (RTSP)** is an application-layer protocol used to establish and control multimedia streaming sessions across IP networks.

Unlike RTP, which transports the actual audio and video data, RTSP is responsible for **controlling the media session**. It allows a client to issue commands such as play, pause, stop, or seek while the media itself is typically delivered using RTP or another streaming protocol.

RTSP is widely deployed in:

- IP surveillance cameras
- Network Video Recorders (NVR)
- Digital Video Recorders (DVR)
- Smart home devices
- Video streaming servers
- Industrial monitoring systems
- Broadcasting infrastructure

Because many IP cameras expose RTSP services with weak authentication or default credentials, RTSP is one of the most frequently encountered protocols during network reconnaissance.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Real-Time Streaming Protocol |
| Default Port | TCP 554 |
| Secure Port | RTSPS (Vendor Dependent) |
| Transport | TCP |
| Encryption | Optional |
| RFC | RFC 2326, RFC 7826 |
| Application Layer | Yes |

---

# Primary Purpose

RTSP is designed to:

- Establish streaming sessions
- Control media playback
- Pause video streams
- Resume playback
- Terminate sessions
- Negotiate multimedia delivery
- Manage surveillance camera streams

---

# RTSP Architecture

```text
              RTSP Client

                   │

          PLAY / PAUSE / TEARDOWN

                   ▼

              RTSP Server

                   │

         RTP Audio / Video Stream

                   ▼

              Media Player
```

---

# Communication Workflow

```text
Client

   │

OPTIONS

   ▼

RTSP Server

   │

DESCRIBE

   ▼

Session Information

   │

SETUP

   ▼

Media Session

   │

PLAY

   ▼

RTP Stream

   │

TEARDOWN

   ▼

Session Closed
```

---

# Common RTSP Methods

| Method | Purpose |
|----------|----------|
| OPTIONS | Query Supported Methods |
| DESCRIBE | Retrieve Stream Description |
| SETUP | Initialize Session |
| PLAY | Start Streaming |
| PAUSE | Pause Stream |
| RECORD | Upload Media (Optional) |
| ANNOUNCE | Update Session |
| TEARDOWN | Close Session |

---

# Typical Enterprise Usage

RTSP is commonly found in:

- CCTV systems
- Smart buildings
- Industrial monitoring
- Traffic cameras
- Security control rooms
- Broadcast studios
- Video analytics platforms
- Remote surveillance systems

---

# Common RTSP Servers

| Software | Platform |
|-----------|----------|
| Live555 Media Server | Cross-platform |
| GStreamer RTSP Server | Linux |
| VLC Streaming Server | Cross-platform |
| FFmpeg RTSP Server | Cross-platform |
| Axis Camera Firmware | Embedded |
| Hikvision Firmware | Embedded |
| Dahua Firmware | Embedded |

---

# Typical Enterprise Architecture

```text
             Security Cameras

          ┌────────┴────────┐

          │                 │

     Camera 1          Camera 2

          │                 │

          └────────┬────────┘

                   │

             RTSP Streams

                   ▼

          Network Video Recorder

                   │

             Security Console
```

---

# RTSP URLs

RTSP streams are commonly accessed using URLs such as:

```text
rtsp://camera-ip/live

rtsp://camera-ip:554/stream

rtsp://username:password@camera-ip/live
```

Some vendors use custom paths for different channels or stream qualities.

---

# Authentication Methods

RTSP implementations commonly support:

- No authentication
- Basic Authentication
- Digest Authentication
- Vendor-specific authentication
- Token-based authentication (modern platforms)

---

# Nmap Detection

Basic Scan

```bash
nmap -p554 target
```

Version Detection

```bash
nmap -sV -p554 target
```

Aggressive Scan

```bash
nmap -A -p554 target
```

Default Scripts

```bash
nmap -sC -sV -p554 target
```

---

# Useful NSE Scripts

Retrieve RTSP Methods

```bash
nmap --script rtsp-methods -p554 target
```

Retrieve Banner

```bash
nmap --script banner -p554 target
```

Version Detection

```bash
nmap -sV -p554 target
```

---

# Example Output

```text
554/tcp open rtsp
```

Example Enumeration

```text
Supported Methods

OPTIONS

DESCRIBE

SETUP

PLAY

PAUSE

TEARDOWN
```

---

# Information That Can Be Collected

RTSP enumeration may reveal:

- Camera vendor
- Device model
- Firmware version
- Supported RTSP methods
- Authentication type
- Stream paths
- Video channels
- Media formats
- Software implementation

---

# Blue Team Perspective

Recommendations

- Disable anonymous RTSP access.
- Change default camera credentials.
- Restrict RTSP access using firewalls.
- Use VPNs for remote surveillance.
- Update camera firmware regularly.
- Disable unused services.
- Segment surveillance networks.
- Monitor access attempts.

---

# Red Team Perspective

Interesting Targets

- IP cameras
- NVR systems
- DVR systems
- Smart home hubs
- Industrial monitoring systems
- Building management systems
- Video analytics servers

Useful Enumeration

```bash
nmap -sV \
--script rtsp-methods,banner \
-p554 target
```

Potential Findings

- Camera manufacturer
- Firmware version
- Stream endpoints
- Authentication methods
- Default configuration
- Accessible media streams

---

# Common Security Risks

Frequently observed RTSP weaknesses include:

- Default credentials
- Anonymous streaming
- Internet-exposed cameras
- Outdated firmware
- Weak authentication
- Information disclosure
- Unencrypted media streams
- Vendor-specific vulnerabilities

---

# RTSP vs RTP

| Feature | RTSP | RTP |
|----------|------|-----|
| Session Control | Yes | No |
| Media Transport | No | Yes |
| Playback Commands | Yes | No |
| Audio Transport | No | Yes |
| Video Transport | No | Yes |
| Default Port | 554 | Dynamic |

---

# Best Practices

- Require authentication for all RTSP streams.
- Replace default credentials immediately.
- Keep firmware updated.
- Disable unused camera services.
- Place surveillance devices on isolated VLANs.
- Use VPN access for remote viewing.
- Restrict access to trusted hosts.
- Regularly audit exposed RTSP endpoints.

---

# Real-World Examples

| Environment | Typical RTSP Usage |
|-------------|-------------------|
| Corporate CCTV | Live Camera Streams |
| Hospital | Patient Area Monitoring |
| Airport | Security Surveillance |
| Smart City | Traffic Cameras |
| Manufacturing | Production Monitoring |
| Warehouse | Asset Protection |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| RTSP | Stream Control | 554 |
| RTP | Audio/Video Transport | Dynamic |
| RTCP | Stream Statistics | Dynamic |
| SIP | Session Signaling | 5060 |
| HTTP | Web-Based Streaming | 80 |

---

# Summary

RTSP is the primary protocol for controlling multimedia streaming sessions, particularly in IP surveillance and video distribution systems. While RTP transports the actual media, RTSP manages session establishment, playback, and termination. During reconnaissance, RTSP services can reveal valuable information about camera vendors, firmware versions, supported methods, and stream configurations. Organizations should secure RTSP deployments by enforcing authentication, disabling anonymous access, isolating surveillance networks, and keeping device firmware up to date.

---

# Chapter 25 — MQTT (Message Queuing Telemetry Transport)

## Overview

**Message Queuing Telemetry Transport (MQTT)** is a lightweight publish/subscribe messaging protocol designed for devices with limited computing power, low bandwidth, or unreliable network connections.

Originally developed for remote monitoring in the oil and gas industry, MQTT has become one of the most widely used protocols in the **Internet of Things (IoT)** ecosystem.

Today, MQTT is commonly found in:

- Smart homes
- Industrial IoT (IIoT)
- Smart factories
- Environmental monitoring
- Healthcare devices
- Connected vehicles
- Agriculture systems
- Cloud IoT platforms

Unlike HTTP's request-response model, MQTT uses a **broker-based publish/subscribe architecture**, allowing devices to exchange messages efficiently without direct communication.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Message Queuing Telemetry Transport |
| Default Port | TCP 1883 |
| Secure Port | TCP 8883 (MQTT over TLS) |
| Transport | TCP |
| Encryption | Optional (TLS) |
| Current Standard | MQTT 5.0 |
| Application Layer | Yes |

---

# Primary Purpose

MQTT enables systems to:

- Exchange telemetry data
- Deliver IoT sensor readings
- Control smart devices
- Monitor industrial equipment
- Trigger automation workflows
- Exchange real-time events
- Minimize bandwidth usage

---

# MQTT Architecture

```text
               MQTT Broker

           (Message Server)

          ┌──────┼──────┐

          │      │      │

     Client A Client B Client C

      Publish Subscribe Publish

          │      │      │

          └──────┼──────┘

            Topic-Based Messaging
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Broker | Central message server |
| Publisher | Sends messages |
| Subscriber | Receives messages |
| Topic | Message category |
| Client | Any MQTT-enabled device |

---

# Communication Workflow

```text
Temperature Sensor

        │

Publish

        ▼

Topic:

factory/temp

        ▼

MQTT Broker

        │

Distribute Message

        ▼

Subscribers

Dashboard

Alarm System

Database
```

---

# Publish/Subscribe Model

Unlike HTTP:

```text
HTTP

Client

   │

Request

   ▼

Server

   │

Response

   ▼

Client
```

MQTT uses:

```text
Publisher

     │

Publish

     ▼

Broker

     │

Topic

     ▼

Subscribers
```

Publishers and subscribers never communicate directly.

---

# Topics

Messages are organized into **topics**.

Examples:

```text
home/livingroom/light

factory/line1/temperature

building/floor2/hvac

vehicles/car001/location

hospital/room5/heart-rate
```

Topics may include hierarchical levels separated by `/`.

---

# Wildcards

MQTT supports wildcard subscriptions.

| Wildcard | Purpose |
|----------|----------|
| + | Single Level |
| # | Multiple Levels |

Examples:

```text
factory/+/temperature

factory/#

home/#
```

---

# Quality of Service (QoS)

MQTT supports three Quality of Service levels.

| QoS | Description |
|------|-------------|
| 0 | At most once |
| 1 | At least once |
| 2 | Exactly once |

Higher QoS provides greater delivery reliability at the cost of additional protocol overhead.

---

# Enterprise Usage

MQTT is widely deployed in:

- Smart factories
- Building automation
- Energy management
- Smart cities
- Connected vehicles
- Healthcare monitoring
- Retail analytics
- Cloud IoT platforms

---

# Common MQTT Brokers

| Software | Platform |
|-----------|----------|
| Eclipse Mosquitto | Cross-platform |
| EMQX | Cross-platform |
| HiveMQ | Enterprise |
| RabbitMQ (MQTT Plugin) | Cross-platform |
| VerneMQ | Cross-platform |
| AWS IoT Core | Cloud |
| Azure IoT Hub | Cloud |

---

# Typical Enterprise Architecture

```text
          IoT Sensors

      ┌──────┼──────┐

      ▼      ▼      ▼

 Temperature Motion Humidity

      │

 Publish

      ▼

 MQTT Broker

      │

      ├─────────────┐

      ▼             ▼

 Database     Monitoring

                    │

             Alert System
```

---

# Nmap Detection

Basic Scan

```bash
nmap -p1883 target
```

Secure MQTT

```bash
nmap -p8883 target
```

Version Detection

```bash
nmap -sV -p1883 target
```

Aggressive Scan

```bash
nmap -A -p1883 target
```

---

# Useful NSE Scripts

Retrieve MQTT Information

```bash
nmap --script mqtt-subscribe -p1883 target
```

Retrieve Banner

```bash
nmap --script banner -p1883 target
```

Version Detection

```bash
nmap -sV -p1883 target
```

> **Note:** NSE support for MQTT is more limited than for protocols such as HTTP or SMB. Many assessments rely on version detection, banner grabbing, and specialized MQTT client tools for deeper enumeration.

---

# Example Output

```text
1883/tcp open mqtt
```

Example Banner

```text
MQTT Broker

Protocol Version:

MQTT 5.0

Server:

Eclipse Mosquitto
```

---

# Information That Can Be Collected

MQTT enumeration may reveal:

- Broker software
- Protocol version
- Supported authentication
- TLS availability
- Broker banner
- Topic structure (when authorized)
- Client identifiers
- Connected devices

---

# Blue Team Perspective

Recommendations

- Require client authentication.
- Enable TLS (TCP 8883).
- Disable anonymous access.
- Apply topic-based access controls.
- Monitor broker logs.
- Restrict broker exposure.
- Rotate credentials regularly.
- Keep broker software updated.

---

# Red Team Perspective

Interesting Targets

- Smart factories
- IoT gateways
- Building automation systems
- Cloud IoT brokers
- Smart energy platforms
- Healthcare IoT devices
- Industrial monitoring systems

Useful Enumeration

```bash
nmap -sV \
--script banner,mqtt-subscribe \
-p1883 target
```

Potential Findings

- Broker software
- Anonymous access
- Topic names
- Device identifiers
- Authentication configuration
- Broker version
- Cloud integration

---

# Common Security Risks

Frequently observed MQTT weaknesses include:

- Anonymous connections
- Unencrypted communication
- Weak credentials
- Excessive topic permissions
- Internet-exposed brokers
- Insecure IoT firmware
- Missing access controls
- Information disclosure

---

# MQTT vs HTTP

| Feature | MQTT | HTTP |
|----------|------|------|
| Communication Model | Publish/Subscribe | Request/Response |
| Overhead | Very Low | Higher |
| Persistent Connection | Yes | Optional |
| IoT Optimized | Yes | Limited |
| Broker Required | Yes | No |
| Default Port | 1883 | 80 |

---

# Best Practices

- Enable TLS for all MQTT communications.
- Disable anonymous authentication.
- Apply least-privilege topic permissions.
- Monitor broker activity continuously.
- Segment IoT networks from enterprise systems.
- Keep broker software and device firmware updated.
- Audit connected clients regularly.
- Use strong authentication mechanisms.

---

# Real-World Examples

| Environment | Typical MQTT Usage |
|-------------|-------------------|
| Smart Home | Lighting Control |
| Manufacturing | Machine Telemetry |
| Agriculture | Soil Monitoring |
| Hospital | Medical Sensor Data |
| Smart City | Traffic Monitoring |
| Energy Grid | Smart Meter Communication |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| MQTT | IoT Messaging | 1883 / 8883 |
| HTTP | Web Communication | 80 |
| HTTPS | Secure Web Communication | 443 |
| AMQP | Enterprise Messaging | 5672 |
| CoAP | Constrained IoT Devices | 5683 |

---

# Summary

MQTT is a lightweight messaging protocol optimized for IoT and machine-to-machine communication. Its publish/subscribe architecture enables efficient message distribution through a central broker, making it ideal for bandwidth-constrained and resource-limited environments. During reconnaissance, MQTT services may reveal broker software, protocol versions, authentication mechanisms, and topic structures. Organizations should secure MQTT deployments by enforcing TLS, disabling anonymous access, implementing topic-level authorization, and continuously monitoring broker activity.

---

# Chapter 26 — AMQP (Advanced Message Queuing Protocol)

## Overview

**Advanced Message Queuing Protocol (AMQP)** is an open standard application-layer protocol designed for reliable, secure, and interoperable message-oriented middleware.

Unlike lightweight messaging protocols such as MQTT, AMQP provides advanced messaging capabilities including:

- Reliable message delivery
- Message routing
- Transactions
- Queue management
- Publisher acknowledgements
- Consumer acknowledgements
- High availability
- Enterprise integration

AMQP is widely used in enterprise software, financial systems, cloud platforms, distributed applications, and microservice architectures where reliable communication between applications is critical.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Advanced Message Queuing Protocol |
| Default Port | TCP 5672 |
| Secure Port | TCP 5671 (TLS) |
| Transport | TCP |
| Encryption | Optional (TLS) |
| Current Standard | AMQP 1.0 |
| Application Layer | Yes |

---

# Primary Purpose

AMQP enables applications to:

- Exchange messages reliably
- Decouple distributed systems
- Process asynchronous tasks
- Build event-driven architectures
- Queue background jobs
- Balance workloads
- Integrate enterprise applications

---

# AMQP Architecture

```text
        Producer

           │

        Publish

           ▼

        Exchange

           │

 ┌─────────┼─────────┐

 ▼         ▼         ▼

Queue A  Queue B  Queue C

 │         │         │

 ▼         ▼         ▼

Consumer Consumer Consumer
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Producer | Sends messages |
| Exchange | Routes messages |
| Queue | Stores messages |
| Consumer | Processes messages |
| Binding | Connects exchanges and queues |
| Broker | Central messaging server |

---

# Communication Workflow

```text
Application A

      │

Publish Message

      ▼

AMQP Broker

      │

Exchange

      │

Routing

      ▼

Queue

      │

Consumer

      ▼

Application B
```

---

# Exchange Types

AMQP exchanges determine how messages are routed.

| Exchange Type | Description |
|---------------|-------------|
| Direct | Exact routing key match |
| Fanout | Broadcast to all queues |
| Topic | Pattern-based routing |
| Headers | Route using message headers |

---

# Message Lifecycle

```text
Producer

    │

Publish

    ▼

Exchange

    │

Routing Key

    ▼

Queue

    │

Store Message

    ▼

Consumer

    │

ACK

    ▼

Message Removed
```

---

# Routing Keys

Routing keys determine which queue receives a message.

Example:

```text
orders.created

orders.updated

payments.completed

inventory.low

alerts.security
```

---

# Enterprise Usage

AMQP is commonly deployed in:

- Banking systems
- Financial trading platforms
- E-commerce platforms
- Microservices
- Cloud-native applications
- ERP systems
- Healthcare systems
- Logistics platforms

---

# Common AMQP Brokers

| Software | Platform |
|-----------|----------|
| RabbitMQ | Cross-platform |
| Apache ActiveMQ | Cross-platform |
| Apache Qpid | Cross-platform |
| Azure Service Bus | Cloud |
| Red Hat AMQ | Enterprise |
| IBM MQ | Enterprise |

---

# Typical Enterprise Architecture

```text
        Web Application

              │

         Publish Event

              ▼

        RabbitMQ Cluster

      ┌──────┼──────┐

      ▼      ▼      ▼

 Orders Inventory Billing

      ▼      ▼      ▼

 Worker  Worker  Worker

              │

          Database
```

---

# Reliable Delivery

AMQP supports several reliability mechanisms.

| Feature | Purpose |
|----------|----------|
| ACK | Confirm message processing |
| Durable Queues | Survive broker restart |
| Persistent Messages | Survive failures |
| Transactions | Atomic operations |
| Dead Letter Queue | Handle failed messages |

These features make AMQP suitable for mission-critical applications.

---

# AMQP vs MQTT

| Feature | AMQP | MQTT |
|----------|------|------|
| Enterprise Messaging | Yes | Limited |
| IoT Optimized | No | Yes |
| Routing | Advanced | Basic |
| Transactions | Yes | No |
| Queue Support | Yes | Limited |
| Reliability | Very High | Moderate |

---

# Nmap Detection

Basic Scan

```bash
nmap -p5672 target
```

Secure AMQP

```bash
nmap -p5671 target
```

Version Detection

```bash
nmap -sV -p5672 target
```

Aggressive Scan

```bash
nmap -A -p5672 target
```

---

# Useful NSE Scripts

Retrieve Banner

```bash
nmap --script banner -p5672 target
```

Version Detection

```bash
nmap -sV -p5672 target
```

Default Scripts

```bash
nmap -sC -sV -p5672 target
```

> **Note:** Nmap currently provides limited protocol-specific NSE support for AMQP. Deeper inspection is generally performed using AMQP-aware clients and broker management interfaces.

---

# Example Output

```text
5672/tcp open amqp
```

Example Banner

```text
RabbitMQ

AMQP 0-9-1

TLS Supported
```

---

# Information That Can Be Collected

AMQP enumeration may reveal:

- Broker software
- Protocol version
- TLS support
- Product banner
- Vendor information
- Management interfaces
- Authentication mechanisms
- Cluster configuration hints

---

# Blue Team Perspective

Recommendations

- Enable TLS for broker communications.
- Require strong client authentication.
- Disable anonymous connections.
- Restrict broker access using firewalls.
- Monitor queue activity.
- Apply role-based access control (RBAC).
- Keep broker software updated.
- Audit message permissions regularly.

---

# Red Team Perspective

Interesting Targets

- RabbitMQ clusters
- Enterprise integration platforms
- Financial systems
- Kubernetes applications
- Microservice environments
- Cloud messaging platforms

Useful Enumeration

```bash
nmap -sV \
--script banner \
-p5672 target
```

Potential Findings

- RabbitMQ version
- Broker implementation
- TLS availability
- Authentication methods
- Management endpoints
- Cluster information
- Enterprise integration services

---

# Common Security Risks

Frequently observed AMQP weaknesses include:

- Anonymous broker access
- Weak authentication
- Unencrypted communication
- Internet-exposed brokers
- Misconfigured permissions
- Excessive administrative privileges
- Outdated broker software
- Information disclosure through management interfaces

---

# High Availability

AMQP brokers commonly operate in clustered environments.

```text
        Load Balancer

             │

     ┌───────┼────────┐

     ▼       ▼        ▼

 Broker1 Broker2 Broker3

     │       │        │

     └───────┼────────┘

         Shared Queues

              │

         Client Applications
```

Clustering improves redundancy, fault tolerance, and scalability.

---

# Best Practices

- Encrypt all broker communications using TLS.
- Disable anonymous logins.
- Enforce least-privilege permissions.
- Separate management interfaces from production networks.
- Monitor queue growth and failed deliveries.
- Enable audit logging.
- Rotate credentials regularly.
- Patch brokers promptly.

---

# Real-World Examples

| Environment | Typical AMQP Usage |
|-------------|-------------------|
| Banking | Transaction Processing |
| E-commerce | Order Processing |
| Microservices | Event Distribution |
| Logistics | Shipment Tracking |
| Healthcare | Laboratory Workflows |
| Cloud Platform | Background Task Processing |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| AMQP | Enterprise Messaging | 5672 / 5671 |
| MQTT | IoT Messaging | 1883 / 8883 |
| STOMP | Simple Messaging | 61613 |
| Kafka | Distributed Event Streaming | 9092 |
| HTTP | Web Communication | 80 |

---

# Summary

AMQP is a feature-rich messaging protocol designed for reliable communication between distributed applications. Its support for queues, exchanges, routing, acknowledgements, and transactions makes it a cornerstone of enterprise messaging systems and microservice architectures. During reconnaissance, AMQP services can reveal broker software, protocol versions, authentication mechanisms, and messaging infrastructure details. Organizations should secure AMQP deployments with TLS, strong authentication, role-based access control, and continuous monitoring to protect critical messaging services.

---

# Chapter 27 — Redis

## Overview

**Redis (Remote Dictionary Server)** is an open-source, in-memory data structure store that functions as a database, cache, message broker, and streaming engine.

Unlike traditional relational databases that primarily store data on disk, Redis keeps data in memory, enabling **extremely low-latency read and write operations**.

Redis is widely used in modern software architectures for:

- Caching
- Session storage
- Real-time analytics
- Rate limiting
- Distributed locking
- Pub/Sub messaging
- Job queues
- Leaderboards

Because Redis often contains sensitive application data and is sometimes deployed without authentication, it has become a frequent target during penetration tests.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Remote Dictionary Server |
| Default Port | TCP 6379 |
| Cluster Bus Port | TCP 16379 |
| Transport | TCP |
| Encryption | Optional (TLS) |
| Authentication | Optional (ACLs / Password) |
| Application Layer | Yes |

---

# Primary Purpose

Redis is designed to:

- Cache frequently accessed data
- Store user sessions
- Improve application performance
- Manage queues
- Support real-time messaging
- Store temporary data
- Process streams
- Coordinate distributed systems

---

# Redis Architecture

```text
            Client Applications

        ┌────────┼────────┐

        ▼        ▼        ▼

     Web API  Worker   Backend

                │

          TCP 6379

                ▼

          Redis Server

                │

     In-Memory Data Store
```

---

# Supported Data Structures

Redis supports far more than simple key-value pairs.

| Data Type | Purpose |
|------------|----------|
| String | Basic values |
| Hash | Objects |
| List | Ordered collections |
| Set | Unique values |
| Sorted Set | Rankings |
| Stream | Event streams |
| Bitmap | Bit operations |
| HyperLogLog | Cardinality estimation |
| Geo | Geographic indexing |

---

# Communication Workflow

```text
Application

      │

GET user:1001

      ▼

Redis

      │

Lookup

      ▼

Return Value

      │

Application
```

Write operation:

```text
Application

      │

SET session:abc123

      ▼

Redis

      │

Store In Memory

      ▼

OK
```

---

# Common Redis Commands

| Command | Description |
|----------|-------------|
| GET | Retrieve value |
| SET | Store value |
| DEL | Delete key |
| EXISTS | Check key |
| KEYS | List keys |
| EXPIRE | Set expiration |
| TTL | Remaining lifetime |
| INFO | Server information |
| CONFIG | Server configuration |
| PING | Connectivity test |

---

# Enterprise Usage

Redis is commonly deployed in:

- Web applications
- Microservices
- E-commerce platforms
- Gaming platforms
- Financial applications
- Cloud-native environments
- Kubernetes clusters
- API gateways

---

# Common Redis Implementations

| Software | Platform |
|-----------|----------|
| Redis Open Source | Cross-platform |
| Redis Enterprise | Enterprise |
| Valkey | Cross-platform |
| Amazon ElastiCache | AWS |
| Azure Cache for Redis | Microsoft Azure |

---

# Typical Enterprise Architecture

```text
             Internet

                 │

          Load Balancer

                 │

        Web Application

                 │

        ┌────────┴────────┐

        ▼                 ▼

     Redis Cache      SQL Database

        │

 Session Storage

 Rate Limiting

 Pub/Sub
```

---

# Persistence Options

Although Redis is primarily an in-memory database, it supports persistence.

| Method | Description |
|----------|-------------|
| RDB | Point-in-time snapshots |
| AOF | Append Only File |
| Hybrid | Snapshot + AOF |

Persistence improves durability while maintaining high performance.

---

# Replication

Redis supports replication for redundancy.

```text
           Primary

              │

     ┌────────┼────────┐

     ▼        ▼        ▼

 Replica 1 Replica 2 Replica 3
```

Replicas can improve read scalability and availability.

---

# Redis Cluster

Large deployments often use Redis Cluster.

```text
          Redis Cluster

     ┌────────┬────────┐

     ▼        ▼        ▼

   Node 1   Node 2   Node 3

        Automatic Sharding
```

The cluster distributes keys across multiple nodes for scalability.

---

# Nmap Detection

Basic Scan

```bash
nmap -p6379 target
```

Version Detection

```bash
nmap -sV -p6379 target
```

Aggressive Scan

```bash
nmap -A -p6379 target
```

---

# Useful NSE Scripts

Retrieve Redis Information

```bash
nmap --script redis-info -p6379 target
```

Brute Force Authentication (Authorized Testing Only)

```bash
nmap --script redis-brute -p6379 target
```

Retrieve Banner

```bash
nmap --script banner -p6379 target
```

---

# Example Output

```text
6379/tcp open redis
```

Example Enumeration

```text
Redis Version:

7.2.0

Role:

master

Connected Clients:

12

Authentication:

Disabled
```

---

# Information That Can Be Collected

Redis enumeration may reveal:

- Redis version
- Authentication status
- Server role
- Connected clients
- Memory usage
- Persistence configuration
- Operating system
- Replication status
- Cluster information

---

# Blue Team Perspective

Recommendations

- Require authentication using ACLs.
- Enable TLS where supported.
- Disable dangerous administrative commands when appropriate.
- Restrict Redis access to trusted networks.
- Disable Internet exposure.
- Monitor client connections.
- Keep Redis updated.
- Enable logging and auditing.

---

# Red Team Perspective

Interesting Targets

- Session stores
- API gateways
- Kubernetes applications
- Cloud environments
- E-commerce platforms
- Authentication services
- Caching servers

Useful Enumeration

```bash
nmap -sV \
--script redis-info,banner \
-p6379 target
```

Potential Findings

- Redis version
- Anonymous access
- Server role
- Cluster topology
- Replication settings
- Connected client count
- Persistence configuration

---

# Common Security Risks

Frequently observed Redis weaknesses include:

- No authentication
- Internet-exposed Redis instances
- Weak passwords
- Unencrypted communication
- Dangerous administrative commands
- Sensitive cached data
- Misconfigured ACLs
- Outdated Redis versions

---

# Authentication

Modern Redis versions support Access Control Lists (ACLs).

```text
Client

   │

AUTH username password

   ▼

Redis Server

   │

Permission Verification

   ▼

Authorized Commands
```

Older deployments often relied on a single shared password or no authentication at all.

---

# Redis Pub/Sub

Redis also supports publish/subscribe messaging.

```text
Publisher

     │

Publish

     ▼

Redis Channel

     │

     ▼

Subscriber A

Subscriber B

Subscriber C
```

This feature is commonly used for notifications, chat applications, and real-time event processing.

---

# Best Practices

- Enable authentication and ACLs.
- Encrypt traffic with TLS.
- Restrict administrative commands.
- Disable public network exposure.
- Segment Redis servers from client networks.
- Monitor unusual commands and connections.
- Keep Redis software updated.
- Perform regular configuration reviews.

---

# Real-World Examples

| Environment | Typical Redis Usage |
|-------------|--------------------|
| E-commerce | Shopping Cart Cache |
| Social Media | Session Storage |
| Banking | Rate Limiting |
| Gaming | Leaderboards |
| Kubernetes | Distributed Cache |
| API Platform | Token Storage |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Redis | In-Memory Database | 6379 |
| Memcached | Distributed Cache | 11211 |
| AMQP | Enterprise Messaging | 5672 |
| MQTT | IoT Messaging | 1883 |
| HTTP | Web Communication | 80 |

---

# Summary

Redis is one of the most widely deployed in-memory databases and caching platforms in modern software infrastructure. Its exceptional performance, support for multiple data structures, and messaging capabilities make it a key component of cloud-native and distributed applications. During reconnaissance, Redis services can reveal software versions, authentication settings, cluster roles, replication status, and configuration details. Organizations should secure Redis by enabling authentication and ACLs, encrypting communications with TLS, restricting network access, and regularly auditing configurations.

---

# Chapter 28 — Memcached

## Overview

**Memcached** is a high-performance, distributed, in-memory caching system designed to reduce database load and improve application performance.

Unlike Redis, which supports numerous advanced data structures and persistence mechanisms, Memcached focuses on one task:

> **Fast temporary storage of key-value pairs in memory.**

Memcached is commonly deployed in front of relational databases to cache frequently requested information, reducing response times and increasing application scalability.

It is widely used in:

- Web applications
- Content Management Systems (CMS)
- E-commerce platforms
- API gateways
- Social media applications
- Cloud-native services
- High-traffic websites

Since Memcached often stores sensitive application data and historically lacked built-in authentication, improperly exposed servers have frequently been abused in cyber attacks, including large-scale DDoS amplification attacks.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Memcached |
| Default Port | TCP 11211 |
| UDP Port | UDP 11211 (often disabled today) |
| Transport | TCP / UDP |
| Encryption | No (native) |
| Authentication | No (native) |
| Application Layer | Yes |

---

# Primary Purpose

Memcached is designed to:

- Cache database query results
- Reduce application latency
- Minimize database load
- Improve scalability
- Store temporary session data
- Cache API responses
- Increase website performance

---

# Memcached Architecture

```text
            Web Clients

                 │

          HTTP Requests

                 ▼

         Web Application

        ┌────────┴────────┐

        ▼                 ▼

   Memcached         SQL Database

        │

 Cached Objects

 Session Data

 API Responses
```

---

# Communication Workflow

```text
Application

      │

GET user:125

      ▼

Memcached

      │

Cache Hit?

 ┌────┴────┐

 │         │

Yes        No

 │          │

 ▼          ▼

Return    Database

Cached      Query

Data         │

             ▼

         Store Cache

             ▼

        Return Result
```

---

# Common Commands

| Command | Description |
|----------|-------------|
| get | Retrieve value |
| set | Store value |
| add | Store if key does not exist |
| replace | Replace existing value |
| delete | Remove key |
| flush_all | Clear cache |
| stats | Display statistics |
| version | Show server version |

---

# Enterprise Usage

Memcached is commonly deployed in:

- WordPress installations
- Drupal websites
- Magento stores
- Laravel applications
- Django applications
- High-traffic APIs
- SaaS platforms
- Content delivery environments

---

# Common Implementations

| Software | Platform |
|-----------|----------|
| Memcached | Linux |
| Memcached | Windows (Community Ports) |
| AWS ElastiCache for Memcached | AWS |
| Google Cloud Memorystore | Google Cloud |

---

# Typical Enterprise Architecture

```text
            Internet

                │

         Load Balancer

                │

        Web Application

        ┌───────┴────────┐

        ▼                ▼

   Memcached         SQL Database

        │

 Frequently Accessed Data
```

---

# Cache Lifecycle

```text
User Request

      │

Application

      │

Check Cache

      ▼

Cache Miss

      │

Query Database

      ▼

Store Result

      ▼

Future Requests

      ▼

Cache Hit
```

---

# Memcached vs Redis

| Feature | Memcached | Redis |
|----------|-----------|-------|
| In-Memory Storage | Yes | Yes |
| Persistence | No | Yes |
| Data Structures | Strings Only | Multiple Types |
| Replication | No | Yes |
| Clustering | Client-Side | Native |
| Pub/Sub | No | Yes |
| Authentication | No (Native) | Yes |
| Default Port | 11211 | 6379 |

---

# Nmap Detection

Basic Scan

```bash
nmap -p11211 target
```

Version Detection

```bash
nmap -sV -p11211 target
```

Aggressive Scan

```bash
nmap -A -p11211 target
```

TCP Scan

```bash
nmap -sT -p11211 target
```

---

# Useful NSE Scripts

Retrieve Memcached Information

```bash
nmap --script memcached-info -p11211 target
```

Version Detection

```bash
nmap -sV -p11211 target
```

Retrieve Banner

```bash
nmap --script banner -p11211 target
```

---

# Example Output

```text
11211/tcp open memcached
```

Example Enumeration

```text
Version:

1.6.21

Maximum Memory:

2048 MB

Current Connections:

34

Uptime:

12 Days
```

---

# Information That Can Be Collected

Memcached enumeration may reveal:

- Software version
- Cache statistics
- Uptime
- Memory allocation
- Current connections
- Maximum memory
- Cache hit ratio
- Server implementation

---

# Blue Team Perspective

Recommendations

- Never expose Memcached directly to the Internet.
- Disable UDP support unless absolutely required.
- Restrict access using firewalls.
- Deploy Memcached only on internal networks.
- Monitor cache statistics.
- Upgrade to supported versions.
- Protect administrative access.
- Use network segmentation.

---

# Red Team Perspective

Interesting Targets

- Web application caches
- E-commerce platforms
- API gateways
- Cloud-native applications
- SaaS platforms
- Enterprise portals
- CMS environments

Useful Enumeration

```bash
nmap -sV \
--script memcached-info,banner \
-p11211 target
```

Potential Findings

- Memcached version
- Memory statistics
- Connection count
- Cache usage
- Internal infrastructure hints
- Performance metrics

---

# Common Security Risks

Frequently observed Memcached weaknesses include:

- Internet-exposed instances
- No authentication
- Unencrypted communication
- Information disclosure
- DDoS amplification abuse
- Sensitive cached data
- Poor network segmentation
- Outdated software versions

---

# Memcached Amplification Attacks

Historically, exposed UDP-enabled Memcached servers have been abused in reflection and amplification attacks.

```text
Attacker

    │

Spoofed UDP Request

    ▼

Public Memcached Server

    │

Large Response

    ▼

Victim
```

Because the response can be significantly larger than the request, attackers have used vulnerable Memcached servers to generate massive volumes of traffic toward victims.

Modern deployments typically disable UDP support to mitigate this risk.

---

# Best Practices

- Disable UDP unless operationally required.
- Restrict Memcached to internal networks.
- Block Internet access using firewalls.
- Monitor cache usage and connection counts.
- Keep Memcached updated.
- Avoid storing highly sensitive data in cache.
- Review infrastructure exposure regularly.
- Use encrypted network segments when possible.

---

# Real-World Examples

| Environment | Typical Memcached Usage |
|-------------|------------------------|
| WordPress | Object Cache |
| Magento | Product Cache |
| Laravel | Session Cache |
| Django | Query Cache |
| SaaS Platform | API Response Cache |
| E-commerce | Shopping Cart Cache |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Memcached | Distributed Cache | 11211 |
| Redis | In-Memory Database | 6379 |
| HTTP | Web Communication | 80 |
| MySQL | Relational Database | 3306 |
| PostgreSQL | Relational Database | 5432 |

---

# Summary

Memcached is a lightweight, high-performance in-memory caching system designed to reduce database load and improve application responsiveness. Its simplicity makes it an excellent choice for caching temporary application data, but its lack of built-in authentication and encryption requires careful network isolation. During reconnaissance, Memcached services may expose software versions, memory statistics, connection information, and performance metrics. Organizations should disable unnecessary UDP support, restrict access to trusted networks, and continuously monitor cache infrastructure to prevent information disclosure and abuse.

---

# Chapter 29 — Elasticsearch

## Overview

**Elasticsearch** is a distributed, RESTful search and analytics engine built on top of the Apache Lucene library. It is designed to store, search, and analyze massive volumes of structured, semi-structured, and unstructured data with near real-time performance.

Elasticsearch has become one of the core technologies in modern observability, security monitoring, business intelligence, and enterprise search platforms.

It is commonly deployed in:

- SIEM platforms
- Log management systems
- Security monitoring
- Enterprise search
- E-commerce search
- Application monitoring
- Big data analytics
- Cloud-native environments

Although Elasticsearch provides powerful indexing and search capabilities, improperly secured deployments have historically exposed sensitive corporate information, making it an attractive target during security assessments.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Elasticsearch |
| Default REST Port | TCP 9200 |
| Cluster Communication Port | TCP 9300 |
| Transport | HTTP / HTTPS |
| Encryption | Optional (TLS) |
| Authentication | Optional (X-Pack Security) |
| Application Layer | Yes |

---

# Primary Purpose

Elasticsearch is designed to:

- Index documents
- Perform full-text searches
- Analyze log data
- Store security events
- Aggregate metrics
- Support dashboards
- Power enterprise search
- Process real-time analytics

---

# Elasticsearch Architecture

```text
            Applications

                 │

          REST API (HTTP)

                 ▼

          Elasticsearch

        ┌────────┼────────┐

        ▼        ▼        ▼

     Node 1   Node 2   Node 3

                 │

        Distributed Indexes
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Cluster | Collection of nodes |
| Node | Elasticsearch server |
| Index | Logical data collection |
| Document | JSON record |
| Shard | Partition of an index |
| Replica | Copy of a shard |

---

# Communication Workflow

```text
Application

      │

HTTP Request

      ▼

REST API

      ▼

Elasticsearch Node

      │

Search Index

      ▼

Matching Documents

      ▼

JSON Response
```

---

# Data Organization

```text
Cluster

   │

Index

   │

Shard

   │

Document

   │

Fields
```

Example document:

```json
{
  "username": "alice",
  "event": "login",
  "source_ip": "192.168.10.15",
  "timestamp": "2026-07-20T12:30:15Z"
}
```

---

# Enterprise Usage

Elasticsearch is widely deployed in:

- Security Operations Centers (SOC)
- Cloud platforms
- Kubernetes clusters
- Financial institutions
- E-commerce platforms
- Healthcare systems
- Manufacturing environments
- Government infrastructure

---

# Common Implementations

| Software | Platform |
|-----------|----------|
| Elasticsearch | Cross-platform |
| Elastic Cloud | Cloud |
| OpenSearch | Cross-platform |
| Amazon OpenSearch Service | AWS |

---

# Typical Enterprise Architecture

```text
         Web Servers

             │

        Application Logs

             ▼

        Log Forwarders

             ▼

      Elasticsearch Cluster

             │

      ┌──────┴──────┐

      ▼             ▼

 Kibana         SIEM Platform
```

---

# Common APIs

| API | Purpose |
|------|---------|
| GET / | Cluster Information |
| _search | Search Documents |
| _cat | Cluster Statistics |
| _cluster | Cluster Health |
| _nodes | Node Information |
| _indices | Index Information |

---

# Nmap Detection

Basic Scan

```bash
nmap -p9200 target
```

Version Detection

```bash
nmap -sV -p9200 target
```

Aggressive Scan

```bash
nmap -A -p9200 target
```

Default Scripts

```bash
nmap -sC -sV -p9200 target
```

---

# Useful NSE Scripts

Retrieve Banner

```bash
nmap --script banner -p9200 target
```

HTTP Title

```bash
nmap --script http-title -p9200 target
```

HTTP Headers

```bash
nmap --script http-headers -p9200 target
```

HTTP Methods

```bash
nmap --script http-methods -p9200 target
```

---

# Example Output

```text
9200/tcp open http

Elasticsearch 8.16.0
```

Example Banner

```text
{
  "name":"es-node01",
  "cluster_name":"production-cluster",
  "version":{
    "number":"8.16.0"
  }
}
```

---

# Information That Can Be Collected

Elasticsearch enumeration may reveal:

- Product version
- Cluster name
- Node name
- HTTP headers
- API endpoints
- Authentication status
- TLS support
- Index names
- Node count
- Plugin information

---

# Blue Team Perspective

Recommendations

- Enable authentication for all clusters.
- Require TLS for HTTP and transport traffic.
- Disable anonymous access.
- Restrict REST API access using firewalls.
- Protect management interfaces.
- Monitor cluster health continuously.
- Apply security updates promptly.
- Enable audit logging.

---

# Red Team Perspective

Interesting Targets

- SIEM platforms
- Log aggregation servers
- Security monitoring infrastructure
- Kubernetes logging stacks
- Elastic Cloud deployments
- Application monitoring platforms

Useful Enumeration

```bash
nmap -sV \
--script banner,http-title,http-headers \
-p9200 target
```

Potential Findings

- Elasticsearch version
- Cluster name
- Node identifiers
- Authentication status
- Public REST endpoints
- Product branding
- Available HTTP methods

---

# Common Security Risks

Frequently observed Elasticsearch weaknesses include:

- Anonymous REST API access
- Internet-exposed clusters
- Missing authentication
- Unencrypted HTTP traffic
- Sensitive log exposure
- Weak access controls
- Outdated Elasticsearch versions
- Information disclosure through cluster APIs

---

# Elasticsearch vs OpenSearch

| Feature | Elasticsearch | OpenSearch |
|----------|---------------|------------|
| Origin | Elastic | AWS Fork |
| REST API | Yes | Yes |
| Distributed Search | Yes | Yes |
| Full-Text Search | Yes | Yes |
| Analytics | Yes | Yes |
| Default REST Port | 9200 | 9200 |

Both platforms share a similar architecture and many administrative concepts, although features and licensing differ.

---

# Best Practices

- Enable TLS for all communications.
- Require authentication for REST APIs.
- Restrict cluster access to trusted networks.
- Disable anonymous users.
- Protect sensitive indices with role-based access control.
- Monitor cluster logs and health metrics.
- Keep nodes patched and updated.
- Regularly audit exposed APIs.

---

# Real-World Examples

| Environment | Typical Elasticsearch Usage |
|-------------|----------------------------|
| SOC | Security Event Storage |
| SIEM | Log Correlation |
| E-commerce | Product Search |
| Kubernetes | Container Log Indexing |
| Banking | Fraud Analytics |
| Cloud Platform | Application Monitoring |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Elasticsearch REST API | Search & Analytics | 9200 |
| Elasticsearch Transport | Node Communication | 9300 |
| HTTP | Web Communication | 80 |
| HTTPS | Secure Web Communication | 443 |
| Syslog | Log Collection | 514 |

---

# Summary

Elasticsearch is a distributed search and analytics engine that powers many modern logging, monitoring, and enterprise search solutions. Its RESTful architecture and scalable indexing capabilities make it a cornerstone of SIEM platforms, observability stacks, and cloud-native applications. During reconnaissance, Elasticsearch services can reveal cluster names, node information, software versions, authentication status, and exposed REST APIs. Organizations should secure Elasticsearch by enforcing authentication, enabling TLS, restricting API access, and continuously monitoring cluster health and security events.

---

# Chapter 30 — Apache Kafka

## Overview

**Apache Kafka** is a distributed event streaming platform designed to handle high-throughput, fault-tolerant, and real-time data pipelines.

Originally developed by **LinkedIn** and later donated to the Apache Software Foundation, Kafka has become one of the most widely adopted technologies for processing event streams, log aggregation, messaging, and real-time analytics.

Unlike traditional message brokers that remove messages after delivery, Kafka stores events in an **append-only distributed log**, allowing multiple consumers to process the same data independently.

Kafka is commonly deployed in:

- Microservices
- Financial systems
- Log aggregation platforms
- SIEM pipelines
- IoT platforms
- Cloud-native applications
- Data lakes
- Event-driven architectures

Because Kafka often transports sensitive business events, financial transactions, authentication logs, and security events, securing Kafka clusters is a critical aspect of enterprise infrastructure.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Apache Kafka |
| Default Broker Port | TCP 9092 |
| Secure Broker Port | TCP 9093 (Common) |
| Controller Port | Varies by Deployment |
| Transport | TCP |
| Encryption | Optional (TLS) |
| Authentication | SASL / TLS |
| Application Layer | Yes |

---

# Primary Purpose

Kafka enables systems to:

- Stream events
- Process logs
- Exchange messages
- Build event-driven applications
- Replicate data
- Integrate distributed services
- Perform real-time analytics
- Collect telemetry

---

# Kafka Architecture

```text
             Producers

         ┌──────┼──────┐

         ▼      ▼      ▼

          Kafka Cluster

      ┌──────┼──────┐

      ▼      ▼      ▼

   Broker1 Broker2 Broker3

      │      │      │

      └──────┼──────┘

          Topics

      ┌──────┼──────┐

      ▼      ▼      ▼

 Consumer Consumer Consumer
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Producer | Publishes events |
| Broker | Stores events |
| Topic | Event category |
| Partition | Parallel storage unit |
| Consumer | Reads events |
| Consumer Group | Coordinates consumers |
| Cluster | Collection of brokers |

---

# Communication Workflow

```text
Application

      │

Produce Event

      ▼

Kafka Topic

      │

Persist Event

      ▼

Broker

      │

Consumer Poll

      ▼

Application
```

Unlike traditional queues, Kafka allows multiple consumers to independently process the same event stream.

---

# Topics and Partitions

Kafka stores events inside **topics**, which are divided into **partitions**.

```text
Topic: Orders

 ├── Partition 0

 ├── Partition 1

 ├── Partition 2

 └── Partition 3
```

Partitions enable:

- Parallel processing
- Horizontal scaling
- High throughput
- Fault tolerance

---

# Consumer Groups

Consumer Groups allow workloads to be distributed.

```text
             Topic

               │

      ┌────────┴────────┐

      ▼                 ▼

 Consumer A       Consumer B

      │                 │

 Partition 0      Partition 1
```

Each partition is consumed by only one consumer within the same consumer group.

---

# Enterprise Usage

Kafka is commonly deployed in:

- Banking
- Fraud detection
- E-commerce
- SIEM pipelines
- Kubernetes platforms
- Telecommunications
- Healthcare
- Cloud-native applications

---

# Common Kafka Implementations

| Software | Platform |
|-----------|----------|
| Apache Kafka | Cross-platform |
| Confluent Platform | Enterprise |
| Amazon MSK | AWS |
| Azure Event Hubs (Kafka API) | Azure |
| Redpanda | Cross-platform |

---

# Typical Enterprise Architecture

```text
          Web Applications

                │

           Produce Events

                ▼

          Kafka Cluster

      ┌────────┼────────┐

      ▼        ▼        ▼

 Fraud     Analytics   Billing

 Service     Engine     Service

      ▼        ▼        ▼

 Databases Dashboards Notifications
```

---

# Replication

Kafka provides fault tolerance through replication.

```text
          Broker 1

        (Leader)

            │

    ┌───────┴────────┐

    ▼                ▼

Broker 2        Broker 3

(Follower)      (Follower)
```

If the leader broker fails, a follower can become the new leader.

---

# Message Retention

Unlike many traditional messaging systems, Kafka retains messages for a configurable period.

Retention policies may be based on:

- Time
- Storage size
- Log compaction

This allows consumers to replay historical events when necessary.

---

# Nmap Detection

Basic Scan

```bash
nmap -p9092 target
```

Version Detection

```bash
nmap -sV -p9092 target
```

Aggressive Scan

```bash
nmap -A -p9092 target
```

---

# Useful NSE Scripts

Retrieve Banner

```bash
nmap --script banner -p9092 target
```

Version Detection

```bash
nmap -sV -p9092 target
```

Default Scripts

```bash
nmap -sC -sV -p9092 target
```

> **Note:** Nmap has limited Kafka-specific NSE support. In practice, Kafka enumeration is often supplemented with Kafka-native administration tools and client libraries.

---

# Example Output

```text
9092/tcp open kafka
```

Example Banner

```text
Apache Kafka

Broker ID:

2

Cluster ID:

QnL4Ab9eT8K

Protocol:

Kafka
```

---

# Information That Can Be Collected

Kafka enumeration may reveal:

- Kafka version
- Broker identifiers
- Cluster identifiers
- TLS availability
- Authentication mechanisms
- Service banners
- Open broker ports
- Vendor information

---

# Blue Team Perspective

Recommendations

- Require authentication using SASL.
- Encrypt communications with TLS.
- Disable anonymous clients.
- Restrict broker access using firewalls.
- Protect administrative interfaces.
- Monitor broker health and logs.
- Keep Kafka updated.
- Apply role-based access controls.

---

# Red Team Perspective

Interesting Targets

- SIEM ingestion pipelines
- Banking infrastructure
- Event streaming platforms
- Cloud-native applications
- Kubernetes environments
- Log aggregation systems
- Data processing clusters

Useful Enumeration

```bash
nmap -sV \
--script banner \
-p9092 target
```

Potential Findings

- Kafka broker version
- Cluster identifiers
- Authentication configuration
- TLS support
- Open broker services
- Event streaming infrastructure
- Enterprise integration points

---

# Common Security Risks

Frequently observed Kafka weaknesses include:

- Anonymous broker access
- Unencrypted broker communication
- Weak SASL credentials
- Internet-exposed brokers
- Misconfigured ACLs
- Outdated Kafka versions
- Information disclosure through metadata
- Insecure management interfaces

---

# Kafka vs Traditional Message Queues

| Feature | Kafka | Traditional Queue |
|----------|--------|-------------------|
| Message Retention | Yes | Usually Removed After Delivery |
| Event Replay | Yes | Limited |
| Horizontal Scaling | Excellent | Varies |
| Throughput | Very High | Moderate |
| Partitioning | Yes | Limited |
| Multiple Consumers | Native | Often Limited |

---

# Best Practices

- Enable TLS for all broker communications.
- Require SASL authentication.
- Restrict broker access to trusted networks.
- Implement ACLs for topics and consumer groups.
- Monitor broker metrics continuously.
- Encrypt sensitive data before publishing.
- Keep Kafka brokers updated.
- Regularly audit cluster configurations.

---

# Real-World Examples

| Environment | Typical Kafka Usage |
|-------------|--------------------|
| Banking | Transaction Streaming |
| SIEM Platform | Security Event Pipeline |
| E-commerce | Order Processing |
| IoT Platform | Sensor Event Collection |
| Kubernetes | Application Logging |
| Telecommunications | Network Event Streaming |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Kafka | Event Streaming | 9092 |
| AMQP | Enterprise Messaging | 5672 |
| MQTT | IoT Messaging | 1883 |
| Redis Pub/Sub | Lightweight Messaging | 6379 |
| Syslog | Log Collection | 514 |

---

# Summary

Apache Kafka is a distributed event streaming platform designed for high-throughput, fault-tolerant data pipelines and real-time event processing. Its architecture based on brokers, topics, partitions, and consumer groups enables scalable communication between distributed applications. During reconnaissance, Kafka services can reveal broker versions, cluster identifiers, authentication mechanisms, and deployment characteristics. Organizations should secure Kafka by enabling TLS, enforcing SASL authentication, applying access control lists, and continuously monitoring broker health and event traffic.

---

# Chapter 31 — Docker Remote API

## Overview

**Docker Remote API** is a RESTful HTTP API that allows administrators, orchestration platforms, and automation tools to remotely manage Docker daemons.

Instead of interacting with Docker through the local `docker` command-line interface (CLI), applications communicate directly with the Docker Engine over HTTP or HTTPS.

Docker Remote API enables remote management of:

- Containers
- Images
- Networks
- Volumes
- Secrets
- Plugins
- Swarm clusters

While extremely powerful, exposing the Docker Remote API without proper authentication is considered one of the most dangerous Docker misconfigurations because it effectively grants administrative control over the host system.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Docker Remote API |
| Default TCP Port | 2375 |
| Secure TCP Port | 2376 |
| Local Communication | Unix Socket (`/var/run/docker.sock`) |
| Transport | HTTP / HTTPS |
| Encryption | TLS (Recommended) |
| Authentication | Mutual TLS |
| Application Layer | Yes |

---

# Primary Purpose

Docker Remote API allows administrators and automation tools to:

- Create containers
- Delete containers
- Start services
- Stop services
- Pull images
- Push images
- Build images
- Manage networks
- Manage storage volumes
- Monitor Docker hosts

---

# Docker Architecture

```text
            Docker CLI

                 │

          HTTP / HTTPS

                 ▼

        Docker Remote API

                 │

         Docker Engine

      ┌──────────┼──────────┐

      ▼          ▼          ▼

 Containers   Images   Networks
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Docker Engine | Container runtime |
| Docker CLI | Command-line client |
| Docker API | Remote management interface |
| Container | Running application |
| Image | Container template |
| Volume | Persistent storage |
| Network | Container communication |

---

# Communication Workflow

```text
Administrator

      │

Docker CLI

      │

HTTP Request

      ▼

Docker Engine API

      │

Create Container

      ▼

Running Container
```

---

# Typical REST API Endpoints

| Endpoint | Purpose |
|----------|----------|
| /version | Docker version |
| /info | Engine information |
| /containers/json | List containers |
| /containers/create | Create container |
| /containers/{id}/start | Start container |
| /containers/{id}/stop | Stop container |
| /images/json | List images |
| /networks | List networks |

---

# Example HTTP Request

```http
GET /version HTTP/1.1
Host: docker.example.com:2375
```

Example response:

```json
{
  "Version": "28.2.2",
  "ApiVersion": "1.49",
  "Os": "linux",
  "Arch": "amd64"
}
```

---

# Enterprise Usage

Docker Remote API is commonly used in:

- CI/CD pipelines
- Kubernetes environments
- DevOps automation
- Infrastructure management
- Cloud platforms
- Build servers
- Container orchestration
- Continuous deployment systems

---

# Typical Enterprise Architecture

```text
         DevOps Engineer

                │

        Docker CLI / API

                ▼

       Docker Engine Cluster

      ┌────────┼────────┐

      ▼        ▼        ▼

 Host A    Host B    Host C

      │        │        │

 Containers Containers Containers
```

---

# Docker Socket vs Remote API

| Feature | Unix Socket | Remote API |
|----------|-------------|------------|
| Default | Yes | No |
| Network Accessible | No | Yes |
| Performance | High | High |
| Authentication | OS Permissions | TLS Certificates |
| Remote Management | No | Yes |

---

# Nmap Detection

Basic Scan

```bash
nmap -p2375 target
```

Secure API

```bash
nmap -p2376 target
```

Version Detection

```bash
nmap -sV -p2375,2376 target
```

Aggressive Scan

```bash
nmap -A -p2375 target
```

---

# Useful NSE Scripts

Retrieve HTTP Title

```bash
nmap --script http-title -p2375 target
```

Retrieve Headers

```bash
nmap --script http-headers -p2375 target
```

Enumerate HTTP Methods

```bash
nmap --script http-methods -p2375 target
```

Retrieve Banner

```bash
nmap --script banner -p2375 target
```

---

# Example Output

```text
2375/tcp open http

Docker Remote API
```

Example Banner

```text
Docker Engine

API Version: 1.49

Operating System:

Linux
```

---

# Information That Can Be Collected

Enumeration may reveal:

- Docker version
- API version
- Operating system
- Host architecture
- Running containers
- Installed images
- Docker networks
- Docker volumes
- Engine configuration
- Swarm status

---

# Blue Team Perspective

Recommendations

- Never expose TCP 2375 to untrusted networks.
- Prefer the Unix socket for local management.
- Require mutual TLS on TCP 2376.
- Restrict API access using firewalls.
- Monitor Docker API activity.
- Apply role separation for administrators.
- Keep Docker Engine updated.
- Disable unused remote management services.

---

# Red Team Perspective

Interesting Targets

- CI/CD servers
- Build infrastructure
- Kubernetes worker nodes
- Docker hosts
- Cloud instances
- Development environments
- Container management servers

Useful Enumeration

```bash
nmap -sV \
--script http-title,http-headers,http-methods \
-p2375 target
```

Potential Findings

- Docker version
- API version
- Running containers
- Host operating system
- Exposed management interfaces
- Network configuration
- Swarm participation

---

# Common Security Risks

Frequently observed Docker Remote API weaknesses include:

- Unauthenticated Remote API exposure
- Publicly accessible TCP 2375
- Missing TLS encryption
- Excessive administrative privileges
- Weak firewall rules
- Information disclosure
- Outdated Docker Engine versions
- Insecure CI/CD integrations

---

# Why TCP 2375 Is Dangerous

An exposed Docker API may allow attackers to:

```text
Attacker

    │

HTTP Request

    ▼

Docker Engine

    │

Create Privileged Container

    ▼

Mount Host Filesystem

    ▼

Execute Commands

    ▼

Full Host Compromise
```

Because Docker containers can be started with elevated privileges and host filesystem mounts, unrestricted access to the Docker API can result in complete control of the underlying operating system.

---

# Docker API Security

```text
Administrator

      │

Mutual TLS

      ▼

Docker API

      │

Certificate Validation

      ▼

Authorized Requests
```

Mutual TLS ensures that both the client and the server authenticate each other before management operations are permitted.

---

# Best Practices

- Disable unauthenticated TCP access.
- Use TLS with client certificate authentication.
- Restrict API exposure to management networks.
- Apply least-privilege administrative access.
- Monitor Docker events and audit logs.
- Rotate certificates regularly.
- Patch Docker Engine promptly.
- Perform periodic security reviews of container hosts.

---

# Real-World Examples

| Environment | Typical Docker API Usage |
|-------------|--------------------------|
| CI/CD Pipeline | Automated Container Deployment |
| Kubernetes Node | Runtime Management |
| Development Server | Container Lifecycle Control |
| Cloud Platform | Infrastructure Automation |
| DevOps Team | Image Management |
| Test Environment | Automated Integration Testing |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Docker Remote API | Container Management | 2375 / 2376 |
| Kubernetes API | Cluster Management | 6443 |
| SSH | Secure Administration | 22 |
| HTTP | Web Communication | 80 |
| HTTPS | Secure Web Communication | 443 |

---

# Summary

Docker Remote API provides a powerful REST interface for managing Docker Engine remotely. It enables automation, orchestration, and infrastructure management but also presents significant security risks if exposed without authentication or encryption. During reconnaissance, Docker API endpoints can reveal engine versions, host information, running containers, and infrastructure details. Organizations should secure Docker Remote API by disabling unauthenticated access, enforcing mutual TLS, limiting network exposure, and continuously monitoring administrative activity.

---

# Chapter 32 — Kubernetes API Server

## Overview

**Kubernetes API Server** is the central management component of a Kubernetes cluster. Every interaction with Kubernetes—whether initiated by users, administrators, automation tools, or internal cluster components—is processed through the API Server.

It acts as the **control plane gateway**, validating requests, enforcing authentication and authorization, storing cluster state, and coordinating communication between Kubernetes components.

The Kubernetes API Server is one of the most security-sensitive services in modern cloud infrastructure because it controls the entire cluster.

It is commonly found in:

- Kubernetes clusters
- Managed Kubernetes services
- Private cloud platforms
- Hybrid cloud environments
- DevOps infrastructure
- CI/CD platforms
- Container orchestration systems

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Kubernetes API Server |
| Default Secure Port | TCP 6443 |
| Legacy Insecure Port | TCP 8080 (Deprecated) |
| Transport | HTTPS |
| Encryption | TLS |
| Authentication | Certificates, Tokens, OIDC, Service Accounts |
| Application Layer | Yes |

---

# Primary Purpose

The Kubernetes API Server is responsible for:

- Managing cluster resources
- Authenticating users
- Authorizing requests
- Scheduling workloads
- Managing Pods
- Managing Nodes
- Managing Deployments
- Maintaining cluster state

---

# Kubernetes Architecture

```text
            kubectl

               │

          HTTPS 6443

               ▼

      Kubernetes API Server

               │

     ┌─────────┼─────────┐

     ▼         ▼         ▼

 Scheduler Controller etcd

               │

               ▼

            Worker Nodes

      ┌────────┼────────┐

      ▼        ▼        ▼

    Pod A    Pod B    Pod C
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| API Server | Cluster management interface |
| etcd | Cluster database |
| Scheduler | Assigns Pods to Nodes |
| Controller Manager | Maintains desired state |
| kubelet | Node agent |
| kube-proxy | Network proxy |

---

# Communication Workflow

```text
Administrator

      │

kubectl

      │

HTTPS Request

      ▼

API Server

      │

Validate Request

      ▼

Authentication

      ▼

Authorization

      ▼

Update etcd

      ▼

Cluster State Updated
```

---

# Common Kubernetes Resources

| Resource | Purpose |
|-----------|----------|
| Pod | Smallest deployable unit |
| Deployment | Application deployment |
| Service | Network access |
| Namespace | Resource isolation |
| ConfigMap | Configuration storage |
| Secret | Sensitive data |
| StatefulSet | Stateful workloads |
| Job | Batch execution |

---

# REST API Structure

Example endpoints:

```text
/api

/apis

/api/v1

/apis/apps/v1

/apis/networking.k8s.io/v1

/version

/healthz

/livez

/readyz
```

---

# Enterprise Usage

Kubernetes API Server is deployed in:

- Cloud-native applications
- Financial services
- Government infrastructure
- Healthcare
- Telecommunications
- Manufacturing
- AI platforms
- Enterprise SaaS

---

# Typical Enterprise Architecture

```text
        Administrators

             │

         kubectl / API

             ▼

      Load Balancer

             ▼

     API Server Cluster

      ┌──────┼──────┐

      ▼      ▼      ▼

 API1    API2    API3

             │

           etcd

             │

      Worker Nodes
```

---

# Authentication Methods

| Method | Description |
|----------|-------------|
| Client Certificates | X.509 authentication |
| Bearer Token | API token |
| Service Account | Internal authentication |
| OpenID Connect | Identity Provider |
| Webhook | External authentication |

---

# Authorization Models

| Model | Description |
|--------|-------------|
| RBAC | Role-Based Access Control |
| ABAC | Attribute-Based Access Control |
| Webhook | External authorization |
| Node Authorization | Node permissions |

RBAC is the most commonly used authorization model in production clusters.

---

# Nmap Detection

Basic Scan

```bash
nmap -p6443 target
```

Version Detection

```bash
nmap -sV -p6443 target
```

Service Detection

```bash
nmap -sC -sV -p6443 target
```

Aggressive Scan

```bash
nmap -A -p6443 target
```

---

# Useful NSE Scripts

Retrieve HTTP Title

```bash
nmap --script http-title -p6443 target
```

Retrieve HTTP Headers

```bash
nmap --script http-headers -p6443 target
```

Enumerate HTTP Methods

```bash
nmap --script http-methods -p6443 target
```

SSL Certificate Information

```bash
nmap --script ssl-cert -p6443 target
```

Supported TLS Ciphers

```bash
nmap --script ssl-enum-ciphers -p6443 target
```

---

# Example Output

```text
6443/tcp open ssl/https

Kubernetes API Server
```

Example Banner

```text
Server:

kube-apiserver

Version:

v1.31.2
```

---

# Information That Can Be Collected

Enumeration may reveal:

- Kubernetes version
- API version
- TLS configuration
- Supported HTTP methods
- SSL certificate details
- Server headers
- Authentication mechanisms
- Cluster identifiers

---

# Blue Team Perspective

Recommendations

- Enable strong RBAC policies.
- Require TLS for all communications.
- Disable anonymous authentication.
- Restrict API access using firewalls.
- Enable audit logging.
- Rotate certificates regularly.
- Monitor API activity continuously.
- Keep Kubernetes updated.

---

# Red Team Perspective

Interesting Targets

- Cloud Kubernetes clusters
- On-premises Kubernetes deployments
- Managed Kubernetes services
- CI/CD platforms
- Container orchestration infrastructure
- Development clusters

Useful Enumeration

```bash
nmap -sV \
--script ssl-cert,http-title,http-headers \
-p6443 target
```

Potential Findings

- Kubernetes version
- TLS configuration
- Certificate metadata
- API availability
- HTTP headers
- Server information
- Cluster management interface

---

# Common Security Risks

Frequently observed Kubernetes API Server weaknesses include:

- Anonymous API access
- Overly permissive RBAC roles
- Exposed API Server
- Weak Service Account permissions
- Expired or weak certificates
- Misconfigured admission controllers
- Excessive cluster-admin privileges
- Outdated Kubernetes versions

---

# Kubernetes Control Plane

```text
          API Server

               │

     ┌─────────┼─────────┐

     ▼         ▼         ▼

 Scheduler Controller   etcd

               │

               ▼

         Worker Nodes

               │

               ▼

              Pods
```

The API Server is the central coordination point for the entire control plane.

---

# API Server Security

```text
Client

   │

TLS Connection

   ▼

Authentication

   ▼

Authorization (RBAC)

   ▼

Admission Controllers

   ▼

API Server

   ▼

etcd
```

Every request should pass through multiple security layers before modifying cluster resources.

---

# Best Practices

- Restrict API Server exposure to trusted networks.
- Enforce least-privilege RBAC roles.
- Enable audit logging.
- Rotate certificates and tokens.
- Disable anonymous authentication.
- Protect etcd with encryption.
- Keep the control plane fully patched.
- Continuously monitor Kubernetes events.

---

# Real-World Examples

| Environment | Typical Kubernetes API Usage |
|-------------|-----------------------------|
| CI/CD Platform | Deploy Applications |
| Cloud Provider | Cluster Management |
| Enterprise SaaS | Container Orchestration |
| AI Platform | GPU Workload Scheduling |
| Financial Institution | Microservices |
| Government Cloud | Secure Infrastructure |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Kubernetes API | Cluster Management | 6443 |
| Docker Remote API | Container Management | 2375/2376 |
| etcd | Cluster Database | 2379 |
| HTTPS | Secure Web Communication | 443 |
| SSH | Remote Administration | 22 |

---

# Summary

The Kubernetes API Server is the central management interface of every Kubernetes cluster, responsible for authentication, authorization, resource management, and coordination of the control plane. Because it provides administrative access to the entire cluster, it is one of the most critical services to secure. During reconnaissance, Kubernetes API Servers may reveal version information, TLS configuration, API endpoints, and authentication details. Organizations should protect API Servers with strong RBAC policies, mutual TLS, restricted network exposure, comprehensive auditing, and continuous monitoring.

---

# Chapter 33 — etcd

## Overview

**etcd** is a distributed, reliable, and strongly consistent key-value store used primarily for storing configuration data, service discovery information, and distributed system state.

Developed by **CoreOS** (now part of Red Hat), etcd has become one of the most important infrastructure components in cloud-native environments.

Its most well-known role is serving as the **primary datastore for Kubernetes**, where it stores the complete state of the cluster.

Because etcd contains highly sensitive infrastructure information—including secrets, certificates, cluster configuration, and application metadata—it is considered one of the highest-value targets during infrastructure assessments.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | etcd Distributed Key-Value Store |
| Default Client Port | TCP 2379 |
| Default Peer Port | TCP 2380 |
| Transport | HTTP / HTTPS |
| Encryption | TLS (Recommended) |
| Authentication | Optional |
| Consistency Model | Strong Consistency (Raft) |

---

# Primary Purpose

etcd is designed to:

- Store cluster configuration
- Maintain distributed system state
- Provide service discovery
- Coordinate distributed applications
- Store Kubernetes objects
- Manage distributed locks
- Maintain leader election
- Store secrets and metadata

---

# etcd Architecture

```text
            Client Applications

                  │

          HTTP / HTTPS API

                  ▼

           etcd Cluster

      ┌────────┼────────┐

      ▼        ▼        ▼

    Node1    Node2    Node3

      │        │        │

      └────────┼────────┘

        Raft Consensus
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Member | Individual etcd node |
| Cluster | Collection of members |
| Leader | Coordinates writes |
| Follower | Replicates data |
| Client API | Read/write interface |
| Raft | Consensus protocol |

---

# Communication Workflow

```text
Application

      │

PUT / GET Request

      ▼

Leader Node

      │

Raft Replication

      ▼

Follower Nodes

      │

Consensus

      ▼

Response Returned
```

---

# Data Model

etcd stores data as hierarchical key-value pairs.

Example:

```text
/config/database/host

/config/database/port

/users/admin

/kubernetes.io/pods

/kubernetes.io/secrets
```

---

# Key Operations

| Operation | Description |
|-----------|-------------|
| GET | Read value |
| PUT | Store value |
| DELETE | Remove value |
| WATCH | Monitor changes |
| LEASE | Temporary keys |
| TXN | Atomic transaction |

---

# Enterprise Usage

etcd is widely deployed in:

- Kubernetes clusters
- OpenShift
- Cloud-native infrastructure
- Service discovery systems
- Distributed databases
- DevOps platforms
- High-availability clusters
- Configuration management systems

---

# Kubernetes Integration

Within Kubernetes, etcd stores nearly every cluster object.

```text
           Kubernetes

                │

         API Server

                │

                ▼

              etcd

     ┌──────────┼──────────┐

     ▼          ▼          ▼

   Pods      Secrets    ConfigMaps

 Deployments  Nodes      Services
```

Without etcd, Kubernetes cannot maintain its desired state.

---

# High Availability

Production deployments typically use an odd number of nodes.

```text
          etcd Cluster

      ┌────────┼────────┐

      ▼        ▼        ▼

   Node1    Node2    Node3

       Leader + Followers
```

An odd number of members ensures proper quorum for the Raft consensus algorithm.

---

# Raft Consensus

```text
Client

   │

Write Request

   ▼

Leader

   │

Replicate Log

   ▼

Followers

   │

Majority ACK

   ▼

Commit
```

A write operation is considered successful only after it has been acknowledged by a majority of cluster members.

---

# Nmap Detection

Basic Scan

```bash
nmap -p2379,2380 target
```

Version Detection

```bash
nmap -sV -p2379,2380 target
```

Aggressive Scan

```bash
nmap -A -p2379 target
```

Default Scripts

```bash
nmap -sC -sV -p2379 target
```

---

# Useful NSE Scripts

Retrieve Banner

```bash
nmap --script banner -p2379 target
```

HTTP Headers

```bash
nmap --script http-headers -p2379 target
```

HTTP Title

```bash
nmap --script http-title -p2379 target
```

SSL Certificate

```bash
nmap --script ssl-cert -p2379 target
```

---

# Example Output

```text
2379/tcp open ssl/http

etcd Client API
```

Example Response

```text
Server:

etcd

Version:

3.5.15

Cluster ID:

7e27652122e8b2ae
```

---

# Information That Can Be Collected

Enumeration may reveal:

- etcd version
- Cluster identifiers
- Member identifiers
- TLS configuration
- Client API availability
- HTTP headers
- Certificate details
- Software implementation

---

# Blue Team Perspective

Recommendations

- Never expose etcd directly to the Internet.
- Enable mutual TLS authentication.
- Restrict client API access.
- Encrypt data at rest.
- Protect Kubernetes Secrets.
- Monitor cluster health.
- Enable audit logging.
- Keep etcd updated.

---

# Red Team Perspective

Interesting Targets

- Kubernetes control planes
- OpenShift clusters
- Cloud-native platforms
- CI/CD infrastructure
- High-availability clusters
- Enterprise orchestration systems

Useful Enumeration

```bash
nmap -sV \
--script ssl-cert,http-title,http-headers \
-p2379 target
```

Potential Findings

- etcd version
- TLS certificates
- Cluster identifiers
- Client API availability
- Software metadata
- HTTP responses
- Infrastructure fingerprints

---

# Common Security Risks

Frequently observed etcd weaknesses include:

- Exposed client API
- Missing TLS encryption
- Anonymous access
- Weak certificate management
- Internet-accessible clusters
- Outdated etcd versions
- Sensitive configuration disclosure
- Poor network segmentation

---

# etcd Security Model

```text
Administrator

      │

TLS Authentication

      ▼

Client API

      │

Authorization

      ▼

Raft Cluster

      ▼

Encrypted Storage
```

Security depends on protecting both network communication and stored cluster data.

---

# Backup and Disaster Recovery

Regular backups are essential because etcd stores the authoritative state of the cluster.

Typical backup process:

```text
Running Cluster

      │

Snapshot

      ▼

Encrypted Backup

      ▼

Secure Storage

      ▼

Disaster Recovery
```

Without valid backups, recovering a failed Kubernetes control plane can be significantly more difficult.

---

# Best Practices

- Enable mutual TLS for all cluster communications.
- Restrict client access using firewalls.
- Encrypt sensitive data at rest.
- Perform regular snapshot backups.
- Monitor cluster health continuously.
- Keep etcd updated.
- Protect backup files.
- Limit administrative access.

---

# Real-World Examples

| Environment | Typical etcd Usage |
|-------------|-------------------|
| Kubernetes | Cluster State Storage |
| OpenShift | Configuration Database |
| Service Discovery | Distributed Registry |
| Cloud Platform | Infrastructure Metadata |
| DevOps | Configuration Management |
| High Availability | Leader Election |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| etcd Client API | Key-Value Operations | 2379 |
| etcd Peer API | Cluster Replication | 2380 |
| Kubernetes API | Cluster Management | 6443 |
| Docker Remote API | Container Management | 2375/2376 |
| HTTPS | Secure Communication | 443 |

---

# Summary

etcd is a distributed, strongly consistent key-value store that forms the foundation of Kubernetes and many other cloud-native platforms. By maintaining cluster configuration, secrets, service discovery information, and distributed state, it enables reliable coordination across complex environments. During reconnaissance, etcd services can reveal software versions, cluster metadata, TLS configuration, and infrastructure details. Organizations should secure etcd by enforcing mutual TLS, restricting network access, encrypting sensitive data, maintaining regular backups, and continuously monitoring cluster health.

---

# Chapter 34 — Consul

## Overview

**HashiCorp Consul** is a distributed service networking platform that provides **service discovery, health checking, configuration management, and service mesh capabilities** for modern distributed applications.

Originally developed by HashiCorp, Consul has become one of the most popular service discovery solutions for cloud-native infrastructure, microservices, and hybrid cloud deployments.

Unlike traditional DNS servers that only resolve hostnames, Consul continuously monitors services, tracks their health, and automatically updates service information as infrastructure changes.

Consul is commonly deployed in:

- Kubernetes clusters
- Docker environments
- Microservice architectures
- Hybrid cloud infrastructures
- Service mesh deployments
- DevOps platforms
- Multi-datacenter environments
- Enterprise applications

Because Consul maintains detailed information about infrastructure, services, nodes, and configuration, an exposed Consul deployment can reveal valuable information during reconnaissance.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | HashiCorp Consul |
| Default HTTP Port | TCP 8500 |
| Default HTTPS Port | TCP 8501 |
| Default DNS Port | TCP/UDP 8600 |
| Server Communication | TCP 8300 |
| LAN Gossip | TCP/UDP 8301 |
| WAN Gossip | TCP/UDP 8302 |
| Transport | HTTP / HTTPS / DNS |
| Encryption | TLS Supported |
| Authentication | ACL Tokens |

---

# Primary Purpose

Consul provides:

- Service discovery
- Health checking
- Service mesh
- Configuration storage
- Distributed key-value storage
- Multi-datacenter networking
- DNS-based service discovery
- Infrastructure automation

---

# Consul Architecture

```text
            Applications

       ┌────────┼────────┐

       ▼        ▼        ▼

     Agent    Agent    Agent

       │        │        │

       └────────┼────────┘

          Consul Servers

      ┌────────┼────────┐

      ▼        ▼        ▼

   Server1  Server2  Server3

         Raft Consensus
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Server | Stores cluster state |
| Client Agent | Local service agent |
| Service | Registered application |
| Health Check | Service monitoring |
| KV Store | Configuration storage |
| ACL | Access control |
| Connect | Service Mesh |

---

# Communication Workflow

```text
Application

      │

Register Service

      ▼

Local Agent

      │

Forward Request

      ▼

Consul Server

      │

Update Catalog

      ▼

DNS / HTTP Query

      ▼

Client
```

---

# Service Registration

Services register themselves with Consul.

```text
Web Server

      │

Register

      ▼

Consul Agent

      │

Catalog

      ▼

Service Available
```

Each registered service can include:

- Service name
- IP address
- Port
- Tags
- Metadata
- Health checks

---

# Health Checks

Consul continuously evaluates service health.

Common health check types:

| Check Type | Description |
|------------|-------------|
| HTTP | HTTP endpoint |
| TCP | Open port |
| Script | Execute script |
| TTL | Time-to-live heartbeat |
| gRPC | gRPC health check |

Example:

```text
Healthy

↓

Passing

↓

Returned by DNS
```

If the service fails:

```text
Critical

↓

Removed from Discovery
```

---

# Key-Value Store

Consul includes a distributed KV database.

Example keys:

```text
config/database/password

config/api/url

production/cache/enabled

application/theme

feature/login
```

Applications can dynamically retrieve configuration values without requiring redeployment.

---

# Enterprise Usage

Consul is commonly deployed in:

- Kubernetes
- Nomad clusters
- Docker Swarm
- Hybrid cloud
- Financial services
- Telecommunications
- Government infrastructure
- Enterprise microservices

---

# Multi-Datacenter Support

```text
        Datacenter A

      ┌───────────────┐

      │ Consul Server │

      └───────────────┘

              │

       WAN Federation

              │

      ┌───────────────┐

      │ Consul Server │

      └───────────────┘

        Datacenter B
```

Consul supports secure communication across geographically distributed environments.

---

# Consul Connect Service Mesh

Consul Connect enables encrypted service-to-service communication.

```text
Service A

     │

mTLS

     ▼

Proxy Sidecar

     │

Encrypted Traffic

     ▼

Proxy Sidecar

     │

Service B
```

This architecture helps enforce zero-trust networking principles.

---

# Nmap Detection

Basic Scan

```bash
nmap -p8500 target
```

Version Detection

```bash
nmap -sV -p8500 target
```

Aggressive Scan

```bash
nmap -A -p8500 target
```

HTTPS Interface

```bash
nmap -sV -p8501 target
```

---

# Useful NSE Scripts

Retrieve Banner

```bash
nmap --script banner -p8500 target
```

Retrieve HTTP Title

```bash
nmap --script http-title -p8500 target
```

Retrieve HTTP Headers

```bash
nmap --script http-headers -p8500 target
```

Enumerate HTTP Methods

```bash
nmap --script http-methods -p8500 target
```

SSL Information

```bash
nmap --script ssl-cert -p8501 target
```

---

# Example Output

```text
8500/tcp open http

HashiCorp Consul
```

Example Banner

```text
Consul

Version:

1.21.0

Datacenter:

production

Leader:

true
```

---

# Information That Can Be Collected

Enumeration may reveal:

- Consul version
- Datacenter name
- Cluster members
- Leader node
- HTTP endpoints
- TLS support
- DNS service
- Service catalog
- Health status
- ACL configuration

---

# Blue Team Perspective

Recommendations

- Enable ACL enforcement.
- Require TLS for all communications.
- Restrict access to the HTTP API.
- Secure gossip communication.
- Protect the KV store.
- Monitor cluster membership.
- Enable audit logging where available.
- Keep Consul updated.

---

# Red Team Perspective

Interesting Targets

- Kubernetes clusters
- Service mesh deployments
- DevOps infrastructure
- Cloud-native platforms
- Hybrid cloud environments
- Enterprise microservices
- Configuration management systems

Useful Enumeration

```bash
nmap -sV \
--script banner,http-title,http-headers \
-p8500 target
```

Potential Findings

- Consul version
- Cluster topology
- Datacenter names
- Service catalog
- Registered nodes
- HTTP API availability
- Health check endpoints
- Configuration metadata

---

# Common Security Risks

Frequently observed Consul weaknesses include:

- Unauthenticated HTTP API
- Weak ACL policies
- Publicly exposed Consul servers
- Missing TLS encryption
- Information disclosure through service catalog
- Exposed KV store
- Insecure gossip communication
- Outdated Consul versions

---

# Consul Security Model

```text
Administrator

      │

ACL Token

      ▼

TLS

      ▼

HTTP API

      ▼

Authorization

      ▼

Consul Server
```

Multiple security layers should be used to protect administrative operations and service metadata.

---

# Best Practices

- Enable ACLs for all deployments.
- Encrypt HTTP and gossip traffic with TLS.
- Restrict management interfaces to trusted networks.
- Secure the KV store with least-privilege access.
- Monitor cluster membership changes.
- Rotate ACL tokens regularly.
- Patch Consul servers promptly.
- Audit service registrations periodically.

---

# Real-World Examples

| Environment | Typical Consul Usage |
|-------------|---------------------|
| Kubernetes | Service Discovery |
| Nomad | Service Networking |
| Microservices | Dynamic Service Registry |
| Banking | Service Mesh |
| Cloud Platform | Configuration Store |
| Enterprise SaaS | Health Monitoring |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Consul HTTP API | Management API | 8500 |
| Consul HTTPS API | Secure Management | 8501 |
| Consul DNS | Service Discovery | 8600 |
| etcd | Distributed KV Store | 2379 |
| Kubernetes API | Cluster Management | 6443 |

---

# Summary

HashiCorp Consul is a distributed service networking platform that combines service discovery, health monitoring, configuration management, and service mesh capabilities. It enables applications to dynamically locate healthy services while maintaining a consistent view of infrastructure across multiple environments. During reconnaissance, Consul services may reveal cluster members, service catalogs, datacenter names, health checks, and management interfaces. Organizations should secure Consul deployments by enabling ACLs, enforcing TLS, protecting the HTTP API, encrypting gossip communication, and continuously monitoring cluster activity.

---

# Chapter 35 — Apache ZooKeeper

## Overview

**Apache ZooKeeper** is a distributed coordination service designed to help large-scale distributed applications maintain configuration information, naming services, synchronization, and leader election.

Originally developed at Yahoo! and now maintained by the Apache Software Foundation, ZooKeeper provides a centralized coordination mechanism that enables distributed systems to behave consistently even across multiple servers.

Unlike databases that primarily store business data, ZooKeeper stores **coordination metadata** used by distributed applications.

ZooKeeper is commonly deployed alongside:

- Apache Kafka
- Apache Hadoop
- Apache HBase
- Apache Solr
- Apache Storm
- Apache NiFi
- Distributed databases
- Enterprise microservices

Although newer Kafka deployments can operate without ZooKeeper (using KRaft mode), ZooKeeper remains widely deployed in enterprise environments.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Apache ZooKeeper |
| Default Client Port | TCP 2181 |
| Leader Election Ports | TCP 2888 / 3888 |
| Transport | TCP |
| Encryption | TLS (Supported) |
| Authentication | SASL / Kerberos / Digest |
| Application Layer | Yes |

---

# Primary Purpose

ZooKeeper provides:

- Distributed coordination
- Configuration management
- Service discovery
- Leader election
- Distributed locking
- Naming services
- Cluster membership
- Synchronization

---

# ZooKeeper Architecture

```text
           Client Applications

        ┌────────┼────────┐

        ▼        ▼        ▼

      Client   Client   Client

               │

               ▼

        ZooKeeper Ensemble

     ┌─────────┼─────────┐

     ▼         ▼         ▼

  Server1   Server2   Server3

      Leader + Followers
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Ensemble | ZooKeeper cluster |
| Leader | Coordinates writes |
| Follower | Replicates updates |
| Observer | Read-only participant |
| Client | Application using ZooKeeper |
| ZNode | Data object |

---

# Communication Workflow

```text
Application

      │

Read / Write

      ▼

ZooKeeper Client

      │

TCP Request

      ▼

Leader

      │

Replication

      ▼

Followers

      │

Acknowledgement

      ▼

Response
```

---

# Data Model

ZooKeeper stores information in a hierarchical namespace.

```text
/

├── kafka

│   ├── brokers

│   └── topics

├── hadoop

├── services

└── applications
```

Each entry is called a **ZNode**.

---

# ZNodes

ZooKeeper data is stored inside ZNodes.

| ZNode Type | Description |
|------------|-------------|
| Persistent | Remains until deleted |
| Ephemeral | Removed when client disconnects |
| Sequential | Automatically numbered |
| Container | Automatically cleaned up |

---

# Watches

ZooKeeper allows clients to monitor changes.

```text
Client

   │

Register Watch

   ▼

ZooKeeper

   │

Configuration Changes

   ▼

Notification Sent
```

This enables applications to react immediately when configuration or cluster membership changes.

---

# Enterprise Usage

ZooKeeper is commonly deployed in:

- Kafka clusters
- Hadoop ecosystems
- Distributed databases
- Big data platforms
- Financial systems
- Telecommunications
- Cloud infrastructure
- Enterprise analytics

---

# Typical Enterprise Architecture

```text
         Kafka Brokers

      ┌────────┼────────┐

      ▼        ▼        ▼

 Broker1   Broker2   Broker3

      │        │        │

      └────────┼────────┘

        ZooKeeper Ensemble

      ┌────────┼────────┐

      ▼        ▼        ▼

   Node1    Node2    Node3
```

---

# Leader Election

ZooKeeper performs leader election automatically.

```text
        Ensemble

   ┌──────┼──────┐

   ▼      ▼      ▼

 Node1  Node2  Node3

    │

Leader Selected

    ▼

Coordinate Writes
```

Only one leader processes write requests at a time.

---

# Distributed Locking

ZooKeeper supports distributed locks.

```text
Application A

      │

Acquire Lock

      ▼

ZooKeeper

      │

Granted

      ▼

Critical Section

      │

Release Lock
```

Distributed locking prevents conflicting operations across multiple applications.

---

# Nmap Detection

Basic Scan

```bash
nmap -p2181 target
```

Version Detection

```bash
nmap -sV -p2181 target
```

Aggressive Scan

```bash
nmap -A -p2181 target
```

Default Scripts

```bash
nmap -sC -sV -p2181 target
```

---

# Useful NSE Scripts

Retrieve Banner

```bash
nmap --script banner -p2181 target
```

Version Detection

```bash
nmap -sV -p2181 target
```

Default Enumeration

```bash
nmap -sC -p2181 target
```

> **Note:** Nmap provides only limited ZooKeeper-specific NSE support. Detailed assessment is typically performed using ZooKeeper administration commands and client utilities.

---

# Example Output

```text
2181/tcp open zookeeper
```

Example Banner

```text
Apache ZooKeeper

Version:

3.9.2

Mode:

leader
```

---

# Information That Can Be Collected

Enumeration may reveal:

- ZooKeeper version
- Cluster mode
- Leader information
- Client port
- Authentication mechanisms
- TLS support
- Service banner
- Ensemble size

---

# Blue Team Perspective

Recommendations

- Enable client authentication.
- Encrypt communications with TLS.
- Restrict client access using firewalls.
- Protect administrative interfaces.
- Monitor leader election events.
- Secure configuration data.
- Keep ZooKeeper updated.
- Enable audit logging where supported.

---

# Red Team Perspective

Interesting Targets

- Kafka infrastructures
- Hadoop clusters
- Big data platforms
- Enterprise analytics systems
- Distributed databases
- Cloud-native applications
- Financial data platforms

Useful Enumeration

```bash
nmap -sV \
--script banner \
-p2181 target
```

Potential Findings

- ZooKeeper version
- Leader or follower role
- Ensemble topology
- Authentication status
- TLS availability
- Service banner
- Infrastructure relationships

---

# Common Security Risks

Frequently observed ZooKeeper weaknesses include:

- Anonymous client access
- Missing TLS encryption
- Publicly exposed client ports
- Weak authentication
- Information disclosure through administrative commands
- Outdated ZooKeeper versions
- Excessive client permissions
- Poor network segmentation

---

# ZooKeeper Security Model

```text
Client

   │

Authentication

   ▼

Authorization

   ▼

ZooKeeper Server

   │

Replicate

   ▼

Ensemble
```

Every client should authenticate before accessing configuration data or coordination services.

---

# Best Practices

- Restrict ZooKeeper access to trusted networks.
- Enable TLS for client and quorum communication.
- Require strong authentication.
- Monitor cluster membership continuously.
- Protect sensitive configuration data.
- Patch ZooKeeper regularly.
- Limit administrative access.
- Audit client activity.

---

# Real-World Examples

| Environment | Typical ZooKeeper Usage |
|-------------|------------------------|
| Apache Kafka | Broker Coordination |
| Hadoop | Cluster Coordination |
| HBase | Metadata Management |
| SolrCloud | Search Cluster Coordination |
| Distributed Database | Leader Election |
| Enterprise Analytics | Service Discovery |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| ZooKeeper | Distributed Coordination | 2181 |
| Kafka | Event Streaming | 9092 |
| etcd | Distributed Key-Value Store | 2379 |
| Consul | Service Discovery | 8500 |
| HTTPS | Secure Management | 443 |

---

# Summary

Apache ZooKeeper is a distributed coordination service that enables configuration management, leader election, distributed locking, and service discovery across complex distributed systems. It has historically served as a foundational component for platforms such as Kafka and Hadoop. During reconnaissance, ZooKeeper services can reveal version information, cluster roles, authentication mechanisms, and infrastructure topology. Organizations should secure ZooKeeper by enabling authentication, enforcing TLS, restricting network exposure, and continuously monitoring cluster health and client activity.

---

# Chapter 36 — RabbitMQ

## Overview

**RabbitMQ** is one of the world's most widely used **message broker** platforms, implementing the **Advanced Message Queuing Protocol (AMQP)** while also supporting several additional messaging protocols through plugins.

Developed originally by Rabbit Technologies and now maintained by VMware and the open-source community, RabbitMQ enables reliable, asynchronous communication between applications.

Instead of applications communicating directly with one another, RabbitMQ acts as an intermediary that receives, routes, stores, and delivers messages.

RabbitMQ is commonly used in:

- Microservices
- Financial systems
- Banking applications
- E-commerce platforms
- Cloud-native applications
- IoT backends
- Background task processing
- Enterprise integration

Because RabbitMQ frequently transports sensitive business data and administrative tasks, improperly secured deployments can expose significant infrastructure information.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | RabbitMQ |
| Default AMQP Port | TCP 5672 |
| Secure AMQP Port | TCP 5671 |
| Management UI | TCP 15672 |
| Management HTTPS | TCP 15671 |
| Clustering | TCP 25672 |
| Transport | TCP |
| Encryption | TLS Supported |
| Authentication | Username / Password, LDAP, OAuth2 |
| Application Layer | Yes |

---

# Primary Purpose

RabbitMQ provides:

- Reliable message delivery
- Asynchronous communication
- Task distribution
- Load balancing
- Event processing
- Workflow orchestration
- Enterprise messaging
- Service decoupling

---

# RabbitMQ Architecture

```text
          Producers

      ┌──────┼──────┐

      ▼      ▼      ▼

          Exchange

              │

     ┌────────┼────────┐

     ▼        ▼        ▼

   Queue1   Queue2   Queue3

     │         │         │

     ▼         ▼         ▼

 Consumer Consumer Consumer
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Producer | Publishes messages |
| Exchange | Routes messages |
| Queue | Stores messages |
| Consumer | Processes messages |
| Binding | Connects queues and exchanges |
| Broker | RabbitMQ server |
| Virtual Host | Logical isolation |

---

# Communication Workflow

```text
Application A

      │

Publish

      ▼

Exchange

      │

Routing Key

      ▼

Queue

      │

Consumer

      ▼

Application B
```

Messages are stored until acknowledged by the consumer or until configured expiration rules are met.

---

# Exchange Types

RabbitMQ supports multiple routing models.

| Exchange Type | Description |
|---------------|-------------|
| Direct | Exact routing key match |
| Fanout | Broadcast to all queues |
| Topic | Pattern-based routing |
| Headers | Route using message headers |
| Default | Predefined direct exchange |

---

# Message Lifecycle

```text
Producer

    │

Publish

    ▼

Exchange

    │

Route

    ▼

Queue

    │

Store

    ▼

Consumer

    │

ACK

    ▼

Delete Message
```

---

# Virtual Hosts (vHosts)

RabbitMQ uses **Virtual Hosts** to separate applications.

```text
RabbitMQ Server

├── /production

├── /development

├── /testing

└── /internal
```

Each Virtual Host maintains its own:

- Queues
- Exchanges
- Bindings
- Users
- Permissions

---

# Enterprise Usage

RabbitMQ is commonly deployed in:

- Banking
- Insurance
- Retail
- Healthcare
- Government
- Manufacturing
- Telecommunications
- Cloud platforms

---

# Typical Enterprise Architecture

```text
        Web Applications

               │

         Publish Events

               ▼

         RabbitMQ Cluster

      ┌────────┼────────┐

      ▼        ▼        ▼

 Queue A  Queue B  Queue C

      ▼        ▼        ▼

 Billing Inventory Notification
```

---

# Clustering

RabbitMQ supports clustered deployments.

```text
         RabbitMQ Cluster

     ┌────────┼────────┐

     ▼        ▼        ▼

   Node1    Node2    Node3

         Shared Metadata
```

Clustering improves scalability and availability.

---

# High Availability

Modern RabbitMQ deployments commonly use **Quorum Queues**.

```text
Producer

    │

Publish

    ▼

Leader Queue

    │

Replicate

    ▼

Follower Nodes

    │

Majority ACK

    ▼

Success
```

Quorum queues increase reliability and resilience against node failures.

---

# Nmap Detection

Basic Scan

```bash
nmap -p5672 target
```

Management Interface

```bash
nmap -p15672 target
```

Version Detection

```bash
nmap -sV -p5672,15672 target
```

Aggressive Scan

```bash
nmap -A -p5672 target
```

---

# Useful NSE Scripts

Banner Detection

```bash
nmap --script banner -p5672 target
```

Management HTTP Title

```bash
nmap --script http-title -p15672 target
```

HTTP Headers

```bash
nmap --script http-headers -p15672 target
```

HTTP Methods

```bash
nmap --script http-methods -p15672 target
```

SSL Certificate

```bash
nmap --script ssl-cert -p5671 target
```

---

# Example Output

```text
5672/tcp open amqp

RabbitMQ
```

Management Interface

```text
15672/tcp open http

RabbitMQ Management
```

---

# Information That Can Be Collected

Enumeration may reveal:

- RabbitMQ version
- AMQP version
- Management interface
- TLS configuration
- Authentication methods
- Virtual host names
- Queue statistics
- Exchange information
- Cluster configuration
- Node names

---

# Blue Team Perspective

Recommendations

- Enable TLS for client connections.
- Disable default credentials immediately.
- Restrict management UI access.
- Use strong passwords or centralized authentication.
- Enable role-based permissions.
- Monitor queue activity.
- Enable audit logging.
- Keep RabbitMQ updated.

---

# Red Team Perspective

Interesting Targets

- Financial systems
- Kubernetes environments
- Cloud-native platforms
- Enterprise messaging systems
- CI/CD pipelines
- Banking infrastructure
- E-commerce platforms

Useful Enumeration

```bash
nmap -sV \
--script banner,http-title,http-headers \
-p5672,15672 target
```

Potential Findings

- RabbitMQ version
- Management portal
- TLS availability
- Authentication mechanisms
- Cluster topology
- Queue names
- Exchange information
- Virtual Hosts

---

# Common Security Risks

Frequently observed RabbitMQ weaknesses include:

- Default credentials
- Publicly exposed management interface
- Missing TLS
- Weak passwords
- Anonymous access
- Overly permissive permissions
- Outdated RabbitMQ versions
- Information disclosure through the management API

---

# Authentication and Authorization

RabbitMQ supports multiple authentication backends.

| Method | Description |
|---------|-------------|
| Internal Database | Built-in users |
| LDAP | Enterprise directory integration |
| OAuth 2.0 | Identity provider integration |
| TLS Certificates | Mutual authentication |

Authorization is typically applied at the Virtual Host level, allowing administrators to grant fine-grained permissions for configuring exchanges, publishing messages, and consuming queues.

---

# RabbitMQ Management Plugin

The Management Plugin provides a web interface for administrators.

```text
Browser

    │

HTTPS

    ▼

RabbitMQ Management

    │

Dashboard

 ├── Nodes

 ├── Queues

 ├── Exchanges

 ├── Connections

 └── Users
```

This interface simplifies administration but should never be publicly accessible.

---

# RabbitMQ vs Apache Kafka

| Feature | RabbitMQ | Kafka |
|----------|----------|-------|
| Primary Role | Message Broker | Event Streaming Platform |
| Queue Support | Native | Topic-Based |
| Message Retention | Until ACK or Policy | Configurable Retention |
| Routing | Advanced Exchanges | Topic Partitions |
| Ordering | Queue-Based | Partition-Based |
| Throughput | High | Extremely High |
| Enterprise Messaging | Excellent | Excellent |
| Event Replay | Limited | Native |

---

# Best Practices

- Disable default accounts.
- Require TLS for all client connections.
- Restrict management interfaces to trusted networks.
- Use Virtual Hosts for isolation.
- Apply least-privilege permissions.
- Enable monitoring and alerting.
- Patch RabbitMQ regularly.
- Review queues and exchanges periodically.

---

# Real-World Examples

| Environment | Typical RabbitMQ Usage |
|-------------|-----------------------|
| Banking | Transaction Processing |
| E-commerce | Order Queue |
| Healthcare | Laboratory Workflows |
| Manufacturing | Production Events |
| Cloud Platform | Background Jobs |
| SaaS Platform | Notification Processing |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| RabbitMQ (AMQP) | Enterprise Messaging | 5672 |
| AMQP | Messaging Protocol | 5672 |
| MQTT | IoT Messaging | 1883 |
| Kafka | Event Streaming | 9092 |
| STOMP | Messaging Protocol | 61613 |

---

# Summary

RabbitMQ is a mature, feature-rich message broker that enables reliable asynchronous communication between distributed applications. Its flexible routing model, support for acknowledgements, Virtual Hosts, clustering, and multiple messaging protocols make it a core component of many enterprise systems. During reconnaissance, RabbitMQ services can reveal broker versions, management interfaces, authentication mechanisms, and cluster metadata. Organizations should secure RabbitMQ by disabling default credentials, enforcing TLS, restricting management access, implementing least-privilege permissions, and continuously monitoring messaging infrastructure.

---

# Chapter 37 — Jenkins

## Overview

**Jenkins** is one of the world's most popular open-source **Continuous Integration and Continuous Delivery (CI/CD)** automation servers.

Originally developed as **Hudson** and later forked into Jenkins, it enables software teams to automatically build, test, package, and deploy applications.

Rather than developers manually compiling code or deploying applications, Jenkins automates these repetitive tasks through configurable pipelines.

Jenkins is widely deployed in:

- Software development companies
- DevOps environments
- CI/CD pipelines
- Kubernetes platforms
- Cloud-native applications
- Enterprise software development
- Mobile application development
- Infrastructure automation

Because Jenkins often stores source code, credentials, deployment keys, API tokens, and infrastructure secrets, it represents one of the most valuable targets in enterprise environments.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Jenkins Automation Server |
| Default HTTP Port | TCP 8080 |
| HTTPS Port | Configurable |
| Agent Port | TCP 50000 |
| Transport | HTTP / HTTPS |
| Encryption | TLS Supported |
| Authentication | Local, LDAP, OAuth, SAML, OpenID Connect |
| Application Layer | Yes |

---

# Primary Purpose

Jenkins automates:

- Source code builds
- Unit testing
- Integration testing
- Package generation
- Container builds
- Infrastructure deployment
- Continuous delivery
- Continuous integration

---

# Jenkins Architecture

```text
             Developers

                  │

             Git Commit

                  ▼

            Git Repository

                  │

             Webhook Trigger

                  ▼

              Jenkins

        ┌────────┼────────┐

        ▼        ▼        ▼

     Build     Test    Deploy

        │

        ▼

   Target Environment
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Controller | Central Jenkins server |
| Agent | Executes jobs |
| Pipeline | Automation workflow |
| Job | Build task |
| Plugin | Extends functionality |
| Credential Store | Stores secrets |
| Workspace | Temporary build directory |

---

# Communication Workflow

```text
Developer

     │

Push Code

     ▼

Git Repository

     │

Webhook

     ▼

Jenkins

     │

Execute Pipeline

     ▼

Build

Test

Deploy

     ▼

Production
```

---

# Jenkins Pipelines

Modern Jenkins uses **Pipeline as Code** through a `Jenkinsfile`.

Example stages:

```text
Pipeline

├── Checkout

├── Build

├── Test

├── Package

├── Deploy

└── Notify
```

Pipelines improve reproducibility and version control for build automation.

---

# Common Integrations

Jenkins integrates with numerous development tools.

| Integration | Purpose |
|-------------|----------|
| Git | Source Control |
| GitHub | Repository Hosting |
| GitLab | DevOps Platform |
| Docker | Container Builds |
| Kubernetes | Deployment |
| Maven | Java Builds |
| Gradle | Build Automation |
| SonarQube | Code Analysis |

---

# Enterprise Usage

Jenkins is commonly deployed in:

- Financial institutions
- Software companies
- Government agencies
- Healthcare
- Telecommunications
- Manufacturing
- Cloud providers
- Enterprise DevOps teams

---

# Typical Enterprise Architecture

```text
          Developers

               │

        Git Repository

               │

         Jenkins Server

      ┌────────┼────────┐

      ▼        ▼        ▼

 Linux     Windows   Kubernetes

 Agents      Agents     Agents

      │        │         │

      └────────┼─────────┘

         Build Artifacts
```

---

# Jenkins Agents

Large deployments distribute workloads across multiple agents.

```text
        Jenkins Controller

               │

      ┌────────┼────────┐

      ▼        ▼        ▼

 Agent1    Agent2    Agent3

      │        │        │

 Build     Test     Deploy
```

This architecture improves scalability and parallel execution.

---

# Plugin System

One of Jenkins' strongest features is its plugin ecosystem.

Common plugin categories include:

- Source control
- Authentication
- Cloud providers
- Docker
- Kubernetes
- Notifications
- Security scanning
- Artifact repositories

A production Jenkins instance may have hundreds of installed plugins.

---

# Nmap Detection

Basic Scan

```bash
nmap -p8080 target
```

Version Detection

```bash
nmap -sV -p8080 target
```

Aggressive Scan

```bash
nmap -A -p8080 target
```

HTTPS Scan

```bash
nmap -sV -p443 target
```

---

# Useful NSE Scripts

Retrieve HTTP Title

```bash
nmap --script http-title -p8080 target
```

Retrieve HTTP Headers

```bash
nmap --script http-headers -p8080 target
```

Enumerate HTTP Methods

```bash
nmap --script http-methods -p8080 target
```

Retrieve Banner

```bash
nmap --script banner -p8080 target
```

SSL Certificate

```bash
nmap --script ssl-cert -p443 target
```

---

# Example Output

```text
8080/tcp open http

Jenkins
```

Example Banner

```text
Jenkins

Version:

2.516.1

Server:

Jetty
```

---

# Information That Can Be Collected

Enumeration may reveal:

- Jenkins version
- Web server
- Installed plugins
- Authentication methods
- HTTP headers
- TLS configuration
- Build agent information
- API endpoints
- Server banner

---

# Blue Team Perspective

Recommendations

- Require strong authentication.
- Enable Multi-Factor Authentication (MFA) where possible.
- Restrict administrative access.
- Limit anonymous permissions.
- Encrypt communications using TLS.
- Protect the credentials store.
- Review installed plugins regularly.
- Keep Jenkins and plugins updated.

---

# Red Team Perspective

Interesting Targets

- CI/CD servers
- DevOps infrastructure
- Kubernetes deployments
- Software development environments
- Enterprise build servers
- Cloud-native platforms
- Internal Git integrations

Useful Enumeration

```bash
nmap -sV \
--script http-title,http-headers,http-methods \
-p8080 target
```

Potential Findings

- Jenkins version
- Web server type
- Plugin-related information
- Authentication configuration
- API availability
- Build infrastructure
- Development workflows

---

# Common Security Risks

Frequently observed Jenkins weaknesses include:

- Anonymous access
- Weak administrator passwords
- Outdated plugins
- Internet-exposed Jenkins instances
- Stored plaintext credentials
- Excessive administrative privileges
- Remote code execution vulnerabilities
- Insecure build pipelines

---

# Jenkins Security Model

```text
User

   │

Authentication

   ▼

Authorization

   ▼

Controller

   │

Credentials Store

   ▼

Agents
```

Access to jobs, credentials, and administrative functions should be restricted using role-based authorization.

---

# REST API

Jenkins exposes a REST API for automation.

Common endpoints:

| Endpoint | Purpose |
|-----------|----------|
| /api/json | General API |
| /computer/api/json | Agent information |
| /job/{job}/api/json | Job details |
| /pluginManager | Plugin management |
| /manage | Administrative interface |

The REST API enables integration with external tools but should be secured to prevent unauthorized access.

---

# Best Practices

- Enable HTTPS for all communications.
- Disable anonymous access.
- Use centralized authentication (LDAP, SAML, OIDC).
- Apply least-privilege permissions.
- Keep plugins updated.
- Rotate API tokens regularly.
- Isolate build agents from production systems.
- Continuously monitor build activity and audit logs.

---

# Real-World Examples

| Environment | Typical Jenkins Usage |
|-------------|----------------------|
| Software Company | CI/CD Pipeline |
| Banking | Secure Build Automation |
| Cloud Provider | Container Deployment |
| Kubernetes | Automated Application Delivery |
| Mobile Development | Build and Test |
| Enterprise DevOps | Continuous Integration |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Jenkins HTTP | Web Interface | 8080 |
| Jenkins Agent | Agent Communication | 50000 |
| Git | Source Control | 9418 / SSH |
| Docker Remote API | Container Management | 2375 / 2376 |
| Kubernetes API | Cluster Management | 6443 |

---

# Summary

Jenkins is a leading automation server that enables continuous integration and continuous delivery across modern software development environments. Its support for pipelines, distributed agents, extensive plugin integrations, and automation workflows makes it a cornerstone of DevOps infrastructure. During reconnaissance, Jenkins services may reveal version information, authentication methods, installed plugins, API endpoints, and build infrastructure details. Organizations should secure Jenkins by enforcing strong authentication, limiting administrative access, protecting credentials, keeping plugins updated, and continuously monitoring automation activities.

---

# Chapter 38 — GitLab

## Overview

**GitLab** is a comprehensive **DevSecOps platform** that provides source code management, Continuous Integration/Continuous Deployment (CI/CD), security testing, issue tracking, package management, and infrastructure automation within a single application.

Unlike traditional Git hosting services that primarily focus on version control, GitLab aims to cover the **entire software development lifecycle (SDLC)** from planning to monitoring.

GitLab is available as:

- GitLab Community Edition (CE)
- GitLab Enterprise Edition (EE)
- GitLab Dedicated
- GitLab SaaS (gitlab.com)

GitLab has become one of the most widely deployed DevOps platforms in enterprise environments.

Because GitLab stores source code, deployment pipelines, credentials, access tokens, secrets, container registries, and infrastructure configurations, it is considered a high-value target during security assessments.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | GitLab |
| Default HTTP Port | TCP 80 |
| Default HTTPS Port | TCP 443 |
| Default SSH Port | TCP 22 |
| Git over HTTP | Yes |
| Git over SSH | Yes |
| REST API | Yes |
| GraphQL API | Yes |
| Authentication | Local, LDAP, OAuth, SAML, OpenID Connect |
| Encryption | TLS Supported |

---

# Primary Purpose

GitLab enables organizations to:

- Host Git repositories
- Manage CI/CD pipelines
- Perform code reviews
- Track issues
- Store packages
- Manage releases
- Scan application security
- Automate deployments

---

# GitLab Architecture

```text
             Developers

         ┌────────┼────────┐

         ▼        ▼        ▼

      Git Push  Merge Request

                │

                ▼

             GitLab

      ┌────────┼────────┐

      ▼        ▼        ▼

Repositories CI/CD Registry

                │

          Deployments
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Repository | Source code storage |
| Project | Development workspace |
| Group | Project organization |
| Runner | Executes CI/CD jobs |
| Pipeline | Automation workflow |
| Registry | Container and package storage |
| Wiki | Documentation |
| Issues | Project tracking |

---

# Communication Workflow

```text
Developer

     │

Git Push

     ▼

GitLab Repository

     │

Pipeline Trigger

     ▼

GitLab Runner

     │

Build

Test

Deploy

     ▼

Production
```

---

# Repository Structure

A typical GitLab project may contain:

```text
Project

├── Source Code

├── .gitlab-ci.yml

├── Documentation

├── Issues

├── Merge Requests

├── Releases

└── Packages
```

---

# GitLab CI/CD

GitLab pipelines are defined using the **`.gitlab-ci.yml`** file.

Example pipeline stages:

```text
Pipeline

├── Build

├── Unit Tests

├── Security Scan

├── Package

├── Deploy

└── Notifications
```

Pipelines execute automatically after commits, merge requests, or scheduled jobs.

---

# GitLab Runner

GitLab Runner executes CI/CD jobs.

```text
GitLab Server

      │

Assign Job

      ▼

Runner

      │

Execute Pipeline

      ▼

Return Status
```

Runner types include:

- Shared Runner
- Group Runner
- Project Runner
- Instance Runner

---

# Enterprise Usage

GitLab is commonly deployed in:

- Financial institutions
- Government organizations
- Software companies
- Healthcare
- Telecommunications
- Cloud providers
- Defense contractors
- Enterprise DevOps teams

---

# Typical Enterprise Architecture

```text
          Developers

               │

         Git Push / API

               ▼

        GitLab Server

      ┌────────┼────────┐

      ▼        ▼        ▼

 Repository CI/CD Registry

               │

        GitLab Runners

               │

      Kubernetes Cluster

               │

        Production
```

---

# Security Features

GitLab includes numerous built-in security capabilities.

| Feature | Purpose |
|----------|----------|
| SAST | Static code analysis |
| DAST | Dynamic application testing |
| Dependency Scanning | Vulnerable packages |
| Secret Detection | Credential discovery |
| Container Scanning | Image security |
| License Compliance | OSS license validation |
| Code Quality | Maintainability analysis |

---

# APIs

GitLab exposes multiple APIs.

| API | Purpose |
|------|---------|
| REST API | Administration |
| GraphQL API | Flexible queries |
| Webhooks | Event notifications |
| Runner API | Job execution |
| Container Registry API | Image management |

---

# Nmap Detection

Basic Scan

```bash
nmap -p80,443 target
```

Version Detection

```bash
nmap -sV -p80,443 target
```

Aggressive Scan

```bash
nmap -A target
```

HTTPS Scan

```bash
nmap -sV -p443 target
```

---

# Useful NSE Scripts

Retrieve HTTP Title

```bash
nmap --script http-title -p443 target
```

Retrieve HTTP Headers

```bash
nmap --script http-headers -p443 target
```

Enumerate HTTP Methods

```bash
nmap --script http-methods -p443 target
```

SSL Certificate Information

```bash
nmap --script ssl-cert -p443 target
```

Supported TLS Ciphers

```bash
nmap --script ssl-enum-ciphers -p443 target
```

---

# Example Output

```text
443/tcp open https

GitLab
```

Example Banner

```text
Server:

GitLab

Version:

18.0

Web Server:

NGINX
```

---

# Information That Can Be Collected

Enumeration may reveal:

- GitLab version
- Web server
- TLS configuration
- HTTP headers
- Authentication methods
- API availability
- SSH support
- Container Registry endpoints
- GraphQL endpoint
- Runner configuration hints

---

# Blue Team Perspective

Recommendations

- Enable Multi-Factor Authentication (MFA).
- Restrict administrator accounts.
- Protect API access tokens.
- Encrypt all communications with TLS.
- Keep GitLab updated.
- Monitor Runner activity.
- Protect secrets stored in CI/CD variables.
- Enable audit logging.

---

# Red Team Perspective

Interesting Targets

- Enterprise DevOps platforms
- Internal Git repositories
- CI/CD infrastructure
- Container registries
- Cloud-native deployments
- Kubernetes integrations
- Self-hosted GitLab instances

Useful Enumeration

```bash
nmap -sV \
--script http-title,http-headers,http-methods,ssl-cert \
-p443 target
```

Potential Findings

- GitLab version
- Web server
- Available APIs
- TLS configuration
- Authentication mechanisms
- Registry endpoints
- Administrative interface
- Runner infrastructure

---

# Common Security Risks

Frequently observed GitLab weaknesses include:

- Weak administrator passwords
- Publicly accessible private repositories
- Leaked Personal Access Tokens
- Misconfigured CI/CD variables
- Outdated GitLab versions
- Vulnerable GitLab Runners
- Excessive user permissions
- Exposed administrative interfaces

---

# Authentication Model

GitLab supports multiple authentication providers.

| Authentication Method | Description |
|-----------------------|-------------|
| Local Database | Built-in user accounts |
| LDAP | Enterprise directory integration |
| OAuth 2.0 | Third-party identity providers |
| SAML | Single Sign-On |
| OpenID Connect | Federated authentication |
| Two-Factor Authentication | Additional account protection |

---

# GitLab Runner Security

```text
Developer

     │

Push Code

     ▼

GitLab

     │

Pipeline

     ▼

Runner

     │

Temporary Build Environment

     ▼

Artifacts
```

Runners should execute in isolated environments to reduce the impact of malicious or compromised build jobs.

---

# GitLab vs Jenkins

| Feature | GitLab | Jenkins |
|----------|---------|----------|
| Git Repository | Native | External |
| CI/CD | Built-in | Plugin-Based |
| Issue Tracking | Yes | Limited |
| Container Registry | Native | External |
| DevSecOps Features | Extensive | Plugin-Based |
| Package Registry | Yes | Limited |
| Pipeline as Code | Yes | Yes |

---

# Best Practices

- Require MFA for privileged users.
- Protect Personal Access Tokens.
- Restrict Runner permissions.
- Isolate build environments.
- Enable branch protection.
- Review merge requests carefully.
- Rotate secrets regularly.
- Keep GitLab and Runners updated.

---

# Real-World Examples

| Environment | Typical GitLab Usage |
|-------------|---------------------|
| Software Company | Source Code Management |
| Banking | Secure CI/CD |
| Cloud Platform | Kubernetes Deployment |
| Enterprise SaaS | DevSecOps Platform |
| Government | Internal Git Hosting |
| Healthcare | Application Development |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| GitLab HTTPS | Web Interface | 443 |
| GitLab HTTP | Web Interface | 80 |
| Git over SSH | Source Control | 22 |
| Jenkins | CI/CD Automation | 8080 |
| Docker Registry | Container Images | 5000 |

---

# Summary

GitLab is a comprehensive DevSecOps platform that combines source code management, CI/CD, security testing, package management, and deployment automation into a unified solution. Its integrated approach streamlines software development while centralizing critical assets such as repositories, credentials, pipelines, and deployment configurations. During reconnaissance, GitLab services may reveal version information, authentication methods, API endpoints, TLS configuration, and CI/CD infrastructure details. Organizations should secure GitLab by enforcing MFA, protecting access tokens, restricting Runner permissions, isolating build environments, and maintaining up-to-date software.

---

# Chapter 39 — SonarQube

## Overview

**SonarQube** is a platform for **continuous code quality inspection and security analysis**. It performs static application security testing (SAST), identifies bugs, detects security vulnerabilities, measures technical debt, and evaluates overall code quality.

Developed by **SonarSource**, SonarQube integrates seamlessly into modern CI/CD pipelines, allowing organizations to identify software defects before applications reach production.

Unlike traditional vulnerability scanners that analyze running systems, SonarQube analyzes **source code** and build artifacts.

It is commonly deployed in:

- DevSecOps platforms
- Enterprise software development
- CI/CD pipelines
- Cloud-native environments
- Financial institutions
- Government software projects
- SaaS companies
- Open-source projects

Because SonarQube stores source code metadata, project configurations, quality reports, authentication tokens, and user information, an exposed or improperly configured instance can reveal valuable intelligence about an organization's software development lifecycle.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | SonarQube |
| Default HTTP Port | TCP 9000 |
| HTTPS Port | Configurable |
| Transport | HTTP / HTTPS |
| Encryption | TLS Supported |
| Authentication | Local, LDAP, SAML, GitHub, GitLab, Azure AD |
| Analysis Type | Static Code Analysis (SAST) |

---

# Primary Purpose

SonarQube helps organizations:

- Detect security vulnerabilities
- Identify programming bugs
- Measure code quality
- Reduce technical debt
- Enforce coding standards
- Review pull requests
- Monitor code coverage
- Improve software maintainability

---

# SonarQube Architecture

```text
          Developers

               │

        Push Source Code

               ▼

        CI/CD Pipeline

               │

        Sonar Scanner

               ▼

         SonarQube Server

               │

     ┌─────────┼─────────┐

     ▼         ▼         ▼

 Database   Reports   Dashboard
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| SonarQube Server | Central analysis platform |
| Sonar Scanner | Collects project data |
| Database | Stores analysis results |
| Project | Source code repository |
| Quality Gate | Pass/Fail evaluation |
| Rule Set | Coding standards |
| Dashboard | Visualization interface |

---

# Communication Workflow

```text
Developer

     │

Commit Code

     ▼

CI/CD Pipeline

     │

Execute Scanner

     ▼

SonarQube Server

     │

Analyze Code

     ▼

Generate Report

     ▼

Quality Gate Result
```

---

# Analysis Workflow

```text
Source Code

      │

Static Analysis

      ▼

Bug Detection

      ▼

Security Analysis

      ▼

Code Smells

      ▼

Quality Gate

      ▼

Report
```

---

# Code Quality Metrics

SonarQube evaluates numerous software quality metrics.

| Metric | Description |
|----------|-------------|
| Bugs | Programming defects |
| Vulnerabilities | Security issues |
| Code Smells | Maintainability problems |
| Technical Debt | Estimated remediation effort |
| Coverage | Test coverage percentage |
| Duplications | Repeated code |
| Reliability Rating | Bug severity score |
| Security Rating | Vulnerability severity |

---

# Supported Languages

SonarQube supports many programming languages.

| Language | Supported |
|-----------|-----------|
| Java | Yes |
| C# | Yes |
| Python | Yes |
| JavaScript | Yes |
| TypeScript | Yes |
| PHP | Yes |
| Go | Yes |
| C/C++ | Yes |
| Kotlin | Yes |
| Ruby | Yes |

---

# Enterprise Usage

SonarQube is commonly deployed in:

- Enterprise DevSecOps
- Banking
- Healthcare
- Government
- Defense
- Software companies
- Cloud platforms
- SaaS providers

---

# Typical Enterprise Architecture

```text
      Developers

           │

      Git Repository

           │

     CI/CD Pipeline

           │

    Sonar Scanner

           │

     SonarQube

      ┌────┴────┐

      ▼         ▼

 Database  Dashboard
```

---

# Quality Gates

A Quality Gate determines whether a project satisfies predefined quality standards.

Example policy:

```text
Coverage > 80%

No Critical Vulnerabilities

No Blocker Bugs

Technical Debt < 5%

↓

PASS
```

If any required condition fails, the pipeline can be configured to stop automatically.

---

# Nmap Detection

Basic Scan

```bash
nmap -p9000 target
```

Version Detection

```bash
nmap -sV -p9000 target
```

Aggressive Scan

```bash
nmap -A -p9000 target
```

HTTPS Scan

```bash
nmap -sV -p443 target
```

---

# Useful NSE Scripts

Retrieve HTTP Title

```bash
nmap --script http-title -p9000 target
```

Retrieve HTTP Headers

```bash
nmap --script http-headers -p9000 target
```

Enumerate HTTP Methods

```bash
nmap --script http-methods -p9000 target
```

Retrieve Banner

```bash
nmap --script banner -p9000 target
```

SSL Certificate

```bash
nmap --script ssl-cert -p443 target
```

---

# Example Output

```text
9000/tcp open http

SonarQube
```

Example Banner

```text
Server:

SonarQube

Version:

2025.3 LTS
```

---

# Information That Can Be Collected

Enumeration may reveal:

- SonarQube version
- Server banner
- HTTP headers
- Authentication methods
- API availability
- Project names
- Public dashboards
- Plugin information
- Web server details

---

# REST API

SonarQube exposes a REST API for automation and integration.

Common endpoints include:

| Endpoint | Purpose |
|-----------|----------|
| /api/system/status | Server status |
| /api/projects/search | Project list |
| /api/measures | Project metrics |
| /api/issues/search | Security findings |
| /api/qualitygates | Quality Gate information |
| /api/users | User management |

The REST API is widely used by CI/CD systems and reporting tools.

---

# Blue Team Perspective

Recommendations

- Require authentication for all users.
- Restrict anonymous project access.
- Protect API tokens.
- Enable HTTPS.
- Limit administrator accounts.
- Review Quality Gate policies regularly.
- Monitor authentication logs.
- Keep SonarQube updated.

---

# Red Team Perspective

Interesting Targets

- Enterprise CI/CD platforms
- Internal development environments
- DevSecOps infrastructure
- Software quality portals
- Source code management systems
- Cloud-native build environments

Useful Enumeration

```bash
nmap -sV \
--script http-title,http-headers,http-methods \
-p9000 target
```

Potential Findings

- SonarQube version
- Public projects
- API endpoints
- Authentication configuration
- Server technology
- Plugin information
- Build infrastructure

---

# Common Security Risks

Frequently observed SonarQube weaknesses include:

- Anonymous project access
- Exposed REST API
- Weak administrator passwords
- Leaked API tokens
- Outdated plugins
- Missing TLS
- Excessive user permissions
- Publicly accessible dashboards

---

# Authentication Model

SonarQube supports several authentication providers.

| Method | Description |
|----------|-------------|
| Local Accounts | Internal users |
| LDAP | Enterprise directory |
| SAML | Single Sign-On |
| GitHub | OAuth integration |
| GitLab | OAuth integration |
| Azure Active Directory | Enterprise identity |

API tokens are commonly used for CI/CD integrations and should be treated as sensitive credentials.

---

# SonarQube vs Traditional SAST Tools

| Feature | SonarQube | Traditional SAST |
|----------|-----------|------------------|
| Static Analysis | Yes | Yes |
| CI/CD Integration | Native | Varies |
| Dashboard | Comprehensive | Usually Limited |
| Technical Debt Analysis | Yes | Rare |
| Quality Gates | Yes | Limited |
| Open Source Edition | Yes | Varies |

---

# Best Practices

- Enforce HTTPS across all interfaces.
- Protect API tokens using secure secret management.
- Disable anonymous project browsing.
- Apply least-privilege permissions.
- Review Quality Gates periodically.
- Keep plugins and the server updated.
- Monitor audit logs.
- Integrate SonarQube into every production pipeline.

---

# Real-World Examples

| Environment | Typical SonarQube Usage |
|-------------|-------------------------|
| Banking | Secure Code Review |
| Enterprise SaaS | CI/CD Quality Control |
| Government | Compliance Verification |
| Healthcare | Secure Development |
| Cloud Platform | Automated Code Analysis |
| Software Company | Technical Debt Monitoring |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| SonarQube HTTP | Web Interface | 9000 |
| HTTPS | Secure Web Interface | 443 |
| GitLab | DevSecOps Platform | 443 |
| Jenkins | CI/CD Automation | 8080 |
| Docker Remote API | Container Management | 2375 / 2376 |

---

# Summary

SonarQube is a leading static code analysis platform that helps organizations improve software quality, identify vulnerabilities, reduce technical debt, and enforce secure coding practices. Its integration with CI/CD pipelines and support for multiple programming languages make it a key component of modern DevSecOps environments. During reconnaissance, SonarQube services may reveal version information, API endpoints, public projects, authentication methods, and infrastructure details. Organizations should secure SonarQube by enforcing authentication, protecting API tokens, enabling HTTPS, restricting project visibility, and maintaining an up-to-date installation.

---

# Chapter 40 — Grafana

## Overview

**Grafana** is one of the world's leading **observability and visualization platforms**, designed to display metrics, logs, traces, and operational data through highly customizable dashboards.

Originally released by Grafana Labs, Grafana has become a standard component of modern monitoring stacks and is widely integrated with platforms such as Prometheus, Elasticsearch, InfluxDB, Loki, OpenSearch, Graphite, Azure Monitor, CloudWatch, and many others.

Unlike monitoring systems that primarily collect data, Grafana focuses on **visualizing and analyzing information collected from multiple data sources**.

Grafana is commonly deployed in:

- Kubernetes clusters
- Cloud infrastructure
- Enterprise data centers
- DevOps platforms
- Network Operations Centers (NOC)
- Security Operations Centers (SOC)
- Industrial monitoring
- IoT platforms

Because Grafana often aggregates operational data from numerous systems, a compromised or publicly exposed instance may reveal infrastructure topology, internal hostnames, cloud environments, application metrics, and monitoring configurations.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Grafana |
| Default HTTP Port | TCP 3000 |
| HTTPS Port | Configurable |
| Transport | HTTP / HTTPS |
| Encryption | TLS Supported |
| Authentication | Local, LDAP, OAuth, SAML, OpenID Connect |
| REST API | Yes |
| Default Database | SQLite (Default), MySQL, PostgreSQL |

---

# Primary Purpose

Grafana provides:

- Metrics visualization
- Dashboard creation
- Alert management
- Log exploration
- Distributed tracing
- Infrastructure monitoring
- Performance analysis
- Observability

---

# Grafana Architecture

```text
               Data Sources

      ┌──────────┼──────────┐

      ▼          ▼          ▼

 Prometheus  Elasticsearch  Loki

      │          │          │

      └──────────┼──────────┘

                 ▼

             Grafana

        ┌────────┼────────┐

        ▼        ▼        ▼

 Dashboards Alerts Users

                 │

                 ▼

            Administrators
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Dashboard | Data visualization |
| Panel | Individual visualization |
| Data Source | External monitoring system |
| Alert Rule | Notification trigger |
| Folder | Dashboard organization |
| User | Platform access |
| Organization | Multi-tenant management |
| Plugin | Extend functionality |

---

# Communication Workflow

```text
Monitoring System

        │

Collect Metrics

        ▼

Database

        │

Query

        ▼

Grafana

        │

Render Dashboard

        ▼

Administrator
```

---

# Dashboard Structure

A dashboard is composed of multiple visualization panels.

```text
Dashboard

├── CPU Usage

├── Memory Usage

├── Disk I/O

├── Network Traffic

├── Error Rate

├── Response Time

└── Alerts
```

---

# Supported Data Sources

Grafana supports dozens of data sources.

| Data Source | Purpose |
|-------------|----------|
| Prometheus | Metrics |
| Loki | Logs |
| Elasticsearch | Search & Logs |
| OpenSearch | Search |
| InfluxDB | Time-Series Database |
| Graphite | Metrics |
| MySQL | SQL Data |
| PostgreSQL | SQL Data |
| MSSQL | SQL Data |
| Azure Monitor | Cloud Monitoring |
| Amazon CloudWatch | AWS Monitoring |

---

# Enterprise Usage

Grafana is commonly deployed in:

- Enterprise monitoring
- Kubernetes platforms
- Financial institutions
- Government agencies
- Healthcare
- Manufacturing
- Telecommunications
- Cloud providers

---

# Typical Enterprise Architecture

```text
               Servers

        ┌────────┼────────┐

        ▼        ▼        ▼

 Linux   Windows  Network

        │        │        │

        └────────┼────────┘

             Prometheus

                  │

             Grafana

        ┌────────┼────────┐

        ▼        ▼        ▼

  Dashboards Alerts Reports
```

---

# Alerting System

Grafana can generate alerts based on metrics.

```text
CPU Usage

      │

Threshold > 90%

      ▼

Alert Rule

      ▼

Notification

      ▼

Email / Slack / Teams / PagerDuty
```

Alerts help administrators identify issues before they affect production services.

---

# Organizations and Permissions

Grafana supports multi-tenancy through Organizations.

```text
Grafana

├── Organization A

│      ├── Users

│      └── Dashboards

├── Organization B

└── Organization C
```

Role-based access control helps isolate teams and environments.

---

# Plugins

Grafana provides an extensive plugin ecosystem.

Common plugin categories include:

- Data source plugins
- Visualization plugins
- Application plugins
- Panel plugins
- Alert integrations

Plugins allow organizations to extend Grafana without modifying the core platform.

---

# Nmap Detection

Basic Scan

```bash
nmap -p3000 target
```

Version Detection

```bash
nmap -sV -p3000 target
```

Aggressive Scan

```bash
nmap -A -p3000 target
```

HTTPS Scan

```bash
nmap -sV -p443 target
```

---

# Useful NSE Scripts

Retrieve HTTP Title

```bash
nmap --script http-title -p3000 target
```

Retrieve HTTP Headers

```bash
nmap --script http-headers -p3000 target
```

Enumerate HTTP Methods

```bash
nmap --script http-methods -p3000 target
```

Retrieve Banner

```bash
nmap --script banner -p3000 target
```

SSL Certificate

```bash
nmap --script ssl-cert -p443 target
```

SSL Cipher Enumeration

```bash
nmap --script ssl-enum-ciphers -p443 target
```

---

# Example Output

```text
3000/tcp open http

Grafana
```

Example Banner

```text
Server:

Grafana

Version:

12.x

Web Server:

Grafana HTTP Server
```

---

# Information That Can Be Collected

Enumeration may reveal:

- Grafana version
- Dashboard titles
- HTTP headers
- Authentication methods
- Public dashboards
- Plugin information
- REST API availability
- TLS configuration
- Web server details

---

# REST API

Grafana provides a comprehensive REST API.

Common endpoints include:

| Endpoint | Purpose |
|----------|----------|
| /api/health | Server health |
| /api/search | Dashboard search |
| /api/dashboards | Dashboard management |
| /api/datasources | Data source configuration |
| /api/users | User management |
| /api/org | Organization information |
| /api/admin | Administrative operations |

API access should always be protected using authentication and appropriate authorization controls.

---

# Blue Team Perspective

Recommendations

- Disable anonymous access unless explicitly required.
- Enforce Multi-Factor Authentication (MFA).
- Protect API keys and service accounts.
- Restrict dashboard visibility.
- Enable HTTPS.
- Keep plugins updated.
- Monitor login activity.
- Enable audit logging.

---

# Red Team Perspective

Interesting Targets

- Monitoring infrastructure
- SOC environments
- Kubernetes monitoring
- Enterprise dashboards
- Cloud monitoring platforms
- Internal metrics systems
- Network monitoring servers

Useful Enumeration

```bash
nmap -sV \
--script http-title,http-headers,http-methods,ssl-cert \
-p3000 target
```

Potential Findings

- Grafana version
- Authentication methods
- Public dashboards
- Installed plugins
- REST API
- TLS configuration
- Infrastructure naming conventions
- Monitoring technologies

---

# Common Security Risks

Frequently observed Grafana weaknesses include:

- Anonymous dashboard access
- Default administrator credentials
- Publicly exposed dashboards
- Weak API key management
- Missing TLS encryption
- Excessive user permissions
- Outdated plugins
- Information disclosure through dashboards

---

# Authentication Model

Grafana supports multiple identity providers.

| Authentication Method | Description |
|-----------------------|-------------|
| Local Database | Built-in users |
| LDAP | Enterprise directory |
| OAuth 2.0 | Third-party identity providers |
| SAML | Single Sign-On |
| OpenID Connect | Federated authentication |
| Anonymous Access | Optional public dashboards |

Organizations should disable anonymous access unless there is a clear operational requirement.

---

# Alerting Architecture

```text
Data Source

     │

Collect Metrics

     ▼

Grafana

     │

Evaluate Rules

     ▼

Alert Manager

     │

Notifications

     ▼

Email / Slack / Teams / Webhooks
```

Modern Grafana deployments integrate alerting directly into operational workflows.

---

# Grafana vs Kibana

| Feature | Grafana | Kibana |
|----------|----------|---------|
| Primary Purpose | Observability Platform | Elasticsearch Visualization |
| Metrics | Excellent | Limited |
| Logs | Yes | Excellent |
| Tracing | Yes | Limited |
| Multiple Data Sources | Yes | Primarily Elastic Stack |
| Dashboard Flexibility | Very High | High |
| Alerting | Native | Native |

---

# Best Practices

- Require MFA for privileged users.
- Disable anonymous access.
- Protect API tokens and service accounts.
- Restrict dashboard permissions.
- Regularly update Grafana and plugins.
- Encrypt all communications with TLS.
- Audit user activity.
- Monitor dashboard sharing.

---

# Real-World Examples

| Environment | Typical Grafana Usage |
|-------------|----------------------|
| Kubernetes | Cluster Monitoring |
| Banking | Infrastructure Dashboards |
| Cloud Provider | Resource Monitoring |
| SOC | Security Metrics |
| NOC | Network Operations |
| Manufacturing | Industrial Monitoring |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Grafana HTTP | Web Interface | 3000 |
| HTTPS | Secure Web Interface | 443 |
| Prometheus | Metrics Collection | 9090 |
| Loki | Log Aggregation | 3100 |
| Elasticsearch | Search & Analytics | 9200 |

---

# Summary

Grafana is a powerful observability platform that centralizes metrics, logs, traces, dashboards, and alerts from diverse monitoring systems into a single interface. Its flexibility, plugin ecosystem, and extensive integrations have made it a standard component of modern DevOps, SRE, and enterprise monitoring environments. During reconnaissance, Grafana services may expose dashboard names, infrastructure metadata, authentication methods, API endpoints, and monitoring configurations. Organizations should secure Grafana by enforcing strong authentication, disabling anonymous access, protecting API tokens, restricting dashboard visibility, enabling TLS, and continuously monitoring user activity.

---

# Chapter 41 — Kibana

## Overview

**Kibana** is a powerful **data visualization, exploration, and analytics platform** that is part of the **Elastic Stack (ELK Stack)**, which consists of Elasticsearch, Logstash, Kibana, and Beats.

Developed by Elastic, Kibana enables users to search, visualize, analyze, and monitor large volumes of structured and unstructured data stored in Elasticsearch.

Unlike traditional dashboards that focus only on metrics, Kibana provides advanced capabilities for:

- Log analysis
- Security monitoring
- Infrastructure monitoring
- Threat hunting
- Application Performance Monitoring (APM)
- Machine Learning visualization
- SIEM operations
- Business analytics

Because Kibana provides direct access to enterprise log data, monitoring dashboards, infrastructure information, and security events, improperly secured deployments may expose highly valuable reconnaissance information.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Kibana |
| Default HTTP Port | TCP 5601 |
| HTTPS | Supported |
| Transport | HTTP / HTTPS |
| Backend | Elasticsearch |
| Authentication | Local, LDAP, SAML, OpenID Connect, OAuth |
| REST API | Yes |
| Application Layer | Yes |

---

# Primary Purpose

Kibana provides:

- Log visualization
- Data exploration
- Dashboard creation
- Threat hunting
- SIEM dashboards
- Infrastructure monitoring
- Application monitoring
- Machine Learning visualization

---

# Kibana Architecture

```text
             Data Sources

      ┌────────┼─────────┐

      ▼        ▼         ▼

    Beats   Logstash   Elastic Agent

             │

             ▼

       Elasticsearch

             │

             ▼

           Kibana

      ┌──────┼────────┐

      ▼      ▼        ▼

 Dashboards SIEM Discover
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Discover | Search raw logs |
| Dashboard | Visualizations |
| Lens | Interactive analytics |
| Maps | Geographic visualization |
| Canvas | Reporting |
| Stack Management | Administration |
| Dev Tools | API console |
| Machine Learning | Anomaly detection |

---

# Communication Workflow

```text
Servers

     │

Generate Logs

     ▼

Logstash / Beats

     ▼

Elasticsearch

     ▼

Kibana

     ▼

Visualization
```

---

# Data Flow

```text
Applications

      │

Logs

      ▼

Beats

      ▼

Logstash

      ▼

Elasticsearch

      ▼

Kibana
```

---

# Kibana Spaces

Spaces allow logical separation of dashboards.

```text
Kibana

├── SOC

├── DevOps

├── Production

├── Development

└── Finance
```

Each space can have separate dashboards, users, and permissions.

---

# Enterprise Usage

Kibana is commonly deployed in:

- Security Operations Centers
- Network Operations Centers
- Cloud platforms
- Financial institutions
- Government agencies
- Healthcare
- Telecommunications
- Enterprise IT

---

# Typical Enterprise Architecture

```text
        Enterprise Systems

     ┌────────┼────────┐

     ▼        ▼        ▼

 Servers  Firewalls  Applications

      │        │        │

      └────────┼────────┘

           Log Collectors

                │

                ▼

         Elasticsearch Cluster

                │

                ▼

             Kibana
```

---

# Dashboards

Dashboards combine multiple visualizations.

Example:

```text
Security Dashboard

├── Authentication Events

├── Failed Logins

├── Malware Alerts

├── Firewall Activity

├── DNS Queries

├── Network Traffic

└── Active Users
```

---

# Discover Module

The Discover interface enables interactive searching.

Capabilities include:

- Full-text search
- Filtering
- Time-based queries
- Field inspection
- Saved searches
- Exporting results

---

# Dev Tools

Kibana provides an integrated console for Elasticsearch APIs.

Example request:

```http
GET /_cluster/health
```

Example search:

```http
GET logs-*/_search
```

This feature greatly simplifies Elasticsearch administration.

---

# Machine Learning

Commercial editions of Kibana include Machine Learning.

Example use cases:

- Network anomaly detection
- Login anomaly detection
- Fraud detection
- Resource consumption anomalies
- Application performance anomalies

---

# SIEM Capabilities

Elastic Security integrates directly with Kibana.

```text
Endpoints

      │

Security Events

      ▼

Elasticsearch

      ▼

Elastic Security

      ▼

SOC Dashboard
```

Security analysts use Kibana for investigation and threat hunting.

---

# Nmap Detection

Basic Scan

```bash
nmap -p5601 target
```

Version Detection

```bash
nmap -sV -p5601 target
```

Aggressive Scan

```bash
nmap -A -p5601 target
```

HTTPS Scan

```bash
nmap -sV -p443 target
```

---

# Useful NSE Scripts

Retrieve HTTP Title

```bash
nmap --script http-title -p5601 target
```

Retrieve HTTP Headers

```bash
nmap --script http-headers -p5601 target
```

Enumerate HTTP Methods

```bash
nmap --script http-methods -p5601 target
```

Retrieve Banner

```bash
nmap --script banner -p5601 target
```

SSL Certificate

```bash
nmap --script ssl-cert -p443 target
```

SSL Cipher Enumeration

```bash
nmap --script ssl-enum-ciphers -p443 target
```

---

# Example Output

```text
5601/tcp open http

Kibana
```

Example Banner

```text
Server:

Kibana

Version:

9.x
```

---

# Information That Can Be Collected

Enumeration may reveal:

- Kibana version
- HTTP headers
- Public dashboards
- Space names
- Elasticsearch connectivity
- Authentication methods
- TLS configuration
- API availability
- Plugin information

---

# REST APIs

Kibana exposes numerous REST APIs.

Common endpoints:

| Endpoint | Purpose |
|----------|----------|
| /api/status | Server status |
| /api/features | Available features |
| /api/spaces | Space management |
| /api/saved_objects | Dashboard management |
| /internal/security | Authentication |
| /api/actions | Alerting |

These APIs should be protected using authentication and role-based authorization.

---

# Blue Team Perspective

Recommendations

- Enable HTTPS for all connections.
- Restrict anonymous access.
- Use role-based access control.
- Integrate centralized identity providers.
- Protect Elasticsearch from direct public access.
- Monitor audit logs.
- Regularly update Kibana.
- Secure saved objects and dashboards.

---

# Red Team Perspective

Interesting Targets

- SIEM platforms
- SOC dashboards
- Log management systems
- Cloud monitoring
- Enterprise logging
- Security monitoring infrastructure
- Elastic Stack deployments

Useful Enumeration

```bash
nmap -sV \
--script http-title,http-headers,http-methods \
-p5601 target
```

Potential Findings

- Kibana version
- Dashboard titles
- Space names
- Authentication methods
- REST API availability
- Plugin information
- Backend technologies
- Elasticsearch integration

---

# Common Security Risks

Frequently observed Kibana weaknesses include:

- Anonymous dashboard access
- Public Elasticsearch exposure
- Weak administrator passwords
- Missing TLS
- Excessive user permissions
- Public Dev Tools access
- Outdated Elastic Stack versions
- Information disclosure through dashboards

---

# Authentication Model

Kibana supports several enterprise authentication mechanisms.

| Method | Description |
|----------|-------------|
| Native Users | Internal authentication |
| LDAP | Enterprise directory |
| Active Directory | Windows integration |
| SAML | Single Sign-On |
| OpenID Connect | Federated authentication |
| OAuth 2.0 | Identity provider integration |

---

# Kibana vs Grafana

| Feature | Kibana | Grafana |
|----------|---------|----------|
| Primary Purpose | Log Analytics | Metrics & Observability |
| Elasticsearch Integration | Native | Plugin |
| SIEM Features | Extensive | Limited |
| Metrics | Good | Excellent |
| Log Analysis | Excellent | Good |
| Distributed Tracing | Supported | Supported |
| Machine Learning | Native | Limited |

---

# Best Practices

- Enforce HTTPS across all interfaces.
- Disable anonymous access.
- Protect Dev Tools from unauthorized users.
- Implement least-privilege permissions.
- Secure Elasticsearch independently.
- Enable audit logging.
- Review dashboard permissions regularly.
- Keep the entire Elastic Stack updated.

---

# Real-World Examples

| Environment | Typical Kibana Usage |
|-------------|----------------------|
| SOC | Threat Hunting |
| Enterprise IT | Log Analysis |
| Banking | Security Monitoring |
| Healthcare | Compliance Monitoring |
| Cloud Provider | Infrastructure Monitoring |
| Government | Incident Investigation |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Kibana HTTP | Web Interface | 5601 |
| Elasticsearch | Search Engine | 9200 |
| Logstash | Log Processing | 5044 / 9600 |
| Beats | Log Shipping | Various |
| Grafana | Observability | 3000 |

---

# Summary

Kibana is the visualization and analytics component of the Elastic Stack, enabling organizations to search, analyze, and visualize operational and security data stored in Elasticsearch. Its capabilities extend from log analysis and infrastructure monitoring to SIEM operations and machine learning-assisted threat detection. During reconnaissance, Kibana services may reveal version information, dashboard names, authentication mechanisms, API endpoints, and backend integrations. Organizations should secure Kibana by enforcing strong authentication, restricting dashboard access, protecting Dev Tools, enabling TLS, and maintaining a secure Elastic Stack deployment.

---

# Chapter 42 — Prometheus

## Overview

**Prometheus** is an open-source **monitoring and alerting toolkit** originally developed at SoundCloud and now maintained by the **Cloud Native Computing Foundation (CNCF)**.

Prometheus is designed to collect, store, query, and analyze time-series metrics from applications, servers, containers, and network devices.

Unlike traditional monitoring systems that rely on agents pushing data to a server, Prometheus primarily uses a **pull-based architecture**, periodically scraping metrics from configured targets.

Today, Prometheus is one of the most widely adopted monitoring platforms in cloud-native environments and is considered the standard monitoring solution for Kubernetes.

Prometheus is commonly deployed in:

- Kubernetes clusters
- Docker environments
- Cloud-native platforms
- Enterprise data centers
- DevOps infrastructures
- Site Reliability Engineering (SRE)
- Infrastructure monitoring
- Microservices

Because Prometheus continuously collects infrastructure metrics, an exposed instance can reveal valuable information about an organization's internal systems, services, performance, and architecture.

---

# Basic Information

| Property | Value |
|-----------|-------|
| Full Name | Prometheus |
| Default HTTP Port | TCP 9090 |
| Transport | HTTP / HTTPS |
| Data Type | Time-Series Database (TSDB) |
| Query Language | PromQL |
| Authentication | External (Reverse Proxy/OAuth) |
| Encryption | TLS Supported |
| REST API | Yes |

---

# Primary Purpose

Prometheus provides:

- Metrics collection
- Time-series storage
- Infrastructure monitoring
- Service monitoring
- Alert generation
- Performance analysis
- Capacity planning
- Kubernetes monitoring

---

# Prometheus Architecture

```text
           Exporters

     ┌────────┼─────────┐

     ▼        ▼         ▼

 Node     MySQL     Application

 Exporter Exporter    Metrics

      │        │         │

      └────────┼─────────┘

               ▼

          Prometheus

               │

      ┌────────┼────────┐

      ▼        ▼        ▼

 Alertmanager API   TSDB

               │

               ▼

            Grafana
```

---

# Core Components

| Component | Purpose |
|-----------|----------|
| Prometheus Server | Metrics collection |
| Exporter | Exposes metrics |
| TSDB | Time-series storage |
| Alertmanager | Alert processing |
| PromQL | Query language |
| Service Discovery | Automatic target discovery |
| Recording Rules | Precomputed metrics |

---

# Communication Workflow

```text
Exporter

    │

Expose Metrics

    ▼

HTTP Endpoint

    │

Scrape

    ▼

Prometheus

    │

Store Metrics

    ▼

Query

    ▼

Dashboard / Alerts
```

---

# Metrics Collection

Prometheus periodically collects metrics.

```text
Target

    │

/metrics

    ▼

HTTP Response

    ▼

Prometheus

    ▼

Time-Series Database
```

Each metric consists of:

- Metric name
- Value
- Timestamp
- Labels

---

# Prometheus Data Model

Example metric:

```text
http_requests_total

Value:

15238

Labels:

method="GET"

status="200"

instance="web01"
```

Labels make Prometheus extremely flexible for filtering and aggregation.

---

# PromQL

PromQL is Prometheus' query language.

Example queries:

```text
up
```

```text
node_cpu_seconds_total
```

```text
rate(http_requests_total[5m])
```

```text
sum(rate(container_cpu_usage_seconds_total[5m]))
```

PromQL supports aggregation, filtering, mathematical operations, and time-based calculations.

---

# Exporters

Exporters expose metrics from various systems.

| Exporter | Purpose |
|-----------|----------|
| Node Exporter | Linux metrics |
| Windows Exporter | Windows metrics |
| Blackbox Exporter | Endpoint probing |
| SNMP Exporter | Network devices |
| MySQL Exporter | MySQL metrics |
| PostgreSQL Exporter | PostgreSQL metrics |
| Redis Exporter | Redis metrics |
| Kubernetes Exporter | Cluster metrics |

---

# Service Discovery

Prometheus supports automatic target discovery.

Supported environments include:

- Kubernetes
- Docker
- Consul
- EC2
- Azure
- Google Cloud
- OpenStack
- Static configurations

---

# Alertmanager

Alertmanager processes alerts generated by Prometheus.

```text
Prometheus

      │

Alert Rule

      ▼

Alertmanager

      │

Deduplicate

      ▼

Notifications

 ├── Email

 ├── Slack

 ├── Teams

 ├── PagerDuty

 └── Webhook
```

---

# Enterprise Usage

Prometheus is commonly deployed in:

- Kubernetes
- Financial institutions
- Cloud providers
- Enterprise SaaS
- Telecommunications
- Government
- Healthcare
- Manufacturing

---

# Typical Enterprise Architecture

```text
      Applications

   ┌──────┼────────┐

   ▼      ▼        ▼

Node   Database  Kubernetes

Exporter Exporter Exporter

      │      │        │

      └──────┼────────┘

          Prometheus

               │

      ┌────────┼────────┐

      ▼        ▼        ▼

 Alertmanager Grafana Long-Term Storage
```

---

# Recording Rules

Recording Rules precompute expensive PromQL queries.

Example:

```text
CPU Usage

↓

Average CPU

↓

Stored Metric

↓

Fast Queries
```

This improves dashboard performance and reduces query execution time.

---

# Federation

Large organizations often deploy multiple Prometheus servers.

```text
Regional Prometheus

      │

Federation

      ▼

Global Prometheus

      ▼

Enterprise Dashboard
```

Federation enables scalable monitoring across multiple environments.

---

# Nmap Detection

Basic Scan

```bash
nmap -p9090 target
```

Version Detection

```bash
nmap -sV -p9090 target
```

Aggressive Scan

```bash
nmap -A -p9090 target
```

HTTPS Scan

```bash
nmap -sV -p443 target
```

---

# Useful NSE Scripts

Retrieve HTTP Title

```bash
nmap --script http-title -p9090 target
```

Retrieve HTTP Headers

```bash
nmap --script http-headers -p9090 target
```

Enumerate HTTP Methods

```bash
nmap --script http-methods -p9090 target
```

Retrieve Banner

```bash
nmap --script banner -p9090 target
```

SSL Certificate

```bash
nmap --script ssl-cert -p443 target
```

---

# Example Output

```text
9090/tcp open http

Prometheus Time Series Collection
```

Example Banner

```text
Prometheus

Version:

3.x

Storage:

TSDB
```

---

# Information That Can Be Collected

Enumeration may reveal:

- Prometheus version
- HTTP headers
- Available endpoints
- Metric names
- Exporter types
- Service discovery configuration
- Alert rules
- Storage information
- Build details

---

# REST API

Prometheus provides a REST API.

Common endpoints include:

| Endpoint | Purpose |
|----------|----------|
| /api/v1/query | Execute PromQL |
| /api/v1/query_range | Time-range queries |
| /api/v1/targets | Active scrape targets |
| /api/v1/rules | Alert and recording rules |
| /api/v1/alerts | Active alerts |
| /metrics | Internal Prometheus metrics |

These endpoints should be protected from unauthorized access, as they can reveal sensitive operational details.

---

# Blue Team Perspective

Recommendations

- Restrict public access to Prometheus.
- Place Prometheus behind a reverse proxy with authentication.
- Enable HTTPS.
- Protect API endpoints.
- Limit access to metrics exporters.
- Monitor configuration changes.
- Secure Alertmanager integrations.
- Keep Prometheus updated.

---

# Red Team Perspective

Interesting Targets

- Kubernetes clusters
- Cloud-native platforms
- Monitoring infrastructure
- Enterprise metrics servers
- DevOps environments
- Container orchestration platforms
- Internal observability systems

Useful Enumeration

```bash
nmap -sV \
--script http-title,http-headers,http-methods \
-p9090 target
```

Potential Findings

- Prometheus version
- Metric endpoints
- Active exporters
- Monitoring targets
- Alert rules
- API availability
- Infrastructure naming conventions
- Kubernetes integrations

---

# Common Security Risks

Frequently observed Prometheus weaknesses include:

- Publicly accessible web interface
- Unprotected REST API
- Missing authentication
- Missing TLS encryption
- Information disclosure through metrics
- Exposed monitoring targets
- Weak reverse proxy configuration
- Outdated Prometheus versions

---

# Authentication Considerations

Prometheus does not provide a comprehensive built-in authentication system.

Authentication is commonly implemented through:

| Method | Description |
|----------|-------------|
| Reverse Proxy | NGINX, Apache |
| OAuth 2.0 | Identity provider integration |
| Basic Authentication | Proxy-based |
| Mutual TLS | Client certificate authentication |
| VPN Access | Internal-only deployment |

Organizations should avoid exposing Prometheus directly to the Internet without additional access controls.

---

# Prometheus vs Grafana

| Feature | Prometheus | Grafana |
|----------|------------|----------|
| Primary Role | Metrics Collection | Visualization |
| Database | Built-in TSDB | External Data Sources |
| Alerting | Native | Native |
| Dashboards | Basic | Advanced |
| Query Language | PromQL | Depends on Data Source |
| Metrics Storage | Yes | No |
| Visualization | Limited | Extensive |

---

# Best Practices

- Keep Prometheus on internal networks.
- Enable TLS for all communications.
- Protect API endpoints with authentication.
- Secure exporters individually.
- Regularly review alert rules.
- Limit service discovery scope.
- Monitor configuration changes.
- Keep Prometheus and exporters updated.

---

# Real-World Examples

| Environment | Typical Prometheus Usage |
|-------------|--------------------------|
| Kubernetes | Cluster Monitoring |
| Banking | Infrastructure Metrics |
| Cloud Provider | Resource Monitoring |
| SaaS Platform | Application Metrics |
| Telecommunications | Network Monitoring |
| Manufacturing | System Performance |

---

# Related Protocols

| Protocol | Purpose | Default Port |
|----------|----------|-------------|
| Prometheus HTTP | Metrics Server | 9090 |
| Grafana | Visualization | 3000 |
| Alertmanager | Alert Processing | 9093 |
| Node Exporter | Host Metrics | 9100 |
| Pushgateway | Push Metrics | 9091 |

---

# Summary

Prometheus is a leading open-source monitoring platform that collects, stores, and analyzes time-series metrics from infrastructure and applications. Its pull-based architecture, powerful PromQL language, extensive exporter ecosystem, and seamless integration with Kubernetes have made it a cornerstone of modern observability. During reconnaissance, Prometheus services may expose metric names, exporter information, monitoring targets, API endpoints, and infrastructure metadata. Organizations should secure Prometheus by restricting access, protecting its APIs, enabling TLS, authenticating users through reverse proxies, and regularly updating both the server and exporters.

---

# Chapter 43 — Summary

## Overview

Throughout this reference, we explored the most common network services encountered during penetration tests, vulnerability assessments, enterprise network administration, and security monitoring.

Understanding a service means far more than simply recognizing its default port. A security professional should understand:

- The purpose of the service
- Communication workflow
- Authentication mechanisms
- Common implementations
- Enterprise use cases
- Typical attack surface
- Nmap detection techniques
- NSE enumeration scripts
- Common security risks
- Defensive best practices

Mastering these topics enables faster service identification, more effective reconnaissance, and better security assessments.

---

# Service Categories

| Category | Services |
|----------|----------|
| Web Services | HTTP, HTTPS |
| Remote Administration | SSH, Telnet, RDP, VNC, WinRM |
| File Transfer & Sharing | FTP, FTPS, SFTP, SMB, NFS, rsync |
| Network Infrastructure | DNS, DHCP, RPC |
| Identity & Authentication | LDAP, Kerberos |
| Email Services | SMTP, POP3, IMAP |
| Voice over IP | SIP, RTP |
| Database Services | MySQL, PostgreSQL, MSSQL, Oracle, MongoDB, Redis, Elasticsearch |
| Containers | Docker API, Kubernetes |
| Messaging | MQTT, AMQP, Kafka |
| Development | Git |
| Enterprise Infrastructure | VMware, Printing Services, VPN, PKI |
| Security Platforms | SIEM, IDS / IPS |

---

# Common Default Ports

| Service | Port |
|----------|------|
| HTTP | 80 |
| HTTPS | 443 |
| SSH | 22 |
| FTP | 21 |
| FTPS | 990 / 21 |
| SFTP | 22 |
| SMB | 445 |
| DNS | 53 |
| DHCP | 67 / 68 |
| LDAP | 389 |
| LDAPS | 636 |
| Kerberos | 88 |
| SMTP | 25 |
| POP3 | 110 |
| IMAP | 143 |
| RDP | 3389 |
| VNC | 5900 |
| Telnet | 23 |
| SIP | 5060 / 5061 |
| RTP | Dynamic |
| MySQL | 3306 |
| PostgreSQL | 5432 |
| Microsoft SQL Server | 1433 |
| Oracle Database | 1521 |
| MongoDB | 27017 |
| Redis | 6379 |
| Elasticsearch | 9200 |
| Docker API | 2375 / 2376 |
| Kubernetes API | 6443 |
| WinRM | 5985 / 5986 |
| RPC | 135 |
| NFS | 2049 |
| rsync | 873 |
| MQTT | 1883 / 8883 |
| AMQP | 5672 / 5671 |
| Kafka | 9092 |
| Git | 9418 |

---

# Service Recognition Workflow

```text
Host Discovery

      │

      ▼

Port Scan

      │

      ▼

Service Detection

(-sV)

      │

      ▼

Version Detection

      │

      ▼

Banner Grabbing

      │

      ▼

NSE Enumeration

      │

      ▼

Service Fingerprinting

      │

      ▼

Attack Surface Analysis
```

---

# Recommended Nmap Commands

Basic Scan

```bash
nmap target
```

Service Detection

```bash
nmap -sV target
```

Default Scripts

```bash
nmap -sC -sV target
```

Aggressive Scan

```bash
nmap -A target
```

Operating System Detection

```bash
nmap -O target
```

UDP Scan

```bash
nmap -sU target
```

Selected Ports

```bash
nmap -p22,80,443 target
```

All Ports

```bash
nmap -p- target
```

---

# Useful NSE Categories

| Category | Purpose |
|----------|----------|
| default | Safe default scripts |
| auth | Authentication checks |
| brute | Brute-force testing |
| discovery | Information gathering |
| vuln | Vulnerability detection |
| version | Version identification |
| malware | Malware detection |
| safe | Low-risk enumeration |
| intrusive | Aggressive testing |

---

# Common Enumeration Scripts

| Service | Example NSE Script |
|----------|-------------------|
| HTTP | http-title |
| HTTPS | ssl-cert |
| SSH | ssh-hostkey |
| FTP | ftp-anon |
| SMB | smb-os-discovery |
| DNS | dns-recursion |
| LDAP | ldap-rootdse |
| SMTP | smtp-enum-users |
| MySQL | mysql-info |
| MSSQL | ms-sql-info |
| MongoDB | mongodb-info |
| Redis | redis-info |
| Elasticsearch | http-title |
| Kubernetes | http-title |

---

# Blue Team Checklist

Before exposing a service to production:

- Keep software updated.
- Disable unnecessary services.
- Remove default credentials.
- Enable encryption where available.
- Restrict administrative interfaces.
- Apply least-privilege access controls.
- Enable logging and auditing.
- Monitor authentication attempts.
- Regularly review firewall rules.
- Perform vulnerability assessments.
- Conduct periodic penetration testing.
- Back up critical configurations.

---

# Red Team Checklist

During reconnaissance:

- Identify open ports.
- Detect service versions.
- Collect banners.
- Enumerate available endpoints.
- Identify authentication methods.
- Search for anonymous access.
- Check for default credentials.
- Inspect TLS configurations.
- Run appropriate NSE scripts.
- Search for known CVEs.
- Identify exposed management interfaces.
- Document attack paths.

---

# Best Practices

- Never rely solely on default ports for service identification.
- Always perform version detection.
- Combine multiple NSE scripts for deeper enumeration.
- Verify banners with additional fingerprinting techniques.
- Correlate service information with operating system detection.
- Document every discovered service.
- Validate findings manually when necessary.
- Continuously update your knowledge of new technologies.

---

# Final Thoughts

Network services form the foundation of every modern IT infrastructure. Whether performing penetration testing, threat hunting, incident response, or system administration, understanding how these services operate is essential.

Nmap is more than a port scanner—it is a comprehensive reconnaissance framework. Its true strength comes from combining service detection, version identification, scripting, and protocol knowledge to build an accurate picture of a target environment.

The goal of this guide has been not only to explain individual services, but also to provide the context needed to recognize, analyze, and assess them effectively in real-world environments.

Continuous practice, hands-on labs, and staying current with evolving technologies will turn this reference into practical expertise.

---

# Congratulations

You have completed the **Common Network Services** reference.

You now have a comprehensive understanding of:

- Common enterprise network services
- Service architectures
- Default ports
- Authentication mechanisms
- Nmap detection techniques
- NSE script usage
- Enumeration methodologies
- Security risks
- Blue Team defenses
- Red Team reconnaissance strategies
- Enterprise best practices

This knowledge provides a strong foundation for advanced topics such as vulnerability assessment, penetration testing, Active Directory security, cloud security, and red team operations.