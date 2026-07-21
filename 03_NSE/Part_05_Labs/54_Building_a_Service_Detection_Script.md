# Chapter 54 — Building a Service Detection Script

Discovering an open port is only the first step of network reconnaissance.

Knowing that port **80** is open tells us that a web service exists, but it does not tell us **which web server is running**, **which software version is installed**, or **whether the service matches the expected protocol**.

Service detection answers these questions.

Professional penetration testers use service detection to identify technologies, verify configurations, detect outdated software, and prioritize vulnerability assessments.

In this chapter, you will build an NSE script that communicates with network services, analyzes their responses, and attempts to identify the software behind them.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Understand service detection.
- Connect to network services.
- Read service banners.
- Identify common protocols.
- Recognize software versions.
- Produce structured detection reports.
- Build a reusable service detection script.

---

# What Is Service Detection?

Service detection identifies the software running behind an open port.

Example:

```text
Port Scan

↓

Port 22 Open

↓

Connect

↓

Receive Banner

↓

SSH-2.0-OpenSSH_9.2

↓

Identify Service
```

The goal is to learn more than simply "port 22 is open."

---

# Why Service Detection Matters

Knowing the software provides valuable intelligence.

Example:

```text
Open Port

↓

Apache 2.4.57

↓

Research Vulnerabilities

↓

Determine Risk
```

Service versions often determine whether a system is vulnerable.

---

# Information We Want

A service detection script should attempt to collect:

- Service name
- Product
- Version
- Protocol
- Banner
- Port number
- Transport protocol

Example:

```text
HTTP

Apache

2.4.57

TCP

Port 80
```

---

# Required Libraries

```lua
local nmap =
require("nmap")

local stdnse =
require("stdnse")
```

---

# Defining the Rule

The script targets TCP services.

```lua
portrule = function(host, port)

    return port.protocol == "tcp"

end
```

---

# Creating the Socket

```lua
local socket =
nmap.new_socket()

socket:set_timeout(5000)
```

Timeouts prevent the script from waiting indefinitely.

---

# Connecting to the Service

```lua
local status, err =
socket:connect(host, port)

if not status then

    socket:close()

    return

    "Connection failed."

end
```

---

# Receiving the Banner

```lua
local ok, banner =
socket:receive()

socket:close()
```

Example banner:

```text
SSH-2.0-OpenSSH_9.2
```

---

# Identifying the Service

A simple approach is to search for known keywords.

Example:

```lua
if banner:find("OpenSSH") then

    return

    "SSH Server"

end
```

Likewise:

```lua
if banner:find("Apache") then

    return

    "Apache Web Server"

end
```

---

# Detecting FTP

Example banner:

```text
220 ProFTPD 1.3.6
```

Detection:

```lua
if banner:find("FTP") then

    return

    "FTP Service"

end
```

---

# Detecting SMTP

Example:

```text
220 mail.example.com ESMTP
```

Detection:

```lua
if banner:find("SMTP") then

    return

    "SMTP Service"

end
```

---

# Detecting HTTP

Sometimes the banner itself is unavailable.

Instead, send a request.

```lua
socket:send(

"HEAD / HTTP/1.1\r\n" ..

"Host: localhost\r\n\r\n"

)
```

Possible response:

```text
HTTP/1.1 200 OK
```

This confirms an HTTP service.

---

# Complete Script

```lua
local nmap =
require("nmap")

local stdnse =
require("stdnse")

portrule = function(host, port)

    return port.protocol == "tcp"

end

action = function(host, port)

    local socket =
        nmap.new_socket()

    socket:set_timeout(5000)

    local status, err =
        socket:connect(host, port)

    if not status then

        socket:close()

        return

        "Connection failed."

    end

    local ok, banner =
        socket:receive()

    socket:close()

    if not ok then

        return

        "No banner received."

    end

    local service = "Unknown"

    if banner:find("OpenSSH") then

        service = "SSH"

    elseif banner:find("Apache") then

        service = "HTTP (Apache)"

    elseif banner:find("FTP") then

        service = "FTP"

    elseif banner:find("SMTP") then

        service = "SMTP"

    end

    return

        "Detected Service: " ..

        service ..

        "\nBanner: " ..

        banner

end
```

---

# Running the Script

```bash
nmap \
-p21,22,25,80 \
--script service-detect.nse \
192.168.1.20
```

Example output:

```text
PORT   STATE SERVICE

22/tcp open ssh

| service-detect:

| Detected Service: SSH

| Banner:

| SSH-2.0-OpenSSH_9.2

|_
```

---

# Example Results

SSH:

```text
Detected Service

SSH

Version

OpenSSH_9.2
```

FTP:

```text
Detected Service

FTP

Version

ProFTPD 1.3.6
```

SMTP:

```text
Detected Service

SMTP

Version

Postfix
```

---

# Building a Detection Workflow

```text
Connect

↓

Receive Banner

↓

Analyze Text

↓

Known Pattern?

├── Yes

│     ↓

│  Identify Service

│

└── No

      ↓

Unknown Service
```

This pattern forms the basis of many fingerprinting scripts.

---

# Improving Detection

The current script uses simple string matching.

Future improvements could include:

- Regular expressions
- Protocol-specific requests
- Banner normalization
- Version extraction
- Fingerprint databases
- Confidence scoring

Professional detection engines combine many techniques.

---

# Practical Uses

Service detection supports:

- Vulnerability assessment
- Asset management
- Network inventory
- Technology identification
- Configuration auditing
- Security monitoring

It is one of the most valuable phases of reconnaissance.

---

# Debugging

Useful debug messages:

```lua
stdnse.debug(
1,
"Connecting..."
)

stdnse.debug(
1,
"Receiving banner..."
)

stdnse.debug(
1,
"Analyzing response..."
)
```

Run:

```bash
nmap -d
```

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Assuming every service sends a banner | Many services remain silent |
| Using exact string comparisons | Versions frequently change |
| Ignoring unknown services | Unknown results are still valuable |
| Forgetting socket timeouts | Scripts may hang |
| Not validating responses | Can cause runtime errors |

---

# Best Practices

When writing service detection scripts:

- Validate every network operation.
- Set socket timeouts.
- Handle missing banners.
- Use flexible pattern matching.
- Keep detection logic modular.
- Produce concise reports.
- Test against multiple protocols.

---

# Lab Challenge

Complete the following tasks:

1. Create `service-detect.nse`.
2. Connect to TCP services.
3. Receive service banners.
4. Identify SSH services.
5. Identify FTP services.
6. Identify SMTP services.
7. Format the output.
8. Add debug messages.
9. Test against at least five different services.
10. Extend the script to recognize additional protocols.

---

# What You Learned

After completing this lab, you should understand:

- How service detection works.
- How to analyze service banners.
- How to recognize common protocols.
- How to identify software products.
- How to organize detection results.
- Why service detection is essential for reconnaissance.

This project demonstrates how NSE can transform raw network responses into meaningful information for security assessments.

---

## Chapter Summary

In this chapter, you built a practical service detection script capable of connecting to TCP services, reading banners, identifying common protocols, and presenting structured results. While the detection logic used simple pattern matching, it illustrates the core workflow employed by more advanced fingerprinting tools.

Service detection is a natural progression from port enumeration, providing the context needed to evaluate software versions and identify potential security issues. In the next chapter, you will take another step forward by building a **Vulnerability Checker**, combining service identification with basic security checks to detect common weaknesses automatically.

---

# Next Chapter

## Chapter 55 — Building a Vulnerability Checker