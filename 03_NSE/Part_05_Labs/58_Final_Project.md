# Chapter 58 — Final Project

Congratulations!

You have reached the final laboratory of the **Nmap Scripting Engine (NSE)** section.

Throughout the previous chapters, you learned how to:

- Build basic NSE scripts
- Use the Lua programming language
- Work with hosts and ports
- Communicate using TCP and UDP
- Perform HTTP requests
- Parse responses
- Handle errors
- Debug scripts
- Improve performance
- Refactor code
- Build practical reconnaissance tools

Now it is time to combine everything into a single professional project.

---

# Learning Objectives

By the end of this project, you will be able to:

- Design a complete NSE script.
- Apply modular programming.
- Combine multiple NSE libraries.
- Collect information from network services.
- Detect technologies.
- Report findings professionally.
- Apply performance optimizations.
- Build production-quality code.

---

# Project Goal

Build a script called

```text
recon-assistant.nse
```

that performs multiple reconnaissance tasks automatically.

Instead of checking only one thing, the script should gather as much useful information as possible.

---

# Features

Our final script should attempt to collect:

- Host IP
- Port number
- Service name
- Banner
- HTTP title
- HTTP server header
- Basic vulnerability indicators
- Response time
- Error information

---

# High-Level Architecture

```text
                Start
                  │
                  ▼
          Receive Target
                  │
                  ▼
         Check Port Rules
                  │
                  ▼
         Open TCP Connection
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
   HTTP Service?       Other Service?
        │                   │
        ▼                   ▼
 Retrieve Page         Read Banner
        │                   │
        └─────────┬─────────┘
                  ▼
        Analyze Information
                  │
                  ▼
      Generate Final Report
                  │
                  ▼
                Finish
```

---

# Required Libraries

```lua
local nmap =
require("nmap")

local http =
require("http")

local shortport =
require("shortport")

local stdnse =
require("stdnse")
```

---

# Script Layout

```text
Imports

↓

Constants

↓

Helper Functions

↓

portrule

↓

Information Collection

↓

Analysis

↓

Reporting
```

Professional scripts should follow a predictable structure.

---

# Defining the Rule

The script targets common TCP services.

```lua
portrule = function(host, port)

    return

    port.protocol == "tcp"

end
```

---

# Step 1 — Collect Basic Information

Every NSE script already has access to:

```lua
host.ip

port.number

port.protocol

port.service

port.state
```

Example:

```text
Host

192.168.1.20

Port

80

Service

HTTP
```

---

# Step 2 — Read the Banner

Create a socket.

```lua
local socket =
nmap.new_socket()
```

Connect.

```lua
socket:connect(host, port)
```

Receive data.

```lua
local status, banner =
socket:receive()
```

Close.

```lua
socket:close()
```

---

# Step 3 — Request HTTP Information

If the detected service is HTTP:

```lua
local response =

http.get(
host,
port,
"/"
)
```

Retrieve:

- Title
- Headers
- Response code

---

# Step 4 — Extract HTML Title

Example:

```lua
local title =

response.body:match(

"<title>(.-)</title>"

)
```

Possible output:

```text
Apache2 Ubuntu Default Page
```

---

# Step 5 — Read Server Header

HTTP headers often reveal software.

Example:

```text
Server:

Apache/2.4.58
```

Retrieve:

```lua
response.header.server
```

---

# Step 6 — Analyze the Banner

Example:

```lua
if banner then

    if banner:find("OpenSSH") then

        ...

    end

end
```

Possible detections:

- OpenSSH
- Apache
- nginx
- IIS
- vsFTPd
- Postfix

---

# Step 7 — Simple Vulnerability Rules

Example:

```lua
if banner then

    if banner:find("Apache/2.2") then

        ...

    end

end
```

Remember:

This is only a **potential** vulnerability indicator.

---

# Step 8 — Measure Response Time

Conceptually:

```text
Start Timer

↓

Connect

↓

Receive

↓

Stop Timer
```

Response time can indicate:

- Congestion
- Firewalls
- High latency

---

# Step 9 — Build the Report

Professional output:

```text
Recon Report

------------------------

Host

192.168.1.20

Port

80

Protocol

TCP

Service

HTTP

Title

Apache Default Page

Server

Apache/2.4.58

Banner

Apache HTTP Server

Possible Issues

None
```

---

# Complete Example

```lua
local nmap =
require("nmap")

local http =
require("http")

local shortport =
require("shortport")

portrule =
shortport.port_or_service(
80,
"http"
)

action = function(host, port)

    local output = {}

    local response =
        http.get(
        host,
        port,
        "/"
    )

    output[#output+1] =
        "Host: " ..
        host.ip

    output[#output+1] =
        "Port: " ..
        port.number

    output[#output+1] =
        "Service: " ..
        port.service

    if response then

        local title =
            response.body:match(
            "<title>(.-)</title>"
        )

        if title then

            output[#output+1] =
                "Title: " ..
                title

        end

        if response.header then

            if response.header.server then

                output[#output+1] =
                    "Server: " ..
                    response.header.server

            end

        end

    end

    return table.concat(
        output,
        "\n"
    )

end
```

---

# Running the Script

```bash
nmap \
-sV \
-p80 \
--script recon-assistant.nse \
scanme.nmap.org
```

---

# Example Output

```text
PORT   STATE SERVICE

80/tcp open http

| recon-assistant:

| Host: 45.33.xx.xx

| Port: 80

| Service: http

| Title: Example Domain

| Server: ECS

|_
```

---

# Possible Extensions

Professional developers could extend the project with:

- SSL certificate inspection
- Redirect detection
- Cookie analysis
- Technology fingerprinting
- HTTP security headers
- Robots.txt analysis
- Favicon hashing
- Directory discovery
- CVE lookups
- JSON output support

---

# Project Workflow

```text
Target

↓

Port Rule

↓

Connection

↓

HTTP Request

↓

Banner Analysis

↓

Header Analysis

↓

Title Extraction

↓

Vulnerability Checks

↓

Report Generation
```

---

# Performance Considerations

The project should:

- Reuse connections whenever possible.
- Avoid duplicate HTTP requests.
- Filter ports early.
- Handle failures gracefully.
- Return concise output.
- Close sockets immediately after use.

---

# Error Handling

Always validate:

```lua
if not response then

    return

    "Unable to retrieve HTTP response."

end
```

Never assume every request succeeds.

---

# Debugging

Useful debug messages include:

```lua
stdnse.debug(
1,
"Connecting..."
)

stdnse.debug(
1,
"Retrieving page..."
)

stdnse.debug(
1,
"Generating report..."
)
```

---

# Code Organization

A professional project separates responsibilities.

```text
Imports

↓

Configuration

↓

Network Functions

↓

Parsing Functions

↓

Detection Functions

↓

Output Functions

↓

Action
```

---

# Testing Checklist

Test against:

- Apache
- nginx
- IIS
- OpenSSH
- FTP
- SMTP
- Local virtual machines
- Docker containers
- Public test servers

Verify:

- Correct output
- Proper formatting
- Error handling
- Performance

---

# Final Project Challenge

Extend the project by implementing:

1. SSL detection.
2. Redirect following.
3. HTTP status reporting.
4. Security header detection.
5. Cookie enumeration.
6. Response timing.
7. Banner fingerprinting.
8. Custom script arguments.
9. JSON-style output.
10. Support for multiple HTTP paths.

---

# Skills You Have Mastered

You can now:

- Write Lua scripts.
- Develop NSE modules.
- Use official NSE libraries.
- Create TCP and UDP clients.
- Perform HTTP requests.
- Parse HTML.
- Extract banners.
- Handle errors.
- Debug scripts.
- Optimize performance.
- Refactor code.
- Build professional reconnaissance tools.

---

# End of Part Summary

Congratulations!

You have successfully completed **Part 05 — Labs**.

Throughout twenty laboratory chapters, you progressed from writing your first NSE script to designing a complete reconnaissance tool capable of collecting, analyzing, and presenting valuable information about network services.

More importantly, you learned not only *how* to write NSE scripts, but also *how to structure, optimize, debug, and maintain them* using professional software engineering practices.

You are now prepared to:

- Read and understand official NSE scripts.
- Modify existing scripts for your own needs.
- Create custom automation for penetration testing.
- Contribute to the Nmap NSE ecosystem.
- Develop advanced security tooling using Lua.

The knowledge gained in this part forms a strong foundation for real-world network reconnaissance and security assessments.

---

# Overall NSE Journey

```text
Introduction
      │
      ▼
Architecture
      │
      ▼
Script Categories
      │
      ▼
Lua Programming
      │
      ▼
Practical Labs
      │
      ▼
Final Project
      │
      ▼
Professional NSE Development
```

---

# Congratulations!

You have completed the **Nmap Scripting Engine (NSE)** section of **Nmap Master Academy Knowledge**.

You are no longer limited to running existing NSE scripts—you now have the knowledge to **design, develop, optimize, and maintain your own professional-grade Nmap scripts**.

The next stage of your Nmap journey is to apply these skills in real-world environments, contribute to the open-source community, and continue expanding your automation capabilities.

**Happy scripting, and happy hacking—ethically and responsibly.**