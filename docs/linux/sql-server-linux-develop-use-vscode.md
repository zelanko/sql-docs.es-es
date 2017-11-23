---
title: "Use la extensión de mssql de código de Visual Studio para SQL Server | Documentos de Microsoft"
description: "Este tutorial muestra cómo utilizar la extensión mssql para el código de VS. Esta extensión le permite editar y ejecutar scripts de Transact-SQL en el código de VS."
author: erickangMSFT
ms.author: erickang
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: 
ms.workload: Active
ms.openlocfilehash: 41bfb66db6f16d9e7ca8829568798a2aa57316da
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts-for-sql-server"></a>Usar código de Visual Studio para crear y ejecutar secuencias de comandos de Transact-SQL para SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este tema muestra cómo utilizar el **mssql** extensión para Visual Studio Code (código de VS) para desarrollar bases de datos de SQL Server.

Código de Visual Studio es un editor de código gráfica para Linux, Mac OS y Windows que admita extensiones. El [**mssql** extensión de VS Code] le permite conectarse a SQL Server, consulta con Transact-SQL (T-SQL) y ver los resultados.

## <a name="install-vs-code"></a>Instalar el código de VS
1. Si todavía no ha instalado VS Code, [descargar e instalar VS Code] en su equipo.

2. Iniciar frente a código.

## <a name="install-the-mssql-extension"></a>Instalar la extensión de mssql
Los siguientes pasos explican cómo instalar la extensión mssql. 

1. Presione **CTRL + MAYÚS + P** (o **F1**) para abrir la paleta de comando en el código de VS. 

2. Seleccione **instalar extensión** y tipo **mssql**.
   > [!TIP] 
   > Para macOS, el **CMD** clave es equivalente a **CTRL** clave en Linux y Windows.

2. Haga clic en instalar **mssql**. 
   
   <img src="./media/sql-server-linux-develop-use-vscode/vscode-extension.png" alt="Install the extension" style="width: 600px;"/>

3. El **mssql** extensión toma hasta un minuto para instalar. Espere a que el mensaje que indica que se instaló correctamente.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-install-success-notification.png" alt="Installation success notification" style="width: 600px;"/>

   > [!NOTE]
   > Para macOS, debe instalar OpenSSL. Se trata de un requisito previo para .net Core usa la extensión mssql. Siga el **instalar requisitos previos** los pasos de la [.Net Core instrucciones]. O bien, puede ejecutar los siguientes comandos en el Terminal de Mac OS.
   >
   >   ```bash
   >   brew update
   >   brew install openssl
   >   ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
   >   ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
   >   ```
   
   > [!NOTE]
   > Para Windows 8.1, Windows Server 2012 o versiones inferiores, debe descargar e instalar la [tiempo de ejecución de C Universal de Windows 10]. Descargue y abra el archivo zip. A continuación, ejecute al instalador (archivo .msu) que se dirige a la configuración del sistema operativo actual.

## <a name="create-or-open-a-sql-file"></a>Crear o abrir un archivo SQL

El **mssql** extensión permite mssql comandos y T-SQL IntelliSense en el editor cuando el modo de idioma está establecido en **SQL**.

1. Presione **CTRL + N**. Código de Visual Studio abre un nuevo archivo de 'Texto' de forma predeterminada. 

2. Presione **CTRL + K, M** y cambie el modo de lenguaje a **SQL**. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png" alt="SQL language mode" style="width: 500px;" />

3. Como alternativa, puede abrir un archivo existente con la extensión de archivo. SQL. El modo de lenguaje es automáticamente **SQL** para los archivos que tienen la extensión. SQL.  

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

Los pasos siguientes muestran cómo conectarse a SQL Server con el código de VS.

1. En el código de VS, presione **CTRL + MAYÚS + P** (o **F1**) para abrir la paleta de comando.

2. Tipo de **sql** para mostrar los comandos mssql.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-commands.png" alt="mssql commands" style="width: 500px;" />
   

3. Seleccione el **MS SQL: conectar** comando. Puede escribir simplemente **sqlcon** y presione **ENTRAR**.

4. Seleccione **Crear perfil de conexión**. Esto crea un perfil de conexión para la instancia de SQL Server.

5. Siga las indicaciones para especificar las propiedades de conexión para el nuevo perfil de conexión. Después de especificar cada valor, presione **ENTRAR** para continuar. 

   En la tabla siguiente se describe las propiedades de perfil de conexión.

   | Configuración | Description |
   |-----|-----|
   | **Nombre del servidor** | El nombre de instancia de SQL Server. Para este tutorial, utilice **localhost** para conectarse a la instancia de SQL Server local en su equipo. Si se conecta a un servidor SQL remoto, escriba el nombre de la máquina de SQL Server de destino o su dirección IP. |
   | **[Opcional] Nombre de base de datos** | La base de datos que desea usar. Para fines de este tutorial, no se especifica una base de datos y presione **ENTRAR** para continuar. |
   | **Nombre de usuario.** | Escriba el nombre de un usuario con acceso a una base de datos en el servidor. Para este tutorial, utilice el valor predeterminado **SA** cuenta creada durante la instalación de SQL Server. |
   | **Contraseña (inicio de sesión SQL)** | Escriba la contraseña del usuario especificado. | 
   | **¿Guardar contraseña?** | Tipo de **Sí** para guardar la contraseña. En caso contrario, escriba **No** que se le pida la contraseña cada vez que se usa el perfil de conexión. |
   | **[Opcional] Escriba un nombre para este perfil** | El nombre del perfil de conexión. Por ejemplo, podría denominar el perfil **localhost perfil**. 

   > [!Tip] 
   > Puede crear y editar perfiles de conexión en el archivo de configuración de usuario (settings.json). Abra el archivo de configuración seleccionando **preferencias** y, a continuación, **configuración de usuario** en el menú de VS Code. Para obtener más información, consulte [administrar perfiles de conexión].

6. Presione el **ESC** tecla para cerrar el mensaje de información que le informa de que el perfil se crea y conectado.

   > [!TIP]
   > Si se produce un error de conexión, en primer lugar intenta diagnosticar el problema del mensaje de error en la **salida** panel en VS Code (seleccione **salida** en el **vista** menú). Luego revise las [recomendaciones para solucionar problemas de conexión].

7. Compruebe la conexión en la barra de estado.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png" alt="Connection status" style="width: 500px;" />

## <a name="create-a-database"></a>Crear una base de datos

1. En el editor, escriba **sql** para que aparezca una lista de fragmentos de código modificable. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png" alt="SQL snippets" style="width: 500px;" />

2. Seleccione **sqlCreateDatabase**.

3. En el fragmento de código, escriba **TutorialDB** para el nombre de la base de datos.

   ```sql
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
   
4. Presione **CTRL + MAYÚS + E** para ejecutar los comandos de Transact-SQL. Ver los resultados en la ventana de consulta.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-create-database-messages.png" alt="create database messages" style="width: 500px;" />

   > [!TIP]
   > Puede personalizar los enlaces de teclado de método abreviado para los comandos de extensión mssql. Vea [personalizar métodos abreviados de].

## <a name="create-a-table"></a>Creación de una tabla

1. Quitar el contenido de la ventana del editor.

2. Presione **F1** para mostrar la paleta de comando.

3. Tipo de **sql** en la paleta de comando para mostrar los comandos SQL o el tipo **sqluse** para **base de datos de MS SQL** comando.

4. Haga clic en **base de datos de MS SQL**y seleccione el **TutorialDB** base de datos. Esto cambia el contexto a la base de datos creada en la sección anterior.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-use-database.png" alt="use database" style="width: 500px;" />

3. En el editor, escriba **sql** para mostrar los fragmentos de código y, a continuación, seleccione **sqlCreateTable** y presione **escriba**.

4. En el fragmento de código, escriba **empleados** para el nombre de tabla.

5. Presione **ficha**y, a continuación, escriba **dbo** para el nombre del esquema.

   > [!NOTE]
   > Después de agregar el fragmento de código, debe escribir los nombres de tabla y el esquema sin cambiar el foco del editor de código de VS.

6. Cambiar el nombre de columna de **Column1** a **nombre** y **Column2** a **ubicación**.

   ```sql
   -- Create a new table called 'Employees' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Employees', 'U') IS NOT NULL
   DROP TABLE dbo.Employees
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Employees
   (
      EmployeesId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location   [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

7. Presione **CTRL + MAYÚS + E** para crear la tabla.

## <a name="insert-and-query"></a>INSERT y consulta

1. Agregue las siguientes instrucciones para insertar cuatro filas en la **empleados** tabla. A continuación, seleccione todas las filas.

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

   > [!TIP]
   > Mientras se escribe, use la Ayuda de IntelliSense de T-SQL.
   >   <img src="./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png" alt="TSQL IntelliSense" style="width: 500px;" />

2. Presione **CTRL + MAYÚS + E** para ejecutar los comandos. Los dos conjuntos de presentación en como resultado la **resultados** ventana. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png" alt="Results" style="width: 300px;" />

## <a name="view-and-save-the-result"></a>Ver y guardar el resultado

1. En el **vista** menú, seleccione **diseño del grupo de alternar Editor** para cambiar a diseño de división vertical u horizontal.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-split.png" alt="Vertical split" style="width: 500px;" />

2. Haga clic en el **resultados** y **mensajes** cabezal del panel para contraer y expandir el panel.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png" alt="Toggle Messages" style="width: 500px;" />

   > [!TIP]
   > Puede personalizar el comportamiento predeterminado de la extensión mssql. Vea [personalizar las opciones de extensión].

2. Haga clic en el icono de cuadrícula maximizar en la segunda cuadrícula de resultados para acercar.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png" alt="Maximize grid" style="width: 500px;" />

   > [!NOTE]
   > Se muestra el icono de maximizar cuando el script de T-SQL tiene dos o varias cuadrículas de resultados.

3. Abra el menú contextual de cuadrícula con el botón secundario del mouse en una cuadrícula. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png" alt="Context menu" style="width: 500px;" />

4. Seleccione **seleccionar todo**.

5. Abra el menú contextual de cuadrícula y seleccione **Guardar como JSON** para guardar el resultado en un archivo .json.

6. Especifique un nombre de archivo para el archivo JSON. Para este tutorial, escriba **employees.json**.

7. Compruebe que el archivo JSON se guarda y se abre en el código de VS.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png" alt="Save as Json" style="width: 500px;" />

## <a name="next-steps"></a>Pasos siguientes

En un escenario real, puede crear una secuencia de comandos que necesita para guardar y ejecutar una versión posterior (para la administración o como parte de un proyecto de desarrollo más grande). En este caso, puede guardar la secuencia de comandos con un **.sql** extensión.

Si está familiarizado con T-SQL, vea [Tutorial: escribir instrucciones de Transact-SQL] y [referencia de Transact-SQL (motor de base de datos)].

Para obtener más información sobre el uso o que han contribuido a la extensión mssql, consulte [el wiki de proyecto de extensión mssql].

Para obtener más información sobre el uso de código de VS, consulte el [documentación de código de Visual Studio](https://code.visualstudio.com/docs).

[**mssql** extensión de VS Code]:https://aka.ms/mssql-marketplace
[descargar e instalar VS Code]:https://code.visualstudio.com/Download
[.Net Core instrucciones]:https://www.microsoft.com/net/core
[administrar perfiles de conexión]:https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles
[recomendaciones para solucionar problemas de conexión]:./sql-server-linux-troubleshooting-guide.md#connection
[personalizar métodos abreviados de]:https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts
[Tutorial: escribir instrucciones de Transact-SQL]:https://msdn.microsoft.com/library/ms365303.aspx
[referencia de Transact-SQL (motor de base de datos)]:https://msdn.microsoft.com/library/bb510741.aspx
[Visual Studio Code documentation]:https://code.visualstudio.com/docs
[tiempo de ejecución de C Universal de Windows 10]:https://github.com/Microsoft/vscode-mssql/wiki/windows10-universal-c-runtime-requirement
[personalizar las opciones de extensión]: https://github.com/Microsoft/vscode-mssql/wiki/customize-options
[el wiki de proyecto de extensión mssql]: https://github.com/Microsoft/vscode-mssql/wiki
