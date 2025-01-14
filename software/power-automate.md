---
title: Power Automate
description: SaaS platform by Microsoft for optimizing and automating workflows and business processes
published: true
date: 2025-01-14T16:35:05.008Z
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
# Special
#### Test against crontab-style schedule
**Now**: compose an array of current date/time values:
```wdl
[
  @{int(formatDateTime(utcNow(), 'mm'))},
  @{int(formatDateTime(utcNow(), 'HH'))},
  @{int(formatDateTime(utcNow(), 'dd'))},
  @{int(formatDateTime(utcNow(), 'MM'))},
  @{int(replace(string(dayOfWeek(utcNow())), '7', '0'))}
]
```
**Input**: we're using a compose `Schedule` that contains a crontab string and split that into an array:
```wdl
[
  "@{split(outputs('Schedule'), ' ')?[0]}",
  "@{split(outputs('Schedule'), ' ')?[1]}",
  "@{split(outputs('Schedule'), ' ')?[2]}",
  "@{split(outputs('Schedule'), ' ')?[3]}",
  "@{split(outputs('Schedule'), ' ')?[4]}"
]
```
**Output**: lets compare the two arrays:
> Below implementation supports operators `*`, `,` and `-`.
> Operator `/` is not supported.
{.is-warning}
```wdl
[
  @{if(
    equals(outputs('Input')?[0], '*'),
    true,
if(
    isInt(outputs('Input')?[0]),
    equals(int(outputs('Input')?[0]), outputs('Now')?[0]),
if(
    contains(outputs('Input')?[0], ','),
    contains(split(outputs('Input')?[0], ','), string(outputs('Now')?[0])),
if(
    contains(outputs('Input')?[0], '-'),
    contains(range(int(split(outputs('Input')?[0], '-')[0]), int(split(outputs('Input')?[0], '-')[1])), outputs('Now')?[0]),
    false
))))},
  @{if(
    equals(outputs('Input')?[1], '*'),
    true,
if(
    isInt(outputs('Input')?[1]),
    equals(int(outputs('Input')?[1]), outputs('Now')?[1]),
if(
    contains(outputs('Input')?[1], ','),
    contains(split(outputs('Input')?[1], ','), string(outputs('Now')?[1])),
if(
    contains(outputs('Input')?[1], '-'),
    contains(range(int(split(outputs('Input')?[1], '-')[0]), int(split(outputs('Input')?[1], '-')[1])), outputs('Now')?[1]),
    false
))))},
  @{if(
    equals(outputs('Input')?[2], '*'),
    true,
if(
    isInt(outputs('Input')?[2]),
    equals(int(outputs('Input')?[2]), outputs('Now')?[2]),
if(
    contains(outputs('Input')?[2], ','),
    contains(split(outputs('Input')?[2], ','), string(outputs('Now')?[2])),
if(
    contains(outputs('Input')?[2], '-'),
    contains(range(int(split(outputs('Input')?[2], '-')[0]), int(split(outputs('Input')?[2], '-')[1])), outputs('Now')?[2]),
    false
))))},
  @{if(
    equals(outputs('Input')?[3], '*'),
    true,
if(
    isInt(outputs('Input')?[3]),
    equals(int(outputs('Input')?[3]), outputs('Now')?[3]),
if(
    contains(outputs('Input')?[3], ','),
    contains(split(outputs('Input')?[3], ','), string(outputs('Now')?[3])),
if(
    contains(outputs('Input')?[3], '-'),
    contains(range(int(split(outputs('Input')?[3], '-')[0]), int(split(outputs('Input')?[3], '-')[1])), outputs('Now')?[3]),
    false
))))},
  @{if(
    equals(outputs('Input')?[4], '*'),
    true,
if(
    isInt(outputs('Input')?[4]),
    equals(int(outputs('Input')?[4]), outputs('Now')?[4]),
if(
    contains(outputs('Input')?[4], ','),
    contains(split(outputs('Input')?[4], ','), string(outputs('Now')?[4])),
if(
    contains(outputs('Input')?[4], '-'),
    contains(range(int(split(outputs('Input')?[4], '-')[0]), int(split(outputs('Input')?[4], '-')[1])), outputs('Now')?[4]),
    false
))))}
]
```
That will leave us with an array of booleans.
We can use `contains()` to check if array contains any `false`.
In case it doesn't, it means crontab matches current time.
```wdl
@{contains(outputs('Output'), false)}
```


