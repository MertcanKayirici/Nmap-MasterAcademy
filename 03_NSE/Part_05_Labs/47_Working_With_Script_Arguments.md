# Chapter 47 — Working With Script Arguments

Until now, every script we have written has behaved the same way each time it was executed. While this is sufficient for simple demonstrations, real-world security assessments require flexibility.

Imagine a script that checks HTTP authentication.

Instead of hardcoding:

- Username
- Password
- URL
- Timeout
- Request method

we should allow the user to provide these values when the script is executed.

This is the purpose of **script arguments**.

Script arguments make NSE scripts configurable without modifying the source code, allowing a single script to operate in many different environments.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Pass arguments to NSE scripts.
- Retrieve argument values.
- Use default values.
- Validate user input.
- Convert argument types.
- Build configurable scripts.
- Apply best practices for argument handling.

---

# Why Script Arguments Matter

Consider two approaches.

Without script arguments:

```lua
local username = "admin"

local password = "admin123"
```

Changing the credentials requires editing the script every time.

With script arguments:

```bash
--script-args \
username=alice,\
password=Secret123
```

The same script can be reused for different systems.

---

# How Script Arguments Work

```text
User

      │

      ▼

--script-args

      │

      ▼

Nmap

      │

      ▼

NSE Script

      │

      ▼

Read Arguments

      │

      ▼

Execute Logic
```

Arguments are supplied by the user and retrieved inside the script.

---

# Importing stdnse

Arguments are accessed through the `stdnse` library.

```lua
local stdnse =
require("stdnse")
```

---

# Reading an Argument

Example:

```lua
local username =
stdnse.get_script_args("username")
```

If the command is:

```bash
nmap \
--script example \
--script-args username=alice
```

Then:

```text
username

↓

alice
```

---

# Creating a Simple Script

```lua
local stdnse =
require("stdnse")

action = function()

    local name =
        stdnse.get_script_args("name")

    return

        "Hello " ..

        name

end
```

Run:

```bash
nmap \
--script hello \
--script-args name=Alice
```

Output:

```text
Hello Alice
```

---

# Using Default Values

Sometimes users forget to provide arguments.

Instead of failing:

```lua
local username =
stdnse.get_script_args("username")
or
"guest"
```

Execution:

```text
Argument Missing

↓

Use "guest"
```

Default values improve usability.

---

# Reading Multiple Arguments

Example:

```lua
local username =
stdnse.get_script_args("username")

local password =
stdnse.get_script_args("password")
```

Command:

```bash
--script-args \
username=admin,\
password=secret
```

Both values become available.

---

# Converting Numbers

Arguments are always received as strings.

Example:

```bash
--script-args timeout=10
```

Lua:

```lua
local timeout =
tonumber(

stdnse.get_script_args(
"timeout"

))

or

5
```

Always convert numeric values before calculations.

---

# Boolean Arguments

Example:

```bash
--script-args verbose=true
```

Lua:

```lua
local verbose =
stdnse.get_script_args("verbose")
```

Example usage:

```lua
if verbose then

    print("Verbose mode enabled.")

end
```

---

# Namespaced Arguments

Professional NSE scripts often use namespaces.

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
--script-args \
http.username=admin
```

Lua:

```lua
local username =

stdnse.get_script_args(
"http.username"
)
```

Namespaces prevent naming conflicts.

---

# Validating Input

Never assume the user provides valid data.

Example:

```lua
local timeout =
tonumber(

stdnse.get_script_args(
"timeout"
)

)

if not timeout then

    return
    "Invalid timeout."

end
```

Validation prevents unexpected errors.

---

# Complete Example

```lua
local stdnse =
require("stdnse")

action = function()

    local username =

    stdnse.get_script_args(
    "username"
    )

    or

    "guest"

    local timeout =

    tonumber(

    stdnse.get_script_args(
    "timeout"
    )

    )

    or

    5

    return

    "User: "

    ..

    username

    ..

    "\nTimeout: "

    ..

    timeout

end
```

Example output:

```text
User: admin

Timeout: 5
```

---

# Using Arguments in HTTP Scripts

Suppose we want to request different URLs.

Instead of:

```lua
http.get(host, port, "/")
```

we can write:

```lua
local path =

stdnse.get_script_args(
"http.path"
)

or

"/"
```

Now the user chooses the page.

Example:

```bash
--script-args \
http.path=/admin
```

---

# Passing Credentials

Example:

```bash
--script-args \
http.username=admin,\
http.password=secret
```

Workflow:

```text
Command Line

↓

Arguments

↓

Script

↓

Authentication
```

This approach is widely used by official NSE scripts.

---

# Debugging Arguments

Useful during development:

```lua
local stdnse =
require("stdnse")

stdnse.debug(

1,

"Username: "

..

(
stdnse.get_script_args(
"username"
)

or

"none"

)

)
```

Run:

```bash
nmap -d
```

---

# Security Considerations

Script arguments may contain sensitive data.

Examples:

- Passwords
- Tokens
- API keys
- Session cookies

Avoid:

```text
Printing passwords

Saving credentials

Logging secrets
```

Always protect confidential information.

---

# Common Argument Types

| Type | Example |
|------|----------|
| Username | admin |
| Password | secret |
| URL Path | /login |
| Timeout | 5 |
| Hostname | example.com |
| Port | 443 |
| Boolean | true |
| Integer | 100 |

---

# Practical Example

Imagine scanning multiple web applications.

Instead of modifying the script:

```lua
"/admin"
```

the user executes:

```bash
--script-args \
http.path=/administrator
```

The script immediately adapts.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Forgetting `stdnse.get_script_args()` | Arguments cannot be accessed |
| Assuming arguments always exist | May produce `nil` values |
| Forgetting `tonumber()` | Numeric calculations fail |
| Hardcoding configuration | Reduces flexibility |
| Printing sensitive arguments | Security risk |

---

# Best Practices

When using script arguments:

- Provide sensible defaults.
- Validate every argument.
- Convert numeric values.
- Use descriptive names.
- Prefer namespaced arguments.
- Avoid exposing secrets.
- Document all supported arguments.
- Keep configuration separate from business logic.

---

# Lab Challenge

Complete the following tasks:

1. Create `arguments-demo.nse`.
2. Read a username argument.
3. Read a password argument.
4. Read a timeout value.
5. Convert the timeout to a number.
6. Provide default values.
7. Validate user input.
8. Add debug messages.
9. Test the script with different arguments.
10. Modify an HTTP request using `http.path`.

---

# What You Learned

After completing this lab, you should understand:

- How script arguments work.
- How to retrieve arguments.
- How to validate input.
- How to use default values.
- How to convert argument types.
- Why configurable scripts are preferable to hardcoded values.

These techniques make NSE scripts more reusable and adaptable to different environments.

---

## Chapter Summary

Script arguments transform static NSE scripts into flexible tools that can be customized at runtime. By retrieving user-supplied values through the `stdnse` library, validating them carefully, and providing sensible defaults, developers can create scripts that adapt to different hosts, services, and testing scenarios without requiring source code modifications.

With configurable scripts now covered, the next lab focuses on **output formatting**, where you will learn how to present information clearly, organize complex results, and produce professional-quality output similar to that of the official Nmap script collection.

---

# Next Chapter

## Chapter 48 — Output Formatting