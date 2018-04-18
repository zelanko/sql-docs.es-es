---
title: "Inicio rápido: Conectarse y consultar un almacén de datos de SQL Azure con SQL Operations Studio (versión preliminar) | Documentos de Microsoft"
description: "Este tutorial rápido muestra cómo utilizar SQL Operations Studio (versión preliminar) para conectarse a una base de datos SQL y ejecutar una consulta"
ms.custom: tools|sos
ms.date: 03/08/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d4ed7d25abb2780c719c5b8201ecae54e8e86bf
ms.sourcegitcommit: 6c06267f3eeeb3f0d6fc4c57e1387621720ca8bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2018
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-data-in-azure-sql-data-warehouse"></a>Inicio rápido: Usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse y consultar los datos en el almacén de datos de SQL Azure

Este tutorial rápido muestra cómo usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectar al almacén de datos de SQL Azure y, a continuación, utilizar instrucciones Transact-SQL para crear, insertar y seleccionar los datos. 

## <a name="prerequisites"></a>Requisitos previos
Para completar este tutorial rápido, necesita [!INCLUDE[name-sos](../includes/name-sos-short.md)]y un almacén de datos de SQL Azure.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Si aún no tiene un almacén de datos SQL, consulte [crear un almacén de datos de SQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision).

Recuerde el nombre del servidor y las credenciales de inicio de sesión.


## <a name="connect-to-your-data-warehouse"></a>Conectar con el almacenamiento de datos

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para establecer una conexión con el servidor de almacenamiento de datos de SQL Azure.

1. La primera vez que ejecute [!INCLUDE[name-sos](../includes/name-sos-short.md)] el **conexión** debe abrir la página. Si no ve el **conexión** página, haga clic en **Agregar conexión**, o la **nueva conexión** icono en el **servidores** sidebar:
   
   ![Nuevo icono de conexión](media/quickstart-sql-dw/new-connection-icon.png)

2. Este artículo usa *inicio de sesión SQL*, pero *autenticación de Windows* también se admite. Rellene los campos como se indica a continuación mediante el nombre del servidor, el nombre de usuario y la contraseña para *su* servidor SQL de Azure:

   | Configuración       | Valor sugerido | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Nombre completo del servidor | El nombre debe ser algo parecido a esto: **sqldwsample.database.windows.net** |
   | **Autenticación** | Inicio de sesión de SQL| Autenticación de SQL se utiliza en este tutorial. |
   | **Nombre de usuario.** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña (inicio de sesión de SQL)** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |
   | **¿Desea guardar la contraseña?** | Sí o no | Seleccione Sí si no desea escribir la contraseña cada vez. |
   | **Nombre de la base de datos** | *Deje en blanco* | Nombre de la base de datos a la que se va a conectar. |
   | **Grupo de servidores** | Seleccione <Default> | Si ha creado un grupo de servidores, puede establecer en un grupo de servidores específico. | 

   ![Nuevo icono de conexión](media/quickstart-sql-dw/new-connection-screen.png) 

3. Si el servidor no tiene una regla de firewall que permita las SQL Operations Studio para conectarse, el **crear nueva regla de firewall** se abrirá el formulario. Complete el formulario para crear una nueva regla de firewall. Para obtener más información, consulte [las reglas de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nueva regla de firewall](media/quickstart-sql-dw/firewall.png)  

4. Después de conectarse correctamente el servidor se abre en el *servidores* sidebar.

## <a name="create-the-tutorial-data-warehouse"></a>Crear el almacén de datos del tutorial
1. Haga clic con el botón secundario en el servidor, en el Explorador de objetos y seleccione **nueva consulta.**

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

El editor de consultas aún está conectado a la *maestro* base de datos, pero desea crear una tabla en la *TutorialDB* base de datos. 

1. Cambiar el contexto de conexión a **TutorialDB**:

   ![Cambio de contexto](media/quickstart-sql-database/change-context.png)


1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **ejecutar**:

   > [!NOTE]
   > Puede anexar a o sobrescriba la consulta anterior en el editor. Tenga en cuenta que al hacer clic **ejecutar** ejecuta solo la consulta seleccionada. Si se selecciona nada, haga clic en **ejecutar** ejecuta todas las consultas en el editor.

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


## <a name="clean-up-resources"></a>Limpiar los recursos

Otros artículos en esta colección se basan en este tutorial rápido. Si va a continuar en trabajar con los tutoriales posteriores, no liberar los recursos creados en este tutorial rápido. Si no va a continuar, utilice los pasos siguientes para eliminar los recursos creados por este inicio rápido en el portal de Azure.
Limpiar los recursos mediante la eliminación de los grupos de recursos que ya no necesita. Para obtener más información, consulte [limpiar los recursos](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-portal#clean-up-resources).


## <a name="next-steps"></a>Pasos siguientes

Ahora que ha conectado correctamente a un almacenamiento de datos de SQL Azure y ejecutara una consulta, pruebe el [tutorial del editor de código](tutorial-sql-editor.md).
