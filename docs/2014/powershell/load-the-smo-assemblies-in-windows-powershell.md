---
title: Carga de ensamblados SMO en Windows PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8ca42b69-da5a-47f4-9085-34e443f0e389
caps.latest.revision: 7
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: eefd944cf5e577dc16218e88911e9a1dcdc7c828
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202976"
---
# <a name="load-the-smo-assemblies-in-windows-powershell"></a>Cargar ensamblados SMO en Windows PowerShell
  En este tema se describe cómo cargar los ensamblados del objeto de administración de SQL Server (SMO) en scripts de Windows PowerShell que no usan el proveedor de PowerShell de SQL Server.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
 El mecanismo preferido para cargar ensamblados SMO es cargar el módulo de `sqlps`. El proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] incluye en el módulo carga automáticamente los ensamblados SMO y también implementa características que amplían la utilidad de los objetos SMO en los scripts de PowerShell.  
  
 Hay dos casos en los que puede que tenga que cargar los ensamblados de SMO directamente:  
  
-   Si un script hace referencia a un objeto de SMO antes del primer comando que hace referencia al proveedor o cmdlets desde los complementos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Se desea pasar código de SMO desde otro lenguaje, como C# o Visual Basic, que no usa el proveedor ni cmdlets.  
  
## <a name="example-loading-the-sql-server-management-objects"></a>Ejemplo: Cargar objetos de Administración de SQL Server  
 El código siguiente carga los ensamblados de SMO:  
  
```  
#  
# Loads the SQL Server Management Objects (SMO)  
#  
  
$ErrorActionPreference = "Stop"  
  
$sqlpsreg="HKLM:\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Microsoft.SqlServer.Management.PowerShell.sqlps"  
  
if (Get-ChildItem $sqlpsreg -ErrorAction "SilentlyContinue")  
{  
    throw "SQL Server Provider for Windows PowerShell is not installed."  
}  
else  
{  
    $item = Get-ItemProperty $sqlpsreg  
    $sqlpsPath = [System.IO.Path]::GetDirectoryName($item.Path)  
}  
  
$assemblylist =   
"Microsoft.SqlServer.Management.Common",  
"Microsoft.SqlServer.Smo",  
"Microsoft.SqlServer.Dmf ",  
"Microsoft.SqlServer.Instapi ",  
"Microsoft.SqlServer.SqlWmiManagement ",  
"Microsoft.SqlServer.ConnectionInfo ",  
"Microsoft.SqlServer.SmoExtended ",  
"Microsoft.SqlServer.SqlTDiagM ",  
"Microsoft.SqlServer.SString ",  
"Microsoft.SqlServer.Management.RegisteredServers ",  
"Microsoft.SqlServer.Management.Sdk.Sfc ",  
"Microsoft.SqlServer.SqlEnum ",  
"Microsoft.SqlServer.RegSvrEnum ",  
"Microsoft.SqlServer.WmiEnum ",  
"Microsoft.SqlServer.ServiceBrokerEnum ",  
"Microsoft.SqlServer.ConnectionInfoExtended ",  
"Microsoft.SqlServer.Management.Collector ",  
"Microsoft.SqlServer.Management.CollectorEnum",  
"Microsoft.SqlServer.Management.Dac",  
"Microsoft.SqlServer.Management.DacEnum",  
"Microsoft.SqlServer.Management.Utility"  
  
foreach ($asm in $assemblylist)  
{  
    $asm = [Reflection.Assembly]::LoadWithPartialName($asm)  
}  
  
Push-Location  
cd $sqlpsPath  
update-FormatData -prependpath SQLProvider.Format.ps1xml   
Pop-Location  
```  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  