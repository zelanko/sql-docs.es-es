---
title: "Tutorial: Usar el editor de Transact-SQL de las operaciones de SQL Studio (versión preliminar) para crear objetos de base de datos | Documentos de Microsoft"
description: "Este tutorial muestra las características claves de Studio de operaciones de SQL (vista previa) que simplifican el uso de T-SQL."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2754a998963be5a25d00aa58dcb9b4105bb8f37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-use-the-transact-sql-editor-to-create-database-objects---includename-sosincludesname-sos-shortmd"></a>Tutorial: Usar el editor de Transact-SQL para crear objetos de base de datos-[!INCLUDE[name-sos](../includes/name-sos-short.md)]

Crear y ejecutar consultas, procedimientos almacenados, scripts, etc. son las tareas principales de profesionales de la base de datos. Este tutorial muestra las características clave en el editor de T-SQL para crear objetos de base de datos.

En este tutorial, aprenderá a utilizar [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] para:
> [!div class="checklist"]
> * Objetos de base de datos de búsqueda
> * Editar datos de tabla 
> * Usar fragmentos de código para escribir rápidamente código T-SQL
> * Ver detalles de objeto de base de datos mediante *ver la definición* y *ir a definición*


## <a name="prerequisites"></a>Prerequisites

Este tutorial requiere SQL Server o base de datos de SQL Azure *TutorialDB*. Para crear el *TutorialDB* base de datos, complete uno de los siguientes tutoriales:

- [Conectarse y consultar mediante SQL Server[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [Conectarse y consultar mediante la base de datos de SQL Azure[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="quickly-locate-a-database-object-and-perform-a-common-task"></a>Buscar un objeto de base de datos rápidamente y realizar una tarea común

[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]Proporciona un widget de búsqueda para encontrar rápidamente los objetos de base de datos. La lista de resultados proporciona un menú contextual para realizar tareas habituales relacionadas con el objeto seleccionado, como *editar datos* para una tabla.

1. Abrir la barra lateral de servidores (**Ctrl + G**), expanda **bases de datos**y seleccione **TutorialDB**. 

1. Abra la *TutorialDB panel* seleccionando **administrar** en el menú contextual.

   ![menú contextual: administrar](./media/tutorial-sql-editor/insight-open-dashboard.png)

1. Busque la *clientes* tabla escribiendo *Perso* en el widget de búsqueda.
1. Haga clic en **dbo. Los clientes** y seleccione **editar datos**.

   ![widget de búsqueda rápida](./media/tutorial-sql-editor/quick-search-widget.png)

1. Editar la **correo electrónico** columna en la primera fila, tipo  *orlando0@adventure-works.com* y presione **ENTRAR** para guardar el cambio.

   ![Editar datos](./media/tutorial-sql-editor/edit-data.png)

## <a name="use-t-sql-snippets-to-create-a-stored-procedure"></a>Usar fragmentos de código de T-SQL para crear un procedimiento almacenado

### <a name="use-snippets-in-includename-sos-shortincludesname-sos-shortmd"></a>Use fragmentos de código en[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]

1. Abra un nuevo editor de consultas presionando **CTRL+n**.

2. Tipo de **sql** en el editor, la flecha hacia abajo hasta **sqlCreateStoredProcedure**y presione la *ficha* clave para cargar el nuevo fragmento de código de procedimiento almacenado.

   ![lista de fragmentos](./media/tutorial-sql-editor/snippet-list.png)

3. Tipo de *getCustomer* y todos los *StoredProcedureName* cambian las entradas a *getCustomer*. 

   ![Fragmento de código](./media/tutorial-sql-editor/snippet.png)

4. Reemplace el resto del procedimiento almacenado con el código T-SQL siguiente:

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
    SELECT  c.CustomerID, 
    c.Name, 
    c.Location, 
    c.Email
    FROM dbo.Customers c
    WHERE c.CustomerID = @ID
    FOR JSON PATH

    GO
    -- example to execute the stored procedure we just created
    EXECUTE dbo.getCustomer 1
    GO
    ```
    
5. Para crear el procedimiento almacenado y asignarle una serie de pruebas, presione **F5**.

## <a name="use-peek-definition-and-go-to-definition"></a>Definición de Peek de uso e ir a definición 

1. Abra un nuevo editor presionando **CTRL+n**. 

2. Escriba y seleccione **sqlCreateStoredProcedure** desde la lista de sugerencias de fragmento de código. Escriba en **setCustomer** para **StoredProcedureName** y **dbo** para **SchemaName**

3. Reemplace el @param líneas con la definición del parámetro siguiente:

   ```sql
       @json_val nvarchar(max)
   ```

4. Reemplace el cuerpo del procedimiento almacenado con lo siguiente:
   ```sql
   -- body of the stored procedure
   INSERT INTO dbo.Customers
   ```

5. Haga clic en **dbo. Los clientes** y seleccione **ver la definición**.

   ![definición de Peek](./media/tutorial-sql-editor/peek-definition.png)

6. Use la definición de tabla para completar la instrucción de inserción siguiente:

   ```sql
   INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
   ```
7. La instrucción final debe ser:

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
       INSERT INTO dbo.Customers (CustomerID, Name, Location, Email)
       SELECT CustomerID, Name, Location, Email
       FROM OPENJSON (@json_val)
       WITH(   CustomerID int, 
               Name nvarchar(50), 
               Location nvarchar(50), 
               Email nvarchar(50)
       )
   GO
   ```

8. Para ejecutar la secuencia de comandos, presione **F5**.

## <a name="use-save-query-results-as-json-to-test-our-stored-procedure"></a>Use Guardar resultados de la consulta como JSON para probar el procedimiento almacenado

1. **Seleccionar las primeras 1000 filas** desde el *dbo. Los clientes* tabla.

2. Seleccione la primera fila en la vista de resultados y haga clic en **Guardar como JSON**.  
3. Haga clic en **guardar**, y se abre la fila resaltada en formato JSON.

   ![Guardar como JSON](./media/tutorial-sql-editor/save-as-json.png)

4. Seleccione los datos JSON y cópiela.

5. Abrir una consulta nueva para *TutorialDB* y complete el siguiente script de prueba con los datos JSON como una plantilla en el paso anterior. Modifica los valores de *CustomerID*, *nombre*, *ubicación*, y *correo electrónico*.

   ```sql
   -- example to execute the stored procedure we just created
   declare @json nvarchar(max) =
   N'[
       {
           "CustomerID": 5,
           "Name": "Lucy",
           "Location": "Canada",
           "Email": "lucy0@adventure-works.com"
       }
   ]'

   EXECUTE dbo.setCustomer @json_val = @json
   GO

   EXECUTE dbo.getCustomer @ID = 5
   ```

7. Ejecute la secuencia de comandos presionando **F5**. La secuencia de comandos inserta a un nuevo cliente y devuelve la nueva información del cliente en formato JSON. Haga clic en el resultado para abrir una vista con formato.

   ![Resultado de pruebas](./media/tutorial-sql-editor/test-result.png)

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo:
> [!div class="checklist"]
> * Objetos de esquema de búsqueda rápida
> * Editar datos de tabla 
> * Escribir el script de T-SQL con fragmentos de código
> * Obtenga información acerca de los detalles de objeto de base de datos mediante la definición de Peek e ir a definición


Para obtener información sobre cómo habilitar la **cinco consultas más lentas** una visión general de ejemplo, siga el tutorial siguiente:

> [!div class="nextstepaction"]
> [Habilitar el widget de una visión general de ejemplo de consultas de ejecución lenta](tutorial-qds-sql-server.md)
