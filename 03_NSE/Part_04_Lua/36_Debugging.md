# Chapter 36 — Debugging

No programmer writes perfect code on the first attempt. Even experienced developers introduce bugs, make incorrect assumptions, or encounter unexpected behavior during execution.

The process of finding, understanding, and fixing these problems is known as **debugging**.

Debugging is one of the most valuable skills an NSE developer can acquire. A well-written debugging strategy not only reduces development time but also improves script quality and reliability.

In this chapter, we will explore the tools, techniques, and best practices used to debug Lua programs and NSE scripts.

---

# What Is Debugging?

Debugging is the process of identifying and correcting errors in a program.

A typical workflow looks like this:

```text
Write Code
     │
     ▼
Run Script
     │
     ▼
Unexpected Behavior
     │
     ▼
Investigate
     │
     ▼
Identify Cause
     │
     ▼
Fix Problem
     │
     ▼
Test Again
```

This cycle is repeated until the script behaves as expected.

---

# Types of Bugs

Most programming errors fall into three categories.

| Type | Description |
|------|-------------|
| Syntax Error | Invalid Lua syntax |
| Runtime Error | Error occurs while the script is running |
| Logical Error | Script runs but produces incorrect results |

Each type requires a different debugging approach.

---

# Syntax Errors

Syntax errors occur before the program begins executing.

Example:

```lua
if true then

    print("Hello")
```

Output:

```text
'end' expected
```

The interpreter immediately reports the missing keyword.

These errors are usually the easiest to fix.

---

# Runtime Errors

Runtime errors occur while the script is executing.

Example:

```lua
local host = nil

print(host.ip)
```

Output:

```text
attempt to index a nil value
```

The script starts correctly but fails when it encounters invalid data.

---

# Logical Errors

Logical errors are often the most difficult to detect.

Example:

```lua
local port = 80

if port == 443 then
    print("HTTP")
end
```

The script executes without errors but produces no output because the condition is incorrect.

No exception is generated, making logical bugs harder to identify.

---

# Using print()

The simplest debugging technique is printing values.

Example:

```lua
local port = 80

print(port)
```

Output:

```text
80
```

Printing intermediate values helps verify that variables contain the expected data.

---

# Tracing Program Flow

Printing messages also reveals which parts of the program are executing.

Example:

```lua
print("Step 1")

print("Connecting...")

print("Step 2")
```

Output:

```text
Step 1
Connecting...
Step 2
```

If execution stops unexpectedly, the last printed message indicates where the failure occurred.

---

# Inspecting Variables

During development, print important variables.

Example:

```lua
print(host.ip)

print(port.number)

print(port.service)
```

Confirming values early often reveals incorrect assumptions.

---

# Debugging Tables

Printing a table directly is usually not helpful.

```lua
print(host)
```

Output:

```text
table: 0x55ab34...
```

Instead, inspect its contents.

Example:

```lua
for key, value in pairs(host) do

    print(key, value)

end
```

This displays individual fields instead of the table's memory address.

---

# Using stdnse.debug()

NSE provides built-in debugging support through the `stdnse` library.

Import:

```lua
local stdnse = require("stdnse")
```

Example:

```lua
stdnse.debug(1, "Connecting to server...")
```

Unlike `print()`, debug messages are shown only when Nmap is running in debug mode.

This keeps normal output clean while still providing diagnostic information.

---

# Running Nmap in Debug Mode

Enable debugging with:

```bash
nmap -d
```

Increase verbosity:

```bash
nmap -d2
```

or:

```bash
nmap -d5
```

Higher levels display more internal information about script execution.

---

# Verbose Mode

Verbose mode provides additional script output.

Example:

```bash
nmap -v
```

Combine it with debugging:

```bash
nmap -v -d
```

This is a common combination during NSE development.

---

# Using Assertions

Assertions verify assumptions.

Example:

```lua
assert(port.number > 0, "Invalid port.")
```

If the assumption fails, Lua immediately reports the problem.

Assertions help detect bugs early.

---

# Using pcall()

Risky operations should be protected.

Example:

```lua
local success, result = pcall(function()

    return http.get(host, port, "/")

end)

if not success then

    print(result)

end
```

Instead of crashing, the script reports the error and continues running.

---

# Debugging Network Operations

Network communication often fails for reasons outside your control.

Typical debugging workflow:

```text
Connect
   │
   ▼
Success?
 ┌──┴────┐
 │       │
Yes     No
 │       │
 ▼       ▼
Continue Print Error
```

Always verify that network requests succeed before processing responses.

---

# Reading Error Messages

Error messages often contain valuable information.

Example:

```text
attempt to call a nil value
```

Possible causes:

- Misspelled function name
- Missing library
- Incorrect variable assignment

Carefully reading the error message frequently reveals the solution.

---

# Debugging Rule Functions

Sometimes the script never reaches `action()`.

Check whether the rule function executes.

Example:

```lua
portrule = function(host, port)

    print("Rule evaluated.")

    return true

end
```

If nothing is printed, the rule itself may never be evaluated.

---

# Debugging action()

Confirm that `action()` is called.

```lua
action = function(host, port)

    print("Inside action().")

    return "Done."

end
```

If this message never appears, revisit the rule function.

---

# Incremental Development

Avoid writing an entire script before testing it.

Instead:

```text
Write Small Feature
        │
        ▼
Test
        │
        ▼
Works?
 ┌──────┴──────┐
 │             │
Yes           No
 │             │
 ▼             ▼
Next Step   Fix Bug
```

Small incremental changes make debugging much easier.

---

# Logging Important Events

Helpful debugging messages describe significant events.

Examples:

```text
Connecting...

Authentication successful.

Received HTTP response.

Parsing HTML.

Completed.
```

Meaningful messages are more useful than printing random variables.

---

# Common Debugging Workflow

Professional developers often follow this sequence:

```text
Reproduce Problem
        │
        ▼
Read Error Message
        │
        ▼
Inspect Variables
        │
        ▼
Verify Assumptions
        │
        ▼
Fix Bug
        │
        ▼
Retest
```

Skipping steps usually leads to wasted time.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Guessing instead of testing | Makes debugging slower |
| Ignoring error messages | Valuable information is lost |
| Printing too little | Difficult to locate bugs |
| Printing everything | Output becomes overwhelming |
| Testing only once | Bugs may reappear |

Effective debugging relies on observation rather than guesswork.

---

# Best Practices

When debugging Lua and NSE scripts:

- Read error messages carefully.
- Test small changes frequently.
- Use `stdnse.debug()` instead of `print()` for diagnostic output.
- Validate assumptions with `assert()`.
- Protect risky operations with `pcall()`.
- Check return values before using them.
- Remove unnecessary debugging messages before releasing a script.

A disciplined debugging process saves significant development time.

---

# Debugging Checklist

Before assuming an NSE script is broken, verify the following:

- Is the script loaded correctly?
- Is the rule function returning `true`?
- Is `action()` being executed?
- Are all required libraries imported?
- Are script arguments valid?
- Are network requests succeeding?
- Are return values checked?
- Does the output match expectations?

Systematically checking these questions resolves many common issues.

---

## Chapter Summary

Debugging is an essential part of software development and a critical skill for every NSE developer. By understanding different types of errors, using diagnostic tools such as `stdnse.debug()`, validating assumptions, and testing incrementally, you can identify problems quickly and build more reliable scripts.

Professional developers treat debugging as a structured process rather than trial and error. With these techniques, you are now prepared to diagnose issues in your own NSE scripts and confidently troubleshoot complex network interactions.

---

# Next Chapter

## Chapter 37 — Writing Your First NSE Script