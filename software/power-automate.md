---
title: Power Automate
description: SaaS platform by Microsoft for optimizing and automating workflows and business processes
published: true
date: 2025-01-14T14:35:33.690Z
tags: saas, ms-power-automate
editor: markdown
dateCreated: 2025-01-14T14:19:58.918Z
---

# Usage
## Date & time
### Conversion
#### dd-mm-yyyy to yyyy-mm-dd
```
concat(
	split(outputs('Compose_Date'),'-')[2]
	,'-'
	,split(outputs('Compose_Date'),'-')[1]
	,'-'
	,split(outputs('Compose_Date'),'-')[0]
)
```