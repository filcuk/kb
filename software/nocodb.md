---
title: NocoDB
description: Spreadsheet interface for creating online databases
published: true
date: 2025-04-06T20:20:09.904Z
tags: 
editor: markdown
dateCreated: 2025-04-06T20:06:53.307Z
---

# Tips
### Create column with unique constraint
#### Using NocoDB API
- URL: `https://nocodb.<instance>/api/v2/meta/tables/<table>/columns`
- Body:
```json
{
  "title": "<column1>",
  "uidt": "SingleLineText",
  "unique": 1
}
```
Docs: [nocodb.com](https://meta-apis-v2.nocodb.com/#tag/Fields/operation/db-table-column-create)