# Chapter 24 — Variables and Data Types

Variables are one of the most fundamental concepts in every programming language. They allow programs to store information, manipulate values, and exchange data between different parts of the code.

In Lua, variables are simple to declare because the language is **dynamically typed**. Unlike languages such as C++, Java, or C#, you do not need to specify a variable's type before assigning a value.

Understanding variables and data types is essential before writing NSE scripts, as every script stores information such as hosts, ports, services, and scan results using variables.

---

## What Is a Variable?

A variable is a named location in memory used to store data.

Example:

```lua
local username = "admin"
```

Here:

- `local` declares a local variable.
- `username` is the variable name.
- `"admin"` is the assigned value.

The value can later be used throughout the program.

```lua
print(username)
```

Output:

```text
admin
```

---

## Variable Declaration

Variables are created simply by assigning a value.

```lua
local port = 80
```

```lua
local service = "http"
```

```lua
local secure = true
```

---

## Why Use `local`?

Lua supports both **global** and **local** variables.

Example:

```lua
local host = "192.168.1.10"
```

The variable exists only within the current block.

Without `local`:

```lua
host = "192.168.1.10"
```

The variable becomes global.

For NSE development, **local variables should almost always be preferred** because they:

- Reduce memory usage
- Improve performance
- Prevent naming conflicts
- Make scripts easier to maintain

---

## Variable Assignment

Variables can be reassigned.

```lua
local count = 1

count = 2

print(count)
```

Output:

```text
2
```

The previous value is replaced.

---

## Multiple Assignment

Lua supports assigning multiple variables simultaneously.

```lua
local host, port = "scanme.nmap.org", 80
```

```lua
print(host)
print(port)
```

Output:

```text
scanme.nmap.org
80
```

---

## Swapping Variables

One of Lua's elegant features is automatic value swapping.

Instead of:

```lua
local a = 1
local b = 2

local temp = a
a = b
b = temp
```

Lua allows:

```lua
local a = 1
local b = 2

a, b = b, a
```

Output:

```text
a = 2
b = 1
```

No temporary variable is required.

---

# Data Types

Lua has a small set of built-in data types.

| Type | Description |
|------|-------------|
| nil | Represents the absence of a value |
| boolean | true or false |
| number | Integer or floating-point value |
| string | Text |
| function | Executable function |
| table | Collection of values |
| userdata | External C objects |
| thread | Lua coroutine |

For most NSE development, you will primarily use:

- nil
- boolean
- number
- string
- table

---

## Numbers

Numbers represent numeric values.

Examples:

```lua
local port = 443
```

```lua
local version = 5.4
```

```lua
local timeout = 3000
```

Arithmetic operations are supported naturally.

```lua
local result = 5 + 10

print(result)
```

Output:

```text
15
```

---

## Strings

Strings represent text.

Examples:

```lua
local service = "SSH"
```

```lua
local banner = "OpenSSH 9.7"
```

```lua
print(service)
```

Output:

```text
SSH
```

Strings are heavily used in NSE because protocols exchange textual data.

---

## Booleans

Boolean values represent logical truth.

Only two values exist.

```lua
true
```

```lua
false
```

Example:

```lua
local openPort = true

print(openPort)
```

Output:

```text
true
```

Booleans are commonly used in conditions.

---

## Nil

`nil` represents the absence of a value.

Example:

```lua
local password = nil
```

It may indicate:

- Unknown value
- Missing information
- Deleted variable

Example:

```lua
local host = "server"

host = nil

print(host)
```

Output:

```text
nil
```

---

## Tables

Tables are Lua's most powerful data structure.

Example:

```lua
local ports = {22, 80, 443}
```

Access values:

```lua
print(ports[1])
```

Output:

```text
22
```

Tables will be studied in depth in a later chapter because they are fundamental to NSE development.

---

## Functions

Functions are values in Lua.

Example:

```lua
local greet = function()

    print("Hello")

end
```

Functions can be stored inside variables, passed as arguments, and returned from other functions.

---

## Checking a Variable's Type

Lua provides the `type()` function.

Example:

```lua
local port = 80

print(type(port))
```

Output:

```text
number
```

More examples:

```lua
print(type("SSH"))
```

```text
string
```

```lua
print(type(true))
```

```text
boolean
```

---

## Dynamic Typing

Variables are **not permanently bound** to a single type.

Example:

```lua
local value = 80

value = "HTTP"

value = true
```

The same variable now stores different data types.

This flexibility simplifies scripting but requires careful programming.

---

## Type Conversion

Lua performs some automatic conversions, but explicit conversion is often safer.

Convert string to number:

```lua
local port = tonumber("443")
```

Convert number to string:

```lua
local version = tostring(5.4)
```

These functions are frequently used when processing network data.

---

## Variable Scope

Variables exist only within their scope.

Example:

```lua
local host = "server"

if true then

    local port = 80

end
```

Here:

- `host` exists throughout the file.
- `port` exists only inside the `if` block.

Keeping variables local prevents accidental modification.

---

## Common Beginner Mistakes

| Mistake | Example |
|----------|---------|
| Forgetting `local` | Creates unwanted global variables |
| Using the wrong type | Treating text as a number |
| Misspelling variable names | `host` vs `Host` |
| Overwriting variables | Losing previous values |
| Confusing `nil` with `false` | They are different values |

Understanding these differences prevents many programming errors.

---

## Best Practices

When working with variables:

- Prefer `local` variables.
- Use descriptive names.
- Avoid unnecessary global variables.
- Initialize variables clearly.
- Keep variable scope as small as possible.
- Use `type()` when debugging.

These habits improve readability and reliability.

---

## Chapter Summary

Variables allow Lua programs to store and manipulate information efficiently.

Lua's dynamic typing system provides flexibility while supporting a concise and readable programming style. By understanding variable declaration, scope, assignment, and the fundamental data types, you now have the knowledge required to begin writing more complex programs.

In the next chapter, we will explore **operators**, which allow variables and values to be combined, compared, and manipulated through arithmetic, logical, relational, and string operations.

---

# Next Chapter

## Chapter 25 — Operators