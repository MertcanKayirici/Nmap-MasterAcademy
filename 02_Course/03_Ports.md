# Nmap Master Academy

# Course 03

# Ports

---

## Course Information

**Course Number:** 03

**Difficulty:** Beginner

**Estimated Reading Time:** 60–90 Minutes

**Prerequisites:**
- Course 01 – Introduction
- Course 02 – Network Basics

---

# Table of Contents

1. What is a Port?
2. Why Ports Exist
3. How Ports Work
4. Port Numbers
5. Port Ranges
6. TCP and UDP Ports
7. Well-Known Ports
8. Registered Ports
9. Dynamic (Ephemeral) Ports
10. Common Services
11. Open vs Closed Ports
12. Port States
13. Listening Services
14. Firewalls and Ports
15. Why Nmap Scans Ports
16. Summary

---

# 1. What is a Port?

A port is a logical communication endpoint used by applications to send and receive network traffic.

Think of an IP address as the address of a building.

A port is the specific room inside that building.

Example:

```text
Building Address (IP)

192.168.1.20

↓

Room Number (Port)

22 → SSH

80 → HTTP

443 → HTTPS
```

Without ports, a computer would not know which application should receive incoming network traffic.

---

# 2. Why Ports Exist

A single computer can run many network services simultaneously.

For example:

- Web Server
- SSH Server
- FTP Server
- Mail Server
- Database Server

Each service requires its own communication channel.

Ports provide these channels.

Example:

```text
Computer

│

├── Port 22 → SSH

├── Port 80 → HTTP

├── Port 443 → HTTPS

├── Port 3306 → MySQL

└── Port 3389 → RDP
```

Without ports, all applications would receive mixed network traffic.

---

# 3. How Ports Work

Every network connection is identified by:

```text
Source IP

Source Port

Destination IP

Destination Port
```

Example:

```text
192.168.1.10:51324

↓

192.168.1.20:80
```

In this example:

Client

IP:
192.168.1.10

Port:
51324

Server

IP:
192.168.1.20

Port:
80

Port 51324 is a temporary client port.

Port 80 belongs to the web server.

---

# 4. Port Numbers

Port numbers range from:

```text
0

↓

65535
```

Total possible ports:

```text
65,536
```

Each TCP or UDP protocol has its own independent port space.

Therefore:

TCP Port 80

and

UDP Port 80

are completely different.

---

# 5. Port Ranges

The Internet Assigned Numbers Authority (IANA) divides ports into three categories.

| Range | Name |
|---------|--------------------|
| 0–1023 | Well-Known Ports |
| 1024–49151 | Registered Ports |
| 49152–65535 | Dynamic / Private Ports |

---

## Well-Known Ports

Reserved for standard Internet services.

Examples:

| Port | Service |
|------|----------|
| 20 | FTP Data |
| 21 | FTP Control |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 67 | DHCP |
| 68 | DHCP |
| 69 | TFTP |
| 80 | HTTP |
| 110 | POP3 |
| 123 | NTP |
| 143 | IMAP |
| 161 | SNMP |
| 389 | LDAP |
| 443 | HTTPS |
| 445 | SMB |
| 993 | IMAPS |
| 995 | POP3S |

---

## Registered Ports

Assigned to software vendors.

Examples:

| Port | Service |
|------|----------|
| 1433 | Microsoft SQL Server |
| 1521 | Oracle Database |
| 2049 | NFS |
| 2375 | Docker |
| 3306 | MySQL |
| 3389 | Remote Desktop |
| 5432 | PostgreSQL |
| 5900 | VNC |
| 6379 | Redis |
| 8080 | Alternative HTTP |

---

## Dynamic Ports

Also called:

- Ephemeral Ports
- Private Ports

Usually assigned automatically by the operating system when a client initiates a connection.

Example:

```text
Client

192.168.1.50:52341

↓

Server

192.168.1.20:443
```

Port 52341 disappears after the session ends.

---

# 6. TCP and UDP Ports

Ports exist independently for TCP and UDP.

Example:

```text
TCP 53

UDP 53
```

Although both use port 53, they represent different services at the transport layer.

Examples:

DNS

Mostly UDP

Sometimes TCP

HTTP

TCP

SSH

TCP

DHCP

UDP

SNMP

UDP

---

# 7. Common Services

Some of the most frequently encountered services during penetration testing include:

| Port | Service | Protocol |
|------|----------|----------|
| 21 | FTP | TCP |
| 22 | SSH | TCP |
| 23 | Telnet | TCP |
| 25 | SMTP | TCP |
| 53 | DNS | UDP/TCP |
| 80 | HTTP | TCP |
| 110 | POP3 | TCP |
| 135 | MSRPC | TCP |
| 139 | NetBIOS | TCP |
| 143 | IMAP | TCP |
| 389 | LDAP | TCP |
| 443 | HTTPS | TCP |
| 445 | SMB | TCP |
| 1433 | MSSQL | TCP |
| 3306 | MySQL | TCP |
| 3389 | RDP | TCP |
| 5432 | PostgreSQL | TCP |
| 5900 | VNC | TCP |
| 6379 | Redis | TCP |
| 8080 | HTTP Alternate | TCP |

---

# 8. Open vs Closed Ports

An open port indicates that an application is actively listening.

```text
Client

↓

Server

↓

Port 80

↓

HTTP Service Running
```

A closed port means that no application is listening, but the host is reachable.

A filtered port usually means that a firewall or packet filter is preventing communication.

---

# 9. Port States

Nmap reports several possible port states.

| State | Meaning |
|---------|-------------------------------|
| open | Application is accepting connections |
| closed | No service is listening |
| filtered | Firewall prevented detection |
| unfiltered | Accessible but state unknown |
| open\|filtered | Cannot distinguish |
| closed\|filtered | Rare, state uncertain |

These states will be explored in detail in later courses.

---

# 10. Listening Services

Operating systems allow applications to "listen" on ports.

Example:

```text
SSH Server

↓

Listening

↓

Port 22
```

When a packet arrives on port 22, the operating system forwards it to the SSH server.

---

# 11. Firewalls and Ports

Firewalls decide which ports may communicate.

Example:

```text
Internet

↓

Firewall

↓

Allow

80

443

↓

Block

22

3389
```

From Nmap's perspective:

Allowed ports often appear as open.

Blocked ports frequently appear as filtered.

---

# 12. Why Nmap Scans Ports

Nmap scans ports to answer several important questions:

- Which services are running?
- Which ports are open?
- Are unnecessary services exposed?
- Is the firewall configured correctly?
- Which applications might contain vulnerabilities?

Port scanning is the foundation of reconnaissance.

---

# Summary

In this course, you learned:

- What ports are
- Why ports exist
- Port numbering
- IANA port ranges
- TCP vs UDP ports
- Common network services
- Open, closed, and filtered ports
- Listening services
- Firewall interaction
- Why Nmap performs port scanning

Understanding ports is essential because almost every Nmap scan revolves around discovering and analyzing them.

---

# Key Takeaways

✓ Ports identify applications, not computers.

✓ IP addresses locate devices; ports locate services.

✓ TCP and UDP use separate port spaces.

✓ Open ports reveal available services.

✓ Closed ports indicate reachable hosts without active services.

✓ Filtered ports often suggest firewall protection.

✓ Port scanning is the foundation of network reconnaissance.

---

# Next Course

## Course 04

**TCP**