# Chapter 9 — Default Scripts

The **default** category is one of the most important script categories in the Nmap Scripting Engine (NSE). It contains a carefully selected collection of scripts that provide valuable information during a scan while maintaining a low risk of disrupting the target system.

When users execute the `-sC` option, Nmap automatically runs every script that belongs to the **default** category.

For many administrators, penetration testers, and security analysts, default scripts serve as the starting point for service enumeration because they collect useful information without requiring the user to manually select individual scripts.

---

## What Are Default Scripts?

Default scripts are official NSE scripts that have been designated as safe and broadly useful for general-purpose scanning.

Unlike specialized categories such as **vuln** or **brute**, the **default** category focuses on gathering information that is useful in nearly every assessment.

These scripts typically perform tasks such as:

- Service enumeration
- Banner collection
- Protocol identification
- SSL/TLS inspection
- HTTP analysis
- SMB enumeration
- DNS information gathering
- SSH information collection

The goal is to maximize useful output while minimizing unnecessary network traffic and operational risk.

---

## Executing Default Scripts

Running default scripts is straightforward.

The recommended command is:

```bash
nmap -sC target
```

The `-sC` option is simply a shortcut for:

```bash
nmap --script default target
```

Both commands execute the same collection of scripts.

Most professionals combine default scripts with version detection.

```bash
nmap -sC -sV target
```

This allows scripts to make decisions based on detected services and software versions.

---

## How Nmap Selects Default Scripts

Every NSE script contains a list of categories.

For example:

```lua
categories = {
    "default",
    "safe",
    "discovery"
}
```

When the user specifies:

```bash
nmap --script default
```

Nmap searches its script database and loads every script containing the **default** category.

Scripts that do not belong to this category are ignored unless explicitly requested.

---

## Typical Information Collected

Depending on the services discovered, default scripts may retrieve:

- HTTP page titles
- HTTP server headers
- SSL certificates
- SSH host keys
- DNS records
- SMB shares
- SMB operating system information
- NTP server information
- SMTP capabilities
- FTP banners
- POP3 capabilities
- IMAP capabilities

Because execution depends on detected services, every scan may produce different results.

---

## Example Scan

Command:

```bash
nmap -sC -sV scanme.nmap.org
```

Example output:

```text
PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 9.7

| ssh-hostkey:
|   256 SHA256:xxxxxxxxxxxxxxxx
|   3072 SHA256:yyyyyyyyyyyyyyyy

80/tcp  open  http    Apache httpd

| http-title:
|   Example Website

| http-server-header:
|   Apache/2.4.62

443/tcp open ssl/http Apache httpd

| ssl-cert:
|   Subject: CN=scanme.nmap.org
|   Issuer: Let's Encrypt
|   Validity:
|     Not Before...
|     Not After...
```

Even without selecting individual scripts, the scan produces significantly more information than a standard service scan.

---

## Common Default Scripts

Some of the most frequently executed default scripts include:

| Script | Purpose |
|---------|---------|
| http-title | Retrieves the title of a web page |
| http-server-header | Displays the HTTP Server header |
| ssl-cert | Retrieves SSL/TLS certificate information |
| ssh-hostkey | Collects SSH host keys |
| smb-os-discovery | Detects SMB operating system information |
| dns-service-discovery | Collects DNS service information |
| ftp-anon | Checks anonymous FTP access |
| smtp-commands | Lists supported SMTP commands |

These scripts represent only a small portion of the official default collection.

---

## Advantages of Default Scripts

Default scripts provide several important benefits.

| Advantage | Description |
|-----------|-------------|
| Safe | Designed to minimize impact on target systems |
| Automated | Executes useful scripts automatically |
| Efficient | No need to specify individual scripts |
| Informative | Provides detailed service information |
| Reliable | Officially maintained by the Nmap project |
| Flexible | Works with many different protocols |

For these reasons, many professionals include `-sC` in nearly every reconnaissance scan.

---

## Limitations

Although default scripts are extremely useful, they have limitations.

They generally do **not**:

- Perform aggressive vulnerability testing
- Execute brute-force attacks
- Attempt exploitation
- Conduct denial-of-service testing
- Perform intrusive authentication attacks

Their purpose is information gathering rather than offensive testing.

Users requiring more advanced functionality should combine default scripts with additional categories.

For example:

```bash
nmap -sC --script vuln target
```

or

```bash
nmap -sC --script auth target
```

---

## Best Practices

When using default scripts, consider the following recommendations.

- Combine `-sC` with `-sV`.
- Review script output carefully.
- Use XML or grepable output for large scans.
- Update the NSE script database regularly.
- Avoid assuming every service has an associated default script.
- Combine with additional categories only when necessary.

Following these practices helps maximize the usefulness of default scans.

---

## Real-World Use Cases

Default scripts are commonly used for:

- Initial penetration testing reconnaissance
- Internal network assessments
- External perimeter scans
- Asset inventory
- Service validation
- Security auditing
- Network documentation
- Vulnerability assessment preparation

Because they are both informative and relatively safe, they are suitable for a wide range of environments.

---

## Chapter Summary

The **default** category provides a carefully selected collection of official NSE scripts designed to gather valuable information during standard Nmap scans.

Executed using either `-sC` or `--script default`, these scripts perform protocol-aware enumeration, collect service metadata, inspect certificates, retrieve banners, and provide additional context beyond traditional port scanning.

Understanding the default category is essential because it forms the foundation of most NSE-based reconnaissance workflows.

---

# Next Chapter

## Chapter 10 — Safe Scripts