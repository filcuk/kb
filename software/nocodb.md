---
title: NocoDB
description: Spreadsheet interface for creating online databases
published: true
date: 2025-04-06T20:26:26.359Z
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

#### Via Docker container's shell
>  All unquoted names are considered lower-case and won't work with variable-case table names!
{.is-warning}

> In case you need to select a DB manually, run `\c your_db`
{.is-success}


1. Connect to psql: `docker exec -i your_container -U your_user -W your_db`
1. List all relations: `\dt *.*` - find your table, make note of the schema
1. List table detail `\d "your_schema.your_table"`
1. If you got `ERROR: relation "your_schema.your_table" does not exist`, continue, otherwise skip the next step
1. Run `SET search_path TO your_schema;` *(this setting only lasts for the duration of current session)*
1. Run `ALTER TABLE "your_table" ADD CONSTRAINT your_constraint_name ("Colum1", "Column2");`
1. Repeat step 3 to check your new constraint

Links: [github.com](https://github.com/nocodb/nocodb/issues/4728#issuecomment-2571408864)