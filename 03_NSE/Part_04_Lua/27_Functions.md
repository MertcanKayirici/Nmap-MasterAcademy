# Chapter 27 — Functions

As programs grow larger, repeating the same code multiple times becomes inefficient and difficult to maintain. **Functions** solve this problem by allowing developers to organize reusable blocks of code into named units.

Functions are one of the most important features of Lua and form the foundation of every NSE script. In fact, every NSE script contains at least one function—the `action()` function—which serves as the script's entry point.

Learning how functions work is therefore essential before writing custom NSE scripts.

---

## What Is a Function?

A function is a reusable block of code that performs a specific task.

Instead of writing the same instructions repeatedly, the instructions are written once and executed whenever needed.

Without functions:

```text
Task A
Task A
Task A
Task A
```

With functions:

```text
Function
     │
     ▼
Execute
     │
     ▼
Task A
```

Functions improve:

- Readability
- Reusability
- Organization
- Maintainability
- Testing

---

## Defining a Function

A function is defined using the `function` keyword.

Syntax:

```lua
function functionName()

    -- code

end
```

Example:

```lua
function greet()

    print("Hello, Lua!")

end
```

The function is now defined but has not yet been executed.

---

## Calling a Function

To execute a function, write its name followed by parentheses.

```lua
greet()
```

Output:

```text
Hello, Lua!
```

A function may be called as many times as necessary.

```lua
greet()
greet()
greet()
```

Output:

```text
Hello, Lua!
Hello, Lua!
Hello, Lua!
```

---

## Local Functions

Functions can also be local.

```lua
local function scan()

    print("Scanning...")

end
```

Using `local` prevents the function from becoming globally accessible.

For NSE development, local functions are generally preferred because they reduce namespace pollution and improve script organization.

---

## Function Parameters

Functions often require input values.

These inputs are called **parameters**.

Example:

```lua
function greet(name)

    print("Hello, " .. name)

end
```

Calling the function:

```lua
greet("Alice")
```

Output:

```text
Hello, Alice
```

Parameters make functions reusable for different inputs.

---

## Multiple Parameters

Functions may accept multiple parameters.

Example:

```lua
function connect(host, port)

    print(host)
    print(port)

end
```

Call:

```lua
connect("scanme.nmap.org", 80)
```

Output:

```text
scanme.nmap.org
80
```

---

## Returning Values

Functions may return information to the caller.

Example:

```lua
function add(a, b)

    return a + b

end
```

Call:

```lua
local result = add(5, 8)

print(result)
```

Output:

```text
13
```

The `return` statement immediately ends the function and sends a value back.

---

## Returning Multiple Values

One unique feature of Lua is its ability to return multiple values.

Example:

```lua
function getServer()

    return "scanme.nmap.org", 80

end
```

Usage:

```lua
local host, port = getServer()

print(host)
print(port)
```

Output:

```text
scanme.nmap.org
80
```

This feature is widely used throughout Lua and NSE.

---

## Anonymous Functions

Functions do not always require names.

Example:

```lua
local greet = function()

    print("Hello!")

end
```

Call:

```lua
greet()
```

Output:

```text
Hello!
```

Anonymous functions are commonly used when passing functions as arguments.

---

## Functions as Values

In Lua, functions are **first-class values**.

This means they can be:

- Stored in variables
- Passed as arguments
- Returned from other functions
- Assigned to tables

Example:

```lua
local action = greet

action()
```

Output:

```text
Hello!
```

This flexibility is one of Lua's defining features.

---

## Variable Scope Inside Functions

Variables declared with `local` exist only inside the function.

Example:

```lua
function example()

    local port = 80

    print(port)

end
```

Outside the function:

```lua
print(port)
```

Output:

```text
nil
```

Local scope prevents accidental modification of variables elsewhere in the program.

---

## Recursive Functions

A function may call itself.

Example:

```lua
function countdown(n)

    if n == 0 then
        return
    end

    print(n)

    countdown(n - 1)

end

countdown(3)
```

Output:

```text
3
2
1
```

Recursion is a powerful technique but should be used carefully to avoid excessive memory usage.

---

## Practical NSE Example

Suppose an NSE script needs to display information about open ports.

```lua
local function printPort(port)

    print("Open Port: " .. port)

end

printPort(22)
printPort(80)
printPort(443)
```

Output:

```text
Open Port: 22
Open Port: 80
Open Port: 443
```

Instead of repeating the `print()` statement, a reusable function handles the task.

---

## Why Functions Matter in NSE

Every official NSE script relies heavily on functions.

A simplified structure looks like this:

```text
Script Starts
      │
      ▼
Helper Functions
      │
      ▼
Library Functions
      │
      ▼
action()
      │
      ▼
Generate Output
```

Functions divide large scripts into manageable components, making them easier to understand and maintain.

---

## Common Beginner Mistakes

| Mistake | Example |
|----------|---------|
| Forgetting to call the function | Defining without executing |
| Missing `return` | No value returned |
| Using global variables unnecessarily | Poor encapsulation |
| Too many parameters | Difficult-to-use functions |
| Long, complex functions | Hard to maintain |

Keeping functions focused on a single responsibility improves readability.

---

## Best Practices

When writing functions:

- Give each function one clear purpose.
- Prefer local functions.
- Use descriptive function names.
- Keep functions short.
- Return values instead of modifying globals.
- Document complex functions with comments.
- Reuse functions instead of duplicating code.

Well-designed functions are easier to test, debug, and maintain.

---

## Chapter Summary

Functions are reusable blocks of code that improve organization, readability, and maintainability.

Lua functions support parameters, return values, multiple return values, recursion, and first-class function behavior, making them both simple and highly flexible.

Because every NSE script depends on functions—especially the `action()` function—mastering this concept is a critical step toward writing professional Nmap scripts.

---

# Next Chapter

## Chapter 28 — Tables