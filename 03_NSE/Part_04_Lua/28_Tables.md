# Chapter 28 — Tables

Tables are the most important data structure in Lua. Unlike many programming languages that provide separate structures for arrays, dictionaries, objects, lists, and maps, Lua uses **tables** to represent all of these concepts.

Because of their flexibility, tables are used extensively throughout the Lua language and are fundamental to NSE script development. Nmap itself represents hosts, ports, services, script arguments, protocol headers, and many library objects as tables.

Understanding tables is therefore one of the most significant milestones in learning Lua for NSE scripting.

---

## What Is a Table?

A table is a collection of values organized by **keys**.

Unlike traditional arrays, Lua tables allow values to be accessed using either:

- Numeric keys
- String keys
- Other Lua values (with some restrictions)

Conceptually:

```text
+-----------------------+
| Key      | Value      |
+-----------------------+
| 1        | HTTP       |
| 2        | SSH        |
| 3        | HTTPS      |
+-----------------------+
```

Or:

```text
+-----------------------+
| Key      | Value      |
+-----------------------+
| host     | scanme     |
| port     | 80         |
| state    | open       |
+-----------------------+
```

---

# Creating Tables

The simplest table is empty.

```lua
local ports = {}
```

This creates an empty table ready to store data.

---

## Array-Style Tables

Tables often behave like arrays.

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

---

## Lua Starts at Index 1

Unlike C, Java, Python, or JavaScript, Lua arrays begin with index **1**.

```lua
local ports = {22,80,443}
```

```text
Index 1 → 22
Index 2 → 80
Index 3 → 443
```

This is one of the most common surprises for new Lua programmers.

---

## Accessing Elements

Retrieve values using square brackets.

```lua
local ports = {22,80,443}

print(ports[2])
```

Output:

```text
80
```

---

## Modifying Elements

Existing values may be changed.

```lua
local ports = {22,80,443}

ports[2] = 8080

print(ports[2])
```

Output:

```text
8080
```

---

## Adding New Elements

Assign a value to a new index.

```lua
local ports = {22,80}

ports[3] = 443
```

The table now contains:

```text
22
80
443
```

---

# Key-Value Tables

Tables can also store named fields.

Example:

```lua
local server = {

    host = "scanme.nmap.org",
    port = 80,
    service = "http"

}
```

Access values:

```lua
print(server.host)
```

Output:

```text
scanme.nmap.org
```

The following syntax is equivalent:

```lua
print(server["host"])
```

---

## Mixing Keys

Lua allows numeric and named keys in the same table.

```lua
local example = {

    "HTTP",
    "SSH",

    version = "1.0",
    secure = true

}
```

This flexibility makes tables extremely powerful.

---

# Nested Tables

Tables may contain other tables.

Example:

```lua
local host = {

    ip = "192.168.1.10",

    ports = {

        22,
        80,
        443

    }

}
```

Access nested values:

```lua
print(host.ports[2])
```

Output:

```text
80
```

Nested tables are extremely common inside NSE libraries.

---

# Iterating Through Tables

The `ipairs()` function iterates through array-style tables.

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

---

## Using pairs()

For key-value tables, use `pairs()`.

```lua
local server = {

    host = "scanme.nmap.org",
    port = 80,
    ssl = false

}

for key, value in pairs(server) do

    print(key, value)

end
```

Possible output:

```text
host    scanme.nmap.org
port    80
ssl     false
```

Unlike `ipairs()`, the order of iteration is not guaranteed.

---

# Table Length

The length operator returns the number of consecutive numeric elements.

```lua
local ports = {22,80,443}

print(#ports)
```

Output:

```text
3
```

Note that `#` is reliable only for sequential numeric indices.

---

# Removing Elements

Lua provides `table.remove()`.

Example:

```lua
local ports = {22,80,443}

table.remove(ports, 2)
```

Result:

```text
22
443
```

Remaining indices are automatically adjusted.

---

# Inserting Elements

Use `table.insert()`.

Example:

```lua
local ports = {22,443}

table.insert(ports, 2, 80)
```

Result:

```text
22
80
443
```

---

# Common Table Functions

| Function | Purpose |
|----------|---------|
| `table.insert()` | Add an element |
| `table.remove()` | Remove an element |
| `table.sort()` | Sort values |
| `table.concat()` | Join strings |
| `ipairs()` | Iterate arrays |
| `pairs()` | Iterate key-value tables |

These utilities simplify many common tasks.

---

# Practical NSE Example

Suppose an NSE script discovers several open ports.

```lua
local openPorts = {

    22,
    80,
    443,
    8080

}

for _, port in ipairs(openPorts) do

    print("Open:", port)

end
```

Output:

```text
Open: 22
Open: 80
Open: 443
Open: 8080
```

---

## Representing Host Information

Tables naturally represent structured network data.

```lua
local host = {

    ip = "192.168.1.15",
    hostname = "server01",
    os = "Linux",

    ports = {

        22,
        80,
        443

    }

}
```

Accessing values:

```lua
print(host.hostname)
```

```lua
print(host.ports[3])
```

Output:

```text
server01
443
```

This closely resembles how Nmap libraries internally organize information.

---

# Tables in Official NSE Scripts

Most NSE libraries return tables.

Example (conceptual):

```text
Host
│
├── IP Address
├── Hostname
├── Status
├── OS
└── Open Ports
```

Instead of creating dozens of variables, related information is grouped into a single table, making scripts easier to understand and extend.

---

# Common Beginner Mistakes

| Mistake | Example |
|----------|---------|
| Forgetting Lua starts at index 1 | Accessing `table[0]` |
| Using `ipairs()` on key-value tables | Missing entries |
| Assuming `pairs()` has a fixed order | Unpredictable iteration |
| Confusing arrays with key-value tables | Incorrect access |
| Modifying a table during iteration | Unexpected behavior |

Understanding how tables store and organize data helps avoid these issues.

---

# Best Practices

When working with tables:

- Use array-style tables for ordered lists.
- Use key-value tables for structured data.
- Prefer descriptive key names.
- Keep related information together.
- Use `ipairs()` for sequential arrays.
- Use `pairs()` for dictionaries.
- Avoid mixing unrelated data in the same table unless necessary.

Well-designed tables make Lua programs significantly easier to maintain.

---

## Chapter Summary

Tables are Lua's universal data structure, capable of representing arrays, dictionaries, objects, and complex nested data.

Because nearly every NSE library and script relies on tables to organize hosts, ports, services, and protocol information, mastering them is essential for effective NSE development.

With a solid understanding of tables, you are now ready to learn how Lua organizes reusable code through **modules**, allowing scripts to share functionality across multiple files.

---

# Next Chapter

## Chapter 29 — Modules