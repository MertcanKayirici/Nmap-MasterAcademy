# Chapter 10 — Safe Scripts

The **safe** category contains NSE scripts that are designed to gather information without intentionally disrupting the target system. These scripts perform passive or minimally invasive interactions, making them suitable for production environments where maintaining service availability is critical.

Although no network activity is entirely risk-free, scripts in the **safe** category are carefully selected to minimize the likelihood of causing crashes, service interruptions, or unexpected side effects.

For this reason, safe scripts are commonly used during network inventories, security audits, compliance assessments, and the reconnaissance phase of penetration tests.

---

## What Are Safe Scripts?

A script belongs to the **safe** category if it performs useful security-related tasks while avoiding operations that could negatively affect the target.

Typical safe scripts:

- Retrieve information
- Read configuration data
- Collect protocol metadata
- Enumerate available services
- Inspect certificates
- Query server capabilities

They generally do **not**:

- Exploit vulnerabilities
- Attempt authentication bypasses
- Perform brute-force attacks
- Modify system configuration
- Upload files
- Delete data
- Execute remote commands

Their purpose is observation rather than interaction.

---

## Executing Safe Scripts

The simplest way to execute every safe script is:

```bash
nmap --script safe target
```

Safe scripts are often combined with version detection.

```bash
nmap -sV --script safe target
```

Many security professionals also combine safe scripts with the default category.

```bash
nmap -sV --script "default,safe" target
```

This produces detailed reconnaissance results while maintaining a low operational risk.

---

## How Safe Scripts Are Classified

Every NSE script declares one or more categories.

Example:

```lua
categories = {
    "safe",
    "default"
}
```

During script selection, Nmap searches its script database for all scripts that belong to the requested category.

A script may belong to multiple categories simultaneously.

For example:

```lua
categories = {
    "safe",
    "discovery",
    "version"
}
```

This allows a single script to participate in different types of assessments.

---

## Characteristics of Safe Scripts

Safe scripts are designed around several core principles.

| Characteristic | Description |
|---------------|-------------|
| Read-only | Collects information without modifying the target |
| Low Impact | Minimizes network and system load |
| Reliable | Designed for routine assessments |
| Protocol-Aware | Communicates using legitimate application protocols |
| Non-Destructive | Avoids actions that may interrupt services |

These characteristics make safe scripts appropriate for most production environments.

---

## Examples of Safe Scripts

Several official NSE scripts belong to the safe category.

| Script | Purpose |
|---------|---------|
| http-title | Retrieves the title of a web page |
| http-server-header | Displays the HTTP Server header |
| ssl-cert | Retrieves SSL/TLS certificate information |
| ssh-hostkey | Collects SSH host keys |
| smtp-commands | Lists supported SMTP commands |
| dns-service-discovery | Retrieves DNS information |
| ntp-info | Collects NTP server information |
| smb-os-discovery | Identifies SMB operating system details |

These scripts gather valuable information without intentionally performing intrusive actions.

---

## Example Scan

Command:

```bash
nmap -sV --script safe scanme.nmap.org
```

Example output:

```text
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 9.7

| ssh-hostkey:
|   256 SHA256:xxxxxxxxxxxxxxxx

80/tcp  open  http

| http-title:
|   Example Website

| http-server-header:
|   Apache/2.4.62

443/tcp open ssl/http

| ssl-cert:
|   Subject: CN=scanme.nmap.org
|   Issuer: Let's Encrypt
```

The scan collects useful service information without attempting aggressive security testing.

---

## Safe Scripts vs Intrusive Scripts

The distinction between safe and intrusive scripts is one of the most important concepts in NSE.

| Safe Scripts | Intrusive Scripts |
|--------------|-------------------|
| Read information | May actively test the target |
| Low operational risk | Higher operational risk |
| Suitable for production | Better suited for test environments |
| Avoid disruptive behavior | May stress or affect services |
| Information gathering | Active security testing |

Choosing the correct category depends on the scope and authorization of the assessment.

---

## When Should Safe Scripts Be Used?

Safe scripts are recommended for:

- Production environments
- Corporate security audits
- Asset inventories
- Routine vulnerability assessments
- Compliance verification
- Change management reviews
- External perimeter reconnaissance
- Continuous monitoring

Because they minimize operational impact, they are often approved even in highly regulated environments.

---

## Limitations

Although safe scripts provide extensive information, they are intentionally conservative.

They generally do **not**:

- Verify exploitability
- Guess passwords
- Test default credentials aggressively
- Exploit vulnerabilities
- Perform denial-of-service testing
- Execute malware detection routines requiring intrusive behavior

Additional categories are required for these objectives.

---

## Best Practices

When using safe scripts:

- Combine them with `-sV` whenever possible.
- Execute them before intrusive categories.
- Review script documentation to understand exactly what each script does.
- Verify authorization before scanning production systems.
- Keep the NSE script database updated.
- Save results for later comparison during periodic assessments.

These practices improve both accuracy and operational safety.

---

## Common Misconceptions

One common misunderstanding is that **safe** means **completely risk-free**.

This is not entirely accurate.

Even safe scripts generate network traffic, establish connections, and communicate with services. While they are designed to avoid harmful behavior, poorly implemented services or unstable applications may still react unexpectedly.

Therefore, every security assessment should be performed responsibly and with proper authorization.

---

## Real-World Use Cases

Safe scripts are frequently used during:

- Enterprise asset discovery
- Internal security audits
- Cloud infrastructure assessments
- Web server reconnaissance
- Certificate inventory
- Network documentation
- Pre-penetration testing reconnaissance
- Continuous security monitoring

Because they provide detailed information with minimal disruption, they are often the preferred starting point for professional assessments.

---

## Chapter Summary

The **safe** category contains NSE scripts designed to gather valuable security information while minimizing the likelihood of disrupting target systems.

These scripts focus on enumeration, protocol analysis, certificate inspection, and service identification without attempting exploitation or other high-impact activities.

Understanding the safe category is essential because it represents the recommended approach for conducting reconnaissance and security assessments in production environments.

---

# Next Chapter

## Chapter 11 — Discovery Scripts