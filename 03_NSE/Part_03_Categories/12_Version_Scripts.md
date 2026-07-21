# Chapter 12 — Version Scripts

The **version** category contains NSE scripts that collect additional information about the software running on discovered services. These scripts complement Nmap's built-in version detection by identifying product details, software versions, supported features, and protocol-specific characteristics.

While the `-sV` option determines which service is running, version scripts extend this process by performing deeper analysis through application-layer communication.

This additional information helps security professionals identify outdated software, understand service capabilities, and prepare for vulnerability assessments.

---

## What Are Version Scripts?

Version scripts are designed to improve service fingerprinting.

Rather than simply reporting that a service is running, these scripts communicate with the service to obtain more detailed information.

Typical objectives include:

- Identifying software versions
- Collecting product information
- Detecting supported protocol features
- Reading service banners
- Identifying implementation details
- Retrieving server metadata
- Improving service fingerprints

The collected information provides a more accurate picture of the target environment.

---

## Executing Version Scripts

To execute every version script, use:

```bash
nmap --script version target
```

Version scripts are most effective when combined with service detection.

```bash
nmap -sV --script version target
```

Many professionals also combine them with the default category.

```bash
nmap -sV --script "default,version" target
```

This combination provides detailed service identification and additional protocol information.

---

## Relationship with -sV

One common misconception is that the **version** category replaces Nmap's version detection.

It does not.

The `-sV` option performs the initial service fingerprinting, while version scripts extend the information gathered during that process.

The workflow is typically:

```text
Open Port
      │
      ▼
Service Detection (-sV)
      │
      ▼
Version Script Selection
      │
      ▼
Protocol Communication
      │
      ▼
Additional Version Information
```

This layered approach improves both accuracy and efficiency.

---

## Information Collected

Depending on the protocol, version scripts may retrieve:

- Product names
- Software versions
- Server banners
- Supported protocol extensions
- Authentication mechanisms
- Build information
- Vendor identifiers
- Service capabilities

The exact information depends on how much the target service exposes.

---

## Common Version Scripts

Examples of official version-related scripts include:

| Script | Purpose |
|---------|---------|
| ssh2-enum-algos | Lists supported SSH algorithms |
| smtp-commands | Displays supported SMTP commands |
| ssl-cert | Retrieves SSL/TLS certificate details |
| ssl-enum-ciphers | Enumerates supported TLS cipher suites |
| http-server-header | Displays the HTTP Server header |
| ftp-syst | Retrieves FTP system information |
| mysql-info | Displays MySQL server information |
| redis-info | Collects Redis server details |

These scripts enhance the information already obtained through service detection.

---

## Example Scan

Command:

```bash
nmap -sV --script version scanme.nmap.org
```

Example output:

```text
PORT    STATE SERVICE VERSION
22/tcp  open  ssh OpenSSH 9.7

| ssh2-enum-algos:
|   kex_algorithms:
|     curve25519-sha256
|     ecdh-sha2-nistp256
|
|   server_host_key_algorithms:
|     rsa-sha2-512
|     ecdsa-sha2-nistp256

443/tcp open ssl/http Apache httpd

| ssl-cert:
|   Subject: CN=scanme.nmap.org
|   Issuer: Let's Encrypt

| ssl-enum-ciphers:
|   TLSv1.3:
|     TLS_AES_256_GCM_SHA384
|     TLS_CHACHA20_POLY1305_SHA256
```

This output provides protocol-specific information that cannot be obtained from service detection alone.

---

## Benefits of Version Scripts

Version scripts provide several important advantages.

| Benefit | Description |
|---------|-------------|
| Improved Fingerprinting | Collects additional service details |
| Better Accuracy | Refines service identification |
| Protocol Awareness | Understands application-layer protocols |
| Security Insight | Reveals supported features and configurations |
| Automation | Eliminates manual inspection |
| Integration | Works seamlessly with `-sV` |

These benefits make version scripts valuable during both reconnaissance and vulnerability assessment.

---

## Limitations

Version scripts focus on identification rather than security testing.

They generally do **not**:

- Exploit vulnerabilities
- Guess passwords
- Perform brute-force attacks
- Verify exploitability
- Modify target systems
- Conduct denial-of-service testing

Their primary goal is to improve understanding of the services being scanned.

---

## Best Practices

For effective use of version scripts:

- Always combine them with `-sV`.
- Review banners carefully, as they may reveal outdated software.
- Verify unexpected version information manually.
- Remember that some administrators intentionally hide or modify version strings.
- Update the NSE script database regularly.

These practices improve the accuracy of service fingerprinting.

---

## Real-World Use Cases

Version scripts are frequently used during:

- Asset identification
- Security audits
- Software inventory
- Vulnerability assessment preparation
- Patch verification
- Compliance assessments
- Network documentation
- Technology migration planning

The detailed information they provide is often essential for determining whether a service may be affected by known vulnerabilities.

---

## Version Scripts vs Discovery Scripts

Although both categories gather information, they have different objectives.

| Version Scripts | Discovery Scripts |
|-----------------|-------------------|
| Identify software versions | Enumerate resources |
| Improve service fingerprinting | Gather environmental information |
| Detect product details | Discover services and metadata |
| Focus on software identification | Focus on reconnaissance |

Discovery scripts answer **"What resources are available?"**, while version scripts answer **"Exactly what software is running?"**

---

## Chapter Summary

The **version** category enhances Nmap's service detection by collecting additional software and protocol information from discovered services.

Working alongside the `-sV` option, these scripts improve service fingerprinting, identify supported features, and provide valuable context for security assessments and vulnerability analysis.

A thorough understanding of version scripts enables security professionals to identify target technologies more accurately and prepare for deeper testing.

---

# Next Chapter

## Chapter 13 — Authentication Scripts