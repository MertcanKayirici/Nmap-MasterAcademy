# Chapter 57 — Code Review and Refactoring

Writing an NSE script that works is an important milestone.

Writing an NSE script that is **clean, maintainable, efficient, and easy for others to understand** is what separates a beginner from a professional developer.

As projects grow, scripts often become more complex. Variables accumulate, duplicate code appears, functions become longer, and debugging becomes increasingly difficult.

Code review and refactoring help solve these problems.

In this chapter, you will learn how to review existing NSE scripts, identify weaknesses, improve their structure, and prepare them for long-term maintenance.

---

# Learning Objectives

By the end of this chapter, you will be able to:

- Understand code review principles.
- Recognize common code smells.
- Refactor Lua code safely.
- Improve readability.
- Reduce duplication.
- Organize NSE scripts professionally.
- Prepare scripts for production environments.

---

# What Is Code Review?

Code review is the process of examining source code to improve its:

- Correctness
- Readability
- Performance
- Maintainability
- Security

Professional teams perform code reviews before merging new code into a project.

---

# What Is Refactoring?

Refactoring means improving the internal structure of code **without changing its behavior**.

Example:

Before

```text
Works
↓

Messy
```

After

```text
Works

↓

Clean

↓

Easier to Maintain
```

The functionality remains exactly the same.

---

# Refactoring Goals

A good refactoring process aims to:

- Reduce complexity.
- Eliminate duplicate code.
- Improve naming.
- Increase modularity.
- Simplify logic.
- Improve maintainability.

---

# Example of Poor Code

```lua
action = function(host, port)

local socket =
nmap.new_socket()

socket:set_timeout(5000)

local status =
socket:connect(host, port)

if status then

local ok,data =
socket:receive()

socket:close()

return data

else

socket:close()

return nil

end

end
```

Although functional, this code has several issues.

---

# Problems

The previous example contains:

- Poor indentation.
- Inconsistent spacing.
- Duplicate code.
- No comments.
- Weak variable names.
- No error messages.
- Difficult readability.

Professional code should avoid these issues.

---

# Improved Version

```lua
action = function(host, port)

    local socket =
        nmap.new_socket()

    socket:set_timeout(5000)

    local status =
        socket:connect(host, port)

    if not status then

        socket:close()

        return

        "Connection failed."

    end

    local ok, response =
        socket:receive()

    socket:close()

    if not ok then

        return

        "No response."

    end

    return response

end
```

The behavior is identical, but the code is much easier to understand.

---

# Better Variable Names

Poor:

```lua
local a

local b

local c
```

Better:

```lua
local socket

local response

local banner
```

Good names reduce the need for comments.

---

# Removing Duplicate Code

Poor:

```lua
socket:close()

return

"Failed."
```

appearing several times.

Better:

```lua
local function closeSocket(socket)

    socket:close()

end
```

Centralizing repeated logic improves maintainability.

---

# Breaking Large Functions

Poor:

```text
action()

↓

250 Lines
```

Better:

```text
action()

↓

connect()

↓

receive()

↓

parse()

↓

report()
```

Small functions are easier to test and reuse.

---

# Creating Helper Functions

Example:

```lua
local function receiveBanner(socket)

    local ok, banner =
        socket:receive()

    if not ok then

        return nil

    end

    return banner

end
```

The main function becomes much cleaner.

---

# Organizing the Script

A professional NSE script often follows this layout:

```text
Imports

↓

Constants

↓

Helper Functions

↓

portrule

↓

action()

↓

Return Results
```

A consistent structure makes navigation easier.

---

# Avoid Deep Nesting

Poor:

```text
if

↓

if

↓

if

↓

if

↓

if
```

Better:

```text
Check

↓

Return Early

↓

Continue
```

Returning early reduces nesting and improves readability.

---

# Replace Magic Values

Poor:

```lua
socket:set_timeout(4378)
```

Better:

```lua
local TIMEOUT = 5000

socket:set_timeout(TIMEOUT)
```

Named constants clearly express intent.

---

# Add Meaningful Comments

Poor:

```lua
-- Receive data
```

Better:

```lua
-- Receive the service banner after a successful TCP connection.
```

Comments should explain **why**, not merely **what**.

---

# Improve Output Formatting

Poor:

```text
SSH
22
OpenSSH
```

Better:

```text
Service Information

-------------------

Port      : 22

Protocol  : TCP

Service   : SSH

Product   : OpenSSH
```

Readable output improves the user experience.

---

# Error Handling

Instead of:

```lua
return nil
```

Use:

```lua
return

"Unable to connect to target service."
```

Descriptive errors simplify troubleshooting.

---

# Refactoring Workflow

```text
Existing Script

↓

Review

↓

Identify Problems

↓

Refactor

↓

Test

↓

Compare Results

↓

Release
```

Always verify that the script still behaves correctly after refactoring.

---

# Before and After

Before:

```text
Long Function

Duplicate Code

Poor Names

Minimal Errors
```

After:

```text
Small Functions

Reusable Logic

Clear Names

Helpful Messages
```

The script is easier to maintain without changing its functionality.

---

# Example Project Structure

```text
http-title.nse

│

├── Imports

├── Constants

├── Helper Functions

├── portrule

├── action()

└── Output
```

Consistent organization helps future contributors understand the script quickly.

---

# Review Checklist

Before publishing an NSE script, ask:

- Is the code readable?
- Are variables descriptive?
- Is duplicate code removed?
- Are helper functions used?
- Is error handling complete?
- Is output consistent?
- Are comments meaningful?
- Does the script still work correctly?

---

# Common Code Smells

| Code Smell | Why It Is a Problem |
|------------|---------------------|
| Long functions | Difficult to maintain |
| Duplicate logic | Hard to update consistently |
| Poor variable names | Reduces readability |
| Deep nesting | Makes logic difficult to follow |
| Magic numbers | Hard to understand |
| Inconsistent formatting | Reduces maintainability |

---

# Best Practices

When reviewing NSE scripts:

- Keep functions small.
- Choose descriptive names.
- Remove duplicate code.
- Return early when possible.
- Separate logic into helper functions.
- Handle every error condition.
- Keep formatting consistent.
- Test after every refactoring.

---

# Lab Challenge

Complete the following tasks:

1. Select one of your previous NSE scripts.
2. Improve its formatting.
3. Rename unclear variables.
4. Remove duplicated logic.
5. Create at least two helper functions.
6. Replace magic values with constants.
7. Improve error handling.
8. Add meaningful comments.
9. Test the refactored script.
10. Verify that the output matches the original behavior.

---

# What You Learned

After completing this chapter, you should understand:

- Why code reviews are important.
- How to identify common code smells.
- How to refactor Lua code safely.
- How to improve readability.
- How helper functions simplify maintenance.
- Why clean code is essential for long-term projects.

Professional NSE development is not only about writing scripts that work—it is also about writing scripts that others can understand, maintain, and extend.

---

## Chapter Summary

In this chapter, you learned how to transform functional NSE scripts into clean, maintainable, production-quality code. By improving naming, reducing duplication, introducing helper functions, simplifying control flow, and organizing code consistently, you created scripts that are easier to debug, review, and extend.

Code review and refactoring are ongoing processes rather than one-time activities. Every improvement made today reduces future maintenance costs and increases the reliability of your tools.

The next chapter brings together everything you have learned throughout this part. You will design and implement a complete **Final Project**, integrating host discovery, service enumeration, HTTP requests, banner analysis, vulnerability checks, error handling, and professional reporting into a single comprehensive NSE script.

---

# Next Chapter

## Chapter 58 — Final Project