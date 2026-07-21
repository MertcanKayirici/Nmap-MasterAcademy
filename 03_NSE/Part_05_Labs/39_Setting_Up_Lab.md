# Chapter 39 — Setting Up the Lab

Before writing real NSE scripts, it is important to prepare a proper development environment. While simple scripts can be created with any text editor, professional NSE development requires a structured workspace, suitable test targets, and an efficient workflow.

In this chapter, you will build a complete NSE laboratory that will be used throughout the remainder of this book.

The goal is to create an environment where scripts can be written, tested, debugged, and improved safely without affecting production systems.

---

# Learning Objectives

By the end of this lab, you will be able to:

- Install and verify Nmap.
- Locate the NSE script directory.
- Understand the structure of the Nmap scripts folder.
- Create custom `.nse` scripts.
- Execute local scripts.
- Update the NSE script database.
- Configure Visual Studio Code for Lua development.
- Prepare vulnerable virtual machines for testing.
- Build a reusable laboratory for future chapters.

---

# Lab Requirements

Minimum software:

| Software | Purpose |
|----------|----------|
| Nmap | Script execution |
| Visual Studio Code | Code editor |
| Lua Extension | Syntax highlighting |
| Terminal | Running Nmap |
| Virtual Machine | Safe testing |

Recommended operating systems:

- Kali Linux
- Ubuntu
- Debian
- Windows
- macOS

---

# Installing Nmap

Verify the installation.

Linux:

```bash
nmap --version
```

Windows (PowerShell):

```powershell
nmap --version
```

Expected output:

```text
Nmap version 7.xx
Compiled with Lua
Compiled with OpenSSL
Compiled with libpcap
```

If Lua support is missing, NSE will not function correctly.

---

# Finding the Script Directory

Most Linux installations store NSE scripts here:

```text
/usr/share/nmap/scripts/
```

Example:

```bash
ls /usr/share/nmap/scripts
```

Example output:

```text
http-title.nse
ftp-anon.nse
ssl-cert.nse
ssh-hostkey.nse
...
```

Hundreds of official scripts are included with Nmap.

---

# Understanding the Directory

The directory contains:

```text
scripts/

│

├── ftp-anon.nse
├── http-title.nse
├── smb-os-discovery.nse
├── ssl-cert.nse
├── ssh-hostkey.nse
└── ...
```

Each file is a standalone Lua script executed by the Nmap Scripting Engine.

---

# Creating a Workspace

Instead of modifying the official scripts, create a personal development folder.

Example:

```text
NSE-Lab/

├── scripts/
├── notes/
├── examples/
├── outputs/
└── README.md
```

Keeping custom scripts separate makes updates and maintenance easier.

---

# Creating Your First Script

Inside the `scripts` directory:

```text
scripts/

└── hello.nse
```

Example content:

```lua
description = [[
My first lab script.
]]

author = "Your Name"

license = "Same as Nmap"

categories = {"safe"}

hostrule = function()

    return true

end

action = function()

    return "Hello NSE!"

end
```

---

# Running a Local Script

Move into the project directory.

Example:

```bash
cd NSE-Lab
```

Run:

```bash
nmap --script ./scripts/hello.nse scanme.nmap.org
```

Expected output:

```text
| hello:
|   Hello NSE!
|_
```

Congratulations!

You have executed your first custom NSE script.

---

# Updating the Script Database

If scripts are copied into the official scripts directory:

```bash
sudo cp hello.nse /usr/share/nmap/scripts/
```

Update the database.

```bash
sudo nmap --script-updatedb
```

Nmap scans every `.nse` file and rebuilds its script database.

Workflow:

```text
New Script

↓

Copy

↓

Run --script-updatedb

↓

Script Available
```

---

# Executing by Name

After updating the database:

```bash
nmap --script hello scanme.nmap.org
```

instead of

```bash
nmap --script ./scripts/hello.nse
```

---

# Visual Studio Code Setup

Recommended extensions:

- Lua
- Lua Language Server
- Markdown All in One
- Error Lens
- GitLens

These extensions improve productivity while developing NSE scripts.

---

# Recommended Workspace

```text
NSE-Lab/

├── scripts/
├── libraries/
├── examples/
├── screenshots/
├── outputs/
├── notes/
└── README.md
```

As your projects grow, organizing files becomes increasingly important.

---

# Recommended Test Targets

Avoid testing against random Internet hosts.

Instead, use intentionally vulnerable machines.

Examples:

| Target | Purpose |
|---------|----------|
| Metasploitable 2 | Linux services |
| Metasploitable 3 | Enterprise services |
| OWASP Broken Web Apps | Web testing |
| DVWA | Web vulnerabilities |
| Localhost | Safe experimentation |

These systems are designed specifically for security training.

---

# Using Virtual Machines

A common laboratory setup:

```text
Host Computer

│

├── Kali Linux

├── Metasploitable

├── Windows VM

└── DVWA
```

All machines communicate inside an isolated virtual network.

---

# Example Network

```text
192.168.56.10

↓

Kali Linux

↓

192.168.56.20

↓

Metasploitable

↓

192.168.56.30

↓

DVWA
```

Using private IP addresses prevents accidental scans of public systems.

---

# Testing Connectivity

Before running scripts:

```bash
ping 192.168.56.20
```

Then:

```bash
nmap 192.168.56.20
```

Verify that the target is reachable.

---

# Enabling Debugging

Useful during development:

```bash
nmap -d
```

or

```bash
nmap -d2
```

or

```bash
nmap -v -d
```

Debugging output simplifies troubleshooting.

---

# Organizing Script Versions

Instead of overwriting files:

```text
hello_v1.nse

hello_v2.nse

hello_v3.nse
```

or use Git:

```bash
git init
```

Version control is strongly recommended for professional development.

---

# Keeping Notes

Document your experiments.

Example:

```text
notes/

├── HTTP.md
├── FTP.md
├── SMB.md
└── Bugs.md
```

Good documentation accelerates future development.

---

# Typical Development Workflow

```text
Write Script

↓

Run Nmap

↓

Observe Output

↓

Debug

↓

Modify Code

↓

Test Again

↓

Commit Changes
```

This cycle will be repeated throughout the remaining labs.

---

# Common Beginner Mistakes

| Mistake | Explanation |
|----------|-------------|
| Editing official scripts directly | Updates may overwrite changes |
| Forgetting `--script-updatedb` | Nmap cannot find new scripts |
| Testing against production systems | Unsafe and unethical |
| Ignoring debug output | Harder to diagnose issues |
| Working without version control | Difficult to recover previous changes |

Avoiding these mistakes creates a safer and more productive workflow.

---

# Best Practices

When preparing your NSE laboratory:

- Keep custom scripts in a dedicated workspace.
- Use Git for version control.
- Test against virtual machines.
- Keep detailed notes.
- Update the script database when necessary.
- Enable debugging while developing.
- Organize scripts by purpose.
- Never test unauthorized systems.

These habits will save time throughout the rest of the book.

---

# Lab Challenge

Complete the following tasks:

1. Install Nmap.
2. Verify Lua support.
3. Locate the official scripts directory.
4. Create an `NSE-Lab` workspace.
5. Write the `hello.nse` script.
6. Execute it successfully.
7. Update the script database.
8. Run the script by name.
9. Initialize a Git repository.
10. Record your observations in a Markdown file.

If all tasks are completed successfully, your laboratory is ready for the remaining chapters.

---

## Chapter Summary

In this lab, you created a professional development environment for NSE scripting. You installed and verified Nmap, explored the official scripts directory, created a personal workspace, executed your first custom script, configured debugging tools, and prepared virtual machines for safe testing.

With the laboratory complete, you are ready to begin writing increasingly powerful NSE scripts. The next chapter starts with a simple but important exercise: creating and understanding a classic **Hello NSE** script while examining every line of code in detail.

---

# Next Chapter

## Chapter 40 — Hello NSE