# Chapter 43 — Using NSE Libraries

In the previous chapters, we explored the **host** and **port** objects. These objects provide valuable information collected by Nmap, but they do not actively communicate with remote services.

Professional NSE scripts go much further.

Instead of only reading scan results, they establish network connections, send requests, receive responses, parse protocols, and analyze remote systems. Rather than implementing these capabilities from scratch, NSE provides a rich collection of **libraries**.

Libraries are one of the greatest strengths of the Nmap Scripting Engine. They allow developers to build powerful scripts with relatively little code while maintaining consistency, reliability, and performance.

In this lab, you will learn how to import and use NSE libraries to perform real network operations.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Understand the purpose of NSE libraries.
- Import libraries using `require()`.
- Use built-in NSE modules.
- Perform simple HTTP requests.
- Understand library documentation.
- Reuse library functions.
- Build cleaner and more maintainable scripts.

---

# What Is an NSE Library?

An NSE library is a reusable Lua module that provides functionality shared across many scripts.

Instead of writing complex code yourself, you simply call the appropriate function.

Conceptually:

```text
Your Script

      │

      ▼

NSE Library

      │

      ▼

Network Operation

      │

      ▼

Result
```

Libraries reduce duplicated code and simplify development.

---

# Why Libraries Exist

Imagine implementing an HTTP client manually.

You would need to:

- Create sockets
- Send requests
- Receive packets
- Parse HTTP headers
- Handle redirects
- Process responses
- Manage errors

This could require hundreds of lines of code.

Instead:

```lua
http.get(...)
```

accomplishes the same task with a single function call.

---

# Importing a Library

Libraries are imported using `require()`.

Example:

```lua
local http = require("http")
```

Now every function inside the HTTP library becomes available.

---

# Common NSE Libraries

Some of the most frequently used libraries include:

| Library | Purpose |
|----------|----------|
| `http` | HTTP communication |
| `shortport` | Rule helpers |
| `stdnse` | Utility functions |
| `ftp` | FTP communication |
| `dns` | DNS queries |
| `smtp` | SMTP communication |
| `sslcert` | SSL certificate parsing |
| `json` | JSON processing |
| `string` | String manipulation |
| `table` | Table utilities |

These libraries are used throughout the official NSE collection.

---

# Creating a Script

Create:

```text
http-test.nse
```

---

# Import the HTTP Library

```lua
local http = require("http")
```

This gives the script access to HTTP functions.

---

# Define the Rule

```lua
local shortport = require("shortport")

portrule = shortport.http
```

The script now executes only against HTTP services.

---

# Making Your First HTTP Request

Example:

```lua
action = function(host, port)

    local response =
        http.get(host, port, "/")

    if response then

        return response.status

    end

    return "No response."

end
```

Workflow:

```text
Host

      │

      ▼

HTTP Library

      │

      ▼

GET /

      │

      ▼

HTTP Response

      │

      ▼

Return Status
```

---

# Running the Script

Example:

```bash
nmap \
-p80 \
--script ./scripts/http-test.nse \
scanme.nmap.org
```

Possible output:

```text
HTTP Status: 200
```

The exact status depends on the server.

---

# Reading the Response

The returned object contains multiple fields.

Conceptually:

```text
Response

│

├── Status

├── Header

├── Body

├── Cookies

└── Metadata
```

The HTTP library organizes server responses into structured data.

---

# Displaying the Status Code

Example:

```lua
return

"Status: "

..

response.status
```

Possible output:

```text
Status: 200
```

---

# Displaying the Response Body

Example:

```lua
return response.body
```

The body usually contains HTML.

Example:

```html
<html>

<head>

<title>Example</title>

</head>

...
```

Be careful—response bodies can be very large.

---

# Displaying Headers

Headers are stored inside a table.

Example:

```lua
for key, value in pairs(response.header) do

    print(key, value)

end
```

Possible output:

```text
Server

Apache

Content-Type

text/html

Content-Length

512
```

---

# Handling Failures

Servers may not respond.

Always check:

```lua
if not response then

    return "Connection failed."

end
```

Never assume network communication always succeeds.

---

# Using stdnse

Import:

```lua
local stdnse =
require("stdnse")
```

Example:

```lua
stdnse.debug(
1,
"Sending HTTP request."
)
```

Run:

```bash
nmap -d
```

The debug message appears only in debug mode.

---

# Using shortport

Instead of writing:

```lua
return port.number == 80
```

Use:

```lua
portrule = shortport.http
```

Advantages:

- Cleaner
- More readable
- Reusable
- Supports multiple HTTP ports

---

# Combining Libraries

Scripts frequently import multiple libraries.

Example:

```lua
local http =
require("http")

local stdnse =
require("stdnse")

local shortport =
require("shortport")
```

Each library contributes a different capability.

---

# Practical Example

```lua
local http =
require("http")

local shortport =
require("shortport")

portrule =
shortport.http

action = function(host, port)

    local response =
    http.get(host, port, "/")

    if not response then

        return "No response."

    end

    return

        "Status: "

        ..

        response.status

end
```

This script performs a complete HTTP request using only a few lines of code.

---

# Understanding Library Documentation

Every library provides documentation describing:

- Available functions
- Parameters
- Return values
- Usage examples
- Limitations

Before using a new library, always review its documentation.

---

# Reusing Libraries

Libraries are designed for reuse.

```text
Script A

      │

      ▼

HTTP Library

      ▲

      │

Script B

      │

      ▼

HTTP Library

      ▲

      │

Script C
```

One library may support hundreds of different scripts.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Forgetting `require()` | Library functions are unavailable |
| Ignoring failed requests | Causes runtime errors |
| Printing the entire response body | Output becomes unreadable |
| Reimplementing existing functions | Wastes time |
| Not reading documentation | Incorrect library usage |

---

# Best Practices

When using NSE libraries:

- Import only the libraries you need.
- Reuse existing functionality.
- Always validate returned values.
- Read library documentation.
- Avoid duplicating library features.
- Keep network operations inside helper functions when possible.
- Use `shortport` instead of manual rules whenever appropriate.

---

# Lab Challenge

Complete the following tasks:

1. Create `http-test.nse`.
2. Import the HTTP library.
3. Import `shortport`.
4. Import `stdnse`.
5. Execute an HTTP GET request.
6. Display the HTTP status code.
7. Display the server header.
8. Handle connection failures.
9. Add debug messages.
10. Test the script against at least three different web servers.

---

# What You Learned

After completing this lab, you should understand:

- Why NSE libraries exist.
- How to import libraries using `require()`.
- How to perform HTTP requests.
- How to use `shortport`.
- How to use `stdnse`.
- How to safely handle library return values.

These concepts will be expanded throughout the remaining labs as we build increasingly sophisticated NSE scripts.

---

## Chapter Summary

NSE libraries provide reusable building blocks that dramatically simplify script development. By importing modules such as `http`, `shortport`, and `stdnse`, developers can focus on solving security problems instead of implementing low-level networking code.

Learning to use libraries effectively is one of the defining skills of an NSE developer. In the next chapter, you will move beyond helper functions and begin working directly with **TCP communication**, learning how NSE scripts establish socket connections, exchange data with remote services, and process network responses.

---

# Next Chapter

## Chapter 44 — HTTP Scripts