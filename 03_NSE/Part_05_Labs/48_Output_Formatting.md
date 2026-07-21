# Chapter 48 — Output Formatting

Writing a script that gathers information is only half of the job.

The other half is presenting that information in a way that is easy to read, understand, and analyze.

Imagine running an NSE script against hundreds of hosts. If the output is poorly formatted, finding useful information becomes difficult—even if the script itself works perfectly.

Professional NSE scripts focus not only on collecting data but also on presenting it clearly.

In this chapter, you will learn how to produce clean, structured, and professional output similar to the official Nmap NSE scripts.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Produce readable script output.
- Return strings correctly.
- Return Lua tables.
- Format multiline output.
- Organize related information.
- Avoid excessive output.
- Follow official NSE output conventions.

---

# Why Output Formatting Matters

Poor output:

```text
Apache Linux HTTP 2.4.57 PHP 8.2 OpenSSL Enabled Cookie SessionID=yes Redirect=True
```

Good output:

```text
Server Information

---------------

Server      : Apache

Version     : 2.4.57

Operating System : Linux

PHP          : 8.2

SSL          : Enabled

Session Cookie : Yes

Redirects    : True
```

Both contain the same information.

Only one is easy to read.

---

# The Simplest Output

Every action function returns data.

Example:

```lua
action = function()

    return "Hello NSE"

end
```

Output:

```text
Hello NSE
```

---

# Returning Variables

Instead of returning fixed text:

```lua
local version = "2.4.57"

return version
```

Output:

```text
2.4.57
```

---

# Combining Strings

Example:

```lua
local server = "Apache"

local version = "2.4.57"

return

server ..

" " ..

version
```

Output:

```text
Apache 2.4.57
```

---

# Using New Lines

Readable output usually spans multiple lines.

Example:

```lua
return

"Server: Apache\n" ..

"Version: 2.4.57"
```

Output:

```text
Server: Apache

Version: 2.4.57
```

---

# Returning Lua Tables

NSE can format tables automatically.

Example:

```lua
return {

Server = "Apache",

Version = "2.4.57",

SSL = "Enabled"

}
```

Conceptually:

```text
Lua Table

↓

Nmap Formatter

↓

Readable Output
```

Returning structured data is often preferable to manually formatting long strings.

---

# Nested Tables

More complex information can also be grouped.

Example:

```lua
return {

HTTP = {

Version = "HTTP/1.1",

Status = 200

},

Server = "Apache"

}
```

Nested tables help organize related information.

---

# Formatting Lists

Example:

```lua
return {

"HTTP",

"HTTPS",

"SSH",

"FTP"

}
```

Possible output:

```text
HTTP

HTTPS

SSH

FTP
```

Lists are useful for discovered services or supported protocols.

---

# Indentation

Good indentation improves readability.

Poor:

```text
Server

Apache

Version

2.4.57
```

Better:

```text
Server : Apache

Version: 2.4.57
```

Alignment makes reports easier to scan.

---

# Example HTTP Report

```text
HTTP Information

----------------

Status Code : 200

Server      : nginx

Content-Type: text/html

Length      : 1240
```

This style resembles many official NSE scripts.

---

# Avoid Excessive Output

Instead of:

```lua
return response.body
```

use:

```lua
return

response.body:sub(1,150)
```

Displaying only a preview keeps reports concise.

---

# Reporting Errors

Instead of:

```text
nil
```

Return meaningful messages.

```lua
return

"Connection failed."
```

Better examples:

```text
HTTP request timed out.

Authentication failed.

Server did not respond.

DNS query failed.
```

Helpful messages simplify troubleshooting.

---

# Building Output Step by Step

Example:

```lua
local result = ""

result = result ..

"Server: Apache\n"

result = result ..

"Version: 2.4.57\n"

result = result ..

"Status: 200"

return result
```

This approach is useful for larger reports.

---

# Example Report Structure

```text
Host

↓

HTTP

↓

Headers

↓

Cookies

↓

Security

↓

Summary
```

Organizing information into logical sections improves readability.

---

# Keeping Output Relevant

Avoid displaying unnecessary information.

Instead of:

```text
Every Header

Every Cookie

Entire HTML

Entire Response
```

Return only the most useful findings.

Professional reports emphasize quality over quantity.

---

# Consistent Labels

Choose descriptive labels.

Good:

```text
Server

Status

Title

Redirect

Cookies
```

Avoid abbreviations unless they are widely recognized.

---

# Complete Example

```lua
action = function(host, port)

    local output = ""

    output = output ..

    "Host: " ..

    host.ip ..

    "\n"

    output = output ..

    "Port: " ..

    port.number ..

    "\n"

    output = output ..

    "Protocol: " ..

    port.protocol

    return output

end
```

Possible output:

```text
Host: 192.168.1.20

Port: 80

Protocol: tcp
```

---

# Comparing Good and Bad Output

Poor:

```text
Apache2.4.57LinuxSSLYesHTTP200
```

Better:

```text
Server : Apache

Version: 2.4.57

OS     : Linux

SSL    : Enabled

Status : 200
```

Readable output saves analysts valuable time.

---

# Using Debug Output

Debug information should not appear during normal execution.

Example:

```lua
stdnse.debug(
1,
"Parsing response."
)
```

Run:

```bash
nmap -d
```

Keep debugging separate from user-facing output.

---

# Output Design Principles

Professional reports should be:

```text
Readable

↓

Consistent

↓

Relevant

↓

Concise

↓

Structured
```

These principles improve the user experience.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Returning entire HTML pages | Produces overwhelming output |
| Using inconsistent labels | Makes reports confusing |
| Mixing debug messages with results | Reduces readability |
| Returning raw Lua objects | Difficult to interpret |
| Ignoring formatting | Professional appearance suffers |

---

# Best Practices

When formatting NSE output:

- Keep reports concise.
- Group related information.
- Use descriptive labels.
- Return structured tables when appropriate.
- Display only useful findings.
- Separate debug output from final results.
- Maintain consistent formatting throughout the script.

These practices make scripts easier to use and maintain.

---

# Lab Challenge

Complete the following tasks:

1. Create `formatted-output.nse`.
2. Display the host IP.
3. Display the port number.
4. Display the protocol.
5. Format the output using multiple lines.
6. Return a Lua table.
7. Preview only the first 100 characters of an HTTP response.
8. Add meaningful error messages.
9. Compare string-based and table-based output.
10. Test the script against multiple hosts.

---

# What You Learned

After completing this lab, you should understand:

- How to create readable output.
- How to return strings and tables.
- How to organize information logically.
- How to avoid excessive output.
- How professional NSE reports are structured.
- Why presentation is as important as data collection.

These techniques greatly improve the usability and professionalism of your NSE scripts.

---

## Chapter Summary

Well-formatted output transforms raw scan data into meaningful information that analysts can understand quickly. By organizing results into logical sections, using descriptive labels, returning structured tables, and limiting unnecessary details, your scripts become significantly more useful during real-world security assessments.

With output formatting complete, the next chapter focuses on **error handling**, where you will learn how to anticipate failures, recover gracefully from network and runtime errors, and build robust NSE scripts that continue operating reliably even in unpredictable environments.

---

# Next Chapter

## Chapter 49 — Error Handling Lab