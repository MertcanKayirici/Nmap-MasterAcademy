# Chapter 33 — Hostrule and Portrule

Every NSE script must answer one fundamental question:

> **When should this script run?**

Nmap answers this question through **rule functions**.

A rule function determines whether a script should execute for a particular host, a particular port, before the scan begins, or after it finishes.

Among these rule types, **hostrule** and **portrule** are by far the most commonly used.

Understanding how they work is essential because every practical NSE script relies on one of them.

---

# The Role of Rule Functions

When Nmap discovers hosts and services, it does **not** automatically execute every script.

Instead, every script is asked a question.

```text
Should I run?
```

The rule function provides the answer.

```text
Host
 │
 ▼
Rule Function
 │
 ├── true
 │      │
 │      ▼
 │   Execute Script
 │
 └── false
        │
        ▼
    Skip Script
```

This mechanism prevents unnecessary execution and greatly improves performance.

---

# Types of Rule Functions

NSE supports four primary rule types.

| Rule | Purpose |
|------|----------|
| `hostrule` | Execute once per host |
| `portrule` | Execute for matching ports |
| `prerule` | Execute before scanning |
| `postrule` | Execute after scanning |

Most scripts use either:

- `hostrule`
- `portrule`

---

# Understanding hostrule

A `hostrule` decides whether a script should execute for an entire host.

Syntax:

```lua
hostrule = function(host)

    return true

end
```

If the function returns:

```lua
true
```

the script executes once for that host.

If it returns:

```lua
false
```

the script is skipped.

---

# Host Execution Flow

```text
Host Found
     │
     ▼
hostrule()
     │
 ┌───┴────┐
 │        │
True     False
 │        │
 ▼        ▼
Run      Skip
```

The decision is made before `action()` is called.

---

# Simple Hostrule Example

```lua
hostrule = function(host)

    return true

end
```

Every discovered host runs the script.

---

# Filtering Hosts

Rules may inspect host information.

Example:

```lua
hostrule = function(host)

    return host.ip ~= nil

end
```

Only hosts with a valid IP address execute the script.

---

# Practical Host Example

Suppose a script collects operating system information.

Workflow:

```text
Host
 │
 ▼
hostrule()
 │
 ▼
action(host)
 │
 ▼
Collect Information
```

Since the operation concerns the entire host rather than a specific service, `hostrule` is the appropriate choice.

---

# Understanding portrule

Most NSE scripts operate on services.

For these scripts, `portrule` is used.

Syntax:

```lua
portrule = function(host, port)

    return true

end
```

Unlike `hostrule`, the function receives both:

- host
- port

---

# Port Execution Flow

```text
Host
 │
 ▼
Open Port
 │
 ▼
portrule()
 │
 ┌───┴────┐
 │        │
True     False
 │        │
 ▼        ▼
Run      Skip
```

Every discovered port is evaluated independently.

---

# Matching a Specific Port

Example:

```lua
portrule = function(host, port)

    return port.number == 80

end
```

The script executes only for:

```text
80/tcp
```

---

# Matching Multiple Ports

Example:

```lua
portrule = function(host, port)

    return port.number == 80
        or port.number == 443

end
```

The script now runs on both:

```text
80/tcp
443/tcp
```

---

# Matching by Service Name

Instead of checking numbers, rules may inspect services.

Example:

```lua
portrule = function(host, port)

    return port.service == "http"

end
```

This approach is often more flexible because services may operate on non-standard ports.

---

# Matching by Protocol

Rules may also inspect the protocol.

Example:

```lua
portrule = function(host, port)

    return port.protocol == "tcp"

end
```

Only TCP services execute the script.

---

# Combining Conditions

Rules may contain complex logic.

Example:

```lua
portrule = function(host, port)

    return port.protocol == "tcp"
       and port.state == "open"
       and port.number == 443

end
```

This script executes only when:

- TCP
- Open
- Port 443

---

# Using the shortport Library

Most official scripts avoid writing complex rule logic manually.

Instead they use the `shortport` library.

Import:

```lua
local shortport = require("shortport")
```

Example:

```lua
portrule = shortport.http
```

This single line replaces dozens of manual checks.

---

# Common shortport Helpers

Some useful helper functions include:

| Helper | Matches |
|---------|----------|
| `shortport.http` | HTTP services |
| `shortport.ssl` | SSL/TLS services |
| `shortport.portnumber()` | Specific port |
| `shortport.service()` | Service name |
| `shortport.version_port_or_service()` | Version-detected services |

These helpers improve readability and consistency.

---

# Example Using shortport

Instead of:

```lua
portrule = function(host, port)

    return port.number == 80
        or port.number == 8080
        or port.number == 8000

end
```

You can write:

```lua
portrule = shortport.http
```

The intent is immediately clear.

---

# Hostrule vs. Portrule

| hostrule | portrule |
|----------|-----------|
| Runs once per host | Runs once per matching port |
| Uses host information | Uses host and port information |
| Suitable for host-wide tasks | Suitable for service-specific tasks |
| Fewer executions | Potentially many executions |

Choosing the correct rule type improves efficiency.

---

# Real-World Examples

## Host Script

```text
Host
│
├── Collect hostname
├── Detect operating system
├── Determine uptime
└── Display summary
```

One execution is sufficient.

---

## Port Script

```text
Host
│
├── 22/tcp
├── 80/tcp
├── 443/tcp
└── 3306/tcp
```

Each service is evaluated separately.

---

# Choosing the Correct Rule

Use **hostrule** when:

- Gathering host information
- Enumerating operating systems
- Collecting host-wide metadata
- Performing inventory tasks

Use **portrule** when:

- Communicating with services
- Testing protocols
- Detecting vulnerabilities
- Enumerating banners
- Checking authentication

Most vulnerability and version-detection scripts use `portrule`.

---

# Performance Considerations

Poorly designed rules waste time.

Bad example:

```lua
return true
```

The script executes everywhere.

Better example:

```lua
return port.number == 443
```

Only relevant services are tested.

Efficient rules reduce:

- Scan duration
- CPU usage
- Network traffic

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Always returning `true` | Script runs unnecessarily |
| Using `hostrule` for service detection | Wrong execution model |
| Ignoring `port.state` | Closed ports may be processed |
| Repeating logic already provided by `shortport` | Unnecessary code |
| Writing overly complex conditions | Difficult maintenance |

Keeping rule functions focused and concise improves readability.

---

# Best Practices

When writing rule functions:

- Choose the appropriate rule type.
- Keep rule logic simple.
- Prefer `shortport` helpers whenever possible.
- Avoid unnecessary comparisons.
- Execute scripts only when needed.
- Document unusual rule conditions.

Well-designed rules make scripts faster and easier to maintain.

---

## Rule Evaluation in the NSE Lifecycle

The following diagram illustrates where rule functions fit into the execution process.

```text
Load Script
      │
      ▼
Import Libraries
      │
      ▼
Evaluate Rule
      │
 ┌────┴────┐
 │         │
False     True
 │         │
 ▼         ▼
Skip     action()
              │
              ▼
         Produce Output
```

Notice that the `action()` function is **never executed** unless the rule function returns `true`.

---

## Chapter Summary

Rule functions determine **when** an NSE script should execute.

The `hostrule` function evaluates entire hosts, while `portrule` evaluates individual services. Choosing the correct rule type ensures that scripts run only where they are relevant, improving both performance and accuracy.

In professional NSE development, rule functions are intentionally kept simple, often relying on helper libraries such as `shortport` to express matching conditions clearly and concisely.

With rule selection understood, we are now ready to examine the heart of every NSE script—the **`action()` function**, where the actual work of the script is performed.

---

# Next Chapter

## Chapter 34 — Action Function