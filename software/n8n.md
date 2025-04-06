---
title: n8n
description: Workflow automation
published: true
date: 2025-04-06T20:16:13.345Z
tags: self-hosted, fos
editor: markdown
dateCreated: 2025-04-06T20:06:33.911Z
---

# Tips
### Outputting duration of execution
#### Current execution in seconds
1. Create 'Edit fields' node named 'Variables' and add field `startTime` = `{{ $now.toISO() }}`
1. Add this to output: `{{ $now.diff(DateTime.fromISO($('Variables').item.json.startTime)).as('seconds')}}s`

#### Execution using n8n API as an object
1. Create 'n8n' node and select 'Execution' resource
1. Add this to output: `{{ DateTime.fromISO($('n8n').item.json.stoppedAt).diff(DateTime.fromISO($('n8n').item.json.startedAt), ["days","hours", "minutes", "seconds"]).toObject() }}`