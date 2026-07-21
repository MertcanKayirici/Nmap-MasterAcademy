# Lab 23 — Database Server Assessment

> Perform a structured assessment of database servers using Nmap to identify database technologies, exposed services, and supporting infrastructure.

---

# Overview

Database servers store and manage critical business information.

They commonly support:

- Enterprise Applications
- Web Applications
- ERP Systems
- CRM Platforms
- Analytics Platforms
- Internal Services

Because databases often contain sensitive information, understanding their network exposure is an essential part of infrastructure assessments.

This lab focuses on identifying database services and documenting their characteristics without interacting with stored data.

---

# Learning Objectives

After completing this lab, you will be able to:

- Identify common database services.
- Detect database versions.
- Recognize database technologies.
- Enumerate database-related information using NSE.
- Build a database infrastructure profile.
- Produce a professional assessment report.

---

# Difficulty

⭐⭐⭐⭐☆

---

# Estimated Time

90–120 Minutes

---

# Prerequisites

- Parts 01–03 completed
- Basic understanding of relational databases
- Target containing one or more database services

---

# Lab Environment

| Machine | IP Address | Role |
|----------|------------|------|
| Kali Linux | 192.168.56.10 | Scanner |
| DB01 | 192.168.56.50 | Database Server |

---

# Scenario

A database server has been deployed to support internal business applications.

Your objectives are:

- Identify the database platform.
- Detect exposed database services.
- Determine software versions.
- Collect infrastructure information.
- Produce a technical report.

No authentication attempts or database queries are authorized.

---

# Assessment Workflow

```
Host Discovery

↓

Port Scan

↓

Service Detection

↓

Database Identification

↓

NSE Enumeration

↓

Infrastructure Analysis

↓

Documentation
```

---

# Common Database Ports

| Port | Service |
|------|----------|
| 1433 | Microsoft SQL Server |
| 1434 | SQL Server Browser |
| 1521 | Oracle Database |
| 27017 | MongoDB |
| 3306 | MySQL / MariaDB |
| 5432 | PostgreSQL |
| 6379 | Redis |
| 9042 | Cassandra |

---

# Phase 1 — Verify Connectivity

```bash
ping -c 4 192.168.56.50
```

Record:

- Reachability
- Average latency
- Packet loss

---

# Phase 2 — Initial Scan

```bash
nmap 192.168.56.50
```

Example

```text
3306/tcp open mysql
```

or

```text
5432/tcp open postgresql
```

---

# Phase 3 — Full TCP Scan

```bash
nmap -p- 192.168.56.50
```

Questions:

- Are multiple database services present?
- Are management interfaces exposed?

---

# Phase 4 — Service Detection

```bash
nmap -sV 192.168.56.50
```

Document:

- Product
- Vendor
- Version
- Port

---

# Phase 5 — Database Enumeration

Example for MySQL:

```bash
nmap --script mysql-info -p3306 192.168.56.50
```

Example for PostgreSQL:

```bash
nmap --script pgsql-info -p5432 192.168.56.50
```

Example for Microsoft SQL Server:

```bash
nmap --script ms-sql-info -p1433 192.168.56.50
```

Review:

- Database version
- Server information
- Supported protocol details

---

# Phase 6 — Default NSE Scripts

```bash
nmap -sC -sV 192.168.56.50
```

Document additional information returned by NSE.

---

# Phase 7 — Infrastructure Role Analysis

Based on discovered services:

Example:

```text
3306

8080

22
```

Possible interpretation:

- Application server with local database

---

Another Example

```text
1433

3389
```

Possible interpretation:

- Windows database server

Remember that these are working hypotheses based on observed services and should be confirmed through authorized documentation or administration.

---

# Database Inventory

| Category | Finding |
|----------|----------|
| Database Platform | |
| Version | |
| Port | |
| Operating System | |
| Supporting Services | |
| Notes | |

---

# Common NSE Database Scripts

| Script | Purpose |
|---------|---------|
| mysql-info | MySQL information |
| mysql-variables | Server variables |
| pgsql-info | PostgreSQL information |
| ms-sql-info | Microsoft SQL Server information |
| oracle-tns-version | Oracle listener version |

---

# Decision Tree

```
Database Port Found

↓

Identify Database

↓

Determine Version

↓

Run Relevant NSE Script

↓

Analyze Supporting Services

↓

Document Findings
```

---

# Thinking Like an Analyst

Suppose you discover:

```text
3306

22
```

Questions:

- Is the database dedicated or hosted on an application server?
- Should the database be directly reachable from this network?
- Which applications are likely to use it?

---

Another Example

```text
1433

3389

5985
```

Questions:

- Does this appear to be a Windows-based SQL Server?
- Which remote management services are available?
- Does the observed configuration match the expected server role?

---

# Reporting Template

## Executive Summary

## Scope

## Methodology

## Database Platform

## Service Inventory

## Supporting Infrastructure

## Observations

## Recommendations

---

# Challenge

Perform a complete assessment and document:

- Database software
- Version
- Supporting services
- Operating system estimate
- Infrastructure role
- Final assessment

---

# Bonus Challenge

Create a single Nmap command that performs:

- Service Detection
- OS Detection
- Default NSE Scripts
- Database Enumeration

Save the output as:

```bash
-oA database_assessment
```

---

# Key Takeaways

- Database servers can often be identified through characteristic ports and service banners.
- Database-specific NSE scripts provide valuable infrastructure information.
- Supporting services help determine the role of the host within the environment.
- Database assessments should focus on identification and documentation unless additional authorization is provided.
- A structured workflow enables consistent and repeatable assessments.

---

# Next Lab

➡ **Lab 24 — DMZ Assessment**

In the next lab, you will assess a Demilitarized Zone (DMZ) environment by identifying externally exposed services, documenting network segmentation, and evaluating the roles of publicly accessible systems.