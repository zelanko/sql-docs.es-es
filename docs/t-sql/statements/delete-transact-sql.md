---
title: DELETE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DELETE
- DELETE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- row removal [SQL Server]
- DELETE statement [SQL Server], about DELETE statement
- views [SQL Server], deleting rows
- removing rows
- tables [SQL Server], deleting rows
- DELETE statement [SQL Server]
- deleting rows
- row removal [SQL Server], DELETE statement
- deleting data
ms.assetid: ed6b2105-0f35-408f-ba51-e36ade7ad5b2
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: f0741ba08adf5299e8a4f5a3021f533d44988459
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="delete-transact-sql"></a>DELETE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Quita una o varias filas de una tabla o vista en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
[ WITH <common_table_expression> [ ,...n ] ]  
DELETE   
    [ TOP ( expression ) [ PERCENT ] ]   
    [ FROM ]   
    { { table_alias  
      | <object>   
      | rowset_function_limited   
      [ WITH ( table_hint_limited [ ...n ] ) ] }   
      | @table_variable  
    }  
    [ <OUTPUT Clause> ]  
    [ FROM table_source [ ,...n ] ]   
    [ WHERE { <search_condition>   
            | { [ CURRENT OF   
                   { { [ GLOBAL ] cursor_name }   
                       | cursor_variable_name   
                   }   
                ]  
              }  
            }   
    ]   
    [ OPTION ( <Query Hint> [ ,...n ] ) ]   
[; ]  
  
<object> ::=  
{   
    [ server_name.database_name.schema_name.   
      | database_name. [ schema_name ] .   
      | schema_name.  
    ]  
    table_or_view_name   
}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
DELETE FROM [database_name . [ schema ] . | schema. ] table_name    
    [ WHERE <search_condition> ]   
    [ OPTION ( <query_options> [ ,...n ]  ) ]  
[; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 CON \<common_table_expression >  
 Especifica el conjunto de resultados de nombre temporal, también conocido como expresión de tabla común, definido dentro del ámbito de la instrucción DELETE. El conjunto de resultados se deriva de una instrucción SELECT.  
  
 Las expresiones de tabla comunes también se pueden utilizar con las instrucciones SELECT, INSERT, UPDATE y CREATE VIEW. Para obtener más información, consulte [con common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Parte superior **(***expresión***)** [%]  
 Especifica el número o el porcentaje de filas aleatorias que se van a eliminar. *expression* puede ser un número o un porcentaje de las filas. Las filas a las que se hace referencia en la expresión TOP utilizada con INSERT, UPDATE o DELETE no se ordenan. Para obtener más información, vea [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 FROM  
 Una palabra clave opcional que se puede usar entre la palabra clave DELETE y el destino *nombre_tabla_o_vista*, o *funciónConjuntoFilasLimit*.  
  
 *aliasTabla*  
 El alias especificado en el campo de *table_source* cláusula que representa la tabla o la vista desde la que las filas se va a eliminar.  
  
 *nombre_servidor*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 El nombre del servidor (con un nombre de servidor vinculado o [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) funcionar como el nombre del servidor) en el que se encuentra la tabla o vista. Si *nombre_servidor* se especifica, *database_name* y *schema_name* son necesarios.  
  
 *database_name*  
 El nombre de la base de datos.  
  
 *schema_name*  
 Nombre del esquema al que pertenece la tabla o la vista.  
  
 *view_name table_or*  
 Nombre de la tabla o vista cuyas filas se van a quitar.  
  
 En este ámbito, se puede utilizar una variable de tabla como origen de tabla de una instrucción DELETE.  
  
 La vista hace referencia a *nombre_tabla_o_vista* debe ser actualizable y referencia exactamente a una tabla base en la cláusula FROM de la definición de vista. Para obtener más información acerca de las vistas actualizables, vea [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 *funciónConjuntoFilasLimitado*  
 **Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Ya sea la [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) o [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) función, dependiendo del proveedor.  
  
 CON **(** \<sugerenciaTablaLimitada > [... *n*] **)**  
 Especifica una o varias sugerencias de tabla que están permitidas en una tabla de destino. La palabra clave WITH y los paréntesis son obligatorios. No se permiten NOLOCK ni READUNCOMMITTED. Para obtener más información acerca de las sugerencias de tabla, vea [sugerencias de tabla &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
 \<OUTPUT_Clause >  
 Devuelve filas eliminadas, o expresiones basadas en ellas, como parte de la operación DELETE. La cláusula OUTPUT no se admite en instrucciones DML dirigidas a tablas o vistas remotas. Para obtener más información, vea [cláusula OUTPUT &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
 DE *table_source*  
 Especifica una cláusula FROM adicional. Esto [!INCLUDE[tsql](../../includes/tsql-md.md)] extensión DELETE permite especificar datos de \<table_source > y eliminar las filas correspondientes de la tabla en el primer campo de cláusula.  
  
 Se puede utilizar esta extensión, que especifica una combinación, en lugar de una subconsulta en la cláusula WHERE para identificar las filas que se van a quitar.  
  
 Para obtener más información, vea [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
 WHERE  
 Especifica las condiciones utilizadas para limitar el número de filas que se van a eliminar. Si no se proporciona una cláusula WHERE, DELETE quita todas las filas de la tabla.  
  
 Hay dos formas de operaciones de eliminación, que se basan en las condiciones que se especifiquen en la cláusula WHERE:  
  
-   Las eliminaciones por búsqueda especifican una condición de búsqueda que califica las filas que se van a eliminar. Por ejemplo, donde *column_name* = *valor*.  
  
-   Las eliminaciones por posición utilizan la cláusula CURRENT OF para especificar un cursor. La operación de eliminación se produce en la posición actual del cursor. Esto puede ser más preciso que una instrucción DELETE por búsqueda que utilice un WHERE *search_condition* cláusula para calificar las filas que se va a eliminar. Una instrucción DELETE por búsqueda elimina varias filas si la condición de búsqueda no identifica exclusivamente una única fila.  
  
\<search_condition >  
 Especifica las condiciones restrictivas de las filas que se van a eliminar. No hay límite en el número de predicados que se pueden incluir en una condición de búsqueda. Para obtener más información, vea [condición de búsqueda &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
 CURRENT OF  
 Especifica que la instrucción DELETE se ejecutará en la posición actual del cursor especificado.  
  
 GLOBAL  
 Especifica que *cursor_name* hace referencia a un cursor global.  
  
 *cursor_name*  
 Es el nombre del cursor abierto desde el que se realiza la captura. Si tanto un cursor global y otro local con el nombre *cursor_name* existe, este argumento hace referencia al cursor global si se especifica GLOBAL; en caso contrario, hace referencia al cursor local. El cursor debe permitir actualizaciones.  
  
 *cursor_variable_name*  
 Nombre de una variable de cursor. La variable de cursor debe hacer referencia a un cursor que permita realizar actualizaciones.  
  
 OPCIÓN **(** \<query_hint > [ **,**... *n*] **)**  
 Palabras clave que indican que se utilizan sugerencias del optimizador para personalizar el procesamiento de la instrucción por parte del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para obtener más información, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Para eliminar todas las filas de una tabla, use TRUNCATE TABLE. TRUNCATE TABLE es más rápido que DELETE y utiliza menos recursos de los registros de transacciones y de sistema. TRUNCATE TABLE tiene restricciones; por ejemplo, la tabla no puede participar en la replicación. Para obtener más información, vea [TRUNCATE TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/truncate-table-transact-sql.md)  
  
 Use el @@ROWCOUNT eliminado de función para devolver el número de filas a la aplicación cliente. Para obtener más información, consulte [@@ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md).  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Puede implementar el control de errores de la instrucción DELETE especificando la instrucción en una construcción TRY…CATCH.  
  
 La instrucción DELETE puede tener un error si infringe un desencadenador o intenta quitar una fila a la que hacen referencia datos de otra tabla con una restricción FOREIGN KEY. Si la instrucción DELETE quita varias filas y cualquiera de las filas eliminadas infringe un desencadenador o restricción, se cancela la instrucción, se devuelve un error y no se elimina ninguna fila.  
  
 Cuando una instrucción DELETE encuentra un error aritmético (desbordamiento, división entre cero o error de dominio) al evaluar una expresión, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] trata ese error como si SET ARITHABORT fuese ON. Se cancela el resto del proceso por lotes y se devuelve un mensaje de error.  
  
## <a name="interoperability"></a>Interoperabilidad  
 Es posible utilizar DELETE en el cuerpo de una función definida por el usuario si el objeto que se va a modificar es una variable de tabla.  
  
 Al eliminar una fila que contiene una columna FILESTREAM, también elimina los archivos del sistema de archivos subyacentes. El recolector de elementos no utilizados de FILESTREAM quita los archivos subyacentes. Para obtener más información, consulte [acceder a los datos de FILESTREAM con Transact-SQL](../../relational-databases/blob/access-filestream-data-with-transact-sql.md).  
  
 No se puede especificar la cláusula FROM en una instrucción DELETE que haga referencia, directa o indirectamente, a una vista que tiene definido un desencadenador INSTEAD OF. Para obtener más información acerca de desencadenadores INSTEAD OF, vea [CREATE TRIGGER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Cuando se usa TOP con DELETE, las filas a las que hace referencia no están organizadas de ninguna manera y la cláusula ORDER BY no se puede especificar directamente en esta instrucción. Si necesita utilizar TOP para eliminar filas por un orden cronológico significativo, debe usar TOP junto con una cláusula ORDER BY en una instrucción de subselección. Vea la sección Ejemplos que aparece más adelante en este tema.  
  
 TOP no se puede usar en una instrucción DELETE con vistas divididas en particiones.  
  
## <a name="locking-behavior"></a>Comportamiento del bloqueo  
 De forma predeterminada, una instrucción DELETE siempre adquiere un bloqueo exclusivo (X) en la tabla que modifica y retiene ese bloqueo hasta que se completa la transacción. Al utilizar un bloqueo exclusivo (X), el resto de las transacciones no pueden modificar los datos; las operaciones de lectura solo se pueden realizar si se utiliza la sugerencia NOLOCK o el nivel de aislamiento de lectura no confirmada. Puede especificar sugerencias de tabla para invalidar este comportamiento predeterminado durante la ejecución de la instrucción DELETE especificando otro método de bloqueo, sin embargo se recomienda que solo los desarrolladores y administradores de bases de datos experimentados usen las sugerencias y únicamente como último recurso. Para obtener más información, vea [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Cuando se eliminan filas de un montón, [!INCLUDE[ssDE](../../includes/ssde-md.md)] puede usar bloqueo de filas o páginas para la operación. Como consecuencia, las páginas que han quedado vacías por la operación de eliminación permanecen asignadas al montón. Si no se cancela la asignación de las páginas vacías, otros objetos de la base de datos no pueden volver a utilizar el espacio asociado.  
  
 Para eliminar las filas de un montón y cancelar la asignación de las páginas, use uno de los métodos siguientes.  
  
-   Especifique la sugerencia TABLOCK en la instrucción DELETE. Si se utiliza la sugerencia TABLOCK, la operación de eliminación aplica un bloqueo exclusivo a la tabla, en lugar de un bloqueo de fila o de página. Esto permite cancelar la asignación de las páginas. Para obtener más información acerca de la sugerencia TABLOCK, vea [sugerencias de tabla &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
-   Se debe utilizar TRUNCATE TABLE si se van a eliminar todas las filas de la tabla.  
  
-   Cree un índice clúster en el montón antes de eliminar las filas. Puede quitar el índice clúster tras eliminar las filas. Este método requiere más tiempo que los métodos anteriores y utiliza más recursos temporales.  
  
> [!NOTE]  
>  Páginas vacías se pueden quitar de un montón en cualquier momento mediante el uso de la `ALTER TABLE <table_name> REBUILD` instrucción.  
  
## <a name="logging-behavior"></a>Comportamiento del registro  
 La instrucción DELETE siempre está registrada totalmente.  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Se requieren permisos DELETE en la tabla de destino. También se requieren los permisos para utilizar SELECT si la instrucción contiene una cláusula WHERE.  
  
 ELIMINAR los permisos predeterminados de los miembros de la **sysadmin** fija de servidor sysadmin el **db_owner** y **db_datawriter** se han corregido los roles de base de datos y el propietario de la tabla. Los miembros de la **sysadmin**, **db_owner**y el **db_securityadmin** roles y el propietario de la tabla pueden transferir permisos a otros usuarios.  
  
## <a name="examples"></a>Ejemplos  
  
|Categoría|Elementos de sintaxis ofrecidos|  
|--------------|------------------------------|  
|[Sintaxis básica](#BasicSyntax)|DELETE|  
|[Limitar las filas eliminadas](#LimitRows)|WHERE • FROM • cursor •|  
|[Eliminar filas de una tabla remota](#RemoteTables)|Servidor vinculado • función de conjunto de filas OPENQUERY • función de conjunto de filas OPENDATASOURCE|  
|[Capturar los resultados de la instrucción DELETE](#CaptureResults)|Cláusula OUTPUT|  
  
###  <a name="BasicSyntax"></a>Sintaxis básica  
 En los ejemplos de esta sección se muestra la funcionalidad básica de la instrucción DELETE usando la sintaxis mínima requerida.  
  
#### <a name="a-using-delete-with-no-where-clause"></a>A. Utilizar DELETE sin la cláusula WHERE  
 En el ejemplo siguiente se eliminan todas las filas de la tabla `SalesPersonQuotaHistory` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] porque no se utiliza una cláusula WHERE para limitar el número de filas eliminadas.  
  
```  
DELETE FROM Sales.SalesPersonQuotaHistory;  
GO  
```  
  
###  <a name="LimitRows"></a>Limitar las filas eliminadas  
 En los ejemplos de esta sección se muestra cómo se limita el número de filas que se van a eliminar.  
  
#### <a name="b-using-the-where-clause-to-delete-a-set-of-rows"></a>B. Usar la cláusula WHERE para eliminar un conjunto de filas  
 En el ejemplo siguiente se elimina todas las filas de la `ProductCostHistory` tabla el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos en el que el valor de la `StandardCost` columna es más de `1000.00`.  
  
```    
DELETE FROM Production.ProductCostHistory  
WHERE StandardCost > 1000.00;  
GO  
```  
  
 En el siguiente ejemplo se muestra una cláusula WHERE más compleja. La cláusula WHERE define dos condiciones que deben cumplirse para determinar las filas que se van a eliminar. El valor de la columna `StandardCost` debe estar comprendido entre `12.00` y `14.00` y el valor de la columna `SellEndDate` debe ser NULL. También se imprime el valor de la **@@ROWCOUNT**  función para devolver el número de filas eliminadas.  
  
```  
DELETE Production.ProductCostHistory  
WHERE StandardCost BETWEEN 12.00 AND 14.00  
      AND EndDate IS NULL;  
PRINT 'Number of rows deleted is ' + CAST(@@ROWCOUNT as char(3));  
```  
  
#### <a name="c-using-a-cursor-to-determine-the-row-to-delete"></a>C. Usar un cursor para determinar la fila que se va a eliminar  
 En el ejemplo siguiente se elimina una fila única de la `EmployeePayHistory` tabla el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos mediante un cursor denominado `my_cursor`. La operación de eliminación solo afecta a la única fila que se captura actualmente del cursor.  
  
```  
DECLARE complex_cursor CURSOR FOR  
    SELECT a.BusinessEntityID  
    FROM HumanResources.EmployeePayHistory AS a  
    WHERE RateChangeDate <>   
         (SELECT MAX(RateChangeDate)  
          FROM HumanResources.EmployeePayHistory AS b  
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;  
OPEN complex_cursor;  
FETCH FROM complex_cursor;  
DELETE FROM HumanResources.EmployeePayHistory  
WHERE CURRENT OF complex_cursor;  
CLOSE complex_cursor;  
DEALLOCATE complex_cursor;  
GO  
```  
  
#### <a name="d-using-joins-and-subqueries-to-data-in-one-table-to-delete-rows-in-another-table"></a>D. Usar combinaciones y subconsultas en los datos de una tabla para eliminar filas de otra tabla  
 En los siguientes ejemplos se muestran dos maneras de eliminar filas de una tabla en función de los datos de otra tabla. En ambos ejemplos, las filas de la `SalesPersonQuotaHistory` tabla el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos se eliminan en función de las ventas del año hasta la fecha almacenadas en el `SalesPerson` tabla. La primera `DELETE` instrucción muestra la solución de subconsulta compatible con ISO y el segundo `DELETE` instrucción muestra la [!INCLUDE[tsql](../../includes/tsql-md.md)] de extensión para combinar las dos tablas.  
  
```  
-- SQL-2003 Standard subquery  
  
DELETE FROM Sales.SalesPersonQuotaHistory   
WHERE BusinessEntityID IN   
    (SELECT BusinessEntityID   
     FROM Sales.SalesPerson   
     WHERE SalesYTD > 2500000.00);  
GO  
```  
  
```  
-- Transact-SQL extension  
  
DELETE FROM Sales.SalesPersonQuotaHistory   
FROM Sales.SalesPersonQuotaHistory AS spqh  
INNER JOIN Sales.SalesPerson AS sp  
ON spqh.BusinessEntityID = sp.BusinessEntityID  
WHERE sp.SalesYTD > 2500000.00;  
GO  
```  
  
```  
-- No need to mention target table more than once.  
  
DELETE spqh  
  FROM  
        Sales.SalesPersonQuotaHistory AS spqh  
    INNER JOIN Sales.SalesPerson AS sp  
        ON spqh.BusinessEntityID = sp.BusinessEntityID  
  WHERE  sp.SalesYTD > 2500000.00;  
```  
  
#### <a name="e-using-top-to-limit-the-number-of-rows-deleted"></a>E. Utilizar TOP para limitar el número de filas eliminadas  
 Cuando una parte superior (*n*) se utiliza la cláusula con la eliminación, la operación de eliminación se realiza en una selección aleatoria de  *n*  número de filas. En el ejemplo siguiente se eliminan `20` filas aleatorias de la `PurchaseOrderDetail` tabla el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos que tienen debido a las fechas anteriores al 1 de julio de 2006.  
  
```  
DELETE TOP (20)   
FROM Purchasing.PurchaseOrderDetail  
WHERE DueDate < '20020701';  
GO  
```  
  
 Si necesita utilizar TOP para eliminar filas por un orden cronológico significativo, debe utilizarla junto con ORDER BY en una instrucción de subselección. La siguiente consulta elimina de la tabla `PurchaseOrderDetail` las 10 filas con las fechas de vencimiento más antiguas. Para garantizar que solo se eliminen 10 filas, la columna especificada en la instrucción de subselección (`PurchaseOrderID`) es la clave principal de la tabla. El uso de una columna sin clave en la instrucción de subselección podría causar la eliminación de más de 10 filas si la columna especificada contiene valores duplicados.  
  
```  
DELETE FROM Purchasing.PurchaseOrderDetail  
WHERE PurchaseOrderDetailID IN  
   (SELECT TOP 10 PurchaseOrderDetailID   
    FROM Purchasing.PurchaseOrderDetail   
    ORDER BY DueDate ASC);  
GO  
```  
  
###  <a name="RemoteTables"></a>Eliminar filas de una tabla remota  
 Ejemplos de esta sección muestran cómo se eliminan filas de una tabla remota mediante un [servidor vinculado](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) o un [función rowset](../../t-sql/functions/rowset-functions-transact-sql.md) para hacer referencia a la tabla remota. Una tabla remota existe en un servidor o instancia diferente de SQL Server.  
  
**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
#### <a name="f-deleting-data-from-a-remote-table-by-using-a-linked-server"></a>F. Eliminar datos de una tabla remota usando un servidor vinculado  
 En el ejemplo siguiente se eliminan filas de una tabla remota. El ejemplo comienza creando un vínculo al origen de datos remoto mediante el uso de [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). El nombre del servidor vinculado, `MyLinkServer`, a continuación, se especifica como parte del nombre de objeto de cuatro partes con el formato *servidor.catálogo.esquema.objeto*.  
  
```  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' or 'server_name\instance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  
```  
  
```  
-- Specify the remote data source using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
DELETE MyLinkServer.AdventureWorks2012.HumanResources.Department 
WHERE DepartmentID > 16;  
GO  
```  
  
#### <a name="g-deleting-data-from-a-remote-table-by-using-the-openquery-function"></a>G. Eliminar datos de una tabla remota con la función OPENQUERY  
 En el ejemplo siguiente se elimina filas de una tabla remota especificando la [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) función de conjunto de filas. En este ejemplo se usa el nombre del servidor vinculado creado en el ejemplo anterior.  
  
```  
DELETE OPENQUERY (MyLinkServer, 'SELECT Name, GroupName 
FROM AdventureWorks2012.HumanResources.Department  
WHERE DepartmentID = 18');  
GO  
```  
  
#### <a name="h-deleting-data-from-a-remote-table-by-using-the-opendatasource-function"></a>H. Eliminar datos de una tabla remota con una función OPENDATASOURCE  
 En el ejemplo siguiente se elimina filas de una tabla remota especificando la [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) función de conjunto de filas. Especifique un nombre de servidor válido para el origen de datos con el formato *nombre_servidor* o *nombre_servidor ombre_instancia*.  
  
```  
DELETE FROM OPENDATASOURCE('SQLNCLI',  
    'Data Source= <server_name>; Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department   
WHERE DepartmentID = 17;'  
```  
  
###  <a name="CaptureResults"></a>Capturar los resultados de la instrucción DELETE  
  
#### <a name="i-using-delete-with-the-output-clause"></a>I. Usar DELETE con la cláusula OUTPUT  
 En el ejemplo siguiente se muestra cómo guardar los resultados de un `DELETE` instrucción a una variable de tabla en la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos.  
  
```  
DELETE Sales.ShoppingCartItem  
OUTPUT DELETED.*   
WHERE ShoppingCartID = 20621;  
  
--Verify the rows in the table matching the WHERE clause have been deleted.  
SELECT COUNT(*) AS [Rows in Table] 
FROM Sales.ShoppingCartItem 
WHERE ShoppingCartID = 20621;  
GO  
```  
  
#### <a name="j-using-output-with-fromtablename-in-a-delete-statement"></a>J. Utilizar OUTPUT con <from_table_name> en una instrucción DELETE  
 En el ejemplo siguiente se elimina las filas de la `ProductProductPhoto` tabla el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos en función de criterios de búsqueda definidos en el `FROM` cláusula de la `DELETE` instrucción. La cláusula `OUTPUT` devuelve columnas de la tabla que se elimina ( `DELETED.ProductID`, `DELETED.ProductPhotoID`) y de la tabla `Product` . Esta información se utiliza en la cláusula `FROM` para especificar las filas que se deben eliminar.  
  
```  
DECLARE @MyTableVar table (  
    ProductID int NOT NULL,   
    ProductName nvarchar(50)NOT NULL,  
    ProductModelID int NOT NULL,   
    PhotoID int NOT NULL);  
  
DELETE Production.ProductProductPhoto  
OUTPUT DELETED.ProductID,  
       p.Name,  
       p.ProductModelID,  
       DELETED.ProductPhotoID  
    INTO @MyTableVar  
FROM Production.ProductProductPhoto AS ph  
JOIN Production.Product as p   
    ON ph.ProductID = p.ProductID   
    WHERE p.ProductModelID BETWEEN 120 and 130;  
  
--Display the results of the table variable.  
SELECT ProductID, ProductName, ProductModelID, PhotoID   
FROM @MyTableVar  
ORDER BY ProductModelID;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="k-delete-all-rows-from-a-table"></a>K. Eliminar todas las filas de una tabla  
 En el ejemplo siguiente se eliminan todas las filas de la tabla `Table1` porque no se utiliza una cláusula WHERE para limitar el número de filas eliminadas.  
  
```  
DELETE FROM Table1;  
```  
  
### <a name="l-delete-a-set-of-rows-from-a-table"></a>L. ELIMINAR un conjunto de filas de una tabla  
 En el ejemplo siguiente se elimina todas las filas de la `Table1` tabla que tienen un valor mayor que 1000.00 en la `StandardCost` columna.  
  
```  
DELETE FROM Table1  
WHERE StandardCost > 1000.00;  
```  
  
### <a name="m-using-label-with-a-delete-statement"></a>M. Uso de etiqueta con una instrucción DELETE  
 En el ejemplo siguiente se usa una etiqueta con la instrucción DELETE.  
  
```  
DELETE FROM Table1  
OPTION ( LABEL = N'label1' );  
  
```  
  
### <a name="n-using-a-label-and-a-query-hint-with-the-delete-statement"></a>N. Con una etiqueta y una sugerencia de consulta con la instrucción DELETE  
 Esta consulta muestra la sintaxis básica para el uso de una sugerencia de combinación de la consulta con la instrucción DELETE. Para obtener más información sobre las sugerencias de combinación y cómo usar la cláusula OPTION, consulte [opción (SQL Server PDW)](http://msdn.microsoft.com/en-us/72bbce98-305b-42fa-a19f-d89620621ecc).  
  
```  
-- Uses AdventureWorks  
  
DELETE FROM dbo.FactInternetSales  
WHERE ProductKey IN (   
    SELECT T1.ProductKey FROM dbo.DimProduct T1   
    JOIN dbo.DimProductSubcategory T2  
    ON T1.ProductSubcategoryKey = T2.ProductSubcategoryKey  
    WHERE T2.EnglishProductSubcategoryName = 'Road Bikes' )  
OPTION ( LABEL = N'CustomJoin', HASH JOIN ) ;  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [TRUNCATE TABLE &#40; Transact-SQL &#41;](../../t-sql/statements/truncate-table-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [CON common_table_expression &#40; Transact-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)   
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)  
  
  

