---
title: Implementar un proyecto de SSIS con código .NET (C#) | Microsoft Docs
ms.date: 09/25/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: quick-start
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0fc40c9db57dece328a8bcc205115c0570a167e9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-an-ssis-project-with-c-code-in-a-net-app"></a>Implementar un proyecto de SSIS con código C# en una aplicación .NET
Este tutorial de inicio rápido muestra cómo escribir código C# para conectarse a un servidor de bases de datos e implementar un proyecto de SSIS.

Para crear una aplicación de C#, puede usar Visual Studio, Visual Studio Code u otra herramienta de su elección.

## <a name="prerequisites"></a>Prerequisites

Antes de empezar, asegúrese de tener instalado Visual Studio o Visual Studio Code. Descargue la edición gratuita de Visual Studio Community Edition o Visual Studio Code desde [Descargas de Visual Studio](https://www.visualstudio.com/downloads/).

> [!NOTE]
> Un servidor Azure SQL Database escucha en el puerto 1433. Si está intentando conectarse a un servidor de Azure SQL Database desde un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

## <a name="get-the-connection-info-if-deployed-to-sql-database"></a>Obtener la información de conexión si la implementación se realiza en SQL Database 

Si sus paquetes se han implementado en Azure SQL Database, obtenga la información de conexión necesaria para conectarse a la base de datos del catálogo de SSIS (SSISDB). Necesita el nombre completo y la información de inicio de sesión del servidor en los procedimientos siguientes.

1. Inicie sesión en el [Portal de Azure](https://portal.azure.com/).
2. Seleccione **Bases de datos SQL** en el menú izquierdo y, a continuación, haga clic en la base de datos SSISDB en la página **Bases de datos SQL**. 
3. En la página **Introducción** de la base de datos, compruebe el nombre completo del servidor. Mantenga el puntero del ratón sobre el nombre del servidor para que aparezca la opción **Haga clic para copiar**. 
4. Si olvida la información de inicio de sesión del servidor de Azure SQL Database, navegue a la página del servidor de SQL Database para ver el nombre del administrador del servidor. Si es necesario, puede restablecer la contraseña.
5. Haga clic en **Mostrar las cadenas de conexión de la base de datos**.
6. Revise la cadena de conexión **ADO.NET** completa. El código de ejemplo usa una clase `SqlConnectionStringBuilder` para volver a crear esta cadena de conexión con los valores de parámetros individuales que ha proporcionado.

## <a name="create-a-new-visual-studio-project"></a>Crear un nuevo proyecto de Visual Studio

1. En Visual Studio, elija **Archivo**, **Nuevo**, **Proyecto**. 
2. En el cuadro de diálogo **Nuevo proyecto**, expanda **Visual C#**.
3. Seleccione **Aplicación de consola** y escriba *deploy_ssis_project* como nombre del proyecto.
4. Haga clic en **Aceptar** para crear y abrir el nuevo proyecto en Visual Studio.

## <a name="add-references"></a>Agregar referencias
1. En el Explorador de soluciones, haga clic con el botón derecho en la carpeta **Referencias** y seleccione **Agregar referencia**. Se abre el cuadro de diálogo **Administrador de referencias**.
2. En el cuadro de diálogo **Administrador de referencias**, expanda **Ensamblados** y seleccione **Extensiones**.
3. Seleccione las dos referencias siguientes para agregarlas:
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. Haga clic en el botón **Examinar** para agregar una referencia a **Microsoft.SqlServer.Management.IntegrationServices**. [Este ensamblado solo se instala en la caché global de ensamblados (GAC)]. Se abre el cuadro de diálogo **Seleccionar archivos para referencia**.
5. En el cuadro de diálogo **Seleccionar archivos para referencia**, vaya a la carpeta de GAC que contiene el ensamblado. Normalmente, esta carpeta es `C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`.
6. Seleccione el ensamblado (es decir, el archivo .dll) en la carpeta y haga clic en **Agregar**.
7. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Administrador de referencias** y agregue las tres referencias. Para asegurarse de que existen las referencias, consulte la lista **Referencias** en el Explorador de soluciones.

## <a name="add-the-c-code"></a>Agregar el código C# 
1. Abra **Program.cs**.

2. Reemplace el contenido de **Program.cs** por el código siguiente. Agregue los valores adecuados para el servidor, la base de datos, el usuario y la contraseña.

> [!NOTE]
> En el ejemplo siguiente se usa la autenticación de Windows. Para usar la autenticación de SQL Server, reemplace el argumento `Integrated Security=SSPI;` por `User ID=<user name>;Password=<password>;`.

```csharp
using Microsoft.SqlServer.Management.IntegrationServices;
using System;
using System.Data.SqlClient;
using System.IO;

namespace deploy_ssis_project
{
    class Program
    {
        static void Main(string[] args)
        {
            // Variables
            string targetServerName = "localhost";
            string targetFolderName = "Project1Folder";
            string projectName = "Integration Services Project1";
            string projectFilePath = @"C:\Projects\Integration Services Project1\Integration Services Project1\bin\Development\Integration Services Project1.ispac";

            // Create a connection to the server
            string sqlConnectionString = "Data Source=" + targetServerName +
                ";Initial Catalog=master;Integrated Security=SSPI;";
            SqlConnection sqlConnection = new SqlConnection(sqlConnectionString);

            // Create the Integration Services object
            IntegrationServices integrationServices = new IntegrationServices(sqlConnection);

            // Get the Integration Services catalog
            Catalog catalog = integrationServices.Catalogs["SSISDB"];

            // Create the target folder
            CatalogFolder folder = new CatalogFolder(catalog,
                targetFolderName, "Folder description");
            folder.Create();

            Console.WriteLine("Deploying " + projectName + " project.");

            byte[] projectFile = File.ReadAllBytes(projectFilePath);
            folder.DeployProject(projectName, projectFile);

            Console.WriteLine("Done.");
        }
    }
}
```

## <a name="run-the-code"></a>Ejecutar el código

1. Presione **F5** para ejecutar la aplicación.
2. En SSMS, compruebe que se ha implementado el proyecto.

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas de implementar un paquete.
    - [Implementar un paquete SSIS con SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implementar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Deploy an SSIS package with Transact-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md) [Implementar un paquete SSIS con Transact-SQL (VSCode)]
    - [Deploy an SSIS package from the command prompt](./ssis-quickstart-deploy-cmdline.md) (Implementar un paquete SSIS desde el símbolo del sistema)
    - [Deploy an SSIS package with PowerShell](ssis-quickstart-deploy-powershell.md) (Implementar un paquete SSIS con PowerShell)
- Ejecutar un paquete implementado. Para ejecutar un paquete, puede elegir entre varias herramientas y lenguajes. Para obtener más información, vea los artículos siguientes:
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Run an SSIS package with Transact-SQL (SSMS) (Ejecutar un paquete SSIS con Transact-SQL [SSMS])](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS desde el símbolo del sistema](./ssis-quickstart-run-cmdline.md)
    - [Run an SSIS package with PowerShell](ssis-quickstart-run-powershell.md) (Ejecutar un paquete de SSIS con PowerShell)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 
