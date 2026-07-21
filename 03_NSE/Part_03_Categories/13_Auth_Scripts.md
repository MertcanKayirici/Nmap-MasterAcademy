# Chapter 13 — Authentication Scripts

The **auth** category contains NSE scripts designed to evaluate authentication mechanisms implemented by network services. Rather than attempting to exploit vulnerabilities directly, these scripts focus on identifying supported authentication methods, validating login mechanisms, and detecting weak or misconfigured authentication settings.

Authentication is often the first security barrier protecting network services. Understanding how a service authenticates users provides valuable information for security assessments, penetration testing, and compliance verification.

Unlike brute-force scripts, authentication scripts typically analyze authentication capabilities rather than repeatedly attempting to guess credentials.

---

## What Are Authentication Scripts?

Authentication scripts communicate with services that require user authentication and gather information about how those authentication systems operate.

Typical objectives include:

- Identifying supported authentication methods
- Detecting anonymous authentication
- Enumerating login mechanisms
- Identifying authentication protocols
- Verifying server authentication capabilities
- Collecting authentication-related metadata

These scripts help analysts understand how access to a service is controlled.

---

## Executing Authentication Scripts

To execute every authentication-related script, use:

```bash
nmap --script auth target
```

Authentication scripts are commonly combined with service detection.

```bash
nmap -sV --script auth target
```

They may also be combined with other categories.

```bash
nmap -sV --script "default,auth" target
```

This approach provides both service identification and authentication analysis within a single scan.

---

## How Authentication Scripts Work

Authentication scripts typically follow a structured process.

```text
Service Detection
        │
        ▼
Authentication Script Selected
        │
        ▼
Connect to Service
        │
        ▼
Query Authentication Features
        │
        ▼
Analyze Response
        │
        ▼
Generate Report
```

Most scripts stop after identifying authentication mechanisms and do not attempt repeated login attempts.

---

## Information Gathered

Depending on the protocol, authentication scripts may retrieve:

- Supported authentication methods
- Login capabilities
- Anonymous access status
- Authentication banners
- Security mechanisms
- Supported SASL methods
- Kerberos support
- NTLM support
- Basic authentication support
- Digest authentication support

The collected information helps determine whether additional security testing is appropriate.

---

## Common Authentication Scripts

Several official NSE scripts belong to the authentication category.

| Script | Purpose |
|---------|---------|
| ftp-anon | Checks for anonymous FTP access |
| http-auth | Identifies supported HTTP authentication methods |
| smtp-commands | Retrieves SMTP authentication capabilities |
| imap-capabilities | Lists IMAP authentication features |
| pop3-capabilities | Displays POP3 authentication mechanisms |
| ssh-auth-methods | Enumerates supported SSH authentication methods |
| xmpp-info | Retrieves XMPP authentication information |
| oracle-enum-users | Enumerates Oracle users (where permitted) |

The exact scripts available depend on the installed version of Nmap.

---

## Example Scan

Command:

```bash
nmap -sV --script auth target
```

Example output:

```text
21/tcp open ftp

| ftp-anon:
|   Anonymous FTP login allowed
|   Files:
|     README.txt
|     public/

22/tcp open ssh

| ssh-auth-methods:
|   Supported authentication methods:
|     publickey
|     password
```

This information reveals important aspects of the target's authentication configuration.

---

## Why Authentication Analysis Matters

Authentication is frequently the first line of defense protecting network services.

Weak authentication mechanisms may expose organizations to:

- Unauthorized access
- Credential theft
- Password attacks
- Privilege escalation
- Information disclosure
- Compliance violations

Identifying these weaknesses early allows administrators to strengthen access controls before attackers exploit them.

---

## Authentication Scripts vs Brute Scripts

Authentication scripts are often confused with brute-force scripts.

However, they serve different purposes.

| Authentication Scripts | Brute Scripts |
|------------------------|---------------|
| Analyze authentication mechanisms | Attempt repeated logins |
| Collect configuration information | Guess usernames and passwords |
| Low operational impact | Higher operational impact |
| Information gathering | Active credential testing |

Authentication scripts determine **how** a service authenticates users, while brute-force scripts attempt to determine **which credentials work**.

---

## Benefits

Authentication scripts provide several advantages.

| Benefit | Description |
|---------|-------------|
| Safe Enumeration | Collects authentication information without repeated login attempts |
| Protocol Awareness | Understands service-specific authentication protocols |
| Automation | Eliminates manual authentication analysis |
| Better Reconnaissance | Identifies security mechanisms before testing |
| Improved Planning | Helps determine appropriate next steps |

These advantages make authentication scripts an important part of professional reconnaissance.

---

## Limitations

Authentication scripts generally do **not**:

- Guess passwords
- Perform dictionary attacks
- Bypass authentication
- Exploit vulnerabilities
- Modify user accounts
- Create new credentials

Their objective is to understand authentication systems rather than compromise them.

---

## Best Practices

When using authentication scripts:

- Always combine them with `-sV`.
- Review authentication methods before performing password testing.
- Verify anonymous access immediately if detected.
- Document all supported authentication mechanisms.
- Obtain authorization before conducting further credential testing.

These practices improve both security assessments and reporting quality.

---

## Real-World Use Cases

Authentication scripts are commonly used during:

- Internal penetration tests
- External security assessments
- Authentication audits
- Compliance reviews
- Active Directory assessments
- Email server security reviews
- File server assessments
- VPN infrastructure audits

Understanding authentication capabilities helps security teams prioritize further testing activities.

---

## Chapter Summary

The **auth** category contains NSE scripts that analyze how services authenticate users and clients.

Rather than performing password attacks, these scripts identify supported authentication mechanisms, detect anonymous access, and collect authentication-related information that assists later stages of a security assessment.

Understanding authentication scripts provides an essential foundation before moving to the next category, which focuses on active credential testing through brute-force techniques.

---

# Next Chapter

## Chapter 14 — Brute Force Scripts