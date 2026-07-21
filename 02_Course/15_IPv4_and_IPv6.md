# Nmap Master Academy

# Course 14

# DNS Resolution

---

## Course Information

**Course Number:** 14

**Difficulty:** Intermediate

**Estimated Reading Time:** 60–90 Minutes

**Prerequisites**

- Course 01–13

---

# Table of Contents

1. What is DNS?
2. Why DNS Resolution Matters
3. Forward DNS Resolution
4. Reverse DNS Resolution
5. DNS Resolution in Nmap
6. Disabling DNS Resolution (-n)
7. Forcing DNS Resolution (-R)
8. Specifying DNS Servers (--dns-servers)
9. Parallel DNS Resolution
10. Real-World Examples
11. Best Practices
12. Summary

---

# 1. What is DNS?

The Domain Name System (DNS) translates human-readable domain names into IP addresses.

For example:

```
example.com

↓

93.184.216.34
```

Without DNS, users would need to remember numerical IP addresses for every network service.

---

# 2. Why DNS Resolution Matters

DNS Resolution helps identify systems using meaningful names instead of raw IP addresses.

Examples:

```
192.168.1.10

↓

mail.company.local
```

```
10.0.0.5

↓

dc01.company.local
```

Hostnames often reveal the purpose of a system.

---

# 3. Forward DNS Resolution

Forward lookup converts a hostname into an IP address.

Example:

```
www.example.com

↓

93.184.216.34
```

Nmap automatically performs this conversion when scanning a hostname.

Command:

```bash
nmap www.example.com
```

---

# 4. Reverse DNS Resolution

Reverse DNS performs the opposite operation.

```
93.184.216.34

↓

example.com
```

This information is obtained from PTR records.

Reverse DNS is commonly used during IP range scanning.

---

# 5. DNS Resolution in Nmap

When an IP address is scanned, Nmap attempts a reverse DNS lookup by default.

Example:

```bash
nmap 192.168.1.10
```

Possible output:

```text
Nmap scan report for server01.local

(192.168.1.10)
```

---

# 6. Disabling DNS Resolution (-n)

DNS lookups can significantly slow large scans.

Disable hostname resolution:

```bash
nmap -n target
```

Advantages:

✓ Faster scanning

✓ Less DNS traffic

✓ Useful during large assessments

---

# Example

Without:

```bash
nmap target
```

With:

```bash
nmap -n target
```

The second scan skips all hostname lookups.

---

# 7. Forcing DNS Resolution (-R)

Normally, Nmap performs reverse lookups only when appropriate.

To force hostname resolution:

```bash
nmap -R target
```

This is useful when complete hostname information is required.

---

# 8. Specifying DNS Servers

Use custom DNS servers during a scan.

Command:

```bash
nmap --dns-servers 8.8.8.8 target
```

Multiple servers:

```bash
nmap --dns-servers 8.8.8.8,1.1.1.1 target
```

This overrides the system's default resolver.

---

# 9. Parallel DNS Resolution

When scanning many hosts, Nmap performs DNS queries in parallel.

```
Host1

Host2

Host3

Host4

↓

Parallel DNS Queries
```

This improves performance while resolving large numbers of hosts.

---

# 10. Real-World Examples

Scan without DNS:

```bash
nmap -n 192.168.1.0/24
```

Force reverse lookups:

```bash
nmap -R 192.168.1.0/24
```

Use Google's DNS:

```bash
nmap --dns-servers 8.8.8.8 target
```

Combine options:

```bash
nmap -sS -sV -n target
```

---

# 11. Best Practices

✓ Use `-n` during large network scans.

✓ Enable DNS resolution when documenting systems.

✓ Verify unexpected hostnames.

✓ Use trusted DNS servers.

✓ Remember that DNS records may be outdated.

---

# Summary

DNS Resolution allows Nmap to translate between hostnames and IP addresses.

Understanding when to enable, disable, or customize DNS lookups helps improve both scan performance and report quality.

---

# Key Takeaways

✓ DNS maps names to IP addresses.

✓ Reverse DNS uses PTR records.

✓ `-n` disables DNS resolution.

✓ `-R` forces hostname resolution.

✓ `--dns-servers` specifies custom DNS servers.

✓ DNS configuration can significantly affect scan speed.

---

# Next Course

## Course 15

# IPv4 and IPv6 Scanning