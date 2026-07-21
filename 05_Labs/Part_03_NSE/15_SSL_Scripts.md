# Lab 15 — SSL Scripts

> Learn how to inspect SSL/TLS services using Nmap NSE scripts and analyze certificates, supported protocols, and encryption settings.

---

# Overview

Many modern services encrypt network traffic using SSL/TLS.

Examples include:

- HTTPS
- SMTPS
- IMAPS
- LDAPS
- FTPS

Encryption protects data during transmission, but the security of the connection depends heavily on how the service is configured.

Nmap provides several NSE scripts that allow administrators and security professionals to inspect SSL/TLS configurations without modifying the target system.

---

# Learning Objectives

After completing this lab, you will be able to:

- Retrieve SSL certificates.
- Identify certificate details.
- Detect supported TLS protocol versions.
- Enumerate supported cipher suites.
- Understand SSL-related findings.
- Interpret encryption configuration.

---

# Difficulty

⭐⭐⭐☆☆ Intermediate

---

# Estimated Time

45–60 Minutes

---

# Prerequisites

- Lab 11 completed
- Target with HTTPS or another SSL/TLS service

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| HTTPS Server | 192.168.56.20 | Target |

---

# Scenario

Your scan identified:

```text
443/tcp open https
```

Now you want to determine:

- Which certificate is presented?
- Which TLS versions are supported?
- Which cipher suites are available?
- Does the configuration appear appropriate?

---

# What is SSL/TLS?

SSL/TLS provides encrypted communication between clients and servers.

Modern deployments primarily use TLS.

Common services include:

| Port | Service |
|------|----------|
| 443 | HTTPS |
| 465 | SMTPS |
| 636 | LDAPS |
| 990 | FTPS |
| 993 | IMAPS |

---

# Step 1 — Retrieve Certificate Information

Run:

```bash
nmap --script ssl-cert -p443 192.168.56.20
```

Example Output

```text
Subject:
CN=example.local

Issuer:
Example CA

Valid From:
2026

Valid Until:
2027
```

---

# Step 2 — Enumerate Supported Cipher Suites

Run:

```bash
nmap --script ssl-enum-ciphers -p443 192.168.56.20
```

Example Output

```text
TLSv1.2

TLS_AES_256_GCM_SHA384

TLS_CHACHA20_POLY1305_SHA256
```

---

# Step 3 — Combine with Service Detection

Run:

```bash
nmap -sV --script ssl-cert,ssl-enum-ciphers -p443 192.168.56.20
```

This provides:

- HTTPS version
- Certificate
- Cipher suites
- Server software

---

# Understanding Certificates

Certificates commonly contain:

- Common Name (CN)
- Subject Alternative Names (SAN)
- Issuer
- Validity Period
- Public Key
- Signature Algorithm

These fields help identify the service and verify certificate deployment.

---

# Understanding Cipher Suites

Cipher suites define how encrypted communication is established.

Example:

```text
TLS_AES_256_GCM_SHA384
```

Components include:

- Key exchange
- Authentication
- Encryption
- Integrity protection

Modern servers typically support multiple cipher suites.

---

# Common SSL Scripts

| Script | Purpose |
|---------|---------|
| ssl-cert | Display certificate information |
| ssl-enum-ciphers | Enumerate supported cipher suites |
| ssl-date | Retrieve server time via TLS |
| ssl-known-key | Identify known public keys |

---

# NSE Script Deep Dive

## Script

```text
ssl-cert.nse
```

Category

```text
default
safe
discovery
```

Purpose

Retrieves and displays the server's SSL/TLS certificate.

Typical Uses

- Verify certificate deployment
- Identify hostnames
- Review certificate validity

Limitations

- Requires an SSL/TLS-enabled service.
- Does not validate organizational policy compliance.

Related Scripts

- ssl-enum-ciphers
- ssl-date

---

# Related Services

SSL/TLS commonly protects:

- HTTPS
- FTPS
- SMTPS
- IMAPS
- POP3S
- LDAPS

Understanding SSL/TLS helps analyze many encrypted network services.

---

# Thinking Like an Analyst

Suppose the certificate reports:

```text
CN=internal.example.local
```

Questions:

- Is this the expected hostname?
- Does the certificate match the service?
- Are additional hostnames listed?

---

Another Example

```text
Issuer:
Internal CA
```

Questions:

- Is the certificate publicly trusted?
- Is it intended only for internal use?
- Does it match organizational infrastructure?

---

# Common Mistakes

## Assuming Encryption Means Secure Configuration

Encryption alone does not guarantee an appropriate configuration.

Protocol support, certificate deployment, and cipher selection all matter.

---

## Ignoring Certificate Metadata

Certificates often reveal valuable infrastructure information such as hostnames and issuing authorities.

---

## Looking Only at Port 443

Many services use SSL/TLS on ports other than HTTPS.

---

# Challenge

Run:

```bash
nmap --script ssl-cert,ssl-enum-ciphers -p443 target
```

Document:

- Certificate Subject
- Issuer
- Validity Period
- Supported TLS versions
- Cipher suites

---

# Bonus Challenge

List SSL-related NSE scripts:

```bash
ls /usr/share/nmap/scripts/ssl*
```

Answer:

- Which scripts retrieve certificates?
- Which enumerate ciphers?
- Which inspect server time?
- Which appear specialized?

---

# Key Takeaways

- SSL/TLS enumeration reveals certificate and encryption details.
- Certificates provide valuable operational information.
- Cipher enumeration helps understand supported encryption methods.
- SSL-related NSE scripts support informed analysis of encrypted services.

---

# Next Lab

➡ **Lab 16 — DNS Scripts**

In the next lab, you will enumerate DNS servers, discover DNS records, and analyze name resolution services using NSE.