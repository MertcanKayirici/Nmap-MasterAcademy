# Chapter 40 — Hello NSE

The traditional starting point for learning a new programming language is the **"Hello, World!"** program. Although simple, it introduces the basic structure of a program and demonstrates how different components work together.

In the context of the Nmap Scripting Engine (NSE), a "Hello NSE" script serves the same purpose. Rather than performing network enumeration or vulnerability detection, it allows us to understand the anatomy of an NSE script and the execution flow used by Nmap.

In this lab, we will build a minimal but fully functional NSE script and analyze every line in detail.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Create a valid `.nse` file.
- Understand every required section of an NSE script.
- Execute the script using Nmap.
- Interpret the output.
- Modify the script to display dynamic information.
- Understand the execution lifecycle of an NSE script.

---

# Lab Environment

Required software:

- Nmap
- Visual Studio Code
- Terminal
- Local development workspace from Chapter 39

Recommended target:

```text
scanme.nmap.org
```

or

```text
127.0.0.1
```

---

# Understanding the Structure

Every NSE script contains several logical sections.

```text
Metadata
    │
    ▼
Rule Function
    │
    ▼
Action Function
    │
    ▼
Output
```

Even large official scripts follow this same structure.

---

# Step 1 — Create the Script

Create a file named:

```text
hello.nse
```

inside your workspace.

Example:

```text
NSE-Lab/

└── scripts/

    └── hello.nse
```

---

# Step 2 — Add Script Metadata

Insert the following code:

```lua
description = [[
Simple Hello NSE script.
]]

author = "Your Name"

license = "Same as Nmap"

categories = {"safe"}
```

---

## Understanding the Metadata

### Description

```lua
description = [[
Simple Hello NSE script.
]]
```

The description tells users what the script does.

Official NSE scripts always include a meaningful description.

---

### Author

```lua
author = "Your Name"
```

Specifies who created the script.

---

### License

```lua
license = "Same as Nmap"
```

Indicates the licensing terms.

---

### Categories

```lua
categories = {"safe"}
```

The category determines where the script belongs within the NSE ecosystem.

Since this script performs no intrusive actions, the `safe` category is appropriate.

---

# Step 3 — Add the Rule Function

Now define a rule.

```lua
hostrule = function(host)

    return true

end
```

---

## Understanding the Rule

The rule answers one question:

> **Should this script run?**

Because we return:

```lua
true
```

the answer is always yes.

Execution flow:

```text
Host Found

↓

Evaluate Rule

↓

true

↓

Execute Script
```

---

# Step 4 — Add the action() Function

```lua
action = function(host)

    return "Hello from NSE!"

end
```

This function performs the work of the script.

Here, it simply returns a string.

---

# Complete Script

```lua
description = [[
Simple Hello NSE script.
]]

author = "Your Name"

license = "Same as Nmap"

categories = {"safe"}

hostrule = function(host)

    return true

end

action = function(host)

    return "Hello from NSE!"

end
```

This is a complete, valid NSE script.

---

# Running the Script

Execute:

```bash
nmap --script ./scripts/hello.nse scanme.nmap.org
```

Execution process:

```text
Load Script

↓

Read Metadata

↓

Evaluate Rule

↓

Run action()

↓

Display Output
```

---

# Expected Output

Example:

```text
Starting Nmap

...

| hello:
|   Hello from NSE!
|_

Nmap done.
```

The returned string becomes the script's output.

---

# Modifying the Output

Instead of returning a fixed message:

```lua
return "Hello from NSE!"
```

return the target IP.

```lua
return "Scanning: " .. host.ip
```

Possible output:

```text
Scanning: 45.33.32.156
```

The script is now dynamic.

---

# Using the Hostname

Some targets have a hostname.

```lua
action = function(host)

    if host.name then

        return host.name

    end

    return host.ip

end
```

Possible output:

```text
scanme.nmap.org
```

---

# Returning Multiple Lines

Output may contain multiple lines.

Example:

```lua
action = function(host)

    return
        "Hello NSE\n" ..
        "Target: " .. host.ip

end
```

Example output:

```text
Hello NSE

Target: 192.168.1.20
```

---

# Adding Debug Messages

Import:

```lua
local stdnse = require("stdnse")
```

Use:

```lua
stdnse.debug(1, "Action function started.")
```

Run:

```bash
nmap -d --script ./scripts/hello.nse scanme.nmap.org
```

Debug messages appear only when debugging is enabled.

---

# Experiment 1

Modify:

```lua
return "Hello NSE!"
```

to:

```lua
return "Welcome to the Nmap Scripting Engine."
```

Observe the new output.

---

# Experiment 2

Display both hostname and IP.

```lua
action = function(host)

    return

        "Host: " ..

        (host.name or "Unknown")

        ..

        "\nIP: "

        ..

        host.ip

end
```

Expected output:

```text
Host: scanme.nmap.org

IP: 45.33.32.156
```

---

# Experiment 3

Print a timestamp.

```lua
action = function(host)

    return os.date()

end
```

Each execution displays the current system time.

---

# Understanding the Execution Lifecycle

Every execution follows the same sequence.

```text
Nmap

↓

Load hello.nse

↓

Read Metadata

↓

Evaluate hostrule()

↓

hostrule returns true

↓

Call action()

↓

Return String

↓

Display Output
```

This lifecycle applies to every NSE script, regardless of complexity.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Missing `action()` | Script has nothing to execute |
| Missing rule function | Script is never selected |
| Returning `nil` | No output is produced |
| Syntax errors | Script fails to load |
| Saving with `.lua` instead of `.nse` | Nmap does not recognize the file |

---

# Best Practices

When writing simple NSE scripts:

- Start with the smallest possible example.
- Test after every change.
- Use meaningful descriptions.
- Keep output concise and informative.
- Follow the same structure used by official scripts.
- Add complexity gradually.

---

# Lab Challenge

Complete the following tasks:

1. Create `hello.nse`.
2. Execute it successfully.
3. Display the target IP.
4. Display the hostname.
5. Print the current date.
6. Add a debug message.
7. Verify the debug output using `-d`.
8. Return a multi-line message.
9. Change the category to another valid category and observe the effect.
10. Commit your script to Git.

---

# What You Learned

After completing this lab, you should understand:

- The anatomy of an NSE script.
- The purpose of metadata.
- How `hostrule()` controls execution.
- The role of `action()`.
- How returned values become Nmap output.
- How to execute local scripts.
- How to modify and test scripts safely.

These concepts form the foundation for every advanced NSE script you will build.

---

## Chapter Summary

In this lab, you created your first fully functional NSE script and examined each of its components in detail. Although the script simply displayed a message, it demonstrated the complete execution lifecycle used by every NSE script: loading metadata, evaluating rule functions, executing `action()`, and presenting formatted output.

This small exercise establishes the foundation for more advanced scripting techniques. In the next chapter, you will begin working with the `host` object to access real information about scanned systems, such as IP addresses, hostnames, and other metadata collected by Nmap.

---

# Next Chapter

## Chapter 41 — Host Information