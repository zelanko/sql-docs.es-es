---
title: "Ejecutar un paquete SSIS con Transact-SQL (código de VS) | Documentos de Microsoft"
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
ms.openlocfilehash: a912bf7f7944d4af3d41c5596e67aa77f3214112
ms.contentlocale: es-es
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-visual-studio-code-with-transact-sql"></a>Ejecutar un paquete SSIS desde código de Visual Studio con Transact-SQL
Este tutorial muestra cómo utilizar código de Visual Studio para conectarse a la base de datos de catálogo de SSIS y, a continuación, utilizar instrucciones Transact-SQL para ejecutar un paquete SSIS que se almacenan en el catálogo de SSIS.

Código de Visual Studio es un editor de código para Windows, Mac OS y Linux que admita extensiones, incluida la `mssql` extensión para conectarse a Microsoft SQL Server, base de datos de SQL Azure o almacenamiento de datos de SQL Azure. Para obtener más información sobre el código de VS, consulte [Cod de Visual Studio](https://code.visualstudio.com/).

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que ha instalado la versión más reciente de Visual Studio Code y cargar la `mssql` extensión. Para descargar estas herramientas, vea las siguientes páginas:
-   [Descargar Visual Studio Code](https://code.visualstudio.com/Download)
-   [extensión de MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="set-language-mode-to-sql-in-vs-code"></a>Establecer el modo de lenguaje a SQL en el código de VS

Para habilitar `mssql` comandos y T-SQL IntelliSense, ajuste el modo de idioma está establecido en **SQL** en código de Visual Studio.

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
   | **Nombre del servidor** | El nombre completo del servidor | Si se está conectando a un servidor de base de datos de SQL Azure, el nombre está en este formato: `<server_name>.database.windows.net`. |
   | **Nombre de la base de datos** | **SSISDB** | El nombre de la base de datos que se va a conectar. |
   | **Autenticación** | Inicio de sesión de SQL| Este tutorial rápido usa la autenticación de SQL. |
   | **Nombre de usuario.** | La cuenta de administrador de servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña (inicio de sesión SQL)** | La contraseña de la cuenta de administrador del servidor | Esta es la contraseña que especificó cuando creó el servidor. |
   | **¿Guardar contraseña?** | Sí o no | Si no desea escribir la contraseña cada vez, seleccione Sí. |
   | **Escriba un nombre para este perfil** | Nombre de un perfil, como **mySSISServer** | Un nombre de perfil guardado acelera la conexión en inicios de sesión posteriores. | 

5. Presione el **ESC** tecla para cerrar el mensaje de información que le informa de que el perfil se crea y conectado.

6. Compruebe la conexión en la barra de estado.

## <a name="run-the-t-sql-code"></a>Ejecute el código de T-SQL
Ejecute el siguiente código de Transact-SQL para ejecutar un paquete SSIS.

1. En el **Editor** ventana, escriba la siguiente consulta en la ventana de consulta vacía. (Este código es el código generado por el **Script** opción en el **Ejecutar paquete** cuadro de diálogo de SSMS.)

2. Actualice los valores de parámetro en el `catalog.create_execution` procedimiento almacenado para el sistema.

3. Presione **CTRL + MAYÚS + E** para ejecutar el código y ejecutar el paquete.

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
    - [Ejecutar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS desde la línea de comandos](./ssis-quickstart-run-cmdline.md)
    - [Ejecutar un paquete SSIS con PowerShell](ssis-quickstart-run-powershell.md)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 

