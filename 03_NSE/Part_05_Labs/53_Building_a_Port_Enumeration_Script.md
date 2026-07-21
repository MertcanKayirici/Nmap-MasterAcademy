# Chapter 53 — Building a Port Enumeration Script

One of the primary objectives of every network scan is discovering which services are running on a target system.

Although Nmap already identifies open ports, NSE allows us to extend this information by collecting additional details, organizing results, and presenting customized reports.

A port enumeration script can combine information from the **host**, **port**, and **service** objects to produce richer output than a traditional port scan.

In this chapter, you will build an NSE script that enumerates open ports and displays useful service information in a structured format.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Access port information.
- Read service attributes.
- Build structured reports.
- Filter ports based on conditions.
- Improve output readability.
- Combine multiple NSE concepts into a complete project.

---

# What Is Port Enumeration?

Port enumeration is the process of identifying network services running on a target.

Example:

```text
Target

      │

      ▼

Open Ports

      │

      ▼

Service Detection

      │

      ▼

Report
```

Instead of simply identifying open ports, enumeration gathers additional details about each service.

---

# Information Available

Each port object contains valuable information.

```text
Port Object

│

├── Number

├── Protocol

├── State

├── Service

└── Version (if detected)
```

These fields form the foundation of most NSE enumeration scripts.

---

# Required Libraries

```lua
local shortport =
require("shortport")
```

This library helps determine when the script should execute.

---

# Creating the Rule

For this example, the script runs against all TCP ports.

```lua
portrule = function(host, port)

    return port.protocol == "tcp"

end
```

---

# Accessing Port Information

The port number:

```lua
port.number
```

Protocol:

```lua
port.protocol
```

State:

```lua
port.state
```

Service:

```lua
port.service
```

---

# Basic Script

```lua
action = function(host, port)

    return

    "Port: " ..

    port.number

end
```

Output:

```text
Port: 80
```

---

# Displaying Multiple Fields

```lua
action = function(host, port)

    return

    "Port: " ..

    port.number ..

    "\nProtocol: " ..

    port.protocol ..

    "\nService: " ..

    port.service

end
```

Example output:

```text
Port: 80

Protocol: tcp

Service: http
```

---

# Including Host Information

The host object is also available.

```lua
return

"Host: " ..

host.ip ..

"\nPort: " ..

port.number
```

Example:

```text
Host: 192.168.1.20

Port: 443
```

---

# Complete Script

```lua
portrule = function(host, port)

    return port.protocol == "tcp"

end

action = function(host, port)

    local output = ""

    output = output ..

    "Host: " ..

    host.ip ..

    "\n"

    output = output ..

    "Port: " ..

    port.number ..

    "\n"

    output = output ..

    "Protocol: " ..

    port.protocol ..

    "\n"

    output = output ..

    "State: " ..

    port.state ..

    "\n"

    output = output ..

    "Service: " ..

    port.service

    return output

end
```

---

# Running the Script

```bash
nmap \
-sV \
-p80,443 \
--script port-enum.nse \
scanme.nmap.org
```

Example output:

```text
PORT    STATE SERVICE

80/tcp  open  http

| port-enum:

| Host: 45.33.xx.xx

| Port: 80

| Protocol: tcp

| State: open

| Service: http

|_
```

---

# Filtering Services

Suppose we only want web servers.

```lua
if port.service == "http" then

    return

    "HTTP Service Found"

end
```

Or SSH:

```lua
if port.service == "ssh" then

    return

    "SSH Service Found"

end
```

---

# Detecting Secure Services

Example:

```lua
if port.number == 443 then

    return

    "HTTPS Service"

end
```

This technique allows scripts to target specific technologies.

---

# Service Categorization

```text
Port

↓

Service

↓

Category

↓

Report
```

Example:

| Service | Category |
|----------|----------|
| HTTP | Web |
| HTTPS | Secure Web |
| FTP | File Transfer |
| SSH | Remote Access |
| SMTP | Email |
| DNS | Infrastructure |

Categorization improves report readability.

---

# Building a Professional Report

Instead of:

```text
80 tcp http
```

Return:

```text
Service Information

-------------------

Host      : 192.168.1.20

Port      : 80

Protocol  : TCP

State     : Open

Service   : HTTP
```

Structured reports are easier to interpret.

---

# Adding Debug Messages

```lua
local stdnse =
require("stdnse")

stdnse.debug(
1,
"Enumerating port " ..
port.number
)
```

Run:

```bash
nmap -d
```

Debug messages help during development.

---

# Practical Uses

Port enumeration is useful for:

- Asset inventory
- Service discovery
- Attack surface mapping
- Compliance verification
- Vulnerability assessment
- Network documentation

It is one of the most common tasks in penetration testing.

---

# Execution Flow

```text
Receive Port

↓

Read Properties

↓

Filter

↓

Generate Report

↓

Display Result
```

---

# Improving the Script

Possible enhancements include:

- Display version information.
- Detect SSL-enabled services.
- Group services by category.
- Highlight uncommon ports.
- Export results to structured tables.
- Combine results with vulnerability checks.

These additions make the script significantly more useful.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Ignoring the host object | Misses valuable context |
| Hardcoding port numbers | Reduces flexibility |
| Returning poorly formatted output | Difficult to read |
| Assuming service detection is always accurate | Detection may be incomplete |
| Forgetting service filtering | Script runs unnecessarily |

---

# Best Practices

When writing port enumeration scripts:

- Use descriptive labels.
- Format output consistently.
- Validate service names.
- Keep reports concise.
- Test against multiple operating systems.
- Use service detection (`-sV`) whenever possible.
- Separate enumeration logic from presentation.

---

# Lab Challenge

Complete the following tasks:

1. Create `port-enum.nse`.
2. Display the host IP.
3. Display the port number.
4. Display the protocol.
5. Display the service name.
6. Display the port state.
7. Filter only HTTP and HTTPS services.
8. Add debug messages.
9. Test against multiple hosts.
10. Extend the script to categorize services automatically.

---

# What You Learned

After completing this lab, you should understand:

- How to access host and port information.
- How to enumerate network services.
- How to build structured reports.
- How to filter services.
- How to improve script readability.
- How port enumeration supports reconnaissance.

This project demonstrates how simple NSE scripts can provide meaningful service information during network assessments.

---

## Chapter Summary

In this chapter, you developed a practical port enumeration script that combines host information, port attributes, and service details into a structured report. This project reinforced core NSE concepts such as working with host and port objects, filtering services, formatting output, and building reusable reconnaissance tools.

Port enumeration forms the foundation for more advanced security assessments. Once you know which services are available, you can begin interacting with them directly. In the next chapter, you will build a **Service Detection Script**, extending basic enumeration by communicating with network services and identifying software versions, banners, and implementation details.

---

# Next Chapter

## Chapter 54 — Building a Service Detection Script