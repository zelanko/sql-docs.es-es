---
title: Usar los cmdlets del motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
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
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: efd59bc8c0d6bb748b9ae6c314b0a75cc6d98c5f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927916"
---
# <a name="use-the-database-engine-cmdlets"></a>Utilizar los cmdlets del motor de base de datos
  Los cmdlets de Windows PowerShell son comandos de una sola función que suelen seguir la convención de nomenclatura verbo-nombre, como **Get-Help** o **Set-MachineName**. El proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para Windows PowerShell proporciona cmdlets específicos a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="database-engine-cmdlets"></a>Cmdlets del motor de base de datos  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implementa una pequeña parte de los cmdlets de [!INCLUDE[ssDE](../includes/ssde-md.md)]. Estos cmdlets se usan principalmente para ejecutar scripts Transact-SQL existentes de los nuevos scripts de PowerShell, evaluar las directivas de administración basadas en directivas y ayuda a especificar los identificadores de SQL Server en rutas de acceso del proveedor de SQL Server.  
  
 La mayoría de los scripts de Windows PowerShell funciona con [!INCLUDE[ssDE](../includes/ssde-md.md)] mediante el proveedor de SQL Server PowerShell y los modelos de objetos de administración de SQL Server. Para más información, consulte el artículo sobre [SQL Server PowerShell](../powershell/sql-server-powershell.md).  
  
### <a name="get-cmdlet-help"></a>Obtener Ayuda de los cmdlets  
 En el entorno de Windows PowerShell, el cmdlet **Get-Help** proporciona información de ayuda para cada cmdlet. **Get-Help** devuelve información como la sintaxis, las definiciones de parámetro, los tipos de entrada y salida y una descripción de la acción realizada por el cmdlet. Para más información, consulte [Get Help SQL Server PowerShell](../../2014/database-engine/get-help-sql-server-powershell.md).  
  
### <a name="partial-parameter-names"></a>Nombres de parámetros parciales  
 No tiene que especificar el nombre completo de un parámetro de cmdlet. Solo tiene que especificar una parte del nombre que sea suficiente para separarlo de forma exclusiva de los otros parámetros admitidos por el cmdlet. Por ejemplo, en estos ejemplos se muestran tres formas de especificar el parámetro **Invoke-Sqlcmd -QueryTimeout** :  
  
```powershell
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTimeout 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTime 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryT 3  
```  
  
## <a name="database-engine-cmdlet-tasks"></a>Tareas de cmdlets del motor de base de datos  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe el uso de **Invoke-Sqlcmd** para ejecutar scripts de **sqlcmd** o comandos que contienen instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] o XQuery. Puede aceptar la entrada de **sqlcmd** como parámetro de entrada de la cadena de caracteres o como nombre de un archivo de script que se va a abrir.|[cmdlet Invoke-Sqlcmd](../../2014/database-engine/invoke-sqlcmd-cmdlet.md)|  
|Describe el uso de **Invoke-PolicyEvaluation** para informar de si un conjunto de objetos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de destino cumple las condiciones definidas en las directivas de administración basadas en directivas. Opcionalmente, el cmdlet se puede usar para volver a configurar cualquier opción que se pueda establecer en los objetos de destino que no cumplan las condiciones de la directiva.|[cmdlet Invoke-PolicyEvaluation](../../2014/database-engine/invoke-policyevaluation-cmdlet.md)|  
|Describe el uso de `Encode-Sqlname` y `Decode-Sqlname` para administrar los identificadores de SQL Server que contienen caracteres no admitidos en las rutas de Windows PowerShell.|[Codificar y descodificar identificadores de SQL Server](../powershell/encode-and-decode-sql-server-identifiers.md)|  
|Describe el uso de `Convert-UrnToPath` para convertir un nombre de recursos uniforme (URN) del objeto de administración de SQL Server a la ruta de acceso equivalente en el proveedor de SQL Server.|[Convertir URN en rutas de acceso del proveedor de SQL Server](../../2014/database-engine/convert-urns-to-sql-server-provider-paths.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Proveedor de SQL Server PowerShell](../powershell/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [Información general de los cmdlets de PowerShell para Grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
