---
title: 'Inicio rápido: Conectarse y consultar Azure SQL database mediante Azure Data Studio | Microsoft Docs'
description: En este tutorial rápido se muestra cómo usar Azure Data Studio para conectarse a una base de datos SQL y ejecutar una consulta
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: quickstart
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 00ed5c02e423e5d51fd6f0ee3aabfc73a752e403
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "48039027"
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>Inicio rápido: Usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse y consultar la base de datos SQL de Azure

En este tutorial rápido se muestra cómo usar *[!INCLUDE[name-sos](../includes/name-sos-short.md)]* para conectarse a una base de datos SQL de Azure y, a continuación, usar instrucciones Transact-SQL (T-SQL) para crear el *TutorialDB* utilizados en [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriales.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial rápido, necesitará [!INCLUDE[name-sos](../includes/name-sos-short.md)]y un servidor SQL Azure.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Si aún no tiene un servidor SQL Azure, complete uno de los siguientes inicios rápidos de Azure SQL Database (recuerde el nombre del servidor y las credenciales de inicio de sesión.):

- [Crear base de datos: Portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Creación de base de datos: CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Creación de base de datos: PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Conectarse al servidor de base de datos de SQL Azure

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para establecer una conexión al servidor de Azure SQL Database.

1. La primera vez que ejecute [!INCLUDE[name-sos](../includes/name-sos-short.md)] el **conexión** debe abrir la página. Si no ve el **conexión** página, haga clic en **Agregar conexión**, o el **nueva conexión** icono en el **servidores** sidebar:
   
   ![Nuevo icono de conexión](media/quickstart-sql-database/new-connection-icon.png)

2. Este artículo se usa *inicio de sesión SQL*, pero *Windows autenticación* también es compatible. Rellene los campos como se indica a continuación con el nombre del servidor, el nombre de usuario y la contraseña para *su* servidor SQL de Azure:

   | Configuración       | Valor sugerido | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Nombre completo del servidor | El nombre debe ser algo parecido a esto: **nombreDeServidor.baseDeDatos.Windows.NET** |
   | **Autenticación** | Inicio de sesión de SQL| En este tutorial, se utiliza la autenticación de SQL. |
   | **Nombre de usuario.** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña (inicio de sesión de SQL)** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |
   | **¿Desea guardar la contraseña?** | Sí o no | Seleccione Sí si no desea escribir la contraseña cada vez. |
   | **Nombre de la base de datos** | *Deje en blanco* | El nombre de la base de datos que desea conectarse. |
   | **Grupo de servidores** | Seleccione <Default> | Si ha creado un grupo de servidores, puede establecer para un grupo de servidores específicos. | 

   ![Nuevo icono de conexión](media/quickstart-sql-database/new-connection-screen.png)  

3. Si el servidor no tiene una regla de firewall que permita Studio de datos de Azure para conectarse, el **crear nueva regla de firewall** se abrirá el formulario. Complete el formulario para crear una nueva regla de firewall. Para obtener más información, consulte [reglas de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nueva regla de firewall](media/quickstart-sql-database/firewall.png)  

4. Después de conectarse correctamente el servidor se abre en el *servidores* barra lateral.

## <a name="create-the-tutorial-database"></a>Crear la base de datos tutorial

Las siguientes secciones se creación el *TutorialDB* base de datos que se utiliza en varios [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriales.

1. Haga clic con el botón derecho en el servidor SQL de Azure en la barra lateral de los servidores y seleccione **nueva consulta.**

1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **ejecutar**:

   ```sql
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
      CustomerId        INT    NOT NULL   PRIMARY KEY, -- primary key column
      Name      [NVARCHAR](50)  NOT NULL,
      Location  [NVARCHAR](50)  NOT NULL,
      Email     [NVARCHAR](50)  NOT NULL
   );
   GO
   ```


## <a name="insert-rows"></a>Insertar filas

- Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **ejecutar**:

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


## <a name="view-the-result"></a>Ver el resultado
1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **ejecutar**:

   ```sql
   -- Select rows from table 'Customers'
   SELECT * FROM dbo.Customers;
   ```

1. Se muestran los resultados de la consulta:

   ![Seleccione los resultados](media/quickstart-sql-database/select-results.png)


## <a name="clean-up-resources"></a>Limpiar recursos

Otros artículos de esta colección se basan en esta guía. Si tiene previsto seguir trabajando con los tutoriales posteriores, no limpie los recursos creados en esta guía de inicio rápido. Si no tiene previsto continuar, utilice los pasos siguientes para eliminar recursos creados en este inicio rápido en el portal de Azure.
Limpiar los recursos mediante la eliminación de los grupos de recursos que ya no necesita. Para obtener más información, consulte [limpiar recursos](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha conectado correctamente a una base de datos SQL de Azure y ejecutar una consulta, pruebe el [tutorial del editor de código](tutorial-sql-editor.md).
