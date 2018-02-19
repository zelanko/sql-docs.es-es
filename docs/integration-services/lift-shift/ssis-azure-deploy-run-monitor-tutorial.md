---
title: Implementar, ejecutar y supervisar un paquete SSIS en Azure | Microsoft Docs
ms.date: 02/05/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: aa1cc5db91745fb7773856a8f66b03c82bba3e9a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="deploy-run-and-monitor-an-ssis-package-on-azure"></a>Implementar, ejecutar y supervisar un paquete SSIS en Azure
Este tutorial muestra cómo implementar un proyecto de SQL Server Integration Services para la base de datos del catálogo de SSISDB en Azure SQL Database, ejecutar un paquete en Azure-SSIS Integration Runtime y supervisar el paquete en ejecución.

## <a name="prerequisites"></a>Prerequisites

Antes de comenzar, asegúrese de que tiene instalada la versión 17.2 (o posterior) de SQL Server Management Studio. Para descargar la versión más reciente de SSMS, consulte [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) [Descargar SQL Server Management Studio (SSMS)].

Asegúrese también de que la base de datos SSISDB esté configurada y Azure-SSIS Integration Runtime aprovisionado. Para obtener información sobre el aprovisionamiento de SSIS en Azure, consulte [Lift and shift SQL Server Integration Services (SSIS) packages to Azure](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure) [Migrar paquetes de SQL Server Integration Services (SSIS) a Azure mediante lift-and-shift].

## <a name="connect-to-the-ssisdb-database"></a>Conectarse a la base de datos de SSISDB

Use SQL Server Management Studio para conectarse al catálogo de SSIS en el servidor de Azure SQL Database. Para obtener más información, consulte [Connect to the SSISDB Catalog database on Azure](ssis-azure-connect-to-catalog-database.md) (Conectarse a la base de datos del catálogo de SSISDB en Azure).

> [!IMPORTANT]
> Un servidor Azure SQL Database escucha en el puerto 1433. Si está intentando conectarse a un servidor de Azure SQL Database desde un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

1. Abra SQL Server Management Studio.

2. **Conéctese al servidor**. En el cuadro de diálogo **Conectar con el servidor**, escriba la información siguiente:

   | Configuración       | Valor sugerido | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | Nombre completo del servidor | El nombre debe tener este formato: **mysqldbserver.database.windows.net**. Para obtener más información, consulte [Connect to the SSISDB Catalog database on Azure](ssis-azure-connect-to-catalog-database.md) (Conectarse a la base de datos del catálogo de SSISDB en Azure). |
   | **Autenticación** | Autenticación de SQL Server | Esta guía de inicio rápido usa la autenticación SQL. |
   | **Inicio de sesión** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |

3. **Conéctese a la base de datos de SSISDB**. Seleccione **Opciones** para expandir el cuadro de diálogo **Conectar con el servidor**. En el cuadro de diálogo **Conectar con el servidor** expandido, seleccione la pestaña **Propiedades de conexión**. En el campo **Conectar con base de datos**, seleccione o escriba `SSISDB`.

4. A continuación, seleccione **Conectar**. La ventana Explorador de objetos se abre en SSMS. 

5. En el Explorador de objetos, expanda la opción **Catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos de la base de datos del catálogo de SSIS.

## <a name="deploy-a-project-with-the-deployment-wizard"></a>Implementar un proyecto con el Asistente para implementación

### <a name="start-the-integration-services-deployment-wizard"></a>Iniciar el Asistente para implementación de Integration Services
1. En el Explorador de objetos de SSMS, con el nodo **Catálogos de Integration Services** y el nodo **SSISDB** expandidos, expanda una carpeta de proyecto.

2.  Seleccione el nodo **Proyectos**.

3.  Haga doble clic en el nodo **Proyectos** y seleccione **Implementar proyecto**. Se abre el Asistente para implementación de Integration Services. Puede implementar un proyecto desde una base de datos del catálogo de SSIS o desde el sistema de archivos.

### <a name="deploy-a-project-with-the-deployment-wizard"></a>Implementar un proyecto con el Asistente para implementación
1. En la página **Introducción** del Asistente para implementación, revise la introducción. Seleccione **Siguiente** para abrir la página **Seleccionar origen**.

2. En la página **Seleccionar origen**, seleccione el proyecto SSIS existente que hay que implementar.
    -   Para implementar un archivo de implementación de proyectos que haya creado, seleccione **Archivo de implementación de proyecto** y especifique la ruta de acceso del archivo .ispac.
    -   Para implementar un proyecto que resida en un catálogo de SSIS, seleccione **Catálogo de Integration Services** y especifique el nombre del servidor y la ruta de acceso al proyecto en el catálogo.
    -   Seleccione **Siguiente** para ver la página **Seleccionar destino**.
  
3.  En la página **Seleccionar destino**, seleccione el destino del proyecto.
    -   Escriba el nombre completo del servidor con el formato `<server_name>.database.windows.net`.
    -   A continuación, haga clic en **Examinar** para seleccionar la carpeta de destino de SSISDB.
    -   Seleccione **Siguiente** para abrir la página **Revisión**.  
  
4.  En la página **Revisión**, revise la configuración seleccionada.
    -   Puede cambiar las selecciones si hace clic en **Anterior** o en cualquiera de los pasos del panel izquierdo.
    -   Seleccione **Implementar** para iniciar el proceso de implementación.

    > ![NOTA] Si recibe el mensaje de error **No hay ningún agente de trabajo activo (proveedor de datos .NetSqlClient)**, asegúrese de que se está ejecutando Azure-SSIS IR. Este error se produce si intenta implementar mientras Azure-SSIS IR está en estado detenido.

5.  Una vez completado el proceso de implementación, se abrirá la página **Resultados**. Esta página muestra si cada acción si se completó correctamente o no.
    -   Si la acción no se realiza correctamente, seleccione **Error** en la columna **Resultado** para que aparezca una explicación del error.
    -   De forma opcional, seleccione **Guardar informe** para guardar los resultados en un archivo XML.
    -   Seleccione **Cerrar** para salir del asistente.

## <a name="deploy-a-project-with-powershell"></a>Implementar un proyecto con PowerShell

Para implementar un proyecto con PowerShell en SSISDB en Azure SQL Database, adapte el siguiente script según sus requisitos:

```powershell
# Variables
$ProjectFilePath = "C:\<folder>"
$SSISDBServerEndpoint = "<servername>.database.windows.net"
$SSISDBServerAdminUserName = "<username>"
$SSISDBServerAdminPassword = "<password>"

# Load the IntegrationServices Assembly
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices") | Out-Null;

# Store the IntegrationServices Assembly namespace to avoid typing it every time
$ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"

Write-Host "Connecting to server ..."

# Create a connection to the server
$sqlConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword + ";Initial Catalog=SSISDB"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection

# Get the catalog
$catalog = $integrationServices.Catalogs['SSISDB']

write-host "Enumerating all folders..."

$folders = ls -Path $ProjectFilePath -Directory

if ($folders.Count -gt 0)
{
    foreach ($filefolder in $folders)
    {
        Write-Host "Creating Folder " $filefolder.Name " ..."

        # Create a new folder
        $folder = New-Object $ISNamespace".CatalogFolder" ($catalog, $filefolder.Name, "Folder description")
        $folder.Create()

        $projects = ls -Path $filefolder.FullName -File -Filter *.ispac
        if ($projects.Count -gt 0)
        {
            foreach($projectfile in $projects)
            {
                $projectfilename = $projectfile.Name.Replace(".ispac", "")
                Write-Host "Deploying " $projectfilename " project ..."

                # Read the project file, and deploy it to the folder
                [byte[]] $projectFileContent = [System.IO.File]::ReadAllBytes($projectfile.FullName)
                $folder.DeployProject($projectfilename, $projectFileContent)
            }
        }
    }
}

Write-Host "All done." 
```

## <a name="run-a-package"></a>Ejecutar un paquete

1. En el Explorador de objetos de SSMS, seleccione el paquete que quiere ejecutar.

2. Haga clic con el botón derecho y seleccione **Ejecutar** para abrir el cuadro de diálogo **Ejecutar paquete**.

3.  En el cuadro de diálogo **Ejecutar paquete**, configure la ejecución del paquete mediante las opciones de las pestañas **Parámetros**, **Administradores de conexión** y **Avanzadas**.

4.  Seleccione **Aceptar** para ejecutar el paquete.

## <a name="monitor-the-running-package-in-ssms"></a>Supervisar el paquete en ejecución en SSMS

Para ver el estado de las operaciones de Integration Services que se están ejecutando actualmente en el servidor de Integration Services, como las de implementación, validación y ejecución del paquete, use el cuadro de diálogo **Operaciones activas** de SSMS. Para abrir el cuadro de diálogo **Operaciones activas**, haga clic con el botón derecho en **SSISDB** y, a continuación, seleccione **Operaciones activas**.

También puede seleccionar un paquete en el Explorador de objetos, hacer clic con el botón derecho y seleccionar **Informes**. A continuación, elija **Informes estándar** y **Todas las ejecuciones**.

Para obtener más información sobre cómo supervisar paquetes en ejecución en SSMS, vea [Monitor Running Packages and Other Operations](https://docs.microsoft.com/sql/integration-services/performance/monitor-running-packages-and-other-operations) (Supervisar paquetes en ejecución y otras operaciones).

## <a name="monitor-the-azure-ssis-integration-runtime"></a>Supervisar Azure-SSIS Integration Runtime

Para obtener información de estado sobre la instancia de Azure-SSIS Integration Runtime donde se ejecutan los paquetes, use los siguientes comandos de PowerShell: para cada uno de los comandos, proporcione los nombres de Data Factory, la instancia de Azure-SSIS IR y el grupo de recursos.

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>Obtener los metadatos de Azure-SSIS Integration Runtime

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>Obtener el estado de Azure-SSIS Integration Runtime

```powershell
Get-AzureRmDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>Pasos siguientes
- Aprenda a programar la ejecución de paquetes. Para obtener más información, consulte [Schedule SSIS package execution on Azure](ssis-azure-schedule-packages.md) (Programar la ejecución de paquetes de SSIS en Azure).
