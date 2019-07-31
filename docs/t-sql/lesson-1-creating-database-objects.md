---
title: 'Tutorial de T-SQL: Creación y consulta de objetos de base de datos | Microsoft Docs'
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
ms.assetid: 9fb8656b-0e4e-4ada-b404-4db4d3eea995
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aa027f58bd673539dd09f118ea1b9433c42c7990
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000279"
---
# <a name="lesson-1-create-and-query-database-objects"></a>Lección 1: Creación y consulta de objetos de base de datos
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

En esta lección se muestra cómo crear una base de datos, crear una tabla en la base de datos y, a continuación, tener acceso a los datos de la tabla y cambiarlos. Puesto que esta lección es una introducción al uso de [!INCLUDE[tsql](../includes/tsql-md.md)], no usa ni describe las múltiples opciones disponibles para estas instrucciones.  
  
[!INCLUDE[tsql](../includes/tsql-md.md)] se pueden escribir y enviar a [!INCLUDE[ssDE](../includes/ssde-md.md)] de las siguientes maneras:  
  
-   Mediante el uso de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. En este tutorial se supone que se usa [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], pero también puede usarse [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Express, disponible como descarga gratuita en el [Centro de descargas de Microsoft](https://go.microsoft.com/fwlink/?linkid=67359).  
  
-   Mediante el uso de la [utilidad sqlcmd](../tools/sqlcmd-utility.md).  
  
-   Mediante la conexión desde una aplicación que cree.  
  
El código se ejecuta en [!INCLUDE[ssDE](../includes/ssde-md.md)] de la misma forma y con los mismos permisos, independientemente de cómo envíe las instrucciones de código.  
  
Para ejecutar instrucciones de [!INCLUDE[tsql](../includes/tsql-md.md)] en [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], abra [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] y conéctese a una instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)].  

## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, así como acceso a una instancia de SQL Server. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Si no tiene acceso a ninguna instancia de SQL Server, seleccione su plataforma en uno de los vínculos siguientes. Si elige la autenticación de SQL, use sus credenciales de inicio de sesión de SQL Server.
- **Windows**: [Descargar SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [Descargar SQL Server 2017 en Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).

## <a name="create-a-database"></a>Crear una base de datos
Como muchas instrucciones de [!INCLUDE[tsql](../includes/tsql-md.md)] , la instrucción CREATE DATABASE tiene un parámetro requerido: el nombre de la base de datos. CREATE DATABASE también tiene muchos parámetros opcionales, como la ubicación de disco donde se desean colocar los archivos de la base de datos. Si se ejecuta CREATE DATABASE sin los parámetros opcionales, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa los valores predeterminados para muchos de estos parámetros. Este tutorial usa algunos de los parámetros de sintaxis opcionales.   

1.  En una ventana del Editor de consultas, escriba el código siguiente, pero no lo ejecute:  
  
    ```sql  
    CREATE DATABASE TestData  
    GO  
    ```  
  
2.  Use el puntero para seleccionar las palabras `CREATE DATABASE`y, a continuación, presione **F1**. Debe abrirse el tema CREATE DATABASE de los Libros en pantalla de SQL Server. Puede usar esta técnica para encontrar la sintaxis completa de CREATE DATABASE y de otras instrucciones que se usan en este tutorial.  
  
3.  En el Editor de consultas, presione **F5** para ejecutar la instrucción y crear una base de datos con el nombre `TestData`.  
  
Al crear una base de datos, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] realiza una copia de la base de datos **model** y cambia el nombre de la copia por el nombre de la base de datos. Esta operación solo debería tardar algunos segundos, a menos que especifique un tamaño inicial grande de la base de datos como un parámetro opcional.  
  
> [!NOTE]  
> La palabra clave GO separa las instrucciones cuando se envían varias instrucciones en un solo lote. GO es opcional cuando el lote solo contiene una instrucción.  

## <a name="create-a-table"></a>Crear una tabla
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]

Para crear una tabla, debe proporcionar un nombre para ésta además de los nombres y los tipos de datos de cada columna de la tabla. También es recomendable indicar si se permiten valores NULL en cada columna. Para crear una tabla, debe tener el permiso `CREATE TABLE` y el permiso `ALTER SCHEMA` en el esquema que contiene la tabla. El rol fijo de base de datos [`db_ddladmin`](../relational-databases/security/authentication-access/database-level-roles.md) tiene estos permisos.  
  
La mayoría de las tablas tienen una clave principal, que se compone de una o varias columnas de la tabla. Una clave principal siempre es única. [!INCLUDE[ssDE](../includes/ssde-md.md)] exigirá la restricción de que el valor de la clave principal no se puede repetir en la tabla.  
  
Para obtener una lista de tipos de datos y vínculos para una descripción de cada uno, consulte [Tipos de datos &#40;Transact-SQL&#41;](../t-sql/data-types/data-types-transact-sql.md).  
  
> [!NOTE]  
> [!INCLUDE[ssDE](../includes/ssde-md.md)] se puede instalar para distinguir mayúsculas de minúsculas o no distinguir mayúsculas de minúsculas. Si se instala [!INCLUDE[ssDE](../includes/ssde-md.md)] para distinguir mayúsculas de minúsculas, los nombres de objetos siempre deben tener las mismas mayúsculas y minúsculas. Por ejemplo, una tabla denominada OrderData es diferente de la denominada ORDERDATA. Si se instala [!INCLUDE[ssDE](../includes/ssde-md.md)] para no distinguir mayúsculas de minúsculas, esos dos nombres de tablas se consideran la misma tabla y ese nombre solo se puede utilizar una vez.  
  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>Cambie la conexión del Editor de consultas a la base de datos TestData  
En una ventana del Editor de consultas, escriba y ejecute el siguiente código para cambiar la conexión a la base de datos `TestData` .  
  
  ```sql  
  USE TestData  
  GO  
  ```  
  
### <a name="create-the-table"></a>Creación de la tabla
En una ventana del Editor de consultas, escriba y ejecute el siguiente código para crear una tabla sencilla denominada `Products`. Las columnas de la tabla son `ProductID`, `ProductName`, `Price`y `ProductDescription`. La columna `ProductID` es la clave principal de la tabla. `int`, `varchar(25)`, `money`y `text` son todos los tipos de datos. Solo las columnas `Price` y `ProductionDescription` pueden no tener datos cuando se inserta o cambia una fila. Esta instrucción contiene un elemento opcional (`dbo.`) denominado esquema. El esquema es el objeto de base de datos propietario de la tabla. Si es un administrador, `dbo` es el esquema predeterminado. `dbo` hace referencia al propietario de la base de datos.  
  
  ```sql  
  CREATE TABLE dbo.Products  
     (ProductID int PRIMARY KEY NOT NULL,  
     ProductName varchar(25) NOT NULL,  
     Price money NULL,  
     ProductDescription text NULL)  
  GO  
 ```  

## <a name="insert-and-update-data-in-a-table"></a>Inserción y actualización de datos de una tabla
Ahora que ha creado la tabla **Products** , ya está listo para insertar datos en la tabla mediante la instrucción INSERT. Después de insertar los datos, cambiará el contenido de una fila con una instrucción UPDATE. Utilizará la cláusula WHERE de la instrucción UPDATE para restringir la actualización a una sola fila. Las cuatro instrucciones introducirán los siguientes datos.  
  
|ProductID|ProductName|Price|ProductDescription|  
|-------------|---------------|---------|----------------------|  
|1|Clamp|12,48|Workbench clamp|  
|50|Screwdriver|3,17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|3mm Bracket|,52||  
  
La sintaxis básica es: INSERT, nombre de tabla, lista de columnas, VALUES y, a continuación, una lista de los valores que se van a insertar. Los dos guiones dobles antes de cada línea indican que la línea es un comentario y el compilador ignorará el texto. En este caso, el comentario describe una variación permitida de la sintaxis.  
  
### <a name="insert-data-into-a-table"></a>Inserción de datos en una tabla  
  
1.  Ejecute la instrucción siguiente para insertar una fila en la tabla `Products` que se ha creado en la tarea anterior. Ésta es la sintaxis básica.  
  
   ```sql 
   -- Standard syntax  
   INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
       VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
   GO   
   ```  
  
2.  La instrucción siguiente muestra cómo se puede cambiar el orden en que se proporcionan los parámetros modificando la situación de `ProductID` y `ProductName` en la lista de campos (entre paréntesis) y en la lista de valores.  
  
   ```sql  
   -- Changing the order of the columns  
   INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
       VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
   GO    
   ```  
  
3.  La instrucción siguiente demuestra que los nombres de las columnas son opcionales, siempre y cuando los valores se enumeren en el orden correcto. Esta sintaxis es habitual, pero no se recomienda porque podría ser difícil para otros comprender su código. `NULL` se especifica para la columna `Price` porque el precio de este producto no se conoce todavía.  
  
   ```sql  
   -- Skipping the column list, but keeping the values in order  
   INSERT dbo.Products  
       VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
   GO  
  ```  
  
4.  El nombre de esquema es opcional mientras tenga acceso a una tabla del esquema predeterminado y la modifique. Puesto que la columna `ProductDescription` permite valores NULL y no se ha proporcionado ningún valor, el nombre de columna y el valor de `ProductDescription` se pueden quitar por completo de la instrucción.  
  
   ```sql  
   -- Dropping the optional dbo and dropping the ProductDescription column  
   INSERT Products (ProductID, ProductName, Price)  
       VALUES (3000, '3mm Bracket', .52)  
   GO  
   ```  
  
### <a name="update-the-products-table"></a>Actualización de la tabla de productos  
Escriba y ejecute la siguiente instrucción `UPDATE` para cambiar el `ProductName` del segundo producto de `Screwdriver`a `Flat Head Screwdriver`.  
  
  ```sql  
  UPDATE dbo.Products  
      SET ProductName = 'Flat Head Screwdriver'  
      WHERE ProductID = 50  
  GO  
  ```  

## <a name="read-data-from-a-table"></a>Lectura de datos de una tabla
Use la instrucción SELECT para leer los datos de una tabla. La instrucción SELECT es una de las instrucciones de [!INCLUDE[tsql](../includes/tsql-md.md)] más importantes y tiene muchas variaciones en la sintaxis. Para este tutorial, trabajará con cinco versiones sencillas.  
  
### <a name="read-the-data-in-a-table"></a>Lectura de datos en una tabla  
  
1.  Escriba y ejecute las siguientes instrucciones para leer los datos de la tabla `Products` .  
  
  ```sql 
  -- The basic syntax for reading data from a single table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
  GO  
  ```  
  
2.  Puede usar un asterisco para seleccionar todas las columnas de la tabla. Esto se suele usar en las consultas ad hoc. Debe proporcionar la lista de columnas en el código permanente de modo que la instrucción devuelva las columnas previstas, incluso si más tarde se agrega una columna nueva a la tabla.  
  
  ```sql  
  -- Returns all columns in the table  
  -- Does not use the optional schema, dbo  
  SELECT * FROM Products  
  GO   
  ```  
  
3.  Puede omitir columnas que ya no desea que se devuelvan. Las columnas se devolverán en el orden en que aparecen.  
  
  ```sql  
  -- Returns only two of the columns from the table  
  SELECT ProductName, Price  
      FROM dbo.Products  
  GO    
  ```  
  
4.  Use una cláusula `WHERE` para limitar las filas que se devuelven al usuario.  
  
  ``` sql 
  -- Returns only two of the records in the table  
  SELECT ProductID, ProductName, Price, ProductDescription  
      FROM dbo.Products  
      WHERE ProductID < 60  
  GO    
  ```  
  
5.  Puede trabajar con los valores de las columnas según se devuelven. En el siguiente ejemplo se realiza una operación matemática en la columna `Price` . Las columnas que se han cambiado de esta manera no tendrán un nombre, a menos que proporcione uno mediante la palabra clave `AS` .  
  
  ```sql  
  -- Returns ProductName and the Price including a 7% tax  
  -- Provides the name CustomerPays for the calculated column  
  SELECT ProductName, Price * 1.07 AS CustomerPays  
      FROM dbo.Products  
  GO  
  ```  
  
### <a name="useful-functions-in-a-select-statement"></a>Funciones útiles en una instrucción SELECT  
Para obtener información sobre algunas de las funciones que puede usar para trabajar con datos en instrucciones SELECT, vea los siguientes temas:  
  
|||  
|-|-|  
|[Funciones de cadena &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)|[Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)|  
|[Funciones matemáticas &#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)|[Funciones de texto e imagen &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|  

## <a name="create-views-and-stored-procedures"></a>Creación de vistas y procedimientos almacenados
Una vista es una instrucción SELECT almacenada y un procedimiento almacenado es una o varias instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] que se ejecutan como un lote.  
  
Las vistas se consultan como las tablas y no aceptan parámetros. Los procedimientos almacenados son más complejos que las vistas. Los procedimientos almacenados pueden tener parámetros de entrada y salida y pueden contener instrucciones para controlar el flujo del código, como instrucciones IF y WHILE. Una práctica recomendable de programación es usar procedimientos almacenados para realizar todas las tareas repetitivas en la base de datos.  
  
Para este ejemplo, usará CREATE VIEW para crear una vista que seleccione solo dos de las columnas de la tabla **Products** . A continuación, usará CREATE PROCEDURE para crear un procedimiento almacenado que acepta un parámetro de precio y devuelve solo los productos cuyo costo es menor que el valor del parámetro especificado.  
  
### <a name="create-a-view"></a>Creación de una vista  
  
Ejecute la instrucción siguiente para crear una vista muy sencilla que ejecuta una instrucción SELECT y devuelve los nombres y los precios de nuestros productos al usuario.  
  
  ```sql  
  CREATE VIEW vw_Names  
     AS  
     SELECT ProductName, Price FROM Products;  
  GO    
  ```  
  
### <a name="test-the-view"></a>Pruebe la vista  
  
Las vistas se tratan como tablas. Use una instrucción `SELECT` para tener acceso a la vista.  
  
  ```sql  
  SELECT * FROM vw_Names;  
  GO   
  ```  
  
### <a name="create-a-stored-procedure"></a>Creación de un procedimiento almacenado  
  
La siguiente instrucción crea un procedimiento almacenado denominado `pr_Names`, acepta un parámetro de entrada denominado `@VarPrice` del tipo de datos `money`. El procedimiento almacenado imprime la instrucción `Products less than` concatenada con el parámetro de entrada que cambia del tipo de datos `money` a un tipo de datos de carácter `varchar(10)` . A continuación, el procedimiento ejecuta una instrucción `SELECT` en la vista y le pasa el parámetro de entrada como parte de la cláusula `WHERE` . Esto devuelve todos los productos cuyo costo es menor que el valor del parámetro de entrada.  
  
  ```sql  
  CREATE PROCEDURE pr_Names @VarPrice money  
     AS  
     BEGIN  
        -- The print statement returns text to the user  
        PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
        -- A second statement starts here  
        SELECT ProductName, Price FROM vw_Names  
              WHERE Price < @varPrice;  
     END  
  GO    
  ```  
  
### <a name="test-the-stored-procedure"></a>Probar el procedimiento almacenado  
  
Para probar el procedimiento almacenado, escriba y ejecute la instrucción siguiente. El procedimiento debe devolver los nombres de dos productos introducidos en la tabla `Products` en la lección 1 con un precio menor que `10.00`.  
  
  ```sql  
  EXECUTE pr_Names 10.00;  
  GO  
  ```  

## <a name="next-steps"></a>Pasos siguientes
En el siguiente artículo se muestra cómo configurar permisos en objetos de base de datos. Los objetos creados en la primera lección también se usarán en la segunda. 

Vaya al siguiente artículo para más información:
> [!div class="nextstepaction"]
> [Pasos siguientes](../t-sql/lesson-2-configuring-permissions-on-database-objects.md)
  
  
  
