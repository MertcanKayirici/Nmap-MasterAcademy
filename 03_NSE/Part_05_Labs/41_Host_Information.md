# Chapter 41 — Host Information

In the previous lab, our script simply returned a fixed message. While this demonstrated the structure of an NSE script, it did not use any information gathered during the scan.

One of the greatest strengths of the Nmap Scripting Engine is that it provides scripts with detailed information about every discovered host. This information is stored inside the **host object**.

Understanding the host object is essential because nearly every NSE script interacts with it. Whether you are performing service enumeration, vulnerability detection, or network discovery, the host object provides the context required for your script to make informed decisions.

In this lab, we will explore the host object and learn how to extract useful information from it.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Understand the purpose of the host object.
- Access host properties.
- Display IP addresses.
- Display hostnames.
- Explore available host information.
- Print multiple host attributes.
- Build reusable host information scripts.

---

# What Is the Host Object?

Whenever a `hostrule()` or `action()` function receives a parameter named `host`, Nmap passes an object containing information about the scanned target.

Conceptually:

```text
Nmap Scan

      │

      ▼

 Host Object

      │

      ├── IP Address

      ├── Hostname

      ├── MAC Address

      ├── Status

      ├── Interfaces

      └── Additional Metadata
```

This object is automatically created by Nmap.

---

# Basic Script

Create a new file:

```text
host-info.nse
```

Example:

```lua
description = [[
Displays host IP.
]]

author = "Your Name"

license = "Same as Nmap"

categories = {"safe"}

hostrule = function()

    return true

end

action = function(host)

    return host.ip

end
```

---

# Running the Script

```bash
nmap --script ./scripts/host-info.nse scanme.nmap.org
```

Example output:

```text
| host-info:
|   45.33.32.156
|_
```

Instead of returning a fixed string, the script now uses real scan data.

---

# The IP Address

The most commonly used field is:

```lua
host.ip
```

Example:

```lua
action = function(host)

    return "IP Address: " .. host.ip

end
```

Output:

```text
IP Address: 192.168.1.20
```

---

# Hostname

If Nmap resolves a hostname, it becomes available through:

```lua
host.name
```

Example:

```lua
action = function(host)

    return host.name

end
```

Possible output:

```text
scanme.nmap.org
```

---

# Handling Missing Hostnames

Not every target has a hostname.

Avoid:

```lua
return host.name
```

Instead:

```lua
return host.name or "Hostname not available"
```

This prevents confusing output.

---

# Displaying Multiple Values

Example:

```lua
action = function(host)

    return

        "Hostname: " ..

        (host.name or "Unknown")

        ..

        "\nIP: "

        ..

        host.ip

end
```

Example output:

```text
Hostname: scanme.nmap.org

IP: 45.33.32.156
```

---

# Formatting Output

Readable output is important.

Poor:

```text
45.33.32.156
```

Better:

```text
Host Information

IP Address : 45.33.32.156

Hostname   : scanme.nmap.org
```

Always make output easy to interpret.

---

# Inspecting the Host Object

During development, it is often useful to examine available fields.

Example:

```lua
for key, value in pairs(host) do

    print(key, value)

end
```

Possible output:

```text
ip

name

bin_ip

targetname

...
```

The exact fields may vary depending on the scan.

---

# Common Host Fields

| Field | Description |
|--------|-------------|
| `host.ip` | IP address |
| `host.name` | Hostname |
| `host.targetname` | Original target |
| `host.bin_ip` | Binary IP representation |

Some fields are always available, while others depend on scan results.

---

# Example: Display the Target

```lua
action = function(host)

    return

        "Original Target: "

        ..

        (host.targetname or host.ip)

end
```

If the scan began with:

```bash
nmap scanme.nmap.org
```

Output:

```text
Original Target: scanme.nmap.org
```

---

# Using Conditional Logic

Example:

```lua
action = function(host)

    if host.name then

        return host.name

    end

    return host.ip

end
```

Workflow:

```text
Hostname Exists?

      │

 ┌────┴────┐

 │         │

Yes       No

 │         │

 ▼         ▼

Return    Return

Name      IP
```

---

# Creating a Host Report

Example:

```lua
action = function(host)

    local output = ""

    output = output ..
        "Host Report\n"

    output = output ..
        "-----------\n"

    output = output ..
        "Hostname: " ..
        (host.name or "Unknown")

    output = output ..
        "\nIP: " ..
        host.ip

    return output

end
```

Output:

```text
Host Report

-----------

Hostname: scanme.nmap.org

IP: 45.33.32.156
```

---

# Debugging Host Data

While developing:

```lua
local stdnse = require("stdnse")

stdnse.debug(1, host.ip)
```

Run:

```bash
nmap -d --script ./scripts/host-info.nse scanme.nmap.org
```

This helps verify that the host object contains the expected values.

---

# Practical Example

Imagine scanning an internal network.

```text
192.168.1.10

192.168.1.15

192.168.1.22

192.168.1.35
```

Your script could generate a report such as:

```text
Host: Server01

IP: 192.168.1.10

-------------------

Host: Printer01

IP: 192.168.1.22

-------------------

Host: Unknown

IP: 192.168.1.35
```

This information can later be combined with port and service data.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Assuming `host.name` always exists | Some hosts have no hostname |
| Returning raw values without labels | Difficult to read |
| Ignoring `host.ip` | Most reliable identifier |
| Printing the entire table | Displays only a memory reference |
| Forgetting to test different targets | Results vary between hosts |

---

# Best Practices

When working with the host object:

- Always use `host.ip` as the primary identifier.
- Check whether optional fields exist.
- Format output clearly.
- Keep host-related logic separate from port-related logic.
- Test scripts against multiple hosts.
- Use debugging while developing.

These habits improve both reliability and readability.

---

# Lab Challenge

Complete the following tasks:

1. Create `host-info.nse`.
2. Display the IP address.
3. Display the hostname.
4. Display both values together.
5. Handle missing hostnames.
6. Print the original target name.
7. Explore the host object using `pairs()`.
8. Add debug messages.
9. Improve the formatting of the output.
10. Test the script against at least three different hosts.

---

# What You Learned

After completing this lab, you should understand:

- What the host object is.
- How Nmap passes host information to NSE scripts.
- How to access common host properties.
- How to safely handle optional fields.
- How to build readable host reports.

These concepts will be reused throughout the remaining labs.

---

## Chapter Summary

The host object is one of the most important data structures in the Nmap Scripting Engine. It provides scripts with information about the scanned target, including its IP address, hostname, and additional metadata collected during the scan.

By learning to access and format host information, you have taken another step toward writing practical NSE scripts. In the next lab, you will explore the **port object**, which provides detailed information about open ports, protocols, services, and service versions discovered by Nmap.

---

# Next Chapter

## Chapter 42 — Port Information