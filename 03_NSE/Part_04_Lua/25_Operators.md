# Chapter 25 — Operators

Operators are symbols or keywords that allow programs to perform calculations, compare values, combine expressions, and make logical decisions.

Every programming language provides operators, and Lua is no exception. Although Lua has a relatively small operator set compared to many other languages, it provides everything needed for efficient scripting and NSE development.

Understanding operators is essential because they are used in nearly every Lua program—from simple calculations to complex conditional logic inside NSE scripts.

---

## What Is an Operator?

An operator performs an action on one or more values.

Example:

```lua
5 + 3
```

The `+` operator adds two numbers.

Example:

```lua
print(10 - 4)
```

Output:

```text
6
```

---

# Arithmetic Operators

Arithmetic operators perform mathematical calculations.

| Operator | Description | Example |
|----------|-------------|---------|
| `+` | Addition | `5 + 2` |
| `-` | Subtraction | `5 - 2` |
| `*` | Multiplication | `5 * 2` |
| `/` | Division | `10 / 2` |
| `//` | Floor Division | `10 // 3` |
| `%` | Modulus | `10 % 3` |
| `^` | Exponentiation | `2 ^ 3` |
| `-` | Unary Minus | `-5` |

---

## Addition

```lua
local result = 8 + 2

print(result)
```

Output:

```text
10
```

---

## Subtraction

```lua
local result = 20 - 8

print(result)
```

Output:

```text
12
```

---

## Multiplication

```lua
local result = 6 * 7

print(result)
```

Output:

```text
42
```

---

## Division

```lua
local result = 20 / 4

print(result)
```

Output:

```text
5
```

---

## Floor Division

Floor division removes the decimal portion.

```lua
print(10 // 3)
```

Output:

```text
3
```

---

## Modulus

Returns the remainder after division.

```lua
print(10 % 3)
```

Output:

```text
1
```

Useful examples:

- Checking whether a number is even
- Round-robin scheduling
- Network calculations

---

## Exponentiation

Raises one number to the power of another.

```lua
print(2 ^ 5)
```

Output:

```text
32
```

---

# Relational Operators

Relational operators compare two values.

The result is always:

```lua
true
```

or

```lua
false
```

| Operator | Meaning |
|----------|---------|
| `==` | Equal |
| `~=` | Not equal |
| `<` | Less than |
| `>` | Greater than |
| `<=` | Less than or equal |
| `>=` | Greater than or equal |

---

## Equality

```lua
print(80 == 80)
```

Output:

```text
true
```

---

## Inequality

```lua
print(22 ~= 80)
```

Output:

```text
true
```

---

## Greater Than

```lua
print(443 > 80)
```

Output:

```text
true
```

---

## Less Than

```lua
print(22 < 80)
```

Output:

```text
true
```

---

# Logical Operators

Logical operators combine multiple conditions.

| Operator | Description |
|----------|-------------|
| `and` | Both conditions must be true |
| `or` | At least one condition must be true |
| `not` | Reverses a boolean value |

---

## AND

```lua
local open = true
local ssh = true

print(open and ssh)
```

Output:

```text
true
```

---

## OR

```lua
local ftp = false
local ssh = true

print(ftp or ssh)
```

Output:

```text
true
```

---

## NOT

```lua
print(not true)
```

Output:

```text
false
```

---

# String Concatenation

Lua uses the `..` operator to combine strings.

Example:

```lua
local host = "scanme"
local domain = ".nmap.org"

print(host .. domain)
```

Output:

```text
scanme.nmap.org
```

---

## Concatenating Multiple Strings

```lua
local protocol = "https"
local host = "scanme.nmap.org"

print(protocol .. "://" .. host)
```

Output:

```text
https://scanme.nmap.org
```

This operator is used frequently in NSE scripts when constructing URLs or protocol messages.

---

# Length Operator

The `#` operator returns the length of a string or table.

Example:

```lua
print(#"Nmap")
```

Output:

```text
4
```

Table example:

```lua
local ports = {22,80,443}

print(#ports)
```

Output:

```text
3
```

---

# Operator Precedence

Lua evaluates operators according to precedence rules.

Example:

```lua
print(2 + 3 * 4)
```

Output:

```text
14
```

because multiplication is evaluated before addition.

Using parentheses improves readability.

```lua
print((2 + 3) * 4)
```

Output:

```text
20
```

---

## Common NSE Examples

Check whether a port is HTTPS.

```lua
local port = 443

print(port == 443)
```

Output:

```text
true
```

---

Build an HTTP URL.

```lua
local host = "example.com"

print("http://" .. host)
```

Output:

```text
http://example.com
```

---

Determine whether authentication is required.

```lua
local login = true
local ssl = true

if login and ssl then
    print("Secure authentication")
end
```

Output:

```text
Secure authentication
```

---

## Common Beginner Mistakes

| Mistake | Example |
|----------|---------|
| Using `=` instead of `==` | Comparison error |
| Forgetting `..` | String concatenation fails |
| Confusing `and` with `&` | Lua uses keywords |
| Confusing `or` with `\|\|` | Lua does not use C-style operators |
| Ignoring precedence | Unexpected calculations |

---

## Best Practices

When using operators:

- Use parentheses to improve readability.
- Keep logical expressions simple.
- Use descriptive variable names.
- Compare values explicitly.
- Avoid unnecessary complexity in conditions.
- Format long expressions across multiple lines when needed.

These practices improve code clarity and reduce logical errors.

---

## Chapter Summary

Operators allow Lua programs to perform calculations, compare values, manipulate strings, and evaluate logical conditions.

Mastering arithmetic, relational, logical, concatenation, and length operators provides the foundation for writing expressive and efficient Lua programs. These operators are used extensively throughout NSE scripts to process scan results, evaluate conditions, and construct protocol messages.

---

# Next Chapter

## Chapter 26 — Control Structures