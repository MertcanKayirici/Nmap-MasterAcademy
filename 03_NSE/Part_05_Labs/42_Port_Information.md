# Chapter 42 — Port Information

In the previous lab, we explored the **host object**, which provides information about the scanned target itself. However, most NSE scripts are not interested only in hosts—they are designed to interact with **services running on specific ports**.

Whenever a script uses a `portrule()`, Nmap provides a second object called the **port object**. This object contains detailed information about the current port, including its number, protocol, state, service name, and version detection results.

Understanding the port object is fundamental for writing practical NSE scripts, since most scripts execute once for every matching port.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Understand the purpose of the port object.
- Access port properties.
- Display port numbers.
- Display protocols.
- Display detected services.
- Combine host and port information.
- Build simple service reporting scripts.

---

# What Is the Port Object?

The **port object** represents a single port discovered during an Nmap scan.

Conceptually:

```text
Host

│

├── Port 22
│      ├── State
│      ├── Protocol
│      ├── Service
│
├── Port 80
│      ├── State
│      ├── Protocol
│      ├── Service
│
└── Port 443
       ├── State
       ├── Protocol
       └── Service
```

For every port that matches the rule, Nmap creates a port object and passes it to the script.

---

# Creating a Port Script

Create a new file:

```text
port-info.nse
```

Example:

```lua
description = [[
Displays port information.
]]

author = "Your Name"

license = "Same as Nmap"

categories = {"safe"}

portrule = function(host, port)

    return true

end

action = function(host, port)

    return "Port: " .. port.number

end
```

---

# Running the Script

Example:

```bash
nmap -p 22,80,443 \
--script ./scripts/port-info.nse \
scanme.nmap.org
```

Possible output:

```text
| port-info:
|   Port: 22
|_
| port-info:
|   Port: 80
|_
| port-info:
|   Port: 443
|_
```

Notice that the script executes once for each matching port.

---

# Execution Flow

```text
Open Port

      │

      ▼

Evaluate portrule()

      │

      ▼

Rule Returns True

      │

      ▼

action(host, port)

      │

      ▼

Display Result
```

---

# Accessing the Port Number

The simplest property is:

```lua
port.number
```

Example:

```lua
action = function(host, port)

    return "Port Number: " .. port.number

end
```

Output:

```text
Port Number: 80
```

---

# Accessing the Protocol

Every port belongs to a protocol.

Example:

```lua
action = function(host, port)

    return port.protocol

end
```

Possible output:

```text
tcp
```

or

```text
udp
```

---

# Displaying Service Names

If Nmap identifies the service:

```lua
port.service
```

Example:

```lua
action = function(host, port)

    return port.service

end
```

Possible output:

```text
http
```

or

```text
ssh
```

or

```text
ftp
```

---

# Displaying Port State

Each port has a state.

Example:

```lua
action = function(host, port)

    return port.state

end
```

Possible output:

```text
open
```

Other possible states include:

- closed
- filtered
- open|filtered

---

# Combining Information

A more useful script combines multiple properties.

```lua
action = function(host, port)

    return

        "Port: " ..

        port.number ..

        "/" ..

        port.protocol ..

        "\nService: " ..

        port.service

end
```

Output:

```text
Port: 80/tcp

Service: http
```

---

# Building a Service Report

Example:

```lua
action = function(host, port)

    return

        "Host: " ..

        host.ip ..

        "\nPort: " ..

        port.number ..

        "\nProtocol: " ..

        port.protocol ..

        "\nService: " ..

        port.service

end
```

Example output:

```text
Host: 192.168.1.20

Port: 22

Protocol: tcp

Service: ssh
```

---

# Conditional Logic

Suppose we only want HTTP ports.

```lua
action = function(host, port)

    if port.service == "http" then

        return "HTTP Service Found"

    end

    return "Other Service"

end
```

Conditional logic allows scripts to behave differently depending on the detected service.

---

# Using the Port State

Example:

```lua
if port.state == "open" then

    return "Accessible"

end

return "Unavailable"
```

Most NSE scripts operate only on open ports.

---

# Displaying Multiple Ports

Suppose Nmap finds:

```text
22/tcp

80/tcp

443/tcp
```

Your script may generate:

```text
22/tcp  SSH

80/tcp  HTTP

443/tcp HTTPS
```

Readable formatting becomes increasingly important as the amount of information grows.

---

# Exploring the Port Object

During development:

```lua
for key, value in pairs(port) do

    print(key, value)

end
```

Possible fields include:

```text
number

protocol

service

state

version

reason

...
```

The available fields depend on scan options and Nmap's findings.

---

# Common Port Fields

| Field | Description |
|--------|-------------|
| `port.number` | Port number |
| `port.protocol` | TCP or UDP |
| `port.service` | Detected service |
| `port.state` | Current state |
| `port.version` | Version detection data (if available) |
| `port.reason` | Why Nmap assigned the state |

---

# Debugging Port Information

During development:

```lua
local stdnse = require("stdnse")

stdnse.debug(1, port.number)

stdnse.debug(1, port.service)
```

Run:

```bash
nmap -d \
--script ./scripts/port-info.nse \
scanme.nmap.org
```

Debugging confirms that the expected values are available.

---

# Practical Example

Assume a scan discovers:

```text
21/tcp ftp

22/tcp ssh

80/tcp http

3306/tcp mysql
```

A simple reporting script could produce:

```text
FTP detected on port 21

SSH detected on port 22

HTTP detected on port 80

MySQL detected on port 3306
```

Such information forms the basis of many enumeration and vulnerability scripts.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Confusing `host` and `port` objects | They contain different types of information |
| Assuming every port has a detected service | Version detection may be unavailable |
| Ignoring the port state | Closed or filtered ports should often be skipped |
| Hardcoding port numbers | Use the values provided by Nmap whenever possible |
| Returning raw values without labels | Output becomes difficult to interpret |

---

# Best Practices

When working with the port object:

- Always verify the port state.
- Use service names instead of only port numbers.
- Format output clearly.
- Avoid assuming version information is available.
- Test scripts against multiple services.
- Combine host and port information whenever appropriate.

---

# Lab Challenge

Complete the following tasks:

1. Create `port-info.nse`.
2. Display the port number.
3. Display the protocol.
4. Display the service name.
5. Display the port state.
6. Combine host and port information.
7. Print a formatted service report.
8. Explore the port object using `pairs()`.
9. Add debug messages.
10. Test the script against a host with at least five open ports.

---

# What You Learned

After completing this lab, you should understand:

- The structure of the port object.
- How Nmap provides information about individual services.
- How to access common port properties.
- How to combine host and port data.
- How to build readable service reports.

These concepts are used extensively in official NSE scripts.

---

## Chapter Summary

The port object provides detailed information about every port that matches a script's rule. By learning to access properties such as the port number, protocol, state, and detected service, you can write scripts that respond intelligently to the results of an Nmap scan.

Together with the host object introduced in the previous chapter, the port object forms the foundation of nearly every practical NSE script. In the next lab, you will begin using **NSE libraries** to perform real network communication instead of simply displaying information collected by Nmap.

---

# Next Chapter

## Chapter 43 — Using NSE Libraries