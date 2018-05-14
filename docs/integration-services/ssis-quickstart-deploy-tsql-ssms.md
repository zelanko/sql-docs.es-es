---
title: Implementar un proyecto de SSIS con Transact-SQL (SSMS) | Microsoft Docs
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
ms.openlocfilehash: 975bf68b5d3255ff965e9092e84b2dabf982b90b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>Implementar un proyecto de SSIS desde SSMS con Transact-SQL

En esta guía de inicio rápido se muestra cómo usar SQL Server Management Studio (SSMS) para conectarse a la base de datos del catálogo de SSIS, y cómo usar las instrucciones Transact-SQL para implementar un proyecto de SSIS en el catálogo de SSIS. 

> [!NOTE]
> El método que se describe en este artículo no está disponible cuando se conecta a un servidor de Azure SQL Database con SSMS. El procedimiento almacenado `catalog.deploy_project` espera la ruta de acceso al archivo `.ispac` en el sistema de archivos local.

SQL Server Management Studio es un entorno integrado para administrar cualquier infraestructura de SQL, desde SQL Server a SQL Database. Para obtener más información acerca de SSMS, consulte [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Prerequisites

Antes de comenzar, asegúrese de que tiene instalada la última versión de SQL Server Management Studio. Para descargar SSMS, consulte [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) [Descargar SQL Server Management Studio (SSMS)].

## <a name="connect-to-the-ssis-catalog-database"></a>Conectar con la base de datos del catálogo de SSIS

Use SQL Server Management Studio para establecer una conexión con el catálogo de SSIS. 

> [!NOTE]
> Un servidor Azure SQL Database escucha en el puerto 1433. Si está intentando conectarse a un servidor de Azure SQL Database desde un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

1. Abra SQL Server Management Studio.

2. En el cuadro de diálogo **Conectar con el servidor**, escriba la información siguiente:

   | Configuración       | Valor sugerido | Más información | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | Nombre completo del servidor |  |
   | **Autenticación** | Autenticación de SQL Server | Esta guía de inicio rápido usa la autenticación SQL. |
   | **Inicio de sesión** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |

3. Haga clic en **Conectar**. La ventana Explorador de objetos se abre en SSMS. 

4. En el Explorador de objetos, expanda la opción **Catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos de la base de datos del catálogo de SSIS.

## <a name="run-the-t-sql-code"></a>Ejecutar el código T-SQL
Ejecute el siguiente código Transact-SQL para implementar un proyecto de SSIS.

1.  En SSMS, abra una ventana de consulta nueva y pegue el siguiente código.

2.  Actualice los valores de parámetro del procedimiento almacenado `catalog.deploy_project` del sistema.

3.  Asegúrese de que SSISDB es la base de datos actual.

4.  Ejecute el script.

5. En el Explorador de objetos, actualice el contenido de **SSISDB** si es necesario y compruebe el proyecto que ha implementado.

```sql
DECLARE @ProjectBinary AS varbinary(max)
DECLARE @operation_id AS bigint
SET @ProjectBinary =
    (SELECT * FROM OPENROWSET(BULK '<project_file_path>.ispac', SINGLE_BLOB) AS BinaryData)

EXEC catalog.deploy_project @folder_name = '<target_folder>',
    @project_name = '<project_name',
    @Project_Stream = @ProjectBinary,
    @operation_id = @operation_id out
```

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas de implementar un paquete.
    - [Deploy an SSIS package with SSMS](./ssis-quickstart-deploy-ssms.md) (Implementar un paquete SSIS con SSMS)
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
