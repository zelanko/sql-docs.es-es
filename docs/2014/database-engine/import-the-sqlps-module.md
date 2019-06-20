---
title: Importar el módulo SQLPS | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 303d4cb75ad678ddd0c0f49e204566fc8a0d2c2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064729"
---
# <a name="import-the-sqlps-module"></a>Importar el módulo SQLPS
  El método recomendado para administrar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] desde PowerShell consiste en importar el módulo `sqlps` en un entorno de Windows PowerShell 2.0. El módulo carga y registra los complementos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y los ensamblados de administración.  
  
1.  **Antes de comenzar:**  [Seguridad](#Security)  
  
2.  **Para cargar el módulo:**  [Cargar el módulo sqlps](#LoadSqlps)  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Después de importar el módulo de `sqlps` en Windows PowerShell, a continuación puede:  
  
-   Ejecutar interactivamente comandos de Windows PowerShell.  
  
-   Ejecutar archivos de script de Windows PowerShell.  
  
-   Ejecutar cmdlets de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Usar las rutas de acceso del proveedor de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para navegar por la jerarquía de objetos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Usar los modelos de objetos de administración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (como Microsoft.SqlServer.Management.Smo) para administrar los objetos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Los verbos usados en los nombres de dos cmdlets de SQL Server (`Encode-Sqlname` y `Decode-Sqlname`) no coinciden con los verbos aprobados para Windows PowerShell 2.0. Esto no afecta a la operación, pero mejoras de Windows PowerShell genera una advertencia cuando el módulo de `sqlps` se importa a una sesión.  
  
###  <a name="Security"></a> Seguridad  
 De forma predeterminada, Windows PowerShell se ejecuta con la directiva de ejecución de scripting establecida en **Restricted**, lo que evita la ejecución de cualquier script de Windows PowerShell. Para cargar el módulo `sqlps`, puede usar el cmdlet `Set-ExecutionPolicy` para habilitar la ejecución de scripts firmados o de cualquier script. Ejecute solo scripts de orígenes de confianza y proteja todos los archivos de entrada y salida usando los permisos NTFS adecuados. Para obtener más información sobre cómo habilitar scripts de Windows PowerShell, vea cómo [ejecutar scripts de Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/starting-windows-powershell?view=powershell-6#how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows).  
  
##  <a name="LoadSqlps"></a> Cargar el módulo sqlps  
 **Para cargar el módulo sqlps en Windows PowerShell**  
  
1.  Use el cmdlet `Set-ExecutionPolicy` para establecer la directiva de ejecución de script apropiada.  
  
2.  Use el cmdlet `Import-Module` para importar el módulo sqlps. Especifique el parámetro de `DisableNameChecking` si desea suprimir la advertencia acerca de `Encode-Sqlname` y `Decode-Sqlname`.  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
 En este ejemplo se carga el módulo de `sqlps` con la comprobación de nombre desactivada.  
  
```  
## Import the SQL Server Module.  
  
Import-Module "sqlps" -DisableNameChecking  
  
```  
  

  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [Proveedor de PowerShell de SQL Server](../powershell/sql-server-powershell-provider.md)   
 [Usar los cmdlets del motor de base de datos](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  
