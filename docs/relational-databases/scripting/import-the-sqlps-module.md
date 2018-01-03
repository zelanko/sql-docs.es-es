---
title: "Importar el módulo SQLPS | Microsoft Docs"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ae5fb5957e23a6ad4488a33587d227219855d6b8
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="import-the-sqlps-module"></a>Importar el módulo SQLPS
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] El método recomendado para administrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde PowerShell consiste en importar el módulo **sqlps** en un entorno de Windows PowerShell. El módulo carga y registra los complementos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los ensamblados de administración.  A partir de Windows PowerShell 3.0, los módulos se importan automáticamente cuando se usa cualquier cmdlet o función del módulo en un comando. Esta característica funciona en cualquier módulo de un directorio incluido en el valor de la variable de entorno PSModulePath.  Para más información, consulte [Importación de un módulo de PowerShell](https://msdn.microsoft.com/library/dd878284(v=vs.85).aspx).
  
1.  **Antes de comenzar:**  [Seguridad](#Security)  
  
2.  **Para cargar el módulo:**  [Cargar el módulo sqlps](#LoadSqlps)  
  
## <a name="before-you-begin"></a>Antes de comenzar  
 Después de importar el módulo de **sqlps** en Windows PowerShell, a continuación puede:  
  
-   Ejecutar interactivamente comandos de Windows PowerShell.  
  
-   Ejecutar archivos de script de Windows PowerShell.  
  
-   Ejecutar cmdlets de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Usar las rutas de acceso del proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para navegar por la jerarquía de objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Usar los modelos de objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (como Microsoft.SqlServer.Management.Smo) para administrar los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Los verbos usados en los nombres de dos cmdlets de SQL Server (**Encode-Sqlname** y **Decode-Sqlname**) no coinciden con los verbos aprobados para Windows PowerShell. Esto no afecta a la operación, pero mejoras de Windows PowerShell genera una advertencia cuando el módulo de **sqlps** se importa a una sesión.  
  
###  <a name="Security"></a> Seguridad  
 De forma predeterminada, Windows PowerShell se ejecuta con la directiva de ejecución de scripting establecida en **Restricted**, lo que evita la ejecución de cualquier script de Windows PowerShell. Para cargar el módulo **sqlps** , puede usar el cmdlet **Set-ExecutionPolicy** para habilitar la ejecución de scripts firmados o de cualquier script. Ejecute solo scripts de orígenes de confianza y proteja todos los archivos de entrada y salida usando los permisos NTFS adecuados. Para obtener más información sobre cómo habilitar scripts de Windows PowerShell, vea cómo [ejecutar scripts de Windows PowerShell](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx).  
  
##  <a name="LoadSqlps"></a> Cargar el módulo sqlps  
 **Para cargar el módulo sqlps en Windows PowerShell**  
  
1.  Use el cmdlet **Set-ExecutionPolicy** para establecer la directiva de ejecución de script apropiada.  
  
2.  Use el cmdlet **Import-Module** para importar el módulo sqlps. Especifique el parámetro **DisableNameChecking** si quiere suprimir la advertencia sobre **Encode-Sqlname** y **Decode-Sqlname**.  
  
### <a name="example"></a>Ejemplo  
 En este ejemplo se carga el módulo de **sqlps** con la comprobación de nombre desactivada.  
  
```powershell 
# Import the SQL Server Module.    
Import-Module Sqlps -DisableNameChecking;

# To check whether the module is installed.
Get-Module -ListAvailable -Name Sqlps;
```  
  
> [!NOTE]  
>  Si el módulo **sqlps** no está en la ruta de acceso, cambie a la ubicación del módulo o use la ruta de acceso completa en el script (con comillas dobles de carpetas en la ruta de acceso que tienen espacios). El módulo **sqlps** se encuentra en la carpeta Tools\Powershell de la instancia de SQL Server.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[&#91;Arriba&#93;]()  
  
## <a name="see-also"></a>Ver también  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [Proveedor de PowerShell de SQL Server](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [Usar los cmdlets del motor de base de datos](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)  
 [Instalación de un módulo de PowerShell](https://msdn.microsoft.com/library/dd878350(v=vs.85).aspx)  
 [Import-Module](https://technet.microsoft.com/library/hh849725.aspx)
  
  
