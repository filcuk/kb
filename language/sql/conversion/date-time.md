---
title: Date & Time Conversion
description: 
published: true
date: 2024-11-18T14:13:57.196Z
tags: 
editor: markdown
dateCreated: 2024-11-18T13:42:10.849Z
---

# Tab {.tabset}
## T-SQL
```sql
select convert(date, convert(char(8), 20190624))
--> 2019-06-24
select try_convert(date, convert(char(8), 0))
--> null
select try_convert(time, stuff(right('0000' + cast(1530 as varchar), 4), 3, 0, ':'))
--> 15:30:00.0000000
```
> `try_convert()` is available as of MS SQL Server 2012
{.is-info}
# {.tabset}