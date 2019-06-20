---
title: 'Inicio rápido: Conectarse a PostgreSQL y consultas'
titleSuffix: Azure Data Studio
description: En este tutorial rápido se muestra cómo usar Azure Data Studio para conectarse a PostgreSQL y ejecutar una consulta
ms.custom: seodec18
ms.date: 03/19/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: quickstart
author: rachel-msft
ms.author: raagyema
manager: jroth
ms.openlocfilehash: be8683ae563e4e0676f53203cb40386cf8aa4840
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778333"
---
# <a name="quickstart-connect-and-query-postgresql-using-includename-sosincludesname-sos-shortmd"></a>Inicio rápido: Conectarse y consultar con PostgreSQL [!INCLUDE[name-sos](../includes/name-sos-short.md)]
En este tutorial rápido se muestra cómo usar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para conectarse a Postgres y, a continuación, usar instrucciones SQL para crear la base de datos *tutorialdb* y realiza consultas.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial rápido, necesitará [!INCLUDE[name-sos](../includes/name-sos-short.md)], la extensión de PostgreSQL para [! INCLUIR[nombre sos](../includes/name-sos-short.md)y el acceso a un servidor de PostgreSQL.

- [Instalar [!INCLUDE[name-sos](../includes/name-sos-short.md)] ](download.md).
- [Instalar la extensión de PostgreSQL para Azure Data Studio](postgres-extension.md).
- [Instalación de PostgreSQL](https://www.postgresql.org/download/). (Como alternativa, puede crear una base de datos de Postgres en la nube mediante [az postgres de](https://docs.microsoft.com/azure/postgresql/quickstart-create-server-up-azure-cli)). 

## <a name="connect-to-postgresql"></a>Conectarse a PostgreSQL

1. Iniciar **[!INCLUDE[name-sos](../includes/name-sos-short.md)]** .

2. La primera vez que inicie [!INCLUDE[name-sos](../includes/name-sos-short.md)] el **conexión** abre el cuadro de diálogo. Si el **conexión** no abre el cuadro de diálogo, haga clic en el **nueva conexión** icono en el **servidores** página:

   ![Nuevo icono de conexión](media/quickstart-postgresql/new-connection-icon.png)

3. En el formulario que aparece, vaya a **tipo de conexión** y seleccione **PostgreSQL** en la lista desplegable.


4. Rellene los campos restantes con el nombre del servidor, el nombre de usuario y la contraseña para el servidor de PostgreSQL. 

   ![Nueva pantalla de conexión](media/quickstart-postgresql/new-connection-screen.png)  

   | Parámetro       | Valor de ejemplo | Descripción |
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Nombre del servidor** | localhost | Nombre completo del servidor |
   | **Nombre de usuario.** | postgres | El nombre de usuario que desea iniciar sesión. |
   | **Contraseña (inicio de sesión de SQL)** | *password* | La contraseña de la cuenta que va a iniciar sesión. |
   | **Contraseña** | *Comprobación* | Active esta casilla si no desea escribir la contraseña cada vez que se conecte. |
   | **Nombre de la base de datos** | \<Default\> | Rellene esto si desea que la conexión para especificar una base de datos. |
   | **Grupo del servidor** | \<Default\> | Esta opción le permite asignar esta conexión a un grupo de servidores específicos que cree. | 
   | **Nombre (opcional)** | *Deje en blanco* | Esta opción permite especificar un nombre descriptivo para el servidor. | 

5. Seleccione **Conectar**. 

Después de conectarse correctamente, el servidor se abre en el **servidores** barra lateral.


## <a name="create-a-database"></a>Crear una base de datos

Los pasos siguientes crean una base de datos denominada **tutorialdb**:

1. Haga doble clic en el servidor de PostgreSQL en el **servidores** barra lateral y seleccione **nueva consulta**.

2. Pegue esta instrucción SQL en el editor de consultas que se abre.

   ```sql
   CREATE DATABASE tutorialdb;
   ```

3. En la barra de herramientas seleccione **ejecutar** para ejecutar la consulta. Las notificaciones aparecen en la **mensajes** panel para mostrar el progreso de la consulta.

>[!TIP]
> Puede usar **F5** en el teclado para ejecutar la instrucción en lugar de usar **ejecutar**.

Una vez finalizada la consulta, haga clic en **bases de datos** y seleccione **actualizar** para ver **tutorialdb** en la lista bajo el **bases de datos** nodo .


## <a name="create-a-table"></a>Creación de una tabla

 Los pasos siguientes crean una tabla en la **tutorialdb**:

1. Cambiar el contexto de conexión a **tutorialdb** mediante la lista desplegable en el editor de consultas. 

   ![Cambio de contexto](media/quickstart-postgresql/change-context.png)

2. Pegue la siguiente instrucción SQL en el editor de consultas y haga clic en **ejecutar**. 

   > [!NOTE]
   > Puede anexar este o sobrescribir la consulta existente en el editor. Al hacer clic en **ejecutar** ejecuta solo la consulta que está resaltada. Si nada está resaltado, haga clic en **ejecutar** ejecuta todas las consultas en el editor.

   ```sql
   -- Drop the table if it already exists
   DROP TABLE IF EXISTS customers;
   -- Create a new table called 'customers'
   CREATE TABLE customers(
       customer_id SERIAL PRIMARY KEY,
       name VARCHAR (50) NOT NULL,
       location VARCHAR (50) NOT NULL,
       email VARCHAR (50) NOT NULL
   );
   ```

## <a name="insert-rows"></a>Insertar filas

Pegue el siguiente fragmento de código en la ventana de consulta y haga clic en **ejecutar**:

   ```sql
   -- Insert rows into table 'customers'
   INSERT INTO customers
       (customer_id, name, location, email)
    VALUES
      ( 1, 'Orlando', 'Australia', ''),
      ( 2, 'Keith', 'India', 'keith0@adventure-works.com'),
      ( 3, 'Donna', 'Germany', 'donna0@adventure-works.com'),
      ( 4, 'Janet', 'United States','janet1@adventure-works.com');
   ```

## <a name="query-the-data"></a>Consultar los datos

1. Pegue el siguiente fragmento de código en el editor de consultas y haga clic en **ejecutar**:
   
   ```sql
   -- Select rows from table 'customers'
   SELECT * FROM customers; 
   ```

2. Se muestran los resultados de la consulta:

   ![Ver los resultados](media/quickstart-postgresql/view-results.png)

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre la [escenarios disponibles para Postgres en Azure Data Studio](postgres-extension.md). 