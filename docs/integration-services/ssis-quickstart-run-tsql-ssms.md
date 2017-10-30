---
title: Ejecutar un paquete SSIS con Transact-SQL (SSMS) | Documentos de Microsoft
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
ms.openlocfilehash: 1c656661f645ac9f5d1659800893290819525f39
ms.contentlocale: es-es
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-ssms-with-transact-sql"></a>Ejecutar un paquete SSIS de SSMS con Transact-SQL
Este inicio rápido muestra cómo usar SQL Server Management Studio (SSMS) para conectarse a la base de datos de catálogo de SSIS y, a continuación, utilizar instrucciones Transact-SQL para ejecutar un paquete SSIS que se almacenan en el catálogo de SSIS.

SQL Server Management Studio es un entorno integrado para administrar cualquier infraestructura de SQL de SQL Server a la base de datos SQL. Para obtener más información acerca de SSMS, vea [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que tiene la versión más reciente de SQL Server Management Studio (SSMS). Para descargar SSMS, vea [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Conectarse a la base de datos SSISDB

Usar SQL Server Management Studio para establecer una conexión con el catálogo de SSIS en el servidor de base de datos de SQL Azure. 

> [!NOTE]
> Un servidor de base de datos de SQL Azure escucha en el puerto 1433. Si está intentando conectarse a un servidor de base de datos de SQL Azure desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

1. Abra SQL Server Management Studio.

2. En el **conectar al servidor** diálogo cuadro, escriba la siguiente información:

   | Configuración       | Valor recomendado | Más información | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | El nombre completo del servidor | Si se está conectando a un servidor de base de datos de SQL Azure, el nombre está en este formato: `<server_name>.database.windows.net`. |
   | **Autenticación** | Autenticación de SQL Server | Este tutorial rápido usa la autenticación de SQL. |
   | **Inicio de sesión** | La cuenta de administrador de servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | La contraseña de la cuenta de administrador del servidor | Esta es la contraseña que especificó cuando creó el servidor. |

3.  Haga clic en **Conectar**. Se abre la ventana de explorador de objetos en SSMS.

4. En el Explorador de objetos, expanda **catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos en la base de datos de catálogo de SSIS.

## <a name="run-a-package"></a>Ejecutar un paquete
Ejecute el siguiente código de Transact-SQL para ejecutar un paquete SSIS.

1.  En SSMS, abra una nueva ventana de consulta y pegue el código siguiente. (Este código es el código generado por el **Script** opción en el **Ejecutar paquete** cuadro de diálogo de SSMS.)

2.  Actualice los valores de parámetro en el `catalog.create_execution` procedimiento almacenado para el sistema.

3.  Asegúrese de que SSISDB es la base de datos actual.

4.  Ejecute el script.

5. En el Explorador de objetos, actualice el contenido de **SSISDB** si es necesario y compruebe si el proyecto que ha implementado.

```sql
Declare @execution_id bigint
EXEC [SSISDB].[catalog].[create_execution] @package_name=N'Package.dtsx',
    @execution_id=@execution_id OUTPUT,
    @folder_name=N'Deployed Projects',
      @project_name=N'Integration Services Project1',
    @use32bitruntime=False,
      @reference_id=Null
Select @execution_id
DECLARE @var0 smallint = 1
EXEC [SSISDB].[catalog].[set_execution_parameter_value] @execution_id,
    @object_type=50,
      @parameter_name=N'LOGGING_LEVEL',
      @parameter_value=@var0
EXEC [SSISDB].[catalog].[start_execution] @execution_id
GO
```

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas para ejecutar un paquete.
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS desde la línea de comandos](./ssis-quickstart-run-cmdline.md)
    - [Ejecutar un paquete SSIS con PowerShell](ssis-quickstart-run-powershell.md)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 

