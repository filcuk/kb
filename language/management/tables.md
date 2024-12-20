---
title: Tables
description: 
published: true
date: 2024-12-20T16:21:36.033Z
tags: 
editor: markdown
dateCreated: 2024-12-20T16:21:00.101Z
---

# Duplicate a table
## Method 1
This method only works if the target table doesn't exist yet.
### Example {.tabset}
#### T-SQL
```sql
SELECT *
  INTO table1_bkp
  FROM table1
```
### End {.tabset}

## Method 2
This method works for existing tables with identical columns.
### Example {.tabset}
#### T-SQL
```sql
INSERT
  INTO table1_bkp
SELECT *
  FROM table1
```
### End {.tabset}

## Method 3
This final method copies the identity, instead of incrementing automatically.
It is necessary to declare individual columns in this case.
### Example {.tabset}
#### T-SQL
```sql
SET IDENTITY_INSERT table1_bkp ON 

INSERT
  INTO table1_bkp
     (
       column1
     , column2
     )
SELECT 
			 column1
     , column2
  FROM table1

SET IDENTITY_INSERT table1_bkp OFF
```
### End {.tabset}