---
title: Trabajar con rutas acceso de SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: f31d8e2c-8d59-4fee-ac2a-324668e54262
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5ca7d915b940296e6de6689e666401b0c3534c9d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "72782730"
---
# <a name="work-with-sql-server-powershell-paths"></a>Trabajar con rutas acceso de SQL Server PowerShell
  Después de haber navegado a un nodo de una ruta de acceso del proveedor de [!INCLUDE[ssDE](../includes/ssde-md.md)] , puede realizar el trabajo o recuperar información mediante los métodos y propiedades de los objetos de administración de [!INCLUDE[ssDE](../includes/ssde-md.md)] asociados al nodo.  
  
1.  [Antes de comenzar](#BeforeYouBegin)  
  
2.  **Para trabajar en un nodo de ruta de acceso:**  [enumerar métodos y propiedades](#ListPropMeth), [usar métodos y propiedades](#UsePropMeth)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
 Después de haber navegado a un nodo de una ruta de acceso del proveedor de [!INCLUDE[ssDE](../includes/ssde-md.md)] , puede realizar dos tipos de acciones:  
  
-   Puede ejecutar los cmdlets de Windows PowerShell que operan en los nodos, como **Rename-Item**.  
  
-   Puede llamar a los métodos desde el modelo de objetos de administración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] asociado, como SMO. Por ejemplo, si navega al nodo Bases de datos de una ruta de acceso, puede usar los métodos y las propiedades de la clase <xref:Microsoft.SqlServer.Management.Smo.Database> .  
  
 El proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se utiliza para administrar los objetos en una instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)]. No se utiliza para trabajar con los datos de las bases de datos. Si ha navegado a una tabla o vista, no puede utilizar el proveedor para seleccionar, insertar, actualizar o eliminar datos. Use el cmdlet **Invoke-Sqlcmd** para consultar o cambiar los datos de las tablas y vistas del entorno de Windows PowerShell. Para obtener más información, vea [cmdlet Invoke-Sqlcmd](../database-engine/invoke-sqlcmd-cmdlet.md).  
  
##  <a name="ListPropMeth"></a> Enumerar métodos y propiedades
  
 Para ver los métodos y propiedades disponibles de determinados objetos o clases de objetos, use el cmdlet **Get-Member** .  
  
### <a name="examples-listing-methods-and-properties"></a>Ejemplos: Enumerar métodos y propiedades  
 En este ejemplo se establece una variable de Windows PowerShell en la clase <xref:Microsoft.SqlServer.Management.Smo.Database> de SMO y se enumeran los métodos y las propiedades:  
  
```powershell
$MyDBVar = New-Object Microsoft.SqlServer.Management.SMO.Database  
$MyDBVar | Get-Member -Type Methods  
$MyDBVar | Get-Member -Type Properties  
```  
  
 También puede usar **Get-Member** para mostrar los métodos y propiedades asociados con el nodo final de una ruta de acceso de Windows PowerShell.  
  
 En este ejemplo se navega al nodo Databases de una ruta de acceso de SQLSERVER: y se muestran las propiedades de la colección:  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
Get-Item . | Get-Member -Type Properties  
```  
  
 En este ejemplo se navega al nodo AdventureWorks2012 de una ruta de acceso de SQLSERVER: y se muestran las propiedades del objeto:  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012  
Get-Item . | Get-Member -Type Properties  
```  
  
##  <a name="UsePropMeth"></a>Usar métodos y propiedades de SMO  
  
 Para realizar el trabajo en objetos de una ruta de acceso del proveedor de [!INCLUDE[ssDE](../includes/ssde-md.md)] , puede usar los métodos y las propiedades de SMO.  
  
### <a name="examples-using-methods-and-properties"></a>Ejemplos: Usar métodos y propiedades  
 En este ejemplo se usa la propiedad **Schema** de SMO para obtener una lista de las tablas del esquema Sales en AdventureWorks2012:  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables  
Get-ChildItem | Where {$_.Schema -eq "Sales"}  
```  
  
 En este ejemplo se usa el método de **script** de SMO para generar un `CREATE VIEW` script que contiene las instrucciones que debe tener para volver a crear las vistas en AdventureWorks2012:  
  
```powershell
Remove-Item C:\PowerShell\CreateViews.sql  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Views  
foreach ($Item in Get-ChildItem) { $Item.Script() | Out-File -Filepath C:\PowerShell\CreateViews.sql -append }  
```  
  
 En este ejemplo se utiliza el método **Create** de SMO para crear una base de datos y, a continuación, se usa la propiedad **State** para mostrar si la base de datos existe:  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
$MyDBVar = New-Object Microsoft.SqlServer.Management.SMO.Database  
$MyDBVar.Parent = (Get-Item ..)  
$MyDBVar.Name = "NewDB"  
$MyDBVar.Create()  
$MyDBVar.State  
```  
  
## <a name="see-also"></a>Consulte también  
 [Proveedor de PowerShell de SQL Server](sql-server-powershell-provider.md)   
 [Navegar por las rutas de acceso de SQL Server PowerShell](navigate-sql-server-powershell-paths.md)   
 [Convertir URN en rutas de acceso del proveedor de SQL Server](../database-engine/convert-urns-to-sql-server-provider-paths.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
