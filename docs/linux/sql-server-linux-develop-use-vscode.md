---
title: Usar la extensión mssql de código de Visual Studio para SQL Server | Microsoft Docs
description: Este tutorial muestra cómo usar la extensión mssql para VS Code. Esta extensión permite editar y ejecutar scripts de Transact-SQL en VS Code.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: sql-linux
ms.openlocfilehash: be5a40a904389979c1646aab9d8b4420ac71356a
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084747"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts-for-sql-server"></a>Use Visual Studio Code para crear y ejecutar scripts de Transact-SQL para SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se muestra cómo usar el **mssql** extensión para Visual Studio Code (VS Code) para desarrollar bases de datos de SQL Server.

Visual Studio Code es un editor de código gráfico para Linux, macOS y Windows que admite extensiones. El [**mssql** extensión de VS Code] le permite conectarse a SQL Server, consulta con Transact-SQL (T-SQL) y ver los resultados.

## <a name="install-vs-code"></a>Instalación de VS Code
1. Si aún no ha instalado VS Code, [descarga e instalación de VS Code] en su equipo.

2. Inicie VS Code.

## <a name="install-the-mssql-extension"></a>Instalar la extensión mssql
Los pasos siguientes explican cómo instalar la extensión mssql. 

1. Presione **CTRL + MAYÚS + P** (o **F1**) para abrir la paleta de comandos en VS Code. 

2. Seleccione **instalar extensión** y tipo **mssql**.
   > [!TIP] 
   > Para macOS, la **CMD** clave equivale a **CTRL** clave en Linux y Windows.

2. Haga clic en instalar **mssql**. 
   
   <img src="./media/sql-server-linux-develop-use-vscode/vscode-extension.png" alt="Install the extension" style="width: 600px;"/>

3. El **mssql** extensión toma hasta un minuto. Espere a que el símbolo del sistema que le indica que se ha instalado correctamente.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-install-success-notification.png" alt="Installation success notification" style="width: 600px;"/>

   > [!NOTE]
   > Para macOS, debe instalar OpenSSL. Se trata de un requisito previo para.Net Core usa la extensión mssql. Siga el **instalar requisitos previos** los pasos de la [Instrucciones de.Net Core]. O bien, puede ejecutar los comandos siguientes en el Terminal de macOS.
   >
   >   ```bash
   >   brew update
   >   brew install openssl
   >   ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/
   >   ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
   >   ```
   
   > [!NOTE]
   > Para Windows 8.1, Windows Server 2012 o versiones inferiores, debe descargar e instalar el [Tiempo de ejecución de C Universal de Windows 10]. Descargue y abra el archivo zip. A continuación, ejecute al instalador (archivo .msu) destinadas a la configuración del sistema operativo actual.

## <a name="create-or-open-a-sql-file"></a>Crear o abrir un archivo SQL

El **mssql** extensión permite comandos mssql y T-SQL IntelliSense en el editor cuando se establece el modo de lenguaje en **SQL**.

1. Presione **CTRL + N**. Visual Studio Code abre un nuevo archivo de "Texto sin formato" de forma predeterminada. 

2. Presione **CTRL + K, M** y cambie el modo de lenguaje a **SQL**. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-language-mode.png" alt="SQL language mode" style="width: 500px;" />

3. Como alternativa, abra un archivo existente con la extensión de archivo. SQL. El modo de lenguaje es automáticamente **SQL** los archivos que tienen la extensión. SQL.  

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

Los pasos siguientes muestran cómo conectarse a SQL Server con VS Code.

1. En VSCode, presione **CTRL+MAYÚS+P** (o **F1**) para abrir la paleta de comandos.

2. Tipo **sql** para mostrar los comandos de mssql.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-commands.png" alt="mssql commands" style="width: 500px;" />
   

3. Seleccione el **MS SQL: conectar** comando. Puede escribir simplemente **sqlcon** y presione **ENTRAR**.

4. Seleccione **Crear perfil de conexión**. Esto crea un perfil de conexión para la instancia de SQL Server.

5. Siga las indicaciones para especificar las propiedades de conexión del nuevo perfil de conexión. Después de especificar cada valor, presione **ENTRAR** para continuar. 

   En la tabla siguiente se describe las propiedades de perfil de conexión.

   | Parámetro | Descripción |
   |-----|-----|
   | **Nombre del servidor** | El nombre de instancia de SQL Server. Para este tutorial, use **localhost** para conectarse a la instancia de SQL Server local en el equipo. Si se conecta a un servidor SQL remoto, escriba el nombre de la máquina de SQL Server de destino o su dirección IP. Si tiene que especificar un puerto para la instancia de SQL Server, use una coma para separarlo de nombre. Por ejemplo para un servidor local que se ejecuta en el puerto 1401 escriba **localhost, 1401**. |
   | **[Opcional] Nombre de la base de datos** | La base de datos que desea usar. Para fines de este tutorial, no se especifica una base de datos y presione **ENTRAR** para continuar. |
   | **Nombre de usuario.** | Escriba el nombre de un usuario con acceso a una base de datos en el servidor. Para este tutorial, use el valor predeterminado **SA** cuenta creada durante la instalación de SQL Server. |
   | **Contraseña (inicio de sesión de SQL)** | Escriba la contraseña del usuario especificado. | 
   | **¿Desea guardar la contraseña?** | Tipo **Sí** para guardar la contraseña. En caso contrario, escriba **No** que se le pida la contraseña cada vez que se usa el perfil de conexión. |
   | **[Opcional] Escriba un nombre para este perfil** | El nombre del perfil de conexión. Por ejemplo, podría denominar el perfil **localhost perfil**. 

   > [!Tip] 
   > Puede crear y editar perfiles de conexión en el archivo de configuración de usuario (settings.json). Abra el archivo de configuración seleccionando **preferencias** y, a continuación, **configuración de usuario** en el menú de VS Code. Para obtener más información, consulte [administrar perfiles de conexión].

6. Presione la tecla **ESC** para cerrar el mensaje de información que le indica que el perfil está creado y conectado.

   > [!TIP]
   > Si se produce un error de conexión, intente primero diagnosticar el problema del mensaje de error en la **salida** panel en VS Code (seleccione **salida** en el **vista** menú). Luego revise las [recomendaciones para solucionar problemas de conexión].

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
   > Puede personalizar los enlaces de teclado para los comandos de la extensión mssql. Consulte [personalizar métodos abreviados].

## <a name="create-a-table"></a>Creación de una tabla

1. Quitar el contenido de la ventana del editor.

2. Presione **F1** para mostrar la paleta de comandos.

3. Tipo **sql** en la paleta de comandos para mostrar los comandos SQL o un tipo **sqluse** para **base de datos de MS SQL** comando.

4. Haga clic en **base de datos de MS SQL**y seleccione el **TutorialDB** base de datos. Esto cambia el contexto a la base de datos creada en la sección anterior.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-use-database.png" alt="use database" style="width: 500px;" />

3. En el editor, escriba **sql** para mostrar los fragmentos de código y, a continuación, seleccione **sqlCreateTable** y presione **escriba**.

4. En el fragmento de código, escriba **empleados** para el nombre de tabla.

5. Presione **ficha**y, a continuación, escriba **dbo** para el nombre del esquema.

   > [!NOTE]
   > Después de agregar el fragmento de código, debe escribir los nombres de tabla y el esquema sin cambiar el foco del editor de código de VS.

6. Cambiar el nombre de columna **Column1** a **nombre** y **Column2** a **ubicación**.

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

## <a name="insert-and-query"></a>Insertar y consultar

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
   > Mientras escribe, use la Ayuda de IntelliSense de T-SQL.
   >   <img src="./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png" alt="TSQL IntelliSense" style="width: 500px;" />

2. Presione **CTRL + MAYÚS + E** para ejecutar los comandos. Dar lugar a los dos conjuntos de presentación en el **resultados** ventana. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png" alt="Results" style="width: 300px;" />

## <a name="view-and-save-the-result"></a>Ver y guardar el resultado

1. En el **vista** menú, seleccione **alternar Editor de diseño del grupo** para cambiar a diseño de división vertical u horizontal.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-split.png" alt="Vertical split" style="width: 500px;" />

2. Haga clic en el **resultados** y **mensajes** encabezado de panel para contraer y expandir el panel.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png" alt="Toggle Messages" style="width: 500px;" />

   > [!TIP]
   > Puede personalizar el comportamiento predeterminado de la extensión mssql. Consulte [personalizar las opciones de extensión].

2. Haga clic en el icono de cuadrícula maximizar en la segunda cuadrícula de resultados para acercar.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-maximize-grid.png" alt="Maximize grid" style="width: 500px;" />

   > [!NOTE]
   > El icono maximizar muestra cuando el script de Transact-SQL tiene dos o más de las cuadrículas de resultados.

3. Abra el menú contextual de cuadrícula con el botón secundario del mouse en una cuadrícula. 

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-grid-context-menu.png" alt="Context menu" style="width: 500px;" />

4. Seleccione **seleccionar todo**.

5. Abra el menú contextual de cuadrícula y seleccione **Guardar como JSON** para guardar el resultado en un archivo .json.

6. Especifique un nombre de archivo para el archivo JSON. Para este tutorial, escriba **employees.json**.

7. Compruebe que el archivo JSON se guarda y se abre en VS Code.

   <img src="./media/sql-server-linux-develop-use-vscode/vscode-save-as-json.png" alt="Save as Json" style="width: 500px;" />

## <a name="next-steps"></a>Pasos siguientes

En un escenario real, podría crear una secuencia de comandos que necesita para guardar y ejecutar una versión posterior (para la administración o como parte de un proyecto de desarrollo más grande). En este caso, puede guardar el script con un **.sql** extensión.

Si está familiarizado con Transact-SQL, consulte [Tutorial: escribir instrucciones Transact-SQL] y [referencia de Transact-SQL (motor de base de datos)].

Para obtener más información sobre el uso o que contribuyen a la extensión mssql, consulte [el wiki de proyecto de extensión mssql].

Para obtener más información sobre el uso de VS Code, consulte el [documentación de Visual Studio Code](https://code.visualstudio.com/docs).

[**mssql** extensión de VS Code]:https://aka.ms/mssql-marketplace
[Descarga e instalación de VS Code]:https://code.visualstudio.com/Download
[Instrucciones de.Net Core]:https://www.microsoft.com/net/core
[Administrar perfiles de conexión]:https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles
[recomendaciones para solucionar problemas de conexión]:./sql-server-linux-troubleshooting-guide.md#connection
[personalizar métodos abreviados]:https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts
[Tutorial: Escribir instrucciones Transact-SQL]:https://msdn.microsoft.com/library/ms365303.aspx
[Referencia de Transact-SQL (motor de base de datos)]:https://msdn.microsoft.com/library/bb510741.aspx
[Visual Studio Code documentation]:https://code.visualstudio.com/docs
[Tiempo de ejecución de C Universal de Windows 10]:https://github.com/Microsoft/vscode-mssql/wiki/windows10-universal-c-runtime-requirement
[personalizar las opciones de extensión]: https://github.com/Microsoft/vscode-mssql/wiki/customize-options
[el wiki de proyecto de extensión mssql]: https://github.com/Microsoft/vscode-mssql/wiki
