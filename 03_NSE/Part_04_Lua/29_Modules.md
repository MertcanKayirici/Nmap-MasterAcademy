# Chapter 29 — Modules

As software projects grow, placing all code into a single file quickly becomes difficult to manage. Functions become scattered, maintenance becomes harder, and code reuse becomes limited.

Lua solves this problem through **modules**.

A module is a reusable collection of related functions, variables, and tables stored in a separate file. Modules allow developers to organize code into logical components and share functionality across multiple programs.

Although many simple Lua programs fit into a single file, virtually every large Lua application—including the Nmap Scripting Engine (NSE)—relies heavily on modules.

---

## What Is a Module?

A module is simply a Lua file that returns a table containing reusable functionality.

Conceptually:

```text
+----------------------+
| network.lua          |
|----------------------|
| connect()            |
| disconnect()         |
| send()               |
| receive()            |
+----------------------+
           │
           ▼
Imported by other files
```

Instead of rewriting the same code, other programs can simply import the module.

---

# Why Modules Matter

Modules provide several important benefits.

They improve:

- Code organization
- Reusability
- Readability
- Maintainability
- Collaboration

Without modules:

```text
Program.lua

5000 lines
```

With modules:

```text
Program.lua

network.lua
database.lua
http.lua
crypto.lua
output.lua
```

Each file has a single responsibility.

---

# Creating Your First Module

Suppose we create a file named:

```text
mathutils.lua
```

Contents:

```lua
local mathutils = {}

function mathutils.add(a, b)
    return a + b
end

return mathutils
```

This file creates a table named `mathutils`, adds a function to it, and returns the table.

That returned table becomes the module.

---

# Loading a Module

Modules are loaded using `require()`.

Example:

```lua
local mathutils = require("mathutils")

print(mathutils.add(5, 3))
```

Output:

```text
8
```

The module is loaded only once during program execution.

---

# How require() Works

When Lua executes:

```lua
require("mathutils")
```

it performs several steps:

```text
Search module
      │
      ▼
Load file
      │
      ▼
Execute file
      │
      ▼
Return module table
      │
      ▼
Cache module
```

If another part of the program calls:

```lua
require("mathutils")
```

again, Lua returns the cached module instead of loading the file a second time.

---

# Module Structure

Most Lua modules follow the same structure.

```lua
local module = {}

function module.function1()

end

function module.function2()

end

return module
```

This pattern is considered standard Lua practice.

---

# Multiple Functions

Modules usually contain multiple related functions.

Example:

```lua
local calculator = {}

function calculator.add(a, b)
    return a + b
end

function calculator.subtract(a, b)
    return a - b
end

function calculator.multiply(a, b)
    return a * b
end

return calculator
```

Usage:

```lua
local calc = require("calculator")

print(calc.multiply(5, 4))
```

Output:

```text
20
```

---

# Local Variables Inside Modules

Internal variables should usually remain private.

Example:

```lua
local network = {}

local timeout = 5000

function network.getTimeout()

    return timeout

end

return network
```

Outside programs cannot directly access:

```lua
timeout
```

Only exported functions expose the data.

This is known as **encapsulation**.

---

# Module Namespace

Modules help prevent naming conflicts.

Without modules:

```lua
function connect()

end

function send()

end
```

With modules:

```lua
network.connect()

network.send()

http.connect()

ftp.connect()
```

Different modules may safely define functions with the same name.

---

# Returning Tables

Almost every Lua module returns a table.

Example:

```lua
local server = {}

server.host = "scanme.nmap.org"

server.port = 80

return server
```

Usage:

```lua
local server = require("server")

print(server.host)
```

Output:

```text
scanme.nmap.org
```

---

# Module Search Path

Lua searches specific directories when loading modules.

The search path is stored in:

```lua
package.path
```

View it:

```lua
print(package.path)
```

Typical output:

```text
./?.lua
/usr/share/lua/5.4/?.lua
...
```

Each `?` is replaced with the requested module name.

---

# Modules in Nmap

NSE scripts rarely implement everything themselves.

Instead, they load existing libraries.

Example:

```lua
local http = require("http")
```

```lua
local shortport = require("shortport")
```

```lua
local stdnse = require("stdnse")
```

```lua
local string = require("string")
```

Each module provides specialized functionality.

---

# Common NSE Libraries

Some frequently used modules include:

| Module | Purpose |
|---------|----------|
| `http` | HTTP communication |
| `shortport` | Port rule helpers |
| `stdnse` | Utility functions |
| `sslcert` | SSL certificate parsing |
| `dns` | DNS queries |
| `json` | JSON processing |
| `base64` | Encoding and decoding |
| `string` | String manipulation |
| `table` | Table utilities |

Most official NSE scripts begin by importing several of these libraries.

---

# Practical Example

A simplified NSE script might begin like this:

```lua
local http = require("http")
local shortport = require("shortport")
local stdnse = require("stdnse")
```

Later:

```lua
local response = http.get(host, port, "/")
```

Instead of implementing an HTTP client from scratch, the script simply calls functions provided by the `http` module.

---

# Advantages of Modules

Modules provide several benefits.

| Advantage | Explanation |
|------------|-------------|
| Reusability | Write code once and use it everywhere |
| Organization | Separate related functionality |
| Encapsulation | Hide internal implementation |
| Maintainability | Easier updates |
| Collaboration | Teams work on different modules independently |
| Reduced duplication | Less repeated code |

These advantages become increasingly important as projects grow.

---

# Common Beginner Mistakes

| Mistake | Example |
|----------|---------|
| Forgetting `return module` | Module loads as `nil` |
| Using globals instead of locals | Namespace pollution |
| Incorrect filename | `require()` cannot find the module |
| Circular dependencies | Modules loading each other |
| Expecting repeated execution | `require()` caches modules |

Understanding Lua's module system helps avoid these problems.

---

# Best Practices

When creating modules:

- Export only what is necessary.
- Keep helper variables local.
- Group related functions together.
- Give modules descriptive names.
- Avoid unnecessary global variables.
- Document exported functions.
- Design each module with a single responsibility.

Following these principles produces clean and reusable Lua code.

---

## Modules vs. Libraries

The terms **module** and **library** are closely related but not identical.

| Module | Library |
|----------|----------|
| A single reusable Lua file | A collection of related modules |
| Usually solves one problem | Covers a broader domain |
| Loaded with `require()` | Often consists of multiple modules |
| Small building block | Larger software package |

For example:

```text
Library
│
├── http.lua
├── response.lua
├── request.lua
└── cookies.lua
```

Each individual file is a module, while together they form a library.

---

## Chapter Summary

Modules allow Lua programs to be divided into reusable, maintainable, and well-organized components. By exporting functionality through tables and importing it with `require()`, developers can avoid code duplication and build applications that scale far beyond a single source file.

For NSE development, understanding modules is essential because almost every official script depends on multiple Nmap libraries. Learning to use these libraries effectively is one of the biggest productivity gains when writing custom NSE scripts.

---

# Next Chapter

## Chapter 30 — Error Handling