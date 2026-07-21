# Chapter 30 — Error Handling

No program is perfect. Network connections fail, files may not exist, users provide invalid input, and remote systems often behave unexpectedly.

For this reason, every robust program must be able to detect, report, and recover from errors gracefully.

Lua provides a simple yet powerful error handling mechanism based on the functions `error()`, `assert()`, `pcall()`, and `xpcall()`. These functions allow programs to continue running safely instead of terminating unexpectedly.

Since NSE scripts interact with remote systems across unreliable networks, understanding error handling is essential for writing stable and professional scripts.

---

## What Is an Error?

An error is an unexpected condition that prevents a program from continuing normally.

Examples include:

- Invalid function arguments
- Missing files
- Failed network connections
- Timeout events
- Division by zero (in some languages)
- Attempting to access nonexistent values

Example:

```lua
local value = nil

print(value.name)
```

Output:

```text
attempt to index a nil value
```

The program stops because it attempted to access a field of a `nil` value.

---

# Runtime Errors

Lua performs most error checking while the program is running.

Example:

```lua
local host = nil

print(host.ip)
```

Output:

```text
attempt to index a nil value
```

This type of problem is called a **runtime error**.

---

# The error() Function

The simplest way to generate an error is with `error()`.

Example:

```lua
error("Invalid port number.")
```

Output:

```text
lua: Invalid port number.
```

Execution immediately stops.

This function is useful when a program detects invalid conditions.

---

# Using error() in Functions

Example:

```lua
function connect(port)

    if port <= 0 then
        error("Port must be positive.")
    end

    print("Connecting...")

end
```

Calling:

```lua
connect(-1)
```

Output:

```text
Port must be positive.
```

The function immediately terminates when the invalid value is detected.

---

# The assert() Function

`assert()` validates conditions.

Syntax:

```lua
assert(condition, message)
```

If the condition is true:

```lua
assert(5 > 2)
```

Nothing happens.

If false:

```lua
assert(false, "Connection failed.")
```

Output:

```text
Connection failed.
```

---

## Practical Example

```lua
local port = 80

assert(port > 0, "Invalid port.")
```

If the assertion succeeds, execution continues normally.

---

# Protected Calls

Normally, an error stops the program.

Example:

```lua
error("Fatal Error")
```

Program:

```text
Stops Immediately
```

Protected calls allow programs to continue.

Lua provides:

```lua
pcall()
```

---

# pcall()

`pcall()` stands for **protected call**.

Syntax:

```lua
local success, result = pcall(functionName)
```

If no error occurs:

```lua
local function greet()

    print("Hello")

end

local ok = pcall(greet)

print(ok)
```

Output:

```text
Hello
true
```

---

## Handling Errors with pcall()

Example:

```lua
local function fail()

    error("Connection failed.")

end

local success, message = pcall(fail)

print(success)
print(message)
```

Output:

```text
false
Connection failed.
```

The program continues running instead of terminating.

---

# Why pcall() Matters

Without `pcall()`:

```text
Error
   │
   ▼
Program Stops
```

With `pcall()`:

```text
Error
   │
   ▼
pcall()
   │
   ▼
Return Error
   │
   ▼
Program Continues
```

This is especially useful when communicating with remote systems that may fail unpredictably.

---

# xpcall()

`xpcall()` works similarly to `pcall()` but allows a custom error handler.

Syntax:

```lua
xpcall(function, errorHandler)
```

Example:

```lua
local function handler(err)

    print("Handled:", err)

end

local function fail()

    error("Network timeout.")

end

xpcall(fail, handler)
```

Output:

```text
Handled: Network timeout.
```

---

# Error Propagation

Errors travel upward through the function call stack until they are handled.

Example:

```text
main()
 │
 ▼
connect()
 │
 ▼
authenticate()
 │
 ▼
error()
```

If no function catches the error, the program terminates.

---

# Practical NSE Example

Suppose an HTTP request fails.

```lua
local success, response = pcall(function()

    return http.get(host, port, "/")

end)

if success then

    print("Received response.")

else

    print("HTTP request failed.")

end
```

Instead of crashing, the script reports the problem and continues execution.

---

# Defensive Programming

Good Lua programs anticipate problems before they occur.

Example:

Instead of:

```lua
print(host.ip)
```

Prefer:

```lua
if host then
    print(host.ip)
end
```

Checking values before using them prevents many runtime errors.

---

# Error Messages

Helpful error messages should explain:

- What happened
- Why it happened
- How to fix it (if possible)

Poor:

```text
Error
```

Better:

```text
HTTP request timed out after 5 seconds.
```

Descriptive messages simplify debugging.

---

# Common Error Sources in NSE

Network scripting introduces many possible failures.

Common examples include:

| Error | Cause |
|---------|-------|
| Connection refused | Service unavailable |
| Timeout | Slow network |
| Host unreachable | Routing failure |
| Invalid response | Malformed protocol data |
| SSL failure | Certificate problems |
| Authentication failure | Incorrect credentials |

Professional NSE scripts should anticipate these situations.

---

# Error Recovery

A robust script should recover whenever possible.

Typical strategy:

```text
Operation
     │
     ▼
Success?
 ┌───┴────┐
 │        │
Yes      No
 │        │
 ▼        ▼
Continue Retry / Report
```

Some errors require immediate termination, while others allow retrying or skipping the current host.

---

# Common Beginner Mistakes

| Mistake | Example |
|----------|---------|
| Ignoring return values | Missing failures |
| Overusing `error()` | Program exits unnecessarily |
| Not using `pcall()` | Script crashes |
| Poor error messages | Difficult debugging |
| Assuming network operations always succeed | Unreliable behavior |

Most runtime issues can be avoided through careful validation and defensive programming.

---

# Best Practices

When handling errors:

- Validate inputs early.
- Use `assert()` for required conditions.
- Use `pcall()` around risky operations.
- Provide descriptive error messages.
- Anticipate network failures.
- Recover gracefully whenever possible.
- Log useful debugging information.

These habits produce stable and reliable Lua applications.

---

## Error Handling in Official NSE Scripts

Official NSE scripts frequently follow a defensive approach.

Typical workflow:

```text
Input
  │
  ▼
Validate Arguments
  │
  ▼
Network Operation
  │
  ▼
Did It Fail?
 ┌────┴────┐
 │         │
No        Yes
 │         │
 ▼         ▼
Continue  Report Error
```

Rather than terminating immediately, many scripts return informative messages or skip unreachable hosts.

---

## Chapter Summary

Errors are an unavoidable part of programming, especially when interacting with remote systems across unreliable networks.

Lua provides a straightforward yet effective error handling model through `error()`, `assert()`, `pcall()`, and `xpcall()`. By validating inputs, protecting risky operations, and reporting meaningful errors, developers can create scripts that remain stable even when unexpected problems occur.

Reliable error handling is a hallmark of professional NSE development and is essential for producing scripts that work consistently in real-world environments.

---

# Next Chapter

## Chapter 31 — NSE Libraries