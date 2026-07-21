# Top 1000 Ports

> A comprehensive reference of the most commonly scanned TCP and UDP ports used in networking, system administration, and penetration testing.

---

# Overview

The first 100 ports cover many of the Internet's oldest and most recognizable services. However, modern enterprise environments rely on hundreds of additional ports for databases, virtualization, cloud platforms, monitoring, remote management, containers, messaging systems, and enterprise applications.

This document extends the reference to the top 1000 ports most frequently encountered during security assessments.

---

# Port Categories

| Category | Description |
|----------|-------------|
| Well-Known | Ports 0–1023 |
| Registered | Ports 1024–49151 |
| Dynamic | Ports 49152–65535 |

---

# Reading This Reference

Each entry includes:

- Port Number
- Protocol
- Service
- Description
- Common Software
- Typical Usage
- Security Notes

---

# Ports 101–120

| Port | Protocol | Service | Description | Common Software | Security Notes |
|------:|:-------:|----------|-------------|-----------------|----------------|
| 101 | TCP | HOSTNAME | NIC Host Name Service | Legacy UNIX | Rarely used today. |
| 102 | TCP | ISO-TSAP | ISO Transport Service Access Point | Siemens, SAP | Often appears in industrial environments. |
| 103 | TCP | Genesis Point-to-Point | Legacy Service | Historical | Usually closed. |
| 104 | TCP | DICOM | Medical Imaging Communication | PACS, Radiology Systems | Restrict access. Contains sensitive medical data. |
| 105 | TCP | CCSO Nameserver | Directory Service | Legacy | Rarely encountered. |
| 106 | TCP | POP3 Password Change | Mail Service | Historical | Obsolete. |
| 107 | TCP | Remote TELNET Service | Remote Administration | Legacy | Replace with SSH. |
| 108 | TCP | SNAGAS | Historical Service | Legacy | Rarely used. |
| 109 | TCP | POP2 | Post Office Protocol v2 | Legacy Mail Servers | Deprecated. |
| 110 | TCP | POP3 | Email Retrieval | Dovecot, Courier, Exchange | Prefer POP3S (995). |
| 111 | TCP/UDP | RPCbind | RPC Port Mapper | rpcbind | Frequently targeted during enumeration. |
| 112 | TCP | MCS | McIDAS Service | Legacy | Rarely used. |
| 113 | TCP | Ident | Identification Protocol | identd | Information disclosure risk. |
| 115 | TCP | SFTP | Simple File Transfer Protocol (RFC 913) | Legacy | Not SSH File Transfer Protocol. Rarely used. |
| 117 | TCP | UUCP Path | UNIX Copy Protocol | UNIX | Historical. |
| 118 | TCP | SQL Services | SQL Service | Various | Vendor-specific. |
| 119 | TCP | NNTP | Network News Transfer Protocol | INN | Restrict public exposure. |
| 120 | TCP | CFDPTKT | CFDPTKT Service | Historical | Rarely encountered. |

---

# Port Spotlight

## Port 104 — DICOM

DICOM is the standard protocol used to transfer medical imaging data.

Typical Environment

```text
MRI Scanner

      │

      ▼

PACS Server

      │

      ▼

Radiology Workstation
```

Common Uses

- MRI
- CT
- X-Ray
- Ultrasound
- PACS

Security Notes

- Contains highly sensitive medical information.
- Should never be exposed to the public Internet.
- Enforce encryption and strict access controls.

---

## Port 110 — POP3

POP3 retrieves email messages from a mail server.

```text
Mail Client

      │

Retrieve Messages

      ▼

Mail Server
```

Common Software

- Dovecot
- Microsoft Exchange
- Courier

Security Recommendations

- Prefer POP3S (995).
- Require TLS.
- Disable plaintext authentication.

---

## Port 111 — RPCbind

RPCbind maps Remote Procedure Call services to dynamic ports.

```text
Client

    │

RPC Request

    ▼

RPCbind (111)

    │

Returns Dynamic Port

    ▼

RPC Service
```

Typical Services

- NFS
- NIS
- Mountd
- Statusd

Example Scan

```bash
nmap -sV -p111 target
```

Useful NSE Scripts

```bash
nmap --script rpcinfo target
```

Security Recommendations

- Restrict access to trusted networks.
- Disable unused RPC services.
- Monitor RPC traffic.

---

## Port 113 — Ident

Ident provides information about the user associated with a TCP connection.

Security Risk

The service may reveal:

- Usernames
- Local account names
- Running services

Recommendation

Disable unless explicitly required.

---

# Common Nmap Commands

Scan Ports 101–120

```bash
nmap -p101-120 target
```

Version Detection

```bash
nmap -sV -p104,110,111 target
```

UDP RPC Scan

```bash
nmap -sU -p111 target
```

---

# Summary

Ports **101–120** introduce enterprise services, medical imaging protocols, legacy email systems, and RPC infrastructure. While several ports in this range are historical, ports such as **104 (DICOM)**, **110 (POP3)**, and **111 (RPCbind)** remain highly relevant in real-world enterprise environments and penetration testing.

---

# Ports 121–140

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 121 | TCP | ERPC | Encore RPC | Encore Systems | Legacy RPC | Rarely encountered. |
| 122 | TCP | SMAKYNET | Smaky Network | Smaky OS | Legacy networking | Historical service. |
| 123 | UDP | NTP | Network Time Protocol | Chrony, ntpd, Windows Time | Time synchronization | Prevent public abuse and monitor time servers. |
| 124 | TCP | ANSATRADER | Financial Trading | Financial Platforms | Trading systems | Restrict access. |
| 125 | TCP | Locus MAP | Locus Mapping | Legacy Systems | Legacy communication | Rarely used. |
| 126 | TCP | Unitary Login | Authentication | Legacy UNIX | Authentication | Obsolete. |
| 127 | TCP | Locus Concorde | Legacy Service | Historical | Legacy | Rarely encountered. |
| 128 | TCP | GSS-XLICEN | License Manager | Various Vendors | Software licensing | Restrict internal access. |
| 129 | TCP | Password Generator | Password Service | Historical | Legacy | Disable if enabled. |
| 130 | TCP | Cisco FNA | Cisco Network Service | Cisco | Network management | Restrict management traffic. |
| 131 | TCP | Cisco TNP | Cisco Network Protocol | Cisco | Device communication | Internal use only. |
| 132 | TCP | Cisco SYS | Cisco System Service | Cisco | Infrastructure | Restrict access. |
| 133 | TCP | Statistics Service | System Statistics | Various | Monitoring | Can reveal host information. |
| 134 | TCP | INGRES-NET | Database Networking | Ingres DB | Database access | Limit exposure. |
| 135 | TCP | MSRPC | Microsoft RPC Endpoint Mapper | Windows | Remote Procedure Calls | High-value target during enumeration. |
| 136 | TCP | Profile Naming | Naming Service | Legacy | Historical | Rarely used. |
| 137 | UDP | NetBIOS Name Service | NetBIOS Name Resolution | Windows | Name resolution | Information disclosure risk. |
| 138 | UDP | NetBIOS Datagram Service | NetBIOS Messaging | Windows | File and printer sharing | Restrict to internal networks. |
| 139 | TCP | NetBIOS Session Service | SMB over NetBIOS | Windows | File sharing | Disable if SMBv2/v3 is available. |
| 140 | TCP | EMFIS Data Service | Enterprise Service | Legacy | Historical | Rarely encountered. |

---

# Port Spotlight

## Port 123 — NTP

Network Time Protocol synchronizes clocks across networked systems.

Accurate system time is essential for:

- Kerberos Authentication
- TLS Certificates
- Log Correlation
- SIEM Platforms
- Active Directory
- Distributed Systems

Architecture

```text
Client

   │

Time Request

   ▼

NTP Server

   │

Time Response

   ▼

Client Clock Updated
```

Common Software

- Chrony
- ntpd
- systemd-timesyncd
- Windows Time Service

Example Scan

```bash
nmap -sU -p123 target
```

Useful NSE Script

```bash
nmap --script ntp-info target
```

Security Recommendations

- Restrict public NTP queries.
- Disable legacy monlist functionality.
- Synchronize all critical infrastructure.
- Monitor unexpected time drift.

---

## Port 135 — MSRPC

Microsoft RPC Endpoint Mapper is one of the most important Windows services.

Purpose

It maps RPC clients to dynamically assigned service ports.

Typical Environment

```text
Client

    │

RPC Request

    ▼

Endpoint Mapper (135)

    │

Returns Dynamic Port

    ▼

RPC Service
```

Common Services Using RPC

- Active Directory
- DCOM
- WMI
- Windows Management
- Print Spooler

Example Scan

```bash
nmap -sV -p135 target
```

Useful NSE Scripts

```bash
nmap --script msrpc-enum target
```

```bash
nmap --script smb-os-discovery target
```

Security Recommendations

- Restrict external access.
- Disable unnecessary RPC services.
- Keep Windows systems fully patched.
- Monitor RPC-related authentication failures.

---

## Port 137 — NetBIOS Name Service

NetBIOS Name Service resolves Windows computer names.

Typical Usage

- Workgroup environments
- Legacy Windows networks
- SMB discovery

Example

```text
PC01

↓

NetBIOS Query

↓

192.168.1.25
```

Useful NSE Script

```bash
nmap --script nbstat target
```

Information Revealed

- Computer Name
- Logged-in User
- MAC Address
- NetBIOS Name Table

Security Recommendations

Disable NetBIOS where Active Directory DNS provides all required functionality.

---

## Port 138 — NetBIOS Datagram Service

Provides connectionless communication between Windows systems.

Common Uses

- Browser announcements
- Network browsing
- Legacy Windows messaging

Security Recommendation

Restrict to trusted internal networks only.

---

## Port 139 — NetBIOS Session Service

Historically used for SMB file sharing.

Architecture

```text
Client

    │

SMB Session

    ▼

TCP 139

    ▼

Windows Server
```

Typical Services

- File Sharing
- Printer Sharing
- Remote Administration

Common Software

- Microsoft Windows
- Samba

Example Scan

```bash
nmap -sV -p139 target
```

Useful NSE Scripts

```bash
nmap --script smb-enum-shares target
```

```bash
nmap --script smb-enum-users target
```

```bash
nmap --script smb-protocols target
```

Security Recommendations

- Prefer SMB over TCP 445.
- Disable SMBv1.
- Restrict anonymous access.
- Enable SMB signing where appropriate.
- Monitor file sharing activity.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 123 | NTP Server |
| 135 | Windows Host |
| 137 | NetBIOS Name Service |
| 138 | NetBIOS Datagram |
| 139 | SMB over NetBIOS |

---

# Blue Team Perspective

Recommended Actions

- Synchronize time using trusted NTP servers.
- Harden Microsoft RPC services.
- Disable NetBIOS where unnecessary.
- Monitor SMB authentication.
- Block unnecessary inbound RPC traffic.
- Audit Windows administrative shares.

---

# Red Team Perspective

Interesting Targets

### Port 123

Possible Findings

- Time synchronization source
- Domain infrastructure
- Time-based attack opportunities

### Ports 135–139

Often indicate:

- Windows Servers
- Active Directory
- SMB Services
- File Shares
- Domain Infrastructure

Common Enumeration Commands

```bash
nmap -A -p135,137,138,139 target
```

```bash
nmap --script smb-enum-shares target
```

```bash
nmap --script smb-os-discovery target
```

```bash
nmap --script smb-security-mode target
```

---

# Summary

Ports **121–140** introduce several important enterprise services, including **NTP (123)**, **MSRPC (135)**, and the **NetBIOS suite (137–139)**. These ports are frequently encountered in Windows environments and often provide valuable information during both system administration and penetration testing. Proper hardening, access control, and continuous monitoring are essential to reduce the attack surface associated with these services.

---

# Ports 141–160

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 141 | TCP | EMFIS Control | EMFIS Control Service | Legacy | Enterprise Systems | Rarely encountered. |
| 142 | TCP | EMFIS Data | EMFIS Data Channel | Legacy | Enterprise Systems | Historical protocol. |
| 143 | TCP | IMAP | Internet Message Access Protocol | Dovecot, Courier, Exchange | Email Retrieval | Prefer IMAPS (993). |
| 144 | TCP | NewS | News Distribution | Legacy | Historical | Rarely used. |
| 145 | TCP | UAAC | Unassigned/Legacy | Historical | Legacy | Normally closed. |
| 146 | TCP | ISO-TP0 | ISO Transport | Industrial Systems | Industrial Networks | Restrict access. |
| 147 | TCP | ISO-IP | ISO Internet Protocol | Legacy | Enterprise | Rarely encountered. |
| 148 | TCP | Jargon | Historical Service | Legacy | Historical | Obsolete. |
| 149 | TCP | AED-512 | Application Service | Vendor Specific | Enterprise | Restrict access. |
| 150 | TCP | SQL-NET | SQL Network | Oracle | Database Communication | Limit database exposure. |
| 151 | TCP | HEMS | Health Enterprise Messaging | Healthcare | Medical Systems | Sensitive data. |
| 152 | TCP | Background File Transfer | File Service | Various | Internal Transfers | Restrict access. |
| 153 | TCP | SGMP | Simple Gateway Monitoring Protocol | Legacy | Monitoring | Superseded by SNMP. |
| 154 | TCP | NETSC | Network Service | Legacy | Enterprise | Historical. |
| 155 | TCP | NETSC-2 | Network Service | Legacy | Enterprise | Rarely used. |
| 156 | TCP | SQL Service | Database Service | Various | Database Access | Restrict externally. |
| 157 | TCP | KNET/VM Command | IBM VM | IBM Systems | Management | Internal use only. |
| 158 | TCP | PCMail | Mail Service | Legacy | Messaging | Historical. |
| 159 | TCP | NSS Routing | Network Routing | Legacy | Routing | Rarely encountered. |
| 160 | TCP | SGMP Traps | Monitoring Notifications | Legacy | Monitoring | Replaced by SNMP Traps. |

---

# Port Spotlight

## Port 143 — IMAP

Internet Message Access Protocol (IMAP) allows users to access and manage email directly on the mail server.

Unlike POP3, messages remain on the server unless explicitly deleted.

Typical Workflow

```text
Mail Client

      │

IMAP Commands

      ▼

Mail Server

      │

Folders

Inbox

Drafts

Sent

Trash
```

Common Software

- Dovecot
- Microsoft Exchange
- Cyrus IMAP
- Courier IMAP

Typical Features

- Folder synchronization
- Multi-device access
- Server-side message storage
- Read/unread status synchronization

Example Scan

```bash
nmap -sV -p143 target
```

Example Output

```text
143/tcp open imap Dovecot imapd
```

Useful NSE Scripts

```bash
nmap --script imap-capabilities target
```

```bash
nmap --script imap-ntlm-info target
```

Security Recommendations

- Prefer IMAPS (Port 993).
- Disable plaintext authentication.
- Require TLS encryption.
- Enable MFA where supported.
- Monitor authentication attempts.

---

## Port 150 — SQL-NET

SQL*NET enables Oracle clients to communicate with Oracle Database servers.

Typical Architecture

```text
Application

      │

SQL Query

      ▼

Oracle Listener

      │

Oracle Database
```

Common Uses

- ERP Applications
- Financial Systems
- Enterprise Databases
- Data Warehouses

Security Recommendations

- Restrict access using firewalls.
- Require encrypted connections.
- Disable unused listeners.
- Monitor failed login attempts.

---

## Port 151 — Healthcare Messaging

Port 151 has historically been associated with healthcare messaging systems.

Typical Environment

```text
Hospital Information System

        │

Patient Data

        ▼

Clinical Server
```

Possible Data

- Patient Records
- Medical History
- Laboratory Results
- Clinical Reports

Security Recommendations

- Encrypt all communications.
- Restrict access to authorized personnel.
- Log all access events.
- Follow healthcare compliance requirements.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 143 | IMAP Mail Server |
| 150 | Oracle Database |
| 151 | Healthcare Infrastructure |
| 156 | SQL Service |
| 160 | Legacy Monitoring |

---

# Blue Team Perspective

Recommendations

- Use IMAPS instead of IMAP.
- Restrict database listeners.
- Encrypt database traffic.
- Monitor email authentication logs.
- Audit access to healthcare systems.
- Remove obsolete services.

---

# Red Team Perspective

Interesting Targets

### Port 143

Possible Findings

- Email Server
- User Enumeration
- Authentication Methods
- Mail Capabilities

Useful Commands

```bash
nmap --script imap-capabilities target
```

```bash
nmap --script imap-ntlm-info target
```

### Port 150

Possible Findings

- Oracle Database
- Enterprise Applications
- Database Listener

Enumeration

```bash
nmap -sV -p150 target
```

---

# Common Nmap Commands

Scan Ports

```bash
nmap -p141-160 target
```

Service Detection

```bash
nmap -sV -p143,150,151 target
```

Default Scripts

```bash
nmap -sC -p143 target
```

Aggressive Scan

```bash
nmap -A -p143,150 target
```

---

# Summary

Ports **141–160** introduce enterprise messaging, database communication, and legacy monitoring services. Among them, **IMAP (143)** remains one of the most widely deployed email protocols, while Oracle SQL networking services are common in enterprise environments. Proper encryption, access control, and continuous monitoring are essential to securing these services.

---

# Ports 161–180

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 161 | UDP | SNMP | Simple Network Management Protocol | Net-SNMP, Cisco IOS | Network Monitoring | Disable default community strings. |
| 162 | UDP | SNMP Trap | SNMP Event Notifications | Net-SNMP | Network Alerts | Accept traps only from trusted devices. |
| 163 | TCP | CMIP | Common Management Information Protocol | Enterprise Systems | Network Management | Rarely deployed today. |
| 164 | TCP | CMIP Agent | CMIP Management Agent | Enterprise Systems | Management | Mostly replaced by SNMP. |
| 165 | TCP | Xerox Service | Xerox Network Service | Xerox Systems | Legacy | Historical protocol. |
| 166 | TCP | SRI Terminal | Stanford Research Terminal | Historical | Legacy | Rarely encountered. |
| 167 | TCP | NAMP | Network Administration | Vendor Specific | Internal Management | Restrict internal access. |
| 168 | TCP | RSVD | Reserved Service | N/A | Reserved | Normally closed. |
| 169 | TCP | SEND | Secure Electronic Network | Legacy | Historical | Rarely used. |
| 170 | TCP | Print Service | Legacy Printing | UNIX | Printing | Restrict access. |
| 171 | TCP | Multiplex | Legacy Multiplexer | Historical | Legacy | Obsolete. |
| 172 | TCP | CL/1 | Network Protocol | Historical | Legacy | Rarely encountered. |
| 173 | TCP | XYPLEX | Terminal Server | Xyplex | Remote Access | Restrict administrative access. |
| 174 | TCP | MAILQ | Mail Queue Service | UNIX Mail | Queue Management | Internal use only. |
| 175 | TCP | VMNET | IBM VM Networking | IBM Systems | Enterprise | Historical deployment. |
| 176 | TCP | GENRAD-MUX | Multiplexer | Legacy | Industrial | Rarely used. |
| 177 | UDP | XDMCP | X Display Manager Control Protocol | X.Org | Linux Remote Login | Disable if unnecessary. |
| 178 | TCP | NextStep | NeXTSTEP Service | NeXT Systems | Historical | Rarely encountered. |
| 179 | TCP | BGP | Border Gateway Protocol | FRRouting, Cisco IOS, Juniper JunOS | Internet Routing | Restrict BGP peers and enable authentication. |
| 180 | TCP | RIS | Remote Installation Service | Legacy | Deployment | Historical implementation. |

---

# Port Spotlight

## Port 161 — SNMP

Simple Network Management Protocol (SNMP) is one of the most widely used protocols for monitoring and managing network devices.

Common Devices

- Routers
- Switches
- Firewalls
- Printers
- UPS Systems
- Wireless Controllers
- IP Cameras

Typical Architecture

```text
Monitoring Server

        │

SNMP Query

        ▼

Network Device

        │

Response

        ▼

CPU

Memory

Interfaces

Temperature

Traffic
```

Common Versions

| Version | Security |
|----------|----------|
| SNMPv1 | Insecure |
| SNMPv2c | Community String Authentication |
| SNMPv3 | Authentication + Encryption |

Example Scan

```bash
nmap -sU -p161 target
```

Useful NSE Scripts

```bash
nmap --script snmp-info target
```

```bash
nmap --script snmp-interfaces target
```

```bash
nmap --script snmp-processes target
```

```bash
nmap --script snmp-sysdescr target
```

Security Recommendations

- Prefer SNMPv3.
- Disable default community strings such as "public" and "private".
- Restrict SNMP access using ACLs.
- Monitor unauthorized SNMP requests.

---

## Port 162 — SNMP Trap

SNMP Trap allows network devices to send alerts without waiting for polling.

Typical Workflow

```text
Switch

    │

Interface Down

    ▼

SNMP Trap

    ▼

Monitoring Server

    │

Alert Generated
```

Common Events

- Interface Failure
- CPU Overload
- Fan Failure
- Power Supply Failure
- Temperature Alarm

Security Recommendations

- Accept traps only from trusted devices.
- Authenticate SNMPv3 trap senders.
- Log all received events.

---

## Port 177 — XDMCP

X Display Manager Control Protocol allows graphical remote login on UNIX/Linux systems.

Typical Environment

```text
Linux Workstation

        │

XDMCP Request

        ▼

Display Manager

        │

Remote Desktop
```

Common Software

- XDM
- GDM
- LightDM

Security Recommendations

- Disable XDMCP unless required.
- Use SSH with X11 Forwarding instead.
- Restrict access to trusted networks.

---

## Port 179 — BGP

Border Gateway Protocol (BGP) is the routing protocol that connects autonomous systems on the Internet.

Typical Architecture

```text
ISP A

    │

BGP Session

    │

ISP B

    │

Route Exchange
```

Common Implementations

- Cisco IOS
- Juniper JunOS
- FRRouting (FRR)
- BIRD
- OpenBGPD

Example Scan

```bash
nmap -sV -p179 target
```

Security Recommendations

- Enable MD5 authentication.
- Filter advertised routes.
- Limit accepted prefixes.
- Monitor BGP session changes.
- Restrict peer IP addresses.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 161 | Network Monitoring (SNMP) |
| 162 | SNMP Trap Receiver |
| 177 | Linux GUI Login |
| 179 | Router / ISP Infrastructure |

---

# Blue Team Perspective

Recommendations

- Use SNMPv3 whenever possible.
- Remove default community strings.
- Disable XDMCP on production systems.
- Secure BGP sessions using authentication.
- Continuously monitor routing changes.
- Restrict management protocols to dedicated networks.

---

# Red Team Perspective

Interesting Targets

### Port 161

Possible Findings

- Device model
- Operating system
- Interface list
- Routing table
- Installed software
- Running processes

Enumeration Commands

```bash
nmap --script snmp-info target
```

```bash
nmap --script snmp-netstat target
```

```bash
nmap --script snmp-processes target
```

### Port 179

Possible Findings

- Internet routers
- Enterprise edge routers
- ISP infrastructure
- Route advertisements

Enumeration

```bash
nmap -sV -p179 target
```

---

# Common Nmap Commands

Scan Ports

```bash
nmap -p161-180 target
```

UDP Scan

```bash
nmap -sU -p161,162,177 target
```

Service Detection

```bash
nmap -sV -p161,177,179 target
```

Aggressive Scan

```bash
nmap -A -p161,179 target
```

---

# Summary

Ports **161–180** introduce several critical infrastructure services used in enterprise networking. **SNMP (161/162)** remains the standard protocol for monitoring network devices, while **BGP (179)** forms the backbone of Internet routing. Proper configuration, authentication, and access control are essential to protect these services from reconnaissance and unauthorized access.

---

# Ports 181–200

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 181 | TCP | Unify | Unify Networking Service | Legacy | Enterprise Systems | Rarely encountered today. |
| 182 | TCP | Audit | Security Audit Service | Various | Auditing | Restrict administrative access. |
| 183 | TCP | OCBinder | Object Binder | Legacy | Enterprise Middleware | Historical implementation. |
| 184 | TCP | OCBinder | Object Binder Service | Legacy | Enterprise Applications | Rarely used. |
| 185 | TCP | Remote KIS | Security Service | Vendor Specific | Authentication | Internal use only. |
| 186 | TCP | KIS Protocol | Enterprise Protocol | Vendor Specific | Management | Restrict access. |
| 187 | TCP | Plus Five MTP | Messaging Protocol | Historical | Messaging | Obsolete. |
| 188 | TCP | Mumps | MUMPS Database | InterSystems | Healthcare | Restrict database access. |
| 189 | TCP | QFT | Quick File Transfer | Legacy | File Transfer | Historical protocol. |
| 190 | TCP | GACP | Gateway Access Control | Vendor Specific | Gateway Management | Internal access only. |
| 191 | TCP | Prospero | Distributed File Service | Prospero | Directory Services | Rarely deployed. |
| 192 | TCP | OSU Network Monitor | Network Monitoring | Legacy | Monitoring | Historical implementation. |
| 193 | TCP | SRMP | Simple Resource Monitoring | Legacy | Monitoring | Obsolete. |
| 194 | TCP | IRC | Internet Relay Chat | UnrealIRCd, InspIRCd | Chat Server | Monitor for unauthorized public access. |
| 195 | TCP | DNSIX Network | Secure DNS | Historical | Networking | Rarely used. |
| 196 | TCP | DN6-NLM-AUD | Network Audit | Legacy | Auditing | Historical. |
| 197 | TCP | DLS | Directory Location Service | Various | Directory Services | Restrict externally. |
| 198 | TCP | DLS Monitor | Directory Monitoring | Various | Monitoring | Internal use. |
| 199 | TCP | SMUX | SNMP Multiplexer | Net-SNMP | SNMP Extensions | Restrict management traffic. |
| 200 | TCP | SRC | IBM System Resource Controller | IBM AIX | System Management | Internal administrative service. |

---

# Port Spotlight

## Port 188 — MUMPS Database

MUMPS (Massachusetts General Hospital Utility Multi-Programming System) is a programming language and database platform widely used in healthcare environments.

Typical Deployments

- Electronic Health Records (EHR)
- Hospital Information Systems (HIS)
- Laboratory Systems
- Clinical Applications

Architecture

```text
Healthcare Application

        │

Database Query

        ▼

MUMPS Database

        │

Patient Records

Appointments

Medical History
```

Security Recommendations

- Restrict database access.
- Encrypt network communications.
- Audit database activity.
- Enforce strong authentication.

---

## Port 194 — IRC

Internet Relay Chat (IRC) provides real-time text communication.

Typical Architecture

```text
Client

     │

IRC Server

     │

Channels

#general

#support

#admin
```

Common Software

- InspIRCd
- UnrealIRCd
- ircd-hybrid
- Ergo

Example Scan

```bash
nmap -sV -p194 target
```

Useful NSE Scripts

```bash
nmap --script irc-info target
```

```bash
nmap --script irc-botnet-channels target
```

Security Risks

- Botnet command-and-control (historically)
- Anonymous communication
- Misconfigured public servers

Recommendations

- Require authentication.
- Restrict administrative commands.
- Keep IRC software updated.

---

## Port 199 — SMUX

SMUX extends SNMP functionality by allowing additional management modules to register with an SNMP agent.

Typical Workflow

```text
Monitoring System

       │

SNMP Agent

       │

SMUX Module

       │

Extended MIB Objects
```

Common Usage

- Network appliances
- Enterprise monitoring
- Router extensions

Security Recommendations

- Restrict access to trusted management hosts.
- Disable unused SMUX modules.
- Monitor unexpected module registrations.

---

## Port 200 — IBM System Resource Controller

IBM System Resource Controller (SRC) manages system services on IBM AIX systems.

Typical Functions

- Service management
- Process monitoring
- Resource control
- System diagnostics

Typical Environment

```text
Administrator

      │

SRC Commands

      ▼

IBM AIX Server

      │

Managed Services
```

Security Recommendations

- Restrict administrative access.
- Monitor privileged operations.
- Audit service management events.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 188 | Healthcare Database |
| 194 | IRC Server |
| 199 | SNMP Extension |
| 200 | IBM AIX System |

---

# Blue Team Perspective

Recommendations

- Protect healthcare databases.
- Restrict IRC usage within enterprise environments.
- Secure SNMP extensions.
- Audit IBM administrative services.
- Remove unused legacy protocols.
- Monitor privileged access.

---

# Red Team Perspective

Interesting Targets

### Port 188

Possible Findings

- Medical databases
- Hospital infrastructure
- Legacy healthcare applications

### Port 194

Possible Findings

- IRC server
- Internal chat platform
- Legacy botnet infrastructure

Useful Commands

```bash
nmap --script irc-info target
```

```bash
nmap -sV -p194 target
```

### Port 200

Possible Findings

- IBM AIX host
- Enterprise UNIX server
- Administrative services

Enumeration

```bash
nmap -sV -p200 target
```

---

# Common Nmap Commands

Scan Ports

```bash
nmap -p181-200 target
```

Version Detection

```bash
nmap -sV -p188,194,199,200 target
```

UDP Scan

```bash
nmap -sU -p199 target
```

Aggressive Scan

```bash
nmap -A -p194,200 target
```

---

# Summary

Ports **181–200** contain a mixture of legacy enterprise protocols, healthcare systems, messaging platforms, and administrative services. While many are uncommon in modern networks, ports such as **188 (MUMPS Database)**, **194 (IRC)**, **199 (SMUX)**, and **200 (IBM SRC)** may still appear in specialized enterprise or legacy environments. Recognizing these services can significantly improve network reconnaissance and infrastructure identification.

---

# Ports 201–220

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 201 | TCP | AppleTalk Routing Maintenance | AppleTalk Routing | Apple Legacy Systems | Network Routing | Legacy protocol. |
| 202 | TCP | AppleTalk Name Binding | AppleTalk NBP | Apple Legacy Systems | Name Resolution | Rarely encountered. |
| 203 | TCP | AppleTalk Echo | AppleTalk Diagnostics | Apple Legacy Systems | Troubleshooting | Historical. |
| 204 | TCP | AppleTalk Zone Information | AppleTalk ZIP | Apple Networks | Zone Discovery | Legacy infrastructure. |
| 205 | TCP | AppleTalk Routing | AppleTalk RTMP | Apple Networks | Routing | Obsolete in modern networks. |
| 206 | TCP | AppleTalk Data | AppleTalk ATP | Apple Systems | Data Transfer | Historical implementation. |
| 207 | TCP | AppleTalk Session | AppleTalk ASP | Apple Systems | Session Management | Rarely deployed. |
| 208 | TCP | AppleTalk Printer | PAP | Apple LaserWriter | Printing | Restrict printer access. |
| 209 | TCP | Quick Mail | Mail Service | Legacy Mail Systems | Messaging | Historical. |
| 210 | TCP | ANSI Z39.50 | Library Information Retrieval | Library Systems | Catalog Search | Restrict public exposure. |
| 211 | TCP | Texas Instruments 914C/G | Device Service | Industrial Systems | Device Management | Internal use only. |
| 212 | TCP | ANET | ATEXSSTR | Legacy | Enterprise | Historical. |
| 213 | TCP | IPX | Novell IPX | NetWare | Enterprise Networking | Legacy protocol. |
| 214 | TCP | VM PWSCS | IBM VM | IBM Systems | Printer Sharing | Internal only. |
| 215 | TCP | SoftPC | Virtual PC Communication | Legacy Software | Virtualization | Historical implementation. |
| 216 | TCP | CAIlic | Computer Associates License Manager | CA Technologies | License Management | Restrict access. |
| 217 | TCP | DBASE | Database Service | dBASE | Database Access | Legacy database platform. |
| 218 | TCP | MPP | Message Passing Protocol | Various | Middleware | Rarely encountered. |
| 219 | TCP | UARPS | AppleTalk Update Protocol | Apple Systems | Routing Updates | Historical protocol. |
| 220 | TCP | IMAP3 | Internet Message Access Protocol v3 | Legacy Mail Servers | Email | Superseded by IMAP4. |

---

# Port Spotlight

## Port 210 — ANSI Z39.50

ANSI Z39.50 is a client-server protocol for searching and retrieving information from remote databases.

It is commonly found in:

- University libraries
- National archives
- Digital repositories
- Government institutions

Typical Architecture

```text
Research Client

      │

Search Query

      ▼

Library Server

      │

Database Search

      ▼

Search Results
```

Common Software

- YAZ Toolkit
- Koha
- Evergreen ILS

Security Recommendations

- Restrict public access where appropriate.
- Use authenticated sessions when supported.
- Monitor search activity.

---

## Port 213 — IPX

Internetwork Packet Exchange (IPX) was developed by Novell for NetWare networks.

Typical Environment

```text
Client

    │

IPX Packet

    ▼

NetWare Server
```

Historical Uses

- File Sharing
- Print Services
- Enterprise LANs

Security Notes

Modern enterprise environments should migrate to TCP/IP-based services.

---

## Port 216 — CA License Manager

Computer Associates License Manager controls software licensing across enterprise environments.

Typical Workflow

```text
Application

     │

License Request

     ▼

License Server

     │

License Granted

     ▼

Application Starts
```

Common Uses

- Enterprise software licensing
- Floating licenses
- Centralized license management

Security Recommendations

- Restrict access to internal hosts.
- Monitor license server availability.
- Keep license manager software updated.

---

## Port 220 — IMAP3

IMAP3 was an experimental version of the Internet Message Access Protocol.

Although historically important, it has been replaced by IMAP4 (Port 143).

Recommendation

Modern systems should use:

- IMAP4 (143)
- IMAPS (993)

instead of IMAP3.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 210 | Library Information System |
| 213 | Novell NetWare |
| 216 | Enterprise License Server |
| 220 | Legacy Mail Server |

---

# Blue Team Perspective

Recommended Actions

- Remove obsolete AppleTalk services.
- Replace IPX with TCP/IP.
- Restrict license servers.
- Disable unused legacy mail protocols.
- Monitor internal enterprise services.

---

# Red Team Perspective

Interesting Targets

### Port 210

Possible Findings

- Digital library
- University infrastructure
- Archive systems

### Port 213

Possible Findings

- Legacy NetWare server
- Historical enterprise network

### Port 216

Possible Findings

- Enterprise software inventory
- Internal licensing infrastructure

Useful Commands

```bash
nmap -sV -p210,213,216,220 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p201-220 target
```

Service Detection

```bash
nmap -sV -p210,213,216 target
```

Aggressive Scan

```bash
nmap -A -p210,216 target
```

Version Detection

```bash
nmap --version-all -p201-220 target
```

---

# Summary

Ports **201–220** primarily consist of legacy enterprise services, AppleTalk protocols, licensing systems, and historical messaging standards. While these services are uncommon in modern infrastructures, they may still appear in specialized industrial environments, educational institutions, or organizations maintaining legacy systems. Identifying them correctly can provide valuable context during network reconnaissance.

---

# Ports 221–240

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 221 | TCP | Berkeley rlogind | Remote Login | BSD Systems | Remote Administration | Legacy protocol. |
| 222 | TCP | Berkeley rshd | Remote Shell | BSD Systems | Remote Command Execution | Replace with SSH. |
| 223 | TCP | Berkeley rcp | Remote Copy | BSD Systems | File Transfer | Uses plaintext authentication. |
| 224 | TCP | MASQDIALER | Modem Dial Service | Legacy | Remote Connectivity | Historical service. |
| 242 | TCP | Direct Client-to-Client | Messaging | IRC Clients | DCC File Transfer | Monitor for unauthorized transfers. |
| 243 | TCP | SUR-MEAS | Survey Measurement | Industrial | Data Collection | Vendor-specific implementation. |
| 244 | TCP | INBUSINESS | Business Service | Enterprise | Internal Applications | Restrict access. |
| 245 | TCP | LINK | Link Service | Vendor Specific | Internal Communication | Historical. |
| 246 | TCP | DSP3270 | IBM Mainframe | IBM Systems | Terminal Access | Restrict trusted hosts. |
| 247 | TCP | SUBNTBCST-TFTP | Subnetwork Broadcast TFTP | Embedded Devices | Network Boot | No authentication. |
| 248 | TCP | BHFHS | Vendor Service | Enterprise | Internal Communication | Rarely encountered. |
| 249 | TCP | SGI-DIAG | Silicon Graphics Diagnostics | SGI Systems | Diagnostics | Internal only. |
| 250 | TCP | CADLOCK | CAD License Manager | CAD Software | License Management | Restrict internal use. |
| 251 | TCP | RSVP Tunnel | Resource Reservation | Enterprise Networks | QoS | Rarely deployed. |
| 252 | TCP | Dynamic Host | Dynamic Host Allocation | Various | Networking | Vendor implementation. |
| 253 | TCP | Berkeley RCP | Remote Copy | BSD Systems | File Transfer | Deprecated. |
| 254 | TCP | VersaLink | Vendor Protocol | Enterprise | Internal Services | Historical. |
| 255 | TCP | Reserved | Reserved | N/A | Reserved | Normally closed. |
| 256 | TCP | RAP | Remote Access | Vendor Specific | Management | Restrict access. |
| 257 | TCP | Secure Electronic Transaction | SET | Financial Applications | Payment Systems | Historical implementation. |

---

# Port Spotlight

## Port 222 — Berkeley Remote Shell (rsh)

The Berkeley Remote Shell protocol allows remote command execution without the strong authentication mechanisms provided by SSH.

Typical Workflow

```text
Administrator

      │

Remote Command

      ▼

rsh Server

      │

Command Executed
```

Security Risks

- Plaintext communication
- Host-based authentication
- No encryption
- Easily intercepted on untrusted networks

Recommendation

Replace all rsh services with SSH.

---

## Port 223 — Berkeley Remote Copy (rcp)

RCP allows copying files between UNIX systems.

Typical Usage

```text
Host A

     │

File Transfer

     ▼

Host B
```

Common Replacement

- SCP
- SFTP
- rsync over SSH

Security Recommendations

- Disable rcp.
- Use encrypted file transfer protocols.
- Restrict legacy services.

---

## Port 247 — Broadcast TFTP

Broadcast TFTP is commonly associated with network boot and embedded systems.

Typical Environment

```text
PXE Client

      │

Broadcast Request

      ▼

TFTP Server

      │

Boot Image

      ▼

Operating System
```

Common Uses

- PXE Boot
- Thin Clients
- Embedded Devices
- Network Appliances

Security Recommendations

- Restrict TFTP to isolated networks.
- Never expose publicly.
- Audit firmware images.

---

## Port 250 — CAD License Manager

Enterprise engineering software frequently relies on centralized license servers.

Examples

- AutoCAD
- SolidWorks
- CATIA
- Siemens NX

Architecture

```text
Engineering Workstation

        │

License Request

        ▼

License Server

        │

License Granted
```

Security Recommendations

- Restrict access to engineering VLANs.
- Backup license databases.
- Monitor license usage.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 222 | Legacy UNIX Server |
| 223 | Legacy File Transfer |
| 247 | PXE / Network Boot |
| 250 | CAD Infrastructure |

---

# Blue Team Perspective

Recommendations

- Remove Berkeley r-services.
- Replace plaintext protocols.
- Restrict PXE environments.
- Secure engineering license servers.
- Disable obsolete services.
- Monitor administrative traffic.

---

# Red Team Perspective

Interesting Targets

### Port 222

Possible Findings

- Legacy UNIX hosts
- Weak authentication
- Command execution opportunities

### Port 223

Possible Findings

- Legacy file transfer
- Trust relationships

### Port 247

Possible Findings

- Boot infrastructure
- Firmware repositories
- Configuration images

Enumeration Commands

```bash
nmap -sV -p222,223,247,250 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p221-240 target
```

Version Detection

```bash
nmap -sV -p222,223,247,250 target
```

Aggressive Detection

```bash
nmap -A -p221-240 target
```

Default Scripts

```bash
nmap -sC -p221-240 target
```

---

# Summary

Ports **221–240** continue the transition from legacy UNIX networking services to specialized enterprise applications. Protocols such as **rsh** and **rcp** should no longer be used due to their lack of encryption, while services related to PXE boot environments and centralized license management remain relevant in modern enterprise networks.

---

# Ports 241–260

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 241 | TCP | Reserved | Reserved Service | N/A | Reserved | Normally closed. |
| 242 | TCP | Direct Client-to-Client | IRC DCC | IRC Clients | File Transfer | Monitor unauthorized transfers. |
| 243 | TCP | SUR-MEAS | Survey Measurement | Industrial Systems | Data Collection | Vendor-specific protocol. |
| 244 | TCP | INBUSINESS | Business Application | Enterprise | Internal Services | Restrict external access. |
| 245 | TCP | LINK | Link Service | Various | Internal Communication | Rarely encountered. |
| 246 | TCP | DSP3270 | IBM Terminal Access | IBM Mainframe | Terminal Sessions | Restrict trusted hosts. |
| 247 | TCP | SUBNTBCST-TFTP | Broadcast TFTP | PXE Systems | Network Boot | No authentication or encryption. |
| 248 | TCP | BHFHS | Vendor Service | Enterprise | Internal Communication | Historical implementation. |
| 249 | TCP | SGI-DIAG | Silicon Graphics Diagnostics | SGI | System Diagnostics | Internal access only. |
| 250 | TCP | CADLOCK | CAD License Manager | AutoCAD, CATIA | License Management | Restrict license servers. |
| 251 | TCP | RSVP Tunnel | RSVP Tunnel | Enterprise Networks | QoS | Rarely deployed. |
| 252 | TCP | Dynamic Host | Dynamic Host Service | Various | Networking | Vendor implementation. |
| 253 | TCP | Berkeley RCP | Remote Copy | BSD Systems | File Transfer | Replace with SCP or SFTP. |
| 254 | TCP | VersaLink | Vendor Protocol | Various | Enterprise | Internal use only. |
| 255 | TCP | Reserved | Reserved Port | N/A | Reserved | Usually closed. |
| 256 | TCP | RAP | Remote Access Protocol | Various | Management | Restrict administrative access. |
| 257 | TCP | Secure Electronic Transaction | SET | Financial Software | Payment Systems | Legacy implementation. |
| 258 | TCP | Yak Chat | Messaging | Legacy | Internal Chat | Historical. |
| 259 | TCP | ESRO-GEN | Efficient Short Remote Operations | Legacy | Embedded Systems | Rarely encountered. |
| 260 | TCP | Openport | Generic Application Port | Various | Vendor Applications | Verify service identity. |

---

# Port Spotlight

## Port 242 — IRC Direct Client-to-Client (DCC)

DCC enables peer-to-peer communication between IRC users without routing all traffic through the IRC server.

Typical Uses

- Direct messaging
- File transfers
- Voice chat
- Peer-to-peer connections

Architecture

```text
User A

    │

Direct Connection

    ▼

User B
```

Security Considerations

- File transfer abuse
- Malware distribution
- Unauthorized data exchange
- Firewall bypass attempts

Recommendation

Monitor DCC traffic and restrict its use in enterprise environments.

---

## Port 247 — Broadcast TFTP

Broadcast TFTP is commonly associated with PXE (Preboot Execution Environment) and network boot operations.

Typical Boot Process

```text
Client

   │

PXE Request

   ▼

DHCP Server

   │

TFTP Request

   ▼

Boot Server

   │

Boot Image

   ▼

Operating System
```

Common Environments

- Data Centers
- Thin Clients
- Diskless Workstations
- Network Appliances

Security Recommendations

- Isolate PXE infrastructure.
- Restrict TFTP access.
- Verify boot image integrity.
- Log firmware downloads.

---

## Port 250 — CADLOCK

CADLOCK is commonly associated with centralized license management systems.

Typical Applications

- AutoCAD
- CATIA
- SolidWorks
- Siemens NX
- Creo

Workflow

```text
CAD Workstation

      │

License Request

      ▼

License Server

      │

License Granted

      ▼

Application Starts
```

Security Recommendations

- Place license servers on internal networks.
- Restrict firewall access.
- Backup license databases.
- Monitor unusual license requests.

---

## Port 257 — Secure Electronic Transaction (SET)

SET was designed to provide secure payment processing for electronic commerce.

Components

```text
Customer

     │

Merchant

     │

Payment Gateway

     │

Bank
```

Although largely replaced by TLS-based payment systems, SET remains historically important in secure payment protocol development.

Security Recommendations

- Use modern TLS.
- Follow PCI DSS requirements.
- Encrypt payment data.
- Monitor transaction logs.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 242 | IRC File Transfer |
| 247 | PXE Boot Infrastructure |
| 250 | Engineering License Server |
| 257 | Legacy Payment Infrastructure |

---

# Blue Team Perspective

Recommended Actions

- Disable unused IRC services.
- Secure PXE environments.
- Restrict TFTP servers.
- Audit engineering license servers.
- Remove obsolete payment protocols.
- Segment management infrastructure.

---

# Red Team Perspective

Interesting Targets

### Port 242

Possible Findings

- Internal chat platforms
- File-sharing channels
- User communication

### Port 247

Possible Findings

- PXE servers
- Boot images
- Firmware repositories

### Port 250

Possible Findings

- Engineering departments
- License servers
- Enterprise software inventory

Useful Commands

```bash
nmap -sV -p242,247,250,257 target
```

```bash
nmap -A -p247 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p241-260 target
```

Version Detection

```bash
nmap -sV -p242,247,250 target
```

Default Scripts

```bash
nmap -sC -p241-260 target
```

Aggressive Scan

```bash
nmap -A -p241-260 target
```

---

# Summary

Ports **241–260** primarily contain specialized enterprise services, legacy communication protocols, and infrastructure components. Although these ports are less frequently encountered than lower-numbered ports, they may appear in engineering environments, PXE deployment infrastructures, industrial systems, and legacy enterprise applications. Correct identification of these services can provide valuable insight during reconnaissance and security assessments.

---

# Ports 261–280

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 261 | TCP | IIOP Name Service | CORBA Naming Service | CORBA | Enterprise Middleware | Restrict access to trusted hosts. |
| 262 | TCP | ARCisdms | ARC Information Service | Legacy | Enterprise Systems | Rarely encountered. |
| 263 | TCP | HDAP | Hewlett-Packard Data Access | HP Systems | Enterprise Management | Vendor specific. |
| 264 | TCP | BGMP | Border Gateway Multicast Protocol | Routers | Multicast Routing | Historical implementation. |
| 265 | TCP | X-Bone CTL | Overlay Network Control | Research Networks | Experimental | Rarely deployed. |
| 266 | TCP | SCSI on Remote TCP | Remote Storage | Storage Systems | Remote Disk Access | Restrict storage traffic. |
| 267 | TCP | Tobit David | Messaging Platform | Tobit | Collaboration | Internal deployment. |
| 268 | TCP | Tobit David Service | Collaboration Service | Tobit | Messaging | Vendor specific. |
| 269 | TCP | MANET | Mobile Ad Hoc Networking | Research | Wireless Networks | Experimental. |
| 270 | TCP | QMODEM | File Transfer | Legacy | Historical | Obsolete. |
| 271 | TCP | PT-TLS | Protected TLS Transport | Various | Secure Communication | Verify encryption settings. |
| 272 | TCP | IPTM | Integrated Process Transport | Industrial | Enterprise | Internal only. |
| 273 | TCP | UMS | Unified Messaging | Various | Messaging | Restrict external access. |
| 274 | TCP | NTSKE | Network Time Security | NTP Implementations | Secure Time Sync | Ensure authenticated communication. |
| 275 | TCP | Personal Link | Vendor Protocol | Various | Synchronization | Rarely encountered. |
| 276 | TCP | CTP | Computer Telephony | PBX Systems | Voice Services | Internal infrastructure. |
| 277 | TCP | DAB-STI-C | Digital Audio Broadcasting | Broadcast Systems | Media | Specialized deployment. |
| 278 | TCP | EPD | Enterprise Process Dispatcher | Middleware | Enterprise | Restrict administrative access. |
| 279 | TCP | PLS | Packet Layer Service | Various | Networking | Vendor implementation. |
| 280 | TCP | HTTP Management | Embedded Web Interface | Network Appliances | Administration | Require authentication and HTTPS. |

---

# Port Spotlight

## Port 266 — Remote SCSI

Remote SCSI allows storage devices to be accessed over TCP/IP networks.

Typical Environment

```text
Application Server

       │

Storage Request

       ▼

Remote Storage

       │

Disk Blocks

       ▼

Storage Array
```

Typical Uses

- SAN environments
- Enterprise storage
- Backup systems
- Virtualization

Security Recommendations

- Isolate storage traffic.
- Restrict access to storage networks.
- Encrypt management traffic.
- Monitor unusual storage activity.

---

## Port 267–268 — Tobit David

Tobit David is a unified messaging and collaboration platform.

Features

- Email
- Fax
- Voice messaging
- Calendar
- Contacts
- Collaboration

Typical Deployment

```text
Users

   │

Messaging Platform

   ▼

Tobit Server

   │

Mail

Fax

Voice
```

Security Recommendations

- Restrict Internet exposure.
- Enable encrypted communication.
- Monitor authentication logs.
- Keep collaboration software updated.

---

## Port 274 — Network Time Security (NTS)

NTS extends the Network Time Protocol by adding authentication and encryption.

Benefits

- Authenticated time synchronization
- Protection against spoofing
- Secure enterprise deployments

Architecture

```text
Client

   │

TLS Handshake

   ▼

NTS Server

   │

Authenticated Time

   ▼

Client Clock Updated
```

Security Recommendations

- Prefer NTS over unauthenticated NTP where supported.
- Synchronize critical infrastructure.
- Monitor certificate validity.

---

## Port 280 — Embedded HTTP Management

Many embedded devices expose web-based management interfaces on alternate HTTP ports.

Examples

- Routers
- Switches
- Firewalls
- NAS Devices
- IP Cameras
- IoT Devices

Example

```text
http://192.168.1.1:280
```

Example Scan

```bash
nmap -sV -p280 target
```

Useful NSE Scripts

```bash
nmap --script http-title target -p280
```

```bash
nmap --script http-enum target -p280
```

```bash
nmap --script http-headers target -p280
```

Security Recommendations

- Require strong authentication.
- Disable default credentials.
- Use HTTPS whenever available.
- Restrict administrative interfaces to management networks.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 266 | Enterprise Storage |
| 267 | Tobit Collaboration |
| 268 | Tobit Messaging |
| 274 | Secure Time Synchronization |
| 280 | Embedded Device Management |

---

# Blue Team Perspective

Recommended Actions

- Isolate storage infrastructure.
- Protect collaboration servers.
- Use authenticated time synchronization.
- Disable default passwords on embedded devices.
- Restrict management interfaces.
- Monitor administrative logins.

---

# Red Team Perspective

Interesting Targets

### Port 266

Possible Findings

- Storage systems
- Backup infrastructure
- Virtualization platforms

### Port 267–268

Possible Findings

- Corporate messaging
- Internal collaboration
- User accounts

### Port 280

Possible Findings

- Router administration
- Firewall management
- NAS web interfaces
- IoT management consoles

Useful Commands

```bash
nmap -sV -p266,267,268,274,280 target
```

```bash
nmap --script http-title,http-enum -p280 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p261-280 target
```

Version Detection

```bash
nmap -sV -p266,267,268,274,280 target
```

Aggressive Scan

```bash
nmap -A -p261-280 target
```

Default Scripts

```bash
nmap -sC -p261-280 target
```

---

# Summary

Ports **261–280** introduce enterprise collaboration platforms, storage services, secure time synchronization, and embedded device management interfaces. While many services in this range are specialized, they are commonly encountered in enterprise infrastructures, data centers, and network appliances. Proper segmentation, authentication, and encryption are essential to securing these services.

---

# Ports 281–300

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 281 | TCP | Personal Link | Legacy Synchronization | Vendor Software | Personal Devices | Rarely used today. |
| 282 | TCP | Cable Port AX | Industrial Communication | Vendor Specific | Automation | Internal use only. |
| 283 | TCP | RESCAP | Resource Capability Exchange | Enterprise Systems | Resource Discovery | Historical protocol. |
| 284 | TCP | CORERJD | Core Remote Job Dispatch | Legacy Systems | Job Scheduling | Restrict administrative access. |
| 285 | TCP | FXP | File Exchange Protocol | Enterprise Applications | File Sharing | Monitor unauthorized transfers. |
| 286 | TCP | K-BLOCK | Vendor Service | Enterprise | Internal Communication | Rarely encountered. |
| 287 | TCP | Novastorbakcup | Backup Service | NovaBACKUP | Backup Infrastructure | Restrict access. |
| 288 | TCP | CSG-Box | Embedded Device Service | Network Appliances | Device Management | Restrict external exposure. |
| 289 | TCP | M2UA | MTP2 User Adaptation | Telecom Equipment | SS7 over IP | Specialized infrastructure. |
| 290 | TCP | Quake | Multiplayer Game Server | id Software | Gaming | Usually Internet-facing. |
| 291 | TCP | Expo | Window System | Legacy UNIX | Remote Graphics | Historical implementation. |
| 292 | TCP | Hyper-G | Hypermedia Server | Research Networks | Information Services | Rarely deployed. |
| 293 | TCP | IPT ANARA | Vendor Service | Enterprise | Internal Communication | Vendor specific. |
| 294 | TCP | ESIP | Enterprise Service | Various | Internal Services | Restrict external access. |
| 295 | TCP | BMC-PATROL-RADAR | Infrastructure Monitoring | BMC Patrol | Monitoring | Protect monitoring systems. |
| 296 | TCP | BMC-PATROL | Monitoring Agent | BMC Patrol | Enterprise Monitoring | Restrict management traffic. |
| 297 | TCP | SMSQ | Messaging Queue | Enterprise Middleware | Message Processing | Internal service. |
| 298 | TCP | ENPP | Efficient Network Protocol | Vendor Specific | Enterprise | Historical. |
| 299 | TCP | AURORA | Enterprise Service | Vendor Software | Internal Applications | Vendor specific. |
| 300 | TCP | HBCI | Home Banking Computer Interface | Banking Software | Financial Transactions | Use encrypted communication. |

---

# Port Spotlight

## Port 287 — NovaBACKUP Service

NovaBACKUP provides enterprise backup and disaster recovery capabilities.

Typical Environment

```text
Workstations

      │

Backup Request

      ▼

Backup Server

      │

Storage Repository
```

Common Uses

- Scheduled backups
- Disaster recovery
- File restoration
- System image backups

Security Recommendations

- Encrypt backup repositories.
- Restrict administrative access.
- Monitor backup jobs.
- Verify backup integrity regularly.

---

## Port 289 — M2UA (MTP2 User Adaptation)

M2UA is part of the SIGTRAN protocol suite, allowing SS7 signaling to operate over IP networks.

Typical Architecture

```text
Telephone Switch

       │

SS7 Signaling

       ▼

SIGTRAN Gateway

       │

IP Network

       ▼

Remote Switch
```

Common Environments

- Telecom providers
- Mobile operators
- Carrier-grade infrastructure

Security Recommendations

- Restrict signaling networks.
- Monitor signaling traffic.
- Separate telecom infrastructure from enterprise networks.

---

## Port 295–296 — BMC Patrol

BMC Patrol is an enterprise monitoring platform used to supervise servers, databases, and applications.

Typical Deployment

```text
Monitoring Console

        │

Monitoring Agent

        ▼

Enterprise Servers

        │

Performance Metrics

Alerts
```

Common Monitored Systems

- Windows Servers
- Linux Servers
- Oracle Databases
- SQL Server
- VMware
- Network Devices

Example Scan

```bash
nmap -sV -p295,296 target
```

Security Recommendations

- Restrict monitoring interfaces.
- Protect administrative credentials.
- Keep monitoring agents updated.
- Monitor agent communications.

---

## Port 300 — HBCI

HBCI (Home Banking Computer Interface) is a German banking protocol used for secure financial communication.

Typical Workflow

```text
Customer Software

        │

Secure Banking Request

        ▼

Bank Server

        │

Transaction Processing

        ▼

Confirmation
```

Security Recommendations

- Require TLS encryption.
- Protect banking credentials.
- Monitor financial transactions.
- Implement strong authentication.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 287 | Backup Infrastructure |
| 289 | Telecom Network |
| 295 | Enterprise Monitoring |
| 296 | Monitoring Agent |
| 300 | Banking System |

---

# Blue Team Perspective

Recommendations

- Protect backup servers from ransomware.
- Segment telecom infrastructure.
- Restrict monitoring platforms to management networks.
- Secure banking communications.
- Audit privileged monitoring accounts.
- Maintain offline backups.

---

# Red Team Perspective

Interesting Targets

### Port 287

Possible Findings

- Backup repositories
- Recovery infrastructure
- Critical business data

### Port 295–296

Possible Findings

- Enterprise monitoring servers
- Infrastructure inventory
- Administrative credentials

### Port 300

Possible Findings

- Financial software
- Banking gateways
- Secure transaction platforms

Useful Commands

```bash
nmap -sV -p287,289,295,296,300 target
```

```bash
nmap -A -p295,296 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p281-300 target
```

Version Detection

```bash
nmap -sV -p287,289,295,296,300 target
```

Default Scripts

```bash
nmap -sC -p281-300 target
```

Aggressive Scan

```bash
nmap -A -p281-300 target
```

---

# Summary

Ports **281–300** include enterprise backup systems, telecom signaling protocols, monitoring platforms, and financial communication services. Although these ports are less common than standard web or mail services, they often support critical infrastructure. During reconnaissance, identifying these services can reveal backup environments, carrier networks, monitoring platforms, or financial systems that require careful security assessment.

---

# Ports 301–320

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 301 | TCP | PADL2SIM | PADL to SIM Bridge | Legacy Systems | Gateway Services | Historical protocol. |
| 302 | TCP | EKSHELL | Enterprise Remote Shell | Vendor Software | Administration | Restrict access to administrators. |
| 303 | TCP | PWSERVER | Printer/Web Server | Embedded Devices | Device Management | Disable if unused. |
| 304 | TCP | ICP | Internet Cache Protocol | Squid, Cache Servers | Proxy Cache Coordination | Restrict to trusted cache peers. |
| 305 | TCP | ISO-IP | ISO Transport over IP | Legacy Networking | Enterprise Communication | Rarely encountered. |
| 306 | TCP | TIMED | Time Synchronization | UNIX Systems | Time Services | Prefer authenticated NTP. |
| 307 | TCP | TSRM | Terminal Service | Legacy Systems | Remote Administration | Replace with modern alternatives. |
| 308 | TCP | COPS | Common Open Policy Service | Network Equipment | Policy Management | Restrict administrative access. |
| 309 | TCP | NNP | Network News Transfer | Legacy News Services | Information Sharing | Historical protocol. |
| 310 | TCP | EntrustTime | Secure Time Service | Entrust | Time Synchronization | Verify certificate integrity. |
| 311 | TCP | MacOS Server | Apple Enterprise Service | Apple Systems | Management | Internal only. |
| 312 | TCP | VSLMP | Vendor Service | Various | Enterprise | Vendor-specific. |
| 313 | TCP | Magenta Logic | Messaging | Enterprise | Internal Applications | Restrict exposure. |
| 314 | TCP | Opalis Robot | Automation Platform | Opalis | Workflow Automation | Protect automation servers. |
| 315 | TCP | DECnet | Digital Equipment Networking | DEC Systems | Enterprise Networks | Historical implementation. |
| 316 | TCP | Z39.50 | Information Retrieval | Libraries | Database Search | Restrict external access. |
| 317 | TCP | PKIX-Timestamp | Timestamp Service | PKI Infrastructure | Digital Signatures | Verify trusted CA. |
| 318 | TCP | PKIX-CMC | Certificate Management | PKI Systems | Certificate Enrollment | Protect certificate authorities. |
| 319 | UDP | PTP Event | Precision Time Protocol | IEEE 1588 | High Precision Time Sync | Critical industrial infrastructure. |
| 320 | UDP | PTP General | Precision Time Protocol | IEEE 1588 | Time Synchronization | Protect against spoofing. |

---

# Port Spotlight

## Port 304 — Internet Cache Protocol (ICP)

Internet Cache Protocol enables proxy servers to cooperate by sharing cached web content.

Typical Architecture

```text
Client

   │

Proxy Server

   │

ICP Query

   ▼

Neighbor Proxy

   │

Cache Hit?

   ▼

Cached Content
```

Common Software

- Squid
- NetCache
- Enterprise Proxy Appliances

Example Scan

```bash
nmap -sU -p304 target
```

Security Recommendations

- Restrict ICP traffic to trusted proxy servers.
- Disable ICP if cache peering is unnecessary.
- Monitor cache communications.

---

## Port 308 — Common Open Policy Service (COPS)

COPS allows network devices to request policy decisions from centralized policy servers.

Common Uses

- Quality of Service (QoS)
- Network admission control
- Policy enforcement
- Enterprise networking

Architecture

```text
Network Device

      │

Policy Request

      ▼

Policy Server

      │

Policy Decision

      ▼

Device Enforcement
```

Security Recommendations

- Restrict access to policy servers.
- Use encrypted management networks.
- Audit policy modifications.

---

## Ports 319–320 — Precision Time Protocol (PTP)

Precision Time Protocol (IEEE 1588) provides sub-microsecond time synchronization for industrial and telecommunications environments.

Typical Deployment

```text
Grandmaster Clock

        │

PTP Event (319)

        │

PTP General (320)

        ▼

Industrial Devices

Robots

PLC

Switches
```

Common Environments

- Industrial automation
- Manufacturing
- Telecommunications
- Financial trading systems
- Scientific laboratories

Example Scan

```bash
nmap -sU -p319,320 target
```

Security Recommendations

- Restrict PTP domains.
- Protect Grandmaster clocks.
- Monitor synchronization anomalies.
- Prevent unauthorized time sources.

---

## Port 317–318 — PKI Services

Public Key Infrastructure services support certificate issuance and trusted timestamps.

Typical Workflow

```text
Client

   │

Certificate Request

   ▼

Certificate Authority

   │

Certificate Issued

   ▼

Secure Communication
```

Common Uses

- Digital certificates
- Code signing
- Secure email
- TLS authentication

Security Recommendations

- Protect Certificate Authorities.
- Monitor certificate issuance.
- Use Hardware Security Modules (HSMs) where possible.
- Audit certificate lifecycle events.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 304 | Proxy Cache Infrastructure |
| 308 | Network Policy Server |
| 317 | Timestamp Authority |
| 318 | Certificate Authority |
| 319–320 | Precision Time Protocol |

---

# Blue Team Perspective

Recommended Actions

- Secure proxy cache communications.
- Protect PKI infrastructure.
- Restrict policy servers.
- Monitor certificate issuance.
- Secure industrial timing systems.
- Audit management traffic.

---

# Red Team Perspective

Interesting Targets

### Port 304

Possible Findings

- Enterprise proxy servers
- Internet cache hierarchy
- Internal browsing infrastructure

### Port 317–318

Possible Findings

- Internal Certificate Authority
- Enterprise PKI
- Digital signature infrastructure

### Ports 319–320

Possible Findings

- Industrial control systems
- Telecom infrastructure
- Manufacturing networks

Useful Commands

```bash
nmap -sU -p304,319,320 target
```

```bash
nmap -sV -p308,317,318 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p301-320 target
```

UDP Scan

```bash
nmap -sU -p304,319,320 target
```

Version Detection

```bash
nmap -sV -p304,308,317,318 target
```

Aggressive Scan

```bash
nmap -A -p301-320 target
```

---

# Summary

Ports **301–320** introduce enterprise policy management, proxy cache coordination, Public Key Infrastructure (PKI), and **Precision Time Protocol (PTP)** services. While many of these ports are uncommon in typical corporate environments, they play critical roles in industrial automation, certificate management, telecommunications, and enterprise networking. Proper identification of these services can reveal highly valuable infrastructure during reconnaissance and security assessments.

---

# Ports 321–340

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 321 | TCP | PIPE Server | Enterprise Pipe Service | Vendor Specific | IPC | Restrict internal access. |
| 322 | TCP | RTSP Control | Streaming Control | Multimedia Systems | Streaming | Protect management interfaces. |
| 323 | UDP | IPTP | Internet Time Protocol | Legacy Systems | Time Synchronization | Historical implementation. |
| 324 | TCP | IBM App Connect | Enterprise Middleware | IBM Products | Integration | Restrict trusted hosts. |
| 325 | TCP | DEC Network | DECnet Services | Legacy DEC Systems | Enterprise Networking | Historical protocol. |
| 326 | TCP | Meta5 | Enterprise Collaboration | Meta5 | Messaging | Vendor-specific deployment. |
| 327 | TCP | AgentX | SNMP Agent Extension | Net-SNMP | Network Monitoring | Restrict management access. |
| 328 | TCP | Apple Remote Event | Apple Systems | Remote Automation | Internal management only. |
| 329 | TCP | TX Control | Transaction Service | Enterprise Software | Transaction Processing | Monitor privileged operations. |
| 330 | TCP | Cisco Agent | Cisco Equipment | Device Management | Internal infrastructure only. |
| 331 | TCP | DEC Notes | Messaging Service | DEC Systems | Collaboration | Legacy platform. |
| 332 | TCP | SSQL | Secure SQL Service | Database Platforms | Database Access | Restrict database exposure. |
| 333 | TCP | Texar Security Port | Security Appliance | Security Products | Monitoring | Internal deployment. |
| 334 | TCP | Microsoft Cluster Net | Cluster Communication | Windows Clustering | HA Systems | Restrict cluster traffic. |
| 335 | TCP | FatPipe | WAN Optimization | FatPipe Networks | SD-WAN | Internal use only. |
| 336 | TCP | COPS-TLS | Secure Policy Management | Network Devices | Policy Control | Use encrypted sessions. |
| 337 | TCP | GateControl | Access Management | Enterprise | Security | Restrict administrators. |
| 338 | TCP | Gnutella | Peer-to-Peer Service | P2P Clients | File Sharing | Monitor for unauthorized usage. |
| 339 | TCP | Enterprise Monitoring | Monitoring Platform | Vendor Software | Infrastructure Monitoring | Protect management interfaces. |
| 340 | TCP | Unknown / Vendor | Vendor Service | Various | Enterprise | Verify service identity. |

---

# Port Spotlight

## Port 327 — AgentX

AgentX is an extension protocol for SNMP that allows multiple management modules to communicate with a master SNMP agent.

Typical Architecture

```text
Network Monitoring

        │

Master SNMP Agent

   ┌────┴────┐

AgentX     AgentX

Module      Module

   │           │

Extra MIB   Extra MIB
```

Common Uses

- Modular SNMP implementations
- Enterprise monitoring
- Network appliances
- Hardware management

Example Scan

```bash
nmap -sV -p327 target
```

Security Recommendations

- Restrict SNMP access.
- Disable unused AgentX modules.
- Monitor management communications.
- Use SNMPv3 whenever possible.

---

## Port 330 — Cisco Agent

Some Cisco products expose management-related services on this port.

Possible Deployments

- Network switches
- Routers
- Security appliances
- Management platforms

Typical Workflow

```text
Administrator

      │

Management Request

      ▼

Cisco Device

      │

Configuration

Monitoring

Diagnostics
```

Security Recommendations

- Restrict management interfaces.
- Use management VLANs.
- Enable AAA authentication.
- Audit configuration changes.

---

## Port 334 — Microsoft Cluster Network

Microsoft Failover Clustering relies on dedicated communication channels between cluster nodes.

Architecture

```text
Cluster Node A

      │

Heartbeat

      │

Cluster Node B

      │

Shared Storage
```

Common Environments

- Hyper-V Clusters
- SQL Server Failover Clusters
- File Server Clusters
- Enterprise Datacenters

Security Recommendations

- Isolate cluster networks.
- Restrict administrative access.
- Monitor heartbeat failures.
- Secure shared storage.

---

## Port 338 — Gnutella

Gnutella is a decentralized peer-to-peer file-sharing protocol.

Typical Topology

```text
Peer

 │

 ├──── Peer

 │

 ├──── Peer

 │

 └──── Peer
```

Common Risks

- Malware distribution
- Data leakage
- Copyright violations
- Shadow IT

Example Scan

```bash
nmap -sV -p338 target
```

Security Recommendations

- Block unauthorized P2P traffic.
- Monitor endpoints.
- Apply application control policies.
- Inspect outbound connections.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 327 | SNMP Extension |
| 330 | Cisco Device Management |
| 334 | Windows Failover Cluster |
| 338 | Peer-to-Peer File Sharing |

---

# Blue Team Perspective

Recommended Actions

- Secure SNMP infrastructure.
- Restrict Cisco management interfaces.
- Segment cluster communication.
- Block unauthorized peer-to-peer traffic.
- Monitor enterprise management services.
- Audit privileged administrative access.

---

# Red Team Perspective

Interesting Targets

### Port 327

Possible Findings

- Network monitoring infrastructure
- SNMP configuration
- Management credentials

### Port 330

Possible Findings

- Cisco routers
- Enterprise switches
- Firewall management

### Port 334

Possible Findings

- High Availability clusters
- SQL Server clusters
- Virtualization infrastructure

### Port 338

Possible Findings

- Unauthorized P2P software
- Internal file sharing
- User workstations

Useful Commands

```bash
nmap -sV -p327,330,334,338 target
```

```bash
nmap --script snmp-info -p327 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p321-340 target
```

Version Detection

```bash
nmap -sV -p327,330,334,338 target
```

Default Scripts

```bash
nmap -sC -p321-340 target
```

Aggressive Scan

```bash
nmap -A -p321-340 target
```

---

# Summary

Ports **321–340** include enterprise management protocols, SNMP extensions, clustering services, and peer-to-peer communication technologies. While many services in this range are vendor-specific, ports such as **327 (AgentX)**, **330 (Cisco Management)**, **334 (Microsoft Cluster Network)**, and **338 (Gnutella)** can reveal valuable information about enterprise infrastructure, high-availability environments, and endpoint activity during network reconnaissance.

---

# Ports 341–360

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 341 | TCP | BMC Patrol Agent | Monitoring Agent | BMC Patrol | Enterprise Monitoring | Restrict management access. |
| 342 | TCP | DTM | Distributed Transaction Manager | Enterprise Middleware | Transactions | Internal infrastructure only. |
| 343 | TCP | Prospect | Data Collection Service | Vendor Specific | Enterprise | Historical deployment. |
| 344 | TCP | PSRP | Performance Reporting | Monitoring Platforms | Metrics Collection | Restrict access. |
| 345 | TCP | PAKNET | Packet Network Service | Legacy | WAN Communication | Rarely encountered. |
| 346 | TCP | ZServ | Zebra Device Service | Zebra Printers | Device Management | Internal only. |
| 347 | TCP | FATSERV | File Access Service | Enterprise | File Sharing | Restrict authentication. |
| 348 | TCP | CSI-SGWP | Gateway Protocol | Telecom | Signaling | Specialized deployments. |
| 349 | TCP | MFTP | Managed File Transfer | Enterprise MFT | Secure File Exchange | Prefer encrypted sessions. |
| 350 | TCP | MATIP-Type A | Mainframe Access | IBM Systems | Financial Networks | Restrict trusted hosts. |
| 351 | TCP | MATIP-Type B | Mainframe Access | IBM Systems | Banking Infrastructure | Internal only. |
| 352 | TCP | DTAG-STE-SB | Telecom Service | Carrier Networks | Signaling | Vendor specific. |
| 353 | TCP | NDSAUTH | Directory Authentication | Novell eDirectory | Authentication | Secure credentials. |
| 354 | TCP | BH611 | Vendor Service | Enterprise | Internal Applications | Verify service identity. |
| 355 | TCP | DATEX-ASN | Data Exchange | Enterprise | Messaging | Historical implementation. |
| 356 | TCP | CLOANTO-NET | Network Service | Cloanto Software | Synchronization | Rarely encountered. |
| 357 | TCP | SHRINKWRAP | Software Distribution | Enterprise | Package Delivery | Restrict administrative access. |
| 358 | TCP | TENEBRIS | Vendor Service | Enterprise | Internal Services | Internal use only. |
| 359 | TCP | NSRMP | Network Resource Management | Enterprise | Infrastructure Management | Restrict management interfaces. |
| 360 | TCP | SCOI2ODIALOG | SCO OpenServer | UNIX Systems | Administrative Services | Protect privileged access. |

---

# Port Spotlight

## Port 349 — Managed File Transfer (MFT)

Managed File Transfer solutions provide centralized, secure, and auditable file exchanges between organizations and internal systems.

Unlike FTP, enterprise MFT platforms include encryption, authentication, scheduling, auditing, and compliance reporting.

Typical Architecture

```text
Business Application

        │

File Transfer Request

        ▼

MFT Server

   ┌─────────────┐

Internal      External

Partner A     Partner B

   │             │

Encrypted File Exchange
```

Common Software

- IBM Sterling File Gateway
- GoAnywhere MFT
- Progress MOVEit
- Axway SecureTransport

Example Scan

```bash
nmap -sV -p349 target
```

Security Recommendations

- Enforce TLS encryption.
- Enable detailed audit logging.
- Apply least-privilege access.
- Rotate service credentials regularly.

---

## Ports 350–351 — MATIP

MATIP (Mapping of Airline Traffic over IP) enables legacy airline and financial mainframe systems to communicate over TCP/IP networks.

Common Environments

- Airlines
- Banking
- Reservation Systems
- Mainframe Data Centers

Architecture

```text
Terminal

    │

MATIP Gateway

    │

TCP/IP Network

    │

IBM Mainframe
```

Security Recommendations

- Isolate legacy infrastructure.
- Restrict external connectivity.
- Monitor mainframe communications.
- Replace unsupported implementations where possible.

---

## Port 353 — Directory Authentication

Port 353 has historically been associated with authentication services in Novell-based environments.

Typical Workflow

```text
Client

   │

Authentication Request

   ▼

Directory Server

   │

Credential Validation

   ▼

Access Granted
```

Common Uses

- Enterprise login
- Identity validation
- Centralized authentication

Security Recommendations

- Enforce strong password policies.
- Enable multi-factor authentication where possible.
- Monitor authentication failures.
- Protect directory services from Internet exposure.

---

## Port 360 — SCO Administrative Services

SCO OpenServer systems may expose administrative services on this port.

Typical Environment

```text
Administrator

      │

Administrative Request

      ▼

SCO UNIX Server

      │

System Services

User Management

Configuration
```

Security Recommendations

- Restrict administrative interfaces.
- Disable unused legacy services.
- Apply vendor security updates.
- Audit administrator activity.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 349 | Managed File Transfer Platform |
| 350–351 | IBM Mainframe / Airline Systems |
| 353 | Enterprise Authentication Service |
| 360 | Legacy UNIX Administration |

---

# Blue Team Perspective

Recommended Actions

- Secure enterprise file transfer platforms.
- Segment mainframe infrastructure.
- Protect centralized authentication systems.
- Remove obsolete UNIX services.
- Restrict administrative interfaces.
- Continuously monitor privileged accounts.

---

# Red Team Perspective

Interesting Targets

### Port 349

Possible Findings

- Enterprise file exchange platform
- Business partner integrations
- Sensitive document transfers

### Ports 350–351

Possible Findings

- Mainframe connectivity
- Airline reservation systems
- Banking infrastructure

### Port 353

Possible Findings

- Identity management platform
- Enterprise authentication
- Legacy directory services

Enumeration Commands

```bash
nmap -sV -p349,350,351,353,360 target
```

```bash
nmap -A -p349,353 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p341-360 target
```

Version Detection

```bash
nmap -sV -p349,350,351,353,360 target
```

Aggressive Scan

```bash
nmap -A -p341-360 target
```

Default Scripts

```bash
nmap -sC -p341-360 target
```

---

# Summary

Ports **341–360** primarily include enterprise middleware, managed file transfer platforms, legacy mainframe communication protocols, and authentication services. Although many services in this range are vendor-specific, ports such as **349 (Managed File Transfer)**, **350–351 (MATIP)**, and **353 (Directory Authentication)** may reveal critical enterprise infrastructure during security assessments. Proper segmentation, encryption, and continuous monitoring are essential to securing these services.

---

# Ports 361–380

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 361 | TCP | SNMP over TLS | Secure SNMP | Net-SNMP | Secure Network Management | Prefer encrypted management. |
| 362 | TCP | SNMP Trap over TLS | Secure Trap Service | Enterprise Monitoring | Event Notifications | Restrict management networks. |
| 363 | TCP | RSVP Tunnel | Resource Reservation | Routers | QoS | Internal routing only. |
| 364 | TCP | Aurora CM | Cluster Management | Vendor Software | High Availability | Restrict administrative access. |
| 365 | TCP | ODMR | On-Demand Mail Relay | Mail Servers | Email Retrieval | Legacy protocol. |
| 366 | TCP | ODMR Secure | Secure Mail Relay | Enterprise Mail | Messaging | Use modern SMTP submission instead. |
| 367 | TCP | MortgageWare | Financial Application | Banking Software | Loan Processing | Internal use only. |
| 368 | TCP | QBikGDP | Vendor Service | Enterprise | Management | Vendor-specific deployment. |
| 369 | TCP | RPC2PORTMAP | RPC Mapping | UNIX Systems | Service Discovery | Restrict access. |
| 370 | TCP | CODAAUTH2 | Authentication Service | Enterprise | Authentication | Protect credentials. |
| 371 | TCP | ClearCase | Version Control | IBM Rational | Software Development | Restrict repositories. |
| 372 | TCP | ULISTPROC | Mailing List Processor | Mail Platforms | Email Automation | Monitor automation tasks. |
| 373 | TCP | LEGENT-1 | Monitoring Agent | Legacy Software | Monitoring | Historical implementation. |
| 374 | TCP | LEGENT-2 | Monitoring Service | Legacy Software | Infrastructure Monitoring | Internal only. |
| 375 | TCP | HASSLE | Vendor Service | Enterprise | Internal Communication | Rarely encountered. |
| 376 | TCP | NI-PROT | Network Interface Protocol | Vendor Systems | Device Communication | Internal deployment. |
| 377 | TCP | HP Collector | HP Management | HP OpenView | Monitoring | Restrict management access. |
| 378 | TCP | HPCP | HP Control Protocol | HP Systems | Administration | Vendor-specific. |
| 379 | TCP | IBM APP | IBM Application Service | IBM Middleware | Enterprise Applications | Internal infrastructure. |
| 380 | TCP | IS99C | Legacy Service | Various | Enterprise | Verify service identity. |

---

# Port Spotlight

## Ports 361–362 — Secure SNMP

These ports are associated with transporting SNMP management traffic using TLS, providing authentication, integrity, and confidentiality that traditional SNMP lacks.

Typical Architecture

```text
Network Management System

          │

Encrypted SNMP

          ▼

Managed Device

          │

Secure Monitoring
```

Advantages

- Encrypted management traffic
- Improved authentication
- Better integrity protection
- Suitable for enterprise environments

Example Scan

```bash
nmap -sV -p361,362 target
```

Security Recommendations

- Prefer SNMPv3 with encryption.
- Restrict access to management VLANs.
- Disable legacy SNMP versions when possible.
- Monitor authentication failures.

---

## Port 365 — On-Demand Mail Relay (ODMR)

ODMR allows remote systems to retrieve queued email from a mail server.

Typical Workflow

```text
Mail Client

     │

Authentication

     ▼

Mail Server

     │

Queued Messages

     ▼

Client Download
```

Common Uses

- Remote branch offices
- Dial-up environments (historically)
- Legacy messaging systems

Security Recommendations

- Replace legacy mail retrieval mechanisms.
- Use authenticated encrypted sessions.
- Monitor relay activity.

---

## Port 371 — IBM Rational ClearCase

ClearCase is an enterprise version control and software configuration management platform.

Typical Deployment

```text
Developer

     │

Checkout Source Code

     ▼

ClearCase Server

     │

Repository

     ▼

Version History
```

Common Uses

- Source code management
- Enterprise software development
- Configuration management
- Release engineering

Example Scan

```bash
nmap -sV -p371 target
```

Security Recommendations

- Protect source repositories.
- Enforce role-based access.
- Enable audit logging.
- Restrict repository access.

---

## Ports 377–378 — HP Enterprise Management

These ports may be used by HP management products for infrastructure monitoring and administration.

Typical Environment

```text
HP OpenView

      │

Monitoring

      ▼

Servers

Switches

Storage

Printers
```

Security Recommendations

- Restrict management traffic.
- Enable encrypted communications.
- Audit administrator activity.
- Isolate management networks.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 361–362 | Secure SNMP Management |
| 365 | Legacy Mail Retrieval |
| 371 | IBM Rational ClearCase |
| 377–378 | HP Enterprise Management |

---

# Blue Team Perspective

Recommended Actions

- Replace insecure SNMP deployments.
- Remove obsolete mail protocols.
- Secure source code repositories.
- Isolate infrastructure management systems.
- Monitor privileged administrative activity.
- Maintain comprehensive audit logs.

---

# Red Team Perspective

Interesting Targets

### Ports 361–362

Possible Findings

- Enterprise monitoring platforms
- Secure management infrastructure
- Network device inventory

### Port 371

Possible Findings

- Source code repositories
- Internal development platforms
- Software release infrastructure

### Ports 377–378

Possible Findings

- HP management servers
- Network inventory
- Infrastructure monitoring

Useful Commands

```bash
nmap -sV -p361,362,371,377,378 target
```

```bash
nmap -A -p371 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p361-380 target
```

Version Detection

```bash
nmap -sV -p361,362,365,371,377,378 target
```

Default Scripts

```bash
nmap -sC -p361-380 target
```

Aggressive Scan

```bash
nmap -A -p361-380 target
```

---

# Summary

Ports **361–380** primarily include secure network management services, enterprise version control platforms, legacy email retrieval protocols, and infrastructure management systems. Although many services are vendor-specific, identifying ports such as **361–362 (Secure SNMP)**, **371 (IBM Rational ClearCase)**, and **377–378 (HP Enterprise Management)** can provide valuable insight into an organization's management infrastructure and software development environment.

---

# Ports 381–400

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 381 | TCP | HP OpenView | Network Management | HP OpenView | Enterprise Monitoring | Restrict management access. |
| 382 | TCP | HP OpenView | Event Management | HP OpenView | Monitoring | Internal management only. |
| 383 | TCP | HP Performance | Performance Monitoring | HP Software | Infrastructure Metrics | Secure management interfaces. |
| 384 | TCP | ARemote | Remote Administration | Vendor Software | System Management | Restrict trusted hosts. |
| 385 | TCP | IBM APP | IBM Enterprise Service | IBM Middleware | Enterprise Applications | Vendor-specific deployment. |
| 386 | TCP | ASA Message Router | Enterprise Messaging | Various | Message Routing | Internal infrastructure only. |
| 387 | TCP | Aurp | AppleTalk Update-Based Routing | Apple Legacy Systems | Routing | Historical protocol. |
| 388 | TCP | Unidata LDAPS | Directory Service | UniData | Authentication | Protect directory services. |
| 389 | TCP/UDP | LDAP | Lightweight Directory Access Protocol | Active Directory, OpenLDAP, OpenDJ | Directory Services | One of the most important enterprise ports. |
| 390 | TCP | SP Switch | IBM High Performance Switch | IBM Systems | Cluster Communication | Restrict internal access. |
| 391 | TCP | Sync Server | Synchronization Service | Vendor Software | Replication | Vendor-specific. |
| 392 | TCP | SynOptics | Network Management | Legacy Systems | Infrastructure | Historical deployment. |
| 393 | TCP | Data Acquisition | Enterprise Service | Various | Monitoring | Internal only. |
| 394 | TCP | EMC CAD | Storage Management | Dell EMC | Storage | Restrict administrative access. |
| 395 | TCP | NETCP | Network Control | Enterprise | Device Management | Monitor privileged operations. |
| 396 | TCP | Novell NetWare | Enterprise Service | NetWare | Legacy Networks | Historical implementation. |
| 397 | TCP | LAN Messaging | Enterprise Messaging | Various | Internal Communication | Restrict external access. |
| 398 | TCP | StarQuiz | Assessment Platform | Educational Systems | Testing | Verify service identity. |
| 399 | TCP | Digital Notary | PKI Service | Security Software | Digital Signatures | Protect certificate services. |
| 400 | TCP | Workstation Broker | Session Broker | Enterprise Platforms | Session Management | Restrict administrative access. |

---

# Port Spotlight

## Port 389 — LDAP (Lightweight Directory Access Protocol)

LDAP is one of the most widely deployed directory protocols in enterprise environments. It provides centralized authentication, authorization, and directory services.

It is heavily used by:

- Microsoft Active Directory
- OpenLDAP
- OpenDJ
- FreeIPA
- Red Hat Identity Management

Typical Architecture

```text
User

 │

Authentication Request

 ▼

LDAP Server

 │

Directory Database

 │

Users

Groups

Policies

Computers
```

Common Information Stored

- User accounts
- Password policies
- Groups
- Organizational Units (OU)
- Computers
- Printers
- Certificates

Example Scan

```bash
nmap -sV -p389 target
```

Useful NSE Scripts

```bash
nmap --script ldap-rootdse target
```

```bash
nmap --script ldap-search target
```

```bash
nmap --script ldap-brute target
```

Security Recommendations

- Use LDAPS (636) whenever possible.
- Disable anonymous binds.
- Enforce least privilege.
- Monitor failed authentication attempts.
- Require strong password policies.

---

## Port 388 — UniData Directory Services

Some UniData and enterprise middleware deployments expose authentication and directory-related services on this port.

Typical Environment

```text
Enterprise Application

       │

Authentication

       ▼

UniData Server

       │

User Database
```

Security Recommendations

- Restrict trusted clients.
- Encrypt management traffic.
- Keep vendor software updated.

---

## Port 399 — Digital Notary

Digital Notary services support trusted timestamps and digital document verification.

Typical Workflow

```text
Document

     │

Hash

     ▼

Digital Notary

     │

Timestamp

     ▼

Verified Document
```

Common Uses

- Legal documents
- Digital signatures
- Compliance
- PKI infrastructures

Security Recommendations

- Protect private keys.
- Monitor certificate usage.
- Restrict administrative access.
- Maintain trusted certificate chains.

---

## Port 400 — Workstation Broker

Session broker services coordinate user sessions across enterprise environments.

Typical Deployment

```text
User

 │

Login

 ▼

Session Broker

 │

Available Server

 ▼

Application Session
```

Common Environments

- Virtual Desktop Infrastructure (VDI)
- Terminal Services
- Remote Application Farms
- Enterprise Workspaces

Security Recommendations

- Protect broker credentials.
- Restrict Internet exposure.
- Monitor session creation.
- Audit privileged logins.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 388 | Enterprise Directory Platform |
| 389 | LDAP / Active Directory |
| 399 | Digital Signature Infrastructure |
| 400 | Session Broker / VDI |

---

# Blue Team Perspective

Recommended Actions

- Secure LDAP servers with TLS.
- Disable anonymous directory queries.
- Protect PKI infrastructure.
- Restrict session broker access.
- Monitor directory replication.
- Audit privileged directory changes.

---

# Red Team Perspective

Interesting Targets

### Port 389

Possible Findings

- Active Directory
- Domain Controllers
- Organizational Units
- User accounts
- Group memberships
- Domain information

Useful Enumeration

```bash
nmap --script ldap-rootdse -p389 target
```

```bash
nmap --script ldap-search -p389 target
```

### Port 400

Possible Findings

- VDI infrastructure
- Remote Desktop Farms
- Session brokers
- Enterprise application delivery

Enumeration Commands

```bash
nmap -sV -p389,400 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p381-400 target
```

Version Detection

```bash
nmap -sV -p388,389,399,400 target
```

LDAP Enumeration

```bash
nmap --script ldap-rootdse,ldap-search -p389 target
```

Aggressive Scan

```bash
nmap -A -p381-400 target
```

---

# Summary

Ports **381–400** introduce several enterprise management and directory-related services, with **Port 389 (LDAP)** standing out as one of the most critical ports for both administrators and penetration testers. LDAP often serves as the foundation of enterprise identity management, making it a high-value target during reconnaissance. Other services in this range, such as digital notary systems and session brokers, can reveal additional information about authentication infrastructure and remote access environments.

---

# Ports 401–420

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 401 | TCP | UPS Management | Power Management | APC, Eaton | UPS Monitoring | Restrict management access. |
| 402 | TCP | Genie | Device Management | Vendor Specific | Embedded Systems | Internal use only. |
| 403 | TCP | DEC-DNS | Digital Directory Service | DEC Systems | Name Resolution | Legacy deployment. |
| 404 | TCP | NDS | Novell Directory Services | eDirectory | Directory Services | Protect authentication data. |
| 405 | TCP | IS99A | Vendor Service | Enterprise | Internal Applications | Vendor-specific implementation. |
| 406 | TCP | IMSP | Internet Message Support Protocol | Messaging Platforms | Email Services | Historical protocol. |
| 407 | TCP | Timbuktu | Remote Desktop | Timbuktu Pro | Remote Administration | Restrict remote access. |
| 408 | TCP | PRM-SM | Performance Resource Management | Enterprise | Monitoring | Internal infrastructure. |
| 409 | TCP | PRM-NM | Network Management | Enterprise | Resource Management | Restrict privileged access. |
| 410 | TCP | Decladebug | Remote Debugging | Development Tools | Debugging | Never expose publicly. |
| 411 | TCP | RMT | Remote Maintenance | Vendor Software | Administration | Vendor-specific deployment. |
| 412 | TCP | Synoptics Trap | Network Monitoring | Legacy Systems | Event Collection | Historical implementation. |
| 413 | TCP | SMSP | Simple Messaging | Enterprise | Internal Messaging | Restrict exposure. |
| 414 | TCP | InfoSeek | Information Service | Research Systems | Data Access | Rarely encountered. |
| 415 | TCP | BNET | Business Network | Enterprise | Internal Services | Vendor specific. |
| 416 | TCP | Silverplatter | Database Retrieval | Libraries | Information Search | Internal use. |
| 417 | TCP | Onmux | Multiplexing Service | Enterprise | Communications | Monitor service activity. |
| 418 | TCP | Hyper-G | Hypermedia Platform | Legacy Systems | Information Services | Historical protocol. |
| 419 | TCP | ARIEL | Document Delivery | Libraries | Digital Documents | Restrict trusted users. |
| 420 | TCP | SMPTE | Media Synchronization | Broadcasting | Video Production | Specialized infrastructure. |

---

# Port Spotlight

## Port 404 — Novell Directory Services (NDS)

Novell Directory Services (later eDirectory) was one of the earliest enterprise directory platforms and influenced many modern identity management systems.

Typical Components

- Users
- Groups
- Organizational Units
- Printers
- Servers
- Policies

Architecture

```text
Administrator

      │

Authentication

      ▼

NDS Server

      │

Directory Database

      │

Enterprise Resources
```

Security Recommendations

- Restrict directory access.
- Enable encrypted authentication.
- Audit administrative operations.
- Remove obsolete directory servers.

---

## Port 407 — Timbuktu Remote Control

Timbuktu was a popular remote administration application before RDP and modern remote support platforms became widespread.

Typical Workflow

```text
Administrator

      │

Remote Session

      ▼

Client Computer

      │

Desktop

Keyboard

Mouse
```

Common Features

- Remote desktop
- File transfer
- Chat
- Remote control

Security Risks

- Weak authentication
- Legacy encryption
- Unauthorized remote access

Recommendation

Replace legacy remote administration software with actively supported solutions.

---

## Port 410 — Remote Debugging

Remote debugging services allow developers to troubleshoot applications over the network.

Typical Deployment

```text
Developer

     │

Debug Session

     ▼

Application Server

     │

Breakpoints

Memory

Variables
```

Security Risks

- Remote code execution
- Information disclosure
- Unauthorized application control

Security Recommendations

- Never expose debugging ports publicly.
- Disable debugging in production.
- Restrict developer access.

---

## Port 420 — SMPTE

SMPTE-related services may appear in professional media production environments.

Common Uses

- Television broadcasting
- Film production
- Audio synchronization
- Video synchronization

Typical Environment

```text
Video Server

      │

Synchronization

      ▼

Production Equipment

      │

Broadcast Network
```

Security Recommendations

- Isolate media production networks.
- Restrict administrative interfaces.
- Monitor synchronization services.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 404 | Novell eDirectory |
| 407 | Legacy Remote Desktop |
| 410 | Remote Debugging |
| 420 | Broadcast Infrastructure |

---

# Blue Team Perspective

Recommended Actions

- Remove unsupported directory services.
- Replace legacy remote access software.
- Disable debugging on production servers.
- Isolate broadcast infrastructure.
- Monitor privileged administrative activity.
- Review firewall rules regularly.

---

# Red Team Perspective

Interesting Targets

### Port 404

Possible Findings

- Legacy enterprise directory
- User accounts
- Authentication infrastructure

### Port 407

Possible Findings

- Remote administration software
- Desktop access
- File transfer capability

### Port 410

Possible Findings

- Development environments
- Debug-enabled applications
- Potential code execution opportunities

Useful Commands

```bash
nmap -sV -p404,407,410,420 target
```

```bash
nmap -A -p404,407 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p401-420 target
```

Version Detection

```bash
nmap -sV -p404,407,410,420 target
```

Default Scripts

```bash
nmap -sC -p401-420 target
```

Aggressive Scan

```bash
nmap -A -p401-420 target
```

---

# Summary

Ports **401–420** include legacy directory services, remote administration tools, development-related services, and media synchronization platforms. Although many protocols in this range are no longer common in modern enterprise environments, identifying services such as **Novell Directory Services (404)**, **Timbuktu Remote Control (407)**, and **Remote Debugging (410)** can reveal legacy infrastructure, development systems, or forgotten administrative interfaces that deserve closer security inspection.

---

# Ports 421–440

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 421 | TCP | ARDP | Asynchronous Reliable Delivery Protocol | Legacy Systems | Reliable Transport | Historical protocol. |
| 422 | TCP | ARDP | Reliable Delivery Service | Enterprise | Data Transfer | Rarely encountered. |
| 423 | TCP | OPC Job Start | Industrial Automation | OPC Servers | Manufacturing | Restrict industrial networks. |
| 424 | TCP | OPC Job Track | Industrial Automation | OPC Systems | Process Monitoring | Internal infrastructure only. |
| 425 | TCP | ICAD | Computer-Aided Design | Engineering Software | CAD Collaboration | Protect engineering assets. |
| 426 | TCP | Smartsdp | Smart Device Protocol | Embedded Systems | Device Management | Restrict management access. |
| 427 | TCP/UDP | SLP | Service Location Protocol | OpenSLP, VMware ESXi | Service Discovery | Can expose internal services. |
| 428 | TCP | OMS | Object Management Service | Enterprise Middleware | Distributed Systems | Vendor-specific deployment. |
| 429 | TCP | IPCP | Interprocess Communication | Enterprise Applications | IPC | Internal only. |
| 430 | TCP | Server Location | Discovery Service | Vendor Software | Service Discovery | Restrict network visibility. |
| 431 | TCP | Enterprise Messaging | Messaging Service | Various | Internal Communication | Monitor message traffic. |
| 432 | TCP | Remote Database | Database Gateway | Enterprise DB | Data Access | Restrict database exposure. |
| 433 | TCP | NNSP | Network News Service | Legacy Platforms | Information Distribution | Historical implementation. |
| 434 | TCP | Mobile IP Agent | Mobile Networking | Cisco, Juniper | Mobility Services | Secure mobility infrastructure. |
| 435 | TCP | Mobile IP Foreign Agent | Mobile IP | Network Devices | Mobility | Restrict administrative access. |
| 436 | TCP | Mobile IP Home Agent | Mobile IP | Enterprise Networks | Mobility | Monitor authentication. |
| 437 | TCP | PDS | Personal Data Service | Vendor Software | Synchronization | Vendor-specific. |
| 438 | TCP | ODS | Object Directory Service | Enterprise Platforms | Directory Services | Restrict trusted hosts. |
| 439 | TCP | NCL | Network Control Layer | Enterprise | Infrastructure | Internal management only. |
| 440 | TCP | SGCP | Simple Gateway Control Protocol | VoIP Systems | Media Gateway Control | Replace with modern protocols where possible. |

---

# Port Spotlight

## Port 427 — Service Location Protocol (SLP)

Service Location Protocol (SLP) enables devices on a local network to automatically discover available services without requiring manual configuration.

SLP is widely used in enterprise environments and virtualization platforms.

Common Software

- OpenSLP
- VMware ESXi
- Hewlett Packard Enterprise
- Network Appliances
- Enterprise Storage

Typical Architecture

```text
Client

   │

Service Request

   ▼

SLP Directory Agent

   │

Registered Services

   ├── Printer

   ├── Storage

   ├── Hypervisor

   └── Database
```

Example Scan

```bash
nmap -sU -p427 target
```

Useful NSE Scripts

```bash
nmap --script=slp-info -p427 target
```

Security Risks

- Information disclosure
- Service enumeration
- Internal infrastructure discovery
- VMware environment identification

Security Recommendations

- Disable SLP if unnecessary.
- Restrict SLP to internal networks.
- Patch vulnerable implementations.
- Monitor unexpected service advertisements.

---

## Ports 434–436 — Mobile IP

Mobile IP allows devices to maintain IP connectivity while moving between different networks.

Typical Workflow

```text
Mobile Device

      │

Roaming

      ▼

Foreign Agent

      │

Tunnel

      ▼

Home Agent

      │

Home Network
```

Common Environments

- Enterprise wireless networks
- Carrier infrastructure
- Mobile research networks

Security Recommendations

- Require authenticated tunnels.
- Monitor roaming events.
- Restrict mobility agents.
- Encrypt management traffic.

---

## Port 440 — Simple Gateway Control Protocol (SGCP)

SGCP was an early protocol for controlling VoIP gateways before MGCP became the preferred standard.

Typical Deployment

```text
Call Controller

        │

Gateway Commands

        ▼

Voice Gateway

        │

PSTN

VoIP Phones
```

Common Uses

- Legacy VoIP
- Telecom gateways
- PBX systems

Security Recommendations

- Replace legacy gateway protocols.
- Restrict gateway management.
- Monitor call control traffic.
- Segment voice networks.

---

## Port 423–424 — OPC Industrial Services

Open Platform Communications (OPC) is widely deployed in industrial control systems (ICS) and SCADA environments.

Typical Environment

```text
Operator Workstation

        │

OPC Server

        │

PLC

Sensors

Industrial Equipment
```

Common Industries

- Manufacturing
- Oil & Gas
- Energy
- Water Treatment
- Chemical Processing

Security Recommendations

- Isolate OT networks.
- Prevent direct Internet access.
- Monitor industrial communications.
- Apply vendor security updates.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 423–424 | Industrial Control Systems |
| 427 | VMware / OpenSLP |
| 434–436 | Mobile IP Infrastructure |
| 440 | Legacy VoIP Gateway |

---

# Blue Team Perspective

Recommended Actions

- Disable unused SLP services.
- Isolate industrial control systems.
- Protect Mobile IP infrastructure.
- Segment VoIP environments.
- Restrict service discovery protocols.
- Monitor device advertisements.

---

# Red Team Perspective

Interesting Targets

### Port 427

Possible Findings

- VMware ESXi Hosts
- Storage Appliances
- Enterprise Services
- Internal Network Inventory

### Ports 423–424

Possible Findings

- ICS infrastructure
- SCADA servers
- PLC management systems

### Port 440

Possible Findings

- VoIP gateways
- Legacy PBX
- Telecom equipment

Useful Commands

```bash
nmap -sV -p423,424,427,440 target
```

```bash
nmap -sU -p427 target
```

```bash
nmap --script=slp-info -p427 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p421-440 target
```

UDP Scan

```bash
nmap -sU -p427 target
```

Version Detection

```bash
nmap -sV -p423,424,427,440 target
```

Aggressive Scan

```bash
nmap -A -p421-440 target
```

---

# Summary

Ports **421–440** introduce enterprise service discovery, industrial automation, Mobile IP infrastructure, and legacy VoIP gateway protocols. Among them, **Port 427 (SLP)** is particularly important because it frequently appears on **VMware ESXi hosts, storage appliances, printers, and enterprise devices**, making it a valuable source of reconnaissance information. Ports **423–424** also deserve attention in OT environments, where they may indicate the presence of industrial control systems and SCADA infrastructure.

---

# Ports 441–460

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 441 | TCP | NetWare Core Protocol | Novell NetWare | Legacy Enterprise | File & Print Services | Legacy infrastructure. |
| 442 | TCP | CVC Host | Card Verification | Financial Systems | Payment Processing | Restrict external access. |
| 443 | TCP | HTTPS | Hypertext Transfer Protocol Secure | Apache, Nginx, IIS, Caddy | Secure Web Services | One of the most critical Internet ports. |
| 444 | TCP | SNPP | Simple Network Paging Protocol | Paging Servers | Notification Systems | Historical deployment. |
| 445 | TCP | Microsoft-DS (SMB) | Server Message Block | Windows Server, Samba | File Sharing & Active Directory | High-value target for attackers. |
| 446 | TCP | DDM-RDB | IBM Distributed Database | IBM DB2 | Database Access | Restrict trusted hosts. |
| 447 | TCP | DDM-RDB | IBM Database Service | IBM Systems | Enterprise Databases | Internal deployment. |
| 448 | TCP | DDM-SSL | Secure IBM Database | IBM DB2 | Secure Database Access | Require encrypted sessions. |
| 449 | TCP | AS Server Mapper | AppleShare | Apple Systems | Resource Discovery | Legacy protocol. |
| 450 | TCP | TACACS | Terminal Access Controller Access-Control System | Cisco | Network Device Authentication | Prefer TACACS+ where supported. |
| 451 | TCP | Cray Network | Supercomputer Services | Cray Systems | HPC | Specialized infrastructure. |
| 452 | TCP | DeviceShare | Device Sharing | Vendor Software | Peripheral Sharing | Restrict management access. |
| 453 | TCP | CreativeServer | Multimedia Services | Creative Labs | Audio Services | Vendor-specific. |
| 454 | TCP | World Wide Web Service | Streaming Control | RTSP Implementations | Media Streaming | Verify exposed services. |
| 455 | TCP | Apple QuickTime | Media Streaming | QuickTime Streaming Server | Video Streaming | Keep updated. |
| 456 | TCP | Message Service | Messaging | Enterprise Software | Internal Communication | Internal use only. |
| 457 | TCP | Application Gateway | Enterprise Gateway | Vendor Platforms | Middleware | Restrict privileged access. |
| 458 | TCP | Apple QuickTime | Streaming Management | Apple | Multimedia | Historical deployment. |
| 459 | TCP | AMPR-RCMD | Amateur Packet Radio | Amateur Radio Networks | Remote Commands | Rarely encountered. |
| 460 | TCP | SKRONK | Vendor Service | Various | Enterprise | Verify service identity. |

---

# Port Spotlight

## Port 443 — HTTPS

HTTPS is the secure version of HTTP and is one of the most important protocols on the Internet.

Nearly every modern website, REST API, cloud platform, and enterprise web application relies on HTTPS.

Common Software

- Apache HTTP Server
- Nginx
- Microsoft IIS
- Caddy
- Envoy
- HAProxy
- Traefik

Typical Architecture

```text
Web Browser

      │

TLS Handshake

      ▼

HTTPS Server

      │

Encrypted HTTP

      ▼

Web Application

      │

Database
```

Common Uses

- Secure websites
- REST APIs
- Authentication portals
- Banking applications
- Cloud platforms
- SaaS applications

Example Scan

```bash
nmap -sV -p443 target
```

SSL Enumeration

```bash
nmap --script ssl-cert target -p443
```

```bash
nmap --script ssl-enum-ciphers target -p443
```

```bash
nmap --script http-title,http-headers target -p443
```

Security Recommendations

- Support TLS 1.2 or TLS 1.3.
- Disable weak ciphers.
- Enable HSTS.
- Use trusted certificates.
- Monitor certificate expiration.

---

## Port 445 — SMB (Microsoft-DS)

Port 445 is one of the highest-value targets during Windows network reconnaissance.

It supports:

- SMB File Sharing
- Active Directory communication
- Group Policy
- Remote Administration
- Printer Sharing

Typical Architecture

```text
Windows Client

      │

SMB

      ▼

Windows Server

      │

Shared Folders

Printers

Domain Services
```

Common Software

- Microsoft Windows
- Samba
- NAS Devices
- Domain Controllers

Example Scan

```bash
nmap -sV -p445 target
```

Useful NSE Scripts

```bash
nmap --script smb-os-discovery target
```

```bash
nmap --script smb-enum-shares target
```

```bash
nmap --script smb-protocols target
```

```bash
nmap --script smb-security-mode target
```

Security Risks

- Anonymous shares
- SMBv1 vulnerabilities
- Weak permissions
- Lateral movement
- Ransomware propagation

Security Recommendations

- Disable SMBv1.
- Restrict anonymous access.
- Enable SMB signing where appropriate.
- Apply Microsoft security updates.
- Audit shared folders regularly.

---

## Port 450 — TACACS

TACACS is commonly used to authenticate administrators accessing network infrastructure devices.

Typical Environment

```text
Network Administrator

        │

Authentication

        ▼

TACACS Server

        │

Router

Switch

Firewall
```

Common Vendors

- Cisco
- Juniper
- Arista
- Extreme Networks

Security Recommendations

- Use TACACS+ when available.
- Require MFA for administrators.
- Centralize authentication logs.
- Restrict management networks.

---

## Ports 454–455 — Streaming Services

These ports are commonly associated with RTSP and media streaming platforms.

Typical Deployment

```text
Media Client

      │

RTSP Control

      ▼

Streaming Server

      │

Video Stream

      ▼

Viewer
```

Common Uses

- IP Cameras
- Media Servers
- Surveillance Systems
- Live Broadcasting

Security Recommendations

- Require authentication.
- Disable anonymous streams.
- Encrypt management traffic.
- Monitor streaming sessions.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 443 | HTTPS Web Server |
| 445 | Windows SMB / Active Directory |
| 450 | Network Authentication Server |
| 454–455 | Streaming Media Services |

---

# Blue Team Perspective

Recommended Actions

- Enforce modern TLS configurations.
- Disable SMBv1.
- Restrict SMB to trusted networks.
- Harden TACACS infrastructure.
- Protect media streaming servers.
- Continuously monitor certificate health.

---

# Red Team Perspective

Interesting Targets

### Port 443

Possible Findings

- Web applications
- APIs
- Authentication portals
- Reverse proxies
- Cloud services

Useful Enumeration

```bash
nmap --script ssl-cert,ssl-enum-ciphers,http-title -p443 target
```

---

### Port 445

Possible Findings

- Active Directory
- File Shares
- Domain Controllers
- NAS Devices
- Windows Servers

Useful Enumeration

```bash
nmap --script smb-os-discovery,smb-enum-shares,smb-security-mode -p445 target
```

---

### Port 450

Possible Findings

- AAA infrastructure
- Network authentication
- Administrative services

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p441-460 target
```

Version Detection

```bash
nmap -sV -p443,445,450,454 target
```

SMB Enumeration

```bash
nmap --script smb-os-discovery,smb-enum-shares -p445 target
```

HTTPS Analysis

```bash
nmap --script ssl-cert,ssl-enum-ciphers -p443 target
```

Aggressive Scan

```bash
nmap -A -p441-460 target
```

---

# Summary

Ports **441–460** contain some of the most valuable services encountered during enterprise network assessments. **Port 443 (HTTPS)** serves as the foundation of secure web communication, while **Port 445 (SMB)** is one of the primary targets in Windows environments due to its role in file sharing, authentication, and Active Directory operations. Ports such as **450 (TACACS)** and **454–455 (Streaming Services)** further reveal network infrastructure and media systems that may require additional security attention.

---

# Ports 461–480

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 461 | TCP | PKIX TimeStamp | Trusted Timestamp Service | PKI Platforms | Certificate Services | Protect CA infrastructure. |
| 462 | TCP | Digital Certificate Service | Certificate Validation | Enterprise PKI | Identity Verification | Restrict administrative access. |
| 463 | TCP | SGS Gateway | Gateway Service | Vendor Software | Enterprise Networks | Internal deployment. |
| 464 | TCP/UDP | Kerberos Password Change | Kerberos Administration | Microsoft Active Directory, MIT Kerberos | Password Management | Critical authentication service. |
| 465 | TCP | SMTPS | Secure SMTP | Postfix, Exchange, Exim | Secure Email Delivery | Use TLS and strong authentication. |
| 466 | TCP | Digital Messaging | Enterprise Messaging | Vendor Platforms | Internal Communication | Restrict external exposure. |
| 467 | TCP | Cisco IPSLA | Cisco Devices | Network Monitoring | Performance Measurement | Internal management only. |
| 468 | TCP | Photuris | Key Management Protocol | Legacy VPN Systems | Secure Key Exchange | Historical protocol. |
| 469 | TCP | RCP | Remote Communication | Enterprise Software | Remote Administration | Verify implementation. |
| 470 | TCP | SCX Proxy | Enterprise Proxy | Vendor Software | Middleware | Restrict trusted clients. |
| 471 | TCP | Mondex | Electronic Payment | Banking Systems | Financial Transactions | Secure payment infrastructure. |
| 472 | TCP | LJK Login | Vendor Authentication | Enterprise | Authentication | Internal use only. |
| 473 | TCP | Hybrid POP | Messaging Service | Mail Platforms | Email Retrieval | Legacy deployment. |
| 474 | TCP | ACI | Application Control | Enterprise | Middleware | Restrict privileged access. |
| 475 | TCP | TCPNETHASPSRV | License Manager | Sentinel HASP | Software Licensing | Restrict access. |
| 476 | TCP | PnP | Plug-and-Play Service | Embedded Devices | Device Discovery | Monitor unauthorized devices. |
| 477 | TCP | NCP | NetWare Core Protocol | Novell | File Services | Legacy infrastructure. |
| 478 | TCP | AAKU | Vendor Service | Enterprise | Internal Systems | Rarely encountered. |
| 479 | TCP | TSP | Telephony Service | PBX Platforms | Voice Infrastructure | Restrict management traffic. |
| 480 | TCP | IFSF | Fuel Station Protocol | Fuel Management Systems | Industrial Automation | Segment operational technology networks. |

---

# Port Spotlight

## Port 464 — Kerberos Password Change

Port **464** is used by Kerberos for password change operations and password set requests.

It is commonly found in:

- Microsoft Active Directory
- Windows Domain Controllers
- MIT Kerberos
- Heimdal Kerberos

Typical Architecture

```text
User

 │

Password Change Request

 ▼

Domain Controller

 │

Kerberos Service

 │

Password Updated
```

Example Scan

```bash
nmap -sV -p464 target
```

Security Recommendations

- Restrict access to trusted networks.
- Require strong password policies.
- Enable account lockout policies.
- Monitor password reset events.

---

## Port 465 — SMTPS

SMTPS provides encrypted email transport using SSL/TLS.

Although modern email submission commonly uses **Port 587**, many servers continue supporting SMTPS on Port 465.

Common Software

- Microsoft Exchange
- Postfix
- Exim
- Sendmail
- Haraka

Typical Workflow

```text
Mail Client

      │

TLS Connection

      ▼

SMTP Server

      │

Mail Queue

      ▼

Destination Server
```

Example Scan

```bash
nmap -sV -p465 target
```

Useful NSE Scripts

```bash
nmap --script ssl-cert -p465 target
```

```bash
nmap --script smtp-commands -p465 target
```

```bash
nmap --script smtp-enum-users -p465 target
```

Security Recommendations

- Require SMTP AUTH.
- Disable weak TLS versions.
- Enable SPF, DKIM, and DMARC.
- Monitor mail relay attempts.

---

## Port 475 — Sentinel HASP License Manager

Sentinel HASP provides centralized software license management for commercial applications.

Typical Deployment

```text
Engineering Software

        │

License Request

        ▼

License Server

        │

License Validation

        ▼

Application Starts
```

Common Software

- Sentinel HASP
- Thales Sentinel
- CAD Applications
- Industrial Software

Security Recommendations

- Restrict license server access.
- Monitor license usage.
- Apply vendor updates.
- Protect administrative credentials.

---

## Port 480 — IFSF Fuel Station Protocol

IFSF is widely used within fuel stations and petroleum retail environments.

Typical Architecture

```text
Fuel Pump

     │

IFSF Network

     ▼

Station Controller

     │

Payment Terminal

     ▼

Back Office System
```

Common Environments

- Gas Stations
- Fuel Terminals
- Petroleum Companies
- Retail Automation

Security Recommendations

- Isolate fuel management networks.
- Restrict remote access.
- Encrypt management traffic.
- Monitor operational technology assets.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 464 | Kerberos Password Service |
| 465 | Secure SMTP |
| 475 | Enterprise License Server |
| 480 | Fuel Station Infrastructure |

---

# Blue Team Perspective

Recommended Actions

- Monitor Kerberos password changes.
- Secure mail servers with modern TLS.
- Protect license management systems.
- Segment operational technology environments.
- Audit authentication logs.
- Restrict administrative interfaces.

---

# Red Team Perspective

Interesting Targets

### Port 464

Possible Findings

- Active Directory
- Domain Controllers
- Kerberos Infrastructure

### Port 465

Possible Findings

- Corporate Mail Server
- SMTP Gateway
- Exchange Server

Useful Enumeration

```bash
nmap --script smtp-commands,smtp-enum-users -p465 target
```

---

### Port 475

Possible Findings

- Enterprise licensing servers
- Engineering departments
- Commercial software inventory

---

### Port 480

Possible Findings

- Industrial automation
- Fuel station management
- Operational Technology (OT)

Enumeration Commands

```bash
nmap -sV -p464,465,475,480 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p461-480 target
```

Version Detection

```bash
nmap -sV -p464,465,475,480 target
```

SMTP Enumeration

```bash
nmap --script smtp-commands,smtp-enum-users -p465 target
```

Aggressive Scan

```bash
nmap -A -p461-480 target
```

---

# Summary

Ports **461–480** include enterprise authentication services, secure email protocols, software licensing platforms, and operational technology (OT) systems. **Port 464 (Kerberos Password Change)** and **Port 465 (SMTPS)** are especially important in Windows domains and enterprise messaging infrastructures, while ports such as **475** and **480** often reveal engineering environments and industrial automation systems during reconnaissance.

---

# Ports 481–500

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 481 | TCP | Ph Service | CCSO Name Service | University Systems | Directory Lookup | Legacy protocol. |
| 482 | TCP | SFS | Secure File System | Distributed Storage | File Services | Restrict access. |
| 483 | TCP | OPSEC | Check Point OPSEC | Check Point Firewalls | Security Management | Management only. |
| 484 | TCP | OPC UA TCP | OPC Unified Architecture | Kepware, Ignition, Siemens | Industrial Automation | High-value OT service. |
| 485 | TCP | IPCS | Interprocess Communication | Enterprise Middleware | Internal Applications | Vendor-specific. |
| 486 | TCP | DPM | Distributed Process Manager | Enterprise Software | Automation | Restrict privileged users. |
| 487 | TCP | SAFT | Secure Automation File Transfer | Industrial Systems | File Exchange | Encrypt communications. |
| 488 | TCP | GSS HTTP | Generic Security Service | Enterprise Platforms | Authentication | Protect service accounts. |
| 489 | TCP | Nest Protocol | Embedded Devices | IoT Vendors | Device Management | Restrict exposure. |
| 490 | TCP | Ticf-1 | Vendor Service | Enterprise | Internal Applications | Rarely encountered. |
| 491 | TCP | GoLogin | Remote Authentication | Vendor Software | Remote Access | Secure authentication. |
| 492 | TCP | TICF-2 | Enterprise Service | Vendor Specific | Internal Systems | Verify implementation. |
| 493 | TCP | LICP | License Protocol | Software Vendors | Licensing | Restrict access. |
| 494 | TCP | Retrospect Backup | Retrospect | Backup Infrastructure | Backup Management | Protect repositories. |
| 495 | TCP | PIM-RP-DISC | PIM Rendezvous Discovery | Routers | Multicast Networking | Internal routing only. |
| 496 | TCP | Pim-RP-Mapping | Multicast Mapping | Cisco, Juniper | Network Routing | Restrict management. |
| 497 | TCP | Dantz | Backup Service | Retrospect | Enterprise Backup | Secure backup servers. |
| 498 | TCP | SIAM | Secure Identity Service | Enterprise IAM | Authentication | Protect identity systems. |
| 499 | TCP | ISO ILL | Interlibrary Loan | Library Systems | Document Exchange | Rarely Internet-facing. |
| 500 | TCP/UDP | ISAKMP | Internet Security Association and Key Management Protocol | IPsec, StrongSwan, Cisco ASA, Palo Alto | VPN Key Exchange | Critical VPN infrastructure. |

---

# Port Spotlight

## Port 484 — OPC UA

OPC Unified Architecture (OPC UA) is the modern successor to classic OPC and is one of the most important protocols used in Industrial Control Systems (ICS).

Unlike classic OPC, OPC UA provides:

- Platform independence
- Encryption
- Authentication
- Rich data modeling
- Secure industrial communication

Common Vendors

- Siemens
- Rockwell Automation
- Schneider Electric
- Beckhoff
- Kepware
- Ignition
- ABB

Typical Architecture

```text
SCADA

   │

OPC UA Client

   │

Secure Channel

   ▼

OPC UA Server

   │

PLC

Robots

Sensors

Industrial Equipment
```

Example Scan

```bash
nmap -sV -p484 target
```

Security Recommendations

- Enable certificate-based authentication.
- Disable anonymous access.
- Segment OT networks.
- Monitor industrial communications.
- Keep OPC UA servers updated.

---

## Port 494 / 497 — Retrospect Backup

Retrospect is a backup and disaster recovery platform.

Typical Environment

```text
Clients

   │

Backup Agent

   ▼

Backup Server

   │

Storage Repository

   ▼

Recovery
```

Common Uses

- Enterprise backup
- Disaster recovery
- Endpoint backup
- Server backup

Security Recommendations

- Encrypt backup storage.
- Require MFA for administrators.
- Protect backup repositories from ransomware.
- Test recovery procedures regularly.

---

## Port 500 — ISAKMP / IKE

Port **500** is one of the most important VPN-related ports on modern networks.

ISAKMP (Internet Security Association and Key Management Protocol) is used by IPsec to negotiate secure VPN tunnels.

Common Software

- StrongSwan
- Libreswan
- Cisco ASA
- Cisco IOS
- Palo Alto PAN-OS
- FortiGate
- Juniper SRX

Typical VPN Workflow

```text
VPN Client

      │

IKE Negotiation

      ▼

VPN Gateway

      │

Authentication

      ▼

IPsec Tunnel

      │

Encrypted Traffic
```

Example Scan

```bash
nmap -sU -p500 target
```

Useful NSE Scripts

```bash
nmap --script ike-version -p500 target
```

Security Recommendations

- Prefer IKEv2.
- Disable weak cryptographic algorithms.
- Require certificate-based authentication.
- Rotate VPN credentials regularly.
- Monitor failed VPN negotiations.

---

## Port 483 — Check Point OPSEC

OPSEC allows Check Point security products to exchange security information with management servers.

Typical Deployment

```text
Management Server

        │

OPSEC

        ▼

Firewall

Gateway

IPS

Log Server
```

Security Recommendations

- Restrict management interfaces.
- Encrypt management communications.
- Audit administrator activity.
- Keep security appliances updated.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 483 | Check Point Security Infrastructure |
| 484 | Industrial Control Systems (OPC UA) |
| 494 / 497 | Enterprise Backup Platform |
| 500 | IPsec VPN Gateway |

---

# Blue Team Perspective

Recommended Actions

- Protect VPN gateways.
- Secure industrial automation systems.
- Encrypt backup repositories.
- Restrict firewall management interfaces.
- Rotate VPN credentials.
- Monitor certificate usage.

---

# Red Team Perspective

Interesting Targets

### Port 484

Possible Findings

- SCADA servers
- PLC infrastructure
- Industrial automation
- Manufacturing environment

### Port 500

Possible Findings

- VPN concentrators
- Remote access gateways
- Branch office connectivity

Useful Enumeration

```bash
nmap --script ike-version -p500 target
```

```bash
nmap -sU -p500 target
```

### Ports 494 / 497

Possible Findings

- Backup servers
- Recovery infrastructure
- Critical enterprise data

Enumeration Commands

```bash
nmap -sV -p483,484,494,497,500 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p481-500 target
```

Version Detection

```bash
nmap -sV -p483,484,494,497 target
```

UDP VPN Scan

```bash
nmap -sU -p500 target
```

IKE Enumeration

```bash
nmap --script ike-version -p500 target
```

Aggressive Scan

```bash
nmap -A -p481-500 target
```

---

# Summary

Ports **481–500** introduce enterprise backup platforms, industrial automation services, security management frameworks, and VPN infrastructure. Among them, **Port 500 (ISAKMP/IKE)** is one of the most significant ports encountered during penetration testing because it identifies IPsec VPN gateways and remote access infrastructure. Likewise, **Port 484 (OPC UA)** is a key indicator of industrial control systems, making it particularly valuable during OT and SCADA assessments.

---

# Ports 501–520

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 501 | TCP | STMF | Stream Management | Enterprise Systems | Data Streaming | Vendor-specific implementation. |
| 502 | TCP | Modbus | Industrial Control Protocol | Schneider Electric, Siemens, ABB | SCADA / PLC Communication | Critical OT protocol with no built-in authentication. |
| 503 | TCP | Intrinsa | Intrusion Detection | Security Appliances | Security Monitoring | Restrict management access. |
| 504 | TCP | Citadel | Authentication Service | Legacy Systems | Authentication | Historical deployment. |
| 505 | TCP | Mailbox-LM | Mailbox Service | Enterprise Messaging | Email Systems | Internal use only. |
| 506 | TCP | Ohimsrv | Healthcare Service | Medical Systems | Clinical Applications | Protect sensitive data. |
| 507 | TCP | CRS | Content Replication | Enterprise Platforms | Data Synchronization | Restrict trusted hosts. |
| 508 | TCP | Xvttp | Vendor Protocol | Various | Internal Applications | Verify implementation. |
| 509 | TCP | SNARE | Security Monitoring | Snare Server | Log Collection | Protect centralized logging. |
| 510 | TCP | FirstClass | Collaboration Platform | OpenText FirstClass | Messaging | Legacy collaboration software. |
| 511 | TCP | PassGo | Authentication | Enterprise Software | Login Services | Monitor authentication attempts. |
| 512 | TCP | exec | Berkeley Remote Execution | UNIX | Remote Command Execution | Insecure legacy protocol. |
| 513 | TCP | login | Berkeley Remote Login | UNIX | Remote Login | Uses plaintext authentication. |
| 514 | TCP | shell / syslog | Remote Shell / Syslog | UNIX, rsyslog, syslog-ng | Logging & Administration | Extremely important enterprise port. |
| 515 | TCP | LPD | Line Printer Daemon | CUPS, UNIX Printing | Network Printing | Restrict printer access. |
| 516 | TCP | Videotex | Legacy Information Service | Historical Systems | Information Retrieval | Rarely encountered. |
| 517 | TCP | Talk | UNIX Talk | BSD Systems | Chat | Historical protocol. |
| 518 | TCP | NTalk | Network Talk | UNIX | Messaging | Legacy service. |
| 519 | TCP | UUCP | UNIX-to-UNIX Copy | UNIX Systems | File Transfer | Obsolete. |
| 520 | TCP/UDP | RIP | Routing Information Protocol | Cisco IOS, FRRouting, Quagga | Dynamic Routing | Restrict routing updates. |

---

# Port Spotlight

## Port 502 — Modbus

Modbus is one of the most widely used industrial communication protocols in Operational Technology (OT) environments.

Unlike many modern protocols, Modbus does **not** provide authentication or encryption.

Common Industries

- Manufacturing
- Power Plants
- Oil & Gas
- Water Treatment
- Chemical Processing
- Smart Buildings

Typical Architecture

```text
SCADA Server

      │

Modbus TCP

      ▼

PLC

      │

Sensors

Actuators

Motors
```

Example Scan

```bash
nmap -sV -p502 target
```

Useful NSE Scripts

```bash
nmap --script modbus-discover -p502 target
```

Security Risks

- No authentication
- Plaintext communication
- Unauthorized PLC control
- Process manipulation

Security Recommendations

- Never expose Modbus to the Internet.
- Segment OT networks.
- Restrict access with firewalls.
- Monitor industrial traffic continuously.

---

## Port 512–514 — Berkeley r-Services

The Berkeley "r-services" were widely used on UNIX systems before SSH became the standard.

Included Services

| Port | Service |
|------:|----------|
| 512 | rexec |
| 513 | rlogin |
| 514 | rsh (TCP) / Syslog (UDP) |

Typical Workflow

```text
Administrator

      │

Remote Login

      ▼

UNIX Server

      │

Command Execution
```

Security Risks

- Plaintext credentials
- Host-based trust
- No encryption
- Easy credential interception

Recommendation

Replace all Berkeley r-services with SSH.

---

## Port 514 — Syslog

UDP Port 514 is the standard port used by Syslog servers for centralized log collection.

Typical Architecture

```text
Firewall

Router

Server

Switch

      │

Syslog Messages

      ▼

Central Syslog Server

      │

SIEM

Monitoring

Alerting
```

Common Software

- rsyslog
- syslog-ng
- Graylog
- Splunk Forwarders
- QRadar

Example Scan

```bash
nmap -sU -p514 target
```

Useful NSE Scripts

```bash
nmap -sU -sV -p514 target
```

Security Recommendations

- Restrict log sources.
- Encrypt logs using TLS where supported.
- Protect centralized logging servers.
- Monitor unexpected log traffic.

---

## Port 520 — Routing Information Protocol (RIP)

RIP is one of the oldest dynamic routing protocols.

Although largely replaced by OSPF and BGP, RIP still appears in:

- Legacy enterprise networks
- Industrial environments
- Small branch offices
- Network laboratories

Architecture

```text
Router A

    │

Routing Updates

    ▼

Router B

    │

Routing Table
```

Example Scan

```bash
nmap -sU -p520 target
```

Security Recommendations

- Disable RIP where unnecessary.
- Authenticate routing updates (RIPv2).
- Restrict routing domains.
- Monitor routing changes.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 502 | Industrial Control System |
| 512–514 | Legacy UNIX Services |
| 514 | Centralized Logging |
| 515 | Network Printer |
| 520 | Dynamic Router |

---

# Blue Team Perspective

Recommended Actions

- Segment industrial control systems.
- Remove legacy Berkeley services.
- Protect centralized logging platforms.
- Restrict printer services.
- Authenticate routing protocols.
- Continuously monitor OT infrastructure.

---

# Red Team Perspective

Interesting Targets

### Port 502

Possible Findings

- PLC devices
- SCADA infrastructure
- Industrial automation
- Critical manufacturing systems

Useful Enumeration

```bash
nmap --script modbus-discover -p502 target
```

---

### Port 514

Possible Findings

- SIEM infrastructure
- Syslog collectors
- Network device inventory
- Enterprise logging systems

---

### Port 520

Possible Findings

- Legacy routers
- Branch office infrastructure
- Dynamic routing domains

Useful Commands

```bash
nmap -sV -p502,514 target
```

```bash
nmap -sU -p514,520 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p501-520 target
```

Version Detection

```bash
nmap -sV -p502,514,515 target
```

UDP Scan

```bash
nmap -sU -p514,520 target
```

Industrial Scan

```bash
nmap --script modbus-discover -p502 target
```

Aggressive Scan

```bash
nmap -A -p501-520 target
```

---

# Summary

Ports **501–520** include several of the most significant services encountered in enterprise and industrial environments. **Port 502 (Modbus)** is a primary indicator of Industrial Control Systems (ICS) and should be treated as highly sensitive due to its lack of built-in security. **Ports 512–514** represent legacy UNIX remote administration services, while **UDP 514 (Syslog)** remains the de facto standard for centralized logging. **Port 520 (RIP)** identifies dynamic routing infrastructure that can reveal valuable information about network topology during reconnaissance.

---

# Ports 521–540

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 521 | TCP | RIPng | Routing Information Protocol Next Generation | Cisco IOS, Juniper | IPv6 Routing | Secure routing advertisements. |
| 522 | TCP | ULP | Ultra Lightweight Protocol | Vendor Software | Embedded Systems | Vendor-specific implementation. |
| 523 | TCP | IBM DB2 | DB2 Administration | IBM DB2 | Database Management | Restrict DBA access. |
| 524 | TCP | NCP | NetWare Core Protocol | Novell NetWare | File Services | Legacy enterprise systems. |
| 525 | TCP | Timed | Time Synchronization | UNIX | Time Services | Prefer modern NTP. |
| 526 | TCP | Tempo | Scheduling Service | Enterprise Applications | Scheduling | Internal service. |
| 527 | TCP | Conference | Conference Control | Collaboration Platforms | Meetings | Historical implementation. |
| 528 | TCP | XCAP | XML Configuration Access | VoIP Platforms | SIP Configuration | Protect provisioning servers. |
| 529 | TCP | IRC Serv | IRC Services | IRC Networks | Chat Infrastructure | Rare on modern networks. |
| 530 | TCP | Courier | RPC Service | Legacy UNIX | Messaging | Verify service identity. |
| 531 | TCP | AIM | Application Integration | Middleware | Enterprise Integration | Restrict privileged access. |
| 532 | TCP | NetNews | News Distribution | Legacy Platforms | Content Distribution | Historical service. |
| 533 | TCP | NetWall | Firewall Management | Security Appliances | Security Administration | Management network only. |
| 534 | TCP | Windream | Document Management | Windream DMS | Enterprise Content | Protect sensitive documents. |
| 535 | TCP | iiop | CORBA IIOP | Java EE, Oracle | Distributed Objects | Internal enterprise service. |
| 536 | TCP | OpenBase | OpenBase Database | OpenBase SQL | Database Systems | Restrict exposure. |
| 537 | TCP | HMMP | HyperMedia Management | Vendor Software | Content Services | Rare deployment. |
| 538 | TCP | GDOMAP | Global Domain Mapping | Enterprise Platforms | Directory Services | Internal infrastructure. |
| 539 | TCP | Apertus LDAP | Directory Service | Legacy LDAP | Identity Services | Secure authentication. |
| 540 | TCP | UUCP | UNIX-to-UNIX Copy | UNIX Systems | File Exchange | Legacy protocol. |

---

# Port Spotlight

## Port 523 — IBM DB2 Administration

Port **523** is commonly associated with IBM DB2 administrative services.

DB2 remains widely deployed in:

- Financial institutions
- Government agencies
- Insurance companies
- Enterprise ERP environments

Typical Architecture

```text
DBA Workstation

       │

DB2 Administration

       ▼

IBM DB2 Server

       │

Enterprise Database

       ▼

Business Applications
```

Example Scan

```bash
nmap -sV -p523 target
```

Security Recommendations

- Restrict administrative interfaces.
- Require encrypted client connections.
- Enforce least privilege.
- Audit DBA activity.

---

## Port 524 — NetWare Core Protocol (NCP)

Although uncommon today, NCP may still appear within older enterprise environments.

Typical Environment

```text
Legacy Client

      │

NCP

      ▼

Novell NetWare

      │

File Server

Print Server
```

Security Risks

- Legacy authentication
- Unsupported software
- Weak encryption
- Outdated operating systems

Security Recommendations

- Replace unsupported systems.
- Restrict legacy network segments.
- Monitor remaining NetWare hosts.

---

## Port 528 — XCAP

XCAP (XML Configuration Access Protocol) allows clients to modify XML-based configuration data stored on SIP servers.

Common Deployments

- IMS Infrastructure
- VoIP Platforms
- SIP Presence Servers
- Unified Communications

Typical Workflow

```text
VoIP Client

      │

HTTPS/XCAP

      ▼

Provisioning Server

      │

Configuration Database

      ▼

SIP Infrastructure
```

Security Recommendations

- Require HTTPS.
- Authenticate all configuration requests.
- Disable anonymous provisioning.
- Audit configuration changes.

---

## Port 535 — IIOP (CORBA)

IIOP (Internet Inter-ORB Protocol) is used by CORBA-based distributed enterprise applications.

Common Platforms

- Oracle WebLogic
- IBM WebSphere
- Java EE Middleware
- Enterprise Banking Applications

Typical Architecture

```text
Application Server

        │

IIOP

        ▼

CORBA Objects

        │

Database

Enterprise Services
```

Example Scan

```bash
nmap -sV -p535 target
```

Security Recommendations

- Restrict internal middleware traffic.
- Disable unused CORBA services.
- Patch application servers regularly.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 523 | IBM DB2 Infrastructure |
| 524 | Novell NetWare |
| 528 | VoIP Provisioning |
| 535 | Java EE / CORBA Middleware |
| 539 | Legacy LDAP Services |

---

# Blue Team Perspective

Recommended Actions

- Harden DB2 administrative services.
- Migrate unsupported NetWare systems.
- Secure VoIP provisioning servers.
- Restrict middleware communications.
- Monitor LDAP authentication events.
- Isolate legacy enterprise platforms.

---

# Red Team Perspective

Interesting Targets

### Port 523

Possible Findings

- IBM DB2 servers
- Enterprise databases
- Financial applications

Useful Enumeration

```bash
nmap -sV -p523 target
```

---

### Port 528

Possible Findings

- SIP provisioning servers
- Unified communications
- Presence infrastructure

---

### Port 535

Possible Findings

- Oracle WebLogic
- IBM WebSphere
- CORBA middleware
- Enterprise Java applications

Enumeration Commands

```bash
nmap -sV -p523,528,535 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p521-540 target
```

Version Detection

```bash
nmap -sV -p523,524,528,535 target
```

Aggressive Scan

```bash
nmap -A -p521-540 target
```

Service Detection

```bash
nmap -sC -sV -p523,528,535 target
```

---

# Summary

Ports **521–540** primarily represent enterprise middleware, legacy networking technologies, database administration, and unified communications. **Port 523 (IBM DB2)** may reveal high-value enterprise databases, while **Port 528 (XCAP)** is closely associated with SIP and VoIP provisioning systems. **Port 535 (IIOP)** frequently indicates Java EE middleware such as Oracle WebLogic or IBM WebSphere, making it an attractive reconnaissance target during enterprise assessments.

---

# Ports 541–560

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 541 | TCP | uucp-rlogin | UUCP Remote Login | Legacy UNIX | Remote Administration | Obsolete; replace with SSH. |
| 542 | TCP | commerce | Commerce Applications | Enterprise Software | E-Commerce | Restrict Internet exposure. |
| 543 | TCP | klogin | Kerberos Login | MIT Kerberos | Secure Remote Login | Strong authentication required. |
| 544 | TCP | kshell | Kerberos Remote Shell | UNIX | Remote Commands | Prefer SSH for modern deployments. |
| 545 | TCP | appleqtcsrvr | Apple QuickTime Streaming | Apple | Media Streaming | Keep patched. |
| 546 | UDP | DHCPv6 Client | DHCPv6 Client Service | Windows, Linux | IPv6 Address Assignment | Local network only. |
| 547 | UDP | DHCPv6 Server | DHCPv6 Server | ISC DHCP, Windows Server | IPv6 Address Distribution | Restrict rogue DHCP servers. |
| 548 | TCP | AFP | Apple Filing Protocol | macOS Server, Netatalk | File Sharing | Secure authentication required. |
| 549 | TCP | IDFP | Integrated Data Facility | Vendor Software | Enterprise Systems | Internal deployment. |
| 550 | TCP | new-rwho | Remote Host Status | UNIX | Host Monitoring | Historical protocol. |
| 551 | TCP | cybercash | Payment Gateway | Financial Systems | Electronic Payments | Legacy financial service. |
| 552 | TCP | deviceshare | Device Sharing | Enterprise Platforms | Hardware Sharing | Restrict management access. |
| 553 | TCP | pirp | Routing Protocol | Network Devices | Routing | Internal infrastructure only. |
| 554 | TCP/UDP | RTSP | Real-Time Streaming Protocol | VLC, Wowza, IP Cameras | Media Streaming | Common on surveillance systems. |
| 555 | TCP | dsf | Distributed Services | Enterprise Middleware | Internal Services | Vendor-specific. |
| 556 | TCP | remotefs | Remote File System | UNIX | File Sharing | Prefer encrypted alternatives. |
| 557 | TCP | openvms-sysipc | OpenVMS IPC | OpenVMS | System Communication | Legacy platform. |
| 558 | TCP | sdnskmp | SDNS Key Management | Government Systems | Cryptographic Services | Restricted environments. |
| 559 | TCP | teedtap | Vendor Service | Enterprise | Internal Applications | Verify service identity. |
| 560 | TCP | rmonitor | Remote Monitoring | Enterprise Monitoring | Performance Monitoring | Restrict monitoring interfaces. |

---

# Port Spotlight

## Port 548 — Apple Filing Protocol (AFP)

AFP is Apple's traditional file-sharing protocol, primarily used before SMB became the default file-sharing protocol in modern macOS versions.

Although SMB has largely replaced AFP, many Apple environments and NAS devices continue supporting it.

Common Software

- macOS Server
- Netatalk
- Synology NAS
- QNAP NAS
- Time Machine Servers

Typical Architecture

```text
Mac Client

     │

AFP

     ▼

File Server

     │

Shared Folders

Backups

Time Machine
```

Example Scan

```bash
nmap -sV -p548 target
```

Useful NSE Scripts

```bash
nmap --script afp-serverinfo -p548 target
```

Security Risks

- Weak authentication
- Guest access
- Legacy AFP implementations
- Information disclosure

Security Recommendations

- Prefer SMB where possible.
- Disable guest access.
- Require strong authentication.
- Restrict AFP to trusted networks.

---

## Ports 546–547 — DHCPv6

DHCPv6 provides automatic IPv6 address assignment and network configuration.

Unlike IPv4 DHCP, DHCPv6 operates alongside IPv6 Neighbor Discovery.

Typical Architecture

```text
Client

   │

DHCPv6 Request

   ▼

DHCPv6 Server

   │

IPv6 Address

DNS Server

Gateway
```

Example Scan

```bash
nmap -sU -p546,547 target
```

Security Risks

- Rogue DHCP servers
- IPv6 misconfiguration
- Address spoofing
- Network disruption

Security Recommendations

- Enable DHCP snooping where supported.
- Monitor unauthorized DHCP advertisements.
- Secure IPv6 infrastructure.
- Restrict administrative access.

---

## Port 554 — RTSP

RTSP (Real-Time Streaming Protocol) controls multimedia streaming sessions.

It is commonly encountered on surveillance cameras, DVRs, NVRs, IPTV systems, and streaming servers.

Common Software

- VLC
- Wowza Streaming Engine
- Hikvision
- Dahua
- Axis Cameras
- GStreamer

Typical Architecture

```text
Viewer

   │

RTSP

   ▼

Camera

Streaming Server

   │

Video Stream

   ▼

Display
```

Example Scan

```bash
nmap -sV -p554 target
```

Useful NSE Scripts

```bash
nmap --script rtsp-url-brute -p554 target
```

Security Risks

- Default credentials
- Anonymous streaming
- Camera exposure
- Sensitive video leakage

Security Recommendations

- Change default passwords.
- Disable anonymous access.
- Restrict RTSP exposure.
- Encrypt management interfaces.

---

## Ports 543–544 — Kerberos Remote Login

These ports support Kerberos-authenticated remote login services.

Typical Deployment

```text
Administrator

      │

Kerberos Authentication

      ▼

Remote UNIX Server

      │

Secure Login

      ▼

Administrative Session
```

Security Recommendations

- Prefer SSH with Kerberos integration.
- Disable legacy remote shell services.
- Monitor authentication logs.
- Require MFA where possible.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 546–547 | IPv6 DHCP Infrastructure |
| 548 | Apple File Sharing |
| 554 | IP Camera / Streaming Server |
| 543–544 | Kerberos Remote Administration |

---

# Blue Team Perspective

Recommended Actions

- Secure DHCPv6 infrastructure.
- Disable unnecessary AFP services.
- Harden RTSP-enabled devices.
- Audit Apple file servers.
- Replace legacy remote login services.
- Monitor streaming activity for unauthorized access.

---

# Red Team Perspective

Interesting Targets

### Port 548

Possible Findings

- macOS Server
- NAS Devices
- Time Machine Backup Servers
- Apple Infrastructure

Useful Enumeration

```bash
nmap --script afp-serverinfo -p548 target
```

---

### Port 554

Possible Findings

- IP Cameras
- DVR/NVR Appliances
- Surveillance Systems
- Streaming Platforms

Useful Enumeration

```bash
nmap --script rtsp-url-brute -p554 target
```

---

### Ports 546–547

Possible Findings

- IPv6-enabled enterprise networks
- DHCP infrastructure
- Network segmentation details

Enumeration Commands

```bash
nmap -sU -p546,547 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p541-560 target
```

Version Detection

```bash
nmap -sV -p548,554 target
```

UDP Scan

```bash
nmap -sU -p546,547 target
```

Streaming Enumeration

```bash
nmap --script rtsp-url-brute -p554 target
```

Aggressive Scan

```bash
nmap -A -p541-560 target
```

---

# Summary

Ports **541–560** include legacy UNIX administration services, IPv6 infrastructure, Apple file-sharing technologies, and multimedia streaming protocols. **Ports 546–547** identify DHCPv6 infrastructure, **Port 548 (AFP)** often reveals Apple ecosystems or NAS devices, and **Port 554 (RTSP)** is one of the most valuable reconnaissance ports for identifying IP cameras, DVR/NVR systems, and media streaming platforms. These services frequently appear in enterprise, surveillance, and mixed-platform environments.

---

# Ports 561–580

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 561 | TCP | monitor | Remote Monitoring | Enterprise Monitoring | Infrastructure Monitoring | Restrict monitoring access. |
| 562 | TCP | chapar | Messaging Service | Legacy Systems | Notifications | Historical deployment. |
| 563 | TCP | NNTPS | Network News Transfer Protocol over SSL | INN, Leafnode | Secure News Distribution | Use TLS certificates. |
| 564 | TCP | 9P (Plan 9 File Protocol) | Distributed File System | Plan 9, Linux v9fs | Virtualization & File Sharing | Restrict exported resources. |
| 565 | TCP | whoami | Identification Service | Vendor Software | Diagnostics | Rarely encountered. |
| 566 | TCP | streettalk | Banyan Directory Service | Banyan VINES | Directory Services | Legacy platform. |
| 567 | TCP | banyan-rpc | Banyan RPC | Banyan VINES | Remote Procedure Calls | Historical protocol. |
| 568 | TCP | ms-shuttle | Microsoft Shuttle | Microsoft | Internal Services | Vendor-specific. |
| 569 | TCP | ms-rome | Microsoft Rome | Microsoft | Internal Communication | Rare deployment. |
| 570 | TCP | meter | Network Metering | Enterprise Software | Usage Statistics | Restrict management access. |
| 571 | TCP | umeter | Usage Meter | Monitoring Platforms | Accounting | Internal use only. |
| 572 | TCP | sonar | Monitoring Service | Enterprise Systems | Network Monitoring | Verify service identity. |
| 573 | TCP | banyan-vip | Banyan VIP | Legacy Enterprise | Authentication | Obsolete service. |
| 574 | TCP | ftp-agent | FTP Management | File Servers | File Administration | Protect administrative interfaces. |
| 575 | TCP | vemmi | VEMMI Multimedia | Multimedia Platforms | Interactive Media | Legacy implementation. |
| 576 | TCP | ipcd | Interprocess Communication Daemon | UNIX | Local Communication | Restrict privileged access. |
| 577 | TCP | vnas | Virtual NAS | Storage Systems | File Storage | Secure shared storage. |
| 578 | TCP | ipdd | IP Device Discovery | Enterprise Networks | Device Discovery | Monitor unexpected responses. |
| 579 | TCP | decbsrv | DEC Backup Service | OpenVMS | Backup Infrastructure | Restrict backup management. |
| 580 | TCP | VNC HTTP | VNC Web Access | RealVNC, TightVNC, UltraVNC | Remote Desktop | Often exposes remote desktop portals. |

---

# Port Spotlight

## Port 580 — VNC over HTTP

Port **580** is commonly used by VNC servers to provide browser-based remote desktop access.

Instead of connecting directly with a VNC client, users access a web interface that launches the remote desktop session.

Common Software

- RealVNC
- TightVNC
- UltraVNC
- TigerVNC

Typical Architecture

```text
Administrator

      │

HTTPS / HTTP

      ▼

VNC Web Server

      │

VNC Session

      ▼

Remote Desktop
```

Example Scan

```bash
nmap -sV -p580 target
```

Useful NSE Scripts

```bash
nmap --script http-title -p580 target
```

```bash
nmap --script http-headers -p580 target
```

Security Risks

- Exposed remote administration
- Weak authentication
- Default credentials
- Information disclosure

Security Recommendations

- Disable web access if unnecessary.
- Require strong passwords.
- Restrict management networks.
- Enable encryption where supported.

---

## Port 563 — NNTPS

NNTPS is the encrypted version of the Network News Transfer Protocol.

Although rarely encountered today, some organizations continue using secure Usenet infrastructures.

Typical Architecture

```text
News Client

      │

TLS

      ▼

NNTPS Server

      │

News Groups

      ▼

Subscribers
```

Security Recommendations

- Use modern TLS versions.
- Disable anonymous posting.
- Monitor authentication logs.

---

## Port 564 — 9P File Protocol

9P is the native file protocol of the Plan 9 operating system.

Today it is most commonly encountered in:

- QEMU
- KVM
- VirtFS
- Linux virtualization environments

Typical Deployment

```text
Virtual Machine

      │

9P

      ▼

Host File System

      │

Shared Directory

      ▼

Guest Access
```

Example Scan

```bash
nmap -sV -p564 target
```

Security Recommendations

- Export only required directories.
- Apply least privilege.
- Restrict host-to-guest sharing.
- Monitor file access.

---

## Port 577 — Virtual NAS

Port 577 may indicate virtualized storage appliances or NAS management services.

Typical Environment

```text
Client

    │

File Access

    ▼

Virtual NAS

    │

Storage Pool

    ▼

Disk Array
```

Common Uses

- Enterprise NAS
- Backup Appliances
- Virtual Storage
- Hyperconverged Infrastructure

Security Recommendations

- Restrict storage management.
- Enable audit logging.
- Encrypt storage traffic.
- Monitor unauthorized access.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 563 | Secure NNTP Server |
| 564 | Virtualization / 9P File Sharing |
| 577 | NAS Infrastructure |
| 580 | VNC Remote Desktop |

---

# Blue Team Perspective

Recommended Actions

- Restrict VNC web interfaces.
- Secure virtualization file sharing.
- Protect NAS management services.
- Remove unused legacy news services.
- Monitor remote desktop access.
- Audit storage permissions regularly.

---

# Red Team Perspective

Interesting Targets

### Port 580

Possible Findings

- Remote desktop portals
- Administrator consoles
- Exposed VNC servers
- Browser-accessible management interfaces

Useful Enumeration

```bash
nmap --script http-title,http-headers -p580 target
```

---

### Port 564

Possible Findings

- KVM virtualization
- Shared host directories
- Hypervisor infrastructure

---

### Port 577

Possible Findings

- Enterprise NAS
- Backup storage
- Shared file repositories

Enumeration Commands

```bash
nmap -sV -p563,564,577,580 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p561-580 target
```

Version Detection

```bash
nmap -sV -p563,564,577,580 target
```

Web Enumeration

```bash
nmap --script http-title,http-headers -p580 target
```

Aggressive Scan

```bash
nmap -A -p561-580 target
```

---

# Summary

Ports **561–580** include legacy messaging services, virtualization file-sharing protocols, storage infrastructure, and browser-based remote desktop services. **Port 580 (VNC over HTTP)** is particularly valuable during reconnaissance because it often exposes web-accessible remote administration interfaces. **Port 564 (9P)** may reveal virtualization platforms such as KVM or QEMU, while **Port 577** can indicate enterprise storage or NAS infrastructure.

---

# Ports 581–600

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 581 | TCP | Bundle Discovery | Bundle Service | Enterprise Systems | Service Discovery | Restrict internal access. |
| 582 | TCP | SCC Security | Security Communication | Enterprise Appliances | Security Infrastructure | Vendor-specific deployment. |
| 583 | TCP | Philips VP | Philips Video Platform | Medical Devices | Video Systems | Restrict management interfaces. |
| 584 | TCP | Key Server | Key Distribution | PKI Platforms | Cryptographic Services | Protect cryptographic keys. |
| 585 | TCP | IMAP4-SSL (Historical) | Secure IMAP | Legacy Mail Servers | Email Retrieval | Modern deployments typically use 993. |
| 586 | TCP | Password Change | Authentication Service | Enterprise Systems | Password Management | Require strong authentication. |
| 587 | TCP | Message Submission | SMTP Submission | Microsoft Exchange, Postfix, Exim | Authenticated Email Submission | Modern email submission standard. |
| 588 | TCP | CAL | Calendar Services | Collaboration Platforms | Scheduling | Restrict authenticated users. |
| 589 | TCP | EYELINK | Eye Tracking Systems | Medical Equipment | Diagnostics | Specialized deployments. |
| 590 | TCP | TNSCML | Oracle Listener Management | Oracle Database | Database Administration | Restrict administrative access. |
| 591 | TCP | FileMaker | FileMaker Database | Claris FileMaker | Business Applications | Limit trusted clients. |
| 592 | TCP | Eudora Set | Eudora Services | Legacy Email | Messaging | Historical protocol. |
| 593 | TCP | HTTP RPC EpMap | Microsoft RPC over HTTP | Windows Server | Remote Procedure Calls | Important Windows infrastructure service. |
| 594 | TCP | TIPC | Transparent Inter-Process Communication | Linux Clusters | Cluster Communication | Internal infrastructure only. |
| 595 | TCP | CAB Protocol | Vendor Service | Enterprise Software | Application Communication | Verify service identity. |
| 596 | TCP | SMSD | Messaging Platform | Enterprise | Notifications | Internal deployment. |
| 597 | TCP | PTCNAMESERVICE | Name Service | Middleware | Service Discovery | Restrict exposure. |
| 598 | TCP | SCO Web Server | Legacy Web Service | SCO UNIX | Web Applications | Keep patched or retire. |
| 599 | TCP | ACP | Application Control Protocol | Enterprise Platforms | Middleware | Vendor-specific. |
| 600 | TCP | IPCServer | Interprocess Communication | Enterprise Applications | Internal Services | Restrict administrative access. |

---

# Port Spotlight

## Port 587 — SMTP Message Submission

Port **587** is the modern standard for authenticated email submission.

Unlike Port 25, which is primarily used for mail transfer between servers, Port 587 is intended for email clients submitting outbound mail.

Common Software

- Microsoft Exchange
- Postfix
- Exim
- Sendmail
- Haraka

Typical Architecture

```text
Mail Client

      │

SMTP AUTH

      ▼

Submission Server

      │

Mail Queue

      ▼

SMTP Relay

      │

Destination Mail Server
```

Example Scan

```bash
nmap -sV -p587 target
```

Useful NSE Scripts

```bash
nmap --script smtp-commands -p587 target
```

```bash
nmap --script smtp-enum-users -p587 target
```

Security Risks

- Weak authentication
- Open relay misconfiguration
- Credential attacks
- Mail abuse

Security Recommendations

- Require SMTP AUTH.
- Enforce TLS encryption.
- Disable open relay.
- Monitor brute-force attempts.

---

## Port 590 — Oracle Listener

Oracle Net Listener accepts incoming connections to Oracle databases.

It is commonly encountered in enterprise environments running Oracle Database.

Typical Architecture

```text
Database Client

      │

Oracle Net

      ▼

Oracle Listener

      │

Oracle Database

      ▼

Enterprise Applications
```

Common Software

- Oracle Database
- Oracle Grid Infrastructure
- Oracle RAC

Example Scan

```bash
nmap -sV -p590 target
```

Security Recommendations

- Restrict listener access.
- Enable listener password protection.
- Apply Oracle Critical Patch Updates.
- Monitor failed connection attempts.

---

## Port 591 — FileMaker Database

FileMaker is a low-code application platform with an integrated database server.

Typical Deployment

```text
FileMaker Client

        │

Database Connection

        ▼

FileMaker Server

        │

Business Database

        ▼

Applications
```

Security Recommendations

- Require strong authentication.
- Encrypt client sessions.
- Restrict database exposure.
- Audit user activity.

---

## Port 593 — Microsoft RPC over HTTP

Port **593** supports Microsoft Remote Procedure Calls transported over HTTP.

This service is frequently associated with:

- Windows Server
- Exchange Server
- Active Directory
- Enterprise Management Tools

Typical Workflow

```text
Windows Client

       │

RPC over HTTP

       ▼

RPC Endpoint Mapper

       │

Windows Services

       ▼

Server Components
```

Example Scan

```bash
nmap -sV -p593 target
```

Useful NSE Scripts

```bash
nmap --script msrpc-enum -p593 target
```

Security Recommendations

- Restrict RPC exposure.
- Enable Windows Firewall.
- Patch Windows systems regularly.
- Monitor RPC endpoint activity.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 587 | Authenticated Mail Server |
| 590 | Oracle Database Infrastructure |
| 591 | FileMaker Database |
| 593 | Windows RPC Services |

---

# Blue Team Perspective

Recommended Actions

- Secure SMTP submission with TLS.
- Restrict Oracle Listener access.
- Audit FileMaker databases.
- Harden Windows RPC services.
- Monitor authentication failures.
- Regularly patch enterprise servers.

---

# Red Team Perspective

Interesting Targets

### Port 587

Possible Findings

- Corporate mail server
- Exchange infrastructure
- SMTP submission service

Useful Enumeration

```bash
nmap --script smtp-commands,smtp-enum-users -p587 target
```

---

### Port 590

Possible Findings

- Oracle Database
- Enterprise ERP
- Financial systems

---

### Port 593

Possible Findings

- Windows Server
- Active Directory
- Exchange Server
- RPC Services

Useful Enumeration

```bash
nmap --script msrpc-enum -p593 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p581-600 target
```

Version Detection

```bash
nmap -sV -p587,590,591,593 target
```

SMTP Enumeration

```bash
nmap --script smtp-commands,smtp-enum-users -p587 target
```

RPC Enumeration

```bash
nmap --script msrpc-enum -p593 target
```

Aggressive Scan

```bash
nmap -A -p581-600 target
```

---

# Summary

Ports **581–600** introduce authenticated email submission, enterprise database infrastructure, Windows RPC services, and business application platforms. **Port 587** is the modern standard for secure SMTP message submission, **Port 590** often identifies Oracle database environments, and **Port 593** is closely tied to Windows RPC communications. These services commonly appear in corporate environments and should be carefully monitored due to their importance in authentication, messaging, and remote management.

---

# Ports 601–620

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 601 | TCP | syslog-conn | Syslog over TCP | rsyslog, syslog-ng | Reliable Log Collection | Prefer encrypted logging (TLS). |
| 602 | TCP | XML-RPC Beacon | XML-RPC Services | Enterprise Middleware | Remote Procedure Calls | Restrict Internet exposure. |
| 603 | TCP | IDXP | Inter-Domain Exchange Protocol | Directory Systems | Identity Services | Internal infrastructure. |
| 604 | TCP | TUNNEL | Vendor Tunnel Service | Enterprise Software | Secure Communications | Verify implementation. |
| 605 | TCP | SOAP-HTTP | SOAP Services | Java EE, .NET | Web Services | Secure authentication required. |
| 606 | TCP | CraySys | Cray Cluster Service | HPC Systems | Cluster Management | Management network only. |
| 607 | TCP | NQS | Network Queuing System | HPC Environments | Batch Processing | Restrict scheduler access. |
| 608 | TCP | SIFT-UFT | Secure File Transfer | Enterprise Platforms | File Exchange | Encrypt transfers. |
| 609 | TCP | NPMP-TRAP | Network Management | Monitoring Systems | Alerts | Internal monitoring only. |
| 610 | TCP | NPMP-LOCAL | Local Network Management | Enterprise | Monitoring | Restrict privileged users. |
| 611 | TCP | NPMP-GUI | GUI Management | Monitoring Platforms | Administration | Protect management interfaces. |
| 612 | TCP | HMMP-IND | HyperMedia Services | Vendor Platforms | Enterprise Content | Vendor-specific deployment. |
| 613 | TCP | HMMP-OP | HyperMedia Operations | Enterprise Systems | Internal Services | Rarely exposed. |
| 614 | TCP | SSHELL | Secure Shell Variant | Proprietary Platforms | Remote Administration | Prefer OpenSSH. |
| 615 | TCP | SCO-INETMGR | SCO Network Manager | SCO UNIX | System Management | Legacy system. |
| 616 | TCP | SCO-SYSMGR | SCO System Manager | SCO UNIX | Administration | Historical deployment. |
| 617 | TCP | SCO-DTMGR | SCO Desktop Manager | SCO UNIX | Desktop Services | Legacy platform. |
| 618 | TCP | DEI-ICDA | Industrial Data Access | Industrial Systems | Automation | Segment OT networks. |
| 619 | TCP | COMPAQ-EV | Compaq Enterprise Service | HPE Legacy Systems | Hardware Management | Restrict management traffic. |
| 620 | TCP | SCO-WEBSRVRMG3 | SCO Web Server | SCO UNIX | Web Applications | Patch or retire legacy systems. |

---

# Port Spotlight

## Port 601 — Syslog over TCP

While traditional Syslog commonly uses UDP Port 514, many enterprise deployments use **TCP Port 601** to ensure reliable log delivery.

Unlike UDP, TCP guarantees message delivery and ordering.

Common Software

- rsyslog
- syslog-ng
- Graylog
- Splunk Universal Forwarder
- Logstash

Typical Architecture

```text
Firewall

Router

Linux Server

Windows Server

      │

TCP Syslog

      ▼

Central Log Server

      │

SIEM

Alerting

Analytics
```

Example Scan

```bash
nmap -sV -p601 target
```

Security Recommendations

- Restrict trusted log sources.
- Enable Syslog over TLS (RFC 5425) where possible.
- Monitor abnormal log volume.
- Secure centralized log storage.

---

## Port 605 — SOAP Web Services

SOAP (Simple Object Access Protocol) is widely used in enterprise applications for exchanging structured XML messages.

Although REST APIs are now more common, SOAP remains heavily deployed in banking, healthcare, ERP, and government systems.

Common Platforms

- Microsoft .NET
- Java EE
- Oracle Middleware
- SAP
- IBM WebSphere

Typical Architecture

```text
Client

   │

SOAP Request

   ▼

Application Server

   │

Business Logic

   ▼

Database
```

Example Scan

```bash
nmap -sV -p605 target
```

Useful NSE Scripts

```bash
nmap --script http-title,http-headers -p605 target
```

Security Recommendations

- Require authentication.
- Disable unnecessary SOAP endpoints.
- Validate XML input.
- Protect against XML External Entity (XXE) attacks.

---

## Ports 615–617 — SCO UNIX Management

These ports are historically associated with SCO UNIX management services.

Although uncommon today, they may still appear in legacy enterprise environments.

Typical Deployment

```text
Administrator

      │

Management Console

      ▼

SCO UNIX Server

      │

System Services

      ▼

Applications
```

Security Recommendations

- Migrate unsupported operating systems.
- Restrict administrative access.
- Monitor legacy infrastructure.
- Remove unnecessary services.

---

## Port 618 — Industrial Data Access

Port **618** may be encountered within industrial environments where vendor-specific automation services are deployed.

Typical Architecture

```text
Engineering Station

        │

Industrial Protocol

        ▼

Controller

        │

Sensors

PLCs

Actuators
```

Common Industries

- Manufacturing
- Utilities
- Oil & Gas
- Water Treatment
- Transportation

Security Recommendations

- Isolate operational technology (OT) networks.
- Restrict remote management.
- Continuously monitor industrial communications.
- Apply vendor security updates.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 601 | Reliable Syslog Infrastructure |
| 605 | SOAP Web Services |
| 615–617 | Legacy SCO UNIX |
| 618 | Industrial Automation |

---

# Blue Team Perspective

Recommended Actions

- Centralize log collection using secure transport.
- Harden SOAP-based web services.
- Remove or isolate legacy SCO UNIX systems.
- Protect industrial management networks.
- Continuously monitor centralized logging infrastructure.
- Audit exposed management interfaces.

---

# Red Team Perspective

Interesting Targets

### Port 601

Possible Findings

- SIEM infrastructure
- Log aggregation servers
- Enterprise monitoring platforms

Useful Enumeration

```bash
nmap -sV -p601 target
```

---

### Port 605

Possible Findings

- Enterprise SOAP APIs
- ERP systems
- Healthcare applications
- Banking middleware

Useful Enumeration

```bash
nmap --script http-title,http-headers -p605 target
```

---

### Port 618

Possible Findings

- Industrial automation
- PLC communication
- Manufacturing control systems

Enumeration Commands

```bash
nmap -sV -p601,605,618 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p601-620 target
```

Version Detection

```bash
nmap -sV -p601,605,618 target
```

Default Script Scan

```bash
nmap -sC -sV -p601,605 target
```

Aggressive Scan

```bash
nmap -A -p601-620 target
```

---

# Summary

Ports **601–620** primarily include enterprise logging, SOAP-based web services, legacy UNIX management interfaces, and industrial automation protocols. **Port 601** often identifies centralized logging infrastructure, making it valuable for understanding an organization's monitoring architecture. **Port 605** commonly reveals enterprise SOAP services that may expose business-critical functionality, while **Port 618** can indicate operational technology (OT) environments where additional caution is required during security assessments.

---

# Ports 621–640

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 621 | TCP | ESCP-IP | Efficient Short Communication Protocol | Enterprise Devices | Embedded Communications | Restrict management access. |
| 622 | TCP | ASIP-WebAdmin | Appliance Web Administration | Network Appliances | Device Management | Management interface only. |
| 623 | UDP | ASF/RMCP (IPMI) | Alert Standard Format / Remote Management Control Protocol | Dell iDRAC, HPE iLO, Supermicro IPMI | Out-of-Band Server Management | Critical management service. |
| 624 | TCP | Crypto Admin | Cryptographic Administration | Security Appliances | Key Management | Restrict administrative access. |
| 625 | TCP | DEC DLM | Distributed Lock Manager | Cluster Systems | High Availability | Internal cluster traffic only. |
| 626 | TCP | ASIA | Application Server Interface | Enterprise Middleware | Business Applications | Vendor-specific deployment. |
| 627 | TCP | QIP Login | QIP DNS/DHCP | Infoblox Legacy | Network Services | Protect administrator accounts. |
| 628 | TCP | QMTP | Quick Mail Transfer Protocol | Mail Servers | Email Transfer | Rare deployment. |
| 629 | TCP | 3Com AMP3 | Network Management | 3Com Devices | Infrastructure Management | Legacy network equipment. |
| 630 | TCP | RDA | Remote Database Access | Enterprise Databases | Database Connectivity | Restrict trusted hosts. |
| 631 | TCP | IPP | Internet Printing Protocol | CUPS, Windows Print Services | Network Printing | Frequently exposed in enterprise networks. |
| 632 | TCP | bmpp | Bulk Messaging | Enterprise Software | Notifications | Internal deployment. |
| 633 | TCP | Service Control | Service Management | Vendor Platforms | Administration | Restrict privileged users. |
| 634 | TCP | ginad | Authentication Service | Enterprise Identity | Login Services | Monitor authentication logs. |
| 635 | TCP | RLZ DBase | Database Service | Legacy Applications | Data Access | Legacy deployment. |
| 636 | TCP | LDAPS | LDAP over SSL/TLS | Microsoft Active Directory, OpenLDAP | Secure Directory Services | Critical identity infrastructure. |
| 637 | TCP | lanserver | LAN Server | IBM LAN Server | File Sharing | Historical implementation. |
| 638 | TCP | mcns-sec | Secure Management | Enterprise Appliances | Secure Administration | Restrict Internet access. |
| 639 | TCP | MSDP | Multicast Source Discovery Protocol | Cisco IOS | Multicast Routing | Internal routing infrastructure. |
| 640 | TCP | entrust-sps | Entrust Secure Services | Entrust PKI | Certificate Management | Protect PKI infrastructure. |

---

# Port Spotlight

## Port 623 — IPMI (ASF/RMCP)

Port **623/UDP** is one of the most important ports in enterprise data centers because it is used by **IPMI (Intelligent Platform Management Interface)**.

IPMI allows administrators to remotely manage physical servers even when the operating system is powered off or unavailable.

Common Vendors

- Dell iDRAC
- HPE iLO
- Lenovo XClarity
- Supermicro IPMI
- ASUS Server Management

Typical Architecture

```text
Administrator

      │

IPMI

      ▼

Management Controller (BMC)

      │

Power Control

Hardware Monitoring

Virtual Console

Firmware Management
```

Example Scan

```bash
nmap -sU -p623 target
```

Useful NSE Scripts

```bash
nmap --script ipmi-version -sU -p623 target
```

```bash
nmap --script ipmi-cipher-zero -sU -p623 target
```

Security Risks

- Default credentials
- Cipher Zero authentication bypass
- Remote power control
- Firmware compromise
- Complete hardware takeover

Security Recommendations

- Disable Cipher Zero.
- Change factory credentials immediately.
- Restrict IPMI to dedicated management networks.
- Enable firmware updates.
- Monitor remote management activity.

---

## Port 631 — Internet Printing Protocol (IPP)

IPP is the modern standard for network printing.

Unlike LPD (Port 515), IPP supports authentication, encryption, and richer printer management capabilities.

Common Software

- CUPS
- Windows Print Server
- HP JetDirect
- Brother Print Server
- Canon Print Services

Typical Architecture

```text
Workstation

      │

IPP

      ▼

Print Server

      │

Network Printer

      ▼

Print Queue
```

Example Scan

```bash
nmap -sV -p631 target
```

Useful NSE Scripts

```bash
nmap --script ipp-info -p631 target
```

Security Risks

- Information disclosure
- Print job interception
- Unauthorized printing
- Printer exploitation

Security Recommendations

- Require authentication.
- Restrict printer administration.
- Disable unused printing protocols.
- Keep printer firmware updated.

---

## Port 636 — LDAPS

LDAPS is the encrypted version of LDAP and is heavily used in enterprise identity management.

Unlike LDAP on Port 389, LDAPS encrypts directory communications using SSL/TLS.

Common Software

- Microsoft Active Directory
- OpenLDAP
- 389 Directory Server
- Red Hat Directory Server

Typical Architecture

```text
Client

   │

TLS

   ▼

LDAPS Server

   │

Authentication

User Lookup

Group Lookup

   ▼

Directory Database
```

Example Scan

```bash
nmap -sV -p636 target
```

Useful NSE Scripts

```bash
nmap --script ldap-rootdse -p636 target
```

```bash
nmap --script ssl-cert -p636 target
```

Security Recommendations

- Require TLS 1.2 or newer.
- Disable anonymous binds.
- Audit privileged directory accounts.
- Monitor LDAP queries.

---

## Port 639 — MSDP

MSDP (Multicast Source Discovery Protocol) exchanges multicast source information between routing domains.

Typical Environment

```text
Router A

     │

MSDP

     ▼

Router B

     │

Multicast Sources

     ▼

Receivers
```

Security Recommendations

- Authenticate routing peers.
- Restrict MSDP neighbors.
- Monitor multicast routing events.
- Disable unused multicast services.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 623 | IPMI / Out-of-Band Management |
| 631 | Network Print Infrastructure |
| 636 | Secure Active Directory / LDAP |
| 639 | Multicast Routing |

---

# Blue Team Perspective

Recommended Actions

- Protect IPMI management interfaces.
- Disable unused printer services.
- Require encrypted LDAP communication.
- Monitor multicast routing changes.
- Separate management and production networks.
- Regularly audit directory service configurations.

---

# Red Team Perspective

Interesting Targets

### Port 623

Possible Findings

- Dell iDRAC
- HPE iLO
- Supermicro IPMI
- Bare-metal server management

Useful Enumeration

```bash
nmap --script ipmi-version,ipmi-cipher-zero -sU -p623 target
```

---

### Port 631

Possible Findings

- Enterprise printers
- Print servers
- Printer management portals

Useful Enumeration

```bash
nmap --script ipp-info -p631 target
```

---

### Port 636

Possible Findings

- Domain Controllers
- Identity providers
- Enterprise directory services

Useful Enumeration

```bash
nmap --script ldap-rootdse,ssl-cert -p636 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p621-640 target
```

Version Detection

```bash
nmap -sV -p631,636 target
```

UDP IPMI Scan

```bash
nmap -sU -p623 target
```

Directory Enumeration

```bash
nmap --script ldap-rootdse -p636 target
```

Aggressive Scan

```bash
nmap -A -p621-640 target
```

---

# Summary

Ports **621–640** include enterprise management services, secure directory infrastructure, printing protocols, and multicast routing technologies. **Port 623 (IPMI)** is particularly sensitive because it provides out-of-band hardware management and, if misconfigured, can allow complete control of physical servers. **Port 631 (IPP)** commonly identifies enterprise print infrastructure, while **Port 636 (LDAPS)** is a strong indicator of Active Directory or other secure directory services. These ports often reveal high-value administrative systems during enterprise reconnaissance.

---

# Ports 641–660

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 641 | TCP | Repcmd | Remote Process Control | Enterprise Systems | Process Management | Restrict administrative access. |
| 642 | TCP | ESet | Embedded Security Service | Security Appliances | Endpoint Management | Internal service only. |
| 643 | TCP | SANity | Storage Area Network Management | SAN Devices | Storage Administration | Protect storage controllers. |
| 644 | TCP | SSLShell | Secure Remote Shell | Proprietary Systems | Remote Administration | Prefer SSH. |
| 645 | TCP | DQM | Distributed Queue Manager | Enterprise Middleware | Message Queues | Restrict trusted hosts. |
| 646 | TCP | LDP | Label Distribution Protocol | Cisco IOS, Juniper, Nokia SR OS | MPLS Networks | Core routing infrastructure. |
| 647 | TCP | DHCP Failover | DHCP Synchronization | ISC DHCP | High Availability | Internal network only. |
| 648 | TCP | RRP | Resource Reservation | Enterprise Platforms | Resource Management | Vendor-specific deployment. |
| 649 | TCP | Cadview-3D | CAD Collaboration | Engineering Software | Design Sharing | Protect intellectual property. |
| 650 | TCP | OBEX | Object Exchange | Bluetooth Gateways | File Transfer | Monitor unauthorized transfers. |
| 651 | TCP | IEEE-MMS | Manufacturing Messaging | Industrial Systems | Process Automation | Segment OT networks. |
| 652 | TCP | HELIX | Helix Server | RealNetworks | Media Streaming | Patch regularly. |
| 653 | TCP | RMC | Remote Management Console | Enterprise Appliances | Administration | Restrict management interfaces. |
| 654 | TCP | AODV | Ad Hoc Routing | Mobile Networks | Routing | Rare deployment. |
| 655 | TCP | TINC | VPN Service | Tinc VPN | Secure Networking | Strong authentication required. |
| 656 | TCP | SPMP | Simple Network Management | Network Devices | Monitoring | Restrict management traffic. |
| 657 | TCP | RMC2 | Remote Console | Enterprise Platforms | Administration | Internal use only. |
| 658 | TCP | TenFold | Identity Management | IAM Platforms | Authentication | Protect directory data. |
| 659 | TCP | Mac-SRVR-ADMIN | Apple Server Administration | macOS Server | Server Management | Secure administrator accounts. |
| 660 | TCP | Apple-MACAPP | Apple Management | Apple Infrastructure | Enterprise Administration | Internal deployment. |

---

# Port Spotlight

## Port 646 — Label Distribution Protocol (LDP)

LDP is one of the core protocols used in **Multiprotocol Label Switching (MPLS)** networks.

It enables routers to exchange label mappings required for forwarding traffic across MPLS infrastructures.

Common Vendors

- Cisco
- Juniper
- Nokia
- Huawei
- Arista

Typical Architecture

```text
Router

   │

LDP

   ▼

MPLS Router

   │

Label Switching

   ▼

Core Network

   │

Destination Router
```

Example Scan

```bash
nmap -sV -p646 target
```

Security Risks

- Routing information disclosure
- Unauthorized MPLS peers
- Core network reconnaissance

Security Recommendations

- Restrict LDP neighbors.
- Authenticate routing peers.
- Monitor MPLS topology changes.
- Separate management and production networks.

---

## Port 647 — DHCP Failover

DHCP Failover synchronizes lease information between redundant DHCP servers to provide high availability.

Typical Deployment

```text
Primary DHCP

      │

Lease Replication

      ▼

Secondary DHCP

      │

Clients

      ▼

Network
```

Common Software

- ISC DHCP
- Enterprise DHCP Appliances

Security Recommendations

- Restrict synchronization links.
- Encrypt replication traffic.
- Monitor lease inconsistencies.
- Audit DHCP server configuration.

---

## Port 651 — Manufacturing Message Specification (MMS)

Manufacturing Message Specification (MMS) is widely used in industrial automation and electrical substations.

It is commonly found in:

- IEC 61850 environments
- Smart grids
- Electrical substations
- Industrial control systems

Typical Architecture

```text
SCADA

   │

MMS

   ▼

Substation Controller

   │

IED

PLC

RTU
```

Example Scan

```bash
nmap -sV -p651 target
```

Security Risks

- Operational disruption
- Unauthorized device control
- Information disclosure

Security Recommendations

- Isolate industrial control networks.
- Restrict engineering workstations.
- Monitor industrial communications.
- Apply vendor firmware updates.

---

## Port 655 — Tinc VPN

Tinc is an open-source mesh VPN designed for secure communication between distributed systems.

Typical Architecture

```text
Node A

   │

Encrypted Tunnel

   ▼

Mesh VPN

   │

Encrypted Tunnel

   ▼

Node B
```

Common Uses

- Site-to-site VPN
- Private cloud networking
- Distributed infrastructure
- Development environments

Example Scan

```bash
nmap -sV -p655 target
```

Security Recommendations

- Rotate VPN keys regularly.
- Restrict node enrollment.
- Monitor mesh topology.
- Keep VPN software updated.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 646 | MPLS Infrastructure |
| 647 | DHCP High Availability |
| 651 | Industrial Automation |
| 655 | Mesh VPN |
| 659–660 | Apple Enterprise Infrastructure |

---

# Blue Team Perspective

Recommended Actions

- Secure MPLS routing peers.
- Protect DHCP replication traffic.
- Isolate industrial automation networks.
- Rotate VPN credentials regularly.
- Restrict Apple management interfaces.
- Continuously monitor critical infrastructure.

---

# Red Team Perspective

Interesting Targets

### Port 646

Possible Findings

- MPLS backbone
- ISP infrastructure
- Enterprise WAN

---

### Port 651

Possible Findings

- Electrical substations
- SCADA servers
- Industrial automation
- Smart grid infrastructure

---

### Port 655

Possible Findings

- Mesh VPN
- Cloud infrastructure
- Secure site-to-site connectivity

Useful Enumeration

```bash
nmap -sV -p646,651,655 target
```

---

### Ports 659–660

Possible Findings

- Apple management servers
- macOS infrastructure
- Enterprise Apple deployment

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p641-660 target
```

Version Detection

```bash
nmap -sV -p646,651,655,659 target
```

Default Script Scan

```bash
nmap -sC -sV -p646,651,655 target
```

Aggressive Scan

```bash
nmap -A -p641-660 target
```

---

# Summary

Ports **641–660** highlight enterprise networking, MPLS routing, industrial automation, VPN technologies, and Apple management infrastructure. **Port 646 (LDP)** is a strong indicator of MPLS-enabled networks, while **Port 651 (MMS)** frequently identifies critical industrial and energy-sector systems implementing IEC 61850 standards. **Port 655 (Tinc VPN)** may reveal secure mesh VPN deployments, and **Ports 659–660** often point to Apple enterprise management environments. These services can provide valuable insight into both IT and OT infrastructures during reconnaissance.

---

# Ports 661–680

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 661 | TCP | MacOS Server Admin | Apple Administration | macOS Server | System Management | Restrict administrator access. |
| 662 | TCP | PFTP | Proprietary File Transfer | Enterprise Software | Data Exchange | Vendor-specific protocol. |
| 663 | TCP | Surveyor | Network Discovery | Monitoring Systems | Infrastructure Discovery | Restrict internal access. |
| 664 | TCP | ASF Secure RMCP | Alert Standard Format | Server Management | Hardware Monitoring | Protect management interfaces. |
| 665 | TCP | SUN-DR | Sun Disaster Recovery | Solaris | Backup & Recovery | Legacy enterprise deployment. |
| 666 | TCP | Doom | Multiplayer Game | Doom Engine | Gaming | Rarely encountered today. |
| 667 | TCP | Disclose | Information Service | Enterprise Software | Internal Communication | Restrict access. |
| 668 | TCP | Mecomm | Messaging Platform | Enterprise Systems | Internal Messaging | Vendor-specific implementation. |
| 669 | TCP | Cisco MGX | ATM Switch Management | Cisco MGX | Carrier Infrastructure | Management network only. |
| 670 | TCP | VACDSM | Vendor Control Service | Enterprise Devices | Administration | Verify implementation. |
| 671 | TCP | VACDSM-SWS | Secure Vendor Service | Enterprise Systems | Secure Management | Restrict privileged users. |
| 672 | TCP | SFS Config | Secure File System | Distributed Storage | Configuration | Internal deployment. |
| 673 | TCP | VPN Control | VPN Management | Security Appliances | VPN Administration | Protect administrator credentials. |
| 674 | TCP | ACAP | Application Configuration Access Protocol | Messaging Platforms | Client Configuration | Legacy service. |
| 675 | TCP | DCTP | Data Communication Transfer | Enterprise Middleware | Data Exchange | Vendor-specific deployment. |
| 676 | TCP | VPP | Virtual Packet Processing | Networking Platforms | Packet Processing | Internal infrastructure. |
| 677 | TCP | NPP | Network Processing | Enterprise Appliances | Network Services | Restrict management. |
| 678 | TCP | Gnutella | Peer-to-Peer Networking | Gnutella Clients | File Sharing | Monitor unauthorized usage. |
| 679 | TCP | MRM | Media Resource Manager | Multimedia Platforms | Resource Management | Vendor-specific. |
| 680 | TCP | Entrust-AAAS | Entrust Authentication | Entrust Identity | AAA Services | Protect authentication infrastructure. |

---

# Port Spotlight

## Port 664 — ASF / Secure RMCP

ASF (Alert Standard Format) extends hardware monitoring capabilities for enterprise servers.

It is closely related to remote management technologies and is commonly encountered alongside IPMI deployments.

Common Vendors

- Dell
- HPE
- Lenovo
- Supermicro

Typical Architecture

```text
Administrator

      │

ASF/RMCP

      ▼

Management Controller

      │

Hardware Status

Power Control

Alerting
```

Example Scan

```bash
nmap -sV -p664 target
```

Security Recommendations

- Restrict management traffic.
- Disable unused remote management services.
- Monitor administrator activity.
- Isolate management networks.

---

## Port 669 — Cisco MGX

Cisco MGX platforms provide carrier-grade switching and WAN infrastructure.

These devices commonly appear in telecommunications and service provider environments.

Typical Deployment

```text
Core Router

      │

Cisco MGX

      │

ATM/MPLS Backbone

      ▼

Branch Networks
```

Common Uses

- Carrier WAN
- MPLS Backbone
- ATM Switching
- Telecom Infrastructure

Security Recommendations

- Restrict administrative access.
- Disable unused management services.
- Monitor routing infrastructure.
- Apply vendor firmware updates.

---

## Port 674 — ACAP

Application Configuration Access Protocol (ACAP) allows centralized storage and retrieval of client configuration information.

Typical Workflow

```text
Mail Client

      │

Configuration Request

      ▼

ACAP Server

      │

User Settings

Address Books

Preferences
```

Security Recommendations

- Require authentication.
- Encrypt client connections.
- Audit configuration changes.
- Disable anonymous access.

---

## Port 678 — Gnutella

Gnutella is one of the earliest decentralized peer-to-peer (P2P) file-sharing protocols.

Although uncommon in modern enterprise environments, its presence may indicate unauthorized file sharing.

Typical Architecture

```text
Peer

   │

P2P Network

   ▼

Peer

   │

File Exchange

   ▼

Peer
```

Security Risks

- Data leakage
- Malware distribution
- Copyright violations
- Unauthorized software

Security Recommendations

- Block unauthorized P2P traffic.
- Monitor endpoint behavior.
- Apply network access controls.
- Educate users about acceptable use policies.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 664 | Hardware Management Infrastructure |
| 669 | Carrier / Cisco WAN |
| 674 | Centralized Client Configuration |
| 678 | Peer-to-Peer File Sharing |
| 680 | Enterprise AAA Infrastructure |

---

# Blue Team Perspective

Recommended Actions

- Secure hardware management controllers.
- Protect carrier network equipment.
- Restrict ACAP configuration servers.
- Detect unauthorized P2P traffic.
- Harden AAA infrastructure.
- Continuously audit administrative services.

---

# Red Team Perspective

Interesting Targets

### Port 664

Possible Findings

- Server management controllers
- Enterprise hardware infrastructure
- Remote administration services

---

### Port 669

Possible Findings

- Cisco carrier equipment
- WAN backbone
- MPLS infrastructure

---

### Port 678

Possible Findings

- Unauthorized P2P software
- File-sharing endpoints
- Shadow IT

Useful Enumeration

```bash
nmap -sV -p664,669,678,680 target
```

---

### Port 680

Possible Findings

- Authentication servers
- Identity infrastructure
- AAA platforms

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p661-680 target
```

Version Detection

```bash
nmap -sV -p664,669,678,680 target
```

Default Script Scan

```bash
nmap -sC -sV -p664,678 target
```

Aggressive Scan

```bash
nmap -A -p661-680 target
```

---

# Summary

Ports **661–680** primarily represent enterprise management services, carrier-grade networking infrastructure, centralized configuration systems, and authentication platforms. **Port 664** may indicate remote hardware management capabilities, **Port 669** often reveals Cisco carrier or MPLS equipment, and **Port 678 (Gnutella)** can identify unauthorized peer-to-peer activity within enterprise environments. **Port 680** may expose enterprise authentication and authorization services that form part of an organization's identity infrastructure.

---

# Ports 681–700

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 681 | TCP | Entrust-KMSH | Entrust Key Management | Entrust PKI | Cryptographic Key Management | Protect certificate infrastructure. |
| 682 | TCP | XFR | File Replication | Enterprise Systems | Data Synchronization | Restrict trusted hosts. |
| 683 | TCP | CORBA-IIOP | Distributed Objects | Oracle, IBM | Enterprise Middleware | Internal communications only. |
| 684 | TCP | PWP | Password Policy Service | Enterprise IAM | Identity Management | Enforce strong authentication. |
| 685 | TCP | MDC-PortMapper | Mapping Service | Enterprise Middleware | Service Discovery | Restrict exposure. |
| 686 | TCP | HCP-WISMAR | Industrial Control | Manufacturing Systems | Process Automation | Isolate OT environments. |
| 687 | TCP | ASIPRegistry | Device Registry | Embedded Platforms | Registration Services | Vendor-specific implementation. |
| 688 | TCP | Realm-RUSD | Realm Registry | Authentication Platforms | Identity Services | Internal infrastructure. |
| 689 | TCP | NMAP | Network Mapping Service | Vendor Platforms | Network Discovery | Verify actual implementation. |
| 690 | TCP | VATP | Virtual Access Transfer Protocol | Enterprise Networks | Secure Communications | Restrict management access. |
| 691 | TCP | MS Exchange Routing | Microsoft Exchange | Mail Routing | Email Infrastructure | Monitor mail routing. |
| 692 | TCP | Hyperwave ISP | Hyperwave | Document Management | Enterprise Collaboration | Legacy deployment. |
| 693 | TCP | Connendp | Connection Endpoint | Middleware | Application Connectivity | Internal service. |
| 694 | TCP | HA Cluster Heartbeat | High Availability | Linux HA, Pacemaker | Cluster Synchronization | Internal cluster traffic only. |
| 695 | TCP | IEEE-MMS-SSL | Secure Manufacturing Messaging | Industrial Systems | Secure Automation | Protect industrial assets. |
| 696 | TCP | ODRP | Object Distribution | Enterprise Middleware | Distributed Systems | Vendor-specific deployment. |
| 697 | TCP | RFS Server | Remote File Service | UNIX | File Sharing | Prefer encrypted alternatives. |
| 698 | TCP | OLSR | Optimized Link State Routing | Mesh Networks | Dynamic Routing | Restrict routing peers. |
| 699 | TCP | Access Network | Network Access Services | Enterprise Appliances | Device Connectivity | Verify configuration. |
| 700 | TCP | EPP | Extensible Provisioning Protocol | Domain Registries | Domain Management | Critical Internet infrastructure. |

---

# Port Spotlight

## Port 694 — High Availability Cluster Heartbeat

Port **694** is commonly associated with heartbeat communications between clustered systems.

It enables multiple servers to continuously verify each other's health and automatically perform failover when a node becomes unavailable.

Common Software

- Pacemaker
- Corosync
- Linux-HA
- Red Hat High Availability
- SUSE HA Extension

Typical Architecture

```text
Node A

   │

Heartbeat

   ▼

Node B

   │

Cluster Manager

   ▼

Shared Storage

Applications
```

Example Scan

```bash
nmap -sV -p694 target
```

Security Risks

- Cluster topology disclosure
- Unauthorized node communication
- Service disruption

Security Recommendations

- Isolate heartbeat networks.
- Authenticate cluster members.
- Restrict management interfaces.
- Monitor cluster synchronization.

---

## Port 695 — Secure Manufacturing Messaging

Secure variants of Manufacturing Message Specification (MMS) may use this port in vendor-specific industrial deployments.

Typical Environment

```text
Engineering Station

        │

Secure MMS

        ▼

Industrial Controller

        │

PLC

IED

RTU
```

Common Industries

- Smart Grid
- Manufacturing
- Oil & Gas
- Utilities
- Transportation

Security Recommendations

- Segment OT environments.
- Enable certificate-based authentication.
- Monitor industrial traffic.
- Maintain vendor firmware updates.

---

## Port 698 — OLSR

Optimized Link State Routing (OLSR) is a routing protocol designed for mobile ad hoc networks (MANETs).

Common Deployments

- Wireless mesh networks
- Emergency communications
- Military networks
- Community Wi-Fi
- Research laboratories

Typical Architecture

```text
Node A

   │

OLSR

   ▼

Mesh Router

   │

OLSR

   ▼

Node B
```

Example Scan

```bash
nmap -sV -p698 target
```

Security Risks

- Rogue routing peers
- Route manipulation
- Topology disclosure

Security Recommendations

- Authenticate routing neighbors.
- Restrict mesh participation.
- Monitor routing updates.
- Encrypt management traffic.

---

## Port 700 — Extensible Provisioning Protocol (EPP)

EPP is the industry-standard protocol used by domain registries and registrars for domain management.

Typical Operations

- Domain registration
- Domain renewal
- Name server updates
- Contact management
- Domain transfers

Typical Architecture

```text
Registrar

     │

EPP

     ▼

Registry

     │

Domain Database

     ▼

DNS Infrastructure
```

Common Platforms

- Verisign
- ICANN-accredited Registries
- Domain Registrars
- OpenRegistry

Example Scan

```bash
nmap -sV -p700 target
```

Security Recommendations

- Require mutual TLS authentication.
- Restrict registrar IP addresses.
- Enable comprehensive logging.
- Monitor provisioning activities.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 694 | High Availability Cluster |
| 695 | Secure Industrial Automation |
| 698 | Wireless Mesh Network |
| 700 | Domain Registry Infrastructure |

---

# Blue Team Perspective

Recommended Actions

- Secure cluster heartbeat communications.
- Isolate industrial automation networks.
- Authenticate routing neighbors.
- Protect domain registry infrastructure.
- Monitor failover events.
- Audit critical administrative actions.

---

# Red Team Perspective

Interesting Targets

### Port 694

Possible Findings

- High-availability clusters
- Shared storage systems
- Mission-critical enterprise applications

---

### Port 695

Possible Findings

- Industrial controllers
- Critical infrastructure
- Secure SCADA environments

---

### Port 698

Possible Findings

- Wireless mesh infrastructure
- MANET deployments
- Community networking

---

### Port 700

Possible Findings

- Domain registry systems
- Registrar infrastructure
- DNS management services

Useful Enumeration

```bash
nmap -sV -p694,695,698,700 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p681-700 target
```

Version Detection

```bash
nmap -sV -p694,695,698,700 target
```

Default Script Scan

```bash
nmap -sC -sV -p694,700 target
```

Aggressive Scan

```bash
nmap -A -p681-700 target
```

---

# Summary

Ports **681–700** include enterprise identity services, clustering technologies, industrial automation, mesh routing protocols, and domain registry infrastructure. **Port 694** is commonly associated with high-availability clusters, making it valuable for identifying redundant enterprise services. **Port 695** may reveal secure industrial automation systems, while **Port 698 (OLSR)** indicates wireless mesh networking. **Port 700 (EPP)** is especially significant in Internet infrastructure because it is used for secure communication between domain registrars and registries.

---

# Ports 701–720

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 701 | TCP | LMP | Link Management Protocol | Carrier Equipment | Optical Networks | Restrict control traffic. |
| 702 | TCP | IRIS Beacon | Monitoring Service | Enterprise Appliances | Health Monitoring | Vendor-specific deployment. |
| 703 | TCP | HP Device Discovery | HP Enterprise | Device Discovery | Infrastructure Inventory | Restrict internal access. |
| 704 | TCP | ELCSD | Embedded Licensing | Enterprise Software | License Management | Protect license servers. |
| 705 | TCP | AgentX | SNMP Agent Extension | Net-SNMP | Monitoring | Restrict SNMP infrastructure. |
| 706 | TCP | SILC | Secure Internet Live Conferencing | SILC Server | Secure Chat | Historical deployment. |
| 707 | TCP | Borland DSJ | Borland Middleware | Enterprise Applications | Development Platforms | Legacy deployment. |
| 708 | TCP | Entrust KMIP | Key Management | Entrust, HSM Vendors | Cryptographic Services | Protect encryption keys. |
| 709 | TCP | Kerberos Administration | Kerberos Realm | Identity Infrastructure | Authentication | Restrict administrator access. |
| 710 | TCP | X Font Service (XFS) | X Window System | Linux/UNIX | Font Distribution | Legacy graphical service. |
| 711 | TCP | Cisco TDP | Tag Distribution Protocol | Cisco IOS | MPLS | Superseded by LDP. |
| 712 | TCP | TBRPF | Topology Broadcast | Routing Platforms | Dynamic Routing | Internal routing only. |
| 713 | TCP | IRIS-XPC | Cross Platform Communication | Enterprise Middleware | Messaging | Vendor-specific. |
| 714 | TCP | IRIS-XPCS | Secure IRIS Communication | Enterprise Systems | Secure Messaging | Internal service. |
| 715 | TCP | IRIS-LWZ | Lightweight Service | Enterprise Platforms | Application Services | Rare deployment. |
| 716 | TCP | PANA | Protocol for Network Access Authentication | Network Appliances | Access Control | Secure authentication required. |
| 717 | TCP | OMSRPC | Object Management RPC | Middleware | Remote Management | Restrict exposure. |
| 718 | TCP | OODMP | Object-Oriented Data Management | Enterprise Software | Database Access | Internal systems only. |
| 719 | TCP | IATP | Intelligent Agent Transfer | Automation Platforms | Agent Communication | Vendor-specific implementation. |
| 720 | TCP | SMQP | Simple Message Queue Protocol | Enterprise Messaging | Queue Management | Restrict broker access. |

---

# Port Spotlight

## Port 705 — AgentX

AgentX extends SNMP by allowing multiple subagents to communicate with a master SNMP agent.

It is commonly found on network monitoring servers and enterprise appliances.

Common Software

- Net-SNMP
- Cisco Network Management
- Juniper Monitoring
- Enterprise Monitoring Platforms

Typical Architecture

```text
Monitoring Server

        │

SNMP Manager

        │

Master Agent

   ┌────┴────┐

Subagent 1  Subagent 2

        │

Network Devices
```

Example Scan

```bash
nmap -sV -p705 target
```

Security Recommendations

- Restrict SNMP management hosts.
- Disable unused subagents.
- Use SNMPv3 whenever possible.
- Monitor configuration changes.

---

## Port 708 — Key Management Infrastructure

Port **708** may appear on enterprise cryptographic key management platforms.

Typical Uses

- Hardware Security Modules (HSM)
- Certificate Authorities
- Encryption Key Management
- Enterprise PKI

Typical Architecture

```text
Application

     │

Key Request

     ▼

Key Management Server

     │

HSM

     ▼

Encrypted Keys
```

Security Recommendations

- Restrict administrator access.
- Use Hardware Security Modules.
- Rotate encryption keys.
- Enable detailed auditing.

---

## Port 710 — X Font Service (XFS)

The X Font Server provides fonts to X11 graphical environments.

Although uncommon today, XFS may still appear on legacy UNIX systems.

Typical Architecture

```text
X Client

   │

Font Request

   ▼

X Font Server

   │

Font Repository

   ▼

Display
```

Security Recommendations

- Remove unused X11 components.
- Restrict access to trusted hosts.
- Migrate to modern graphical environments.

---

## Port 716 — PANA

PANA (Protocol for Carrying Authentication for Network Access) authenticates devices before allowing network access.

Common Deployments

- Enterprise Wi-Fi
- ISP Access Networks
- IoT Infrastructure
- Broadband Services

Typical Workflow

```text
Client Device

      │

Authentication

      ▼

PANA Server

      │

AAA Server

      ▼

Network Access
```

Example Scan

```bash
nmap -sV -p716 target
```

Security Recommendations

- Enforce certificate-based authentication.
- Integrate with RADIUS or AAA.
- Monitor failed authentication attempts.
- Restrict management interfaces.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 705 | SNMP Monitoring Infrastructure |
| 708 | Enterprise Key Management |
| 710 | Legacy UNIX/X11 |
| 716 | Network Access Authentication |
| 720 | Enterprise Message Queue |

---

# Blue Team Perspective

Recommended Actions

- Harden SNMP infrastructure using SNMPv3.
- Protect cryptographic key management systems.
- Remove legacy X11 services where possible.
- Secure network access authentication servers.
- Monitor enterprise messaging platforms.
- Audit privileged administrative accounts.

---

# Red Team Perspective

Interesting Targets

### Port 705

Possible Findings

- Network monitoring servers
- SNMP infrastructure
- Enterprise management platforms

---

### Port 708

Possible Findings

- Certificate Authorities
- Hardware Security Modules
- Enterprise PKI

---

### Port 716

Possible Findings

- AAA infrastructure
- Network authentication services
- ISP access gateways

---

### Port 720

Possible Findings

- Enterprise message brokers
- Internal middleware
- Distributed application infrastructure

Useful Enumeration

```bash
nmap -sV -p705,708,716,720 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p701-720 target
```

Version Detection

```bash
nmap -sV -p705,708,710,716,720 target
```

Default Script Scan

```bash
nmap -sC -sV -p705,716 target
```

Aggressive Scan

```bash
nmap -A -p701-720 target
```

---

# Summary

Ports **701–720** primarily represent enterprise monitoring systems, cryptographic key management, legacy UNIX graphical services, network access authentication, and messaging infrastructure. **Port 705 (AgentX)** often identifies SNMP-based monitoring environments, **Port 708** may indicate enterprise PKI or HSM deployments, and **Port 716 (PANA)** is associated with network access control systems. These services frequently support critical enterprise infrastructure and should be carefully secured and monitored.

---

# Ports 721–740

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 721 | TCP | NETVIEWDM1 | IBM NetView Distribution | IBM NetView | Network Management | Internal enterprise infrastructure. |
| 722 | TCP | NETVIEWDM2 | IBM NetView | Enterprise Monitoring | Network Operations | Restrict administrative access. |
| 723 | TCP | NETVIEWDM3 | IBM NetView | Distributed Management | Monitoring | Vendor-specific deployment. |
| 724 | TCP | ODSD | Object Directory Service | Enterprise Middleware | Directory Services | Internal service. |
| 725 | TCP | OSM | Object Storage Manager | Enterprise Storage | Data Management | Protect storage infrastructure. |
| 726 | TCP | MVS Capacity | IBM Mainframe | Capacity Planning | Mainframe Operations | Restrict privileged users. |
| 727 | TCP | IMS Messaging | IBM IMS | Transaction Processing | Enterprise Applications | Secure middleware communication. |
| 728 | TCP | Oracle Notification | Oracle Products | Event Notifications | Database Infrastructure | Restrict trusted hosts. |
| 729 | TCP | IBM DB2 Event | IBM DB2 | Database Events | Enterprise Databases | Monitor event traffic. |
| 730 | TCP | NetView DM | IBM NetView | Enterprise Monitoring | Infrastructure Management | Internal deployment. |
| 731 | TCP | NetView Event | IBM NetView | Event Management | Monitoring | Vendor-specific. |
| 732 | TCP | NetView Alert | IBM NetView | Alert Distribution | Enterprise Operations | Secure management interfaces. |
| 733 | TCP | Flexible Licensing | License Server | Software Licensing | Enterprise Applications | Restrict access. |
| 734 | TCP | NetScout | Network Analysis | NetScout | Traffic Monitoring | Protect monitoring infrastructure. |
| 735 | TCP | Sonus | VoIP Infrastructure | Sonus SBC | Unified Communications | Restrict management. |
| 736 | TCP | OpenSecure | Secure Communications | Enterprise Platforms | Encrypted Messaging | Internal deployment. |
| 737 | TCP | CAPI | Common ISDN API | Telecommunications | Voice Services | Legacy implementation. |
| 738 | TCP | OSP | Open Settlement Protocol | VoIP Providers | Carrier Billing | Protect signaling infrastructure. |
| 739 | TCP | Carrier Control | Telecom Service | Carrier Networks | Service Control | Internal use only. |
| 740 | TCP | NetGW | Network Gateway | Enterprise Appliances | Gateway Management | Secure administrative access. |

---

# Port Spotlight

## Ports 721–732 — IBM NetView Infrastructure

Several ports within this range are historically associated with **IBM NetView**, an enterprise network monitoring and management platform.

NetView provides:

- Network monitoring
- Event collection
- Fault management
- Performance analysis
- Automation

Typical Architecture

```text
Network Devices

      │

SNMP / Events

      ▼

IBM NetView Server

      │

Monitoring

Automation

Alerting

      ▼

Operations Center
```

Example Scan

```bash
nmap -sV -p721-732 target
```

Security Recommendations

- Restrict NetView access.
- Protect management interfaces.
- Enable administrator auditing.
- Encrypt management traffic.

---

## Port 734 — NetScout

NetScout products provide deep network visibility and performance analytics.

Common Uses

- Traffic analysis
- Application monitoring
- Packet inspection
- Performance troubleshooting

Typical Architecture

```text
Switch

Router

Firewall

      │

Traffic Mirror

      ▼

NetScout Appliance

      │

Analytics

Reports

Alerts
```

Example Scan

```bash
nmap -sV -p734 target
```

Security Recommendations

- Restrict appliance access.
- Secure mirrored traffic.
- Monitor administrator actions.
- Protect captured network data.

---

## Port 735 — Sonus SBC

Port **735** may indicate a **Sonus (Ribbon Communications)** Session Border Controller.

Session Border Controllers protect VoIP infrastructure by controlling SIP traffic.

Typical Deployment

```text
Internet

    │

SIP

    ▼

Session Border Controller

    │

PBX

VoIP Phones

Carrier Network
```

Common Uses

- SIP Security
- VoIP Routing
- NAT Traversal
- Fraud Prevention

Security Recommendations

- Restrict management interfaces.
- Enable SIP authentication.
- Monitor abnormal call activity.
- Keep SBC firmware updated.

---

## Port 738 — Open Settlement Protocol (OSP)

OSP enables secure authorization and settlement between VoIP providers.

Typical Workflow

```text
Carrier A

    │

OSP Request

    ▼

OSP Server

    │

Authorization

Settlement

    ▼

Carrier B
```

Security Recommendations

- Use TLS encryption.
- Restrict trusted peers.
- Audit transaction logs.
- Monitor authorization failures.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 721–732 | IBM NetView Infrastructure |
| 734 | Network Performance Monitoring |
| 735 | Session Border Controller (SBC) |
| 738 | VoIP Settlement Infrastructure |

---

# Blue Team Perspective

Recommended Actions

- Protect enterprise monitoring systems.
- Restrict access to VoIP controllers.
- Encrypt telecom signaling.
- Audit network management platforms.
- Monitor administrative activity.
- Secure analytics appliances.

---

# Red Team Perspective

Interesting Targets

### Ports 721–732

Possible Findings

- Enterprise monitoring systems
- Network operations center
- Infrastructure inventory
- Administrative servers

---

### Port 734

Possible Findings

- Packet capture appliances
- Traffic analysis systems
- Network monitoring infrastructure

---

### Port 735

Possible Findings

- VoIP gateway
- Session Border Controller
- Enterprise telephony

---

### Port 738

Possible Findings

- Carrier infrastructure
- Telecom authorization servers
- VoIP settlement systems

Useful Enumeration

```bash
nmap -sV -p721-740 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p721-740 target
```

Version Detection

```bash
nmap -sV -p721-740 target
```

Default Script Scan

```bash
nmap -sC -sV -p734,735 target
```

Aggressive Scan

```bash
nmap -A -p721-740 target
```

---

# Summary

Ports **721–740** are dominated by enterprise monitoring, IBM mainframe infrastructure, telecom services, and VoIP management platforms. **Ports 721–732** often identify IBM NetView deployments used for centralized network monitoring and automation. **Port 734** may reveal network performance monitoring appliances, while **Ports 735 and 738** are closely associated with carrier-grade VoIP infrastructure. These services are typically found in large enterprise and telecommunications environments and can provide valuable insight into network architecture during reconnaissance.

---

# Ports 741–760

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 741 | TCP | NETGW | Network Gateway Service | Enterprise Gateways | Traffic Forwarding | Restrict management access. |
| 742 | TCP | NETRCS | Remote Control Service | Enterprise Systems | Remote Administration | Require authentication. |
| 743 | TCP | FlexLM | License Manager | FlexNet Publisher | Software Licensing | Limit access to trusted hosts. |
| 744 | TCP | Fujitsu Device Manager | Hardware Management | Fujitsu Servers | Device Administration | Internal infrastructure only. |
| 745 | TCP | SecurID | RSA Authentication | RSA SecurID | Multi-Factor Authentication | Protect authentication servers. |
| 746 | TCP | SilverPlatter | Digital Library | Academic Platforms | Information Retrieval | Legacy deployments. |
| 747 | TCP | Kerberos Password | Kerberos | Password Changes | Identity Services | Require encrypted communication. |
| 748 | TCP | Kerberos Administration | MIT Kerberos | Realm Administration | Authentication | Administrator access only. |
| 749 | TCP | Kerberos Admin | MIT Kerberos KADM | Kerberos Management | Identity Infrastructure | Critical authentication service. |
| 750 | TCP | Kerberos v4 | Legacy Kerberos | Authentication | Legacy UNIX Systems | Upgrade to Kerberos v5. |
| 751 | TCP | Kerberos Login | Legacy Authentication | UNIX | Authentication | Rare today. |
| 752 | TCP | QRH | Quick Recovery Host | Enterprise Systems | Recovery Services | Vendor-specific. |
| 753 | TCP | Reverse Discovery | Discovery Protocol | Network Devices | Asset Identification | Restrict discovery traffic. |
| 754 | TCP | Tell | Administrative Service | Legacy Systems | Remote Administration | Verify implementation. |
| 755 | TCP | NCADG-IP-UDP | DCE/RPC | Distributed Computing | RPC Services | Restrict RPC exposure. |
| 756 | TCP | QSC | Queue Service | Enterprise Middleware | Messaging | Internal systems only. |
| 757 | TCP | ELCSD | Embedded Licensing | Enterprise Applications | License Management | Secure licensing servers. |
| 758 | TCP | DEC DNS | Digital Equipment | Directory Services | Legacy Enterprise | Internal deployment. |
| 759 | TCP | QAZ | Vendor Service | Enterprise Systems | Proprietary Communications | Verify implementation. |
| 760 | TCP | KRBUPDATE | Kerberos Update | Kerberos Infrastructure | Identity Synchronization | Secure authentication updates. |

---

# Port Spotlight

## Ports 747–750 — Kerberos Infrastructure

Ports **747–750** are associated with various Kerberos authentication services, particularly older implementations.

Kerberos is one of the most widely deployed enterprise authentication protocols.

Common Platforms

- Microsoft Active Directory
- MIT Kerberos
- Heimdal
- UNIX
- Linux

Typical Architecture

```text
Client

   │

Authentication Request

   ▼

Kerberos KDC

   │

Ticket Granting Ticket

   ▼

Application Server
```

Example Scan

```bash
nmap -sV -p747-750 target
```

Useful NSE Scripts

```bash
nmap --script krb5-enum-users -p88 target
```

Although Kerberos normally operates on **port 88**, discovering related administrative ports often indicates a complete Kerberos deployment.

Security Risks

- Ticket attacks
- Kerberoasting
- Password spraying
- Administrative interface exposure

Security Recommendations

- Enable strong encryption types.
- Disable legacy Kerberos versions.
- Monitor failed authentication events.
- Restrict administrative services.

---

## Port 743 — FlexLM License Manager

FlexLM (FlexNet Publisher) is one of the most common enterprise software licensing systems.

Typical Software

- AutoCAD
- MATLAB
- ArcGIS
- Siemens NX
- ANSYS

Typical Deployment

```text
Engineering Workstations

        │

License Request

        ▼

FlexLM Server

        │

License Database

        ▼

Software Activation
```

Security Recommendations

- Restrict license server access.
- Monitor abnormal license requests.
- Prevent Internet exposure.
- Maintain software updates.

---

## Port 745 — RSA SecurID

RSA SecurID provides multi-factor authentication for enterprise environments.

Typical Architecture

```text
User

   │

Token Code

   ▼

RSA Authentication Manager

   │

Identity Verification

   ▼

Protected Resource
```

Common Uses

- VPN Authentication
- Remote Access
- Enterprise Login
- Administrative Portals

Security Recommendations

- Enforce MFA.
- Protect token databases.
- Audit authentication logs.
- Restrict administrative interfaces.

---

## Port 755 — DCE/RPC Services

Distributed Computing Environment (DCE) Remote Procedure Calls support communication between distributed applications.

Common Environments

- Enterprise middleware
- Legacy UNIX
- Distributed applications
- Mainframe integration

Security Risks

- Remote procedure abuse
- Service enumeration
- Information disclosure

Example Scan

```bash
nmap -sV -p755 target
```

Security Recommendations

- Restrict RPC exposure.
- Filter external access.
- Enable host-based firewalls.
- Monitor unusual RPC activity.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 743 | Enterprise License Server |
| 745 | Multi-Factor Authentication |
| 747–750 | Kerberos Infrastructure |
| 755 | Distributed RPC Environment |

---

# Blue Team Perspective

Recommended Actions

- Secure Kerberos administrative services.
- Disable legacy authentication protocols.
- Protect enterprise license servers.
- Restrict RPC communications.
- Monitor authentication anomalies.
- Audit privileged administrative activity.

---

# Red Team Perspective

Interesting Targets

### Ports 747–750

Possible Findings

- Kerberos realms
- Identity infrastructure
- Domain authentication
- Legacy UNIX authentication

Potential Opportunities

- Kerberos enumeration
- Legacy protocol identification
- Authentication topology mapping

---

### Port 743

Possible Findings

- Engineering environments
- Software licensing infrastructure
- High-value development systems

---

### Port 745

Possible Findings

- Enterprise MFA deployment
- VPN authentication servers
- Remote access infrastructure

---

### Port 755

Possible Findings

- Middleware platforms
- Distributed applications
- RPC-based services

Useful Enumeration

```bash
nmap -sV -p743,745,747-750,755 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p741-760 target
```

Version Detection

```bash
nmap -sV -p743,745,747-750,755 target
```

Default Script Scan

```bash
nmap -sC -sV -p743,745,755 target
```

Aggressive Scan

```bash
nmap -A -p741-760 target
```

---

# Summary

Ports **741–760** include enterprise authentication services, licensing infrastructure, distributed computing technologies, and legacy network protocols. **Ports 747–750** are especially valuable because they often reveal Kerberos administrative components that accompany enterprise identity systems. **Port 743** frequently identifies FlexLM license servers used by engineering organizations, while **Port 745** may expose RSA SecurID authentication infrastructure. **Port 755** indicates DCE/RPC services commonly found in legacy distributed computing environments. Together, these ports provide important indicators of enterprise authentication, licensing, and middleware architectures.

---

# Ports 761–780

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 761 | TCP | KRBPROP | Kerberos Propagation | MIT Kerberos | Database Replication | Restrict replication traffic. |
| 762 | TCP | KRBUPDATE | Kerberos Updates | Kerberos KDC | Identity Synchronization | Internal authentication only. |
| 763 | TCP | RRS | Resource Reservation Service | Enterprise Systems | Resource Allocation | Vendor-specific implementation. |
| 764 | TCP | CU-SeeMe | Video Conferencing | Legacy Collaboration | Multimedia | Rarely encountered today. |
| 765 | TCP | Webster | Configuration Distribution | JavaSpaces, Jini | Service Discovery | Restrict trusted clients. |
| 766 | TCP | PhoneBook | Directory Service | Enterprise Platforms | Contact Management | Internal deployment. |
| 767 | TCP | PhoneBook-SSL | Secure Directory Service | Enterprise Platforms | Secure Contact Directory | Require TLS. |
| 768 | TCP | GWR | GroupWise Routing | Novell GroupWise | Email Routing | Secure mail infrastructure. |
| 769 | TCP | VID | Video Distribution | Multimedia Platforms | Streaming | Protect media servers. |
| 770 | TCP | CADLock | CAD Licensing | Engineering Software | License Management | Restrict administrator access. |
| 771 | TCP | RTIP | Real-Time Information Protocol | Industrial Systems | Monitoring | Internal network only. |
| 772 | TCP | Cybro | Industrial Controller | PLC Systems | Automation | Segment OT networks. |
| 773 | TCP | Submit | Vendor Messaging | Enterprise Middleware | Message Delivery | Vendor-specific deployment. |
| 774 | TCP | RPass | Remote Password Service | Identity Systems | Password Management | Strong authentication required. |
| 775 | TCP | Moira Database | MIT Moira | Identity Management | User Administration | Restrict administrative access. |
| 776 | TCP | Moira Update | MIT Moira | Configuration Updates | Identity Infrastructure | Internal communications only. |
| 777 | TCP | Multiling HTTP | Application Service | Enterprise Software | Web Services | Verify implementation. |
| 778 | TCP | InterBase | Firebird / InterBase | Database Server | Relational Database | Patch database services. |
| 779 | TCP | IBM Network | Enterprise Systems | IBM Infrastructure | Vendor Service | Internal deployment. |
| 780 | TCP | WPGS | Wireless Gateway | Wireless Infrastructure | Gateway Management | Secure administrative interfaces. |

---

# Port Spotlight

## Port 778 — InterBase / Firebird Database

Port **778** is associated with **InterBase** and some **Firebird** database deployments.

Although less common than MySQL, PostgreSQL, or Microsoft SQL Server, these databases are still found in industrial applications, ERP software, healthcare systems, and embedded enterprise solutions.

Common Software

- InterBase
- Firebird SQL
- Embedded ERP Applications
- Legacy Business Software

Typical Architecture

```text
Application

      │

SQL Queries

      ▼

Firebird / InterBase

      │

Database Files

      ▼

Storage
```

Example Scan

```bash
nmap -sV -p778 target
```

Useful NSE Scripts

```bash
nmap --script banner -p778 target
```

Security Risks

- Weak database credentials
- Information disclosure
- Outdated database engines
- Sensitive business data exposure

Security Recommendations

- Enforce strong authentication.
- Restrict database access.
- Encrypt client connections.
- Apply vendor security patches.

---

## Port 772 — Industrial Controller

Port **772** may appear on industrial automation devices and programmable logic controllers (PLCs).

Typical Environments

- Manufacturing
- Smart Factory
- Water Treatment
- Utilities
- Industrial Control Systems

Typical Architecture

```text
SCADA

   │

Industrial Protocol

   ▼

PLC

   │

Sensors

Actuators

Motors
```

Security Recommendations

- Separate OT from IT networks.
- Disable unused services.
- Monitor industrial communications.
- Limit engineering workstation access.

---

## Ports 775–776 — MIT Moira

Moira is an identity and account management system originally developed at MIT.

Typical Functions

- User account management
- Group administration
- Host configuration
- Access control
- Identity synchronization

Typical Workflow

```text
Administrator

      │

User Changes

      ▼

Moira Server

      │

Synchronization

      ▼

Authentication Systems
```

Security Recommendations

- Restrict administrator accounts.
- Audit configuration changes.
- Encrypt management traffic.
- Integrate with centralized logging.

---

## Port 780 — Wireless Gateway

Wireless gateway services frequently bridge wireless networks with enterprise infrastructure.

Typical Deployment

```text
Wireless Clients

       │

Wi-Fi

       ▼

Wireless Gateway

       │

Firewall

       ▼

Enterprise LAN
```

Common Uses

- Enterprise Wi-Fi
- Campus Networks
- Guest Networks
- IoT Infrastructure

Security Recommendations

- Enable WPA3 where supported.
- Restrict management interfaces.
- Monitor wireless associations.
- Disable insecure legacy protocols.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 772 | Industrial Automation |
| 775–776 | Enterprise Identity Management |
| 778 | Firebird / InterBase Database |
| 780 | Wireless Infrastructure |

---

# Blue Team Perspective

Recommended Actions

- Protect industrial control systems.
- Harden database servers.
- Audit identity management changes.
- Secure wireless gateway devices.
- Monitor administrator activity.
- Segment critical infrastructure.

---

# Red Team Perspective

Interesting Targets

### Port 772

Possible Findings

- PLC devices
- Industrial automation
- Manufacturing systems

---

### Ports 775–776

Possible Findings

- Identity management servers
- User provisioning systems
- Enterprise access control

---

### Port 778

Possible Findings

- Firebird databases
- Legacy ERP applications
- Business management software

Possible Enumeration

```bash
nmap --script banner -p778 target
```

---

### Port 780

Possible Findings

- Wireless controllers
- Enterprise Wi-Fi gateways
- Campus networking equipment

Useful Enumeration

```bash
nmap -sV -p772,775-780 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p761-780 target
```

Version Detection

```bash
nmap -sV -p772,778,780 target
```

Default Script Scan

```bash
nmap -sC -sV -p772,778 target
```

Aggressive Scan

```bash
nmap -A -p761-780 target
```

---

# Summary

Ports **761–780** primarily include enterprise identity services, industrial automation, legacy collaboration platforms, database servers, and wireless infrastructure. **Port 778** is particularly valuable because it often identifies **InterBase** or **Firebird** database servers that may store sensitive enterprise information. **Ports 775–776** can reveal centralized identity management systems, while **Port 772** may indicate industrial control equipment. **Port 780** commonly represents wireless gateway infrastructure that connects enterprise wireless networks to internal systems.

---

# Ports 781–800

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 781 | TCP | HP Device Discovery | HP Enterprise | Device Management | Internal infrastructure only. |
| 782 | TCP | Apache ZooKeeper | Distributed Coordination | Hadoop Ecosystem | Cluster Coordination | Restrict client access. |
| 783 | TCP | SpamAssassin | Mail Filtering | Apache SpamAssassin | Email Security | Internal mail infrastructure. |
| 784 | TCP | Conf Server | Configuration Service | Enterprise Applications | Configuration Management | Authenticate clients. |
| 785 | TCP | Cisco Cluster Manager | Cisco Unified Communications | Cluster Management | VoIP Infrastructure | Restrict administrative access. |
| 786 | TCP | OMS Gateway | Operations Management | Enterprise Monitoring | Monitoring Agents | Internal deployment. |
| 787 | TCP | QSC Audio | Audio Distribution | Q-SYS | Multimedia | Vendor-specific. |
| 788 | TCP | ControlIT | Remote Control Platform | Enterprise Systems | Remote Administration | Secure administrator accounts. |
| 789 | TCP | SKIP Certificate | SKIP Protocol | Legacy VPN | Certificate Exchange | Legacy deployment. |
| 790 | TCP | Unassigned | Reserved | Future Assignment | N/A | Verify actual service. |
| 791 | TCP | Unassigned | Reserved | Future Assignment | N/A | Verify actual service. |
| 792 | TCP | NetNews | News Distribution | Legacy Systems | Message Distribution | Rare deployment. |
| 793 | TCP | Adobe AIR Debug | Adobe Development | Application Debugging | Development | Disable in production. |
| 794 | TCP | Media Management | Enterprise Multimedia | Streaming | Internal deployment. |
| 795 | TCP | Voice Gateway | VoIP Gateway | Unified Communications | Telephony | Secure SIP infrastructure. |
| 796 | TCP | SIP-TLS Auxiliary | Secure VoIP | Voice Infrastructure | Secure Signaling | Require TLS. |
| 797 | TCP | Oracle Listener Extension | Oracle Products | Database Services | Oracle Infrastructure | Restrict trusted hosts. |
| 798 | TCP | WebLogic Internal | Oracle WebLogic | Middleware | Enterprise Applications | Internal use only. |
| 799 | TCP | Secure Messaging | Enterprise Messaging | Collaboration Platforms | Message Routing | Protect message brokers. |
| 800 | TCP | MDBS Daemon | MDBS Database | Database Services | Data Management | Restrict external access. |

---

# Port Spotlight

## Port 782 — Apache ZooKeeper

Apache ZooKeeper is a centralized coordination service used by distributed applications.

It is a critical component in many large-scale platforms.

Common Platforms

- Apache Kafka
- Apache Hadoop
- Apache HBase
- Apache Solr
- Apache Storm

Typical Architecture

```text
Application Nodes

      │

ZooKeeper Client

      ▼

ZooKeeper Cluster

 ┌────┴────┐

Node1 Node2 Node3

      │

Leader Election

Configuration

Distributed Locks
```

Example Scan

```bash
nmap -sV -p782 target
```

Security Risks

- Cluster information disclosure
- Unauthorized node registration
- Configuration manipulation
- Distributed service disruption

Security Recommendations

- Require authentication.
- Enable TLS where supported.
- Restrict client IP addresses.
- Separate coordination traffic from user traffic.

---

## Port 783 — SpamAssassin

SpamAssassin is a widely deployed email filtering system.

Typical Workflow

```text
Internet Mail

      │

SMTP

      ▼

Mail Server

      │

SpamAssassin

      ▼

Inbox

Spam Folder
```

Common Uses

- Spam filtering
- Malware detection
- Email scoring
- Mail gateway protection

Example Scan

```bash
nmap -sV -p783 target
```

Security Recommendations

- Keep spam signatures updated.
- Protect mail gateways.
- Monitor spam scoring anomalies.
- Restrict administrative interfaces.

---

## Port 797 — Oracle Infrastructure

Some Oracle products use auxiliary services within this range for internal communication.

Typical Deployment

```text
Application

      │

Oracle Listener

      ▼

Oracle Database

      │

Storage

Replication

Backup
```

Security Risks

- Database enumeration
- Version disclosure
- Unauthorized access
- Information leakage

Security Recommendations

- Restrict listener access.
- Disable unnecessary Oracle services.
- Patch Oracle software regularly.
- Enable auditing.

---

## Port 800 — MDBS Database

MDBS is a legacy database management system still encountered in certain industrial and embedded environments.

Typical Architecture

```text
Client

   │

Database Request

   ▼

MDBS Server

   │

Storage Engine

   ▼

Database Files
```

Example Scan

```bash
nmap -sV -p800 target
```

Security Recommendations

- Limit database exposure.
- Enforce authentication.
- Perform regular backups.
- Monitor abnormal database activity.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 782 | Distributed Cluster Coordination |
| 783 | Enterprise Mail Filtering |
| 785 | Cisco UC Infrastructure |
| 797 | Oracle Enterprise Services |
| 800 | Legacy Database Platform |

---

# Blue Team Perspective

Recommended Actions

- Secure distributed coordination clusters.
- Harden email filtering systems.
- Restrict Oracle service exposure.
- Protect legacy database servers.
- Audit administrative accounts.
- Continuously monitor enterprise middleware.

---

# Red Team Perspective

Interesting Targets

### Port 782

Possible Findings

- Kafka clusters
- Hadoop infrastructure
- Distributed applications
- Container orchestration support services

Potential Enumeration

- Cluster topology
- Leader election status
- Configuration endpoints

---

### Port 783

Possible Findings

- Corporate email gateway
- Spam filtering infrastructure
- Secure mail environment

---

### Port 797

Possible Findings

- Oracle databases
- Enterprise middleware
- Business-critical applications

---

### Port 800

Possible Findings

- Legacy business databases
- Industrial applications
- Embedded management platforms

Useful Enumeration

```bash
nmap -sV -p782,783,797,800 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p781-800 target
```

Version Detection

```bash
nmap -sV -p782,783,797,800 target
```

Default Script Scan

```bash
nmap -sC -sV -p782,797,800 target
```

Aggressive Scan

```bash
nmap -A -p781-800 target
```

---

# Summary

Ports **781–800** are commonly associated with distributed computing platforms, enterprise messaging, unified communications, Oracle infrastructure, and legacy database systems. **Port 782 (Apache ZooKeeper)** is especially significant because it frequently identifies distributed clusters such as Kafka or Hadoop deployments. **Port 783** often represents enterprise email filtering infrastructure, while **Port 797** may expose Oracle middleware components. **Port 800** is less common but can reveal legacy database platforms supporting older enterprise or industrial applications.

---

# Ports 801–820

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 801 | TCP | Device Management | Embedded Management | Network Appliances | Administration | Restrict management interfaces. |
| 802 | TCP | MODBUS/TCP Alternative | Industrial Communication | ICS Devices | Process Automation | Segment OT environments. |
| 803 | TCP | FCP | File Control Protocol | Enterprise Applications | File Management | Vendor-specific implementation. |
| 804 | TCP | Unassigned | Reserved | Future Use | N/A | Verify detected service. |
| 805 | TCP | Device Gateway | Gateway Service | Embedded Systems | Device Connectivity | Internal deployment. |
| 806 | TCP | Remote Installer | Software Deployment | Enterprise Platforms | Remote Installation | Restrict administrator access. |
| 807 | TCP | Secure Gateway | Encrypted Gateway | Security Appliances | Secure Communications | Require TLS. |
| 808 | TCP | CCProxy | Proxy Service | CCProxy | HTTP Proxy | Monitor proxy usage. |
| 809 | TCP | FCP-UDP | File Control | Enterprise Middleware | Data Exchange | Vendor-specific deployment. |
| 810 | TCP | FCP Control | File Control Service | Enterprise Systems | File Administration | Restrict trusted clients. |
| 811 | TCP | CP Cluster | Cluster Service | Enterprise Applications | High Availability | Internal traffic only. |
| 812 | TCP | VMware Directory | VMware Products | Virtualization | Infrastructure Services | Secure virtualization environment. |
| 813 | TCP | Policy Server | Security Policy | NAC Solutions | Access Control | Protect policy databases. |
| 814 | TCP | Puppet | Puppet Agent | Puppet | Configuration Management | Restrict agent communication. |
| 815 | TCP | Device Provisioning | Embedded Devices | IoT Platforms | Device Enrollment | Authenticate endpoints. |
| 816 | TCP | Automated Deployment | Enterprise Automation | Deployment Tools | Software Rollout | Restrict administrative access. |
| 817 | TCP | Secure Provisioning | Device Enrollment | Enterprise Systems | Certificate Provisioning | Protect PKI infrastructure. |
| 818 | TCP | IT Asset Service | Asset Management | Enterprise Platforms | Inventory | Internal deployment. |
| 819 | TCP | Monitoring Channel | Monitoring | Enterprise Monitoring | Telemetry | Secure monitoring traffic. |
| 820 | TCP | LM PerfWorks | Performance Monitoring | HP/OpenView | Performance Analysis | Restrict management hosts. |

---

# Port Spotlight

## Port 808 — HTTP Proxy Services

Port **808** has historically been used by various HTTP proxy services, including **CCProxy**, although many organizations also use nearby ports such as **8080** for web proxies.

Proxy servers provide:

- Internet access control
- Content filtering
- User authentication
- Traffic logging
- Bandwidth management

Typical Architecture

```text
Client

   │

HTTP Request

   ▼

Proxy Server

   │

Filtering

Authentication

Caching

   ▼

Internet
```

Example Scan

```bash
nmap -sV -p808 target
```

Security Risks

- Open proxy abuse
- Anonymous Internet access
- Traffic interception
- Credential exposure

Security Recommendations

- Require user authentication.
- Disable open proxy functionality.
- Restrict internal users.
- Monitor outbound traffic.

---

## Port 812 — VMware Infrastructure

Port **812** may appear in VMware-related environments supporting virtualization management.

Common Components

- VMware ESXi
- VMware vCenter
- VMware Tools
- Virtual Infrastructure Services

Typical Architecture

```text
Administrator

      │

Management

      ▼

vCenter

      │

ESXi Hosts

      ▼

Virtual Machines
```

Example Scan

```bash
nmap -sV -p812 target
```

Security Recommendations

- Protect management networks.
- Enable multifactor authentication.
- Keep hypervisors updated.
- Audit administrative sessions.

---

## Port 814 — Puppet Configuration Management

Puppet is a widely used Infrastructure-as-Code (IaC) and configuration management platform.

Common Uses

- Server configuration
- Automated deployments
- Compliance management
- Patch automation
- Cloud infrastructure

Typical Workflow

```text
Administrator

      │

Policies

      ▼

Puppet Server

      │

Configuration

      ▼

Managed Nodes
```

Example Scan

```bash
nmap -sV -p814 target
```

Security Risks

- Unauthorized agent enrollment
- Configuration tampering
- Certificate abuse
- Privilege escalation

Security Recommendations

- Enforce mutual TLS.
- Rotate certificates regularly.
- Restrict agent registration.
- Audit configuration changes.

---

## Port 820 — Performance Monitoring

Port **820** is occasionally associated with enterprise performance monitoring platforms.

Typical Environment

```text
Servers

Applications

Network Devices

       │

Metrics

       ▼

Monitoring Server

       │

Dashboards

Alerts

Reports
```

Common Uses

- Capacity planning
- Performance analysis
- Infrastructure monitoring
- SLA reporting

Security Recommendations

- Restrict monitoring consoles.
- Protect collected metrics.
- Encrypt management sessions.
- Enable detailed logging.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 808 | HTTP Proxy Infrastructure |
| 812 | VMware Environment |
| 814 | Puppet Configuration Management |
| 820 | Enterprise Performance Monitoring |

---

# Blue Team Perspective

Recommended Actions

- Disable open proxy functionality.
- Protect virtualization management services.
- Secure Puppet certificate infrastructure.
- Restrict monitoring platforms.
- Audit privileged administrator activity.
- Segment management networks.

---

# Red Team Perspective

Interesting Targets

### Port 808

Possible Findings

- Enterprise proxy server
- Content filtering gateway
- Internet access infrastructure

Potential Enumeration

- Proxy authentication methods
- Banner information
- Supported HTTP methods

---

### Port 812

Possible Findings

- VMware infrastructure
- Virtualization management
- Enterprise datacenter

---

### Port 814

Possible Findings

- Configuration management server
- Infrastructure-as-Code platform
- Automated deployment system

---

### Port 820

Possible Findings

- Enterprise monitoring platform
- Performance analytics
- Infrastructure dashboards

Useful Enumeration

```bash
nmap -sV -p808,812,814,820 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p801-820 target
```

Version Detection

```bash
nmap -sV -p808,812,814,820 target
```

Default Script Scan

```bash
nmap -sC -sV -p808,814 target
```

Aggressive Scan

```bash
nmap -A -p801-820 target
```

---

# Summary

Ports **801–820** are commonly associated with enterprise management platforms, virtualization, configuration management, proxy services, and monitoring infrastructure. **Port 808** frequently indicates HTTP proxy services that can reveal an organization's Internet access architecture. **Port 812** may identify VMware-based virtualization environments, while **Port 814 (Puppet)** is a strong indicator of Infrastructure-as-Code and automated configuration management. **Port 820** often supports performance monitoring platforms used to collect operational metrics from servers, applications, and network devices.

---

# Ports 821–840

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 821 | TCP | CP Cluster | Cluster Communication | Enterprise Clusters | High Availability | Restrict cluster traffic. |
| 822 | TCP | VMware Authentication | VMware Infrastructure | Virtualization | Authentication | Secure management network. |
| 823 | TCP | IBM Tivoli Agent | IBM Tivoli | Systems Monitoring | Enterprise Monitoring | Internal deployment only. |
| 824 | TCP | Network Appliance Sync | Storage Systems | Replication | NAS Synchronization | Restrict replication traffic. |
| 825 | TCP | Device Configuration | Embedded Systems | Configuration Management | Device Administration | Authenticate administrators. |
| 826 | TCP | Security Agent | Endpoint Protection | EDR Platforms | Endpoint Monitoring | Protect agent communications. |
| 827 | TCP | PKI Enrollment | Certificate Services | Enterprise PKI | Certificate Provisioning | Require mutual authentication. |
| 828 | TCP | Oracle Secure Service | Oracle Products | Enterprise Middleware | Internal Oracle Services | Restrict trusted hosts. |
| 829 | TCP | MikroTik Winbox | MikroTik RouterOS | Router Administration | Network Management | Restrict administrator access. |
| 830 | TCP | NETCONF over SSH | Cisco, Juniper, Arista | Network Automation | Device Configuration | Use SSH authentication. |
| 831 | TCP | Device Discovery | Enterprise Appliances | Asset Discovery | Network Inventory | Internal deployment. |
| 832 | TCP | Policy Distribution | Security Appliances | Policy Synchronization | Centralized Management | Encrypt synchronization traffic. |
| 833 | TCP | Bitcoin RPC | Bitcoin Core | Cryptocurrency Node | Blockchain Management | Restrict RPC access. |
| 834 | TCP | Secure Replication | Enterprise Storage | Data Synchronization | Storage Infrastructure | Internal traffic only. |
| 835 | TCP | Automation Service | Enterprise Automation | Workflow Platforms | Task Automation | Authenticate API clients. |
| 836 | TCP | Event Collector | Monitoring Platforms | Log Collection | SIEM Integration | Protect log integrity. |
| 837 | TCP | Backup Controller | Enterprise Backup | Backup Management | Disaster Recovery | Restrict administrator access. |
| 838 | TCP | Secure Messaging | Enterprise Messaging | Internal Communication | Messaging Infrastructure | Encrypt communications. |
| 839 | TCP | Directory Sync | Identity Platforms | Directory Replication | Identity Management | Protect replication traffic. |
| 840 | TCP | Identity Gateway | IAM Platforms | Authentication Gateway | Identity Services | Require strong authentication. |

---

# Port Spotlight

## Port 829 — MikroTik Winbox

Port **829** is the default management port for **MikroTik RouterOS Winbox**, one of the most widely used router administration tools.

Winbox provides:

- Router configuration
- Firewall management
- VPN configuration
- Routing configuration
- Interface monitoring

Common Devices

- MikroTik RouterBOARD
- CCR Series
- CRS Switches
- hAP Series
- Cloud Hosted Router (CHR)

Typical Architecture

```text
Administrator

      │

 Winbox

      ▼

MikroTik Router

      │

Firewall

Routing

VPN

QoS

      ▼

Enterprise Network
```

Example Scan

```bash
nmap -sV -p829 target
```

Useful NSE Scripts

```bash
nmap --script banner -p829 target
```

Security Risks

- Default credentials
- Outdated RouterOS vulnerabilities
- Configuration disclosure
- Router compromise

Security Recommendations

- Restrict Winbox to management VLANs.
- Disable public Internet access.
- Enable multifactor authentication where possible.
- Update RouterOS regularly.

---

## Port 830 — NETCONF over SSH

NETCONF is a modern network configuration protocol standardized by the IETF.

Unlike SNMP, NETCONF supports full configuration management.

Common Vendors

- Cisco
- Juniper
- Nokia
- Huawei
- Arista

Typical Workflow

```text
Automation Server

        │

 NETCONF/SSH

        ▼

Network Device

        │

Configuration

        ▼

Running Config

Startup Config
```

Example Scan

```bash
nmap -sV -p830 target
```

Security Recommendations

- Require SSH key authentication.
- Restrict management hosts.
- Log configuration changes.
- Disable unused management interfaces.

---

## Port 833 — Bitcoin RPC

Bitcoin Core exposes RPC services that allow administrators and applications to interact with blockchain nodes.

Typical Uses

- Wallet management
- Transaction creation
- Blockchain synchronization
- Mining control
- Node administration

Typical Architecture

```text
Administrator

      │

JSON-RPC

      ▼

Bitcoin Core

      │

Blockchain

Wallet

Mempool

      ▼

Peer Network
```

Security Risks

- Wallet theft
- Unauthorized transactions
- Private key exposure
- Remote node compromise

Example Scan

```bash
nmap -sV -p833 target
```

Security Recommendations

- Never expose RPC publicly.
- Restrict trusted IP addresses.
- Enable strong authentication.
- Encrypt management traffic.

---

## Port 840 — Identity Gateway

Identity gateways centralize authentication and authorization for enterprise applications.

Common Functions

- Single Sign-On (SSO)
- MFA Integration
- Identity Federation
- OAuth
- OpenID Connect

Typical Architecture

```text
User

 │

Authentication

 ▼

Identity Gateway

 │

Identity Provider

 │

Enterprise Applications
```

Security Recommendations

- Enable multifactor authentication.
- Audit authentication logs.
- Restrict administrative access.
- Monitor federation trust relationships.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 829 | MikroTik RouterOS |
| 830 | Network Automation Infrastructure |
| 833 | Bitcoin Node |
| 840 | Enterprise Identity Gateway |

---

# Blue Team Perspective

Recommended Actions

- Restrict RouterOS management access.
- Protect NETCONF interfaces.
- Disable public blockchain RPC access.
- Harden identity gateways.
- Monitor administrative logins.
- Enable centralized logging.

---

# Red Team Perspective

Interesting Targets

### Port 829

Possible Findings

- MikroTik routers
- ISP infrastructure
- Wireless ISP equipment
- Branch office gateways

Potential Enumeration

- RouterOS version
- Banner information
- Configuration interface

---

### Port 830

Possible Findings

- Enterprise routers
- Automation platforms
- Software-defined networking infrastructure

---

### Port 833

Possible Findings

- Cryptocurrency nodes
- Wallet infrastructure
- Blockchain services

---

### Port 840

Possible Findings

- SSO platforms
- Enterprise identity providers
- Authentication gateways

Useful Enumeration

```bash
nmap -sV -p829,830,833,840 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p821-840 target
```

Version Detection

```bash
nmap -sV -p829,830,833,840 target
```

Default Script Scan

```bash
nmap -sC -sV -p829,830 target
```

Aggressive Scan

```bash
nmap -A -p821-840 target
```

---

# Summary

Ports **821–840** primarily represent modern enterprise management services, network automation, identity management, virtualization, and emerging infrastructure technologies. **Port 829** is a strong indicator of **MikroTik RouterOS** management interfaces, while **Port 830 (NETCONF over SSH)** frequently identifies network automation environments used by enterprise switches and routers. **Port 833** may reveal **Bitcoin Core RPC** services and blockchain infrastructure, and **Port 840** often represents enterprise identity gateways supporting SSO, MFA, and federated authentication. Together, these ports provide valuable insight into an organization's network management, automation, and authentication architecture.

---

# Ports 841–860

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 841 | TCP | CVP | Computer Voice Processing | IVR Systems | Voice Automation | Restrict management access. |
| 842 | TCP | DHCP Failover Mgmt | DHCP Infrastructure | ISC DHCP | Lease Synchronization | Internal networks only. |
| 843 | TCP | Adobe Flash Policy | Adobe Flash | Cross-Domain Policy | Legacy Web Applications | Flash is deprecated. |
| 844 | TCP | CDDBP | CD Database Protocol | Legacy Multimedia | Media Lookup | Rare deployment. |
| 845 | TCP | VMware Management | VMware Components | Virtualization | Infrastructure Services | Protect management interfaces. |
| 846 | TCP | AIS | Application Integration | Enterprise Middleware | Service Integration | Restrict trusted hosts. |
| 847 | TCP | SAP Router Extension | SAP Systems | ERP Communication | SAP Infrastructure | Harden SAP services. |
| 848 | TCP | Group Policy Distribution | Enterprise Windows | Policy Synchronization | Active Directory | Internal deployment. |
| 849 | TCP | PKI Synchronization | Enterprise PKI | Certificate Services | Trust Management | Protect CA infrastructure. |
| 850 | TCP | RTP Media Control | VoIP Platforms | Multimedia | Voice Communications | Encrypt signaling. |
| 851 | TCP | Device Health Monitor | Enterprise Appliances | Monitoring | Device Telemetry | Restrict monitoring access. |
| 852 | TCP | DNS Management | DNS Infrastructure | Enterprise DNS | Administrative Tasks | Internal service only. |
| 853 | TCP | DNS over TLS (DoT) | BIND, Unbound, Knot Resolver, AdGuard Home | Encrypted DNS | Secure Name Resolution | Require TLS and certificate validation. |
| 854 | TCP | RTSP Alternate | Media Servers | Streaming | Multimedia | Restrict anonymous access. |
| 855 | TCP | VMware Sync | VMware Services | Virtualization | Host Synchronization | Internal deployment. |
| 856 | TCP | Enterprise Messaging | Messaging Middleware | Message Brokers | Enterprise Integration | Secure message queues. |
| 857 | TCP | Security Event Bus | SIEM Platforms | Event Collection | Security Monitoring | Protect telemetry data. |
| 858 | TCP | Backup Synchronization | Enterprise Backup | Disaster Recovery | Data Replication | Restrict replication traffic. |
| 859 | TCP | Device Enrollment | Enterprise Devices | Provisioning | Zero-Touch Deployment | Authenticate endpoints. |
| 860 | TCP | ISCSI Management | Storage Systems | SAN Administration | Storage Infrastructure | Restrict storage management. |

---

# Port Spotlight

## Port 843 — Adobe Flash Policy Server

Port **843** historically hosted **Adobe Flash Policy Servers**, allowing Flash applications to retrieve cross-domain access policies.

Although Adobe Flash reached end-of-life in 2020, this port may still appear on legacy environments.

Typical Workflow

```text
Flash Client

      │

Policy Request

      ▼

Policy Server

      │

crossdomain.xml

      ▼

Application Server
```

Example Scan

```bash
nmap -sV -p843 target
```

Security Risks

- Legacy software exposure
- Cross-domain policy misconfiguration
- Information disclosure
- Unsupported software

Security Recommendations

- Remove Flash services.
- Eliminate unnecessary legacy applications.
- Monitor for obsolete web components.
- Replace Flash-based applications.

---

## Port 853 — DNS over TLS (DoT)

Port **853** is officially assigned to **DNS over TLS (DoT)**, an encrypted protocol that protects DNS queries from interception and manipulation.

Unlike traditional DNS on port **53**, DoT encrypts all DNS traffic using TLS.

Common Software

- Unbound
- BIND 9
- Knot Resolver
- AdGuard Home
- Stubby

Typical Architecture

```text
Client

   │

TLS

   ▼

DNS Resolver

   │

Encrypted DNS Queries

   ▼

Authoritative DNS
```

Example Scan

```bash
nmap -sV -p853 target
```

Useful NSE Scripts

```bash
nmap --script ssl-cert -p853 target
```

Security Risks

- Certificate misconfiguration
- Weak TLS configuration
- DNS fingerprinting
- Unauthorized resolvers

Security Recommendations

- Enforce TLS 1.2 or newer.
- Use trusted certificates.
- Disable weak cipher suites.
- Monitor resolver logs.

---

## Port 860 — iSCSI Management

Port **860** is sometimes encountered in storage management environments supporting iSCSI or SAN infrastructure.

Typical Architecture

```text
Application Server

        │

iSCSI

        ▼

Storage Controller

        │

SAN

        ▼

Disk Arrays
```

Common Uses

- Enterprise storage
- Virtualization clusters
- Backup infrastructure
- Shared storage

Security Recommendations

- Isolate storage networks.
- Require CHAP authentication.
- Restrict management interfaces.
- Monitor storage access logs.

---

## Port 845 — VMware Infrastructure

VMware environments may expose auxiliary management services within this range.

Common Components

- ESXi
- vCenter
- vMotion
- Host Management

Security Recommendations

- Protect management VLANs.
- Enable MFA.
- Restrict administrator IP addresses.
- Keep VMware software updated.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 843 | Legacy Flash Infrastructure |
| 845 | VMware Environment |
| 853 | DNS over TLS Resolver |
| 860 | Enterprise Storage Infrastructure |

---

# Blue Team Perspective

Recommended Actions

- Remove obsolete Flash services.
- Harden DNS over TLS deployments.
- Secure virtualization management interfaces.
- Isolate storage networks.
- Monitor privileged administrative access.
- Enable centralized logging for infrastructure services.

---

# Red Team Perspective

Interesting Targets

### Port 843

Possible Findings

- Legacy web applications
- Deprecated Flash deployments
- Unsupported middleware

---

### Port 853

Possible Findings

- Internal DNS resolvers
- Privacy-focused DNS infrastructure
- Recursive resolvers

Potential Enumeration

```bash
nmap --script ssl-cert -p853 target
```

---

### Port 845

Possible Findings

- VMware infrastructure
- Hypervisor management
- Enterprise virtualization

---

### Port 860

Possible Findings

- SAN controllers
- Shared storage
- Backup repositories
- Virtualization storage

Useful Enumeration

```bash
nmap -sV -p845,853,860 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p841-860 target
```

Version Detection

```bash
nmap -sV -p843,845,853,860 target
```

Default Script Scan

```bash
nmap -sC -sV -p853,860 target
```

SSL Certificate Inspection

```bash
nmap --script ssl-cert -p853 target
```

Aggressive Scan

```bash
nmap -A -p841-860 target
```

---

# Summary

Ports **841–860** include enterprise middleware, virtualization, storage infrastructure, legacy web technologies, and secure DNS services. **Port 853 (DNS over TLS)** is particularly important because it identifies encrypted DNS resolvers that improve privacy and integrity compared to traditional DNS. **Port 843** often reveals obsolete Flash-based environments that should be retired, while **Ports 845** and **860** commonly indicate VMware and enterprise storage infrastructures. Together, these ports help identify critical backend services supporting modern enterprise networks.

---

# Ports 861–880

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 861 | TCP | iSCSI Target Mgmt | Storage Management | SAN Platforms | Storage Administration | Restrict management networks. |
| 862 | TCP | OSPF Management | Routing Infrastructure | Enterprise Routers | Routing Control | Internal deployment only. |
| 863 | TCP | HTTP Device API | Embedded Devices | IoT Platforms | Device Management | Require authentication. |
| 864 | TCP | Secure Device Control | Enterprise Appliances | Remote Administration | Management Interface | Protect administrator accounts. |
| 865 | TCP | SDO | Service Data Objects | Industrial Systems | Device Configuration | Segment OT networks. |
| 866 | TCP | DCA | Distributed Control | Industrial Controllers | Automation | Internal communications only. |
| 867 | TCP | ArcServe Discovery | ArcServe Backup | Backup Infrastructure | Discovery Services | Restrict trusted hosts. |
| 868 | TCP | Messaging Sync | Enterprise Middleware | Synchronization | Internal Messaging | Encrypt synchronization traffic. |
| 869 | TCP | RPC Gateway | Enterprise Middleware | Remote Procedures | Internal Applications | Restrict external exposure. |
| 870 | TCP | VMware Auxiliary | VMware Services | Virtualization | Infrastructure Support | Secure management traffic. |
| 871 | TCP | Automation Agent | DevOps Platforms | Agent Communication | Infrastructure Automation | Authenticate agents. |
| 872 | TCP | rsync | rsync | File Synchronization | Backup & Replication | Restrict anonymous access. |
| 873 | TCP | rsync Daemon | rsync | Remote File Synchronization | Linux/UNIX | Authenticate clients and limit modules. |
| 874 | TCP | Security Telemetry | SIEM Platforms | Event Collection | Monitoring | Protect telemetry integrity. |
| 875 | TCP | Monitoring API | Monitoring Systems | API Access | Observability | Restrict API tokens. |
| 876 | TCP | Cluster Database | Cluster Infrastructure | Database Clusters | Synchronization | Internal cluster only. |
| 877 | TCP | Device Enrollment | Enterprise Devices | Provisioning | Zero-Touch Deployment | Verify device identity. |
| 878 | TCP | Backup Verification | Enterprise Backup | Integrity Checking | Disaster Recovery | Protect backup metadata. |
| 879 | TCP | Certificate Gateway | PKI Infrastructure | Certificate Distribution | Enterprise Security | Protect certificate authorities. |
| 880 | TCP | Secure Control Channel | Enterprise Platforms | Administrative Control | Infrastructure Management | Restrict administrative access. |

---

# Port Spotlight

## Port 873 — rsync

Port **873** is officially assigned to **rsync**, one of the most widely used file synchronization utilities on Linux and UNIX systems.

It provides efficient file transfers by transmitting only changed data blocks.

Common Software

- rsync
- Linux Backup Servers
- NAS Appliances
- Embedded Linux Devices

Typical Uses

- File synchronization
- Incremental backups
- Website deployment
- Disaster recovery
- Repository mirroring

Typical Architecture

```text
Client

   │

rsync Protocol

   ▼

rsync Daemon

   │

File Modules

   ▼

Storage
```

Example Scan

```bash
nmap -sV -p873 target
```

Useful NSE Scripts

```bash
nmap --script rsync-list-modules -p873 target
```

Security Risks

- Anonymous file access
- Information disclosure
- Backup leakage
- Weak authentication

Security Recommendations

- Disable anonymous modules.
- Require authentication.
- Restrict trusted IP ranges.
- Encrypt transfers through SSH when possible.

---

## Port 872 — File Synchronization Services

Port **872** is occasionally used by vendor-specific synchronization services and may also appear alongside rsync deployments.

Typical Environment

```text
Primary Server

      │

Synchronization

      ▼

Secondary Server

      │

Updated Files

      ▼

Clients
```

Security Recommendations

- Restrict synchronization traffic.
- Validate replicated data.
- Monitor synchronization failures.
- Protect backup infrastructure.

---

## Port 879 — Certificate Gateway

Certificate distribution gateways support enterprise Public Key Infrastructure (PKI).

Typical Functions

- Certificate enrollment
- Certificate renewal
- Trust distribution
- CRL publishing
- Identity verification

Typical Architecture

```text
Client

   │

Certificate Request

   ▼

PKI Gateway

   │

Certificate Authority

   ▼

Issued Certificate
```

Security Recommendations

- Protect Certificate Authorities.
- Enable certificate auditing.
- Require mutual TLS.
- Rotate intermediate certificates.

---

## Port 870 — VMware Auxiliary Services

Large VMware deployments may expose additional support services around this range.

Common Components

- ESXi Hosts
- vCenter
- Backup Connectors
- Monitoring Agents

Security Recommendations

- Restrict management VLANs.
- Disable unused services.
- Enable MFA for administrators.
- Monitor API access.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 870 | VMware Infrastructure |
| 872 | File Synchronization |
| 873 | rsync Service |
| 879 | Enterprise PKI |
| 880 | Administrative Control Channel |

---

# Blue Team Perspective

Recommended Actions

- Disable anonymous rsync modules.
- Protect backup repositories.
- Restrict VMware management access.
- Secure PKI infrastructure.
- Monitor synchronization failures.
- Audit privileged administrator activity.

---

# Red Team Perspective

Interesting Targets

### Port 873

Possible Findings

- Backup repositories
- Source code mirrors
- Website deployment servers
- File synchronization services

Potential Enumeration

```bash
nmap --script rsync-list-modules -p873 target
```

---

### Port 870

Possible Findings

- VMware infrastructure
- Virtualization management
- Enterprise datacenter

---

### Port 879

Possible Findings

- Certificate Authorities
- Enterprise PKI
- Certificate enrollment services

---

### Ports 872–873

Possible Findings

- File replication servers
- Backup infrastructure
- Shared storage
- Linux administration servers

Useful Enumeration

```bash
nmap -sV -p872,873,879 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p861-880 target
```

Version Detection

```bash
nmap -sV -p870,872,873,879 target
```

Default Script Scan

```bash
nmap -sC -sV -p873 target
```

Enumerate rsync Modules

```bash
nmap --script rsync-list-modules -p873 target
```

Aggressive Scan

```bash
nmap -A -p861-880 target
```

---

# Summary

Ports **861–880** primarily represent enterprise storage, synchronization, virtualization, PKI, and automation infrastructure. **Port 873 (rsync)** is particularly important because it commonly exposes backup repositories, file synchronization services, and deployment servers across Linux and UNIX environments. **Ports 870** and **879** may reveal VMware management components and enterprise PKI infrastructure, while **Port 872** often indicates synchronization services supporting backup or replication. These ports frequently identify critical backend systems that should be tightly controlled and continuously monitored.

---

# Ports 881–900

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 881 | TCP | Secure Device Manager | Enterprise Appliances | Device Administration | Infrastructure Management | Restrict administrative access. |
| 882 | TCP | VMware Event Service | VMware Infrastructure | Event Collection | Virtualization | Internal deployment only. |
| 883 | TCP | Nessus | Tenable Nessus | Vulnerability Assessment | Security Scanning | Restrict scanner access. |
| 884 | TCP | HTTPS Alternate | Secure Web Service | Enterprise Applications | Web Administration | Require TLS. |
| 885 | TCP | DRMSFSD | Distributed Resource Manager | Enterprise Platforms | Resource Scheduling | Internal communication only. |
| 886 | TCP | Backup Agent | Enterprise Backup | Backup Operations | Disaster Recovery | Authenticate backup agents. |
| 887 | TCP | Secure Messaging Bus | Middleware | Internal Messaging | Enterprise Integration | Encrypt communications. |
| 888 | TCP | AccessBuilder | Enterprise Access Control | Identity Systems | Authentication | Restrict privileged users. |
| 889 | TCP | cddbp-alt | Multimedia Database | Legacy Applications | Metadata Lookup | Rare deployment. |
| 890 | TCP | JMB-CDS1 | Management Service | Enterprise Platforms | Control Channel | Vendor-specific implementation. |
| 891 | TCP | JMB-CDS2 | Control Service | Enterprise Systems | Device Coordination | Internal deployment. |
| 892 | TCP | Lotus Notes Remote | HCL Domino | Collaboration | Messaging Infrastructure | Secure remote access. |
| 893 | TCP | VMware Sync | VMware Components | Infrastructure Synchronization | Virtualization | Restrict synchronization traffic. |
| 894 | TCP | Telemetry Channel | Monitoring Platforms | Metrics Collection | Observability | Protect telemetry data. |
| 895 | TCP | Policy Distribution | NAC Platforms | Security Policy | Central Management | Authenticate endpoints. |
| 896 | TCP | Backup Replication | Backup Infrastructure | Data Replication | Disaster Recovery | Encrypt replication traffic. |
| 897 | TCP | Secure Provisioning | Enterprise Devices | Device Enrollment | Infrastructure Automation | Verify device identity. |
| 898 | TCP | Storage Controller | Enterprise Storage | Storage Management | SAN Infrastructure | Restrict management interfaces. |
| 899 | TCP | Remote Configuration | Enterprise Appliances | Configuration Management | Administration | Internal deployment. |
| 900 | TCP | OMGINIT | CORBA Initialization | Enterprise Middleware | Distributed Applications | Restrict middleware exposure. |

---

# Port Spotlight

## Port 883 — Nessus

Port **883** is commonly associated with the **Tenable Nessus** vulnerability scanner.

Nessus is one of the most widely used vulnerability assessment platforms in enterprise environments.

Common Features

- Vulnerability scanning
- Compliance auditing
- Configuration assessment
- Patch verification
- Asset discovery

Common Software

- Tenable Nessus Professional
- Tenable Security Center
- Tenable.io Scanner

Typical Architecture

```text
Administrator

      │

HTTPS

      ▼

Nessus Server

      │

Scan Engine

      ▼

Target Systems

Servers

Workstations

Network Devices
```

Example Scan

```bash
nmap -sV -p883 target
```

Useful NSE Scripts

```bash
nmap --script http-title -p883 target
```

Security Risks

- Scanner compromise
- Stored vulnerability reports
- Credential exposure
- Administrative interface abuse

Security Recommendations

- Restrict Nessus to management networks.
- Enable multifactor authentication.
- Rotate scanning credentials.
- Keep plugins updated.

---

## Port 892 — HCL Domino / Lotus Notes

Port **892** may appear in environments using **HCL Domino (formerly IBM Lotus Notes)**.

Typical Uses

- Enterprise email
- Collaboration
- Document databases
- Workflow automation

Typical Architecture

```text
Users

   │

Notes Client

   ▼

Domino Server

   │

Mail

Applications

Replication

   ▼

Enterprise Network
```

Security Recommendations

- Require encrypted client sessions.
- Patch Domino servers regularly.
- Restrict remote administration.
- Monitor authentication failures.

---

## Port 898 — Storage Controller

Storage controllers coordinate access to enterprise storage resources.

Typical Environment

```text
Application Servers

        │

Storage Requests

        ▼

Storage Controller

        │

SAN

NAS

Disk Arrays

        ▼

Persistent Storage
```

Common Uses

- SAN management
- Storage virtualization
- Shared storage
- High availability

Security Recommendations

- Isolate storage management networks.
- Require administrator authentication.
- Enable audit logging.
- Monitor storage events.

---

## Port 900 — CORBA Initialization

Port **900** is associated with CORBA initialization services in some distributed enterprise environments.

Typical Architecture

```text
Client

   │

CORBA Request

   ▼

ORB Service

   │

Distributed Objects

   ▼

Enterprise Applications
```

Common Uses

- Financial platforms
- Telecommunications
- Enterprise middleware
- Legacy distributed applications

Security Recommendations

- Restrict middleware services.
- Disable unused CORBA components.
- Monitor object requests.
- Patch legacy middleware.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 883 | Nessus Vulnerability Scanner |
| 892 | HCL Domino Infrastructure |
| 898 | Enterprise Storage Controller |
| 900 | CORBA Middleware |

---

# Blue Team Perspective

Recommended Actions

- Restrict vulnerability scanners to management VLANs.
- Protect scan results and credentials.
- Harden collaboration servers.
- Secure enterprise storage controllers.
- Disable unused middleware services.
- Audit administrator activities.

---

# Red Team Perspective

Interesting Targets

### Port 883

Possible Findings

- Internal vulnerability scanner
- Asset inventory
- Credentialed scanning infrastructure
- Security operations environment

Potential Enumeration

```bash
nmap --script http-title,http-headers -p883 target
```

---

### Port 892

Possible Findings

- Enterprise email platform
- Collaboration servers
- Legacy Domino infrastructure

---

### Port 898

Possible Findings

- SAN controllers
- Storage virtualization
- Backup infrastructure

---

### Port 900

Possible Findings

- Legacy middleware
- Distributed enterprise applications
- Financial or telecom systems

Useful Enumeration

```bash
nmap -sV -p883,892,898,900 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p881-900 target
```

Version Detection

```bash
nmap -sV -p883,892,898,900 target
```

Default Script Scan

```bash
nmap -sC -sV -p883,892 target
```

HTTP Enumeration

```bash
nmap --script http-title,http-headers -p883 target
```

Aggressive Scan

```bash
nmap -A -p881-900 target
```

---

# Summary

Ports **881–900** include enterprise security platforms, collaboration servers, storage management systems, and distributed middleware. **Port 883** is particularly significant because it commonly identifies **Tenable Nessus**, one of the industry's most widely deployed vulnerability scanners. **Port 892** may reveal **HCL Domino** collaboration infrastructure, while **Port 898** often indicates enterprise storage management services. **Port 900** can expose legacy CORBA middleware supporting distributed enterprise applications. Collectively, these ports help identify security operations infrastructure, enterprise collaboration environments, and mission-critical backend services.

---

# Ports 901–920

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 901 | TCP | SWAT | Samba Web Administration Tool | Samba | File Server Administration | Deprecated; disable if unused. |
| 902 | TCP | VMware Server Console | VMware ESXi, VMware Workstation | VM Management | Virtualization | Restrict management access. |
| 903 | TCP | VMware Remote Console | VMware Infrastructure | Remote Console | Hypervisor Management | Internal management only. |
| 904 | TCP | WebSphere JMS | IBM WebSphere | Messaging | Enterprise Middleware | Restrict trusted clients. |
| 905 | TCP | IDEAFARM Door | Enterprise Service | Vendor Software | Internal Communications | Vendor-specific deployment. |
| 906 | TCP | Secure Device Gateway | Security Appliances | Device Management | Enterprise Infrastructure | Require authentication. |
| 907 | TCP | Open Messaging | Enterprise Messaging | Middleware | Message Distribution | Restrict access. |
| 908 | TCP | IBM Directory Services | IBM Security | Identity Services | Directory Management | Internal deployment. |
| 909 | TCP | WebSM | IBM AIX | System Administration | UNIX Management | Restrict administrator access. |
| 910 | TCP | PDL Data Stream | HP JetDirect | Network Printing | Print Services | Limit printer exposure. |
| 911 | TCP | Device Telemetry | Enterprise Monitoring | Monitoring Agents | Metrics Collection | Authenticate endpoints. |
| 912 | TCP | Apex Mesh | Distributed Systems | Cluster Communication | Internal Services | Vendor-specific. |
| 913 | TCP | Secure Messaging | Enterprise Collaboration | Secure Communications | Messaging | Encrypt communications. |
| 914 | TCP | Backup Gateway | Enterprise Backup | Disaster Recovery | Backup Coordination | Protect backup systems. |
| 915 | TCP | Network Policy | NAC Platforms | Policy Enforcement | Access Control | Restrict administrator access. |
| 916 | TCP | Management Broker | Enterprise Middleware | Management Services | Infrastructure Control | Internal only. |
| 917 | TCP | Monitoring Agent | Enterprise Monitoring | Telemetry | Infrastructure Visibility | Protect monitoring credentials. |
| 918 | TCP | Device Enrollment | Enterprise Devices | Provisioning | Zero-Touch Deployment | Verify device identity. |
| 919 | TCP | Authentication Relay | Identity Platforms | Authentication | Enterprise IAM | Secure authentication channels. |
| 920 | TCP | Elastic Auxiliary | Elastic Stack | Search & Analytics | Log Collection | Protect management interfaces. |

---

# Port Spotlight

## Port 901 — Samba Web Administration Tool (SWAT)

SWAT was a browser-based interface for administering Samba servers.

Although no longer recommended, it may still appear in legacy UNIX and Linux environments.

Typical Features

- Samba configuration
- Share management
- User administration
- Service restart
- Configuration editing

Typical Architecture

```text
Administrator

      │

HTTP

      ▼

SWAT Interface

      │

Samba Configuration

      ▼

SMB File Server
```

Example Scan

```bash
nmap -sV -p901 target
```

Security Risks

- Legacy web interface
- Weak administrator credentials
- Remote configuration changes
- Unsupported software

Security Recommendations

- Remove SWAT if no longer required.
- Restrict administrative access.
- Upgrade Samba regularly.
- Replace with modern administration tools.

---

## Ports 902–903 — VMware Management Services

Ports **902** and **903** are among the most recognizable VMware management ports.

These services support communication between VMware clients and ESXi hosts.

Common Components

- VMware ESXi
- VMware Workstation
- VMware Fusion
- VMware vCenter
- VMware Remote Console

Typical Architecture

```text
Administrator

      │

VMware Client

      ▼

vCenter

      │

ESXi Host

      ▼

Virtual Machines
```

Example Scan

```bash
nmap -sV -p902,903 target
```

Useful NSE Scripts

```bash
nmap --script ssl-cert -p902,903 target
```

Security Risks

- Hypervisor compromise
- VM console access
- Credential theft
- Management interface exposure

Security Recommendations

- Isolate management VLANs.
- Enable multifactor authentication.
- Restrict administrator IP addresses.
- Apply VMware security patches promptly.

---

## Port 910 — HP JetDirect Printing

Port **910** is the default RAW printing service used by HP JetDirect and many modern network printers.

It is one of the easiest ways to identify enterprise printers.

Typical Workflow

```text
User

   │

Print Job

   ▼

TCP/910

   ▼

Network Printer

   │

Print Engine

   ▼

Printed Document
```

Common Vendors

- HP
- Canon
- Brother
- Ricoh
- Xerox
- Lexmark

Example Scan

```bash
nmap -sV -p910 target
```

Useful NSE Scripts

```bash
nmap --script printer-info -p910 target
```

Security Risks

- Printer information disclosure
- Unauthorized printing
- Sensitive document leakage
- Pivot opportunities

Security Recommendations

- Disable unused printing protocols.
- Restrict printer access.
- Keep firmware updated.
- Monitor print activity.

---

## Port 920 — Elastic Stack Services

Port **920** is frequently encountered in environments using the **Elastic Stack**.

Although Elasticsearch commonly uses **9200**, auxiliary services or vendor-specific integrations may appear around this range.

Typical Environment

```text
Applications

Servers

Network Devices

      │

Logs

      ▼

Elastic Stack

      │

Indexing

Search

Analytics

      ▼

Dashboards
```

Security Recommendations

- Require authentication.
- Enable TLS encryption.
- Restrict API access.
- Monitor search activity.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 901 | Legacy Samba Administration |
| 902–903 | VMware Infrastructure |
| 909 | IBM AIX Management |
| 910 | Network Printer |
| 920 | Enterprise Analytics Platform |

---

# Blue Team Perspective

Recommended Actions

- Remove obsolete Samba administration interfaces.
- Protect VMware management services.
- Restrict printer network access.
- Harden analytics platforms.
- Monitor privileged administrator activity.
- Segment infrastructure management networks.

---

# Red Team Perspective

Interesting Targets

### Ports 902–903

Possible Findings

- VMware ESXi hosts
- vCenter infrastructure
- Enterprise virtualization
- Datacenter management

---

### Port 910

Possible Findings

- Network printers
- Multifunction devices
- Print servers
- Office infrastructure

Potential Enumeration

```bash
nmap --script printer-info -p910 target
```

---

### Port 920

Possible Findings

- Log management platform
- Search infrastructure
- Security analytics
- Centralized logging

---

### Port 901

Possible Findings

- Legacy Samba servers
- Linux file servers
- Older administrative interfaces

Useful Enumeration

```bash
nmap -sV -p901,902,903,910,920 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p901-920 target
```

Version Detection

```bash
nmap -sV -p901,902,903,910,920 target
```

Default Script Scan

```bash
nmap -sC -sV -p902,903,910 target
```

Printer Enumeration

```bash
nmap --script printer-info -p910 target
```

Aggressive Scan

```bash
nmap -A -p901-920 target
```

---

# Summary

Ports **901–920** primarily represent virtualization management, legacy administration tools, enterprise middleware, network printing, and analytics infrastructure. **Ports 902–903** are strong indicators of **VMware ESXi** or **vCenter** environments, while **Port 910 (HP JetDirect)** commonly identifies enterprise network printers. **Port 901** may expose legacy Samba administration interfaces that should be removed, and **Port 920** can indicate supporting services within centralized logging or analytics platforms. These ports provide valuable insight into enterprise management and operational infrastructure.

---

# Ports 921–940

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 921 | TCP | Media Gateway | Multimedia Platform | VoIP Systems | Voice Services | Restrict management access. |
| 922 | TCP | VMware Authentication | VMware Infrastructure | Authentication | Hypervisor Management | Internal networks only. |
| 923 | TCP | Device Provisioning | Enterprise Appliances | Zero-Touch Deployment | Infrastructure Management | Authenticate endpoints. |
| 924 | TCP | Network Inventory | Asset Discovery | Monitoring Platforms | Device Inventory | Internal deployment. |
| 925 | TCP | Oracle Management | Oracle Enterprise Manager | Database Administration | Enterprise Databases | Restrict administrator access. |
| 926 | TCP | Backup Coordinator | Backup Platforms | Backup Scheduling | Disaster Recovery | Protect backup credentials. |
| 927 | TCP | Monitoring API | Observability Platforms | Metrics Collection | Infrastructure Monitoring | Secure API tokens. |
| 928 | TCP | VMware Replication | VMware Infrastructure | Replication | Virtual Machine Synchronization | Encrypt replication traffic. |
| 929 | TCP | LDAP Gateway | Identity Services | Directory Proxy | Authentication | Require TLS. |
| 930 | TCP | Elasticsearch Transport | Elasticsearch | Cluster Communication | Search Infrastructure | Internal cluster only. |
| 931 | TCP | Cluster Synchronization | Distributed Systems | Cluster Management | High Availability | Restrict trusted nodes. |
| 932 | TCP | Device Telemetry | Enterprise Monitoring | Performance Metrics | Observability | Protect monitoring traffic. |
| 933 | TCP | Secure Messaging | Enterprise Middleware | Message Routing | Enterprise Integration | Encrypt communications. |
| 934 | TCP | Automation Controller | DevOps Platforms | Infrastructure Automation | Configuration Management | Authenticate automation clients. |
| 935 | TCP | Configuration Service | Enterprise Systems | Configuration Distribution | Device Management | Restrict administrator access. |
| 936 | TCP | Secure Backup | Enterprise Backup | Replication | Disaster Recovery | Protect backup repositories. |
| 937 | TCP | Identity Synchronization | IAM Platforms | User Provisioning | Enterprise Identity | Secure synchronization. |
| 938 | TCP | PKI Management | Certificate Services | Trust Management | Enterprise Security | Protect certificate authorities. |
| 939 | TCP | Security Telemetry | SIEM Platforms | Event Collection | Security Operations | Protect log integrity. |
| 940 | TCP | Distributed Cache | Cluster Platforms | High-Speed Data Access | Enterprise Applications | Restrict cluster communication. |

---

# Port Spotlight

## Port 930 — Elasticsearch Transport

Port **930** is the native transport protocol used by **Elasticsearch** nodes for internal cluster communication.

Unlike the REST API (typically on port **9200**), this port handles communication between cluster members.

Common Platforms

- Elasticsearch
- Elastic Stack (ELK)
- OpenSearch
- SIEM Platforms
- Log Analytics

Typical Architecture

```text
 Kibana

    │

REST API

    ▼

Elasticsearch Node

     │

Transport (930)

     ▼

Cluster Nodes

Node A

Node B

Node C
```

Example Scan

```bash
nmap -sV -p930 target
```

Security Risks

- Cluster topology disclosure
- Unauthorized node participation
- Data replication abuse
- Cluster manipulation

Security Recommendations

- Never expose port 930 to the Internet.
- Restrict communication to cluster members.
- Enable TLS between nodes.
- Monitor cluster membership changes.

---

## Port 925 — Oracle Enterprise Management

Port **925** may be used by Oracle management components responsible for database monitoring and administration.

Typical Deployment

```text
Administrator

      │

Management Console

      ▼

Oracle Enterprise Manager

      │

Database Servers

      ▼

Production Databases
```

Security Recommendations

- Require multifactor authentication.
- Restrict administrator IP ranges.
- Enable auditing.
- Keep Oracle software updated.

---

## Port 929 — LDAP Gateway

LDAP gateways act as intermediaries between applications and enterprise directory services.

Common Uses

- Active Directory integration
- LDAP proxy
- Authentication gateway
- Identity federation

Typical Workflow

```text
Application

     │

LDAP Request

     ▼

LDAP Gateway

     │

Directory Service

     ▼

Authentication
```

Security Recommendations

- Require LDAPS whenever possible.
- Disable anonymous binds.
- Monitor authentication failures.
- Protect service accounts.

---

## Port 940 — Distributed Cache

Distributed cache platforms improve application performance by storing frequently accessed data.

Common Platforms

- Hazelcast
- Infinispan
- Oracle Coherence
- Apache Ignite

Typical Architecture

```text
Application

      │

Cache Request

      ▼

Distributed Cache

 ┌────┴────┐

Node A Node B

      │

Database
```

Security Recommendations

- Restrict cluster membership.
- Encrypt node communications.
- Require authentication.
- Monitor cache synchronization.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 925 | Oracle Enterprise Infrastructure |
| 929 | LDAP Proxy or Gateway |
| 930 | Elasticsearch Cluster |
| 940 | Distributed Cache Platform |

---

# Blue Team Perspective

Recommended Actions

- Restrict Elasticsearch transport traffic.
- Secure Oracle management interfaces.
- Harden LDAP gateway configurations.
- Protect distributed cache clusters.
- Enable centralized logging.
- Audit privileged administrative actions.

---

# Red Team Perspective

Interesting Targets

### Port 930

Possible Findings

- Elasticsearch cluster
- Centralized logging
- SIEM infrastructure
- Search platform

Potential Enumeration

- Cluster version
- Node identification
- Internal topology

---

### Port 925

Possible Findings

- Oracle Enterprise Manager
- Database administration
- Mission-critical databases

---

### Port 929

Possible Findings

- LDAP proxy
- Active Directory integration
- Enterprise identity services

---

### Port 940

Possible Findings

- Distributed cache
- Enterprise Java applications
- High-performance middleware

Useful Enumeration

```bash
nmap -sV -p925,929,930,940 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p921-940 target
```

Version Detection

```bash
nmap -sV -p925,929,930,940 target
```

Default Script Scan

```bash
nmap -sC -sV -p929,930 target
```

Aggressive Scan

```bash
nmap -A -p921-940 target
```

---

# Summary

Ports **921–940** commonly identify enterprise database management, directory services, search infrastructure, and distributed application platforms. **Port 930** is particularly important because it is used for **Elasticsearch cluster transport**, making it a strong indicator of centralized logging or analytics environments. **Port 925** may expose Oracle management services, **Port 929** often indicates LDAP proxy infrastructure, and **Port 940** can reveal distributed caching technologies that support high-performance enterprise applications.

---

# Ports 941–960

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 941 | TCP | Git Native Protocol | Git | Source Code Management | Version Control | Prefer SSH or HTTPS over anonymous Git. |
| 942 | TCP | Secure Source Sync | SCM Platforms | Repository Synchronization | Development Infrastructure | Restrict developer access. |
| 943 | TCP | OpenVPN Web Admin | OpenVPN Access Server | VPN Administration | Remote Access | Require MFA and TLS. |
| 944 | TCP | Cluster API | Distributed Systems | Cluster Management | Enterprise Infrastructure | Internal communication only. |
| 945 | TCP | Security Gateway | Security Appliances | Secure Communications | Infrastructure Control | Restrict administrator access. |
| 946 | TCP | Device Automation | Enterprise Automation | Device Provisioning | Configuration Management | Authenticate automation agents. |
| 947 | TCP | Backup Verification | Backup Systems | Integrity Validation | Disaster Recovery | Protect backup metadata. |
| 948 | TCP | Identity Federation | IAM Platforms | Federation Services | Enterprise Authentication | Secure trust relationships. |
| 949 | TCP | Secure Event Channel | SIEM Platforms | Event Transport | Security Monitoring | Encrypt event streams. |
| 950 | TCP | Management API | Enterprise Platforms | Administrative APIs | Infrastructure Management | Restrict API access. |
| 951 | TCP | Storage Monitoring | SAN Platforms | Performance Monitoring | Enterprise Storage | Internal deployment only. |
| 952 | TCP | Certificate Distribution | PKI Platforms | Certificate Services | Enterprise Security | Protect CA infrastructure. |
| 953 | TCP | BIND Remote Name Daemon Control (RNDC) | ISC BIND | DNS Administration | DNS Management | Restrict RNDC keys and hosts. |
| 954 | TCP | DNS Management | DNS Appliances | Administrative Services | Enterprise DNS | Internal use only. |
| 955 | TCP | Virtual Infrastructure | Hypervisors | Infrastructure Services | Virtualization | Restrict management interfaces. |
| 956 | TCP | Monitoring Agent | Enterprise Monitoring | Telemetry | Infrastructure Visibility | Protect monitoring credentials. |
| 957 | TCP | Secure Broker | Enterprise Messaging | Message Routing | Middleware | Require authentication. |
| 958 | TCP | Cluster Replication | Distributed Systems | Data Synchronization | High Availability | Encrypt replication traffic. |
| 959 | TCP | Identity Relay | Enterprise IAM | Authentication Gateway | Identity Services | Require TLS. |
| 960 | TCP | Storage Gateway | Enterprise Storage | Data Access | SAN/NAS Management | Restrict administrative access. |

---

# Port Spotlight

## Port 941 — Git Native Protocol

Port **941** is the default port for the **Git native protocol**, allowing repositories to be cloned without authentication in many public deployments.

Unlike Git over **SSH (22)** or **HTTPS (443)**, the native Git protocol provides fast read-only repository access.

Common Software

- Git
- Git Daemon
- Gitolite
- Embedded Git Servers

Typical Architecture

```text
Developer

     │

git clone

     ▼

Git Daemon

     │

Repositories

     ▼

Source Code
```

Example Scan

```bash
nmap -sV -p941 target
```

Useful NSE Scripts

```bash
nmap --script banner -p941 target
```

Security Risks

- Source code disclosure
- Repository enumeration
- Intellectual property exposure
- Sensitive configuration leakage

Security Recommendations

- Disable anonymous Git access unless required.
- Prefer Git over SSH or HTTPS.
- Restrict repository visibility.
- Audit repository permissions regularly.

---

## Port 943 — OpenVPN Access Server

Port **943** is commonly associated with **OpenVPN Access Server** web administration and client services.

Typical Features

- VPN administration
- User management
- Client configuration downloads
- Authentication
- Certificate management

Typical Architecture

```text
Remote User

      │

HTTPS

      ▼

OpenVPN Access Server

      │

VPN Tunnel

      ▼

Internal Network
```

Example Scan

```bash
nmap -sV -p943 target
```

Useful NSE Scripts

```bash
nmap --script ssl-cert,http-title -p943 target
```

Security Risks

- VPN credential theft
- Administrative interface exposure
- Weak authentication
- Outdated VPN software

Security Recommendations

- Enable MFA.
- Restrict management IP addresses.
- Disable unused administrator accounts.
- Keep OpenVPN updated.

---

## Port 953 — RNDC (Remote Name Daemon Control)

RNDC is the administrative control interface for **ISC BIND DNS** servers.

Administrators use RNDC to:

- Reload DNS zones
- Flush caches
- View server status
- Manage DNSSEC operations
- Restart services

Typical Architecture

```text
Administrator

      │

RNDC

      ▼

BIND DNS Server

      │

DNS Zones

Cache

DNSSEC
```

Example Scan

```bash
nmap -sV -p953 target
```

Security Risks

- DNS manipulation
- Zone modification
- Cache poisoning assistance
- Unauthorized administration

Security Recommendations

- Restrict RNDC to trusted hosts.
- Protect RNDC keys.
- Enable firewall filtering.
- Monitor administrative commands.

---

## Port 960 — Enterprise Storage Gateway

Storage gateways provide centralized access to enterprise storage resources.

Common Platforms

- Dell EMC
- NetApp
- IBM Storage
- HPE Storage
- Hitachi Vantara

Typical Deployment

```text
Applications

Servers

Virtual Machines

       │

Storage Requests

       ▼

Storage Gateway

       │

SAN / NAS

       ▼

Disk Arrays
```

Security Recommendations

- Separate storage management networks.
- Require multifactor authentication.
- Encrypt administrative sessions.
- Monitor storage configuration changes.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 941 | Git Repository Server |
| 943 | OpenVPN Access Server |
| 953 | BIND DNS Administration |
| 960 | Enterprise Storage Infrastructure |

---

# Blue Team Perspective

Recommended Actions

- Disable anonymous Git repositories.
- Secure VPN administration portals.
- Protect RNDC control interfaces.
- Restrict storage management access.
- Enable centralized auditing.
- Monitor privileged administrator sessions.

---

# Red Team Perspective

Interesting Targets

### Port 941

Possible Findings

- Internal Git repositories
- Source code servers
- Development infrastructure
- CI/CD environments

Potential Enumeration

```bash
nmap --script banner -p941 target
```

---

### Port 943

Possible Findings

- Corporate VPN gateway
- Remote access platform
- OpenVPN Access Server

Potential Enumeration

```bash
nmap --script ssl-cert,http-title -p943 target
```

---

### Port 953

Possible Findings

- Internal DNS servers
- BIND infrastructure
- DNS administration interface

---

### Port 960

Possible Findings

- Enterprise SAN
- Storage gateways
- Backup infrastructure

Useful Enumeration

```bash
nmap -sV -p941,943,953,960 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p941-960 target
```

Version Detection

```bash
nmap -sV -p941,943,953,960 target
```

Default Script Scan

```bash
nmap -sC -sV -p943,953 target
```

SSL Enumeration

```bash
nmap --script ssl-cert -p943 target
```

Aggressive Scan

```bash
nmap -A -p941-960 target
```

---

# Summary

Ports **941–960** primarily represent source code management, VPN infrastructure, DNS administration, enterprise storage, and distributed management services. **Port 941 (Git Native Protocol)** frequently identifies Git repository servers that may expose valuable source code if improperly configured. **Port 943** is a strong indicator of **OpenVPN Access Server**, commonly used for secure remote access. **Port 953 (RNDC)** reveals BIND DNS administrative interfaces that should never be publicly accessible, while **Port 960** often identifies enterprise storage gateways supporting SAN and NAS environments. Together, these ports help identify development infrastructure, remote access platforms, DNS management systems, and enterprise storage services.

---

# Ports 961–980

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 961 | TCP | Device Manager | Enterprise Appliances | Device Administration | Infrastructure Management | Restrict management access. |
| 962 | TCP | Secure Provisioning | Enterprise Systems | Provisioning | Infrastructure Automation | Authenticate provisioning agents. |
| 963 | TCP | Monitoring Relay | Monitoring Platforms | Metric Aggregation | Enterprise Monitoring | Protect monitoring credentials. |
| 964 | TCP | Backup Scheduler | Enterprise Backup | Backup Coordination | Disaster Recovery | Restrict trusted hosts. |
| 965 | TCP | PKI Gateway | Certificate Services | Certificate Enrollment | Enterprise Security | Protect certificate authorities. |
| 966 | TCP | Identity Federation | IAM Platforms | Authentication | Identity Management | Require mutual TLS. |
| 967 | TCP | Storage Controller | SAN Infrastructure | Storage Coordination | Enterprise Storage | Internal deployment only. |
| 968 | TCP | Virtual Appliance API | Hypervisor Platforms | Appliance Management | Virtualization | Secure administrative APIs. |
| 969 | TCP | Cluster Membership | Cluster Platforms | Node Coordination | High Availability | Restrict cluster communication. |
| 970 | TCP | L2TP | VPN Services | Layer 2 Tunneling Protocol | Remote Access | Require IPsec protection. |
| 971 | TCP | Secure Messaging | Enterprise Middleware | Message Exchange | Enterprise Integration | Encrypt communications. |
| 972 | TCP | Automation Broker | DevOps Platforms | Task Coordination | Infrastructure Automation | Authenticate automation clients. |
| 973 | TCP | Bitcoin | Bitcoin Core | Cryptocurrency Network | Blockchain | Validate peer connections. |
| 974 | TCP | Certificate Relay | PKI Platforms | Certificate Distribution | Enterprise Security | Monitor certificate issuance. |
| 975 | TCP | Identity Sync | Identity Platforms | User Synchronization | Enterprise IAM | Protect synchronization channels. |
| 976 | TCP | Security Analytics | SIEM Platforms | Event Processing | Security Operations | Restrict administrative access. |
| 977 | TCP | Telemetry Gateway | Observability Platforms | Metrics Collection | Infrastructure Monitoring | Secure telemetry traffic. |
| 978 | TCP | Backup Verification | Backup Systems | Integrity Validation | Disaster Recovery | Audit backup status. |
| 979 | TCP | Storage Replication | Enterprise Storage | Data Synchronization | High Availability | Encrypt replication traffic. |
| 980 | TCP | Secure Cluster API | Cluster Platforms | Administrative Services | Enterprise Infrastructure | Internal deployment only. |

---

# Port Spotlight

## Port 970 — L2TP (Layer 2 Tunneling Protocol)

Port **970** is assigned to **Layer 2 Tunneling Protocol (L2TP)** services in some implementations and enterprise appliances.

L2TP is commonly combined with **IPsec** to provide secure VPN connectivity.

Common Uses

- Remote user VPN
- Site-to-site VPN
- Secure tunneling
- Enterprise remote access

Typical Architecture

```text
Remote Client

      │

L2TP/IPsec Tunnel

      ▼

VPN Gateway

      │

Internal Network

      ▼

Enterprise Resources
```

Example Scan

```bash
nmap -sV -p970 target
```

Security Risks

- Weak authentication
- Legacy VPN configurations
- Credential attacks
- Tunnel misconfiguration

Security Recommendations

- Always pair L2TP with IPsec.
- Use certificate-based authentication.
- Enable MFA.
- Disable legacy encryption algorithms.

---

## Port 973 — Bitcoin Network

Port **973** is well known within the cryptocurrency ecosystem because it is the default listening port for **Bitcoin Core** peer-to-peer communication.

Common Software

- Bitcoin Core
- Bitcoin Full Nodes
- Blockchain Explorers
- Cryptocurrency Infrastructure

Typical Architecture

```text
Bitcoin Node

      │

P2P Network

      ▼

Peer Nodes

      │

Blockchain

      ▼

Consensus
```

Example Scan

```bash
nmap -sV -p973 target
```

Security Risks

- Node fingerprinting
- Version disclosure
- Resource exhaustion attacks
- DDoS targeting

Security Recommendations

- Keep Bitcoin software updated.
- Restrict unnecessary inbound connections.
- Monitor peer activity.
- Protect exposed management interfaces.

---

## Port 967 — Enterprise Storage Controller

Enterprise storage controllers coordinate access between applications and storage infrastructure.

Common Platforms

- Dell EMC
- NetApp
- IBM Storage
- HPE Storage

Typical Workflow

```text
Application

     │

Storage Request

     ▼

Storage Controller

     │

SAN

NAS

Disk Arrays

     ▼

Persistent Data
```

Security Recommendations

- Restrict management interfaces.
- Enable audit logging.
- Use encrypted administration channels.
- Separate storage management VLANs.

---

## Port 976 — Security Analytics Platform

Security analytics platforms process logs collected from enterprise systems.

Typical Sources

- Firewalls
- IDS/IPS
- Active Directory
- Endpoint Detection
- Cloud Infrastructure

Typical Architecture

```text
Enterprise Devices

       │

Security Events

       ▼

Analytics Engine

       │

Correlation

Detection

Alerting

       ▼

SOC Dashboard
```

Security Recommendations

- Restrict administrator accounts.
- Protect log integrity.
- Enable RBAC.
- Monitor configuration changes.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 967 | Enterprise Storage |
| 970 | L2TP VPN Services |
| 973 | Bitcoin Node |
| 976 | Security Analytics Platform |

---

# Blue Team Perspective

Recommended Actions

- Harden VPN gateways.
- Secure blockchain infrastructure where deployed.
- Protect enterprise storage controllers.
- Restrict access to security analytics platforms.
- Enable centralized auditing.
- Monitor privileged administrative sessions.

---

# Red Team Perspective

Interesting Targets

### Port 970

Possible Findings

- VPN gateways
- Remote access infrastructure
- Enterprise edge devices

Potential Enumeration

```bash
nmap -sV -p970 target
```

---

### Port 973

Possible Findings

- Bitcoin full node
- Cryptocurrency infrastructure
- Blockchain services

Potential Enumeration

```bash
nmap -sV --script banner -p973 target
```

---

### Port 967

Possible Findings

- SAN controllers
- Enterprise storage
- Backup infrastructure

---

### Port 976

Possible Findings

- SIEM platform
- SOC infrastructure
- Centralized log management

Useful Enumeration

```bash
nmap -sV -p967,970,973,976 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p961-980 target
```

Version Detection

```bash
nmap -sV -p967,970,973,976 target
```

Default Script Scan

```bash
nmap -sC -sV -p970,973 target
```

Banner Enumeration

```bash
nmap --script banner -p973 target
```

Aggressive Scan

```bash
nmap -A -p961-980 target
```

---

# Summary

Ports **961–980** primarily identify enterprise storage, identity management, VPN technologies, blockchain infrastructure, and security analytics platforms. **Port 970** may indicate **L2TP VPN** services used for secure remote access, while **Port 973** is strongly associated with **Bitcoin Core** peer-to-peer communication. **Port 967** often reveals enterprise storage infrastructure, and **Port 976** can expose centralized security analytics or SIEM components. Proper segmentation, strong authentication, and continuous monitoring are essential for protecting these critical services.

---

# Ports 981–1000

| Port | Protocol | Service | Description | Common Software | Typical Usage | Security Notes |
|------:|:-------:|----------|-------------|-----------------|---------------|----------------|
| 981 | TCP | Enterprise Management | Infrastructure Platforms | Central Management | Enterprise Administration | Restrict management access. |
| 982 | TCP | Monitoring Gateway | Observability Platforms | Metrics Collection | Infrastructure Monitoring | Protect monitoring credentials. |
| 983 | TCP | Secure Provisioning | Enterprise Automation | Device Enrollment | Zero-Touch Provisioning | Authenticate endpoints. |
| 984 | TCP | Identity Services | IAM Platforms | Authentication | Enterprise Identity | Require TLS. |
| 985 | TCP | Backup Coordination | Enterprise Backup | Job Scheduling | Disaster Recovery | Restrict trusted hosts. |
| 986 | TCP | Cluster Controller | Distributed Systems | Cluster Coordination | High Availability | Internal communication only. |
| 987 | TCP | Secure Telemetry | SIEM Platforms | Event Collection | Security Monitoring | Encrypt telemetry traffic. |
| 988 | TCP | Storage Gateway | SAN/NAS Platforms | Storage Access | Enterprise Storage | Restrict administrator access. |
| 989 | TCP | FTPS Data | FTP over TLS | Secure File Transfer | Enterprise File Exchange | Enforce encryption. |
| 990 | TCP | FTPS Control | FTP over TLS | Secure File Transfer | Enterprise File Exchange | Disable insecure FTP. |
| 991 | TCP | NAS Management | Network Storage | Administrative Services | Storage Infrastructure | Restrict management interfaces. |
| 992 | TCP | TelnetS | Secure Telnet (TLS) | Remote Administration | Legacy Secure Management | Prefer SSH where possible. |
| 993 | TCP | IMAPS | Internet Message Access Protocol over TLS | Secure Email Retrieval | Mail Servers | Require strong authentication. |
| 994 | TCP | IRCS | IRC over TLS | Secure Chat | Collaboration | Restrict public access if internal. |
| 995 | TCP | POP3S | POP3 over TLS | Secure Email Retrieval | Mail Servers | Enforce modern TLS versions. |
| 996 | TCP | Secure Device API | Enterprise Appliances | Management API | Infrastructure Control | Authenticate API requests. |
| 997 | TCP | Monitoring Broker | Enterprise Monitoring | Event Aggregation | Infrastructure Visibility | Protect monitoring traffic. |
| 998 | TCP | Distributed Messaging | Enterprise Middleware | Internal Communications | Application Integration | Encrypt communications. |
| 999 | TCP | Scalable Networking | Vendor-Specific Services | Infrastructure Support | Enterprise Platforms | Vendor-dependent implementation. |
| 1000 | TCP | CADLOCK | Legacy Security Service | License Management | Enterprise Applications | Rarely exposed externally. |

---

# Port Spotlight

## Ports 989–990 — FTPS (FTP over TLS)

Ports **989** and **990** are assigned to **FTPS**, which extends the traditional FTP protocol by adding SSL/TLS encryption.

Unlike classic FTP, FTPS protects authentication credentials and transferred files against interception.

Common Software

- FileZilla Server
- Microsoft IIS FTP
- ProFTPD
- vsftpd
- Cerberus FTP Server

Typical Architecture

```text
Client

   │

TLS

   ▼

FTPS Server

   │

Authentication

   ▼

Secure File Transfer
```

Example Scan

```bash
nmap -sV -p989,990 target
```

Useful NSE Scripts

```bash
nmap --script ssl-cert,ssl-enum-ciphers -p989,990 target
```

Security Risks

- Weak TLS configuration
- Anonymous login
- Outdated certificates
- Misconfigured passive ports

Security Recommendations

- Disable insecure FTP.
- Require strong TLS versions.
- Rotate certificates regularly.
- Monitor file transfer activity.

---

## Port 992 — TelnetS

Port **992** provides **Telnet over TLS**, sometimes referred to as **TelnetS**.

Although encrypted, Telnet-based management has largely been replaced by **SSH**.

Typical Uses

- Legacy network devices
- Embedded systems
- Older UNIX platforms
- Specialized industrial equipment

Typical Architecture

```text
Administrator

      │

TLS

      ▼

TelnetS Server

      │

Remote Shell

      ▼

Managed Device
```

Security Recommendations

- Prefer SSH whenever possible.
- Disable Telnet services if unnecessary.
- Restrict access by firewall.
- Require certificate validation.

---

## Port 993 — IMAPS

Port **993** is the standard port for **IMAP over TLS**, allowing secure retrieval and synchronization of email.

Common Software

- Microsoft Exchange
- Dovecot
- Courier IMAP
- Cyrus IMAP
- Zimbra

Typical Workflow

```text
Email Client

      │

IMAPS

      ▼

Mail Server

      │

Mailbox

      ▼

Secure Email Access
```

Example Scan

```bash
nmap -sV -p993 target
```

Useful NSE Scripts

```bash
nmap --script imap-capabilities,ssl-cert -p993 target
```

Security Risks

- Weak passwords
- Credential stuffing
- Legacy TLS versions
- Mailbox enumeration

Security Recommendations

- Require MFA where supported.
- Disable weak authentication.
- Enforce TLS 1.2+.
- Monitor login anomalies.

---

## Port 995 — POP3S

Port **995** provides encrypted **POP3** access using SSL/TLS.

Unlike IMAP, POP3 generally downloads mail to the local client.

Typical Architecture

```text
Mail Client

      │

POP3S

      ▼

Mail Server

      │

Mailbox

      ▼

Downloaded Messages
```

Security Recommendations

- Require encrypted authentication.
- Disable insecure POP3.
- Use strong password policies.
- Audit authentication logs.

---

# Recognition Tips

| Port | Usually Indicates |
|------:|-------------------|
| 989–990 | FTPS Server |
| 992 | Secure Telnet |
| 993 | Secure IMAP Mail Server |
| 995 | Secure POP3 Mail Server |
| 1000 | Legacy Enterprise Service |

---

# Blue Team Perspective

Recommended Actions

- Replace insecure FTP with FTPS or SFTP.
- Migrate Telnet administration to SSH.
- Harden email server authentication.
- Protect TLS private keys.
- Enable certificate monitoring.
- Audit remote access activity.

---

# Red Team Perspective

Interesting Targets

### Ports 989–990

Possible Findings

- Secure FTP servers
- Enterprise file exchange
- Backup repositories
- File transfer gateways

Potential Enumeration

```bash
nmap --script ssl-cert,ssl-enum-ciphers -p989,990 target
```

---

### Port 993

Possible Findings

- Corporate mail server
- IMAP services
- Email infrastructure

Potential Enumeration

```bash
nmap --script imap-capabilities -p993 target
```

---

### Port 995

Possible Findings

- POP3 mail services
- Legacy email systems
- Secure mailbox access

---

### Port 992

Possible Findings

- Legacy administration interfaces
- Embedded systems
- Network appliances

Useful Enumeration

```bash
nmap -sV -p989,990,992,993,995 target
```

---

# Common Nmap Commands

Basic Scan

```bash
nmap -p981-1000 target
```

Version Detection

```bash
nmap -sV -p989,990,992,993,995 target
```

Default Script Scan

```bash
nmap -sC -sV -p993,995 target
```

SSL Enumeration

```bash
nmap --script ssl-cert,ssl-enum-ciphers -p989,990,992,993,995 target
```

Aggressive Scan

```bash
nmap -A -p981-1000 target
```

---

# Summary

Ports **981–1000** conclude the first thousand TCP ports with a strong emphasis on **secure file transfer, encrypted email services, legacy remote administration, and enterprise infrastructure management**. **Ports 989–990** identify **FTPS** services for encrypted FTP communication, while **Port 992** represents **Telnet over TLS**, a legacy protocol that has largely been superseded by SSH. **Ports 993 (IMAPS)** and **995 (POP3S)** are among the most recognizable secure email service ports and frequently indicate corporate or public mail servers. Proper TLS configuration, strong authentication, certificate management, and continuous monitoring remain essential for protecting these exposed services.

---

# Reference Complete

Congratulations! You have completed the **Top 1000 Ports Reference**.

This reference covered:

- The most common TCP ports from **1–1000**
- Well-known services and protocols
- Common enterprise software
- Security considerations
- Blue Team perspectives
- Red Team perspectives
- Port recognition techniques
- Practical Nmap commands
- Useful NSE scripts
- Real-world deployment examples

This document serves as a comprehensive reference for:

- Penetration Testers
- SOC Analysts
- Network Administrators
- System Engineers
- Security Researchers
- Students preparing for certifications such as eJPT, PNPT, Security+, CySA+, CEH, and OSCP.

---

# Next Reference

## 03_Common_Services.md