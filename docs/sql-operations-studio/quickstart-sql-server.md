---
title: 'Inicio rápido: Conectarse y consultar SQL Server mediante SQL Operations Studio (versión preliminar) | Microsoft Docs'
description: En este tutorial rápido se muestra cómo usar SQL Operations Studio (versión preliminar) para conectarse a SQL Server y ejecute una consulta
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 7f8963de448c39709a4df102cdf764a361b7654c
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985077"
---
# <a name="quickstart-connect-and-query-sql-server-using-includename-sosincludesname-sos-shortmd"></a>Inicio rápido: Conectarse y consultar mediante SQL Server [!INCLUDE[name-sos](../includes/name-sos-short.md)]
En este tutorial rápido se muestra cómo usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse a SQL Server y, a continuación, usar instrucciones Transact-SQL (T-SQL) para crear el *TutorialDB* utilizados en [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriales.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial rápido, necesitará [!INCLUDE[name-sos](../includes/name-sos-short.md)]y el acceso a un servidor SQL Server.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Si no tiene acceso a un servidor SQL Server, seleccione su plataforma desde los vínculos siguientes (asegúrese de recordar el inicio de sesión de SQL y la contraseña!):
- [Windows - Descargar SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
- [macOS - Descargar SQL Server 2017 en Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker)
- [Linux: descarga de SQL Server 2017 Developer Edition](https://docs.microsoft.com/sql/linux/sql-server-linux-overview#install) -solo deberá seguir los pasos hasta *crear y consultar datos*.


## <a name="connect-to-a-sql-server"></a>Conectarse a un servidor SQL Server

   
1. Iniciar **[!INCLUDE[name-sos](../includes/name-sos-short.md)]**.
1. La primera vez que ejecute *[!INCLUDE[name-sos](../includes/name-sos-short.md)]* el **conexión** abre el cuadro de diálogo. Si el **conexión** no abre el cuadro de diálogo, haga clic en el **nueva conexión** icono en el **servidores** página:
   
   ![Nuevo icono de conexión](media/quickstart-sql-server/new-connection-icon.png)

1. Este artículo se usa *inicio de sesión SQL*, pero *Windows autenticación* se admite. Rellene los campos como sigue:
 
    - **Nombre del servidor:** localhost
    - **Tipo de autenticación:** inicio de sesión SQL  
    - **Nombre de usuario:** nombre de usuario de SQL Server  
    - **Contraseña:** contraseña de SQL Server  
    - **Nombre de la base de datos:** deje este campo en blanco 
    - **Grupo de servidores:** \<predeterminado\>  

   ![Nueva pantalla de conexión](media/quickstart-sql-server/new-connection-screen.png)



## <a name="create-a-database"></a>Crear una base de datos

Los pasos siguientes crean una base de datos denominada **TutorialDB**:

1. Haga clic con el botón derecho en el servidor, **localhost**y seleccione **nueva consulta.**
1. Pegue el siguiente fragmento de código en la ventana de consulta: 

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

   ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
   GO
   ```
1. Para ejecutar la consulta, haga clic en **ejecutar** .

Una vez finalizada la consulta, el nuevo **TutorialDB** aparece en la lista de bases de datos. Si no lo ve, haga clic en el **bases de datos** nodo y seleccione **actualizar**.


## <a name="create-a-table"></a>Creación de una tabla

El editor de consultas aún está conectado a la *maestro* base de datos, pero si desea crear una tabla en la *TutorialDB* base de datos. 

1. Cambiar el contexto de conexión a **TutorialDB**:

   ![Cambio de contexto](media/quickstart-sql-server/change-context.png)



1. Pegue el siguiente fragmento de código en la ventana de consulta y haga clic en **ejecutar**:

   > [!NOTE]
   > Puede esta opción para anexar o sobrescribir la consulta anterior en el editor. Tenga en cuenta que al hacer clic **ejecutar** ejecuta solo la consulta seleccionada. Si se selecciona nada, haga clic en **ejecutar** ejecuta todas las consultas en el editor.

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

Una vez finalizada la consulta, el nuevo **clientes** tabla aparece en la lista de tablas. Es posible que deba haga el **TutorialDB > tablas** nodo y seleccione **actualizar**.

## <a name="insert-rows"></a>Insertar filas

- Pegue el siguiente fragmento de código en la ventana de consulta y haga clic en **ejecutar**:

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



## <a name="view-the-data-returned-by-a-query"></a>Ver los datos devueltos por una consulta
1. Pegue el siguiente fragmento de código en la ventana de consulta y haga clic en **ejecutar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Se muestran los resultados de la consulta:

   ![Seleccione los resultados](media/quickstart-sql-server/select-results.png)


## <a name="next-steps"></a>Pasos siguientes
Ahora que ha conectado correctamente a SQL Server y ejecute una consulta, pruebe el [tutorial del editor de código](tutorial-sql-editor.md).


