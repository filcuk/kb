---
title: SQL Server
description: Microsoft SQL Server is a proprietary relational database management system developed by Microsoft.
published: true
date: 2024-11-19T10:33:00.116Z
tags: 
editor: markdown
dateCreated: 2024-11-18T11:59:01.049Z
---

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