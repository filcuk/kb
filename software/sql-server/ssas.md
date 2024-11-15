---
title: SSAS
description: SQL Server Analysis Services
published: true
date: 2024-11-15T16:58:19.449Z
tags: 
editor: markdown
dateCreated: 2024-11-13T11:38:19.453Z
---

# Troubleshooting
## 
### Kill stuck cube processing
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
      <CancelAssociated>...</CancelAssociated>  
   </Cancel>  
</Command>  
```

> The Cancel command cancels currently executing commands within the context of a session. If the client application has not requested a session, a command cannot be canceled.
> 
> Source: [learn.microsoft.com](https://learn.microsoft.com/en-us/analysis-services/xmla/xml-elements-commands/cancel-element-xmla?view=asallproducts-allversions#remarks)
{.is-warning}