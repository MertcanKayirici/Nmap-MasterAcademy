# Top 100 Ports

> A quick reference guide to the 100 most commonly encountered TCP and UDP ports in networking, system administration, and penetration testing.

---

# Overview

Ports enable multiple network services to operate simultaneously on a single device. Every network application listens on one or more port numbers, allowing clients to communicate with the correct service.

Understanding common ports is essential for:

- Network Administration
- Penetration Testing
- Vulnerability Assessment
- Firewall Configuration
- Service Identification
- Incident Response

This reference provides a concise overview of the 100 most frequently encountered ports during network administration and security assessments.

---

# Port Number Ranges

| Range | Name | Description |
|-------:|------|-------------|
| 0–1023 | Well-Known Ports | Standard system and network services |
| 1024–49151 | Registered Ports | Vendor and application-specific services |
| 49152–65535 | Dynamic / Ephemeral Ports | Temporary client-side communication ports |

---

# Transport Protocols

Most network services use one of the following transport protocols.

| Protocol | Description |
|----------|-------------|
| TCP | Reliable, connection-oriented communication |
| UDP | Fast, connectionless communication |
| TCP/UDP | Some services support both protocols |

---

# Table Columns

Each entry contains:

- Port Number
- Protocol
- Default Service
- Description
- Common Software
- Security Notes

---

# Ports 1–20

| Port | Protocol | Service | Description | Common Software | Security Notes |
|------:|:-------:|----------|-------------|-----------------|----------------|
| 1 | TCP | TCPMUX | TCP Port Service Multiplexer | inetd | Rarely used. Disable if unnecessary. |
| 2 | TCP | CompressNET | Legacy Compression Service | Historical | Obsolete. Normally closed. |
| 3 | TCP | CompressNET | Legacy Compression Service | Historical | Rarely encountered today. |
| 4 | TCP | Reserved | Reserved Port | N/A | Usually closed. |
| 5 | TCP | RJE | Remote Job Entry | IBM Systems | Legacy enterprise environments only. |
| 7 | TCP/UDP | Echo | Echoes received data | inetd | Vulnerable to reflection attacks. |
| 9 | TCP/UDP | Discard | Discards received packets | inetd | Rarely enabled. |
| 11 | TCP | SYSTAT | Active User Information | BSD Systems | May leak system information. |
| 13 | TCP/UDP | Daytime | Returns system date and time | inetd | Can reveal system details. |
| 17 | TCP/UDP | Quote of the Day | Sends predefined text | inetd | Rarely used today. |
| 18 | TCP | Message Send Protocol | Legacy messaging service | Historical | Obsolete. |
| 19 | TCP/UDP | Chargen | Character Generator | inetd | Commonly abused in amplification attacks. |
| 20 | TCP | FTP Data | FTP data transfer channel | vsFTPd, ProFTPD, FileZilla Server | Prefer SFTP or FTPS. |

---

# Port Spotlight

## Port 7 — Echo

### Purpose

Returns exactly the same data sent by the client.

Example:

```text
Client
   │
   ▼
 Hello
   │
   ▼
Server
   │
   ▼
 Hello
```

### Security Notes

- Reflection attacks
- Amplification attacks
- Usually disabled on modern systems

---

## Port 19 — Chargen

### Purpose

Produces a continuous stream of characters.

Example:

```text
AAAAAAAAAAAAAAAAAAAAAA
BBBBBBBBBBBBBBBBBBBBBB
CCCCCCCCCCCCCCCCCCCCCC
```

### Security Notes

Chargen has historically been used in distributed denial-of-service (DDoS) amplification attacks and should normally remain disabled.

---

## Port 20 — FTP Data

FTP uses two separate channels.

```text
FTP Client
     │
     ├────────────► TCP 21
     │              Control Channel
     │
     └────────────► TCP 20
                    Data Channel
```

### Security Recommendations

- Use SFTP whenever possible.
- Prefer FTPS if FTP compatibility is required.
- Disable anonymous access.
- Use strong authentication.
- Restrict firewall exposure.

---

# Example Scan

```bash
nmap -p 1-20 192.168.1.10
```

Example Output

```text
PORT     STATE  SERVICE

7/tcp    closed echo

19/tcp   open   chargen

20/tcp   open   ftp-data
```

---

# Security Recommendations

Legacy services such as:

- Echo
- Chargen
- Daytime
- Discard

should generally remain disabled unless explicitly required by the environment.

FTP Data (Port 20) should only be used together with secure authentication and encrypted file transfer protocols.

---

# Summary

The first twenty ports are largely composed of historical Internet services and infrastructure protocols. While many of them are no longer common in modern enterprise environments, recognizing them during reconnaissance can reveal legacy systems, insecure configurations, or outdated network devices.

---

# Ports 21–40

| Port | Protocol | Service | Description | Common Software | Security Notes |
|------:|:-------:|----------|-------------|-----------------|----------------|
| 21 | TCP | FTP Control | FTP command and control channel | vsFTPd, ProFTPD, FileZilla Server | Use SFTP or FTPS whenever possible. Disable anonymous access. |
| 22 | TCP | SSH | Secure remote administration | OpenSSH, Dropbear | Use key-based authentication and disable password login when possible. |
| 23 | TCP | Telnet | Remote terminal access | telnetd | Unencrypted. Should not be used on production systems. |
| 25 | TCP | SMTP | Email transfer between mail servers | Postfix, Exim, Microsoft Exchange | Restrict open relays and enable TLS. |
| 37 | TCP/UDP | Time | Returns system time | inetd | Rarely used. Consider disabling if unnecessary. |
| 38 | TCP/UDP | RAP | Route Access Protocol | Historical | Obsolete in modern networks. |
| 39 | TCP/UDP | RLP | Resource Location Protocol | Historical | Rarely encountered. |
| 42 | TCP | WINS Replication | Windows Name Service Replication | Microsoft Windows | Restrict access to trusted hosts. |
| 43 | TCP | WHOIS | Domain registration lookup | WHOIS Server | Public information service. Limit exposure internally. |
| 49 | TCP | TACACS | Authentication service | Cisco TACACS | Replace with TACACS+ where possible. |
| 53 | TCP/UDP | DNS | Domain Name System | BIND, PowerDNS, Microsoft DNS | Prevent open recursion and enable DNSSEC where appropriate. |
| 67 | UDP | DHCP Server | Dynamic Host Configuration Protocol | ISC DHCP, Windows DHCP | Restrict rogue DHCP servers. |
| 68 | UDP | DHCP Client | DHCP Client Communication | Operating Systems | Normally used only by DHCP clients. |
| 69 | UDP | TFTP | Trivial File Transfer Protocol | tftpd-hpa | No authentication. Avoid on untrusted networks. |
| 70 | TCP | Gopher | Document retrieval protocol | Gopher Server | Mostly historical. Rarely used today. |
| 79 | TCP | Finger | User information service | fingerd | Can leak usernames and system information. |
| 80 | TCP | HTTP | Hypertext Transfer Protocol | Apache, Nginx, IIS, Caddy | Prefer HTTPS whenever possible. |
| 81 | TCP | Alternate HTTP | Alternative web service | Various Web Servers | Often used by administration panels. |
| 88 | TCP/UDP | Kerberos | Network Authentication | Microsoft Active Directory, MIT Kerberos | Critical infrastructure service. Protect carefully. |

---

# Port Spotlight

## Port 21 — FTP Control

### Purpose

FTP uses Port **21** for authentication and command exchange.

```text
Client

│

├────────► Port 21

│          Login

│          Commands

│

└────────► Port 20

           Data Transfer
```

### Common Commands

- USER
- PASS
- LIST
- RETR
- STOR
- QUIT

### Security Notes

FTP transmits credentials in plaintext.

Recommendations:

- Prefer SFTP
- Prefer FTPS
- Disable anonymous login
- Restrict access using firewalls

---

## Port 22 — SSH

SSH is the standard protocol for secure remote administration.

### Typical Uses

- Remote terminal
- File transfer (SCP)
- SFTP
- Port forwarding
- Remote automation

Common software:

- OpenSSH
- Dropbear

Example scan:

```bash
nmap -p22 192.168.1.10
```

Example result:

```text
22/tcp open ssh OpenSSH 9.3
```

Security Recommendations

- Disable root login.
- Use public key authentication.
- Disable password authentication where possible.
- Keep OpenSSH updated.

---

## Port 23 — Telnet

Telnet provides remote terminal access without encryption.

```text
Client

↓

Plaintext Network

↓

Server
```

Everything, including usernames and passwords, is transmitted in plaintext.

Modern systems should replace Telnet with SSH.

---

## Port 25 — SMTP

SMTP transfers email between mail servers.

```text
Mail Client

↓

Mail Server

↓

SMTP (25)

↓

Destination Server
```

Common Software

- Postfix
- Exim
- Sendmail
- Microsoft Exchange

Security Recommendations

- Enable STARTTLS
- Prevent Open Relay
- Configure SPF, DKIM, and DMARC

---

## Port 53 — DNS

DNS translates domain names into IP addresses.

```text
example.com

↓

DNS Query

↓

DNS Server

↓

93.184.216.34
```

Common Software

- BIND9
- PowerDNS
- Microsoft DNS

Security Recommendations

- Disable open recursion.
- Enable DNSSEC.
- Restrict zone transfers.

---

## Port 67 / 68 — DHCP

DHCP automatically assigns network settings.

```text
Client

↓

DHCP Discover

↓

Server

↓

Offer

↓

Request

↓

Acknowledgement
```

Security Recommendations

- Enable DHCP Snooping.
- Prevent rogue DHCP servers.
- Monitor lease assignments.

---

## Port 69 — TFTP

TFTP is a lightweight file transfer protocol.

Characteristics

- UDP-based
- No authentication
- No encryption
- Frequently used by network devices

Common Uses

- Router firmware
- PXE Boot
- Switch configuration
- Embedded devices

---

## Port 80 — HTTP

HTTP is the foundation of the World Wide Web.

Common Software

- Apache HTTP Server
- Nginx
- Microsoft IIS
- LiteSpeed
- Caddy

Example Scan

```bash
nmap -sV -p80 scanme.nmap.org
```

Typical Output

```text
80/tcp open http Apache httpd 2.4.x
```

Security Recommendations

- Redirect HTTP to HTTPS.
- Disable unnecessary methods.
- Hide version information.
- Configure security headers.

---

## Port 88 — Kerberos

Kerberos provides secure authentication in Active Directory environments.

```text
Client

↓

Authentication Server

↓

Ticket Granting Ticket

↓

Service Ticket

↓

Access Granted
```

Common Software

- Microsoft Active Directory
- MIT Kerberos
- Heimdal

Security Recommendations

- Synchronize system clocks.
- Protect domain controllers.
- Monitor failed authentication attempts.

---

# Common Nmap Examples

Detect common services:

```bash
nmap -sV -p21,22,23,25,53,80 target
```

Scan UDP infrastructure services:

```bash
nmap -sU -p53,67,68,69 target
```

Aggressive web enumeration:

```bash
nmap -A -p80 target
```

---

# Summary

Ports **21–40** introduce several of the most important Internet services, including FTP, SSH, Telnet, SMTP, DNS, DHCP, TFTP, HTTP, and Kerberos. These ports appear frequently during penetration tests, vulnerability assessments, and system administration tasks. Understanding their purpose, associated software, and security considerations is essential for accurate service identification and effective network defense.

---

# Ports 41–60

| Port | Protocol | Service | Description | Common Software | Security Notes |
|------:|:-------:|----------|-------------|-----------------|----------------|
| 41 | TCP | Graphics | Graphics Service | Legacy Systems | Rarely encountered today. |
| 42 | TCP | WINS Replication | Microsoft Name Replication | Windows Server | Restrict replication partners. |
| 43 | TCP | WHOIS | Domain Registration Lookup | WHOIS Server | Public information service. |
| 44 | TCP | MPM-FLAGS | Message Processing Module | Legacy | Rarely used. |
| 45 | TCP | Message Processing | Legacy Message Protocol | Historical | Obsolete. |
| 46 | TCP | MPM | Message Processing Module | Historical | Rarely seen. |
| 47 | TCP | NI FTP | Network Independent FTP | Historical | Obsolete. |
| 48 | TCP | AuditD | Audit Service | Legacy UNIX | Restrict access. |
| 49 | TCP | TACACS | Cisco Authentication | Cisco TACACS | Prefer TACACS+ for modern deployments. |
| 50 | TCP | Remote Mail Checking | Legacy Mail Service | Historical | Obsolete. |
| 51 | TCP | IMP Logical Address | Legacy ARPANET | Historical | Rarely encountered. |
| 52 | TCP | XNS Time | Xerox Network Systems | XNS | Legacy protocol. |
| 53 | TCP/UDP | DNS | Domain Name System | BIND, PowerDNS | Protect against open recursion. |
| 54 | TCP | XNS Clearinghouse | Xerox Network Systems | XNS | Historical. |
| 55 | TCP | ISI Graphics | Graphics Protocol | Historical | Rarely used. |
| 56 | TCP | XNS Authentication | Xerox Network Systems | XNS | Legacy authentication. |
| 57 | TCP | MTP | Mail Transfer Protocol | Legacy | Mostly obsolete. |
| 58 | TCP | XNS Mail | Xerox Mail Service | XNS | Rarely encountered. |
| 59 | TCP | NFILE | Network File Service | Legacy | Historical implementation. |
| 60 | TCP | Unassigned | Reserved | N/A | Normally closed. |

---

# Port Spotlight

## Port 42 — WINS Replication

Windows Internet Name Service (WINS) replication synchronizes NetBIOS name databases between WINS servers.

Typical Environment

```text
WINS Server A
       │
Replication
       │
       ▼
WINS Server B
```

Security Recommendations

- Limit replication to trusted servers.
- Disable WINS if Active Directory DNS completely replaces NetBIOS.
- Block unnecessary external access.

---

## Port 43 — WHOIS

WHOIS allows users to retrieve domain registration information.

Example

```text
whois example.com
```

Typical Information Returned

- Domain owner
- Registrar
- Registration dates
- Name servers
- Contact information (when available)

Security Considerations

WHOIS itself is not dangerous, but publicly available registration information can assist reconnaissance activities.

---

## Port 49 — TACACS

TACACS is commonly used for centralized authentication on network equipment.

Typical Devices

- Cisco Routers
- Cisco Switches
- Firewalls
- Network Appliances

Architecture

```text
Administrator

      │

      ▼

Network Device

      │

Authentication

      │

      ▼

TACACS Server
```

Benefits

- Centralized authentication
- Authorization
- Accounting (AAA)

Security Recommendations

- Prefer TACACS+ over the original TACACS protocol.
- Encrypt management traffic.
- Restrict access to management networks.

---

## Port 53 — DNS

DNS is one of the most critical Internet services.

Common Record Types

| Record | Purpose |
|---------|----------|
| A | IPv4 Address |
| AAAA | IPv6 Address |
| MX | Mail Server |
| NS | Name Server |
| TXT | Text Record |
| CNAME | Alias |
| PTR | Reverse Lookup |
| SOA | Zone Authority |

Example Query

```bash
dig example.com
```

Example Nmap Scan

```bash
nmap -sU -p53 target
```

DNS Enumeration Example

```bash
nmap --script dns-brute target.com
```

Security Recommendations

- Disable open recursion.
- Restrict zone transfers.
- Enable DNSSEC.
- Monitor DNS logs.

---

# Useful Nmap Commands

Service Detection

```bash
nmap -sV -p42,43,49,53 target
```

UDP DNS Scan

```bash
nmap -sU -p53 target
```

DNS NSE Scripts

```bash
nmap --script dns-recursion target
```

```bash
nmap --script dns-cache-snoop target
```

```bash
nmap --script dns-service-discovery target
```

---

# Recognition Tips

During penetration tests, seeing these ports often indicates:

| Port | Typical Environment |
|------:|---------------------|
| 42 | Older Windows networks |
| 43 | Public WHOIS service |
| 49 | Cisco infrastructure |
| 53 | Nearly every network |
| 57–59 | Legacy systems or historical services |

---

# Blue Team Perspective

When these ports are exposed:

- Verify whether the service is still required.
- Restrict management services to internal networks.
- Disable legacy protocols whenever possible.
- Apply firewall rules to minimize exposure.
- Monitor authentication and DNS logs.

---

# Red Team Perspective

These services can reveal valuable information during reconnaissance.

Examples:

- DNS → Host discovery
- WHOIS → Domain ownership
- TACACS → Network infrastructure
- WINS → Legacy Windows environments

Always verify service versions using:

```bash
nmap -sV target
```

---

# Summary

Ports **41–60** contain a mixture of historical protocols and several important infrastructure services, particularly **DNS (53)** and **TACACS (49)**. While many ports in this range are rarely encountered in modern environments, recognizing them can help identify legacy systems and specialized network equipment during security assessments.

---

# Ports 61–80

| Port | Protocol | Service | Description | Common Software | Security Notes |
|------:|:-------:|----------|-------------|-----------------|----------------|
| 61 | TCP | NI Mail | Legacy Mail Service | Historical | Rarely encountered. |
| 62 | TCP | ACA Services | ACA Management | Legacy | Obsolete. |
| 63 | TCP | WHOIS++ | Enhanced WHOIS | Historical | Rarely deployed. |
| 64 | TCP | Covia | Communications Service | Legacy | Historical protocol. |
| 65 | TCP | TACACS Database | Authentication Database | Legacy | Superseded by TACACS+. |
| 66 | TCP | Oracle SQL*NET | Oracle Database Communication | Oracle Database | Restrict access to trusted hosts. |
| 67 | UDP | DHCP Server | Dynamic Host Configuration Protocol | ISC DHCP, Windows DHCP | Prevent rogue DHCP servers. |
| 68 | UDP | DHCP Client | DHCP Client Communication | Operating Systems | Used by DHCP clients only. |
| 69 | UDP | TFTP | Trivial File Transfer Protocol | tftpd-hpa | No authentication or encryption. |
| 70 | TCP | Gopher | Document Retrieval Service | Gopher Server | Mostly obsolete. |
| 71 | TCP | NETRJS-1 | Remote Job Entry | Historical | Rarely used. |
| 72 | TCP | NETRJS-2 | Remote Job Entry | Historical | Rarely used. |
| 73 | TCP | NETRJS-3 | Remote Job Entry | Historical | Rarely used. |
| 74 | TCP | NETRJS-4 | Remote Job Entry | Historical | Rarely used. |
| 75 | TCP | Private Dial-out | Private Service | Various | Vendor specific. |
| 76 | TCP | Distributed External Object Store | DEOS | Legacy | Rarely encountered. |
| 77 | TCP | Private RJE | Remote Job Entry | Historical | Obsolete. |
| 78 | TCP | Vettcp | Legacy Protocol | Historical | Rarely used. |
| 79 | TCP | Finger | User Information Service | fingerd | Can expose usernames and login activity. |
| 80 | TCP | HTTP | Hypertext Transfer Protocol | Apache, Nginx, IIS, Caddy | Redirect users to HTTPS whenever possible. |

---

# Port Spotlight

## Port 66 — Oracle SQL*NET

Oracle SQL*NET allows client applications to communicate with Oracle Database servers.

Typical Environment

```text
Application

     │

SQL Query

     │

     ▼

Oracle Database
```

Typical Uses

- Enterprise databases
- ERP systems
- Financial applications

Security Recommendations

- Restrict network access.
- Enable encryption.
- Keep Oracle software updated.
- Monitor failed login attempts.

---

## Port 67 / 68 — DHCP

DHCP automatically assigns network configuration to devices.

Communication Flow

```text
Client

   │

Discover

   ▼

DHCP Server

   ▲

Offer

   │

Request

   ▼

Acknowledgement
```

Assigned Information

- IP Address
- Subnet Mask
- Default Gateway
- DNS Server
- Lease Time

Common Attacks

- Rogue DHCP
- DHCP Starvation
- Fake Gateway Assignment

Mitigation

- DHCP Snooping
- Port Security
- Trusted Switch Ports

---

## Port 69 — TFTP

TFTP is a lightweight file transfer protocol using UDP.

Characteristics

| Feature | Value |
|----------|-------|
| Transport | UDP |
| Authentication | None |
| Encryption | None |
| Reliability | Basic |

Typical Uses

- PXE Boot
- Router firmware
- Switch configuration
- Embedded devices
- Network appliance recovery

Example Scan

```bash
nmap -sU -p69 target
```

NSE Example

```bash
nmap --script tftp-enum target
```

Security Recommendations

- Never expose TFTP to the Internet.
- Restrict access using firewall rules.
- Replace with SCP or SFTP whenever possible.

---

## Port 79 — Finger

Finger provides information about users currently registered on a system.

Typical Output

```text
Login Name

Home Directory

Shell

Last Login

Idle Time
```

Security Risks

Finger can reveal:

- Valid usernames
- Login times
- Home directories
- User activity

This information greatly assists attackers during reconnaissance.

Recommendation

Disable the Finger service unless absolutely required.

---

## Port 80 — HTTP

HTTP is the most common application protocol on the Internet.

Typical Architecture

```text
Browser

     │

HTTP Request

     ▼

Web Server

     │

Response

     ▼

HTML

CSS

JavaScript
```

Common Software

- Apache HTTP Server
- Nginx
- Microsoft IIS
- LiteSpeed
- Caddy

Example Scan

```bash
nmap -sV -p80 target
```

Example Output

```text
80/tcp open http Apache httpd 2.4.62
```

Useful NSE Scripts

```bash
nmap --script http-title target
```

```bash
nmap --script http-enum target
```

```bash
nmap --script http-headers target
```

```bash
nmap --script http-methods target
```

```bash
nmap --script http-server-header target
```

Security Recommendations

- Redirect all traffic to HTTPS.
- Disable directory listing.
- Remove unnecessary HTTP methods.
- Hide server version information.
- Configure security headers.
- Keep web server software updated.

---

# Recognition Tips

During reconnaissance:

| Port | Usually Indicates |
|------:|-------------------|
| 66 | Oracle Database |
| 67 | DHCP Server |
| 68 | DHCP Client |
| 69 | TFTP Service |
| 79 | Finger Service |
| 80 | Web Server |

---

# Blue Team Perspective

Recommended actions:

- Remove unused legacy services.
- Disable Finger.
- Never expose TFTP publicly.
- Restrict DHCP administration.
- Harden web servers.
- Continuously monitor HTTP logs.

---

# Red Team Perspective

These ports often provide valuable information.

Examples

Port 80

- Web enumeration
- Directory discovery
- Technology fingerprinting
- CMS identification
- Virtual host discovery

Port 69

- Configuration backup download
- Firmware extraction

Port 79

- Username enumeration

Useful Commands

```bash
nmap -A -p80 target
```

```bash
nmap --script vuln -p80 target
```

```bash
nmap --script http-enum target
```

---

# Summary

Ports **61–80** include several legacy services alongside some of today's most recognizable infrastructure protocols. In particular, **DHCP (67/68)**, **TFTP (69)**, and **HTTP (80)** are encountered frequently in enterprise environments and penetration tests. Understanding their purpose, associated software, and common security risks is essential for accurate service identification and effective network defense.

---

# Ports 81–100

| Port | Protocol | Service | Description | Common Software | Security Notes |
|------:|:-------:|----------|-------------|-----------------|----------------|
| 81 | TCP | Alternate HTTP | Alternative HTTP Service | Apache, Nginx | Often used for admin panels. Restrict access. |
| 82 | TCP | Alternate HTTP | Alternative Web Service | Various | Vendor-specific web interfaces. |
| 83 | TCP | MIT ML Device | MIT ML Device Service | Legacy | Rarely encountered. |
| 84 | TCP | Common Trace Facility | IBM Systems | IBM | Enterprise environments only. |
| 85 | TCP | MIT ML Device | Legacy Service | Historical | Rarely used. |
| 86 | TCP | Micro Focus COBOL | COBOL Runtime | Micro Focus | Enterprise legacy applications. |
| 87 | TCP | Priv-Terminal | Private Terminal Service | Vendor Specific | Internal use only. |
| 88 | TCP/UDP | Kerberos | Authentication Service | Active Directory, MIT Kerberos | Critical authentication infrastructure. |
| 89 | TCP | SU/MIT Telnet Gateway | Gateway Service | Historical | Obsolete. |
| 90 | TCP | DNSIX | DNSIX Security Protocol | Historical | Rarely deployed. |
| 91 | TCP | MIT Dover Spooler | Printing Service | Legacy | Historical service. |
| 92 | TCP | Network Printing | Printing Service | Legacy | Restrict printer exposure. |
| 93 | TCP | Device Control | Device Management | Vendor Specific | Internal management only. |
| 94 | TCP | Tivoli Object Dispatcher | IBM Tivoli | IBM Tivoli | Restrict management access. |
| 95 | TCP | SUPDUP | Remote Terminal Protocol | Historical | Obsolete. |
| 96 | TCP | DIXIE | Directory Service | Historical | Rarely encountered. |
| 97 | TCP | Swift Remote Virtual File Protocol | Banking Systems | SWIFT | Critical financial infrastructure. |
| 98 | TCP | LinuxConf | Linux Configuration Service | LinuxConf | Deprecated administration service. |
| 99 | TCP | Metagram Relay | Legacy Service | Historical | Rarely used. |
| 100 | TCP | Newacct | Process Accounting | UNIX Systems | Monitor accounting information carefully. |

---

# Port Spotlight

## Port 81 — Alternate HTTP

Port 81 is commonly used as an alternative web service port.

Typical Uses

- Web administration panels
- Router configuration pages
- Internal dashboards
- Development environments

Example

```text
http://192.168.1.1:81
```

Example Scan

```bash
nmap -sV -p81 target
```

Security Recommendations

- Require authentication.
- Restrict administrative access.
- Enable HTTPS when supported.
- Avoid exposing management interfaces to the Internet.

---

## Port 88 — Kerberos

Kerberos is the primary authentication protocol used by Microsoft Active Directory.

Authentication Flow

```text
User

 │

 ▼

Authentication Server (AS)

 │

 ▼

Ticket Granting Ticket (TGT)

 │

 ▼

Ticket Granting Server (TGS)

 │

 ▼

Service Ticket

 │

 ▼

Application Server
```

Typical Environment

- Active Directory
- Windows Domain
- Enterprise Networks
- Single Sign-On (SSO)

Common Attacks

- Kerberoasting
- AS-REP Roasting
- Pass-the-Ticket
- Golden Ticket
- Silver Ticket

Useful Nmap Scripts

```bash
nmap --script krb5-enum-users target
```

Security Recommendations

- Use strong service account passwords.
- Enable modern encryption types.
- Synchronize system time.
- Monitor authentication failures.
- Protect Domain Controllers.

---

## Port 97 — SWIFT

Port 97 has historically been associated with SWIFT communication.

Typical Environment

```text
Bank A

     │

Secure Financial Network

     │

Bank B
```

Used By

- Financial institutions
- Banking infrastructure
- International payment systems

Security Importance

Financial communication systems require:

- Strong authentication
- Encryption
- Continuous monitoring
- Network segmentation

---

## Port 100 — Process Accounting

Port 100 has historically been associated with UNIX process accounting.

Purpose

Allows systems to maintain records of:

- Executed commands
- CPU usage
- User activity
- Resource consumption

Typical Environment

- UNIX
- Linux
- Legacy enterprise systems

Security Considerations

Accounting logs may contain:

- Sensitive usernames
- Process information
- System activity

Restrict access appropriately.

---

# Recognition Tips

Common observations during assessments:

| Port | Usually Indicates |
|------:|-------------------|
| 81 | Secondary Web Interface |
| 88 | Active Directory / Kerberos |
| 97 | Banking Infrastructure |
| 100 | UNIX Accounting Service |

---

# Blue Team Perspective

Recommendations

- Secure administrative web interfaces.
- Harden Active Directory.
- Monitor Kerberos events.
- Restrict management ports.
- Audit authentication logs.
- Segment sensitive infrastructure.

---

# Red Team Perspective

Interesting targets

### Port 81

Possible Findings

- Hidden administration panels
- Development websites
- Backup portals
- Monitoring dashboards

Useful Commands

```bash
nmap -sV -p81 target
```

```bash
nmap --script http-title target -p81
```

```bash
nmap --script http-enum target -p81
```

---

### Port 88

Enumeration

```bash
nmap -sV -p88 target
```

```bash
nmap --script krb5-enum-users target
```

Possible Findings

- Domain Controller
- Active Directory
- Kerberos Authentication
- Enterprise Infrastructure

---

# Security Checklist

When encountering any service within the first 100 ports:

✓ Verify the service is required.

✓ Confirm software is fully updated.

✓ Restrict unnecessary public exposure.

✓ Use encryption whenever supported.

✓ Disable obsolete protocols.

✓ Monitor authentication events.

✓ Apply least privilege.

✓ Review firewall rules regularly.

---

# Common Nmap Commands

Scan Top 100 Ports

```bash
nmap --top-ports 100 target
```

Service Detection

```bash
nmap -sV --top-ports 100 target
```

Aggressive Detection

```bash
nmap -A --top-ports 100 target
```

TCP SYN Scan

```bash
nmap -sS --top-ports 100 target
```

UDP Top Ports

```bash
nmap -sU --top-ports 100 target
```

Default Script Scan

```bash
nmap -sC --top-ports 100 target
```

Version Detection

```bash
nmap -sV --version-all target
```

---

# Final Notes

The first 100 ports contain many of the Internet's oldest and most widely recognized services. During penetration testing and network administration, these ports often reveal critical infrastructure such as web servers, DNS servers, mail systems, authentication services, file transfer services, and legacy protocols.

Although many ports in this range are now obsolete, recognizing them remains valuable for identifying outdated systems, legacy applications, and potential security weaknesses.

---

# Chapter Summary

In this reference, you learned:

- The structure of well-known ports
- Common TCP and UDP services
- Typical software implementations
- Security considerations for each service
- Frequently encountered infrastructure protocols
- Common Nmap scanning techniques
- Blue Team and Red Team perspectives
- Practical reconnaissance tips

This chapter serves as a quick-reference guide during penetration testing, system administration, and network troubleshooting.

---

# Next Reference

## 02_Top_1000_Ports.md