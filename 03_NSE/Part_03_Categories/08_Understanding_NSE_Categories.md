# Chapter 8 — Understanding NSE Categories

The Nmap Scripting Engine (NSE) includes hundreds of official scripts, each designed to perform a specific task. As the number of available scripts has grown over the years, organizing them into meaningful groups has become essential.

To simplify script selection and improve usability, every official NSE script belongs to one or more **categories**. These categories describe the script's purpose, behavior, and potential impact on the target system.

Rather than memorizing the name of every individual script, users can execute groups of related scripts simply by specifying a category.

For example:

```bash
nmap --script default target
```

executes all scripts that belong to the **default** category.

Similarly,

```bash
nmap --script vuln target
```

runs every script classified as a vulnerability detection script.

Understanding these categories is one of the most important skills for effective use of the Nmap Scripting Engine.

---

## Why Script Categories Exist

The official NSE repository contains hundreds of scripts covering many different protocols, technologies, and security tasks.

Without organization, users would need to remember the name and purpose of every individual script.

Categories solve this problem by grouping scripts according to their intended use.

This approach offers several advantages:

- Easier script discovery
- Simplified command syntax
- Better automation
- Reduced configuration effort
- Consistent script selection

Instead of selecting dozens of scripts manually, users can simply specify a category.

---

## A Script Can Belong to Multiple Categories

One important characteristic of NSE is that a script is **not limited to a single category**.

A single script may serve multiple purposes.

For example:

```lua
categories = {
    "default",
    "safe",
    "discovery"
}
```

This indicates that the script:

- Is included in default scans
- Is considered safe to execute
- Performs information gathering

Because categories overlap, script selection becomes both flexible and efficient.

---

## How Categories Affect Script Execution

Categories do **not** control how a script works internally.

Instead, they determine **which scripts are selected** when a user specifies a category.

For example,

```bash
nmap --script safe target
```

loads every script classified as **safe**.

Likewise,

```bash
nmap --script auth target
```

loads every authentication-related script.

The execution process itself remains unchanged.

Once selected, each script still passes through the normal NSE execution workflow discussed in the previous chapters.

---

## Official NSE Categories

The official Nmap distribution defines several standard categories.

Each category serves a different purpose.

| Category | Purpose |
|-----------|---------|
| default | Scripts executed during `-sC` scans |
| safe | Non-intrusive scripts |
| discovery | Information gathering |
| version | Service version detection |
| auth | Authentication-related checks |
| brute | Password guessing and brute-force attacks |
| vuln | Vulnerability detection |
| exploit | Exploitation scripts |
| intrusive | Scripts that may affect the target |
| malware | Malware detection |
| dos | Denial-of-Service testing |
| external | Uses third-party resources |
| broadcast | Broadcast network discovery |
| fuzzer | Protocol fuzzing |

Each category represents a different stage or objective of a security assessment.

---

## Selecting Scripts by Category

One of the greatest advantages of categories is simplified script selection.

Examples:

Execute all default scripts.

```bash
nmap -sC target
```

Equivalent command:

```bash
nmap --script default target
```

Run all vulnerability scripts.

```bash
nmap --script vuln target
```

Run all discovery scripts.

```bash
nmap --script discovery target
```

Run multiple categories simultaneously.

```bash
nmap --script "default,vuln,safe" target
```

The scripting engine automatically loads every script belonging to the selected categories.

---

## Category Combinations

Categories may be combined using commas.

For example,

```bash
nmap --script "safe,discovery"
```

loads scripts belonging to either category.

Categories can also be excluded.

Example:

```bash
nmap --script "default and not brute"
```

This command executes every default script except those belonging to the brute-force category.

These selection expressions provide a powerful mechanism for customizing scans.

---

## How Scripts Are Classified

Every NSE script contains a category declaration near the beginning of the file.

Example:

```lua
categories = {
    "default",
    "safe",
    "version"
}
```

When Nmap updates its script database, these category definitions are indexed.

Later, when the user specifies a category, the Script Loader consults the database and loads the appropriate scripts.

---

## Choosing the Right Category

The appropriate category depends on the objective of the assessment.

| Objective | Recommended Category |
|-----------|----------------------|
| General reconnaissance | default |
| Information gathering | discovery |
| Service identification | version |
| Password auditing | brute |
| Authentication analysis | auth |
| Vulnerability assessment | vuln |
| Malware investigation | malware |
| Safe production scanning | safe |
| Protocol testing | fuzzer |

Selecting the appropriate category improves both efficiency and scan accuracy.

---

## Best Practices

When working with NSE categories, consider the following recommendations.

- Begin with the **default** category.
- Use **safe** scripts on production systems whenever possible.
- Execute **vuln** scripts only with authorization.
- Use **brute** scripts carefully to avoid account lockouts.
- Read each script's documentation before execution.
- Combine categories only when necessary.
- Keep the script database updated.

Following these practices helps ensure responsible and effective security assessments.

---

## Chapter Summary

NSE categories organize the extensive collection of official scripts into logical groups based on their intended purpose and behavior.

Rather than selecting scripts individually, users can execute entire categories, simplifying automation and improving workflow efficiency.

Because scripts may belong to multiple categories, NSE provides a flexible and scalable mechanism for selecting the most appropriate scripts for a given assessment.

The following chapters examine each major category in detail, beginning with the **default** scripts that form the foundation of most NSE scans.

---

# Next Chapter

## Chapter 9 — Default Scripts