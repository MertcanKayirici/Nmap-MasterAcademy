# Chapter 49 — Error Handling Lab

No network is perfect.

Servers crash, packets are dropped, firewalls block traffic, services become unavailable, and users provide incorrect input. Even a well-written NSE script can fail if it assumes everything will always work.

Professional NSE developers write scripts that **expect failures** and recover from them gracefully.

A script that crashes during a large network scan wastes time and may prevent valuable information from being collected. Instead, scripts should detect problems, report meaningful errors, and continue whenever possible.

In this chapter, you will learn how to build reliable NSE scripts by applying proper error handling techniques.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Understand common NSE errors.
- Detect failed operations.
- Handle socket errors.
- Validate user input.
- Prevent runtime crashes.
- Produce meaningful error messages.
- Build more reliable NSE scripts.

---

# Why Error Handling Matters

Imagine scanning 500 servers.

```text
500 Hosts

     │

     ▼

One Server Fails

     │

     ▼

Entire Script Crashes
```

Poor error handling can stop an entire scan.

A better workflow is:

```text
500 Hosts

     │

     ▼

One Server Fails

     │

     ▼

Report Error

     │

     ▼

Continue Scanning
```

---

# Common Sources of Errors

Errors can occur because of:

- Connection timeouts
- Closed ports
- Firewall filtering
- Invalid script arguments
- Missing data
- Unexpected protocol responses
- DNS failures
- Network interruptions

Professional scripts assume these situations are normal.

---

# Checking Return Values

Many NSE functions return a status value.

Example:

```lua
local status, result =
socket:connect(host, port)
```

Always verify the status.

```lua
if not status then

    return result

end
```

Ignoring return values often leads to runtime errors.

---

# Handling Connection Failures

Example:

```lua
local status, err =
socket:connect(host, port)

if not status then

    return

    "Connection failed: "

    ..

    err

end
```

Possible output:

```text
Connection failed: Connection refused
```

---

# Handling Timeouts

Timeouts are common during network scans.

Example:

```lua
socket:set_timeout(5000)
```

If no response arrives:

```lua
if not status then

    return

    "Operation timed out."

end
```

Timeouts should never cause the script to crash.

---

# Handling Missing Data

Suppose an HTTP server omits the `Server` header.

Unsafe:

```lua
return
response.header.server
```

If the field does not exist, the script may fail.

Safe:

```lua
return

response.header.server

or

"Unknown"
```

Always expect optional fields to be missing.

---

# Validating Script Arguments

Never trust user input.

Example:

```lua
local timeout =

tonumber(

stdnse.get_script_args(
"timeout"
)

)
```

Validation:

```lua
if not timeout then

    timeout = 5

end
```

Invalid input should fall back to safe defaults.

---

# Handling Nil Values

Lua's `nil` represents the absence of a value.

Unsafe:

```lua
print(response.body)
```

Safe:

```lua
if response.body then

    print(response.body)

end
```

Always check values before using them.

---

# Socket Error Example

```lua
local socket =
nmap.new_socket()

local status, err =
socket:connect(host, port)

if not status then

    socket:close()

    return err

end
```

Even failed sockets should be closed properly.

---

# Safe Workflow

Professional scripts usually follow this pattern.

```text
Create Socket

↓

Set Timeout

↓

Connect

↓

Success?

↓

Yes

↓

Receive Data

↓

Parse

↓

Return Result

↓

Close Socket
```

If any step fails:

```text
Failure

↓

Return Error

↓

Close Socket
```

---

# Protecting Against Unexpected Responses

Suppose an FTP server sends:

```text
ERROR
```

instead of

```text
220 FTP Ready
```

Instead of assuming success:

```lua
if response then

    return response

end

return

"Unexpected response."
```

Unexpected responses should be handled explicitly.

---

# Returning Useful Errors

Avoid:

```text
nil
```

Better:

```text
Connection refused.
```

or

```text
HTTP request timed out.
```

or

```text
DNS query failed.
```

Meaningful errors help users solve problems quickly.

---

# Using Debug Messages

Example:

```lua
stdnse.debug(
1,
"Attempting TCP connection."
)
```

If a connection fails:

```lua
stdnse.debug(
1,
"Connection failed."
)
```

Debug messages should support troubleshooting without affecting normal output.

---

# Complete Example

```lua
local nmap =
require("nmap")

action = function(host, port)

    local socket =
        nmap.new_socket()

    socket:set_timeout(5000)

    local status, err =
        socket:connect(host, port)

    if not status then

        socket:close()

        return

        "Connection failed: "

        ..

        err

    end

    local ok, banner =
        socket:receive()

    socket:close()

    if not ok then

        return

        "Failed to read banner."

    end

    return banner

end
```

This script safely handles failures at every stage.

---

# Error Handling Flow

```text
Start

↓

Connect

↓

Success?

├── Yes

│     ↓

│  Receive Data

│     ↓

│  Parse

│     ↓

│  Return Result

│

└── No

      ↓

Return Error

      ↓

Close Socket
```

---

# Logging vs Reporting

Not every error should be shown to the user.

Examples:

Debug output:

```text
Connecting...

Reading banner...

Parsing response...
```

User output:

```text
FTP Banner

220 FileZilla Server
```

Keep internal diagnostics separate from user-facing results.

---

# Graceful Recovery

A good script continues whenever possible.

Instead of:

```text
Fatal Error

↓

Stop
```

prefer:

```text
Error

↓

Skip Host

↓

Continue Scan
```

This approach is essential for large-scale scanning.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Ignoring return values | Causes unexpected failures |
| Assuming values are never nil | Leads to runtime errors |
| Forgetting to close sockets | Resource leaks |
| Printing cryptic error messages | Difficult to troubleshoot |
| Using hardcoded assumptions | Reduces script reliability |

---

# Best Practices

When handling errors:

- Check every network operation.
- Validate all user input.
- Use sensible default values.
- Close sockets in every execution path.
- Return meaningful error messages.
- Separate debug logs from final output.
- Expect network failures as normal events.

These habits produce scripts that remain reliable in real-world environments.

---

# Lab Challenge

Complete the following tasks:

1. Create `safe-banner.nse`.
2. Set a socket timeout.
3. Handle connection failures.
4. Handle timeout errors.
5. Handle missing responses.
6. Validate script arguments.
7. Close sockets correctly.
8. Add debug messages.
9. Test the script against an unavailable service.
10. Compare the behavior with and without error handling.

---

# What You Learned

After completing this lab, you should understand:

- Why error handling is essential.
- How to detect failed operations.
- How to recover from network errors.
- How to validate user input.
- How to prevent runtime crashes.
- How to build resilient NSE scripts.

These skills are critical for writing scripts that perform reliably during large-scale security assessments.

---

## Chapter Summary

Reliable NSE scripts are built with the expectation that failures will occur. By validating inputs, checking return values, handling timeouts, closing sockets properly, and returning meaningful error messages, you can create scripts that continue operating even in unpredictable network environments.

With robust error handling in place, the next chapter focuses on **debugging NSE scripts**, where you will learn how to diagnose problems, trace script execution, inspect variables, and efficiently troubleshoot complex scripts during development.

---

# Next Chapter

## Chapter 50 — Debugging Lab