# Chapter 35 — Arguments

Most programs become significantly more useful when users can customize their behavior without modifying the source code.

NSE scripts achieve this through **script arguments**.

Script arguments allow users to pass parameters directly from the Nmap command line. Instead of writing separate scripts for different usernames, passwords, URLs, ports, or timeouts, a single script can adapt its behavior based on the arguments it receives.

Nearly every advanced NSE script supports one or more script arguments.

---

# What Are Script Arguments?

A script argument is a user-defined value passed to an NSE script when Nmap executes it.

Conceptually:

```text
User
 │
 ▼
Nmap Command
 │
 ▼
Script Arguments
 │
 ▼
NSE Script
 │
 ▼
Customized Behavior
```

Instead of hardcoding values inside the script, users provide them dynamically.

---

# Why Script Arguments Matter

Without arguments:

```lua
local username = "admin"
```

Changing the username requires editing the script.

With arguments:

```text
Username supplied by user
```

The same script can be reused in many different environments.

Advantages include:

- Flexibility
- Reusability
- Better automation
- Easier testing
- Cleaner code

---

# Passing Arguments from Nmap

Arguments are supplied using the `--script-args` option.

Example:

```bash
nmap --script myscript --script-args username=admin 192.168.1.10
```

Multiple arguments:

```bash
nmap \
--script myscript \
--script-args username=admin,password=secret,timeout=5 \
192.168.1.10
```

Each argument becomes available to the script during execution.

---

# Accessing Arguments

NSE scripts access arguments through the `stdnse` library.

Import:

```lua
local stdnse = require("stdnse")
```

Retrieve an argument:

```lua
local username = stdnse.get_script_args("username")
```

If the user executes:

```bash
nmap --script myscript --script-args username=admin
```

then:

```lua
username
```

contains:

```text
admin
```

---

# Simple Example

Command:

```bash
nmap \
--script hello \
--script-args name=Alice
```

Script:

```lua
local stdnse = require("stdnse")

action = function()

    local name = stdnse.get_script_args("name")

    return "Hello " .. name

end
```

Output:

```text
Hello Alice
```

---

# Default Values

Users may forget to provide an argument.

Instead of failing, provide a default value.

Example:

```lua
local username =
    stdnse.get_script_args("username")
    or "guest"
```

If no argument exists:

```text
guest
```

is used automatically.

This makes scripts more user-friendly.

---

# Boolean Arguments

Arguments may act as switches.

Command:

```bash
nmap \
--script myscript \
--script-args verbose=true
```

Lua:

```lua
local verbose =
    stdnse.get_script_args("verbose")
```

Example:

```lua
if verbose then

    print("Verbose mode enabled.")

end
```

---

# Numeric Arguments

Arguments are received as strings.

Example:

```bash
--script-args timeout=10
```

Lua:

```lua
local timeout =
    tonumber(stdnse.get_script_args("timeout"))
```

Always convert numeric values before performing calculations.

---

# Multiple Arguments

Several arguments may be used together.

Command:

```bash
--script-args username=admin,password=secret
```

Lua:

```lua
local username =
    stdnse.get_script_args("username")

local password =
    stdnse.get_script_args("password")
```

Each argument is retrieved independently.

---

# Namespaced Arguments

Official NSE scripts usually use namespaced argument names.

Instead of:

```text
username
```

they prefer:

```text
http.username
```

or

```text
ftp.username
```

Example:

```bash
--script-args http.username=admin
```

Retrieve:

```lua
local username =
    stdnse.get_script_args("http.username")
```

Namespaces prevent conflicts between different scripts.

---

# Example: HTTP Authentication

Command:

```bash
nmap \
--script http-auth \
--script-args \
http.username=admin,http.password=secret
```

Workflow:

```text
User
 │
 ▼
Arguments
 │
 ▼
Script
 │
 ▼
HTTP Login
```

The script authenticates using the supplied credentials.

---

# Example: Timeout

Command:

```bash
--script-args timeout=3
```

Lua:

```lua
local timeout =
    tonumber(stdnse.get_script_args("timeout"))
    or 5
```

If the argument is omitted:

```text
5
```

seconds becomes the default timeout.

---

# Validating Arguments

Never assume arguments are valid.

Example:

```lua
local timeout =
    tonumber(stdnse.get_script_args("timeout"))

if not timeout then

    return "Invalid timeout."

end
```

Validation prevents runtime errors.

---

# Common Argument Types

| Type | Example |
|------|----------|
| Username | admin |
| Password | secret |
| URL | /login |
| Timeout | 5 |
| Port | 8080 |
| File | users.txt |
| Boolean | true |
| Integer | 100 |
| Hostname | example.com |

Most professional scripts support several configurable parameters.

---

# How Official NSE Scripts Use Arguments

Typical execution flow:

```text
User
 │
 ▼
--script-args
 │
 ▼
stdnse.get_script_args()
 │
 ▼
Validate
 │
 ▼
Use Value
```

The argument influences the script's behavior without requiring code changes.

---

# Real-World Example

Imagine a script testing web authentication.

Without arguments:

```lua
username = "admin"
password = "admin"
```

Every execution uses the same credentials.

With arguments:

```bash
--script-args \
http.username=root,\
http.password=toor
```

The same script now works in different environments.

---

# Security Considerations

Arguments often contain sensitive information.

Examples include:

- Passwords
- API keys
- Tokens
- Session cookies
- Private URLs

Avoid:

- Printing secrets unnecessarily
- Logging credentials
- Returning sensitive values in output

Always treat user-supplied arguments carefully.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Forgetting `stdnse.get_script_args()` | Arguments never read |
| Assuming arguments always exist | Nil errors |
| Forgetting `tonumber()` | String used as number |
| Hardcoding values | Reduced flexibility |
| Not validating input | Unexpected failures |

Proper validation improves both stability and security.

---

# Best Practices

When working with script arguments:

- Provide sensible default values.
- Validate every argument.
- Convert data types when necessary.
- Use descriptive argument names.
- Prefer namespaced arguments.
- Avoid exposing sensitive information.
- Document all supported arguments.

Following these practices makes scripts easier to use and more reliable.

---

# Typical Professional Script

A professional script often begins like this:

```lua
local stdnse = require("stdnse")

local username =
    stdnse.get_script_args("http.username")
    or "guest"

local password =
    stdnse.get_script_args("http.password")

local timeout =
    tonumber(
        stdnse.get_script_args("http.timeout")
    ) or 5
```

All configuration is centralized before the script performs any network operations.

---

## Chapter Summary

Script arguments allow NSE scripts to be customized at runtime without modifying the source code. Using `stdnse.get_script_args()`, developers can retrieve user-supplied values, validate them, and adapt script behavior to different environments.

Well-designed arguments make scripts reusable, flexible, and automation-friendly. Professional NSE scripts rely heavily on arguments for credentials, timeouts, protocol options, and many other configuration settings.

With script customization complete, the next chapter focuses on **debugging**, where you will learn how to identify problems, inspect program execution, and troubleshoot NSE scripts effectively.

---

# Next Chapter

## Chapter 36 — Debugging