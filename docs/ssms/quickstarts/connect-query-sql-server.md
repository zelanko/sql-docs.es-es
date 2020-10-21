---
title: Conexión a una instancia de SQL Server y realización de consultas
description: Conéctese una instancia de SQL Server a través de SQL Server Management Studio y mediante la ejecución de consultas básicas de T-SQL.
ms.prod: sql
ms.technology: ssms
ms.topic: quickstart
author: markingmyname
ms.author: maghan
ms.reviewer: sstein
ms.custom: seo-lt-2019
ms.date: 09/28/2020
ms.openlocfilehash: d44e59e8dfdd9ba38feb2c860348f44af325c768
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038393"
---
# <a name="quickstart-connect-to-and-query-a-sql-server-instance-by-using-sql-server-management-studio-ssms"></a>Inicio rápido: Conexión a una instancia de SQL Server y realización de consultas con SQL Server Management Studio (SSMS)

[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

En este inicio rápido aprenderá a usar SQL Server Management Studio (SSMS) para conectarse a su instancia de SQL Server y a ejecutar algunos comandos básicos de Transact-SQL (T-SQL). En el artículo se muestra cómo seguir estos pasos:

> [!div class="checklist"]
> * Conectarse a una instancia de SQL Server
> * Crear una base de datos ("TutorialDB")
> * Crear una tabla ("Customers") en la nueva base de datos
> * Insertar filas en la nueva tabla
> * Consultar la nueva tabla y ver los resultados
> * Usar la tabla de la ventana de consulta para comprobar las propiedades de la conexión
> * Cambiar el servidor al que está conectada la ventana de consulta

## <a name="prerequisites"></a>Requisitos previos

Para completar este artículo, necesita tener SQL Server Management Studio, así como acceso a una instancia de SQL Server.

* Instale [SQL Server Management Studio](../download-sql-server-management-studio-ssms.md).

Si no tiene acceso a ninguna instancia de SQL Server, seleccione su plataforma en uno de los vínculos siguientes. Si elige la autenticación de SQL, use sus credenciales de inicio de sesión de SQL Server.

* **Windows**: [descargue SQL Server 2019 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
* **macOS**: [descargue SQL Server 2019 en Docker](../../linux/quickstart-install-connect-docker.md).

## <a name="connect-to-a-sql-server-instance"></a>Conectarse a una instancia de SQL Server

[!INCLUDE[ssms-connect-azure-ad](../../includes/ssms-connect-azure-ad.md)]

1. Inicie SQL Server Management Studio. La primera vez que ejecute SSMS se abrirá la ventana **Conectarse al servidor**. Si no se abre, puede abrirla manualmente seleccionando **Explorador de objetos** > **Conectar** > **Motor de base de datos**.

    ![Vínculo Conectar en el Explorador de objetos](media/connect-query-sql-server/connect-object-explorer.png)

2. En la ventana **Conectar al servidor**, siga esta lista:

    * En **Tipo de servidor**, seleccione **Motor de base de datos** (suele ser la opción predeterminada).
    * En **Nombre del servidor**, escriba el nombre de su instancia de SQL Server (en este artículo se usa el nombre de instancia SQL2016ST en el nombre de host NODE5 [NODE5\SQL2016ST]). Si no sabe cómo determinar el nombre de la instancia de SQL Server, vea [Otras recomendaciones y trucos al usar SSMS](../tutorials/ssms-tricks.md#find-sql-server-instance-name).
    * En **Autenticación**, seleccione **Autenticación de Windows**. En este artículo se usa la autenticación de Windows, aunque también se admite el inicio de sesión de SQL Server. Si selecciona **Inicio de sesión SQL**, se le pedirá un nombre de usuario y una contraseña. Para obtener más información sobre los tipos de autenticación, vea [Conectar al servidor (motor de base de datos)](../f1-help/connect-to-server-database-engine.md).

    ![Campo "Nombre del servidor" con la opción para usar la instancia de SQL Server](media/connect-query-sql-server/connection-2.png)

    También puede modificar otras opciones de conexión seleccionando **Opciones**. Como ejemplos de las opciones de conexión tiene la base de datos a la que se está conectando, el valor de tiempo de espera de conexión y el protocolo de red. En este artículo se usan los valores predeterminados para todas las opciones.

3. Una vez cumplimentados todos los campos, seleccione **Conectar**.

### <a name="examples-of-successful-connections"></a>Ejemplos de conexiones correctas

Para comprobar que la conexión a SQL Server se ha establecido correctamente, expanda y explore los objetos del **Explorador de objetos**. Estos objetos son diferentes en función del tipo de servidor al que decida conectarse.

* Conexión a un servidor local de SQL Server (en este caso, NODE5\SQL2016ST): ![Conexión a un servidor local](media/connect-query-sql-server/connect-on-prem.png)

* Conexión a SQL Azure DB (en este caso, msftestserver.database.windows.net): ![Conexión a SQL Azure DB](media/connect-query-sql-server/connect-sql-azure.png)

> [!NOTE]
> En este artículo ha usado la *autenticación de Windows* para conectarse a la instancia local de SQL Server, pero este método no es compatible con SQL Azure DB. Por lo tanto, en esta imagen se muestra el uso de la autenticación de SQL para conectarse a SQL Azure DB. Para más información, vea [Autenticación de SQL local](../../relational-databases/security/choose-an-authentication-mode.md) y [Autenticación de SQL Azure](/azure/sql-database/sql-database-security-overview#access-management).

## <a name="create-a-database"></a>Crear una base de datos

Haga lo siguiente para crear una base de datos denominada TutorialDB:

1. Haga clic con el botón derecho en la instancia del servidor en el Explorador de objetos y seleccione **Nueva consulta**:

   ![Vínculo Nueva consulta](media/connect-query-sql-server/new-query.png)

2. En la ventana de consulta, pegue el siguiente fragmento de código de T-SQL:

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

3. Para ejecutar la consulta, seleccione **Ejecutar** (o presione F5 en el teclado).

   ![Comando Ejecutar](media/connect-query-sql-server/execute.png)
  
    Una vez hecha la consulta, en la lista de bases de datos del Explorador de objetos aparecerá la nueva base de datos TutorialDB. Si no aparece, haga clic con el botón derecho en el nodo **Bases de datos** y seleccione **Actualizar**.  

## <a name="create-a-table-in-the-new-database"></a>Crear una tabla en la nueva base de datos

En esta sección creará una tabla en la base de datos TutorialDB recién creada. Como el editor de consultas sigue en el contexto de la base de datos *master*, debe cambiar el contexto de la conexión a la base de datos *TutorialDB* siguiendo estos pasos:

1. En la lista desplegable de bases de datos, seleccione la base de datos que quiera, como se muestra aquí:

   ![Cambiar la base de datos](media/connect-query-sql-server/change-db.png)

2. Pegue el siguiente fragmento de código de T-SQL en la ventana de consulta, selecciónelo y, después, seleccione **Ejecutar** (o presione F5 en el teclado).  
   Puede reemplazar el texto existente de la ventana de consulta o anexarlo al final. Si quiere ejecutarlo todo en la ventana de consulta, seleccione **Ejecutar**. Si ha anexado el texto, querrá ejecutar solo la parte del texto, así que resáltela y, después, seleccione **Ejecutar**.  
  
   ```sql
   USE [TutorialDB]
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```

Una vez hecha la consulta, se mostrará la nueva tabla Customers (Clientes) en la lista de tablas del Explorador de objetos. Si la tabla no aparece, haga clic con el botón derecho en el nodo **TutorialDB** > **Tablas** en el Explorador de objetos y, después, seleccione **Actualizar**.

## <a name="insert-rows-into-the-new-table"></a>Insertar filas en la nueva tabla

Inserte algunas filas en la tabla Customers que ha creado antes. Para ello, pegue el siguiente fragmento de código de T-SQL en la ventana de consulta y, después, seleccione **Ejecutar**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
   VALUES
      ( 1, N'Orlando', N'Australia', N''),
      ( 2, N'Keith', N'India', N'keith0@adventure-works.com'),
      ( 3, N'Donna', N'Germany', N'donna0@adventure-works.com'),
      ( 4, N'Janet', N'United States', N'janet1@adventure-works.com')
   GO
   ```

## <a name="query-the-table-and-view-the-results"></a>Consultar la tabla y ver los resultados

Los resultados de una consulta aparecen debajo de la ventana de texto de la consulta. Siga estos pasos para consultar la tabla Customers y ver las filas que se han insertado antes:

1. Pegue el siguiente fragmento de código de T-SQL en la ventana de consulta y, después, seleccione **Ejecutar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

    Los resultados de la consulta se muestran debajo del área en la que se ha escrito el texto: 

   ![Lista de resultados](media/connect-query-sql-server/query-results.png)

2. Puede modificar el modo de visualización de los resultados seleccionando una de las siguientes opciones:

     ![Tres opciones para mostrar los resultados de la consulta](media/connect-query-sql-server/results.png)

    * El botón central muestra los resultados en una **vista de cuadrícula**, que es la opción predeterminada.
    * El primer botón muestra los resultados en una **vista de texto**, tal y como se muestra en la imagen de la siguiente sección.
    * El tercer botón le permite guardar los resultados en un archivo cuya extensión es .rpt de forma predeterminada.

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>Comprobar las propiedades de la conexión usando la tabla de la ventana de consulta

Puede buscar información sobre las propiedades de la conexión en los resultados de la consulta. Después de ejecutar la consulta mencionada en el paso anterior, revise las propiedades de la conexión en la parte inferior de la ventana de consulta.

* Puede determinar el servidor y la base de datos a los que se ha conectado, así como el nombre de usuario que ha utilizado.
* También puede ver la duración de la consulta y el número de filas devueltas por la consulta ejecutada.

    ![Propiedades de la conexión](media/connect-query-sql-server/connection-properties.png)

    > [!Note]
    > En la imagen, los resultados se muestran en una **vista de texto**.

## <a name="change-the-server-based-on-the-query-window"></a>Cambio del servidor según la ventana de consulta

Siga estos pasos para cambiar el servidor al que está conectada la ventana de consulta actual:

1. Haga clic con el botón derecho en la ventana de consulta y, después, seleccione **Conexión** > **Cambiar conexión**. Se volverá a abrir la ventana **Conectar al servidor**.

2. Cambie el servidor que la consulta usa.

   ![Comando Cambiar conexión](media/connect-query-sql-server/change-connection.png)

    > [!NOTE]
    > Esta acción cambia solo el servidor al que está conectada la ventana de consulta, y no el servidor que el Explorador de objetos usa.

## <a name="azure-data-studio"></a>Azure Data Studio

También puede conectarse y consultar [SQL Server](../../azure-data-studio/quickstart-sql-server.md), [Azure SQL Database](../../azure-data-studio/quickstart-sql-database.md)y [Azure Synapse Analytics](../../azure-data-studio/quickstart-sql-dw.md) con Azure Data Studio.

## <a name="next-steps"></a>Pasos siguientes

La mejor forma de familiarizarse con SSMS es practicar. Estos artículos lo ayudan con varias características disponibles dentro de SSMS. Estos artículos le mostrarán cómo administrar los componentes de SSMS y cómo localizar las características que utiliza habitualmente.

* [Scripting](../tutorials/scripting-ssms.md)
* [Uso de plantillas en SSMS](../template/templates-ssms.md)
* [Configuración de SSMS](../tutorials/ssms-configuration.md)
* [Otras recomendaciones y trucos al usar SSMS](../tutorials/ssms-tricks.md)
* [Azure Data Studio](../../azure-data-studio/download-azure-data-studio.md)