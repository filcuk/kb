---
title: SQL Server
description: Microsoft SQL Server is a proprietary relational database management system developed by Microsoft.
published: true
date: 2024-11-18T11:59:01.049Z
tags: 
editor: markdown
dateCreated: 2024-11-18T11:59:01.049Z
---

# Troubleshooting
## Permissions
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