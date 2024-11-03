---
title: SQL
description: Structured Query Language
published: true
date: 2024-11-03T21:26:56.908Z
tags: 
editor: markdown
dateCreated: 2024-10-31T22:51:18.475Z
---

# Flavours
There are many 'flavours' of SQL. Some of those include:
- [IBM Db2 *Db2*](t-sql)
- [MS SQL Server (2016+) *T-SQL*](t-sql)
- [MS Access *JET SQL*](jet-sql)
{.links-list}

I will attempt to keep things simple by defining the flavour for each snippet, using 'SQL' for generic code:
### Example {.tabset}
#### SQL
```sql
SELECT *
FROM table1
LIMIT 5;
```
#### T-SQL
```sql
SELECT TOP 5
FROM table1;
```
#### Db2
```sql
SELECT *
FROM table1
FETCH FIRST 5 ROWS;
```