---
title: Date & Time Conversion
description: 
published: true
date: 2024-11-18T13:48:54.622Z
tags: 
editor: markdown
dateCreated: 2024-11-18T13:42:10.849Z
---

# Date
## Tab {.tabset}
### T-SQL
```sql
select convert(date, convert(char(8), 20190624))
--> 2019-06-24
select try_convert(date, convert(char(8), 0))
--> null
```
> `try_convert()` is available as of MS SQL Server 2012
{.is-info}
## {.tabset}