# Chapter 23 — Lua Syntax

Before writing NSE scripts, it is important to understand the basic syntax of the Lua programming language.

One of Lua's greatest strengths is its simplicity. The language contains relatively few keywords and follows a clean, readable syntax. This makes it easy to learn while remaining powerful enough to build complex network automation scripts.

This chapter introduces the core syntax that will be used throughout the remainder of this book.

---

## Your First Lua Program

Traditionally, the first program prints a message to the screen.

```lua
print("Hello, World!")
```

Output:

```text
Hello, World!
```

The `print()` function displays text in the console.

---

## Statements

A Lua program consists of one or more **statements**.

Example:

```lua
print("Nmap")
print("Lua")
print("NSE")
```

Output:

```text
Nmap
Lua
NSE
```

Each statement executes from top to bottom.

---

## Case Sensitivity

Lua is **case-sensitive**.

These variables are different.

```lua
Name
name
NAME
```

Example:

```lua
local name = "Alice"

print(name)
```

This works correctly.

However,

```lua
print(Name)
```

will not produce the expected result because `Name` and `name` are different identifiers.

---

## Comments

Comments improve readability and are ignored by the interpreter.

### Single-line Comment

```lua
-- This is a comment
```

Example:

```lua
-- Print a greeting

print("Hello")
```

---

### Multi-line Comment

```lua
--[[

This
is
a
multi-line
comment.

]]
```

These are useful for documenting larger sections of code.

---

## Blocks

Lua groups related statements into **blocks**.

Example:

```lua
if true then
    print("Condition met")
end
```

Notice the use of the `end` keyword.

Unlike languages that use braces (`{}`), Lua uses keywords to close blocks.

---

## Whitespace

Lua ignores extra spaces and blank lines.

These programs are equivalent.

```lua
print("Hello")
print("Lua")
```

```lua
print("Hello")



print("Lua")
```

However, proper formatting greatly improves readability.

---

## Semicolons

Semicolons are optional.

Both examples are valid.

```lua
print("Hello")
print("Lua")
```

```lua
print("Hello");
print("Lua");
```

Most Lua developers omit semicolons.

---

## Strings

Strings may use either double quotes or single quotes.

```lua
print("Lua")
```

```lua
print('Lua')
```

Both produce:

```text
Lua
```

Choose one style and use it consistently.

---

## Escaping Characters

Special characters use escape sequences.

Example:

```lua
print("Line 1\nLine 2")
```

Output:

```text
Line 1
Line 2
```

Common escape sequences:

| Escape | Meaning |
|---------|---------|
| `\n` | New line |
| `\t` | Tab |
| `\\` | Backslash |
| `\"` | Double quote |
| `\'` | Single quote |

---

## Multiple Statements on One Line

Although possible, it is generally discouraged.

```lua
print("One"); print("Two")
```

Prefer:

```lua
print("One")
print("Two")
```

This improves readability.

---

## Keywords

Lua reserves certain words for the language itself.

Examples include:

```text
and
break
do
else
elseif
end
false
for
function
if
in
local
nil
not
or
repeat
return
then
true
until
while
```

Reserved keywords cannot be used as variable names.

Incorrect:

```lua
local end = 10
```

Correct:

```lua
local ending = 10
```

---

## Identifiers

Identifiers are names assigned to variables, functions, and tables.

Valid examples:

```lua
host
port
username
password
scanResult
```

Invalid examples:

```text
123host
my-variable
local
```

Good identifiers should clearly describe their purpose.

---

## Code Formatting

Readable code is easier to debug and maintain.

Poor formatting:

```lua
if true then print("Hello")end
```

Better formatting:

```lua
if true then
    print("Hello")
end
```

Consistent formatting is especially important when developing larger NSE scripts.

---

## Lua Syntax vs C-Style Languages

Developers coming from C, Java, JavaScript, or C# will notice several differences.

| Lua | C-style Languages |
|------|-------------------|
| Uses `end` | Uses `{}` |
| No semicolon required | Semicolon required |
| Simple syntax | More complex grammar |
| Minimal keywords | Larger keyword set |
| Lightweight | Larger language specification |

These design choices contribute to Lua's simplicity.

---

## Common Beginner Mistakes

New Lua programmers frequently encounter the following issues:

| Mistake | Example |
|----------|---------|
| Missing `end` | Unclosed block |
| Incorrect capitalization | `Print()` instead of `print()` |
| Using reserved keywords | `local function = 1` |
| Forgetting quotes | `print(Hello)` |
| Poor indentation | Difficult-to-read code |

Most syntax errors are easy to identify once you become familiar with Lua's structure.

---

## Best Practices

When writing Lua code:

- Use meaningful variable names.
- Indent nested blocks consistently.
- Write one statement per line.
- Add comments where appropriate.
- Avoid unnecessary complexity.
- Follow a consistent coding style.

Good formatting makes scripts easier to understand and maintain.

---

## Chapter Summary

Lua's syntax is intentionally simple, making it an excellent language for automation and scripting.

By understanding statements, comments, blocks, identifiers, keywords, and formatting conventions, you now have the foundation needed to begin writing real Lua programs.

These basic syntax rules will be used throughout every remaining chapter and every NSE script developed in this book.

---

# Next Chapter

## Chapter 24 — Variables and Data Types