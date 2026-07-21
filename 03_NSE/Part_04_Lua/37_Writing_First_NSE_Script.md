# Chapter 37 — Writing Your First NSE Script

After learning Lua syntax, variables, functions, tables, modules, error handling, libraries, rule functions, and the `action()` function, you now have everything necessary to write your first NSE script.

Although the first script will be intentionally simple, it demonstrates the complete lifecycle of an NSE script—from loading the file and evaluating its rule to executing `action()` and displaying results.

Understanding this workflow provides the foundation for developing increasingly advanced scripts.

---

# Learning Objectives

By the end of this chapter, you will be able to:

- Create a valid NSE script.
- Understand every required section.
- Execute the script with Nmap.
- Read its output.
- Expand it with additional functionality.
- Follow the structure used by official NSE scripts.

---

# Before We Begin

An NSE script is simply a Lua file with the extension:

```text
.nse
```

Example:

```text
hello.nse
```

This file can then be executed by Nmap.

---

# Our Goal

We will build a simple script that prints a message whenever it runs.

Workflow:

```text
Nmap
 │
 ▼
Load Script
 │
 ▼
Evaluate Rule
 │
 ▼
Run action()
 │
 ▼
Display Output
```

Although simple, this demonstrates the complete execution process.

---

# Step 1 — Create the Script

Create a new file named:

```text
hello.nse
```

---

# Step 2 — Add Metadata

Every professional script begins with metadata.

```lua
description = [[
A simple introductory NSE script.
]]

author = "Your Name"

license = "Same as Nmap"

categories = {"safe"}
```

This information helps users understand the purpose of the script.

---

# Step 3 — Define a Rule

For this example, we will execute once for every host.

```lua
hostrule = function(host)

    return true

end
```

Since the rule always returns `true`, the script runs for every discovered host.

---

# Step 4 — Add the action() Function

```lua
action = function(host)

    return "Hello from my first NSE script!"

end
```

The script is now complete.

---

# Complete Script

```lua
description = [[
A simple introductory NSE script.
]]

author = "Your Name"

license = "Same as Nmap"

categories = {"safe"}

hostrule = function(host)

    return true

end

action = function(host)

    return "Hello from my first NSE script!"

end
```

Even though it is only a few lines long, it follows the same structure used by official NSE scripts.

---

# Running the Script

Execute it with:

```bash
nmap --script ./hello.nse scanme.nmap.org
```

Workflow:

```text
Load hello.nse
       │
       ▼
Evaluate hostrule()
       │
       ▼
true
       │
       ▼
Run action()
       │
       ▼
Display Result
```

---

# Expected Output

Example:

```text
Nmap scan report for scanme.nmap.org

Host is up.

| hello:
|   Hello from my first NSE script!
|_

Nmap done.
```

Nmap automatically formats the returned string.

---

# Understanding Each Section

```text
Metadata
    │
    ▼
Rule
    │
    ▼
action()
    │
    ▼
Output
```

Each component has a specific responsibility.

---

# Adding Host Information

Instead of returning a fixed string, we can use information supplied by Nmap.

```lua
action = function(host)

    return "Scanning host: " .. host.ip

end
```

Possible output:

```text
Scanning host: 192.168.1.20
```

The script is now dynamic.

---

# Using the Hostname

```lua
action = function(host)

    if host.name then
        return host.name
    end

    return host.ip

end
```

The script now adapts depending on the available information.

---

# Running Once Per Port

Replace the host rule with a port rule.

```lua
portrule = function(host, port)

    return port.number == 80

end
```

Update `action()`.

```lua
action = function(host, port)

    return "HTTP Port Found"

end
```

Now the script executes only for TCP port 80.

---

# Using shortport

A more professional version imports `shortport`.

```lua
local shortport = require("shortport")

portrule = shortport.http
```

This replaces manual comparisons with a standard helper.

---

# Adding a Library

Import the HTTP library.

```lua
local http = require("http")
```

Use it:

```lua
action = function(host, port)

    local response = http.get(host, port, "/")

    if response then

        return response.status

    end

    return "No response."

end
```

The script now performs a real HTTP request.

---

# Improving Output

Instead of returning raw data, provide meaningful information.

Poor:

```text
200
```

Better:

```text
HTTP Status: 200 OK
```

Clear output is easier for users to interpret.

---

# Adding Error Handling

Network operations may fail.

```lua
local response = http.get(host, port, "/")

if not response then

    return "Unable to retrieve HTTP response."

end
```

Graceful error handling prevents confusing failures.

---

# Debugging the Script

While developing:

```lua
local stdnse = require("stdnse")

stdnse.debug(1, "Starting HTTP request.")
```

Run Nmap:

```bash
nmap -d --script ./hello.nse scanme.nmap.org
```

Debug output appears only when debugging is enabled.

---

# Script Evolution

Most professional scripts evolve gradually.

```text
Hello World
      │
      ▼
Read Host
      │
      ▼
Read Port
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
Report Results
```

Large NSE scripts begin with the same basic structure as this simple example.

---

# Typical Development Workflow

```text
Write Script
      │
      ▼
Run Nmap
      │
      ▼
Check Output
      │
      ▼
Debug
      │
      ▼
Improve
      │
      ▼
Repeat
```

This iterative approach is used by experienced NSE developers.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Missing `action()` | Script never performs any work |
| Missing rule function | Script is never selected |
| Returning nothing | No visible output |
| Forgetting required libraries | Functions unavailable |
| Testing against the wrong target | Misleading results |
| Ignoring error handling | Unexpected crashes |

Each issue becomes easier to identify with practice.

---

# Best Practices

When writing your first NSE scripts:

- Start with a minimal script.
- Add one feature at a time.
- Test after every change.
- Use helper functions for repeated logic.
- Keep `action()` concise.
- Prefer existing NSE libraries.
- Follow the structure used by official scripts.
- Write clear descriptions and meaningful output.

These habits scale well as scripts become more complex.

---

# Where to Go Next

Once comfortable writing simple scripts, begin experimenting with:

- Reading script arguments
- Performing HTTP requests
- Parsing protocol responses
- Enumerating services
- Using multiple libraries
- Returning structured output
- Handling network failures
- Writing reusable helper functions

Each new feature builds naturally upon the foundation established here.

---

## Chapter Summary

Writing your first NSE script marks the transition from learning Lua concepts to applying them in practice. A functional script consists of metadata, a rule function, and an `action()` function that performs the desired task and returns meaningful output.

Although this first example is intentionally simple, it demonstrates the complete execution lifecycle used by every professional NSE script. By gradually adding libraries, network communication, error handling, and structured output, you can transform a basic script into a powerful network automation tool.

The next chapter concludes Part 04 by exploring advanced NSE development techniques, including script design patterns, performance optimization, concurrency, reusable architectures, and recommendations for building production-quality NSE scripts.

---

# Next Chapter

## Chapter 38 — Advanced NSE Development 