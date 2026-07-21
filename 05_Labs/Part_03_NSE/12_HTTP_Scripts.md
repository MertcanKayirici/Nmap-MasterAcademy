# Lab 12 — HTTP Scripts

> Learn how to enumerate web servers using HTTP-related NSE scripts and interpret the collected information.

---

# Overview

Web servers are among the most common services encountered during network assessments.

A simple port scan may reveal that ports **80** or **443** are open, but that alone provides very little information.

HTTP-related NSE scripts allow you to gather additional details such as:

- Page titles
- HTTP headers
- Supported methods
- Robots.txt
- Default pages
- Server software
- Authentication mechanisms

These details help build a clearer understanding of the target before using more specialized web assessment tools.

---

# Learning Objectives

After completing this lab, you will be able to:

- Execute HTTP NSE scripts.
- Retrieve page titles.
- Analyze HTTP response headers.
- Identify server software.
- Discover supported HTTP methods.
- Interpret web server information.
- Decide the next enumeration steps.

---

# Difficulty

⭐⭐⭐☆☆ Intermediate

---

# Estimated Time

45–60 Minutes

---

# Prerequisites

- Part 01 completed
- Part 02 completed
- Lab 11 completed
- A target running an HTTP or HTTPS service

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| Target | 192.168.56.20 | Web Server |

---

# Scenario

An Nmap scan identified:

```text
80/tcp open http
443/tcp open https
```

Your objective is to collect as much information as possible about the web service before performing further web application testing.

---

# Step 1 — Retrieve the Page Title

Run:

```bash
nmap --script http-title 192.168.56.20
```

Example Output

```text
http-title:

Apache2 Ubuntu Default Page
```

The page title often reveals:

- Default installations
- Login portals
- Device management interfaces
- Internal applications

---

# Step 2 — Retrieve HTTP Headers

Run:

```bash
nmap --script http-headers 192.168.56.20
```

Example Output

```text
Server: Apache/2.4.57

Content-Type: text/html

Date: Mon, 20 Jul 2026
```

Questions to consider:

- Which web server is being used?
- Are unnecessary headers exposed?
- Does the response reveal framework or software information?

---

# Step 3 — Identify Server Banner

Run:

```bash
nmap --script http-server-header 192.168.56.20
```

Example Output

```text
Apache/2.4.57 (Ubuntu)
```

Possible servers include:

- Apache
- Nginx
- IIS
- LiteSpeed
- Caddy

---

# Step 4 — Enumerate HTTP Methods

Run:

```bash
nmap --script http-methods 192.168.56.20
```

Example Output

```text
Supported Methods

GET

POST

HEAD

OPTIONS
```

Unexpected methods such as `PUT`, `DELETE`, or `TRACE` may require further investigation.

---

# Step 5 — Retrieve robots.txt

Run:

```bash
nmap --script http-robots.txt 192.168.56.20
```

Example Output

```text
Disallow: /admin

Disallow: /backup
```

These entries may indicate interesting locations for authorized testing.

---

# Step 6 — Execute Multiple HTTP Scripts

Run:

```bash
nmap --script "http-title,http-headers,http-methods,http-server-header" 192.168.56.20
```

This combines several HTTP scripts into a single scan.

---

# Understanding the Results

Example:

```text
Apache/2.4.57
```

Possible conclusions:

- Apache web server
- Modern version
- Linux-based deployment (not guaranteed)
- Suitable for further HTTP enumeration

---

Example:

```text
Microsoft-IIS/10.0
```

Possible conclusions:

- Microsoft IIS
- Windows environment
- ASP.NET applications may be present

---

# Useful HTTP Scripts

| Script | Purpose |
|---------|---------|
| http-title | Retrieve page title |
| http-headers | Display HTTP headers |
| http-server-header | Display server banner |
| http-methods | Enumerate HTTP methods |
| http-robots.txt | Retrieve robots.txt |
| http-auth | Identify authentication methods |
| http-security-headers | Inspect security headers |

---

# NSE Script Deep Dive

## Script

```text
http-title.nse
```

Category

```
default
discovery
```

Purpose

Retrieves the HTML page title.

Typical Uses

- Identify applications
- Discover login pages
- Detect default installations

Limitations

- Dynamic applications may return generic titles.
- Some servers intentionally hide page titles.

Related Scripts

- http-headers
- http-server-header
- http-enum

---

# Thinking Like an Analyst

Suppose the scripts reveal:

```text
Title:

Admin Login
```

Questions:

- Is this the primary application?
- Is authentication enforced?
- Is HTTPS available?
- Does the login page disclose the product name?

---

Another example:

```text
Server:

nginx
```

Questions:

- Reverse proxy or web server?
- Which application is behind it?
- Are additional virtual hosts configured?

---

# Common Mistakes

## Assuming the Server Banner Is Accurate

Administrators may modify or suppress server banners.

Do not rely on them exclusively.

---

## Ignoring HTTP Headers

Headers often reveal frameworks, security configurations, or caching behavior.

---

## Running Every HTTP Script

Some scripts are more intrusive or time-consuming.

Select scripts appropriate for your objective.

---

# Challenge

Run the following:

```bash
nmap --script http-title,http-headers,http-methods target
```

Document:

- Page title
- Server software
- Supported HTTP methods
- Interesting headers

---

# Bonus Challenge

Use:

```bash
ls /usr/share/nmap/scripts/http*
```

Answer:

- How many HTTP-related NSE scripts are installed?
- Which script names suggest content discovery?
- Which scripts appear focused on security?

---

# Key Takeaways

- HTTP NSE scripts provide valuable information beyond open ports.
- Page titles, headers, and supported methods help identify web technologies.
- Server banners should be interpreted carefully.
- The collected information guides the next stage of web enumeration.

---

# Next Lab

➡ **Lab 13 — SMB Scripts**

In the next lab, you will enumerate Windows SMB services, discover shares, identify operating system information, and gather host details using SMB-related NSE scripts.