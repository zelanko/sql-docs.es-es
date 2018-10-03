---
title: Conversión de URN en rutas de acceso del proveedor de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: c9b1b8f1-b117-4e87-9704-2170f62c5c8b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e75581756f0464197e05b78083b7e90d7d3dfb3a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061295"
---
# <a name="convert-urns-to-sql-server-provider-paths"></a>Convertir URN en rutas de acceso del proveedor de SQL Server
  El modelo de objetos de administración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (SMO) compila nombres de recursos uniformes (URN) para sus objetos. Cada URN identifica un objeto SMO y se puede convertir en una ruta de acceso del proveedor de PowerShell de SQL Server mediante el uso de la `Convert-UrnToPath` cmdlet.  
  
## <a name="converting-urns-to-paths"></a>Convertir los URN en rutas de acceso  
 Cada URN tiene la misma información que una ruta de acceso al objeto, pero en un formato diferente. Por ejemplo, esta es la ruta de acceso a una tabla:  
  
 SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Address  
  
 Y este es el URN para el mismo objeto:  
  
 Server[@Name='MyComputer']\Database[@Name='AdventureWorks2012']\Table[@Name='Address' and @Schema='Person']  
  
 Si ha creado un objeto SMO en un script de PowerShell, puede hacer referencia a la propiedad `Urn` para obtener el URN del objeto y a, continuación, usar el cmdlet `Convert-UrnToPath` para convertir la cadena URN de SMO en una ruta de acceso de Windows PowerShell. Puede usar el proveedor para navegar a ubicaciones diferentes de la ruta de acceso.  
  
 Si los nombres de nodo contienen caracteres extendidos que no se admiten en los nombres de ruta de acceso de Windows PowerShell, `Convert-UrnToPath` los codifica en su representación hexadecimal. Por ejemplo "My:Table" se devuelve como "My%3ATable".  
  
 Para obtener ejemplos del uso del cmdlet, en Windows PowerShell, ejecute:  
  
```  
Get-Help Convert-UrnToPath -Examples  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones de consulta y nombres de recursos uniformes](../powershell/query-expressions-and-uniform-resource-names.md)   
 [Proveedor de PowerShell de SQL Server](../powershell/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
