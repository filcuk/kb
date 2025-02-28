---
title: Power Query M
description: 
published: true
date: 2025-02-28T13:04:59.098Z
tags: 
editor: markdown
dateCreated: 2025-02-28T13:04:59.098Z
---

# Basics
## Refering to records
```powerquery
Table = #table({"Column1", "Column2"}, {{"Betty", 90.3}, {"Carl", 89.5}})
Betty = Table[Column1]{0}
```