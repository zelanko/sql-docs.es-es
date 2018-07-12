---
title: Importar el módulo SQLPS | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
caps.latest.revision: 9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c64ba9da7884b1ccb82dd31480d60638c8d952ee
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192477"
---
# <a name="import-the-sqlps-module"></a>Importar el módulo SQLPS
  El método recomendado para administrar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] desde PowerShell consiste en importar el módulo `sqlps` en un entorno de Windows PowerShell 2.0. El módulo carga y registra los complementos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y los ensamblados de administración.  
  
1.  **Antes de comenzar:**  [Seguridad](#Security)  
  
2.  **Para cargar el módulo:**  [Cargar el módulo sqlps](#LoadSqlps)  
  
## <a name="before-you-begin"></a>Antes de comenzar  
 Después de importar el módulo de `sqlps` en Windows PowerShell, a continuación puede:  
  
-   Ejecutar interactivamente comandos de Windows PowerShell.  
  
-   Ejecutar archivos de script de Windows PowerShell.  
  
-   Ejecutar cmdlets de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Usar las rutas de acceso del proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para navegar por la jerarquía de objetos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Usar los modelos de objetos de administración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (como Microsoft.SqlServer.Management.Smo) para administrar los objetos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Los verbos usados en los nombres de dos cmdlets de SQL Server (`Encode-Sqlname` y `Decode-Sqlname`) no coinciden con los verbos aprobados para Windows PowerShell 2.0. Esto no tiene ningún efecto en su funcionamiento, pero Windows PowerShell genera una advertencia cuando el `sqlps` módulo se importa a una sesión.  
  
###  <a name="Security"></a> Seguridad  
 De forma predeterminada, Windows PowerShell se ejecuta con la directiva de ejecución de scripting establecida en **Restricted**, lo que evita la ejecución de cualquier script de Windows PowerShell. Para cargar el módulo `sqlps`, puede usar el cmdlet `Set-ExecutionPolicy` para habilitar la ejecución de scripts firmados o de cualquier script. Ejecute solo scripts de orígenes de confianza y proteja todos los archivos de entrada y salida usando los permisos NTFS adecuados. Para obtener más información sobre cómo habilitar scripts de Windows PowerShell, vea cómo [ejecutar scripts de Windows PowerShell](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx).  
  
##  <a name="LoadSqlps"></a> Cargar el módulo sqlps  
 **Para cargar el módulo sqlps en Windows PowerShell**  
  
1.  Use el `Set-ExecutionPolicy` cmdlet para establecer la directiva de ejecución de script apropiada.  
  
2.  Use el `Import-Module` para importar el módulo sqlps. Especifique el `DisableNameChecking` parámetro si desea suprimir la advertencia sobre `Encode-Sqlname` y `Decode-Sqlname`.  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
 En este ejemplo se carga el módulo de `sqlps` con la comprobación de nombre desactivada.  
  
```  
## Import the SQL Server Module.  
  
Import-Module “sqlps” -DisableNameChecking  
  
```  
  

  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md)   
 [Usar los cmdlets del motor de base de datos](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  
