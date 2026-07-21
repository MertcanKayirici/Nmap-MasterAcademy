# Chapter 44 — HTTP Scripts

HTTP is the most widely used application-layer protocol on the Internet. Websites, REST APIs, cloud services, management interfaces, IoT devices, and countless enterprise applications all rely on HTTP or HTTPS.

Because of its widespread adoption, many NSE scripts target HTTP services. These scripts retrieve web pages, enumerate directories, inspect headers, analyze cookies, detect technologies, discover login pages, and identify vulnerabilities.

Fortunately, NSE provides a powerful **HTTP library** that hides the complexity of the HTTP protocol, allowing developers to focus on security analysis instead of low-level networking.

In this lab, you will learn how to build practical HTTP-based NSE scripts using the official HTTP library.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Use the NSE HTTP library.
- Send HTTP GET requests.
- Send HTTP HEAD requests.
- Read HTTP response headers.
- Read HTTP response bodies.
- Detect web servers.
- Extract useful information from responses.
- Handle HTTP errors gracefully.

---

# Why HTTP Scripts Matter

Many security assessments begin with web enumeration.

Example workflow:

```text
Target

     │

     ▼

HTTP Request

     │

     ▼

Receive Response

     │

     ▼

Analyze

     │

     ▼

Generate Report
```

A single HTTP request can reveal:

- Server software
- Web technologies
- Login pages
- Administrative interfaces
- Cookies
- Security headers
- Redirects
- Error messages

---

# Importing Required Libraries

Every HTTP script begins by importing the required libraries.

```lua
local http = require("http")

local shortport = require("shortport")
```

These libraries provide HTTP communication and rule helpers.

---

# Creating the Rule

Since the script targets web servers:

```lua
portrule = shortport.http
```

The script automatically executes on detected HTTP services.

---

# Making a GET Request

The simplest request is:

```lua
action = function(host, port)

    local response =
        http.get(host, port, "/")

    if not response then
        return "Connection failed."
    end

    return response.status

end
```

Execution flow:

```text
Target

↓

GET /

↓

HTTP Response

↓

Status Code
```

---

# Running the Script

```bash
nmap \
-p80 \
--script ./scripts/http-status.nse \
scanme.nmap.org
```

Possible output:

```text
HTTP Status: 200
```

---

# Understanding the Response Object

The HTTP library returns a structured object.

```text
Response

│

├── Status

├── Header

├── Body

├── Cookies

└── Metadata
```

This structure makes information easy to access.

---

# Reading the Status Code

Example:

```lua
return

"Status: "

..

response.status
```

Possible result:

```text
Status: 200
```

Other common status codes:

| Code | Meaning |
|------|----------|
| 200 | OK |
| 301 | Moved Permanently |
| 302 | Redirect |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

# Reading the Response Body

The page content is stored in:

```lua
response.body
```

Example:

```lua
action = function(host, port)

    local response =
        http.get(host, port, "/")

    return response.body

end
```

Since HTML pages may be very large, returning the entire body is rarely recommended.

---

# Displaying the First Characters

Instead of printing the entire page:

```lua
return response.body
```

display only a preview.

```lua
return response.body:sub(1,200)
```

Example output:

```html
<!DOCTYPE html>

<html>

<head>

<title>Example Domain</title>
```

This is much more readable.

---

# Reading HTTP Headers

Headers are stored inside a table.

Example:

```lua
for key, value in pairs(response.header) do

    print(key, value)

end
```

Possible output:

```text
Server Apache

Content-Type text/html

Content-Length 648

Date Tue...
```

Headers often reveal valuable information.

---

# Detecting the Web Server

Many servers identify themselves.

Example:

```lua
return response.header.server
```

Possible output:

```text
Apache

```

or

```text
nginx
```

or

```text
Microsoft-IIS
```

---

# Handling Missing Headers

Not every server exposes a Server header.

Safe implementation:

```lua
local server =
response.header.server

if server then

    return server

end

return "Server header unavailable."
```

Never assume a field exists.

---

# Sending a HEAD Request

Sometimes only headers are needed.

```lua
local response =
http.head(host, port, "/")
```

Advantages:

- Faster
- Smaller response
- Less bandwidth
- Faster scanning

---

# Following Redirects

Suppose the server responds:

```text
301

↓

/login
```

The HTTP library can follow redirects when configured appropriately, allowing the script to analyze the final destination instead of the initial response.

---

# Detecting Page Titles

Suppose the body contains:

```html
<title>

Admin Login

</title>
```

The script can extract:

```text
Admin Login
```

Many official NSE scripts perform similar parsing.

---

# Looking for Keywords

Example:

```lua
if response.body:find("login") then

    return "Login page detected."

end
```

Possible results:

- Login Portal
- phpMyAdmin
- WordPress
- Jenkins
- GitLab

Keyword matching is useful during reconnaissance.

---

# Using Debug Messages

```lua
local stdnse =
require("stdnse")

stdnse.debug(
1,
"Sending GET request."
)
```

Execute:

```bash
nmap -d
```

This helps diagnose communication problems.

---

# Complete Example

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
        return "Connection failed."
    end

    return

        "HTTP Status: " ..

        response.status ..

        "\nServer: " ..

        (response.header.server or "Unknown")

end
```

Example output:

```text
HTTP Status: 200

Server: nginx
```

---

# Practical Use Cases

HTTP scripts are commonly used for:

- Web reconnaissance
- Technology fingerprinting
- Banner grabbing
- Security header analysis
- Login page detection
- CMS identification
- API discovery
- Vulnerability detection

Many official NSE scripts fall into these categories.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Returning the full HTML page | Produces excessive output |
| Ignoring failed requests | Leads to runtime errors |
| Assuming all headers exist | Some servers hide information |
| Forgetting `shortport.http` | Script may execute on irrelevant services |
| Not validating responses | Unexpected failures occur |

---

# Best Practices

When writing HTTP scripts:

- Check whether a response exists before using it.
- Display concise output.
- Handle missing headers gracefully.
- Avoid printing entire web pages.
- Prefer HEAD requests when only headers are required.
- Use debug messages during development.
- Keep parsing logic separate from network communication.

These practices improve readability, performance, and reliability.

---

# Lab Challenge

Complete the following tasks:

1. Create `http-status.nse`.
2. Send a GET request.
3. Display the HTTP status code.
4. Display the Server header.
5. Display the first 200 characters of the response body.
6. Try a HEAD request.
7. Detect whether the page contains the word "login".
8. Add debug messages.
9. Test the script against three different web servers.
10. Compare the responses from Apache, Nginx, and IIS.

---

# What You Learned

After completing this lab, you should understand:

- How to use the NSE HTTP library.
- How HTTP requests are performed.
- How to read response headers.
- How to process response bodies.
- How to identify common web technologies.
- How to safely handle network failures.

These techniques form the basis of many web-focused NSE scripts.

---

## Chapter Summary

HTTP scripting is one of the most practical applications of the Nmap Scripting Engine. By using the built-in HTTP library, you can interact with web servers, retrieve pages, inspect headers, identify technologies, and gather valuable reconnaissance information with only a small amount of Lua code.

The skills learned in this chapter will be reused extensively as we build more advanced web enumeration and vulnerability detection scripts. In the next lab, we will move one layer deeper and explore **TCP communication**, learning how NSE scripts establish raw socket connections and exchange data directly with network services.

---

# Next Chapter

## Chapter 45 — TCP Communication