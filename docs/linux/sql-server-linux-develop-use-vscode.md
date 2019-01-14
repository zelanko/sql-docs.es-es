---
title: Usar la extensión mssql de código de Visual Studio para SQL Server en Linux | Microsoft Docs
description: Use la extensión mssql para Visual Studio Code para editar y ejecutar scripts de Transact-SQL para SQL Server en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/18/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9766ee75-32d3-4045-82a6-4c7968bdbaa6
ms.custom: sql-linux
ms.openlocfilehash: 583c7ac13b49370b333e80568c4b52885b58dcf3
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100570"
---
# <a name="use-visual-studio-code-to-create-and-run-transact-sql-scripts-on-linux"></a>Use Visual Studio Code para crear y ejecutar scripts de Transact-SQL en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se muestra cómo usar el *mssql* extensión para Visual Studio Code para desarrollar bases de datos de SQL Server en Linux.

## <a name="install-and-start-visual-studio-code"></a>Instalar e iniciar Visual Studio Code

Visual Studio Code es un editor de código gráfico para Linux, macOS y Windows que admite extensiones. 

1. [Descargue e instale Visual Studio Code] en su equipo.
   
1. Inicie Visual Studio Code.
   
   >[!NOTE]
   >Si el código de Visual Studio no se inicia cuando están conectados a través de una sesión de escritorio remoto de xrdp, consulte [VS Code no funciona en Ubuntu cuando se conecta mediante XRDP](https://github.com/Microsoft/vscode/issues/3451).

## <a name="install-the-mssql-extension"></a>Instalar la extensión mssql

El [extensión mssql para Visual Studio Code] le permite conectarse a un servidor SQL Server, la consulta con Transact-SQL (T-SQL) y ver los resultados.

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
   
Si abre un archivo existente que tiene un *.sql* extensión de archivo, se establece automáticamente el modo de lenguaje en SQL.  

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

Siga estos pasos para crear un perfil de conexión y conectarse a un servidor SQL Server.

> [!TIP] 
> También puede crear y editar perfiles de conexión en el archivo de configuración de usuario (*settings.json*). Para abrir el archivo de configuración, seleccione **archivo** > **preferencias** > **configuración**. Para obtener más información, consulte [administrar perfiles de conexión].
   
1. Presione **Ctrl**+**MAYÚS**+**P** o **F1** para abrir el **paleta de comandos**. 
   
1. Tipo *sql* para mostrar el mssql comandos o tipo *sqlcon*y, a continuación, seleccione **MS SQL: Conectar** en la lista desplegable.
   
   ![comandos de MSSQL](./media/sql-server-linux-develop-use-vscode/vscode-commands.png)   
   
   >[!NOTE]
   >Como el archivo vacío de SQL que creó, un archivo de SQL, debe tener el foco en el editor de código para poder ejecutar los comandos de mssql. 

1. Seleccione **Crear perfil de conexión** para crear un nuevo perfil de conexión para SQL Server.
   
1. Siga las indicaciones para especificar las propiedades para el nuevo perfil de conexión. Después de especificar cada valor, presione **ENTRAR** para continuar. 
   
   1. **Nombre del servidor o la cadena de conexión ADO**: Especifique el nombre de instancia de SQL Server. Use *localhost* para conectarse a una instancia de SQL Server en el equipo local. Para conectarse a un servidor SQL remoto, escriba el nombre del destino SQL Server, o su dirección IP. Si tiene que especificar un puerto, use una coma para separarlo de nombre. Por ejemplo, para un servidor local que se ejecuta en el puerto 1401, escriba *localhost, 1401*. 
      
      >[!NOTE]
      >También puede escribir la cadena de conexión de ADO para la base de datos, a continuación, presione **ENTRAR**, nombre, opcionalmente, el perfil de conexión y presione **ENTRAR** nuevo para conectarse y crear el perfil. 
      
   1. **Nombre de la base de datos** (opcional): La base de datos que desea usar. Para crear una nueva base de datos, no se especifica una base de datos de nombre y presione **ENTRAR** para continuar. 
      
   1. **Tipo de autenticación**: Presione **ENTRAR** seleccionar **inicio de sesión SQL**. 
      
   1. **Nombre de usuario**: Escriba el nombre de un usuario con acceso a una base de datos en el servidor.
      
   1. **Contraseña**: Escriba la contraseña del usuario especificado.
      
   1. **Guardar contraseña**: Presione **ENTRAR** seleccionar **Sí** y guarde la contraseña. Seleccione **No** que se le pida la contraseña cada vez que se usa el perfil de conexión. 
      
   1. **Nombre del perfil** (opcional): Escriba un nombre para el perfil de conexión, como *localhost perfil*. 
   
   Después de seleccionar **ENTRAR**, código de Visual Studio crea el perfil de conexión y se conecta a SQL Server. 
   
   > [!TIP]
   > Si se produce un error en la conexión, intente diagnosticar el problema del mensaje de error en la **salida** panel en Visual Studio Code. Para abrir el **salida** panel, seleccione **vista** > **salida**. Revise también el [recomendaciones para solucionar problemas de conexión].
   
1. Compruebe la conexión en la barra de estado inferior.
   
  ![Estado de la conexión](./media/sql-server-linux-develop-use-vscode/vscode-connection-status.png)   
   
## <a name="create-a-sql-database"></a>Crear una base de datos SQL

1. En el nuevo archivo SQL que ha iniciado anteriormente, escriba *sql* para mostrar una lista de fragmentos de código modificable. 

  ![Fragmentos de código SQL](./media/sql-server-linux-develop-use-vscode/vscode-sql-snippets.png)   
   
1. Seleccione **sqlCreateDatabase**.
   
1. En el fragmento de código, reemplace `DatabaseName` con `TutorialDB`:
   
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
> Puede personalizar las teclas de método abreviado para los comandos de mssql. Consulte [personalizar métodos abreviados].

## <a name="create-a-table"></a>Creación de una tabla

1. Elimine el contenido de la ventana del editor de código.
   
1. Presione **Ctrl**+**MAYÚS**+**P** o **F1** para abrir el **paleta de comandos**. 
   
1. Tipo *sql* para mostrar el mssql comandos o tipo *sqluse*y, a continuación, seleccione el **base de datos de MS SQL** comando.
   
1. Seleccione la nueva **TutorialDB** base de datos. 
   
   ![Usar base de datos](./media/sql-server-linux-develop-use-vscode/vscode-use-database.png)   
   
1. En el editor de código, escriba *sql* para mostrar los fragmentos de código, seleccione **sqlCreateTable**y, a continuación, presione **ENTRAR**.
   
1. En el fragmento de código, escriba *empleados* para el nombre de tabla y *dbo* para el nombre del esquema.
   
1. Cree las columnas tal como se muestra en el código siguiente:
   
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
   
   > [!TIP]
   > Mientras escribe, use Transact-SQL IntelliSense para ayudar a completar las instrucciones.
   >![Transact-SQL IntelliSense](./media/sql-server-linux-develop-use-vscode/vscode-intellisense.png)   
   
1. Presione **Ctrl**+**MAYÚS**+**E** para ejecutar los comandos. Dar lugar a los dos conjuntos de presentación en el **resultados** ventana. 
   
   ![Resultado](./media/sql-server-linux-develop-use-vscode/vscode-result-grid.png)   

## <a name="view-and-save-the-result"></a>Ver y guardar el resultado
   
1. Seleccione **vista** > **Editor diseño** > **voltear diseño** para cambiar a un diseño de división vertical u horizontal.
   
1. Seleccione el **resultados** y **mensajes** encabezados para contraer y expandir los paneles del panel.
   
   ![Encabezados de alternancia](./media/sql-server-linux-develop-use-vscode/vscode-toggle-messages-pannel.png)   
   
   > [!TIP]
   > Puede personalizar el comportamiento predeterminado de la extensión mssql. Consulte [personalizar las opciones de extensión].
   
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

Si está familiarizado con Transact-SQL, consulte [Tutorial: Escribir instrucciones Transact-SQL] y [referencia de Transact-SQL (motor de base de datos)].

Para obtener más información sobre el uso o que contribuyen a la extensión mssql, consulte el [wiki de proyecto de extensión mssql].

Para obtener más información sobre el uso de Visual Studio Code, consulte el [documentación de Visual Studio Code](https://code.visualstudio.com/docs).

[extensión MSSQL para Visual Studio Code]:https://aka.ms/mssql-marketplace
[Descargue e instale Visual Studio Code]:https://code.visualstudio.com/Download
[.Net Core instructions]:https://www.microsoft.com/net/core
[Administrar perfiles de conexión]:https://github.com/Microsoft/vscode-mssql/wiki/manage-connection-profiles
[recomendaciones para solucionar problemas de conexión]:./sql-server-linux-troubleshooting-guide.md#connection
[personalizar métodos abreviados]:https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts
[Tutorial: Escribir instrucciones Transact-SQL]:https://docs.microsoft.com/sql/t-sql/tutorial-writing-transact-sql-statements
[Referencia de Transact-SQL (motor de base de datos)]:https://docs.microsoft.com/sql/t-sql/language-reference
[Visual Studio Code documentation]:https://code.visualstudio.com/docs
[Windows 10 Universal C Runtime]:https://github.com/Microsoft/vscode-mssql/wiki/windows10-universal-c-runtime-requirement
[personalizar las opciones de extensión]: https://github.com/Microsoft/vscode-mssql/wiki/customize-options
[wiki de proyecto de extensión MSSQL]: https://github.com/Microsoft/vscode-mssql/wiki
