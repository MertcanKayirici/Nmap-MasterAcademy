# Chapter 51 — Building a Banner Grabber

Throughout this part of the book, you have learned the core building blocks of NSE development:

- Writing scripts
- Using libraries
- Working with sockets
- Handling TCP communication
- Processing output
- Managing errors
- Debugging scripts

Now it is time to combine these concepts into a practical security tool.

One of the simplest—and most useful—network reconnaissance techniques is **banner grabbing**.

Many services identify themselves immediately after a connection is established. This information often reveals:

- Service name
- Software version
- Operating system
- Vendor
- Product edition
- Build number

These details help security professionals identify outdated software, verify configurations, and prioritize vulnerability assessments.

In this chapter, you will build a complete TCP banner grabber using NSE.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Understand banner grabbing.
- Build a complete NSE script.
- Create TCP socket connections.
- Receive service banners.
- Handle communication failures.
- Produce professional output.
- Test the script against multiple services.

---

# What Is Banner Grabbing?

Many TCP services send information immediately after a client connects.

Example:

```text
Client

      │

      ▼

TCP Connection

      │

      ▼

FTP Server

      │

      ▼

220 ProFTPD 1.3.6
```

The server sends this information before the client sends any commands.

---

# Why Is Banner Grabbing Useful?

A banner may reveal:

- Product name
- Software version
- Vendor
- Protocol version
- Server hostname
- Operating system

Example:

```text
220 ProFTPD 1.3.6 Server
```

From a single banner, an analyst already knows:

- FTP service
- ProFTPD
- Version 1.3.6

---

# Common Services That Display Banners

| Port | Service |
|------|----------|
| 21 | FTP |
| 22 | SSH |
| 25 | SMTP |
| 110 | POP3 |
| 143 | IMAP |
| 6379 | Redis |
| 11211 | Memcached |

Many enterprise services identify themselves automatically.

---

# Project Overview

Our banner grabber will:

```text
Target Host

      │

      ▼

Create Socket

      │

      ▼

Connect

      │

      ▼

Receive Banner

      │

      ▼

Parse Output

      │

      ▼

Display Results
```

---

# Required Libraries

```lua
local nmap = require("nmap")

local stdnse = require("stdnse")
```

---

# Defining the Rule

To keep the example simple:

```lua
portrule = function(host, port)

    return port.protocol == "tcp"

end
```

The script runs against TCP ports.

---

# Creating the Socket

```lua
local socket =
nmap.new_socket()
```

Configure a timeout.

```lua
socket:set_timeout(5000)
```

---

# Connecting

```lua
local status, err =
socket:connect(host, port)

if not status then

    socket:close()

    return

    "Connection failed."

end
```

Never continue after a failed connection.

---

# Receiving the Banner

```lua
local ok, banner =
socket:receive()

socket:close()
```

If successful:

```text
220 FTP Ready
```

Otherwise:

```text
No response.
```

---

# Handling Errors

Always validate the response.

```lua
if not ok then

    return

    "No banner received."

end
```

Not every service sends a banner automatically.

---

# Adding Debug Messages

```lua
stdnse.debug(
1,
"Connecting..."
)

stdnse.debug(
1,
"Waiting for banner..."
)
```

Debugging is useful during development.

---

# Formatting the Output

Instead of returning only:

```text
220 FTP Ready
```

Create a report.

```lua
return

"Banner\n" ..

"------\n" ..

banner
```

Example:

```text
Banner

------

220 ProFTPD 1.3.6
```

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

    stdnse.debug(
    1,
    "Connecting..."
    )

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

    return

        "Banner\n" ..

        "------\n" ..

        banner

end
```

---

# Running the Script

```bash
nmap \
-p21 \
--script banner-grabber.nse \
192.168.1.20
```

Example output:

```text
PORT   STATE SERVICE

21/tcp open ftp

| banner-grabber:

| Banner

| ------

| 220 FileZilla Server 1.8.0

|_
```

---

# Testing Against Different Services

FTP:

```text
220 ProFTPD 1.3.6
```

SSH:

```text
SSH-2.0-OpenSSH_9.2
```

SMTP:

```text
220 mail.example.com ESMTP
```

Redis:

```text
-ERR unknown command
```

Notice that not every protocol behaves the same way.

---

# Improving the Script

Instead of printing raw banners, identify the service.

Example:

```text
SSH Banner

SSH-2.0-OpenSSH_9.2
```

or

```text
FTP Banner

220 ProFTPD 1.3.6
```

Small improvements greatly enhance readability.

---

# Detecting Empty Banners

Some services accept connections but remain silent.

Workflow:

```text
Connect

↓

Wait

↓

Timeout

↓

Return

"No banner received."
```

Always handle this case.

---

# Practical Uses

Banner grabbing helps with:

- Service identification
- Version detection
- Asset inventory
- Patch verification
- Vulnerability assessment
- Network reconnaissance

It is often the first step in a penetration test.

---

# Banner Grabbing Workflow

```text
Start

↓

Create Socket

↓

Connect

↓

Receive Banner

↓

Success?

├── Yes

│      ↓

│  Display Banner

│

└── No

       ↓

Return Error

↓

Close Socket
```

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Forgetting timeouts | Script may hang indefinitely |
| Assuming every service sends a banner | Many services remain silent |
| Ignoring failed connections | Leads to runtime errors |
| Forgetting to close sockets | Causes resource leaks |
| Returning raw data without formatting | Reduces readability |

---

# Best Practices

When building banner grabbers:

- Set socket timeouts.
- Validate every network operation.
- Close sockets correctly.
- Format output clearly.
- Add debug messages during development.
- Test against multiple protocols.
- Never assume banners are always present.

---

# Lab Challenge

Complete the following tasks:

1. Create `banner-grabber.nse`.
2. Connect to an FTP server.
3. Receive its banner.
4. Format the output.
5. Handle timeout conditions.
6. Add debug messages.
7. Test the script against SSH.
8. Test against SMTP.
9. Test against Redis.
10. Improve the report by identifying the protocol automatically.

---

# What You Learned

After completing this lab, you should understand:

- How banner grabbing works.
- How to use TCP sockets in a complete script.
- How to receive service banners.
- How to handle connection failures.
- How to produce readable reports.
- Why banner grabbing is an essential reconnaissance technique.

This chapter represents your first complete, real-world NSE utility.

---

## Chapter Summary

In this chapter, you combined multiple NSE concepts into a practical TCP banner grabber. By creating sockets, establishing connections, receiving banners, handling errors, and formatting results, you built a reusable reconnaissance tool that mirrors the design of many official NSE scripts.

Banner grabbing is often the first stage of service enumeration, providing valuable information about software versions and network services. In the next chapter, you will build an **HTTP Title Script**, which retrieves web pages and extracts the HTML `<title>` element—a common technique for identifying web applications and administrative interfaces.

---

# Next Chapter

## Chapter 52 — Building an HTTP Title Script