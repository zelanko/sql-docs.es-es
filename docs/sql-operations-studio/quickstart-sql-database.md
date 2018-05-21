---
title: 'Inicio rápido: Conectarse y consultar una base de datos de SQL Azure con SQL Operations Studio (versión preliminar) | Documentos de Microsoft'
description: Este tutorial rápido muestra cómo utilizar SQL Operations Studio (versión preliminar) para conectarse a una base de datos SQL y ejecutar una consulta
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
ms.openlocfilehash: c72e6d5b8e3e2770300e6b890b076bf77617849b
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2018
---
# <a name="quickstart-use-includename-sosincludesname-sos-shortmd-to-connect-and-query-azure-sql-database"></a>Inicio rápido: Usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse y consultar la base de datos SQL de Azure

Este tutorial rápido muestra cómo usar *[!INCLUDE[name-sos](../includes/name-sos-short.md)]* para conectarse a una base de datos de SQL Azure y, a continuación, utilice las instrucciones de Transact-SQL (T-SQL) para crear el *TutorialDB* utilizados en [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriales.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial rápido, necesita [!INCLUDE[name-sos](../includes/name-sos-short.md)]y un servidor SQL Azure.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).

Si ya no tiene un servidor de SQL Azure, realice uno de los siguientes tutoriales de base de datos de SQL Azure (recuerde el nombre del servidor y las credenciales de inicio de sesión!):

- [Crear base de datos: Portal](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal)
- [Crear base de datos: CLI](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-cli)
- [Crear base de datos: PowerShell](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-powershell)


## <a name="connect-to-your-azure-sql-database-server"></a>Conectarse a su servidor de base de datos de SQL Azure

Use [!INCLUDE[name-sos](../includes/name-sos-short.md)] para establecer una conexión con el servidor de base de datos de SQL Azure.

1. La primera vez que ejecute [!INCLUDE[name-sos](../includes/name-sos-short.md)] el **conexión** debe abrir la página. Si no ve el **conexión** página, haga clic en **Agregar conexión**, o la **nueva conexión** icono en el **servidores** sidebar:
   
   ![Nuevo icono de conexión](media/quickstart-sql-database/new-connection-icon.png)

2. Este artículo usa *inicio de sesión SQL*, pero *autenticación de Windows* también se admite. Rellene los campos como se indica a continuación mediante el nombre del servidor, el nombre de usuario y la contraseña para *su* servidor SQL de Azure:

   | Configuración       | Valor sugerido | Description |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | Nombre completo del servidor | El nombre debe ser algo parecido a esto: **nombreDeServidor.baseDeDatos.Windows.NET** |
   | **Autenticación** | Inicio de sesión de SQL| Autenticación de SQL se utiliza en este tutorial. |
   | **Nombre de usuario.** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña (inicio de sesión de SQL)** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |
   | **¿Desea guardar la contraseña?** | Sí o no | Seleccione Sí si no desea escribir la contraseña cada vez. |
   | **Nombre de la base de datos** | *Deje en blanco* | El nombre de la base de datos que desea conectarse. |
   | **Grupo de servidores** | Seleccione <Default> | Si ha creado un grupo de servidores, puede establecer en un grupo de servidores específico. | 

   ![Nuevo icono de conexión](media/quickstart-sql-database/new-connection-screen.png)  

3. Si el servidor no tiene una regla de firewall que permita las operaciones de SQL Studio para conectarse, el **crear nueva regla de firewall** se abrirá el formulario. Complete el formulario para crear una nueva regla de firewall. Para obtener más información, consulte [las reglas de Firewall](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure).

   ![Nueva regla de firewall](media/quickstart-sql-database/firewall.png)  

4. Después de conectarse correctamente el servidor se abre en el *servidores* sidebar.

## <a name="create-the-tutorial-database"></a>Crear la base de datos tutorial

Crear las siguientes secciones del *TutorialDB* base de datos que se utiliza en varios [!INCLUDE[name-sos](../includes/name-sos-short.md)] tutoriales.

1. Haga clic con el botón secundario en el servidor de SQL Azure en la barra lateral de servidores y seleccione **nueva consulta.**

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


## <a name="clean-up-resources"></a>Limpiar los recursos

Otros artículos en esta colección se basan en este tutorial rápido. Si va a continuar en trabajar con los tutoriales posteriores, no liberar los recursos creados en este tutorial rápido. Si no va a continuar, utilice los pasos siguientes para eliminar los recursos creados por este inicio rápido en el portal de Azure.
Limpiar los recursos mediante la eliminación de los grupos de recursos que ya no necesita. Para obtener más información, consulte [limpiar los recursos](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-get-started-portal#clean-up-resources).

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha conectado correctamente a una base de datos de SQL Azure y ejecutara una consulta, pruebe el [tutorial del editor de código](tutorial-sql-editor.md).
