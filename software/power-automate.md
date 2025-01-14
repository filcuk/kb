---
title: Power Automate
description: SaaS platform by Microsoft for optimizing and automating workflows and business processes
published: true
date: 2025-01-14T15:13:35.994Z
tags: saas, ms-power-automate, wdl
editor: markdown
dateCreated: 2025-01-14T14:19:58.918Z
---

# About
Power Automate uses [Workflow Definition Language](https://learn.microsoft.com/en-us/azure/logic-apps/logic-apps-workflow-definition-language) (WDL), same as Azure Logic Apps.

# Usage
## Tracked properties
Tracked properties are not shown in dynamic values and have to be retrieved explicitely:
```
actions('Compose')?['TrackedProperties/startAt']
```
![power-automate-tracked-properties.png](/software/power-automate/power-automate-tracked-properties.png)

## Date & time
> Power Automate doesn't provide many built-in options for date/time parsing or duration handling.
> Many solutions will involve manipulating the values as strings to get the output desired.
{.is-info}
### Conversion
#### dd-mm-yyyy to yyyy-mm-dd
```wdl
concat(
	split(outputs('Compose_Date'),'-')[2]
	,'-'
	,split(outputs('Compose_Date'),'-')[1]
	,'-'
	,split(outputs('Compose_Date'),'-')[0]
)
```
## Duration
#### Duration between initial timestamp and now
```wdl
dateDifference(
	outputs('Timestamp')
  ,utcNow()
)
```
### Conversion
#### Timestamp diff to duration in seconds with 2 decimals
This assumes that `outputs('Diff')` contains a result of `dateDifference()`, which looks something like `01:17:05.2001589`.

- Duration is split into individual parts
- Hours & minutes are converted to seconds, then added together
- Miliseconds are rounded and added to the end

```wdl
concat(
  add(add(
    mul(mul(int(
      split(split(
        outputs('Diff')
      ,'.')[0]
      ,':')[0]
    ),24),60)

    ,mul(int(
      split(split(
        outputs('Diff')
      ,'.')[0]
      ,':')[1]
    ),60)
  )
  ,int(
    split(split(
      outputs('Diff')
    ,'.')[0]
    ,':')[2]
  ))
  ,'.'
  ,formatNumber(
    split(
      outputs('Diff')
    ,'.')[1]
    ,'#0.00'
  )
  ,' sec'
)
```
## Numbers
#### Rounding
`formatNumber()` is enough to round the number, but it returns a string, so optional `int()` is used to return a number.
```wdl
int(formatNumber(variables('Number'),'#0'))
decimal(formatNumber(variables('Number'),'#0.00'))
```
#### Rounding to nearest multiple
Assuming that `5` is the desired multiple in this example:
- Divide by the multiplier
- Round and convert to decimal
- Multiply by the multiplier
```wdl
mul(
	decimal(
  	formatNumber(
    	div(
      	variables('Number')
      ,5)
    ,'#0')
  )
,5)
```