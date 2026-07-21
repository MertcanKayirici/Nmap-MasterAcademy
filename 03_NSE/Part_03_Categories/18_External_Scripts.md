# Chapter 18 — External Scripts

The **external** category contains NSE scripts that rely on external resources or third-party services to complete their tasks. Unlike most NSE scripts, which perform all processing locally against the target, external scripts communicate with systems outside the scanning environment.

These external resources may include:

- Vulnerability databases
- WHOIS servers
- DNS services
- Internet reputation services
- Geolocation databases
- Certificate transparency services
- Online malware intelligence platforms

Because these scripts depend on external connectivity, their results may vary depending on network availability, service availability, and the quality of external data sources.

---

## What Are External Scripts?

External scripts extend Nmap's capabilities by incorporating information that cannot be obtained directly from the target.

Instead of relying solely on network communication with the scanned host, these scripts may:

- Query public databases
- Retrieve vulnerability information
- Perform online lookups
- Validate certificates
- Search reputation services
- Correlate discovered software with public intelligence

This allows NSE to combine local scan results with globally available security information.

---

## Executing External Scripts

Execute every external script:

```bash
nmap --script external target
```

Combine with service detection:

```bash
nmap -sV --script external target
```

Execute together with vulnerability scripts:

```bash
nmap -sV --script "vuln,external" target
```

Run a specific external script:

```bash
nmap --script vulners target
```

Many external scripts become significantly more useful when version detection (`-sV`) is enabled.

---

## How External Scripts Work

Unlike local NSE scripts, external scripts involve an additional communication step.

```text
Service Detection
        │
        ▼
Collect Target Information
        │
        ▼
Connect to External Service
        │
        ▼
Query External Database
        │
        ▼
Receive Results
        │
        ▼
Correlate with Scan Data
        │
        ▼
Generate Report
```

This workflow allows the script to enrich scan results with external intelligence.

---

## Common External Data Sources

External scripts may communicate with:

- CVE databases
- Vulnerability intelligence platforms
- WHOIS services
- DNS servers
- Public certificate repositories
- Internet reputation services
- Vendor advisory databases

The exact source depends on the script being executed.

---

## Common External Scripts

Examples include:

| Script | Purpose |
|---------|---------|
| vulners | Matches detected software against public vulnerability databases |
| whois-ip | Retrieves WHOIS information for IP addresses |
| dns-brute | May use external DNS resolution |
| ssl-cert | May validate certificate information against external trust data |
| http-google-malware | Checks websites against known malware lists (when supported) |

Some scripts belong to multiple NSE categories because they perform several related tasks.

---

## Example Scan

```bash
nmap -sV --script vulners target
```

Example output:

```text
PORT    STATE SERVICE VERSION
443/tcp open  https Apache httpd 2.4.49

| vulners:
|   Apache httpd 2.4.49
|     CVE-2021-41773
|     CVE-2021-42013
|     CVSS: 9.8
|
|_  Multiple known vulnerabilities identified.
```

The script correlates the detected software version with publicly available vulnerability intelligence.

---

## Internet Connectivity Requirements

Unlike most NSE categories, external scripts generally require Internet access.

Without connectivity:

- External lookups fail.
- Reputation services cannot be queried.
- Vulnerability databases cannot be contacted.
- Online intelligence cannot be retrieved.

For this reason, results may differ between connected and isolated environments.

---

## Advantages

External scripts provide several important benefits.

| Benefit | Description |
|---------|-------------|
| Threat Intelligence | Integrates public security information |
| Richer Results | Extends local scan data |
| Automated Correlation | Matches software with known issues |
| Current Information | Uses frequently updated databases |
| Reduced Manual Research | Automates online lookups |

These capabilities significantly improve the usefulness of reconnaissance and vulnerability assessments.

---

## Limitations

External scripts also introduce several limitations.

They may be affected by:

- Internet outages
- Service downtime
- API limitations
- Rate limiting
- Database inaccuracies
- Changes in external services

Results should therefore be considered advisory rather than absolute.

---

## Privacy Considerations

External scripts may reveal information about your scanning activity.

For example:

- Target IP addresses may be queried.
- Software versions may be transmitted.
- DNS requests may be logged.
- External services may record timestamps.

Organizations with strict privacy requirements should evaluate these implications before using external scripts.

---

## External vs Local Scripts

There is an important distinction between these categories.

| Local Scripts | External Scripts |
|---------------|------------------|
| Work entirely offline | Require external communication |
| Analyze only target responses | Correlate with external intelligence |
| Faster execution | Dependent on network latency |
| No third-party exposure | May reveal scanning activity |

Both categories complement each other during comprehensive assessments.

---

## Best Practices

When using external scripts:

- Enable Internet access if external lookups are required.
- Verify important findings using trusted sources.
- Be aware of organizational privacy policies.
- Review API usage limits where applicable.
- Keep the NSE script database updated.
- Document any external services used during assessments.

These practices improve both transparency and reliability.

---

## Real-World Use Cases

External scripts are commonly used for:

- Vulnerability assessments
- Threat intelligence gathering
- Security audits
- Asset inventory validation
- Compliance reviews
- Internet-facing infrastructure analysis
- Security research
- Patch prioritization

They help security teams enrich local scan results with globally available information.

---

## Ethical Considerations

Because external scripts communicate with third-party services, security professionals should ensure that:

- External queries are permitted.
- Sensitive information is not unnecessarily disclosed.
- Organizational policies are followed.
- Privacy requirements are respected.

Understanding how external services process submitted information is an important part of responsible security testing.

---

## Chapter Summary

The **external** category contains NSE scripts that enhance scan results by communicating with external services such as vulnerability databases, DNS infrastructure, WHOIS servers, and threat intelligence platforms.

By combining local scan data with publicly available security information, these scripts provide richer context and improve decision-making during security assessments.

However, because they depend on Internet connectivity and third-party services, external scripts should be used with an understanding of their operational, privacy, and reliability implications.

---

# Next Chapter

## Chapter 19 — Broadcast Scripts