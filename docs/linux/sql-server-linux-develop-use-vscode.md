---
title: Usar la extensión mssql de código de Visual Studio para SQL Server
titleSuffix: SQL Server
description: Use la extensión mssql para Visual Studio Code para editar y ejecutar scripts de Transact-SQL para SQL Server en Linux.
author: VanMSFT
ms.author: vanto
ms.date: 12/18/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.openlocfilehash: 207a542e07f271607e5d2266b8c32e313b1dff13
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077309"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts"></a>Use Visual Studio Code para crear y ejecutar scripts de Transact-SQL

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se muestra cómo usar el **mssql** extensión para Visual Studio Code para desarrollar bases de datos de SQL Server. Dado que Visual Studio Code es multiplataforma, puede usar **mssql** extensión en Linux, macOS y Windows.

## <a name="install-and-start-visual-studio-code"></a>Instalar e iniciar Visual Studio Code

Visual Studio Code es un editor de código multiplataforma y gráficos que admite extensiones.

1. [Descargue e instale Visual Studio Code](https://code.visualstudio.com/) en su equipo.

1. Inicie Visual Studio Code.

   >[!NOTE]
   >Si el código de Visual Studio no se inicia cuando están conectados a través de una sesión de escritorio remoto de xrdp, consulte [VS Code no funciona en Ubuntu cuando se conecta mediante XRDP](https://github.com/Microsoft/vscode/issues/3451).

## <a name="install-the-mssql-extension"></a>Instalar la extensión mssql

El [extensión mssql para Visual Studio Code](https://aka.ms/mssql-marketplace) le permite conectarse a un servidor SQL Server, la consulta con Transact-SQL (T-SQL) y ver los resultados.

1. En Visual Studio Code, seleccione **vista** > **paleta de comandos**, o bien presione **Ctrl**+**MAYÚS** + **P**, o bien presione **F1** para abrir el **paleta de comandos**.

1. En el **paleta de comandos**, seleccione **extensiones: Instalar extensiones** en la lista desplegable. 

1. En el **extensiones** panel, escriba *mssql*.

1. Seleccione el **SQL Server (mssql)** extensión y, a continuación, seleccione **instalar**.

   ![Instalar la extensión mssql](./media/sql-server-linux-develop-use-vscode/vscode-extension.png)

1. Una vez finalizada la instalación, seleccione **recarga** para habilitar la extensión.

## <a name="create-or-open-a-sql-file"></a>Crear o abrir un archivo SQL

La extensión mssql permite comandos mssql y T-SQL IntelliSense del editor de código cuando se establece el modo de lenguaje en **SQL**.

1. Seleccione **archivo** > **nuevo archivo** o presione **Ctrl**+**N**. Visual Studio Code abre un nuevo archivo de texto sin formato de forma predeterminada. 

1. Seleccione **texto sin formato** en la barra de estado inferior, o presione **Ctrl**+**K** > **M**y seleccione **SQL** en la lista desplegable de idiomas. 

   ![Modo de lenguaje SQL](./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png)

   > [!NOTE]
   > Si se trata de la primera vez que se ha usado la extensión, la extensión instala herramientas auxiliares de SQL Server.

Si abre un archivo existente que tiene un *.sql* extensión de archivo, se establece automáticamente el modo de lenguaje en SQL.  

## <a name="connect-to-sql-server"></a>Conexión con SQL Server

Siga estos pasos para crear un perfil de conexión y conectarse a un servidor SQL Server.

1. Presione **Ctrl**+**MAYÚS**+**P** o **F1** para abrir el **paleta de comandos**. 

1. Tipo *sql* para mostrar el mssql comandos o tipo *sqlcon*y, a continuación, seleccione **MS SQL: Conectar** en la lista desplegable.

   ![comandos de MSSQL](./media/sql-server-linux-develop-use-vscode/vscode-commands.png)

   >[!NOTE]
   >Como el archivo vacío de SQL que creó, un archivo de SQL, debe tener el foco en el editor de código para poder ejecutar los comandos de mssql.

1. Seleccione el **MS SQL: Administrar perfiles de conexión** comando.

1. A continuación, seleccione **crear** para crear un nuevo perfil de conexión para SQL Server.

1. Siga las indicaciones para especificar las propiedades para el nuevo perfil de conexión. Después de especificar cada valor, presione **ENTRAR** para continuar.

   | Propiedad Conexión | Descripción |
   |---|---|
   | **Nombre del servidor o la cadena de conexión de ADO** | Especifique el nombre de instancia de SQL Server. Use *localhost* para conectarse a una instancia de SQL Server en el equipo local. Para conectarse a un servidor SQL remoto, escriba el nombre del destino SQL Server, o su dirección IP. Para conectarse a un contenedor de SQL Server, especifique la dirección IP del equipo de host del contenedor. Si tiene que especificar un puerto, use una coma para separarlo de nombre. Por ejemplo, para un servidor escucha en el puerto 1401, escriba `<servername or IP>,1401`.<br/><br/>Como alternativa, puede escribir la cadena de conexión de ADO para la base de datos aquí. |
   | **Nombre de la base de datos** (opcional) | La base de datos que desea usar. Para conectarse a la base de datos de forma predeterminada, no especifique un nombre de la base de datos. |
   | **Tipo de autenticación** | Elija **integrado** o **inicio de sesión SQL**. |
   | **Nombre de usuario.** | Si seleccionó **inicio de sesión SQL**, escriba el nombre de un usuario con acceso a una base de datos en el servidor. |
   | **Contraseña** | Escriba la contraseña del usuario especificado. |
   | **Guardar contraseña** | Presione **ENTRAR** seleccionar **Sí** y guarde la contraseña. Seleccione **No** que se le pida la contraseña cada vez que se usa el perfil de conexión. |
   | **Nombre del perfil** (opcional) | Escriba un nombre para el perfil de conexión, como *localhost perfil*. |

   Después de escribir todos los valores y seleccione **ENTRAR**, código de Visual Studio crea el perfil de conexión y se conecta a SQL Server.

   > [!TIP]
   > Si se produce un error en la conexión, intente diagnosticar el problema del mensaje de error en la **salida** panel en Visual Studio Code. Para abrir el **salida** panel, seleccione **vista** > **salida**. Revise también el [recomendaciones para solucionar problemas de conexión](./sql-server-linux-troubleshooting-guide.md#connection).

1. Compruebe la conexión en la barra de estado inferior.

   ![Estado de la conexión](./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png)

Como alternativa a los pasos anteriores, también puede crear y editar perfiles de conexión en el archivo de configuración de usuario (*settings.json*). Para abrir el archivo de configuración, seleccione **archivo** > **preferencias** > **configuración**. Para obtener más información, consulte [administrar perfiles de conexión](https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles).

## <a name="create-a-sql-database"></a>Crear una base de datos SQL

1. En el nuevo archivo SQL que ha iniciado anteriormente, escriba *sql* para mostrar una lista de fragmentos de código modificable. 

   ![Fragmentos de código SQL](./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png)

1. Seleccione **sqlCreateDatabase**.

1. En el fragmento de código, escriba `TutorialDB` para reemplazar "DatabaseName":

   ```sql
   -- Create a new database called 'TutorialDB'
   -- Connect to the 'master' database to run this snippet
   USE master
   GO
   IF NOT EXISTS (
      SELECT name
      FROM sys.databases
      WHERE name = N'TutorialDB'
   )
   CREATE DATABASE [TutorialDB]
   GO
   ```

1. Presione **Ctrl**+**MAYÚS**+**E** para ejecutar los comandos de Transact-SQL. Ver los resultados en la ventana de consulta.

   ![Crear mensajes de la base de datos](./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png)

   > [!TIP]
   > Puede personalizar las teclas de método abreviado para los comandos de mssql. Consulte [personalizar métodos abreviados](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts).

## <a name="create-a-table"></a>Creación de una tabla

1. Elimine el contenido de la ventana del editor de código.

1. Presione **Ctrl**+**MAYÚS**+**P** o **F1** para abrir el **paleta de comandos**. 

1. Tipo *sql* para mostrar el mssql comandos o tipo *sqluse*y, a continuación, seleccione el **MS SQL: Usar base de datos** comando.

1. Seleccione la nueva **TutorialDB** base de datos. 

   ![Usar base de datos](./media/sql-server-linux-develop-use-vscode/vscode-use-database.png)

1. En el editor de código, escriba *sql* para mostrar los fragmentos de código, seleccione **sqlCreateTable**y, a continuación, presione **ENTRAR**.

1. En el fragmento de código, escriba `Employees` para el nombre de tabla.

1. Presione **ficha** para obtener al campo siguiente y, a continuación, escriba `dbo` para el nombre del esquema.

1. Reemplazar las definiciones de columna con las siguientes columnas:

   ```sql
   EmployeesId INT NOT NULL PRIMARY KEY,
   Name [NVARCHAR](50)  NOT NULL,
   Location [NVARCHAR](50)  NOT NULL
   ```

1. Presione **Ctrl**+**MAYÚS**+**E** para crear la tabla.

## <a name="insert-and-query"></a>Insertar y consultar

1. Agregue las siguientes instrucciones para insertar cuatro filas en la **empleados** tabla.

   ```sql
   -- Insert rows into table 'Employees'
   INSERT INTO Employees
      ([EmployeesId],[Name],[Location])
   VALUES
      ( 1, N'Jared', N'Australia'),
      ( 2, N'Nikita', N'India'),
      ( 3, N'Tom', N'Germany'),
      ( 4, N'Jake', N'United States')
   GO
   -- Query the total count of employees
   SELECT COUNT(*) as EmployeeCount FROM dbo.Employees;
   -- Query all employee information
   SELECT e.EmployeesId, e.Name, e.Location 
   FROM dbo.Employees as e
   GO
   ```

   Mientras escribe, T-SQL IntelliSense le ayuda a completar las instrucciones:

   ![Transact-SQL IntelliSense](./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png)

   > [!TIP]
   > La extensión mssql también tiene comandos que ayudan a crear instrucciones INSERT y SELECT. Estos datos no se utilizaron en el ejemplo anterior.

1. Presione **Ctrl**+**MAYÚS**+**E** para ejecutar los comandos. Dar lugar a los dos conjuntos de presentación en el **resultados** ventana. 

   ![Resultados](./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png)

## <a name="view-and-save-the-result"></a>Ver y guardar el resultado

1. Seleccione **vista** > **Editor diseño** > **voltear diseño** para cambiar a un diseño de división vertical u horizontal.

1. Seleccione el **resultados** y **mensajes** encabezados para contraer y expandir los paneles del panel.

   ![Encabezados de alternancia](./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png)

   > [!TIP]
   > Puede personalizar el comportamiento predeterminado de la extensión mssql. Consulte [personalizar las opciones de extensión](https://github.com/Microsoft/vscode-mssql/wiki/customize-options).

1. Seleccione el icono de cuadrícula maximizar en la segunda cuadrícula de resultados para acercar esos resultados.

   ![Maximizar la cuadrícula](./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png)

   > [!NOTE]
   > El icono maximizar muestra cuando el script T-SQL genera las cuadrículas de resultados de dos o más.

1. Abra el menú contextual de cuadrícula con el botón secundario en la cuadrícula. 

   ![Menú contextual](./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png)

1. Seleccione **seleccionar todo**.

1. Vuelva a abrir el menú contextual de cuadrícula y seleccione **Guardar como JSON** para guardar el resultado a un *.json* archivo.

1. Especifique un nombre de archivo para el archivo JSON. 

1. Compruebe que el archivo JSON se guarda y se abre en Visual Studio Code.

   ![Guardar como JSON](./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png)

Si tiene que guardar y ejecutar secuencias de comandos SQL más adelante, para la administración o un proyecto de desarrollo más grande, guardar las secuencias de comandos con un *.sql* extensión.

## <a name="next-steps"></a>Pasos siguientes

Si está familiarizado con Transact-SQL, consulte [Tutorial: Escribir instrucciones Transact-SQL](https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements) y [referencia de Transact-SQL (motor de base de datos)](https://docs.microsoft.com/sql/t-sql/language-reference).

Para obtener más información sobre el uso o que contribuyen a la extensión mssql, consulte el [wiki de proyecto de extensión mssql](https://github.com/Microsoft/vscode-mssql/wiki).

Para obtener más información sobre el uso de Visual Studio Code, consulte el [documentación de Visual Studio Code](https://code.visualstudio.com/docs).