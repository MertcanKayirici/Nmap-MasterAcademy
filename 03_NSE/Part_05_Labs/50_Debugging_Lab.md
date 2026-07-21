# Chapter 50 — Debugging Lab

Even experienced developers write code that does not work correctly on the first attempt.

A script may fail to connect to a service, receive unexpected data, produce incorrect output, or stop with an error message. These situations are a normal part of software development.

The difference between a beginner and an experienced developer is not the number of mistakes they make—it is how efficiently they identify and fix those mistakes.

Debugging is the process of observing a program while it runs, understanding its behavior, and locating the source of problems.

In this chapter, you will learn practical debugging techniques for developing reliable NSE scripts.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Understand the debugging process.
- Enable Nmap debug mode.
- Use `stdnse.debug()`.
- Trace script execution.
- Inspect variables.
- Debug socket communication.
- Troubleshoot common NSE errors.

---

# What Is Debugging?

Debugging is the process of finding and correcting errors in a program.

Typical workflow:

```text
Write Script

      │

      ▼

Run Script

      │

      ▼

Observe Problem

      │

      ▼

Collect Information

      │

      ▼

Find Cause

      │

      ▼

Fix Problem

      │

      ▼

Test Again
```

Debugging is an iterative process.

---

# Types of Errors

NSE developers commonly encounter three categories of errors.

| Type | Example |
|------|----------|
| Syntax Error | Missing keyword or symbol |
| Runtime Error | Nil value or failed connection |
| Logic Error | Script runs but produces incorrect results |

Each type requires a different troubleshooting approach.

---

# Running Nmap in Debug Mode

Nmap provides built-in debugging support.

```bash
nmap -d scanme.nmap.org
```

Higher debug levels produce more detailed information.

```bash
nmap -d2

nmap -d3

nmap -d9
```

Higher levels generate significantly more output.

---

# Using stdnse.debug()

Import the library.

```lua
local stdnse =
require("stdnse")
```

Print a debug message.

```lua
stdnse.debug(
1,
"Starting script."
)
```

Normal execution:

```text
No debug message
```

Debug mode:

```text
Starting script.
```

---

# Tracing Execution

Debug messages help identify where execution stops.

Example:

```lua
stdnse.debug(
1,
"Opening socket."
)

stdnse.debug(
1,
"Connecting."
)

stdnse.debug(
1,
"Receiving banner."
)

stdnse.debug(
1,
"Closing socket."
)
```

Output clearly shows how far the script progressed.

---

# Debugging Variables

Inspect variable values.

```lua
stdnse.debug(
1,

"Port: " ..

port.number
)
```

Possible output:

```text
Port: 21
```

This confirms that the expected value was received.

---

# Debugging Script Arguments

Example:

```lua
local username =

stdnse.get_script_args(
"username"
)

stdnse.debug(
1,

"Username: " ..

(
username or "nil"
)
)
```

This helps verify that script arguments were passed correctly.

---

# Debugging Socket Connections

Example:

```lua
stdnse.debug(
1,
"Connecting to server..."
)

local status, err =
socket:connect(host, port)

if not status then

    stdnse.debug(
    1,

    err
    )

end
```

Possible output:

```text
Connecting to server...

Connection refused
```

---

# Debugging Responses

Instead of immediately parsing data:

```lua
local status, response =
socket:receive()
```

Inspect it first.

```lua
stdnse.debug(
1,

response or "No response."
)
```

This often reveals unexpected server behavior.

---

# Debugging HTTP Requests

Example:

```lua
local response =
http.get(host, port, "/")

stdnse.debug(
1,

response.status
)
```

Possible output:

```text
200
```

If the request fails:

```text
nil
```

The problem becomes immediately visible.

---

# Using Multiple Debug Levels

Different messages can use different levels.

```lua
stdnse.debug(
1,
"Connecting."
)

stdnse.debug(
2,
"Sending packet."
)

stdnse.debug(
3,
"Received raw response."
)
```

When running:

```bash
nmap -d2
```

Only messages up to level 2 are displayed.

---

# Debugging Workflow

```text
Run Script

↓

Unexpected Result

↓

Enable Debug

↓

Collect Information

↓

Identify Problem

↓

Modify Code

↓

Run Again
```

Repeat until the problem is solved.

---

# Reading Error Messages

Suppose the console displays:

```text
attempt to index a nil value
```

Interpretation:

```text
Variable

↓

Nil

↓

Accessed

↓

Runtime Error
```

The solution is to check whether the variable exists before using it.

---

# Common Runtime Problems

Examples include:

```text
Connection refused

Timeout

Host unreachable

Nil value

Invalid argument

Unexpected response
```

Debugging helps distinguish between programming errors and network conditions.

---

# Complete Example

```lua
local stdnse =
require("stdnse")

local nmap =
require("nmap")

action = function(host, port)

    stdnse.debug(
    1,

    "Creating socket."
    )

    local socket =
        nmap.new_socket()

    socket:set_timeout(5000)

    stdnse.debug(
    1,

    "Connecting..."
    )

    local status, err =
        socket:connect(host, port)

    if not status then

        stdnse.debug(
        1,

        err
        )

        socket:close()

        return err

    end

    stdnse.debug(
    1,

    "Receiving banner."
    )

    local ok, banner =
        socket:receive()

    socket:close()

    if not ok then

        return "No banner."

    end

    stdnse.debug(
    2,

    banner
    )

    return banner

end
```

---

# Example Debug Output

```text
Creating socket.

Connecting...

Receiving banner.

220 ProFTPD 1.3.6
```

The execution flow is clearly visible.

---

# Common Debugging Mistakes

| Mistake | Explanation |
|----------|-------------|
| Printing too much information | Makes debugging difficult |
| Leaving debug messages in production output | Unprofessional |
| Ignoring error messages | Delays problem resolution |
| Assuming the network is always at fault | The script may contain bugs |
| Debugging without a plan | Leads to confusion |

---

# Best Practices

When debugging NSE scripts:

- Enable debug mode only when needed.
- Add debug messages at important execution points.
- Inspect variables before processing them.
- Test one change at a time.
- Remove unnecessary debug messages before releasing a script.
- Read error messages carefully.
- Reproduce issues consistently before attempting fixes.

---

# Lab Challenge

Complete the following tasks:

1. Create `debug-demo.nse`.
2. Add debug messages before every major operation.
3. Print the current port number.
4. Print received banners.
5. Debug an HTTP request.
6. Pass script arguments and verify them.
7. Trigger a timeout intentionally.
8. Observe Nmap's debug output.
9. Remove unnecessary debug statements.
10. Compare execution with and without debug mode.

---

# What You Learned

After completing this lab, you should understand:

- How debugging works in NSE.
- How to enable Nmap debug mode.
- How to use `stdnse.debug()`.
- How to inspect variables.
- How to troubleshoot socket communication.
- How to diagnose common runtime errors.

Debugging is an essential skill for developing reliable and maintainable NSE scripts.

---

## Chapter Summary

Debugging allows developers to understand what happens inside an NSE script while it executes. By using Nmap's debug mode, strategically placing `stdnse.debug()` statements, inspecting variables, and interpreting error messages, you can quickly identify and resolve issues that would otherwise be difficult to diagnose.

With debugging techniques now mastered, you are ready to begin building practical security tools. In the next chapter, you will develop your first complete utility: a **TCP Banner Grabber**, combining sockets, error handling, debugging, and output formatting into a real-world NSE script.

---

# Next Chapter

## Chapter 51 — Building a Banner Grabber