# Chapter 11 — Discovery Scripts

The **discovery** category contains NSE scripts that focus on gathering information about target systems, services, and network resources. Rather than attempting to exploit vulnerabilities or authenticate to services, discovery scripts are designed to identify valuable information that assists later stages of a security assessment.

In many penetration tests, discovery scripts are executed immediately after host and port scanning because they provide additional context that cannot be obtained through traditional scanning techniques alone.

These scripts are an essential part of the reconnaissance phase and help security professionals understand the target environment before performing more intrusive activities.

---

## What Are Discovery Scripts?

Discovery scripts are responsible for collecting information about a target without attempting to modify its behavior.

Typical tasks include:

- Identifying available services
- Enumerating network resources
- Retrieving protocol information
- Discovering shared resources
- Collecting banners
- Identifying server capabilities
- Enumerating available endpoints
- Gathering metadata

The information collected by these scripts often determines which techniques should be used during later stages of an assessment.

---

## Executing Discovery Scripts

To execute every discovery script, use:

```bash
nmap --script discovery target
```

Discovery scripts are commonly combined with service detection.

```bash
nmap -sV --script discovery target
```

They are also frequently executed alongside the default category.

```bash
nmap -sV --script "default,discovery" target
```

This combination produces a comprehensive reconnaissance scan.

---

## How Discovery Scripts Work

Most discovery scripts operate after service detection has completed.

The workflow typically follows these steps:

```text
Host Discovery
      │
      ▼
Port Scanning
      │
      ▼
Service Detection
      │
      ▼
Discovery Script Selection
      │
      ▼
Protocol Communication
      │
      ▼
Information Collection
      │
      ▼
Formatted Results
```

Because the scripts already know which services are available, they can communicate using the appropriate application-layer protocol.

---

## Information Gathered by Discovery Scripts

Depending on the target, discovery scripts may collect:

- Hostnames
- Domain names
- DNS records
- Web application titles
- Supported HTTP methods
- SSL certificates
- SSH host keys
- SMB shares
- LDAP information
- SNMP system details
- NTP server information
- FTP capabilities
- SMTP extensions

Each protocol provides different information that contributes to a more complete understanding of the target.

---

## Common Discovery Scripts

Some frequently used discovery scripts include:

| Script | Purpose |
|---------|---------|
| http-title | Retrieves the title of a web page |
| http-headers | Displays HTTP response headers |
| http-methods | Lists supported HTTP methods |
| dns-service-discovery | Discovers DNS services |
| smb-enum-shares | Enumerates SMB shares |
| smb-os-discovery | Identifies SMB operating system information |
| snmp-info | Retrieves SNMP system information |
| ssh-hostkey | Collects SSH host keys |
| ssl-cert | Retrieves SSL/TLS certificate information |
| ftp-anon | Checks for anonymous FTP access |

These scripts provide valuable reconnaissance information while requiring minimal manual effort.

---

## Example Scan

Command:

```bash
nmap -sV --script discovery scanme.nmap.org
```

Example output:

```text
PORT    STATE SERVICE VERSION
80/tcp  open  http Apache httpd

| http-title:
|   Example Domain

| http-methods:
|   Supported Methods:
|     GET
|     HEAD
|     OPTIONS

| http-headers:
|   Server: Apache
|   Content-Type: text/html

443/tcp open ssl/http

| ssl-cert:
|   Subject: CN=scanme.nmap.org
```

The scan provides considerably more information than standard service detection alone.

---

## Benefits of Discovery Scripts

Discovery scripts offer several important advantages.

| Benefit | Description |
|---------|-------------|
| Automated Enumeration | Eliminates repetitive manual tasks |
| Protocol Awareness | Understands application-layer protocols |
| Rich Information | Collects detailed service metadata |
| Efficient | Uses existing scan results |
| Scalable | Suitable for large environments |
| Extensible | Supports hundreds of protocols and services |

These benefits make discovery scripts one of the most frequently used NSE categories.

---

## Limitations

Discovery scripts are designed for information gathering rather than active security testing.

They generally do **not**:

- Verify vulnerabilities
- Exploit services
- Guess passwords
- Perform brute-force attacks
- Execute denial-of-service tests
- Modify remote systems

Additional script categories are required for those objectives.

---

## Best Practices

To obtain the best results:

- Always combine discovery scripts with `-sV`.
- Review collected information before proceeding with intrusive testing.
- Save results for future comparison.
- Verify unusual findings manually.
- Use XML output for large assessments.
- Keep the NSE script database up to date.

Following these practices improves both accuracy and efficiency.

---

## Real-World Use Cases

Discovery scripts are widely used for:

- Initial penetration testing reconnaissance
- Enterprise asset inventories
- Internal network mapping
- External attack surface analysis
- Security audits
- Cloud infrastructure assessments
- Network documentation
- Service validation

They often provide the information needed to determine which additional NSE categories should be executed.

---

## Discovery vs Version Scripts

Although discovery and version scripts are closely related, they serve different purposes.

| Discovery Scripts | Version Scripts |
|-------------------|-----------------|
| Gather additional service information | Identify software versions |
| Enumerate resources | Detect products and releases |
| Retrieve metadata | Improve service identification |
| Assist reconnaissance | Assist fingerprinting |

Discovery scripts focus on **learning more about a service**, whereas version scripts focus on **identifying exactly what the service is**.

---

## Chapter Summary

The **discovery** category contains NSE scripts that gather valuable information about network services, protocols, and system resources.

By communicating directly with discovered services, these scripts retrieve metadata, enumerate resources, and collect protocol-specific information that extends far beyond traditional port scanning.

Discovery scripts form a critical part of the reconnaissance process and provide the knowledge required for deeper security assessments.

---

# Next Chapter

## Chapter 12 — Version Scripts