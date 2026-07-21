# Chapter 34 — Action Function

If the rule function determines **when** an NSE script should execute, the **`action()` function** determines **what the script actually does**.

The `action()` function is the heart of every NSE script. Once a rule function returns `true`, Nmap calls `action()` and expects it to perform the script's primary task.

Whether a script retrieves an HTTP title, enumerates SMB shares, checks SSL certificates, or tests for vulnerabilities, all of that logic ultimately resides inside the `action()` function.

Understanding this function is one of the most important milestones in NSE development.

---

# What Is the action() Function?

The `action()` function is the main entry point of an NSE script.

Simplified structure:

```lua
action = function()

    -- Script logic

end
```

Whenever the rule function matches, Nmap executes this function automatically.

---

# Execution Flow

The following diagram illustrates the complete execution process.

```text
Nmap
 │
 ▼
Rule Function
 │
 ├── false
 │      │
 │      ▼
 │   Skip Script
 │
 └── true
        │
        ▼
   action()
        │
        ▼
 Perform Task
        │
        ▼
 Return Result
```

The `action()` function is never called unless the rule function succeeds.

---

# Basic Example

```lua
action = function()

    return "Hello from NSE!"

end
```

Output:

```text
| example:
|   Hello from NSE!
|_
```

The returned string becomes the script's output.

---

# Receiving Parameters

Depending on the rule type, `action()` receives different arguments.

For a `hostrule`:

```lua
action = function(host)

end
```

For a `portrule`:

```lua
action = function(host, port)

end
```

These parameters contain information collected by Nmap.

---

# The Host Object

The `host` parameter represents the scanned host.

Conceptually:

```text
Host
│
├── IP Address
├── Hostname
├── MAC Address
├── Operating System
└── Other Metadata
```

Example:

```lua
action = function(host)

    return host.ip

end
```

Possible output:

```text
192.168.1.15
```

---

# The Port Object

When using a `portrule`, the `port` object provides information about the matched service.

Conceptually:

```text
Port
│
├── Number
├── Protocol
├── State
├── Service Name
└── Version
```

Example:

```lua
action = function(host, port)

    return port.number

end
```

Output:

```text
80
```

---

# Calling Library Functions

The `action()` function rarely performs everything itself.

Instead, it calls functions from imported libraries.

Example:

```lua
local http = require("http")

action = function(host, port)

    local response = http.get(host, port, "/")

    return response.status

end
```

Workflow:

```text
action()
     │
     ▼
HTTP Library
     │
     ▼
Network Request
     │
     ▼
Response
```

---

# Processing Data

Most scripts perform several steps.

Example workflow:

```text
Receive Host
      │
      ▼
Connect
      │
      ▼
Receive Data
      │
      ▼
Parse Response
      │
      ▼
Return Result
```

The `action()` function coordinates these operations.

---

# Using Helper Functions

Large scripts divide work into helper functions.

Example:

```lua
local function getBanner(host, port)

    return http.get(host, port, "/")

end

action = function(host, port)

    return getBanner(host, port)

end
```

Instead of containing every detail itself, `action()` delegates specialized tasks.

---

# Returning Strings

The simplest return value is a string.

Example:

```lua
action = function()

    return "FTP service detected."

end
```

Output:

```text
FTP service detected.
```

---

# Returning Tables

Scripts may also return tables.

Example:

```lua
action = function()

    return {

        host = "server",
        service = "HTTP"

    }

end
```

Nmap formats structured tables into readable output.

This is common in official NSE scripts.

---

# Conditional Logic

The `action()` function often makes decisions.

Example:

```lua
action = function(host, port)

    if port.number == 443 then
        return "HTTPS"

    else
        return "Unknown"

    end

end
```

Different inputs produce different outputs.

---

# Handling Failures

Network operations can fail.

Example:

```lua
action = function(host, port)

    local response = http.get(host, port, "/")

    if not response then

        return "No response received."

    end

    return response.status

end
```

Gracefully handling failures makes scripts more reliable.

---

# Typical Professional Workflow

Many official scripts follow a similar structure.

```text
action()
 │
 ├── Validate Input
 │
 ├── Connect
 │
 ├── Send Request
 │
 ├── Receive Response
 │
 ├── Parse Data
 │
 ├── Format Output
 │
 └── Return Result
```

Keeping these steps separate improves readability.

---

# Example: HTTP Title Script

A simplified version of an HTTP title script might look like this:

```lua
local http = require("http")

action = function(host, port)

    local response = http.get(host, port, "/")

    if response then
        return response.body
    end

    return "No HTTP response."

end
```

Real scripts perform additional parsing and validation, but the overall structure is similar.

---

# Example: Banner Enumeration

```lua
action = function(host, port)

    local banner = getBanner(host, port)

    if banner then

        return banner

    end

    return "Banner unavailable."

end
```

Notice how the helper function keeps `action()` concise.

---

# What Should Not Be Inside action()

Avoid placing unrelated responsibilities inside the main function.

Poor design:

```text
action()

1000 lines
```

Better design:

```text
action()

│

├── connect()
├── authenticate()
├── parseResponse()
├── formatOutput()
└── return
```

Smaller functions are easier to debug and reuse.

---

# Common Patterns

Many official scripts follow patterns such as:

```lua
action()

↓

Connect

↓

Retrieve Information

↓

Parse Results

↓

Return Output
```

or

```lua
action()

↓

Authenticate

↓

Enumerate Data

↓

Generate Report
```

The overall workflow depends on the script's purpose.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Writing everything inside `action()` | Difficult to maintain |
| Ignoring failed requests | Unexpected crashes |
| Returning unformatted data | Poor output quality |
| Duplicating helper code | Unnecessary repetition |
| Using global variables | Reduced readability |

Keeping `action()` focused on orchestration rather than implementation avoids these issues.

---

# Best Practices

When implementing the `action()` function:

- Keep it short and readable.
- Delegate complex work to helper functions.
- Validate inputs before processing.
- Handle network failures gracefully.
- Return clear and informative results.
- Avoid unnecessary global state.
- Reuse library functions whenever possible.

A well-designed `action()` function acts as the coordinator of the script rather than containing every implementation detail.

---

# How Official NSE Scripts Use action()

Most official scripts follow this architecture:

```text
Libraries
     │
     ▼
Rule Function
     │
     ▼
action()
     │
     ├── Helper Functions
     ├── Protocol Libraries
     ├── Data Parsing
     ├── Error Handling
     └── Output Formatting
```

The `action()` function serves as the central controller, coordinating each stage of the script without becoming overly complex.

---

## Chapter Summary

The `action()` function is the execution engine of every NSE script. Once a rule function approves execution, `action()` performs the script's primary task by interacting with libraries, processing network data, and producing output.

Professional scripts keep `action()` concise by delegating specialized tasks to helper functions, validating inputs, handling errors gracefully, and returning well-formatted results.

With a solid understanding of rule functions and the `action()` function, we are now ready to explore how users can customize script behavior through **script arguments**, allowing NSE scripts to become far more flexible and configurable.

---

# Next Chapter

## Chapter 35 — Arguments