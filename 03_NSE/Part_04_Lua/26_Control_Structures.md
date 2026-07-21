# Chapter 26 — Control Structures

Programs become useful when they can make decisions and repeat tasks. These capabilities are provided through **control structures**, which determine the order in which code is executed.

In Lua, control structures are intentionally simple and easy to read. Instead of using braces (`{}`) like C or Java, Lua uses keywords such as `then`, `do`, and `end` to define code blocks.

Control structures are heavily used in NSE scripts to evaluate scan results, process hosts and ports, repeat protocol operations, and handle different network conditions.

---

## What Are Control Structures?

A control structure changes the normal top-to-bottom execution of a program.

Without control structures:

```text
Statement 1
Statement 2
Statement 3
Statement 4
```

With control structures:

```text
Condition
    │
 ┌──┴──┐
 │     │
True  False
 │     │
 ▼     ▼
Code A Code B
```

They allow programs to:

- Make decisions
- Repeat actions
- Skip code
- Exit loops
- Handle different situations

---

# The if Statement

The simplest control structure is the `if` statement.

Syntax:

```lua
if condition then
    -- code
end
```

Example:

```lua
local port = 80

if port == 80 then
    print("HTTP service detected.")
end
```

Output:

```text
HTTP service detected.
```

The code inside the block executes only if the condition is true.

---

# if...else

When two possible outcomes exist, use `else`.

```lua
local port = 22

if port == 80 then
    print("HTTP")
else
    print("Not HTTP")
end
```

Output:

```text
Not HTTP
```

---

# if...elseif...else

Lua supports multiple conditions.

```lua
local port = 443

if port == 22 then
    print("SSH")

elseif port == 80 then
    print("HTTP")

elseif port == 443 then
    print("HTTPS")

else
    print("Unknown Service")
end
```

Output:

```text
HTTPS
```

This structure is common in NSE scripts when handling different protocols.

---

# Nested if Statements

An `if` statement may contain another `if`.

Example:

```lua
local port = 443
local ssl = true

if port == 443 then

    if ssl then
        print("HTTPS")
    end

end
```

Output:

```text
HTTPS
```

Although nesting is supported, excessive nesting reduces readability.

---

# while Loop

The `while` loop repeats code while a condition remains true.

Syntax:

```lua
while condition do
    -- code
end
```

Example:

```lua
local count = 1

while count <= 5 do

    print(count)

    count = count + 1

end
```

Output:

```text
1
2
3
4
5
```

---

# repeat...until Loop

Unlike `while`, the `repeat` loop always executes at least once.

Syntax:

```lua
repeat

    -- code

until condition
```

Example:

```lua
local count = 1

repeat

    print(count)

    count = count + 1

until count > 5
```

Output:

```text
1
2
3
4
5
```

This loop is useful when at least one execution is required.

---

# Numeric for Loop

Numeric loops count through a range.

Syntax:

```lua
for variable = start, finish do
    -- code
end
```

Example:

```lua
for port = 20,25 do

    print(port)

end
```

Output:

```text
20
21
22
23
24
25
```

---

## Step Values

A third value specifies the increment.

Example:

```lua
for number = 0,10,2 do

    print(number)

end
```

Output:

```text
0
2
4
6
8
10
```

---

# Generic for Loop

The generic `for` loop iterates through collections.

Example:

```lua
local ports = {22,80,443}

for index, port in ipairs(ports) do

    print(index, port)

end
```

Output:

```text
1   22
2   80
3   443
```

This is one of the most frequently used loops in NSE scripts.

---

# The break Statement

`break` immediately exits a loop.

Example:

```lua
for i = 1,10 do

    if i == 5 then
        break
    end

    print(i)

end
```

Output:

```text
1
2
3
4
```

---

# Looping Through Tables

Tables are commonly processed using loops.

Example:

```lua
local services = {

    "HTTP",
    "SSH",
    "FTP"

}

for _, service in ipairs(services) do

    print(service)

end
```

Output:

```text
HTTP
SSH
FTP
```

This pattern appears throughout official NSE scripts.

---

# Practical NSE Example

Imagine a script that processes discovered ports.

```lua
local ports = {22,80,443}

for _, port in ipairs(ports) do

    if port == 443 then

        print("HTTPS detected")

    end

end
```

Output:

```text
HTTPS detected
```

The loop examines each port and performs an action when a specific value is found.

---

# Choosing the Right Control Structure

| Structure | Best Use |
|-----------|----------|
| `if` | Single decision |
| `if...else` | Two possible outcomes |
| `elseif` | Multiple conditions |
| `while` | Unknown number of repetitions |
| `repeat` | Execute at least once |
| `for` | Known number of iterations |
| Generic `for` | Iterate through tables |

Selecting the appropriate structure improves readability and efficiency.

---

# Common Beginner Mistakes

| Mistake | Example |
|----------|---------|
| Forgetting `end` | Unclosed block |
| Infinite `while` loop | Condition never changes |
| Incorrect loop bounds | Missing or extra iterations |
| Excessive nesting | Difficult-to-read code |
| Forgetting `break` when needed | Unnecessary iterations |

Carefully reviewing loop conditions helps prevent logical errors.

---

# Best Practices

When using control structures:

- Keep conditions simple.
- Avoid deeply nested blocks.
- Prefer `for` loops when the iteration count is known.
- Use meaningful variable names.
- Exit loops early with `break` when appropriate.
- Format blocks consistently using indentation.

Readable control flow makes debugging significantly easier.

---

## Chapter Summary

Control structures allow Lua programs to make decisions and repeat tasks efficiently.

By understanding conditional statements, loops, and flow-control mechanisms, you can build programs that react intelligently to different situations. These constructs form the backbone of every NSE script, enabling developers to process scan results, iterate through hosts and ports, and implement complex scanning logic.

With control structures complete, the next chapter introduces **functions**, one of the most powerful features of Lua and a fundamental building block of every NSE script.

---

# Next Chapter

## Chapter 27 — Functions