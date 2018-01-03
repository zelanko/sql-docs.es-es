---
title: Implementar un proyecto de SSIS con Transact-SQL (VSCode) | Microsoft Docs
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: quick-start
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f4e5d15cc4ef8c7b51f2fa79e0ff35e7f53d9df
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="deploy-an-ssis-project-from-visual-studio-code-with-transact-sql"></a>Implementar un proyecto de SSIS desde Visual Studio Code con Transact-SQL
En esta guía de inicio rápido se muestra cómo usar Visual Studio Code para conectarse a la base de datos del catálogo de SSIS y, a continuación, usar instrucciones Transact-SQL para implementar un proyecto de SSIS almacenado en el catálogo de SSIS.

> [!NOTE]
> El método que se describe en este artículo no está disponible cuando se conecta a un servidor de Azure SQL Database con VSCode. El procedimiento almacenado `catalog.deploy_project` espera la ruta de acceso al archivo `.ispac` en el sistema de archivos local.

Visual Studio Code es un editor de código para Windows, macOS y Linux que admite extensiones, incluida la extensión `mssql` para conectarse a Microsoft SQL Server, Azure SQL Database o Azure SQL Data Warehouse. Para obtener más información sobre VSCode, consulte [Visual Studio Code](https://code.visualstudio.com/).

## <a name="prerequisites"></a>Prerequisites

Antes de empezar, asegúrese de haber instalado la versión más reciente de Visual Studio Code y cargado la extensión `mssql`. Para descargar estas herramientas, consulte las páginas siguientes:
-   [Descargar Visual Studio Code](https://code.visualstudio.com/Download)
-   [Extensión mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>Establecer el modo de lenguaje en SQL en VSCode

Para habilitar los comandos `mssql` y T-SQL IntelliSense, ajuste el modo de lenguaje en **SQL** en Visual Studio Code.

1. Abra Visual Studio Code y, a continuación, abra una nueva ventana. 

2. Haga clic en **Texto sin formato** en la esquina inferior derecha de la barra de estado.
 
3. En el menú desplegable **Seleccionar modo de lenguaje** que aparece, seleccione o escriba **SQL** y, a continuación, presione **ENTRAR** para establecer el modo de lenguaje en SQL. 

## <a name="connect-to-the-ssis-catalog-database"></a>Conectar con la base de datos del catálogo de SSIS

Use Visual Studio Code para establecer una conexión con el catálogo de SSIS.

> [!IMPORTANT]
> Antes de continuar, asegúrese de que tiene el servidor, la base de datos y la información de inicio de sesión a punto. Si cambia el foco de Visual Studio Code después de comenzar a escribir la información de perfil de conexión, tendrá que volver a iniciar la creación del perfil de conexión.

1. En VSCode, presione **CTRL+MAYÚS+P** (o **F1**) para abrir la paleta de comandos.

2. Escriba **sqlcon** y presione **ENTRAR**.

3. Presione **ENTRAR** para seleccionar **Create Connection Profile** (Crear perfil de conexión). Este paso crea un perfil de conexión para la instancia de SQL Server.

4. Siga las indicaciones para especificar las propiedades de conexión del nuevo perfil de conexión. Después de especificar cada valor, presione **ENTRAR** para continuar. 

   | Configuración       | Valor sugerido | Más información |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Nombre completo del servidor |  |
   | **Nombre de la base de datos** | **SSISDB** | Nombre de la base de datos a la que se va a conectar. |
   | **Autenticación** | Inicio de sesión de SQL| Esta guía de inicio rápido usa la autenticación SQL. |
   | **User name** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña (inicio de sesión de SQL)** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |
   | **¿Desea guardar la contraseña?** | Sí o no | Si no quiere escribir la contraseña cada vez, seleccione Sí. |
   | **Enter a name for this profile** (Escriba un nombre para el perfil) | Nombre de perfil, como **mySSISServer** | Un nombre de perfil guardado acelera la conexión en inicios de sesión posteriores. | 

5. Presione la tecla **ESC** para cerrar el mensaje de información que le indica que el perfil está creado y conectado.

6. Compruebe la conexión en la barra de estado.

## <a name="run-the-t-sql-code"></a>Ejecutar el código T-SQL
Ejecute el siguiente código Transact-SQL para implementar un proyecto de SSIS.

1. En la ventana **Editor**, escriba la siguiente consulta en la ventana de consulta vacía.

2. Actualice los valores de parámetro del procedimiento almacenado `catalog.deploy_project` del sistema.

3. Presione **CTRL+MAYÚS+E** para ejecutar el código e implemente el proyecto.

```sql
DECLARE @ProjectBinary AS varbinary(max)
DECLARE @operation_id AS bigint
SET @ProjectBinary = (SELECT * FROM OPENROWSET(BULK '<project_file_path>.ispac', SINGLE_BLOB) AS BinaryData)

EXEC catalog.deploy_project @folder_name = '<target_folder>',
    @project_name = '<project_name',
    @Project_Stream = @ProjectBinary,
    @operation_id = @operation_id out
```

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas de implementar un paquete.
    - [Implementar un paquete SSIS con SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Deploy an SSIS package with Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md) [Implementar un paquete SSIS con Transact-SQL (SSMS)]
    - [Deploy an SSIS package from the command prompt](./ssis-quickstart-deploy-cmdline.md) (Ejecutar un paquete SSIS desde el símbolo del sistema)
    - [Deploy an SSIS package with PowerShell](ssis-quickstart-deploy-powershell.md) (Implementar un paquete SSIS con PowerShell)
    - [Deploy an SSIS package with C#](./ssis-quickstart-deploy-dotnet.md) (Implementar un paquete SSIS con C#) 
- Ejecute un paquete implementado. Para ejecutar un paquete, puede elegir entre varias herramientas y lenguajes. Para obtener más información, vea los artículos siguientes:
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Run an SSIS package with Transact-SQL (SSMS) (Ejecutar un paquete SSIS con Transact-SQL [SSMS])](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS desde el símbolo del sistema](./ssis-quickstart-run-cmdline.md)
    - [Run an SSIS package with PowerShell](ssis-quickstart-run-powershell.md) (Ejecutar un paquete de SSIS con PowerShell)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 
