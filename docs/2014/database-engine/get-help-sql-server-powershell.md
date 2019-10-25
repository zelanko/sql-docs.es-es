---
title: Obtener ayuda de SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Help [PowerShell]
- Help [SQL Server], PowerShell
- PowerShell [SQL Server], help
ms.assetid: 968c316d-db83-4c24-8ea6-9f18736842f7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 705512f54feae3bf60317c18b8c260ef484abebc
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797875"
---
# <a name="get-help-sql-server-powershell"></a>Get Help SQL Server PowerShell
  Hay varios orígenes de información sobre cómo utilizar los cmdlets y el proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para Windows PowerShell. Esto incluye la ayuda que está disponible en el entorno de Windows PowerShell.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
 Para obtener información sobre Windows PowerShell, vea el [Guía de Introducción de Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).  
  
 Para ver una introducción a los cmdlets y el proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , vea [SQL Server PowerShell](../powershell/sql-server-powershell.md).  
  
### <a name="help-in-the-windows-powershell-environment"></a>Ayuda en el entorno de Windows PowerShell  
 Use el cmdlet **Get-Help** para obtener ayuda en el entorno de Windows PowerShell. **Get-Help** proporciona ayuda básica para el lenguaje de Windows PowerShell y los diversos cmdlets y proveedores disponibles en Windows PowerShell.  
  
 Para obtener más información sobre las formas en que puede usar **Get-Help**, vea [Obtener Ayuda: Get-Help](https://go.microsoft.com/fwlink/?LinkId=102136).  
  
### <a name="sql-server-powershell-provider-help"></a>Ayuda del proveedor de SQL Server PowerShell  
 El proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell implementa varias carpetas en una unidad virtual de SQLSERVER, como el SQLSERVER: \ SQL y SQLSERVER: \ Carpetas de DAC. Cada carpeta está asociada con uno de los modelos de objetos de administración de SQL Server. Aunque puede mostrar los métodos y propiedades asociados con cada nodo en una ruta de acceso de SQL Server, no puede obtener ayuda para ellos en el entorno de PowerShell. Para una tabla de carpetas con vínculos a referencia de programación asociada, vea [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md).  
  
### <a name="invoke-sqlcmd-help"></a>Ayuda de Invoke-Sqlcmd  
 El cmdlet **Invoke-Sqlcmd** toma como entrada cualquier archivo de script o consulta que la utilidad **sqlcmd** pueda ejecutar. Puede usar **Get-Help** para obtener información sobre **Invoke-Sqlcmd** y sus parámetros, pero no hay ninguna cobertura de **Get-Help** para las consultas **sqlcmd** .  
  
 La entrada *-Query* o *-QueryFromFile* puede contener:  
  
-   Variables y comandos de**sqlcmd** . Para obtener información sobre estas variables y comandos, consulte la sección Comentarios de [sqlcmd Utility](../tools/sqlcmd-utility.md).  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] . Para obtener más información sobre el idioma [!INCLUDE[tsql](../includes/tsql-md.md)], vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference).  
  
-   Instrucciones XQuery. Para obtener más información sobre lenguaje XQuery admitido por [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Referencia del lenguaje XQuery &#40;SQL Server&#41;](/sql/xquery/xquery-language-reference-sql-server).  
  
## <a name="get-help-for-a-sql-server-cmdlet"></a>Obtener ayuda para un cmdlet de SQL Server.  
 **Para obtener ayuda para un cmdlet**  
  
-   Ejecute Get-Help especificando el nombre del cmdlet y el nivel de ayuda que se va a devolver.  
  
### <a name="example-cmdlet-get-help"></a>Ejemplo: Get-Help de cmdlet  
 Los siguientes ejemplos devuelven diferentes niveles de ayuda para **Invoke-Sqlcmd**:  
  
```powershell
## Get the basic help.  
Get-Help Invoke-Sqlcmd  
  
## Get the full help.  
Get-Help Invoke-Sqlcmd -Full  
  
## Get the parameter descriptions.  
Get-Help Invoke-Sqlcmd -Parameter *  
  
## Get the code examples.  
Get-Help Invoke-Sqlcmd -Examples  
  
## Get the syntax diagram.  
Get-Help Invoke-Sqlcmd -Syntax  
```  
  
## <a name="get-a-list-of-providers"></a>Obtener una lista de proveedores  

### <a name="to-get-a-list-of-active-providers"></a>Para obtener una lista de proveedores activo
  
1.  Ejecute Get-Help ejecutando la categoría del proveedor.  
  
 Para obtener más información sobre cómo obtener ayuda del proveedor en Windows PowerShell, vea [Unidades y proveedores](https://go.microsoft.com/fwlink/?LinkId=102137).  
  
### <a name="example-get-a-list-of-providers"></a>Ejemplo: Obtener una lista de proveedores  
 Este código devuelve una lista de los proveedores habilitados actualmente en la sesión de Windows PowerShell:  
  
```powershell
Get-Help -Category provider  
```  
  
## <a name="get-help-about-the-sql-server-provider"></a>Obtener ayuda acerca del proveedor de SQL Server  
 **Para obtener ayuda acerca del proveedor**  
  
1.  Ejecute Get-Help especificando el nombre SQLServer  
  
### <a name="example-get-sql-server-provider-help"></a>Ejemplo: Obtener Ayuda del proveedor de SQL Server  
 Este ejemplo devuelve información básica sobre el proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] :  
  
```powershell
Get-Help SQLServer  
```  
  
## <a name="list-methods-and-properties"></a>Enumerar métodos y propiedades  
 **Para mostrar los métodos y propiedades para un nodo en una ruta de acceso del proveedor de SQL Server**  
  
1.  Un CD de un nodo de la ruta de acceso de SQL Server, o crear una variable establecida en esa ubicación.  
  
2.  Ejecute el cmdlet **Get-Member** con el parámetro-type establecido en métodos o propiedades.  
  
### <a name="examples-listing-methods-and-properties"></a>Ejemplos: Enumerar métodos y propiedades  
 En este ejemplo se enumeran los métodos admitidos para el nodo de bases de datos:  
  
```powershell
Set-Location SQL:\MyComputer\DEFAULT\Databases  
Get-Item . | Get-Member -Type Methods  
```  
  
 Este ejemplo enumera las propiedades de una variable que se ha establecido en un objeto SMO Table:  
  
```powershell
$MyVar = New-Object Microsoft.SqlServer.Management.SMO.Table  
$MyVar | Get-Member -Type Properties  
```  
  
## <a name="see-also"></a>Ver también  
 [Proveedor de PowerShell de SQL Server](../powershell/sql-server-powershell-provider.md)   
 [Usar los cmdlets del motor de base de datos](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
