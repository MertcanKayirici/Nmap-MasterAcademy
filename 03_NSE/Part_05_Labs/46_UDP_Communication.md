# Chapter 46 — UDP Communication

In the previous chapter, we learned how NSE scripts communicate with services over TCP using sockets. TCP provides reliable, connection-oriented communication, making it suitable for protocols such as HTTP, FTP, SSH, and SMTP.

However, not every protocol uses TCP.

Many important network services—including DNS, DHCP, NTP, SNMP, TFTP, SIP, and numerous industrial protocols—use **UDP (User Datagram Protocol)**.

Unlike TCP, UDP is connectionless. There is no handshake, no guaranteed delivery, and no automatic retransmission. This makes UDP communication both faster and more challenging.

In this lab, you will learn how NSE communicates with UDP services and how to safely build UDP-based scripts.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Understand UDP communication in NSE.
- Create UDP sockets.
- Send UDP packets.
- Receive UDP responses.
- Handle packet loss.
- Implement timeouts.
- Build simple UDP enumeration scripts.

---

# TCP vs UDP

Before writing UDP scripts, it is important to understand how UDP differs from TCP.

| TCP | UDP |
|------|------|
| Connection-oriented | Connectionless |
| Reliable delivery | Best-effort delivery |
| Three-way handshake | No handshake |
| Ordered packets | No ordering guarantee |
| Error recovery | No retransmission |
| Larger overhead | Smaller overhead |

These differences directly affect how NSE scripts communicate with remote services.

---

# UDP Communication Workflow

Unlike TCP:

```text
Client

↓

Connect

↓

Exchange Data
```

UDP works differently.

```text
Client

↓

Send Datagram

↓

Wait

↓

Receive Response (Optional)
```

Notice that a response is **not guaranteed**.

---

# Importing Required Libraries

UDP communication also uses the `nmap` library.

```lua
local nmap = require("nmap")
```

---

# Creating a UDP Socket

Example:

```lua
local socket =
nmap.new_socket()
```

Although the same function creates the socket, it will later be configured for UDP communication.

---

# UDP Execution Flow

```text
Create Socket

↓

Set Timeout

↓

Send Packet

↓

Wait

↓

Receive Reply

↓

Close Socket
```

---

# Defining the Rule

Suppose we want to communicate with DNS.

```lua
portrule = function(host, port)

    return port.number == 53
        and port.protocol == "udp"

end
```

The script now executes only on UDP port 53.

---

# Sending a Datagram

Example:

```lua
socket:send("Hello")
```

Unlike TCP, there is no connection handshake before sending data.

The packet is transmitted immediately.

---

# Waiting for a Response

Example:

```lua
local status, response =
socket:receive()
```

Possible outcomes:

```text
Response received
```

or

```text
Timeout
```

or

```text
No reply
```

All three situations must be handled.

---

# Setting a Timeout

Timeouts are especially important in UDP.

```lua
socket:set_timeout(3000)
```

This waits up to three seconds for a response.

If nothing arrives, the operation stops.

---

# Handling Missing Responses

Many UDP services intentionally ignore unexpected packets.

Example:

```lua
local status, response =
socket:receive()

if not status then

    return "No response."

end
```

A missing response does **not** necessarily indicate that the host is offline.

---

# Complete Example

```lua
local nmap =
require("nmap")

portrule = function(host, port)

    return port.number == 53
        and port.protocol == "udp"

end

action = function(host, port)

    local socket =
        nmap.new_socket()

    socket:set_timeout(3000)

    socket:send("TEST")

    local status, response =
        socket:receive()

    socket:close()

    if not status then

        return "No UDP response."

    end

    return response

end
```

This script demonstrates the basic UDP workflow.

---

# DNS Example

A DNS server expects properly formatted DNS packets.

Conceptually:

```text
Client

↓

DNS Query

↓

UDP Packet

↓

DNS Server

↓

DNS Response
```

Professional NSE scripts generate valid DNS packets rather than plain text.

---

# SNMP Example

SNMP also uses UDP.

Typical workflow:

```text
Client

↓

SNMP GET Request

↓

UDP

↓

SNMP Agent

↓

SNMP Response
```

Many enumeration scripts rely on this communication model.

---

# TFTP Example

TFTP is another UDP-based protocol.

Example:

```text
Client

↓

Read Request

↓

UDP

↓

TFTP Server

↓

File Blocks
```

Although simple, packet ordering must still be handled correctly by the protocol.

---

# Packet Loss

One of UDP's biggest challenges is packet loss.

```text
Packet Sent

↓

Network

↓

Lost

↓

No Response
```

Unlike TCP, UDP does not automatically retransmit packets.

Scripts should be prepared for this possibility.

---

# Retrying Requests

Professional scripts often retry failed requests.

Example:

```text
Send Packet

↓

Response?

↓

No

↓

Retry

↓

Response?

↓

No

↓

Stop
```

Retries improve reliability on unstable networks.

---

# Using Debug Messages

Example:

```lua
local stdnse =
require("stdnse")

stdnse.debug(
1,
"Sending UDP packet."
)
```

Execute:

```bash
nmap -d
```

Debug output makes troubleshooting much easier.

---

# Practical Example

Suppose a DNS server responds.

```text
DNS Response Received

↓

Parse Packet

↓

Extract Information

↓

Return Result
```

The parsing stage depends on the protocol being analyzed.

---

# Common UDP Services

| Port | Service |
|------|----------|
| 53 | DNS |
| 67 | DHCP |
| 69 | TFTP |
| 123 | NTP |
| 161 | SNMP |
| 500 | IKE/IPsec |
| 514 | Syslog |

Many enterprise services rely on UDP.

---

# Comparing TCP and UDP Scripts

```text
TCP

↓

Connect

↓

Send

↓

Receive

↓

Close
```

versus

```text
UDP

↓

Send

↓

Wait

↓

Receive (Optional)

↓

Stop
```

The lack of a connection phase is the key difference.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Assuming every UDP packet receives a reply | Many services intentionally remain silent |
| Forgetting timeouts | Scripts may wait indefinitely |
| Treating packet loss as host failure | UDP is unreliable by design |
| Never retrying requests | Temporary packet loss may cause false negatives |
| Ignoring protocol specifications | Most UDP protocols require structured packets |

---

# Best Practices

When developing UDP scripts:

- Always configure a timeout.
- Expect packet loss.
- Handle missing responses gracefully.
- Retry when appropriate.
- Validate received data before parsing.
- Keep communication and parsing separate.
- Test against multiple UDP services.

These practices produce more reliable and predictable scripts.

---

# Lab Challenge

Complete the following tasks:

1. Create `udp-test.nse`.
2. Import the `nmap` library.
3. Create a UDP socket.
4. Configure a timeout.
5. Send a UDP packet.
6. Wait for a response.
7. Handle timeout conditions.
8. Add a retry mechanism.
9. Add debug messages.
10. Test the script against a DNS or SNMP server.

---

# What You Learned

After completing this lab, you should understand:

- The differences between TCP and UDP communication.
- How UDP sockets are used in NSE.
- Why timeouts are essential.
- How to handle packet loss.
- How to safely process UDP responses.
- Why many enumeration scripts rely on UDP.

These skills are essential for developing scripts targeting DNS, SNMP, NTP, TFTP, and many other UDP-based services.

---

## Chapter Summary

UDP communication introduces a different programming model from TCP. Since UDP is connectionless and does not guarantee packet delivery, NSE scripts must rely on timeouts, retries, and careful validation of responses. Despite these challenges, UDP remains critical for interacting with many core Internet services.

With both TCP and UDP communication covered, you now understand how NSE scripts communicate with remote systems at the transport layer. In the next chapter, you will learn how to make your scripts configurable by using **script arguments**, allowing users to customize script behavior directly from the Nmap command line.

---

# Next Chapter

## Chapter 47 — Working With Script Arguments