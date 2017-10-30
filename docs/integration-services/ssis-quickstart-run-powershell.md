---
title: Ejecutar un paquete SSIS con PowerShell | Documentos de Microsoft
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: d392ac49442ef0f04961908fff7acf553fa1aa57
ms.contentlocale: es-es
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-powershell"></a>Ejecutar un paquete SSIS con PowerShell
Este tutorial de inicio rápido muestra cómo usar un script de PowerShell para conectarse a un servidor de base de datos y ejecutar un paquete SSIS.

## <a name="powershell-script"></a>Script de PowerShell
Proporcione los valores adecuados para las variables en la parte superior de la secuencia de comandos siguiente y, a continuación, ejecute el script para ejecutar el paquete SSIS.

> [!NOTE]
> En el ejemplo siguiente se utiliza la autenticación de Windows. Para usar autenticación de SQL Server, reemplace la `Integrated Security=SSPI;` argumento con `User ID=<user name>;Password=<password>;`.

```powershell
# Variables
$SSISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"
$TargetServerName = "localhost"
$TargetFolderName = "Project1Folder"
$ProjectName = "Integration Services Project1"
$PackageName = "Package.dtsx"

# Load the IntegrationServices assembly
$loadStatus = [System.Reflection.Assembly]::Load("Microsoft.SQLServer.Management.IntegrationServices, "+
    "Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91, processorArchitecture=MSIL")

# Create a connection to the server
$sqlConnectionString = `
    "Data Source=" + $TargetServerName + ";Initial Catalog=master;Integrated Security=SSPI;"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $SSISNamespace".IntegrationServices" $sqlConnection

# Get the Integration Services catalog
$catalog = $integrationServices.Catalogs["SSISDB"]

# Get the folder
$folder = $catalog.Folders[$TargetFolderName]

# Get the project
$project = $folder.Projects[$ProjectName]

# Get the package
$package = $project.Packages[$PackageName]

Write-Host "Running " $PackageName "..."

$result = $package.Execute("false", $null)

Write-Host "Done."
```

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas para ejecutar un paquete.
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS desde la línea de comandos](./ssis-quickstart-run-cmdline.md)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 

