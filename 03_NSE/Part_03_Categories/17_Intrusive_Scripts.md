# Chapter 17 — Intrusive Scripts

The **intrusive** category contains NSE scripts that perform active security checks which may alter the behavior of the target system, generate noticeable network activity, or trigger security monitoring solutions.

Unlike safe or discovery scripts, intrusive scripts interact with services in ways that may stress applications, modify temporary states, or perform controlled exploitation attempts. Although they are extremely valuable during authorized penetration tests, they should never be executed against production systems without explicit permission.

Understanding the purpose and risks of intrusive scripts is essential for every security professional.

---

## What Are Intrusive Scripts?

Intrusive scripts are designed to perform more aggressive security testing than standard reconnaissance scripts.

Typical objectives include:

- Verifying vulnerabilities
- Testing authentication security
- Performing controlled exploitation checks
- Modifying temporary service states
- Sending crafted protocol requests
- Stress-testing service implementations
- Detecting insecure configurations through active interaction

Because these scripts actively interact with services, they generally produce more noticeable activity than other NSE categories.

---

## Executing Intrusive Scripts

Execute every intrusive script:

```bash
nmap --script intrusive target
```

Combine with service detection:

```bash
nmap -sV --script intrusive target
```

Run together with vulnerability scripts:

```bash
nmap -sV --script "vuln,intrusive" target
```

Execute a specific intrusive script:

```bash
nmap --script smb-vuln-ms17-010 target
```

Running only the required script minimizes unnecessary network activity.

---

## Why Are They Called "Intrusive"?

Unlike passive information gathering, intrusive scripts intentionally interact with services in ways that may influence normal operation.

Examples include:

- Sending malformed requests
- Testing authentication repeatedly
- Triggering application logic
- Performing protocol edge-case testing
- Requesting sensitive resources
- Executing vulnerability verification routines

These actions may be harmless under normal conditions, but they increase operational risk compared to passive scanning.

---

## How Intrusive Scripts Work

A typical intrusive workflow is shown below.

```text
Service Detection
        │
        ▼
Select Intrusive Script
        │
        ▼
Craft Specialized Requests
        │
        ▼
Transmit Requests
        │
        ▼
Analyze Responses
        │
        ▼
Determine Security Status
        │
        ▼
Generate Report
```

The script interacts directly with the service using protocol-aware logic.

---

## Examples of Intrusive Scripts

Examples include:

| Script | Purpose |
|---------|---------|
| smb-vuln-ms17-010 | Tests for EternalBlue vulnerability |
| ftp-brute | Attempts FTP authentication |
| ssh-brute | Attempts SSH authentication |
| http-slowloris-check | Tests susceptibility to Slowloris attacks |
| smtp-open-relay | Tests whether SMTP relay is unrestricted |
| http-put | Tests whether HTTP PUT uploads are allowed |

Many scripts belong to multiple categories because they perform more than one function.

---

## Example Scan

```bash
nmap -sV --script intrusive target
```

Example output:

```text
PORT    STATE SERVICE
445/tcp open  microsoft-ds

| smb-vuln-ms17-010:
|   VULNERABLE:
|   Remote Code Execution Vulnerability
|   State: VULNERABLE
|   Risk factor: Critical
|
|_  Host appears vulnerable.
```

The script actively verifies whether the vulnerability appears to exist.

---

## Potential Risks

Because intrusive scripts interact aggressively with services, they may produce unintended effects.

Possible risks include:

- Increased CPU utilization
- Temporary service slowdown
- IDS/IPS alerts
- Firewall logging
- Account lockouts
- Security monitoring notifications
- Temporary application instability

Although most NSE scripts are carefully written, operational impact should always be considered.

---

## Intrusive vs Safe Scripts

The difference between these categories is significant.

| Safe Scripts | Intrusive Scripts |
|--------------|------------------|
| Minimal operational impact | Higher operational impact |
| Passive information gathering | Active security testing |
| Suitable for routine scanning | Requires authorization |
| Rarely affects services | May influence service behavior |

Choosing the correct category depends on the assessment objectives and operational environment.

---

## Operational Considerations

Before executing intrusive scripts, security professionals should evaluate:

- Whether the target is a production system
- Maintenance windows
- Business impact
- Change management requirements
- Authorization scope
- Incident response procedures
- Monitoring systems

Planning reduces the likelihood of unexpected operational issues.

---

## Benefits

Intrusive scripts provide valuable capabilities.

| Benefit | Description |
|---------|-------------|
| Active Verification | Confirms suspected weaknesses |
| Improved Accuracy | Reduces uncertainty compared to passive analysis |
| Automated Testing | Performs repeatable security checks |
| Protocol Awareness | Understands service-specific behavior |
| Efficient Assessment | Verifies multiple targets quickly |

These benefits make intrusive scripts indispensable during professional penetration testing.

---

## Limitations

Intrusive scripts cannot:

- Guarantee successful exploitation
- Detect every vulnerability
- Replace manual penetration testing
- Replace exploit frameworks
- Bypass authorization requirements
- Eliminate false positives

Human verification remains an essential part of every security assessment.

---

## Best Practices

When using intrusive scripts:

- Obtain written authorization.
- Test production systems during approved maintenance windows.
- Execute only the required scripts.
- Monitor target systems throughout testing.
- Record all findings and unexpected behavior.
- Verify positive results manually.
- Inform stakeholders before beginning intrusive scans.

Responsible operation reduces operational risk and improves assessment quality.

---

## Real-World Use Cases

Intrusive scripts are commonly used during:

- Penetration testing
- Red team engagements
- Internal security assessments
- Security validation
- Vulnerability verification
- Infrastructure hardening
- Controlled exploit verification

Because they provide active verification, intrusive scripts are often executed after reconnaissance and vulnerability identification.

---

## Ethical and Legal Considerations

Intrusive scripts should never be executed against systems without explicit authorization.

Unauthorized intrusive testing may:

- Interrupt business operations
- Trigger incident response procedures
- Violate organizational policies
- Breach contractual agreements
- Result in legal consequences

Professional security testing always requires clearly defined scope and permission.

---

## Chapter Summary

The **intrusive** category contains NSE scripts that perform active security testing through protocol-aware interaction with target services.

Unlike passive reconnaissance scripts, intrusive scripts may generate noticeable network activity and have a greater operational impact. When executed responsibly and within an authorized scope, they provide valuable confirmation of security weaknesses while helping organizations validate the effectiveness of their defenses.

Understanding when and how to use intrusive scripts is a key skill for professional penetration testers and security assessors.

---

# Next Chapter

## Chapter 18 — External Scripts