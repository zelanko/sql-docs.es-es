---
title: Implementar un proyecto de SSIS con SSMS | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: quick-start
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c13783a7bbd5a23c2329151932f4438255babb9b
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>Implementar un proyecto de SSIS con SQL Server Management Studio (SSMS)
En esta guía de inicio rápido se muestra cómo usar SQL Server Management Studio (SSMS) para conectarse a la base de datos del catálogo de SSIS, y cómo ejecutar el Asistente para implementación de Integration Services para implementar un proyecto de SSIS en el catálogo de SSIS. 

SQL Server Management Studio es un entorno integrado para administrar cualquier infraestructura de SQL, desde SQL Server a SQL Database. Para obtener más información acerca de SSMS, consulte [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Prerequisites

Antes de comenzar, asegúrese de que tiene instalada la última versión de SQL Server Management Studio. Para descargar SSMS, consulte [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) [Descargar SQL Server Management Studio (SSMS)].

## <a name="connect-to-the-ssisdb-database"></a>Conectarse a la base de datos de SSISDB

Use SQL Server Management Studio para establecer una conexión con el catálogo de SSIS. 

> [!NOTE]
> Un servidor Azure SQL Database escucha en el puerto 1433. Si está intentando conectarse a un servidor de Azure SQL Database desde un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

1. Abra SQL Server Management Studio.

2. En el cuadro de diálogo **Conectar con el servidor**, escriba la información siguiente:

   | Configuración       | Valor sugerido | Más información | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | Nombre completo del servidor | Si se está conectando a un servidor de Azure SQL Database, el nombre tendrá este formato: `<server_name>.database.windows.net`. |
   | **Autenticación** | Autenticación de SQL Server | Esta guía de inicio rápido usa la autenticación SQL. |
   | **Inicio de sesión** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |

3. Haga clic en **Conectar**. La ventana Explorador de objetos se abre en SSMS. 

4. En el Explorador de objetos, expanda la opción **Catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos de la base de datos del catálogo de SSIS.

## <a name="start-the-integration-services-deployment-wizard"></a>Iniciar el Asistente para implementación de Integration Services
1. En el Explorador de objetos, con el nodo **Catálogos de Integration Services** y el nodo **SSISDB** expandidos, expanda una carpeta de proyecto.

2.  Seleccione el nodo **Proyectos**.

3.  Haga doble clic en el nodo **Proyectos** y seleccione **Implementar proyecto**. Se abre el Asistente para implementación de Integration Services. Puede implementar un proyecto desde el catálogo actual o desde el sistema de archivos.

## <a name="deploy-a-project-with-the-wizard"></a>Implementar un proyecto con el asistente
1. En la página **Introducción** del asistente, revise la introducción. Haga clic en **Siguiente** para abrir la página **Seleccionar origen**.

2. En la página **Seleccionar origen**, seleccione el proyecto SSIS existente que hay que implementar.
    -   Para implementar un archivo de implementación de proyectos que haya creado, seleccione **Archivo de implementación de proyecto** y especifique la ruta de acceso del archivo .ispac.
    -   Para implementar un proyecto que resida en un catálogo de SSIS, seleccione **Catálogo de Integration Services** y especifique el nombre del servidor y la ruta de acceso al proyecto en el catálogo.
    Haga clic en **Siguiente** para ver la página **Seleccionar destino** .
  
3.  En la página **Seleccionar destino**, seleccione el destino del proyecto.
    -   Escriba el nombre completo del servidor. Si el servidor de destino es un servidor de Azure SQL Database, el nombre tendrá este formato: `<server_name>.database.windows.net`.
    -   A continuación, haga clic en **Examinar** para seleccionar la carpeta de destino en SSISDB.
    Haga clic en **Siguiente** para abrir la página **Revisión**.  
  
4.  En la página **Revisión**, revise la configuración seleccionada.
    -   Puede cambiar las selecciones si hace clic en **Anterior**o si hace clic en cualquiera de los pasos del panel izquierdo.
    -   Haga clic en **Implementar** para iniciar el proceso de implementación.
  
5.  Una vez completado el proceso de implementación, se abrirá la página **Resultados**. Esta página muestra si cada acción si se completó correctamente o no.
    -   Si se produce un error en la acción, haga clic en **Error** en la columna **Resultado** para que aparezca una explicación del error.
    -   De forma opcional, puede hacer clic en **Guardar informe** para guardar los resultados en un archivo XML.
    -   Haga clic en **Cerrar** para salir del asistente.

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas de implementar un paquete.
    - [Deploy an SSIS package with Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md) [Implementar un paquete SSIS con Transact-SQL (SSMS)]
    - [Deploy an SSIS package with Transact-SQL (VS Code)](ssis-quickstart-deploy-tsql-vscode.md) [Implementar un paquete SSIS con Transact-SQL (VSCode)]
    - [Deploy an SSIS package from the command prompt](./ssis-quickstart-deploy-cmdline.md) (Implementar un paquete SSIS desde el símbolo del sistema)
    - [Deploy an SSIS package with PowerShell](ssis-quickstart-deploy-powershell.md) (Implementar un paquete SSIS con PowerShell)
    - [Deploy an SSIS package with C#](./ssis-quickstart-deploy-dotnet.md) (Implementar un paquete SSIS con C#) 
- Ejecute un paquete implementado. Para ejecutar un paquete, puede elegir entre varias herramientas y lenguajes. Para obtener más información, vea los artículos siguientes:
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Run an SSIS package with Transact-SQL (SSMS) (Ejecutar un paquete SSIS con Transact-SQL [SSMS])](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS desde el símbolo del sistema](./ssis-quickstart-run-cmdline.md)
    - [Run an SSIS package with PowerShell](ssis-quickstart-run-powershell.md) (Ejecutar un paquete de SSIS con PowerShell)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 
