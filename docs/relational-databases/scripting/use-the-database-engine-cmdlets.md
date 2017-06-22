---
title: Usar los cmdlets del motor de base de datos | Microsoft Docs
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Cmdlets [SQL Server], Encode-Sqlname
- Encode-Sqlname cmdlet
- PowerShell [SQL Server], Encode-Sqlname
- Convert-UrnToPath cmdlet
- PowerShell [SQL Server], cmdlets
- Cmdlets [SQL Server]
- PowerShell [SQL Server], Convert-UrnToPath
- Cmdlets [SQL Server], Convert-UrnToPath
- Decode-Sqlname cmdlet
- PowerShell [SQL Server], Decode-Sqlname
- Cmdlets [SQL Server], Decode-Sqlname
ms.assetid: 720aa982-09ae-41a3-b603-a91004cfbe3e
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 457781b7e16a5722f4d232cff14b8f20c7651972
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="use-the-database-engine-cmdlets"></a>Utilizar los cmdlets del motor de base de datos
  Los cmdlets de Windows PowerShell son comandos de una sola función que suelen seguir la convención de nomenclatura verbo-nombre, como **Get-Help** o **Set-MachineName**. El proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Windows PowerShell proporciona cmdlets específicos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="database-engine-cmdlets"></a>Cmdlets del motor de base de datos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa una pequeña parte de los cmdlets de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Estos cmdlets se usan principalmente para ejecutar scripts Transact-SQL existentes de los nuevos scripts de PowerShell, evaluar las directivas de administración basadas en directivas y ayuda a especificar los identificadores de SQL Server en rutas de acceso del proveedor de SQL Server.  
  
 La mayoría de los scripts de Windows PowerShell funciona con [!INCLUDE[ssDE](../../includes/ssde-md.md)] mediante el proveedor de SQL Server PowerShell y los modelos de objetos de administración de SQL Server. Para más información, vea [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md).  
  
### <a name="get-cmdlet-help"></a>Obtener Ayuda de los cmdlets  
 En el entorno de Windows PowerShell, el cmdlet **Get-Help** proporciona información de ayuda para cada cmdlet. **Get-Help** devuelve información como la sintaxis, las definiciones de parámetro, los tipos de entrada y salida y una descripción de la acción realizada por el cmdlet. Para más información, consulte [Get Help SQL Server PowerShell](../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
### <a name="partial-parameter-names"></a>Nombres de parámetros parciales  
 No tiene que especificar el nombre completo de un parámetro de cmdlet. Solo tiene que especificar una parte del nombre que sea suficiente para separarlo de forma exclusiva de los otros parámetros admitidos por el cmdlet. Por ejemplo, en estos ejemplos se muestran tres formas de especificar el parámetro **Invoke-Sqlcmd -QueryTimeout** :  
  
```  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTimeout 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTime 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryT 3  
```  
  
## <a name="database-engine-cmdlet-tasks"></a>Tareas de cmdlets del motor de base de datos  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe el uso de **Invoke-Sqlcmd** para ejecutar scripts de **sqlcmd** o comandos que contienen instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] o XQuery. Puede aceptar la entrada de **sqlcmd** como parámetro de entrada de la cadena de caracteres o como nombre de un archivo de script que se va a abrir.|[cmdlet Invoke-Sqlcmd](../../powershell/invoke-sqlcmd-cmdlet.md)|  
|Describe el uso de **Invoke-PolicyEvaluation** para informar de si un conjunto de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino cumple las condiciones definidas en las directivas de administración basadas en directivas. Opcionalmente, el cmdlet se puede usar para volver a configurar cualquier opción que se pueda establecer en los objetos de destino que no cumplan las condiciones de la directiva.|[cmdlet Invoke-PolicyEvaluation](../../powershell/invoke-policyevaluation-cmdlet.md)|  
|Describe el uso de **Encode-Sqlname** y **Decode-Sqlname** para administrar los identificadores de SQL Server que contienen caracteres no admitidos en las rutas de acceso de Windows PowerShell.|[Codificar y descodificar identificadores de SQL Server](../../relational-databases/scripting/encode-and-decode-sql-server-identifiers.md)|  
|Describe el uso de **Convert-UrnToPath** para convertir un nombre de recursos uniforme (URN) del objeto de administración de SQL Server a la ruta de acceso equivalente en el proveedor de SQL Server.|[Convertir URN en rutas de acceso del proveedor de SQL Server](../../relational-databases/scripting/convert-urns-to-sql-server-provider-paths.md)|  
  
## <a name="see-also"></a>Vea también  
 [Proveedor de PowerShell de SQL Server](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
[Información general de los cmdlets de PowerShell para grupos de disponibilidad AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)
  
  

