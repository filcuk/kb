---
title: Statistics
description: 
published: true
date: 2024-12-20T11:58:11.224Z
tags: 
editor: markdown
dateCreated: 2024-12-20T11:58:11.224Z
---

### Count distinct records
Total:
### Example {.tabset}
#### T-SQL
```sql
SELECT COUNT(*) 
FROM (
	SELECT DISTINCT column1, column2
	FROM 	table1
  WHERE condition
  ) as dt1
```
### End {.tabset}

By category:
### Example {.tabset}
#### T-SQL
```sql
SELECT category, COUNT(*) 
FROM table1
WHERE condition
GROUP BY category
```
### End {.tabset}