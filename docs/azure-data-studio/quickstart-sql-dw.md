---
title: 'Inicio rápido: Conectarse y consultar Azure SQL Data Warehouse'
titleSuffix: Azure Data Studio
description: En este tutorial rápido se muestra cómo usar Azure Data Studio para conectarse a Azure SQL Data Warehouse y ejecutar una consulta
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: f98f6be4502254910b5c144f08a95181ccf1b2a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800266"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>Inicio rápido: Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse y consultar datos en Azure SQL Data Warehouse

En este tutorial rápido se muestra cómo utilizar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse a Azure SQL data warehouse y, a continuación, usar instrucciones Transact-SQL para crear, insertar y seleccionar los datos. 

## <a name="prerequisites"></a>Requisitos previos
Para completar este tutorial rápido, necesitará [!INCLUDE[name-sos](../includes/name-sos-short.md)]y una instancia de Azure SQL data warehouse.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Si no dispone de un almacén de datos SQL, consulte [crear SQL Data Warehouse](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Recuerde el nombre del servidor y las credenciales de inicio de sesión.


## <a name="connect-to-your-data-warehouse"></a>Conectarse a su almacenamiento de datos

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para establecer una conexión al servidor de Azure SQL Data Warehouse.

1. La primera vez que ejecute [!INCLUDE[name-sos](../includes/name-sos-short.md)] el **conexión** debe abrir la página. Si no ve el **conexión** página, haga clic en **Agregar conexión**, o el **nueva conexión** icono en el **servidores** sidebar:
   
   ![Nuevo icono de conexión](media/quickstart-sql-dw/new-connection-icon.png)

2. Este artículo se usa *inicio de sesión SQL*, pero *Windows autenticación* también es compatible. Rellene los campos como se indica a continuación con el nombre del servidor, el nombre de usuario y la contraseña para *su* servidor SQL de Azure:

   | Configuración       | Valor sugerido | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Nombre completo del servidor | El nombre debe ser algo parecido a esto: **sqldwsample.database.windows.net** |
   | **Autenticación** | Inicio de sesión de SQL| En este tutorial, se utiliza la autenticación de SQL. |
   | **Nombre de usuario.** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña (inicio de sesión de SQL)** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |
   | **¿Desea guardar la contraseña?** | Sí o no | Seleccione Sí si no desea escribir la contraseña cada vez. |
   | **Nombre de la base de datos** | *Deje en blanco* | Nombre de la base de datos a la que se va a conectar. |
   | **Grupo de servidores** | Seleccione <Default> | Si ha creado un grupo de servidores, puede establecer para un grupo de servidores específicos. | 

   ![Nuevo icono de conexión](media/quickstart-sql-dw/new-connection-screen.png) 

3. 4\.Si el servidor no tiene una regla de firewall que permita Studio de datos de Azure para conectarse, se abrirá el formulario **crear nueva regla de firewall**. Complete el formulario para crear una nueva regla de firewall. Para obtener más información, consulte [reglas de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nueva regla de firewall](media/quickstart-sql-dw/firewall.png)  

4. Después de conectarse correctamente el servidor se abre en el *servidores* barra lateral.

## <a name="create-the-tutorial-data-warehouse"></a>Crear el almacén de datos del tutorial
1. Haga clic con el botón derecho en el servidor, en el Explorador de objetos y seleccione **nueva consulta.**

1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **ejecutar**:

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

El editor de consultas aún está conectado a la *maestro* base de datos, pero si desea crear una tabla en la *TutorialDB* base de datos. 

1. Cambiar el contexto de conexión a **TutorialDB**:

   ![Cambio de contexto](media/quickstart-sql-database/change-context.png)


1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **ejecutar**:

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
      CustomerId        INT     NOT NULL,
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>Insertar filas

1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **ejecutar**:

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
1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **ejecutar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Se muestran los resultados de la consulta:

   ![Seleccione los resultados](media/quickstart-sql-dw/select-results.png)


## <a name="clean-up-resources"></a>Limpiar recursos

Otros artículos de esta colección se basan en esta guía. Si tiene previsto seguir trabajando con los tutoriales posteriores, no limpie los recursos creados en esta guía de inicio rápido. Si no tiene previsto continuar, utilice los pasos siguientes para eliminar recursos creados en este inicio rápido en el portal de Azure.
Limpiar los recursos mediante la eliminación de los grupos de recursos que ya no necesita. Para obtener más información, consulte [limpiar recursos](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).


## <a name="next-steps"></a>Pasos siguientes

Ahora que ha conectado correctamente a una Azure SQL data warehouse y se ejecutó una consulta, pruebe el [tutorial del editor de código](tutorial-sql-editor.md).
