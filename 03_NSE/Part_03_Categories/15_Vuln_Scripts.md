# Chapter 14 — Brute Force Scripts

The **brute** category contains NSE scripts that attempt to discover valid credentials by systematically testing usernames, passwords, or authentication tokens against network services.

Unlike the **auth** category, which focuses on identifying authentication mechanisms, brute-force scripts actively attempt to authenticate to a service using multiple credential combinations.

These scripts are valuable during authorized penetration tests, password security audits, and controlled security assessments. However, because they generate repeated authentication attempts, they should only be used with proper authorization and a clear understanding of their potential impact.

---

## What Are Brute Force Scripts?

Brute-force scripts automate the process of testing authentication credentials.

Depending on the script and protocol, they may:

- Test common usernames
- Test common passwords
- Try username/password combinations
- Validate discovered credentials
- Identify weak passwords
- Detect default credentials
- Perform dictionary-based authentication attacks

These scripts help determine whether weak authentication practices expose a service to unauthorized access.

---

## Executing Brute Scripts

To execute all brute-force scripts, use:

```bash
nmap --script brute target
```

Brute-force scripts are usually combined with service detection.

```bash
nmap -sV --script brute target
```

Specific brute-force scripts may also be executed individually.

```bash
nmap --script ftp-brute target
```

```bash
nmap --script ssh-brute target
```

```bash
nmap --script http-brute target
```

Executing only the required script often reduces unnecessary authentication attempts.

---

## How Brute Force Scripts Work

Although each script is protocol-specific, most follow a similar workflow.

```text
Service Detection
        │
        ▼
Select Brute Script
        │
        ▼
Load Username List
        │
        ▼
Load Password List
        │
        ▼
Attempt Authentication
        │
        ▼
Authentication Successful?
      ┌───────┴────────┐
      │                │
     Yes              No
      │                │
Store Result      Try Next Pair
      │                │
      └────────┬───────┘
               ▼
        Generate Report
```

The process continues until valid credentials are found or the available credential lists have been exhausted.

---

## Common Brute Scripts

Nmap includes numerous brute-force scripts for different protocols.

Examples include:

| Script | Target Service |
|---------|----------------|
| ftp-brute | FTP |
| ssh-brute | SSH |
| http-brute | HTTP Basic/Digest Authentication |
| mysql-brute | MySQL |
| mssql-brute | Microsoft SQL Server |
| oracle-brute | Oracle Database |
| redis-brute | Redis |
| vnc-brute | VNC |
| telnet-brute | Telnet |
| smtp-brute | SMTP |
| imap-brute | IMAP |
| pop3-brute | POP3 |

Each script understands the authentication protocol used by its respective service.

---

## Example Scan

Attempt to identify weak SSH credentials.

```bash
nmap -sV --script ssh-brute target
```

Example output:

```text
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 9.7

| ssh-brute:
|   Accounts
|     admin:admin
|     backup:backup123
|   Statistics
|     Performed 214 guesses
|_    Login success: 2
```

The output identifies valid credentials that require immediate remediation.

---

## Credential Lists

Most brute-force scripts rely on credential lists.

Typical sources include:

- Default vendor credentials
- Common passwords
- Frequently used usernames
- Organization-specific wordlists
- Custom dictionaries

Using high-quality credential lists significantly improves testing effectiveness.

---

## Performance Considerations

Brute-force attacks can generate a large number of authentication requests.

Several factors influence performance:

- Network latency
- Service response time
- Rate limiting
- Account lockout policies
- Number of usernames
- Number of passwords
- Thread count

Large credential lists may substantially increase scan duration.

---

## Operational Risks

Brute-force testing introduces considerably more risk than information gathering.

Potential consequences include:

- Account lockouts
- Security alerts
- IDS/IPS detection
- Increased server load
- Audit log generation
- Temporary service restrictions

For this reason, brute-force scripts should be executed carefully and only within the authorized scope of an assessment.

---

## Brute Scripts vs Authentication Scripts

Although both categories relate to authentication, they have different objectives.

| Authentication Scripts | Brute Scripts |
|------------------------|---------------|
| Enumerate authentication methods | Test authentication credentials |
| Read configuration | Attempt repeated logins |
| Low operational impact | Higher operational impact |
| Reconnaissance | Active security testing |

Authentication scripts answer **"How does authentication work?"**, whereas brute-force scripts answer **"Can valid credentials be discovered?"**

---

## Benefits

When used responsibly, brute-force scripts provide valuable security insights.

| Benefit | Description |
|---------|-------------|
| Password Auditing | Identifies weak passwords |
| Default Credential Detection | Finds factory-default accounts |
| Security Validation | Tests password policy effectiveness |
| Automated Testing | Eliminates repetitive manual login attempts |
| Protocol Awareness | Uses service-specific authentication methods |

These capabilities help organizations strengthen authentication security.

---

## Best Practices

When using brute-force scripts:

- Obtain explicit authorization before testing.
- Review account lockout policies.
- Limit authentication attempts where appropriate.
- Use targeted username and password lists.
- Monitor system logs during testing.
- Document every successful authentication.
- Stop testing immediately if unexpected service instability occurs.

Responsible use reduces operational risk while maintaining assessment quality.

---

## Ethical and Legal Considerations

Because brute-force scripts actively attempt authentication, they should never be executed against systems without authorization.

Unauthorized credential attacks may:

- Violate organizational policies
- Breach contractual agreements
- Trigger security monitoring systems
- Result in legal consequences

Always ensure that brute-force testing is explicitly permitted within the scope of the engagement.

---

## Real-World Use Cases

Brute-force scripts are commonly used for:

- Internal password audits
- Red team exercises
- Penetration testing
- Security compliance assessments
- Default credential verification
- Password policy validation
- Infrastructure hardening reviews

Their purpose is to identify weak authentication practices before they can be exploited by attackers.

---

## Chapter Summary

The **brute** category contains NSE scripts that perform controlled credential testing against network services.

By automating authentication attempts using protocol-aware techniques, these scripts help identify weak passwords, default credentials, and ineffective authentication policies.

Because brute-force testing carries a higher operational risk than passive reconnaissance, these scripts should always be used responsibly, within authorized environments, and with careful consideration of account lockout policies and service stability.

---

# Next Chapter

## Chapter 15 — Vulnerability Scripts