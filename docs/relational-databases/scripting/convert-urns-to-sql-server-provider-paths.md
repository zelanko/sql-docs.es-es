---
title: "Convertir URN en rutas de acceso del proveedor de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c9b1b8f1-b117-4e87-9704-2170f62c5c8b
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# Convertir URN en rutas de acceso del proveedor de SQL Server
  El modelo de objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO) compila nombres de recursos uniformes (URN) para sus objetos. Cada URN identifica un objeto SMO y se puede convertir en una rutadel proveedor de PowerShell de SQL Server mediante el cmdlet **Convert-UrnToPath**.  
  
## Convertir los URN en rutas de acceso  
 Cada URN tiene la misma información que una ruta de acceso al objeto, pero en un formato diferente. Por ejemplo, esta es la ruta de acceso a una tabla:  
  
 SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Address  
  
 Y este es el URN para el mismo objeto:  
  
 Server[@Name='MyComputer']\Database[@Name='AdventureWorks2012']\Table[@Name='Address' and @Schema='Person']  
  
 Si ha creado un objeto SMO en un script de PowerShell, puede hacer referencia a la propiedad **Urn** para obtener el URN del objeto y, seguidamente, usar el cmdlet **Convert-UrnToPath** para convertir la cadena URN de SMO en una ruta de acceso de Windows PowerShell. Puede usar el proveedor para navegar a ubicaciones diferentes de la ruta de acceso.  
  
 Si los nombres de nodo contienen caracteres extendidos que no se admiten en los nombres de ruta de acceso de Windows PowerShell, **Convert-UrnToPath** los codifica en su representación hexadecimal. Por ejemplo "My:Table" se devuelve como "My%3ATable".  
  
 Para obtener ejemplos del uso del cmdlet, en Windows PowerShell, ejecute:  
  
```  
Get-Help Convert-UrnToPath -Examples  
```  
  
## Vea también  
 [Expresiones de consulta y nombres de recursos uniformes](../../powershell/query-expressions-and-uniform-resource-names.md)   
 [Proveedor de PowerShell de SQL Server](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  