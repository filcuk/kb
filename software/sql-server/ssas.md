---
title: SSAS
description: SQL Server Analysis Services
published: true
date: 2024-11-15T17:26:19.892Z
tags: 
editor: markdown
dateCreated: 2024-11-13T11:38:19.453Z
---

# Troubleshooting
## Processing
### Chech last time a cube was processed
In [SSAS](/en/software/sql-server/ssas), run the following [MDX](/en/language/mdx) query:
```mdx
SELECT CUBE_NAME, LAST_DATA_UPDATE FROM $System.MDSCHEMA_CUBES
```

### Kill stuck cube processing job
In [SSAS](/en/software/sql-server/ssas), run the following [MDX](/en/language/mdx) query:
```mdx
SELECT * FROM $SYSTEM.DISCOVER_CONNECTIONS
GO
SELECT * FROM $SYSTEM.DISCOVER_SESSIONS
GO
SELECT * FROM $SYSTEM.DISCOVER_COMMANDS
GO
```

Then run the following [XMLA](/en/language/xmla) query using IDs from the previous query:
```xml
<Command>  
   <Cancel>  
      <ConnectionID>...</ConnectionID>  
      <SessionID>...</SessionID>  
      <SPID>...</SPID>  
      <CancelAssociated>1 or 0</CancelAssociated>  
   </Cancel>  
</Command>  
```

> The Cancel command cancels currently executing commands within the context of a session. If the client application has not requested a session, a command cannot be canceled.
> 
> Source: [learn.microsoft.com](https://learn.microsoft.com/en-us/analysis-services/xmla/xml-elements-commands/cancel-element-xmla?view=asallproducts-allversions#remarks)
{.is-warning}