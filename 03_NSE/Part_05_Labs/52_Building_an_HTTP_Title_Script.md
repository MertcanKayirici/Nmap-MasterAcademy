# Chapter 52 — Building an HTTP Title Script

One of the quickest ways to identify a web application is to examine the HTML **`<title>`** element.

Web browsers display this title in the browser tab, but penetration testers often use it to rapidly recognize:

- Login portals
- Administration panels
- Routers
- IP cameras
- NAS devices
- CMS platforms
- Monitoring dashboards
- Development environments

Many reconnaissance tools extract page titles because they provide valuable context with minimal network traffic.

In this chapter, you will build an NSE script that retrieves a web page and extracts its HTML title.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Retrieve web pages using the HTTP library.
- Read HTTP response bodies.
- Extract HTML titles.
- Handle missing titles.
- Produce clean script output.
- Test against multiple websites.

---

# What Is an HTML Title?

Every HTML page may contain a title element.

Example:

```html
<html>

<head>

<title>Example Domain</title>

</head>

<body>

...

</body>

</html>
```

The text inside the `<title>` tag identifies the page.

---

# Why Titles Matter

Suppose a penetration tester scans hundreds of web servers.

Instead of seeing:

```text
80/tcp open http
```

they may see:

```text
Apache2 Ubuntu Default Page
```

or

```text
Jenkins Dashboard
```

or

```text
phpMyAdmin
```

or

```text
Admin Login
```

This immediately provides useful reconnaissance information.

---

# Project Workflow

```text
Target

      │

      ▼

HTTP GET

      │

      ▼

Receive HTML

      │

      ▼

Find <title>

      │

      ▼

Extract Text

      │

      ▼

Display Result
```

---

# Required Libraries

```lua
local http =
require("http")

local shortport =
require("shortport")
```

---

# Defining the Rule

Our script targets web servers.

```lua
portrule =
shortport.http
```

---

# Retrieving the Home Page

```lua
local response =

http.get(
host,
port,
"/"
)
```

If successful:

```text
HTTP 200

↓

HTML Document
```

---

# Validating the Response

Always check whether the request succeeded.

```lua
if not response then

    return

    "No response."

end
```

Never assume every server replies.

---

# Reading the HTML

The HTML document is stored in:

```lua
response.body
```

Conceptually:

```text
HTTP Response

↓

Body

↓

HTML Source
```

---

# Finding the Title

Lua pattern matching can locate the title.

```lua
local title =

response.body:match(

"<title>(.-)</title>"

)
```

If found:

```text
Example Domain
```

The `(.-)` pattern captures everything between the opening and closing tags.

---

# Handling Missing Titles

Not every page contains a title.

Example:

```lua
if not title then

    return

    "Title not found."

end
```

This prevents nil-related runtime errors.

---

# Complete Script

```lua
local http =
require("http")

local shortport =
require("shortport")

portrule =
shortport.http

action = function(host, port)

    local response =

        http.get(
        host,
        port,
        "/"
        )

    if not response then

        return

        "Connection failed."

    end

    local title =

        response.body:match(

        "<title>(.-)</title>"

        )

    if not title then

        return

        "Title not found."

    end

    return

        "Page Title: " ..

        title

end
```

---

# Running the Script

```bash
nmap \
-p80 \
--script http-title.nse \
scanme.nmap.org
```

Possible output:

```text
PORT   STATE SERVICE

80/tcp open http

| http-title:

| Page Title: Example Domain

|_
```

---

# Example Results

Website:

```text
Example Domain
```

Jenkins:

```text
Dashboard [Jenkins]
```

phpMyAdmin:

```text
phpMyAdmin
```

WordPress:

```text
My Blog
```

GitLab:

```text
GitLab
```

Titles often reveal the underlying application immediately.

---

# Ignoring Case

Some websites use uppercase tags.

Example:

```html
<TITLE>

Admin Portal

</TITLE>
```

Professional scripts often perform case-insensitive matching or normalize the HTML before parsing.

---

# Trimming Extra Spaces

Some titles contain unnecessary whitespace.

Example:

```html
<title>

   Admin Login

</title>
```

After processing:

```text
Admin Login
```

Cleaning output improves readability.

---

# Following Redirects

Sometimes the homepage redirects.

```text
GET /

↓

301

↓

/login

↓

Final Page
```

Professional scripts may follow redirects automatically before extracting the title.

---

# Common Web Titles

| Title | Possible Application |
|--------|----------------------|
| Jenkins | Jenkins CI |
| Grafana | Grafana |
| Kibana | Kibana |
| phpMyAdmin | Database Management |
| Admin Login | Administrative Portal |
| Nextcloud | File Sharing |
| GitLab | Source Control |
| WordPress | CMS |

Recognizing these titles speeds up reconnaissance.

---

# Improving the Report

Instead of:

```text
Example Domain
```

Display:

```text
HTTP Information

----------------

Page Title

Example Domain
```

Structured reports are easier to interpret.

---

# Practical Uses

HTTP title extraction helps with:

- Web reconnaissance
- Asset inventory
- CMS identification
- Login portal discovery
- Administrative interface detection
- Technology fingerprinting

Many automated scanners use this technique.

---

# Execution Flow

```text
Start

↓

HTTP Request

↓

Response?

├── Yes

│      ↓

│  Read HTML

│      ↓

│  Find Title

│      ↓

│  Return Result

│

└── No

       ↓

Return Error
```

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Forgetting to validate the HTTP response | May cause runtime errors |
| Assuming every page has a `<title>` | Some pages omit it |
| Returning the entire HTML page | Produces excessive output |
| Ignoring redirects | Important pages may be missed |
| Using overly complex parsing | Simple pattern matching is often sufficient |

---

# Best Practices

When building HTTP title scripts:

- Validate every HTTP response.
- Handle missing titles gracefully.
- Return concise output.
- Test against different web servers.
- Keep parsing simple whenever possible.
- Use descriptive labels in reports.
- Consider redirects when appropriate.

---

# Lab Challenge

Complete the following tasks:

1. Create `http-title.nse`.
2. Retrieve the homepage.
3. Read the HTML response.
4. Extract the `<title>` element.
5. Handle missing titles.
6. Format the output.
7. Test against five different websites.
8. Compare results from Apache and Nginx servers.
9. Add debug messages.
10. Extend the script to support a custom path using `--script-args`.

---

# What You Learned

After completing this lab, you should understand:

- How to retrieve web pages using the HTTP library.
- How to access HTML content.
- How to extract page titles.
- How to handle missing data safely.
- How HTTP title extraction supports reconnaissance.
- How to present results clearly.

This project demonstrates how a small amount of Lua code can produce valuable reconnaissance information during web application assessments.

---

## Chapter Summary

In this chapter, you built a practical HTTP title extraction script using the NSE HTTP library. By requesting a web page, reading its HTML content, locating the `<title>` element, and handling missing or malformed responses gracefully, you created another real-world reconnaissance tool commonly used during penetration tests.

This project also reinforced key NSE concepts, including HTTP communication, pattern matching, error handling, and output formatting. In the next chapter, you will build a **Port Enumeration Script**, combining host and port information to generate structured reports about open services and their characteristics.

---

# Next Chapter

## Chapter 53 — Building a Port Enumeration Script