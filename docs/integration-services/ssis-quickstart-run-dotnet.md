---
title: "Ejecutar un proyecto de SSIS con el código de .NET (C#) | Documentos de Microsoft"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: 65a8db27af80e5cd7001e9a8777dde3c59e9c55e
ms.contentlocale: es-es
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-c-code-in-a-net-app"></a>Ejecutar un paquete SSIS con código C# en una aplicación .NET
Este tutorial de inicio rápido muestra cómo escribir código C# para conectarse a un servidor de base de datos y ejecutar un paquete SSIS.

Puede usar Visual Studio, código de Visual Studio u otra herramienta de su elección para crear una aplicación de C#.

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que está instalado Visual Studio o código de Visual Studio. Descargar la edición gratuita Community de Visual Studio o el libre Visual Studio Code, de [descargas de Visual Studio](https://www.visualstudio.com/downloads/).

> [!NOTE]
> Un servidor de base de datos de SQL Azure escucha en el puerto 1433. Si está intentando conectarse a un servidor de base de datos de SQL Azure desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

## <a name="get-the-connection-info-if-deployed-to-sql-database"></a>Obtener la información de conexión si se implementa en la base de datos SQL

Si los paquetes se implementan en una base de datos de SQL Azure, obtenga la información de conexión que necesaria para conectarse a la base de datos de catálogo de SSIS (SSISDB). Necesita la información de nombre y el inicio de sesión del nombre completo del servidor en los procedimientos siguientes.

1. Inicie sesión en el [Portal de Azure](https://portal.azure.com/).
2. Seleccione **bases de datos SQL** en el menú izquierdo y haga clic en la base de datos de SSISDB en el **bases de datos SQL** página. 
3. En el **Introducción** página de la base de datos, revise el nombre completo del servidor. Para que aparezca el **haga clic aquí para copiar** opción, mantenga el mouse sobre el nombre del servidor. 
4. Si olvida la información de inicio de sesión del servidor de base de datos de SQL Azure, navegue a la página de base de datos de SQL server para ver el nombre del Administrador de servidor. Puede restablecer la contraseña si es necesario.
5. Haga clic en **mostrar cadenas de conexión de base de datos**.
6. Revise la sección completa **ADO.NET** cadena de conexión. El código de ejemplo utiliza un `SqlConnectionStringBuilder` para volver a crear esta cadena de conexión con los valores de parámetro individual que proporcionan.

## <a name="create-a-new-visual-studio-project"></a>Crear un nuevo proyecto de Visual Studio

1. En Visual Studio, elija **archivo**, **New**, **proyecto**. 
2. En el **nuevo proyecto** cuadro de diálogo y expanda **Visual C#**.
3. Seleccione **aplicación de consola** y escriba *run_ssis_project* como nombre del proyecto.
4. Haga clic en **Aceptar** para crear y abrir el nuevo proyecto en Visual Studio.

## <a name="add-references"></a>Agregar referencias
1. En el Explorador de soluciones, haga clic en el **referencias** carpeta y seleccione **Agregar referencia**. El **Administrador de referencias** abre el cuadro de diálogo.
2. En el **Administrador de referencias** cuadro de diálogo, expanda **ensamblados** y seleccione **extensiones**.
3. Seleccione las dos referencias siguientes para agregar:
    -   Microsoft.SqlServer.Management.Sdk.Sfc
    -   Microsoft.SqlServer.Smo
4. Haga clic en el **examinar** botón para agregar una referencia a **Microsoft.SqlServer.Management.IntegrationServices**. (Este ensamblado se instala solo en la caché global de ensamblados (GAC).) El **seleccione los archivos para hacer referencia a** abre el cuadro de diálogo.
5. En el **seleccione los archivos para hacer referencia a** diálogo cuadro, vaya a la carpeta de la GAC que contiene el ensamblado. Normalmente, esta carpeta es `C:\Windows\assembly\GAC_MSIL\Microsoft.SqlServer.Management.IntegrationServices\14.0.0.0__89845dcd8080cc91`.
6. Seleccione el ensamblado (es decir, el archivo .dll) en la carpeta y haga clic en **agregar**.
7. Haga clic en **Aceptar** para cerrar el **Administrador de referencias** diálogo cuadro y agregue las tres referencias. Para asegurarse de que existen las referencias, compruebe el **referencias** lista en el Explorador de soluciones.

## <a name="add-the-c-code"></a>Agregue el código de C# 
1. Abra **Program.cs**.

2. Reemplace el contenido de **Program.cs** con el código siguiente. Agregue los valores adecuados para el servidor, la base de datos, el usuario y la contraseña.

> [!NOTE]
> En el ejemplo siguiente se utiliza la autenticación de Windows. Para usar autenticación de SQL Server, reemplace la `Integrated Security=SSPI;` argumento con `User ID=<user name>;Password=<password>;`.


```csharp
using Microsoft.SqlServer.Management.IntegrationServices;
using System.Data.SqlClient;

namespace run_ssis_package
{
    class Program
    {
        static void Main(string[] args)
        {
            // Variables
            string targetServerName = "localhost";
            string folderName = "Project1Folder";
            string projectName = "Integration Services Project1";
            string packageName = "Package.dtsx";

            // Create a connection to the server
            string sqlConnectionString = "Data Source=" + targetServerName +
                ";Initial Catalog=master;Integrated Security=SSPI;";
            SqlConnection sqlConnection = new SqlConnection(sqlConnectionString);

            // Create the Integration Services object
            IntegrationServices integrationServices = new IntegrationServices(sqlConnection);

            // Get the Integration Services catalog
            Catalog catalog = integrationServices.Catalogs["SSISDB"];

            // Get the folder
            CatalogFolder folder = catalog.Folders[folderName];

            // Get the project
            ProjectInfo project = folder.Projects[projectName];

            // Get the package
            PackageInfo package = project.Packages[packageName];

            // Run the package
            package.Execute(false, null);

        }
    }
}
```

## <a name="run-the-code"></a>Ejecute el código

1. Para ejecutar la aplicación, presione **F5**.
2. Compruebe que el paquete se ejecute según lo previsto y, a continuación, cierre la ventana de la aplicación.

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas para ejecutar un paquete.
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS desde la línea de comandos](./ssis-quickstart-run-cmdline.md)
    - [Ejecutar un paquete SSIS con PowerShell](ssis-quickstart-run-powershell.md)

