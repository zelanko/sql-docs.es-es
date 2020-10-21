---
title: Conexión a Azure Synapse Analytics y realización de consultas
description: En esta guía de inicio rápido se muestra cómo usar Azure Data Studio para conectarse a Azure Synapse Analytics mediante un grupo de SQL dedicado, y ejecutar una consulta.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.reviewer: alayu, maghan, sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
ms.custom: seodec18; seo-lt-2019
ms.date: 09/24/2018
ms.openlocfilehash: c2282220dff18a7f054cc5fd01b3670b6fd14d43
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005492"
---
# <a name="quickstart-use-azure-data-studio-to-connect-and-query-data-using-dedicated-sql-pool-in-azure-synapse-analytics"></a>Inicio rápido: Uso de Azure Data Studio para conectarse y consultar datos mediante un grupo de SQL dedicado en Azure Synapse Analytics

En este inicio rápido, se muestra cómo usar Azure Data Studio para conectarse a Azure Synapse Analytics mediante un grupo de SQL dedicado y, después, usar instrucciones Transact-SQL para crear, insertar y seleccionar datos. 

## <a name="prerequisites"></a>Requisitos previos
Para completar esta guía de inicio rápido, necesita Azure Data Studio y un grupo de SQL dedicado en Azure Synapse Analytics.

- [Instale Azure Data Studio](./download-azure-data-studio.md?view=sql-server-ver15).

Si aún no tiene un grupo de SQL dedicado, vea [Creación de un grupo de SQL dedicado](/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Recuerde el nombre del servidor y las credenciales de inicio de sesión.


## <a name="connect-to-your-dedicated-sql-pool"></a>Conexión al grupo de SQL dedicado

Use Azure Data Studio para establecer una conexión con el servidor de Azure Synapse Analytics.

1. La primera vez que ejecute Azure Data Studio, se abrirá la página **Conexión**. Si no ve la página **Conexión**, haga clic en **Agregar conexión**, o bien en el icono de **Nueva conexión** en la barra lateral **SERVIDORES**:
   
   ![Icono de Nueva conexión](media/quickstart-sql-dw/new-connection-icon.png)

2. En este artículo, se usa el *inicio de sesión de SQL*, pero se admite la *autenticación de Windows*. Rellene los campos como se indica a continuación con el nombre del servidor, el nombre de usuario y la contraseña de *su instancia* de Azure SQL Server:

   | Configuración       | Valor sugerido | Descripción |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Nombre completo del servidor | El nombre tiene que ser similar a este: **sqldwsample.database.windows.net** |
   | **Autenticación** | Inicio de sesión SQL| En este tutorial, se usa la autenticación de SQL. |
   | **Nombre de usuario** | La cuenta de administrador del servidor | Es la cuenta que especificó cuando creó el servidor. |
   | **Contraseña (Inicio de sesión de SQL)** | La contraseña de la cuenta de administrador del servidor | Es la contraseña que especificó cuando creó el servidor. |
   | **¿Desea guardar la contraseña?** | Sí o no | Si no quiere escribir la contraseña cada vez, seleccione Sí. |
   | **Nombre de la base de datos** | *dejar en blanco* | Nombre de la base de datos a la que se va a conectar. |
   | **Grupo de servidores** | Seleccione <Default>. | Si ha creado un grupo de servidores, puede establecerlo en un grupo de servidores específico. | 

   ![Icono de Nueva conexión](media/quickstart-sql-dw/new-connection-screen.png) 

3. Si el servidor no tiene una regla de firewall que permita a Azure Data Studio conectarse, se abrirá el formulario **Crear nueva regla de firewall**. Rellene el formulario para crear una nueva regla de firewall. Para obtener detalles, vea [Reglas de firewall](/azure/sql-database/sql-database-firewall-configure).

   ![Nueva regla de firewall](media/quickstart-sql-dw/firewall.png)  

4. Después de conectarse correctamente, el servidor se abre en la barra lateral *SERVIDORES*.

## <a name="create-the-tutorial-dedicated-sql-pool"></a>Creación del grupo de SQL dedicado del tutorial
1. Haga clic con el botón derecho en el servidor (en el Explorador de objetos) y seleccione **Nueva consulta**.

1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **Ejecutar**:

   ```sql
    IF NOT EXISTS (
       SELECT name
       FROM sys.databases
       WHERE name = N'TutorialDB'
    )
    CREATE DATABASE [TutorialDB] (EDITION = 'datawarehouse', SERVICE_OBJECTIVE='DW100');
    GO  
    
    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
   ```


## <a name="create-a-table"></a>Creación de una tabla

El editor de consultas aún está conectado a la base de datos *maestra*, pero lo que queremos es crear una tabla en la base de datos *TutorialDB*. 

1. Cambie el contexto de conexión a **TutorialDB**:

   ![Cambiar el contexto](media/quickstart-sql-database/change-context.png)


1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **Ejecutar**:

   > [!NOTE]
   > Puede anexar esto, o bien puede sobrescribir la consulta anterior en el editor. Al hacer clic en **Ejecutar**, solo se ejecuta la consulta seleccionada. Si hay ninguna opción seleccionada, al hacer clic en **Ejecutar**, se ejecutarán todas las consultas en el editor.

   ```sql
   -- Create a new table called 'Customers' in schema 'dbo'
   -- Drop the table if it already exists
   IF OBJECT_ID('dbo.Customers', 'U') IS NOT NULL
   DROP TABLE dbo.Customers
   GO
   -- Create the table in the specified schema
   CREATE TABLE dbo.Customers
   (
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>Insertar filas

1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **Ejecutar**:

   ```sql
   -- Insert rows into table 'Customers'
   INSERT INTO dbo.Customers
      ([CustomerId],[Name],[Location],[Email])
      SELECT 1, N'Orlando',N'Australia', N'' UNION ALL
      SELECT 2, N'Keith', N'India', N'keith0@adventure-works.com' UNION ALL
      SELECT 3, N'Donna', N'Germany', N'donna0@adventure-works.com' UNION ALL
      SELECT 4, N'Janet', N'United States', N'janet1@adventure-works.com'
   ```


## <a name="view-the-result"></a>Ver el resultado
1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **Ejecutar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Se muestran los resultados de la consulta:

   ![Seleccionar los resultados](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>Limpieza de recursos

Otros artículos de esta colección se basan en este inicio rápido. Si tiene previsto continuar trabajando con otras guías de inicio rápido posteriores, no elimine los recursos creados en este inicio rápido. Si no tiene previsto continuar, siga este procedimiento para eliminar los recursos creados por este inicio rápido en Azure Portal.
Para limpiar los recursos, elimine los grupos de recursos que ya no necesite. Para obtener más información, vea [Limpieza de recursos](/azure/sql-database/sql-database-get-started-portal#clean-up-resources).


## <a name="next-steps"></a>Pasos siguientes

Ahora que ya se ha conectado correctamente a una instancia de Azure Synapse Analytics y ha ejecutado una consulta, pruebe el [Tutorial del editor de código](tutorial-sql-editor.md).