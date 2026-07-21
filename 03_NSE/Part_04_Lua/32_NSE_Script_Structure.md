# Chapter 32 — NSE Script Structure

After learning Lua fundamentals and becoming familiar with the available NSE libraries, it is time to understand how an actual NSE script is organized.

Although NSE scripts can vary in size and complexity, almost every official script follows a common structure. This consistent layout makes scripts easier to read, maintain, and extend.

In this chapter, we will examine each major component of an NSE script and explain its purpose before we begin writing our own scripts in the following chapters.

---

# Anatomy of an NSE Script

A simplified NSE script consists of several sections.

```text
Script Header
      │
      ▼
Library Imports
      │
      ▼
Metadata
      │
      ▼
Rule Definitions
      │
      ▼
Helper Functions
      │
      ▼
action()
      │
      ▼
Script Output
```

Every part has a specific responsibility.

---

# A Minimal NSE Script

The smallest functional NSE script looks like this:

```lua
description = [[
Simple NSE Script
]]

author = "Your Name"

license = "Same as Nmap"

categories = {"safe"}

hostrule = function(host)
    return true
end

action = function(host)

    return "Hello from NSE!"

end
```

Although simple, this script already contains the essential building blocks of an NSE program.

---

# Script Header

Most official scripts begin with a description.

Example:

```lua
description = [[

Retrieves the HTTP server banner.

]]
```

The description explains:

- What the script does
- What information it retrieves
- When it should be used

Good descriptions save users from reading the source code.

---

# Author Information

Example:

```lua
author = "John Doe"
```

Some scripts contain multiple authors.

```lua
author = {
    "Alice",
    "Bob"
}
```

Author information helps identify the script's maintainer.

---

# License

Official NSE scripts specify a license.

Example:

```lua
license = "Same as Nmap"
```

This ensures the script follows Nmap's licensing terms.

---

# Categories

Every NSE script belongs to one or more categories.

Example:

```lua
categories = {

    "safe",
    "default"

}
```

Possible categories include:

- auth
- broadcast
- brute
- default
- discovery
- dos
- exploit
- external
- fuzzer
- intrusive
- malware
- safe
- version
- vuln

These categories determine how scripts are selected during execution.

---

# Importing Libraries

Most scripts import one or more libraries.

Example:

```lua
local http = require("http")
local shortport = require("shortport")
local stdnse = require("stdnse")
```

Libraries provide reusable functionality and reduce code duplication.

---

# Rule Functions

Rules determine **when** a script should execute.

An NSE script normally defines one of the following:

- `hostrule`
- `portrule`
- `prerule`
- `postrule`

Only one rule is required.

---

## hostrule

Runs once for each host.

Example:

```lua
hostrule = function(host)

    return true

end
```

---

## portrule

Runs for matching ports.

Example:

```lua
portrule = function(host, port)

    return port.number == 80

end
```

Only hosts with port 80 will execute the script.

---

## prerule

Executes before scanning begins.

Example:

```lua
prerule = function()

    return true

end
```

Useful for initialization.

---

## postrule

Runs after all scanning is complete.

Example:

```lua
postrule = function()

    return true

end
```

Useful for generating summaries or reports.

---

# Helper Functions

Large scripts usually contain several helper functions.

Example:

```lua
local function getBanner(host, port)

    return http.get(host, port, "/")

end
```

These functions improve readability by separating individual tasks.

Instead of placing hundreds of lines inside `action()`, helper functions divide the logic into smaller units.

---

# The action() Function

The `action()` function is the heart of every NSE script.

When a rule matches, Nmap executes this function.

Example:

```lua
action = function(host, port)

    return "Hello"

end
```

Everything the script actually does happens inside `action()`.

---

# Returning Results

The return value becomes the script's output.

Example:

```lua
action = function()

    return "HTTP Service Detected"

end
```

Nmap displays:

```text
| http-example:
|   HTTP Service Detected
|_
```

Returning informative results is one of the primary responsibilities of an NSE script.

---

# Using Libraries Inside action()

A more realistic example:

```lua
local http = require("http")

action = function(host, port)

    local response = http.get(host, port, "/")

    return response.status

end
```

Workflow:

```text
Rule Matches
      │
      ▼
action()
      │
      ▼
HTTP Library
      │
      ▼
Receive Response
      │
      ▼
Return Output
```

---

# Typical Script Flow

A complete execution sequence looks like this:

```text
Nmap Starts
      │
      ▼
Load Script
      │
      ▼
Load Libraries
      │
      ▼
Evaluate Rule
      │
      ▼
Rule Matches?
 ┌────┴────┐
 │         │
No        Yes
 │         │
 ▼         ▼
Skip     action()
              │
              ▼
Generate Output
```

Understanding this lifecycle is essential for writing efficient scripts.

---

# Metadata Fields

Many scripts include additional metadata.

Examples:

```lua
dependencies = {

    "http-title"

}
```

```lua
runlevel = 1
```

Some scripts also define:

- Usage examples
- Script arguments
- Output examples

These fields improve usability and documentation.

---

# Script Organization

Professional scripts usually follow this order:

```text
Description
Author
License
Categories

Library Imports

Rule Definition

Constants

Helper Functions

Main action()

Return Output
```

Keeping a consistent structure makes scripts easier to understand.

---

# Large Script Architecture

As scripts become larger, they are often organized like this:

```text
Header
 │
 ├── Imports
 │
 ├── Constants
 │
 ├── Configuration
 │
 ├── Helper Functions
 │
 ├── Parsing Functions
 │
 ├── Network Functions
 │
 ├── Output Functions
 │
 └── action()
```

Each section focuses on a single responsibility.

---

# Reading Official NSE Scripts

When studying official scripts, begin by locating:

1. Description
2. Imported libraries
3. Rule definition
4. Helper functions
5. `action()`

Understanding these five sections allows you to quickly identify how the script works.

---

# Common Beginner Mistakes

| Mistake | Example |
|----------|---------|
| Forgetting `action()` | Script never executes |
| Missing rule function | Script is never selected |
| Importing unused libraries | Unnecessary overhead |
| Writing everything inside `action()` | Difficult maintenance |
| Poor script description | Users cannot understand the script |

A clear structure prevents these problems.

---

# Best Practices

When designing NSE scripts:

- Begin with a clear description.
- Import only the libraries you need.
- Choose the correct rule type.
- Divide complex logic into helper functions.
- Keep `action()` concise.
- Return meaningful output.
- Follow the layout used by official NSE scripts.

Consistent organization improves readability, testing, and long-term maintenance.

---

## Chapter Summary

An NSE script is much more than a collection of Lua statements. It follows a well-defined structure consisting of metadata, library imports, rule definitions, helper functions, and the `action()` function.

Understanding this architecture allows you to read official scripts with confidence and provides the foundation for writing your own professional NSE scripts. In the next chapter, we will examine rule functions in greater detail, focusing on **`hostrule`** and **`portrule`**, which determine exactly when an NSE script is executed.

---

# Next Chapter

## Chapter 33 — Hostrule and Portrule