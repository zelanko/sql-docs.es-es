---
title: Implementar un proyecto de SSIS con Transact-SQL (SSMS) | Documentos de Microsoft
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: e97fb20f5b0ee10aa3e5de690676b7e0bb797b4c
ms.contentlocale: es-es
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-from-ssms-with-transact-sql"></a>Implementar un proyecto de SSIS de SSMS con Transact-SQL

Este inicio rápido muestra cómo usar SQL Server Management Studio (SSMS) para conectarse a la base de datos de catálogo de SSIS y, a continuación, utilice las instrucciones de Transact-SQL para implementar un proyecto de SSIS en el catálogo de SSIS. 

> [!NOTE]
> El método descrito en este artículo no está disponible cuando se conecta a un servidor de base de datos de SQL Azure con SSMS. El `catalog.deploy_project` procedimiento almacenado espera que la ruta de acceso a la `.ispac` archivo en el sistema de archivos local (local).

SQL Server Management Studio es un entorno integrado para administrar cualquier infraestructura de SQL de SQL Server a la base de datos SQL. Para obtener más información acerca de SSMS, vea [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que tiene la última versión de SQL Server Management Studio. Para descargar SSMS, vea [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssis-catalog-database"></a>Conectarse a la base de datos de catálogo de SSIS

Usar SQL Server Management Studio para establecer una conexión con el catálogo de SSIS. 

> [!NOTE]
> Un servidor de base de datos de SQL Azure escucha en el puerto 1433. Si está intentando conectarse a un servidor de base de datos de SQL Azure desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

1. Abra SQL Server Management Studio.

2. En el **conectar al servidor** diálogo cuadro, escriba la siguiente información:

   | Configuración       | Valor recomendado | Más información | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | El nombre completo del servidor |  |
   | **Autenticación** | Autenticación de SQL Server | Este tutorial rápido usa la autenticación de SQL. |
   | **Inicio de sesión** | La cuenta de administrador de servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | La contraseña de la cuenta de administrador del servidor | Esta es la contraseña que especificó cuando creó el servidor. |

3. Haga clic en **Conectar**. Se abre la ventana de explorador de objetos en SSMS. 

4. En el Explorador de objetos, expanda **catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos en la base de datos de catálogo de SSIS.

## <a name="run-the-t-sql-code"></a>Ejecute el código de T-SQL
Ejecute el siguiente código de Transact-SQL para implementar un proyecto de SSIS.

1.  En SSMS, abra una nueva ventana de consulta y pegue el código siguiente.

2.  Actualice los valores de parámetro en el `catalog.deploy_project` procedimiento almacenado para el sistema.

3.  Asegúrese de que SSISDB es la base de datos actual.

4.  Ejecute el script.

5. En el Explorador de objetos, actualice el contenido de **SSISDB** si es necesario y compruebe si el proyecto que ha implementado.

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
    - [Implementar un paquete SSIS con SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implementar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Implementar un paquete SSIS desde el símbolo del sistema](./ssis-quickstart-deploy-cmdline.md)
    - [Implementar un paquete SSIS con PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Implementar un paquete SSIS con C#](./ssis-quickstart-deploy-dotnet.md) 
- Ejecutar un paquete implementado. Para ejecutar un paquete, puede elegir entre varias herramientas y lenguajes. Para obtener más información, vea los siguientes artículos:
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS desde la línea de comandos](./ssis-quickstart-run-cmdline.md)
    - [Ejecutar un paquete SSIS con PowerShell](ssis-quickstart-run-powershell.md)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 

