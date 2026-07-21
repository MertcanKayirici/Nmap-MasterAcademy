# Nmap Master Academy

# Course 07

# Port Scanning

## Part 3 – Stealth Scan Techniques

---

## Course Information

**Course Number:** 07

**Part:** 3 of 4

**Difficulty:** Intermediate → Advanced

**Estimated Reading Time:** 60–90 Minutes

**Prerequisites**

- Course 07 – Part 1
- Course 07 – Part 2

---

# Table of Contents

10. TCP FIN Scan (-sF)

11. TCP NULL Scan (-sN)

12. TCP Xmas Scan (-sX)

13. TCP Maimon Scan (-sM)

14. Stealth Scan Comparison

15. Best Practices

16. Summary

---

# 10. TCP FIN Scan (-sF)

TCP FIN Scan sends a packet with only the FIN flag set.

Unlike a normal TCP connection, no handshake is performed.

Command

```bash
sudo nmap -sF 192.168.1.20
```

---

## Packet Flow

Open Port

```text
FIN

↓

Target

↓

(No Response)
```

Closed Port

```text
FIN

↓

Target

↓

RST
```

---

## Response Interpretation

| Response | Meaning |
|----------|----------|
| No Response | Open or Filtered |
| RST | Closed |
| ICMP Error | Filtered |

---

## Advantages

✓ Generates unusual packets

✓ Can bypass some stateless firewalls

✓ Does not complete a TCP connection

---

## Disadvantages

✗ Ineffective against many Windows systems

✗ Modern firewalls often detect it

✗ Less reliable than SYN Scan

---

# 11. TCP NULL Scan (-sN)

NULL Scan sends a TCP packet with **no flags set**.

Command

```bash
sudo nmap -sN 192.168.1.20
```

---

## Packet Flow

```text
TCP Packet

(No Flags)

↓

Target
```

---

## Response Interpretation

| Response | Meaning |
|----------|----------|
| No Response | Open or Filtered |
| RST | Closed |
| ICMP Error | Filtered |

---

## Why Is It Called NULL?

Because every TCP flag is cleared.

```text
SYN = 0

ACK = 0

FIN = 0

RST = 0

PSH = 0

URG = 0
```

---

## Advantages

✓ Extremely unusual packet

✓ May bypass poorly configured packet filters

---

## Disadvantages

✗ Unsupported by many Windows systems

✗ Frequently detected by IDS/IPS

---

# 12. TCP Xmas Scan (-sX)

Xmas Scan sets multiple TCP flags simultaneously.

Typically:

- FIN
- PSH
- URG

Command

```bash
sudo nmap -sX 192.168.1.20
```

---

## Why "Xmas"?

Because multiple flags are "lit up."

```
FIN ✓

PSH ✓

URG ✓
```

Like a Christmas tree with lights.

---

## Packet Flow

```text
FIN

PSH

URG

↓

Target
```

---

## Response Interpretation

| Response | Meaning |
|----------|----------|
| No Response | Open or Filtered |
| RST | Closed |
| ICMP Error | Filtered |

---

## Advantages

✓ Generates uncommon traffic

✓ Useful against some legacy packet filters

---

## Disadvantages

✗ Less reliable on modern operating systems

✗ Often detected by security appliances

---

# 13. TCP Maimon Scan (-sM)

Maimon Scan is a variation of the FIN Scan.

It sends packets with:

- FIN
- ACK

Command

```bash
sudo nmap -sM 192.168.1.20
```

---

## Packet Flow

```text
FIN

+

ACK

↓

Target
```

---

## Expected Responses

| Response | Meaning |
|----------|----------|
| No Response | Open or Filtered |
| RST | Closed |

---

## History

The scan was proposed by Uriel Maimon after observing differences in how certain BSD-based operating systems processed FIN/ACK packets.

It is primarily of historical interest today because most modern operating systems no longer exhibit this behavior.

---

## Advantages

✓ May identify ports on some legacy BSD systems

✓ Useful for research and historical understanding

---

## Disadvantages

✗ Rarely effective on modern systems

✗ Limited practical use

---

# RFC 793 Behavior

FIN, NULL, Xmas and Maimon scans rely on TCP behavior described in RFC 793.

According to the specification:

```
Closed Port

↓

RST
```

```
Open Port

↓

Ignore Packet
```

Many modern operating systems intentionally deviate from this behavior, reducing the effectiveness of these scans.

---

# Stealth Scan Comparison

| Scan | Open Port | Closed Port | Typical Use |
|------|-----------|-------------|-------------|
| FIN | No Response | RST | Firewall Evasion |
| NULL | No Response | RST | Firewall Testing |
| Xmas | No Response | RST | IDS Testing |
| Maimon | No Response | RST | Legacy BSD Systems |

---

# Operating System Compatibility

| Operating System | Reliability |
|-----------------|-------------|
| Linux | High |
| FreeBSD | Medium |
| OpenBSD | Medium |
| Windows | Low |

---

# Best Practices

✓ Prefer SYN Scan for general assessments.

✓ Use FIN, NULL and Xmas only when stealth techniques are appropriate.

✓ Verify results with additional scan types.

✓ Be aware that modern IDS/IPS solutions can detect these scans.

✓ Do not rely solely on RFC 793 behavior when assessing modern systems.

---

# Summary

This section introduced four TCP stealth scanning techniques.

Although less commonly used today, understanding these scans provides valuable insight into TCP behavior, firewall filtering, and historical scanning methodologies.

They remain useful for learning how Nmap interprets responses from different operating systems and security devices.

---

# Key Takeaways

✓ FIN Scan sends only the FIN flag.

✓ NULL Scan sends no TCP flags.

✓ Xmas Scan sets FIN, PSH and URG simultaneously.

✓ Maimon Scan sends FIN and ACK together.

✓ Modern operating systems reduce the effectiveness of these techniques.

✓ SYN Scan remains the preferred TCP scan in most situations.

---

# Next Part

## Part 4 – Advanced Scan Techniques

- Idle Scan (-sI)
- SCTP Scan
- IP Protocol Scan (-sO)
- Scan Selection Guide
- Best Practices
- Final Comparison