---
title: SQL Server
description: Microsoft SQL Server is a proprietary relational database management system developed by Microsoft.
published: true
date: 2024-12-20T16:08:08.646Z
tags: 
editor: markdown
dateCreated: 2024-11-18T11:59:01.049Z
---

# Record management
### DELETE vs TRUNCATE
`TRUNCATE TABLE` is the recommended way to delete entire table:
- May require fewer locks (typically only a single schema modification lock at a table level)
- Guarantees that all pages are deallocated from a heap table
- Does [minimal logging](https://learn.microsoft.com/en-us/previous-versions/technet-magazine/gg552991(v=msdn.10))
- Can use [deferred drop](https://learn.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms177495(v=sql.105)) (asynchronous deallocation by a background thread)

Source: [dba.stackexchange.com](https://dba.stackexchange.com/a/30347)

# Troubleshooting
## Login
### Unlock an SQL login without resetting the password
1. Temporarily disable 'Enforce password policy'
1. Re-activate account by disabling 'Login is locked out'
1. Re-enable 'Enforce password policy' option

### CHECK_POLICY and CHECK_EXPIRATION options cannot be turned OFF when MUST_CHANGE is ON
The `MUST_CHANGE = ON` indicates that a pending password change is required.
You can use the interface:
1. Change password -> Confirm
1. Re-open → uncheck options → Confirm

Or run the following script to do the same:
```sql
USE Master
GO
ALTER LOGIN UserName WITH PASSWORD = 'Password'
GO
ALTER LOGIN UserName WITH
      CHECK_POLICY = OFF,
      CHECK_EXPIRATION = OFF;
```