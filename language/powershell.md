---
title: PowerShell
description: A task automation and configuration management program from Microsoft.
published: true
date: 2024-11-19T10:42:49.345Z
tags: 
editor: markdown
dateCreated: 2024-11-19T10:30:22.434Z
---

# Basics
### Determine current version
```powershell
$PSVersionTable.PSVersion
```
```
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      19000  4700
```

# Modules
## Management
### List available modules
```powershell
Get-Module -ListAvailable
```
```
Directory: C:\Program Files\WindowsPowerShell\Modules

ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Script     1.0.1      Microsoft.PowerShell.Operation.V... {Get-OperationValidation, Invoke-OperationValidation}
Script     0.86.0.0   Microsoft.PowerToys.Configure
Manifest   1.2.1111   MicrosoftPowerBIMgmt
Binary     1.2.1111   MicrosoftPowerBIMgmt.Admin          {Add-PowerBIEncryptionKey, Get-PowerBIEncryptionKey, Get-P...
Binary     1.2.1111   MicrosoftPowerBIMgmt.Capacities     Get-PowerBICapacity
...
```

### List available commands for given module
Module must be loaded for exported commands to be available:
```powershell
Import-Module -Name <ModuleName>
Get-Command -Module <ModuleName>
```

A shorthand alternative; `<ModuleName>` is optional, all modules are returned if omitted:
```powershell
Get-Module <ModuleName> -ListAvailable | % { $_.ExportedCommands.Values }
```

Another alternative which will search returned commands:
```powershell
Get-Command -Module <ModuleName> | ? {$_.name -match '<Lookup>'}
```

Documentation: [learn.microsoft.com](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/get-command)
