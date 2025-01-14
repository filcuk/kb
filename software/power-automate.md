---
title: Power Automate
description: SaaS platform by Microsoft for optimizing and automating workflows and business processes
published: true
date: 2025-01-14T14:38:22.732Z
tags: saas, ms-power-automate
editor: markdown
dateCreated: 2025-01-14T14:19:58.918Z
---

# Usage
## Date & time
> Power Automate doesn't provide many built-in options for date/time parsing or duration handling.
> Many solutions will involve manipulating the values as strings to get the output desired.
{.is-info}
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