---
title: "Implementar un proyecto de SSIS con Transact-SQL (código de VS) | Documentos de Microsoft"
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
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 2dc6de798ca76b43627a3c381fe628506c3e7480
ms.contentlocale: es-es
ms.lasthandoff: 10/04/2017

---
# <a name="deploy-an-ssis-project-from-visual-studio-code-with-transact-sql"></a>Implementar un proyecto de SSIS de código de Visual Studio con Transact-SQL
Este tutorial muestra cómo utilizar código de Visual Studio para conectarse a la base de datos de catálogo de SSIS y, a continuación, utilice las instrucciones de Transact-SQL para implementar un proyecto de SSIS en el catálogo de SSIS.

> [!NOTE]
> El método descrito en este artículo no está disponible cuando se conecta a un servidor de base de datos de SQL Azure con el código de VS. El `catalog.deploy_project` procedimiento almacenado espera que la ruta de acceso a la `.ispac` archivo en el sistema de archivos local (local).

Código de Visual Studio es un editor de código para Windows, Mac OS y Linux que admita extensiones, incluida la `mssql` extensión para conectarse a Microsoft SQL Server, base de datos de SQL Azure o almacenamiento de datos de SQL Azure. Para obtener más información sobre el código de VS, consulte [código de Visual Studio](https://code.visualstudio.com/).

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que ha instalado la versión más reciente de Visual Studio Code y cargar la `mssql` extensión. Para descargar estas herramientas, vea las siguientes páginas:
-   [Descargar Visual Studio Code](https://code.visualstudio.com/Download)
-   [extensión de MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>Establecer el modo de lenguaje a SQL en el código de VS

Para habilitar `mssql` comandos e IntelliSense de T-SQL, establezca el modo de lenguaje en **SQL** en código de Visual Studio.

1. Abra el código de Visual Studio y, a continuación, abra una ventana nueva. 

2. Haga clic en **texto sin formato** en la esquina inferior derecha de la barra de estado.
 
3. En el **modo Seleccionar idioma** menú desplegable que aparece, seleccione o escriba **SQL**y, a continuación, presione **ENTRAR** para establecer el modo de lenguaje en SQL. 

## <a name="connect-to-the-ssis-catalog-database"></a>Conectarse a la base de datos de catálogo de SSIS

Usar código de Visual Studio para establecer una conexión con el catálogo de SSIS.

> [!IMPORTANT]
> Antes de continuar, asegúrese de que tiene el servidor, la base de datos y la información de inicio de sesión listo. Si cambia el foco de código de Visual Studio después de comenzar a escribir la información de perfil de conexión, tendrá que reiniciar la creación del perfil de conexión.

1. En el código de VS, presione **CTRL + MAYÚS + P** (o **F1**) para abrir la paleta de comando.

2. Tipo de **sqlcon** y presione **ENTRAR**.

3. Presione **ENTRAR** para seleccionar **Crear perfil de conexión**. Este paso crea un perfil de conexión para la instancia de SQL Server.

4. Siga las indicaciones para especificar las propiedades de conexión para el nuevo perfil de conexión. Después de especificar cada valor, presione **ENTRAR** para continuar. 

   | Configuración       | Valor recomendado | Más información |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | El nombre completo del servidor |  |
   | **Nombre de la base de datos** | **SSISDB** | El nombre de la base de datos que se va a conectar. |
   | **Autenticación** | Inicio de sesión de SQL| Este tutorial rápido usa la autenticación de SQL. |
   | **Nombre de usuario.** | La cuenta de administrador de servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña (inicio de sesión SQL)** | La contraseña de la cuenta de administrador del servidor | Esta es la contraseña que especificó cuando creó el servidor. |
   | **¿Guardar contraseña?** | Sí o no | Si no desea escribir la contraseña cada vez, seleccione Sí. |
   | **Escriba un nombre para este perfil** | Nombre de un perfil, como **mySSISServer** | Un nombre de perfil guardado acelera la conexión en inicios de sesión posteriores. | 

5. Presione el **ESC** tecla para cerrar el mensaje de información que le informa de que el perfil se crea y conectado.

6. Compruebe la conexión en la barra de estado.

## <a name="run-the-t-sql-code"></a>Ejecute el código de T-SQL
Ejecute el siguiente código de Transact-SQL para implementar un proyecto de SSIS.

1. En el **Editor** ventana, escriba la siguiente consulta en la ventana de consulta vacía.

2. Actualice los valores de parámetro en el `catalog.deploy_project` procedimiento almacenado para el sistema.

3. Presione **CTRL + MAYÚS + E** para ejecutar el código e implementar el proyecto.

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
    - [Implementar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
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

