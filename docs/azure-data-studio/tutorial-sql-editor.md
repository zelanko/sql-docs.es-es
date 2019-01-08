---
title: 'Tutorial: Usar el editor de Transact-SQL para crear objetos de base de datos'
titleSuffix: Azure Data Studio
description: Este tutorial muestra las características clave en Azure Data Studio que simplifican el trabajo con T-SQL.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 04e6e366d1fd0a5d710296353d6326022f716199
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030459"
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>Tutorial: Utilice el editor de Transact-SQL para crear objetos de base de datos: [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Crear y ejecutar consultas, procedimientos almacenados, scripts, etc. son las tareas principales de los profesionales de TI de la base de datos. Este tutorial muestra las características clave en el editor de Transact-SQL para crear objetos de base de datos.

En este tutorial, obtendrá información sobre cómo usar [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Buscar objetos de base de datos
> * Editar datos de tabla 
> * Usar fragmentos de código para escribir rápidamente T-SQL
> * Ver detalles de objeto de base de datos mediante *ver la definición* y *ir a definición*


## <a name="prerequisites"></a>Requisitos previos

Este tutorial requiere SQL Server o Azure SQL Database *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar con SQL Server [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectarse y consultar con Azure SQL Database [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>Localizar un objeto de base de datos rápidamente y realizar una tarea común

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)] Proporciona un widget de búsqueda para encontrar rápidamente los objetos de base de datos. La lista de resultados proporciona un menú contextual para tareas comunes relacionadas con el objeto seleccionado, como *editar datos* para una tabla.

1. Abra la barra lateral de servidores (**CTRL+g**), expanda **bases de datos**y seleccione **TutorialDB**. 

1. Abra el *TutorialDB panel* con el botón secundario **TutorialDB** y seleccionando **administrar** en el menú contextual:

   ![menú contextual, administrar](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. En el panel, haga clic en **dbo. Los clientes** (en el widget de búsqueda) y seleccione **editar datos**.
   
   > [!TIP]
   > Bases de datos con muchos objetos, use el widget de búsqueda para localizar rápidamente la tabla, vista, etc., que está buscando.

   ![widget de búsqueda rápida](./media/tutorial-sql-editor/quick-search-widget.png)

1. Editar el **correo electrónico** columna en la primera fila, tipo *orlando0@adventure-works.com*y presione **ENTRAR** para guardar el cambio.

   ![Editar datos](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-stored-procedures"></a>Usar fragmentos de código de T-SQL para crear procedimientos almacenados

[!INCLUDE[name-sos](../includes/name-sos-short.md)] proporciona muchos fragmentos de código integrados de T-SQL para crear rápidamente las instrucciones.


1. Abra un nuevo editor de consultas presionando **CTRL+n**.

2. Tipo **sql** en el editor, la flecha hacia abajo para **sqlCreateStoredProcedure**y presione la *ficha* clave (o *ENTRAR*) para cargar el crear almacenado fragmento de código de procedimiento.

   ![lista de fragmentos](./media/tutorial-sql-editor/snippet-list.png)

3. El fragmento de código de procedimiento almacenado de crear tiene dos campos que se configure para su edición rápida, *StoredProcedureName* y *SchemaName*. Seleccione *StoredProcedureName*, con el botón secundario y seleccione **cambiar todas las apariciones**. Ahora escriba *getCustomer* y todos los *StoredProcedureName* cambian las entradas a *getCustomer*.

   ![Fragmento de código](./media/tutorial-sql-editor/snippet.png)

5. Cambie todas las apariciones de *SchemaName* a *dbo*. 
6. El fragmento de código contiene los parámetros de marcador de posición y el texto de cuerpo que se debe actualizar. El *EXECUTE* instrucción también contiene el texto de marcador de posición, puesto que desconoce el número de parámetros del procedimiento tendrá. Por lo tanto para el fragmento de código de actualización de este tutorial es similar al código siguiente:

    ```sql
    -- Create a new stored procedure called 'getCustomer' in schema 'dbo'
    -- Drop the stored procedure if it already exists
    IF EXISTS (
    SELECT *
    FROM INFORMATION_SCHEMA.ROUTINES
    WHERE SPECIFIC_SCHEMA = N'dbo'
    AND SPECIFIC_NAME = N'getCustomer'
    )
    DROP PROCEDURE dbo.getCustomer
    GO
    -- Create the stored procedure in the specified schema
    CREATE PROCEDURE dbo.getCustomer
    @ID int
    -- add more stored procedure parameters here
    AS
    -- body of the stored procedure
    SELECT  c.CustomerId, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerId = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. Para crear el procedimiento almacenado y asignarle una serie de pruebas, presione **F5**.

Ahora se crea el procedimiento almacenado y el **resultados** panel muestra el cliente devuelto en JSON. Para ver con formato JSON, haga clic en el registro devuelto. 


## <a name="use-peek-definition"></a>Usar la definición de Peek 

[!INCLUDE[name-sos](../includes/name-sos-short.md)] proporciona la capacidad para ver una definición de objetos con la característica de la definición de peek. Esta sección crea un segundo procedimiento almacenado y usa la definición de peek para ver cuáles son las columnas de una tabla para crear rápidamente el cuerpo del procedimiento almacenado.

1. Abra un nuevo editor presionando **CTRL+n**. 

2. Tipo *sql* en el editor, la flecha hacia abajo para *sqlCreateStoredProcedure*y presione la *ficha* clave (o *ENTRAR*) para cargar el crear almacenado fragmento de código de procedimiento.
3. Escriba en *setCustomer* para *StoredProcedureName* y *dbo* para *SchemaName*

3. Reemplace el @param marcadores de posición con la siguiente definición de parámetro:

   ```sql
   @json_val nvarchar(max)
   ```

4. Reemplace el cuerpo del procedimiento almacenado con el código siguiente:
   ```sql
   INSERT INTO dbo.Customers
   ```

5. En el *insertar* línea contextual recién agregada, **dbo. Los clientes** y seleccione **ver la definición**.

   ![definición de Peek](./media/tutorial-sql-editor/peek-definition.png)

6. La definición de tabla aparece para que pueda ver rápidamente qué columnas se encuentran en la tabla. Consulte la lista de columnas para completar fácilmente las instrucciones para el procedimiento almacenado. Terminar de crear la instrucción INSERT agregado anteriormente para completar el cuerpo del procedimiento almacenado y cerrar la ventana de definición de peek:

   ```sql
   INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
    )
   ```
7. Eliminar (o marque como comentario) el *EXECUTE* comando en la parte inferior de la consulta.
8. Toda la instrucción debe ser similar al código siguiente:

   ```sql
   -- Create a new stored procedure called 'setCustomer' in schema 'dbo'
   -- Drop the stored procedure if it already exists
   IF EXISTS (
   SELECT *
       FROM INFORMATION_SCHEMA.ROUTINES
       WHERE SPECIFIC_SCHEMA = N'dbo'
       AND SPECIFIC_NAME = N'setCustomer'
   )
   DROP PROCEDURE dbo.setCustomer
   GO
   -- Create the stored procedure in the specified schema
   CREATE PROCEDURE dbo.setCustomer
       @json_val nvarchar(max) 
   AS
       -- body of the stored procedure
       INSERT INTO dbo.Customers (CustomerId, Name, Location, Email)
       SELECT CustomerId, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerId int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. Para crear el *setCustomer* procedimiento almacenado, presione **F5**.

## <a name="use-save-query-results-as-json-to-test-the-setcustomer-stored-procedure"></a>Use Guardar resultados de la consulta como JSON para probar el procedimiento almacenado de setCustomer

El *setCustomer* procedimiento almacenado creado en la sección anterior requiere JSON datos se pasan a la *@json_val* parámetro. En esta sección se muestra cómo obtener un poco de JSON para pasar el parámetro para que pueda probar el procedimiento almacenado con el formato correcto.

1. En el **servidores** sidebar, haga clic en el *dbo. Los clientes* de tabla y haga clic en **seleccionar 1000 filas superiores**.

2. Seleccione la primera fila en la vista de resultados, asegúrese de que toda la fila está seleccionada (haga clic en el número 1 en la columna más a la izquierda) y seleccione **Guardar como JSON**.  
3. Cambiar la carpeta a una ubicación que sea fácil de recordar para que pueda eliminar el archivo más adelante (para escritorio de ejemplo) y haga clic en **guardar**. El archivo se abre en formato el JSON.

   ![Guardar como JSON](./media/tutorial-sql-editor/save-as-json.png)

4. Seleccione los datos JSON en el editor y cópielo.
5. Abra un nuevo editor presionando **CTRL+n**.
6. Los pasos anteriores muestran cómo puede obtener fácilmente los datos con el formato correcto para completar la llamada a la *setCustomer* procedimiento. Puede ver el código siguiente usa el mismo formato JSON con nuevos detalles del cliente, por lo que podemos probar la *setCustomer* procedimiento. La instrucción incluye la sintaxis para declarar el parámetro y ejecutar la operación get nueva y establecer procedimientos. Puede pegar los datos copiados desde la sección anterior y editarlo, por lo que es el mismo que el ejemplo siguiente o simplemente pegue la siguiente instrucción en el editor de consultas.

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerId": 5,
           "Name": "Lucy",
           "Location": "Canada",
           "Email": "lucy0@adventure-works.com"
       }
   ]'

   EXECUTE dbo.setCustomer @json_val = @json
   GO

   EXECUTE dbo.getCustomer @ID = 5
   ```

7. Ejecute el script presionando **F5**. El script inserta a un nuevo cliente y devuelve la nueva información del cliente en formato JSON. Haga clic en el resultado para abrir una vista con formato.

   ![resultado de la prueba](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>Pasos siguientes
En este tutorial ha aprendido a:
> [!div class="checklist"]
> * Objetos de esquema de búsqueda rápida
> * Editar datos de tabla 
> * Escribir el script de T-SQL con fragmentos de código
> * Obtenga información sobre los detalles del objeto de base de datos mediante la definición de Peek e ir a definición


Para obtener información sobre cómo habilitar el **cinco consultas más lentas** widget, completar el tutorial siguiente:

> [!div class="nextstepaction"]
> [Habilitar el widget de insight de ejemplo de consultas lentas](tutorial-qds-sql-server.md)
