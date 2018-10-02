---
Title: 'Tutorial: Connect to and query a SQL Server instance by using SQL Server Management Studio'
description: Tutorial para conectarse a una instancia de SQL Server usando SQL Server Management Studio y ejecutando consultas básicas de T-SQL.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.prod: sql
ms.technology: ssms
ms.openlocfilehash: 02aee760447f61867f5ec85bbe24266539a44a33
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738253"
---
# <a name="tutorial-connect-to-and-query-a-sql-server-instance-by-using-sql-server-management-studio"></a>Tutorial: Conectarse a una instancia de SQL Server y efectuar consultas con SQL Server Management Studio
En este tutorial aprenderá a usar SQL Server Management Studio (SSMS) para conectarse a su instancia de SQL Server y a ejecutar algunos comandos básicos de Transact-SQL (T-SQL). En el artículo se muestra cómo hacer lo siguiente:

> [!div class="checklist"]  
> * Conectarse a una instancia de SQL Server    
> * Crear una base de datos ("TutorialDB")    
> * Crear una tabla ("Customers") en la nueva base de datos   
> * Insertar filas en la nueva tabla 
> * Consultar la nueva tabla y ver los resultados    
> * Usar la tabla de la ventana de consulta para comprobar las propiedades de la conexión 
> * Cambiar el servidor al que está conectada la ventana de consulta

## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, así como acceso a una instancia de SQL Server. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Si no tiene acceso a ninguna instancia de SQL Server, seleccione su plataforma en uno de los vínculos siguientes. Si elige la autenticación de SQL, use sus credenciales de inicio de sesión de SQL Server.
- **Windows**: [Descargar SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [Descargar SQL Server 2017 en Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).


## <a name="connect-to-a-sql-server-instance"></a>Conectarse a una instancia de SQL Server

1. Inicie SQL Server Management Studio. La primera vez que ejecute SSMS se abrirá la ventana **Conectarse al servidor**. Si no se abre, puede abrirla manualmente seleccionando **Explorador de objetos** > **Conectar** > **Motor de base de datos**.

    ![Vínculo Conectar en el Explorador de objetos](media/connect-query-sql-server/connectobjexp.png)

2. En la ventana **Conectar al servidor**, haga lo siguiente: 

    - En **Tipo de servidor**, seleccione **Motor de base de datos** (suele ser la opción predeterminada).
    - En **Nombre del servidor**, escriba el nombre de su instancia de SQL Server (en este artículo se usa el nombre de instancia SQL2016ST en el nombre de host NODE5 [NODE5\SQL2016ST]). Si no sabe cómo determinar el nombre de la instancia de SQL Server, vea [Otras recomendaciones y trucos al usar SSMS](ssms-tricks.md#determine-sql-server-name).  

    ![Campo "Nombre del servidor" con la opción para usar la instancia de SQL Server](media/connect-query-sql-server/connection2.png)

    - En **Autenticación**, seleccione **Autenticación de Windows**. En este artículo se usa la autenticación de Windows, aunque también se admite el inicio de sesión de SQL Server. Si selecciona **Inicio de sesión SQL**, se le pedirá un nombre de usuario y una contraseña. Para más información sobre los tipos de autenticación, vea [Conectar al servidor (motor de base de datos)](https://docs.microsoft.com/sql/ssms/f1-help/connect-to-server-database-engine).

    También puede modificar otras opciones de conexión seleccionando **Opciones**. Como ejemplos de las opciones de conexión tiene la base de datos a la que se está conectando, el valor de tiempo de espera de conexión y el protocolo de red. En este artículo se usan los valores predeterminados para todas las opciones. 

3. Una vez cumplimentados todos los campos, seleccione **Conectar**. 

### <a name="examples-of-successful-connections"></a>Ejemplos de conexiones correctas
Para comprobar que la conexión a SQL Server se ha establecido correctamente, expanda y explore los objetos del **Explorador de objetos**. Estos objetos serán diferentes en función del tipo de servidor al que se haya conectado. 

- Conexión a un servidor local de SQL Server (en este caso, NODE5\SQL2016ST): ![Conexión a un servidor local](media/connect-query-sql-server/connect-on-prem.png)

- Conexión a SQL Azure DB (en este caso, msftestserver.database.windows.net): ![Conexión a SQL Azure DB](media/connect-query-sql-server/connect-sql-azure.png)

  >[!NOTE]
  > En este tutorial ha usado la *autenticación de Windows* para conectarse al servidor local de SQL Server, pero este método no es compatible con SQL Azure DB. Por lo tanto, en esta imagen se muestra el uso de la autenticación de SQL para conectarse a SQL Azure DB. Para más información, vea [Autenticación de SQL local](../../relational-databases/security/choose-an-authentication-mode.md) y [Autenticación de SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview#control-access). 

## <a name="create-a-database"></a>Crear una base de datos
Cree una base de datos denominada TutorialDB siguiendo estos pasos: 

1. Haga clic con el botón derecho en la instancia del servidor en el Explorador de objetos y seleccione **Nueva consulta**:

   ![Vínculo Nueva consulta](media/connect-query-sql-server/newquery.png)
   
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
2. Para ejecutar la consulta, seleccione **Ejecutar** (o presione F5 en el teclado). 

   ![Comando Ejecutar](media/connect-query-sql-server/execute.png)
  
    Una vez hecha la consulta, en la lista de bases de datos del Explorador de objetos aparecerá la nueva base de datos TutorialDB. Si no aparece, haga clic con el botón derecho en el nodo **Bases de datos** y seleccione **Actualizar**.  


## <a name="create-a-table-in-the-new-database"></a>Crear una tabla en la nueva base de datos
En esta sección creará una tabla en la base de datos TutorialDB recién creada. Como el editor de consultas sigue en el contexto de la base de datos *master*, debe cambiar el contexto de la conexión a la base de datos *TutorialDB* siguiendo estos pasos: 

1. En la lista desplegable de bases de datos, seleccione la base de datos que quiera, como se muestra aquí: 

   ![Cambiar la base de datos](media/connect-query-sql-server/changedb.png)

2. Pegue el siguiente fragmento de código de T-SQL en la ventana de consulta, selecciónelo y, después, seleccione **Ejecutar** (o presione F5 en el teclado).  
   Puede reemplazar el texto existente de la ventana de consulta o anexarlo al final. Si quiere ejecutarlo todo en la ventana de consulta, seleccione **Ejecutar**. Si quiere ejecutar una parte del texto, resalte esa parte y seleccione **Ejecutar**.  
  
   ```sql
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

   ![Lista de resultados](media/connect-query-sql-server/queryresults.png)

2. Puede modificar el modo de visualización de los resultados seleccionando una de las siguientes opciones:

     ![Tres opciones para mostrar los resultados de la consulta](media/connect-query-sql-server/results.png)

    - El botón central muestra los resultados en una **vista de cuadrícula**, que es la opción predeterminada. 
    - El primer botón muestra los resultados en una **vista de texto**, tal y como se muestra en la imagen de la siguiente sección.
    - El tercer botón le permite guardar los resultados en un archivo cuya extensión es .rpt de forma predeterminada.

## <a name="verify-your-connection-properties-by-using-the-query-window-table"></a>Comprobar las propiedades de la conexión usando la tabla de la ventana de consulta
Puede buscar información sobre las propiedades de la conexión en los resultados de la consulta. Después de ejecutar la consulta mencionada en el paso anterior, revise las propiedades de la conexión en la parte inferior de la ventana de consulta.

- Puede determinar el servidor y la base de datos a los que se ha conectado, así como el nombre de usuario con el que ha iniciado sesión.
- También puede ver la duración de la consulta y el número de filas devueltas por la consulta ejecutada.

    ![Propiedades de la conexión](media/connect-query-sql-server/connectionproperties.png)
    
    En la imagen, observe que los resultados se muestran en una **vista de texto**. 

## <a name="change-the-server-that-the-query-window-is-connected-to"></a>Cambiar el servidor al que está conectada la ventana de consulta
Siga estos pasos para cambiar el servidor al que está conectada la ventana de consulta actual:

1. Haga clic con el botón derecho en la ventana de consulta y, después, seleccione **Conexión** > **Cambiar conexión**. Se volverá a abrir la ventana **Conectar al servidor**.
2. Cambie el servidor al que está conectada la consulta. 
 
   ![Comando Cambiar conexión](media/connect-query-sql-server/changeconnection.png)

    > [!NOTE]
    > Esta acción cambia solo el servidor al que está conectada la ventana de consulta, y no el servidor al que está conectado el Explorador de objetos. 

## <a name="next-steps"></a>Pasos siguientes
En el siguiente artículo se muestra cómo programar varios objetos en SQL Server Management Studio. 

Vaya al siguiente artículo para más información:
> [!div class="nextstepaction"]
> [Pasos siguientes](scripting-ssms.md)


