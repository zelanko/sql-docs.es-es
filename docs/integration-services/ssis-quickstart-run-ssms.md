---
title: Ejecutar un paquete SSIS con SSMS | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7b35bade8769e3de11f60046375f082146da579d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>Ejecutar un paquete SSIS con SQL Server Management Studio (SSMS)
En esta guía de inicio rápido se muestra cómo usar SQL Server Management Studio (SSMS) para conectarse a la base de datos del catálogo de SSIS, y cómo ejecutar un paquete SSIS almacenado en el catálogo de SSIS desde el Explorador de objetos en SSMS.

SQL Server Management Studio es un entorno integrado para administrar cualquier infraestructura de SQL, desde SQL Server a SQL Database. Para obtener más información acerca de SSMS, consulte [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de comenzar, asegúrese de que tiene instalada la última versión de SQL Server Management Studio (SSMS). Para descargar SSMS, consulte [Descarga de SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Conectarse a la base de datos de SSISDB

Use SQL Server Management Studio para establecer una conexión con el catálogo de SSIS. 

> [!NOTE]
> Un servidor Azure SQL Database se escucha en el puerto 1433. Si está intentando conectarse a un servidor de Azure SQL Database desde un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

1. Abra SQL Server Management Studio.

2. Escriba la información siguiente en el cuadro de diálogo **Conectarse al servidor**:

   | Configuración       | Valor sugerido | Más información | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | Nombre completo del servidor | Si se está conectando a un servidor de Azure SQL Database, el nombre tendrá este formato: `<server_name>.database.windows.net`. |
   | **Autenticación** | Autenticación de SQL Server | Esta guía de inicio rápido usa la autenticación SQL. |
   | **Inicio de sesión** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |

3. Haga clic en **Conectar**. La ventana Explorador de objetos se abre en SSMS. 

4. En el Explorador de objetos, expanda la opción **Catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos de la base de datos del catálogo de SSIS.

## <a name="run-a-package"></a>Ejecutar un paquete

1. En el Explorador de objetos, seleccione el paquete que quiere ejecutar.

2. Haga clic con el botón derecho y seleccione **Ejecutar**. Se abrirá el cuadro de diálogo **Ejecutar paquete**.

3.  Configure la ejecución del paquete mediante las opciones de las pestañas **Parámetros**, **Administradores de conexión** y **Opciones avanzadas** del cuadro de diálogo Ejecutar paquete.

4.  Haga clic en Aceptar para ejecutar el paquete.

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas de ejecutar un paquete.
    - [Run an SSIS package with Transact-SQL (SSMS) (Ejecutar un paquete SSIS con Transact-SQL [SSMS])](./ssis-quickstart-run-tsql-ssms.md)
    - [Run an SSIS package with Transact-SQL (VS Code) (Ejecutar un paquete SSIS con Transact-SQL [VS Code])](ssis-quickstart-run-tsql-vscode.md)
    - [Run an SSIS package from the command prompt (Ejecutar un paquete SSIS desde el símbolo del sistema)](./ssis-quickstart-run-cmdline.md)
    - [Run an SSIS package with PowerShell (Ejecutar un paquete SSIS con PowerShell)](ssis-quickstart-run-powershell.md)
    - [Run an SSIS package with C# (Ejecutar un paquete SSIS con C#)](./ssis-quickstart-run-dotnet.md) 
