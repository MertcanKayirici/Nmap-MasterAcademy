# Chapter 31 — NSE Libraries

Writing network scanners completely from scratch would require implementing support for dozens of protocols, socket management, HTTP parsing, DNS resolution, SSL/TLS communication, output formatting, threading, timing, and many other low-level tasks.

Fortunately, the Nmap Scripting Engine (NSE) provides a rich collection of **built-in libraries** that perform these operations for you.

Instead of reinventing common functionality, NSE scripts simply import the appropriate library and focus on solving the specific problem at hand.

Learning how to use NSE libraries is one of the most important steps toward writing professional Nmap scripts.

---

# What Is an NSE Library?

An NSE library is a reusable Lua module that provides specialized functionality for script developers.

Conceptually:

```text
Your Script
      │
      ▼
NSE Library
      │
      ▼
Operating System
      │
      ▼
Network
```

Libraries hide implementation details so developers can work with simple, high-level functions.

---

# Why NSE Libraries Exist

Without libraries, every script would need to implement:

- Socket creation
- TCP communication
- UDP communication
- HTTP parsing
- SSL handling
- DNS resolution
- Output formatting
- Authentication logic

This would result in duplicated code and inconsistent behavior.

Libraries solve these problems by providing reusable implementations.

---

# Importing Libraries

Libraries are imported using `require()`.

Example:

```lua
local http = require("http")
```

Another example:

```lua
local shortport = require("shortport")
```

Multiple libraries may be imported.

```lua
local http = require("http")
local stdnse = require("stdnse")
local shortport = require("shortport")
```

This is a common pattern in official NSE scripts.

---

# Library Architecture

A simplified view of the NSE library system:

```text
NSE Script
     │
     ▼
+----------------------+
| HTTP Library         |
| DNS Library          |
| SSL Library          |
| FTP Library          |
| SMB Library          |
| SSH Library          |
| SNMP Library         |
| JSON Library         |
| Utility Libraries    |
+----------------------+
     │
     ▼
Network Communication
```

Each library focuses on a specific domain.

---

# The http Library

One of the most widely used libraries is `http`.

Import:

```lua
local http = require("http")
```

Simple request:

```lua
local response = http.get(host, port, "/")
```

The library automatically handles:

- TCP connections
- HTTP requests
- Headers
- Responses
- Protocol details

Without the library, implementing these features would require hundreds of lines of code.

---

# The shortport Library

Most scripts need rules describing when they should execute.

Example:

```lua
local shortport = require("shortport")
```

Later:

```lua
portrule = shortport.http
```

Instead of writing custom port detection logic, the script simply uses predefined helper functions.

This greatly simplifies development.

---

# The stdnse Library

`stdnse` stands for **Standard NSE**.

Import:

```lua
local stdnse = require("stdnse")
```

This library provides many utility functions, including:

- Logging
- Formatting
- Timing
- Script arguments
- Debugging helpers
- General-purpose utilities

Nearly every complex NSE script imports `stdnse`.

---

# The string Library

Lua includes its own string manipulation library.

Example:

```lua
local text = "Nmap"

print(string.upper(text))
```

Output:

```text
NMAP
```

Other useful functions include:

- `string.lower()`
- `string.find()`
- `string.sub()`
- `string.match()`
- `string.gsub()`

These functions are useful when parsing protocol responses.

---

# The table Library

The `table` library provides utilities for working with tables.

Example:

```lua
local ports = {80,22,443}

table.sort(ports)
```

Result:

```text
22
80
443
```

Other functions include:

- `table.insert()`
- `table.remove()`
- `table.concat()`

---

# The math Library

Mathematical operations are provided through the `math` library.

Example:

```lua
print(math.sqrt(81))
```

Output:

```text
9
```

Although less common in NSE development, it is useful for calculations and timing.

---

# The os Library

Lua also provides limited operating system functionality.

Example:

```lua
print(os.date())
```

Output:

```text
Thu Jul 16 21:30:00
```

Within NSE, operating system access is intentionally restricted for security and portability reasons.

---

# Protocol Libraries

Nmap includes specialized libraries for many network protocols.

Examples include:

| Library | Purpose |
|---------|----------|
| `http` | HTTP communication |
| `dns` | DNS requests |
| `ftp` | FTP operations |
| `smtp` | Email protocols |
| `imap` | Mail retrieval |
| `pop3` | POP3 communication |
| `ssh2` | SSH protocol |
| `sslcert` | SSL certificate parsing |
| `snmp` | SNMP communication |
| `ldap` | LDAP queries |
| `mysql` | MySQL protocol |
| `pgsql` | PostgreSQL protocol |
| `mongodb` | MongoDB communication |
| `redis` | Redis protocol |

These libraries eliminate the need to manually implement each protocol.

---

# Utility Libraries

Some libraries provide general-purpose functionality.

Examples include:

| Library | Purpose |
|----------|----------|
| `json` | JSON encoding and decoding |
| `base64` | Base64 conversion |
| `datetime` | Date utilities |
| `ipOps` | IP address manipulation |
| `rand` | Random number generation |
| `url` | URL parsing |
| `creds` | Credential storage |
| `vulns` | Vulnerability reporting |

These libraries are frequently combined within larger scripts.

---

# Example: Combining Libraries

Professional scripts often use several libraries simultaneously.

```lua
local http = require("http")
local shortport = require("shortport")
local stdnse = require("stdnse")
```

Workflow:

```text
Port Detected
      │
      ▼
shortport
      │
      ▼
HTTP Request
      │
      ▼
http
      │
      ▼
Format Output
      │
      ▼
stdnse
```

Each library contributes a specialized capability.

---

# Library Documentation

Official NSE libraries are documented in the Nmap reference guide.

Typical documentation includes:

- Available functions
- Parameters
- Return values
- Usage examples
- Supported protocols

Reading library documentation is an essential skill for NSE developers.

---

# Why Use Libraries Instead of Writing Everything Yourself?

Consider an HTTP request.

Without the library:

```text
Open Socket
      │
Create Request
      │
Send Headers
      │
Receive Response
      │
Parse HTTP
      │
Handle Errors
      │
Close Socket
```

With the `http` library:

```lua
http.get(host, port, "/")
```

The library performs all low-level operations internally.

This saves development time while reducing bugs.

---

# Common Beginner Mistakes

| Mistake | Example |
|----------|---------|
| Forgetting `require()` | Library functions unavailable |
| Misspelling library names | Module not found |
| Ignoring return values | Missing important data |
| Reinventing existing functionality | Unnecessary code |
| Using the wrong library | Incorrect protocol support |

Most issues can be avoided by consulting the official documentation.

---

# Best Practices

When working with NSE libraries:

- Prefer existing libraries over custom implementations.
- Import only the libraries your script needs.
- Read the documentation before using unfamiliar functions.
- Handle library return values carefully.
- Keep protocol-specific logic inside the appropriate library.
- Reuse proven library functions whenever possible.

Leveraging existing libraries results in shorter, more reliable, and more maintainable scripts.

---

# Libraries Used by Official Scripts

A simplified view of a typical official NSE script:

```text
Script
│
├── shortport
├── stdnse
├── http
├── json
├── vulns
└── sslcert
```

Rather than implementing networking, parsing, and reporting themselves, official scripts build upon these reusable components.

---

## Chapter Summary

NSE libraries provide the building blocks that make Nmap scripting efficient and practical. By encapsulating complex networking operations into reusable modules, they allow developers to focus on solving security problems instead of implementing low-level protocol details.

Mastering the available libraries dramatically increases development speed and code quality. Almost every professional NSE script imports several libraries, making them an indispensable part of the NSE ecosystem.

With a solid understanding of Lua fundamentals and the available libraries, you are now ready to examine the internal structure of an NSE script and understand how all of these components fit together.

---

# Next Chapter

## Chapter 32 — NSE Script Structure