# Chapter 45 — TCP Communication

So far, we have used the NSE HTTP library to communicate with web servers. Although this is extremely convenient, the HTTP library hides many of the underlying networking details.

Professional NSE developers often need more control.

Many network protocols do not use HTTP. Services such as FTP, SMTP, POP3, IMAP, Telnet, Redis, Memcached, and numerous custom applications communicate directly over TCP. In these situations, NSE scripts use **TCP sockets** to exchange raw data with remote services.

Understanding TCP communication enables you to write scripts that interact with virtually any TCP-based protocol.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Understand TCP sockets in NSE.
- Create TCP socket connections.
- Connect to remote services.
- Send data through a socket.
- Receive responses.
- Handle communication errors.
- Close connections properly.
- Build simple TCP-based NSE scripts.

---

# What Is a TCP Socket?

A TCP socket is an endpoint for network communication.

Conceptually:

```text
NSE Script

     │

     ▼

TCP Socket

     │

     ▼

Remote Service
```

Unlike HTTP libraries, sockets allow you to communicate directly with the protocol.

---

# Why Use TCP Sockets?

Many protocols are not supported by specialized libraries.

Examples include:

- Custom enterprise services
- Proprietary protocols
- Legacy applications
- Industrial systems
- Internal APIs

TCP sockets allow scripts to communicate with any TCP service.

---

# Importing Required Libraries

```lua
local nmap = require("nmap")
```

The `nmap` library provides socket functionality.

---

# Creating a Socket

Create a socket object.

```lua
local socket =
nmap.new_socket()
```

Workflow:

```text
Create Socket

↓

Configure

↓

Connect

↓

Exchange Data

↓

Close Socket
```

---

# Connecting to a Server

Example:

```lua
local status, err =
socket:connect(host, port)

if not status then

    return err

end
```

The connection must succeed before any data can be exchanged.

---

# Understanding connect()

```text
Script

↓

socket:connect()

↓

TCP Handshake

↓

Connected
```

If the connection fails, the returned error should be handled gracefully.

---

# Sending Data

After connecting:

```lua
socket:send("HELLO\r\n")
```

The transmitted data depends on the protocol being tested.

---

# Receiving Data

Read the server's response.

```lua
local status, response =
socket:receive()
```

Possible response:

```text
220 FTP Server Ready
```

---

# Closing the Socket

Always close the connection.

```lua
socket:close()
```

Closing unused sockets prevents unnecessary resource consumption.

---

# Complete Example

```lua
local nmap =
require("nmap")

portrule = function(host, port)

    return port.number == 21

end

action = function(host, port)

    local socket =
        nmap.new_socket()

    local status, err =
        socket:connect(host, port)

    if not status then

        return err

    end

    local status, banner =
        socket:receive()

    socket:close()

    return banner

end
```

This script connects to an FTP server and reads its banner.

---

# Execution Flow

```text
Create Socket

↓

Connect

↓

Receive Banner

↓

Close Socket

↓

Return Output
```

---

# Reading FTP Banners

Typical FTP server:

```text
220 FileZilla Server

```

or

```text
220 vsFTPd 3.0.5
```

Banner information often reveals the server software.

---

# Reading SMTP Banners

SMTP servers also send banners immediately.

Example:

```text
220 mail.example.com

ESMTP Postfix
```

The same socket code works without modification.

---

# Sending Commands

Some protocols require commands.

Example:

```lua
socket:send("QUIT\r\n")
```

or

```lua
socket:send("HELP\r\n")
```

The server then returns another response.

---

# Example Communication

```text
Client

↓

CONNECT

↓

220 Ready

↓

HELP

↓

214 Supported Commands

↓

QUIT

↓

221 Goodbye
```

Many text-based protocols follow this request-response pattern.

---

# Receiving Multiple Responses

Some services return more than one line.

Example:

```lua
local data = ""

repeat

    local status, line =
        socket:receive()

    if status then
        data = data .. line
    end

until not status
```

This technique collects larger responses.

---

# Setting a Timeout

Never wait forever.

Example:

```lua
socket:set_timeout(5000)
```

The timeout value is expressed in milliseconds.

If no response arrives within five seconds, the operation stops.

---

# Error Handling

Every network operation may fail.

Example:

```lua
local status, err =
socket:connect(host, port)

if not status then

    return
    "Connection failed: " .. err

end
```

Always check return values before continuing.

---

# Using Debug Messages

```lua
local stdnse =
require("stdnse")

stdnse.debug(
1,
"Opening TCP connection."
)
```

Execute with:

```bash
nmap -d
```

Debugging simplifies troubleshooting.

---

# Common TCP Workflow

Professional scripts often follow this sequence.

```text
Create Socket

↓

Set Timeout

↓

Connect

↓

Receive Banner

↓

Send Command

↓

Receive Reply

↓

Parse Data

↓

Close Socket

↓

Return Results
```

This pattern appears throughout many official NSE scripts.

---

# Practical Example

Suppose an FTP server responds:

```text
220 ProFTPD 1.3.6
```

Your script might generate:

```text
FTP Banner

-----------

220 ProFTPD 1.3.6
```

The returned banner can later be compared against vulnerability databases.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Forgetting `socket:close()` | Resource leaks |
| Ignoring connection errors | Causes runtime failures |
| Never setting a timeout | Script may hang indefinitely |
| Sending incorrect protocol commands | Server returns unexpected responses |
| Assuming every service sends a banner | Some protocols require requests first |

---

# Best Practices

When working with TCP sockets:

- Always close sockets.
- Set reasonable timeouts.
- Validate every network operation.
- Parse responses carefully.
- Separate communication logic from parsing logic.
- Use debugging during development.
- Reuse helper functions whenever possible.

These practices improve both performance and reliability.

---

# Lab Challenge

Complete the following tasks:

1. Create `tcp-banner.nse`.
2. Import the `nmap` library.
3. Create a TCP socket.
4. Connect to an FTP server.
5. Receive the server banner.
6. Display the banner.
7. Send the `QUIT` command.
8. Set a five-second timeout.
9. Add debug messages.
10. Test the script against FTP and SMTP services.

---

# What You Learned

After completing this lab, you should understand:

- How TCP sockets work in NSE.
- How to establish TCP connections.
- How to exchange raw protocol data.
- How to handle communication failures.
- How to safely close sockets.
- How banner-grabbing scripts operate internally.

These concepts provide the foundation for communicating with virtually any TCP-based service.

---

## Chapter Summary

TCP socket communication gives NSE developers complete control over interactions with remote services. By creating sockets, connecting to servers, sending protocol-specific commands, receiving responses, and handling errors gracefully, you can build scripts for protocols that are not covered by specialized NSE libraries.

This low-level approach is essential for banner grabbing, custom protocol analysis, and advanced security testing. In the next chapter, you will extend these concepts to **UDP communication**, where connectionless networking introduces a different set of techniques and challenges.

---

# Next Chapter

## Chapter 46 — UDP Communication