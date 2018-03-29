---
Title: 'Tutorial: Connect and Query SQL Server using SQL Server Management Studio'
description: Tutorial para conectarse a SQL Server con SQL Server Management Studio y ejecutando consultas básicas de T-SQL.
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
ms.openlocfilehash: 6f4110a0ae1b4ca349cc9b990cc9a32f7d41764d
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-connect-and-query-sql-server-using-sql-server-management-studio"></a>Tutorial: Conectarse a SQL Server y efectuar consultas con SQL Server Management Studio
En este tutorial aprenderá a usar SQL Server Management Studio (SSMS) para conectarse a su instancia de SQL Server y a ejecutar algunos comandos básicos de Transact-SQL (T-SQL). En este artículo se muestra cómo hacer lo siguiente:

> [!div class="checklist"]
> * [Conectarse a un servidor SQL Server](#connect-to-a-sql-server)
> * [Crear una base de datos (**TutorialDB**)](#create-a-database)
> * [Crear una tabla (**Customers**) en la nueva base de datos](#create-a-table)
> * [Insertar filas en la nueva tabla **Customers**](#insert-rows)
> * [Consultar la tabla **Customers** y ver los resultados](#view-query-results)
> * [Usar la tabla de la ventana de consulta para comprobar las propiedades de la conexión](#verify-your-query-window-connection-properties)
> * [Cambiar el servidor al que está conectada la ventana de consulta](#change-server-connection-within-query-window)


## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, así como acceso a un servidor SQL Server. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).

Si no tiene acceso a SQL Server, seleccione su plataforma en uno de los vínculos siguientes (deberá acordarse de sus credenciales de inicio de sesión de SQL y de su contraseña si elige la autenticación de SQL):
- [Windows - Descargar SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS - Descargar SQL Server 2017 en Docker](https://docs.microsoft.com/en-us/sql/linux/quickstart-install-connect-docker)


## <a name="connect-to-a-sql-server"></a>Conectarse a un servidor SQL Server

1. Inicie SQL Server Management Studio (SSMS).
1. La primera vez que ejecute SSMS, se abrirá el cuadro de diálogo **Conectarse al servidor**. 
      - Si el cuadro de diálogo **Conectarse al servidor** no se abre, se puede abrir manualmente en el **Explorador de objetos** > **Conectar** (o el icono situado al lado) >  **Motor de base de datos**.

        ![Conectar en el Explorador de objetos](media/connect-query-sql-server/connectobjexp.png)

1. En el cuadro de diálogo **Conectarse al servidor**, rellene las opciones de conexión: 

    - **Tipo de servidor**: Motor de base de datos (normalmente está seleccionado de forma predeterminada)
    - **Autenticación**: Autenticación de Windows (en este artículo se usa la autenticación de Windows, pero también se admite el inicio de sesión de SQL, en el que se le pedirá un nombre de usuario y una contraseña si lo selecciona)

      ![Conexión](media/connect-query-sql-server/connection.png)

        También puede modificar otras opciones de conexión (por ejemplo, la base de datos a la que se conectará, el valor de tiempo de espera de conexión y el protocolo de red) haciendo clic en el botón **Opciones**. Para este artículo se ha dejado todo en los valores predeterminados. 

1. Una vez que se hayan rellenado los campos, haga clic en **Conectar**. 

1. Puede comprobar que la conexión se ha establecido correctamente con el servidor SQL Server explorando los objetos en el **Explorador de objetos**: 

   ![Conexión correcta](media/connect-query-sql-server/successfulconnection.png)


## <a name="create-a-database"></a>Crear una base de datos
En los pasos siguientes se crea una base de datos denominada TutorialDB. 

1. Haga clic con el botón derecho en el servidor en el **Explorador de objetos** y seleccione **Nueva consulta**:

   ![Nueva consulta](media/connect-query-sql-server/newquery.png)
   
1. Pegue el siguiente fragmento de código de T-SQL en la ventana de consulta: 
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
2. Para ejecutar la consulta, haga clic en **Ejecutar** (o presione F5 en el teclado). 

   ![Ejecutar consulta](media/connect-query-sql-server/execute.png)
  
 
Una vez hecha la consulta, aparecerá la nueva **TutorialDB** en la lista de bases de datos del **Explorador de objetos**. Si no la ve, haga clic con el botón derecho en el nodo Bases de datos y seleccione **Actualizar**.  


## <a name="create-a-table"></a>Crear una tabla
En los siguientes pasos se creará una tabla en la base de datos **TutorialDB** que acaba de crear, pero el editor de consultas aún está en el contexto de la base de datos *master* y usted quiere crear una tabla en la base de datos *TutorialDB*. 

1. Cambie el contexto de la conexión de la consulta de la base de datos master (maestra) a **TutorialDB**. Para ello, seleccione la base de datos que quiera en la lista desplegable de bases de datos. 

   ![Cambiar la base de datos](media/connect-query-sql-server/changedb.png)

1. Pegue el siguiente fragmento de código de T-SQL en la ventana de consulta, resáltelo y haga clic en **Ejecutar** (o presione F5 en el teclado): 
    - Puede reemplazar el texto existente de la ventana de consulta o anexarlo al final. Si quiere ejecutarlo todo en la ventana de consulta, haga clic en **Ejecutar**. Si quiere ejecutar una parte del texto, resalte esa parte y haga clic en **Ejecutar**.  
  
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
Una vez hecha la consulta, aparecerá la tabla nueva **Customers** (Clientes) en la lista de tablas del **Explorador de objetos**. Si la tabla no está visible, haga clic con el botón derecho en el nodo **TutorialDB > Tablas** en el **Explorador de objetos** y seleccione **Actualizar**.

## <a name="insert-rows"></a>Insertar filas
En el siguiente paso se insertarán algunas filas en la tabla **Customers** que ha creado antes. 

Pegue el siguiente fragmento de código de T-SQL en la ventana de consulta y haga clic en **Ejecutar**: 


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

## <a name="view-query-results"></a>Ver los resultados de la consulta
Los resultados de una consulta aparecen debajo de la ventana de texto de la consulta. En los siguientes pasos podrá consultar la tabla **Customers** y ver las filas que se han insertado.  

1. Pegue el siguiente fragmento de código de T-SQL en la ventana de consulta y haga clic en **Ejecutar**: 

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```
1. Los resultados de la consulta se muestran debajo del área en la que se ha escrito el texto: 

   ![Resultados de la consulta](media/connect-query-sql-server/queryresults.png)


1.  Puede modificar el modo de visualización de los resultados seleccionando una de estas opciones:

     ![resultados](media/connect-query-sql-server/results.png)

    - De forma predeterminada, los resultados se mostrarán en una **vista de cuadrícula**, que es el botón central y muestra los resultados en una tabla. 
    - El primer botón mostrará los resultados en una **vista de texto**, tal y como se muestra en la imagen de la siguiente sección.
    - Con el tercer botón podrá guardar los resultados en un archivo, que de forma predeterminada acaba en *.rpt.

## <a name="verify-your-query-window-connection-properties"></a>Comprobar las propiedades de la conexión de la ventana de consulta
Puede buscar información sobre las propiedades de la conexión en los resultados de la consulta. 
- Después de ejecutar la consulta mencionada del paso anterior, revise las propiedades de la conexión en la parte inferior de la ventana de consulta.
    - Puede determinar el servidor y la base de datos a los que se ha conectad, así como el usuario con el que ha iniciado sesión.
    - También puede ver la duración de la consulta y el número de filas devueltas por la consulta que se ha ejecutado.
    
    ![Propiedades de la conexión](media/connect-query-sql-server/connectionproperties.png)  
    En esta imagen, los resultados se muestran en una **vista de texto**.  

## <a name="change-server-connection-within-query-window"></a>Cambiar la conexión del servidor en la ventana de consulta
Puede cambiar el servidor al que se ha conectado la ventana de consulta actual siguiendo estos pasos.
1. Haga clic con el botón derecho en la ventana de consulta > Conexión > Cambiar conexión.
2. Se volverá a abrir el cuadro de diálogo **Conectarse al servidor**, donde podrá cambiar el servidor al que se ha conectado la consulta. 
 
   ![Cambiar conexión](media/connect-query-sql-server/changeconnection.png)
   - Tenga en cuenta que con esto no se cambia el servidor al que se ha conectado el **Explorador de objetos**, sino solo la ventana de consulta actual. 



