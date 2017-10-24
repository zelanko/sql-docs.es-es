---
title: MERGE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MERGE
- MERGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- updating data [SQL Server]
- modifying data [SQL Server], MERGE statement
- MERGE statement [SQL Server]
- adding data
- DML [SQL Server], MERGE statement
- table modifications [SQL Server], MERGE statement
- data manipulation language [SQL Server], MERGE statement
- inserting data
ms.assetid: c17996d6-56a6-482f-80d8-086a3423eecc
caps.latest.revision: 76
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d071a0137d39abb638131df391c72eae75292c08
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="merge-transact-sql"></a>MERGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Realiza operaciones de inserción, actualización o eliminación en una tabla de destino según los resultados de una combinación con una tabla de origen. Por ejemplo, puede sincronizar dos tablas insertando, actualizando o eliminando las filas de una tabla según las diferencias que se encuentren en la otra.  
  
 **Consejo de rendimiento:** el comportamiento condicional descrito para la instrucción MERGE funciona mejor cuando las dos tablas tienen una mezcla compleja de características de búsqueda de coincidencias. Por ejemplo, insertar una fila si no la hay, o actualizar la fila si esta coincide. Cuando simplemente se actualiza una tabla basada en las filas de otra tabla, se puede lograr un mejor rendimiento y escalabilidad con las instrucciones básicas INSERT, UPDATE y DELETE. Por ejemplo:  
  
```  
INSERT tbl_A (col, col2)  
SELECT col, col2   
FROM tbl_B   
WHERE NOT EXISTS (SELECT col FROM tbl_A A2 WHERE A2.col = tbl_B.col);  
```  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
[ WITH <common_table_expression> [,...n] ]  
MERGE   
    [ TOP ( expression ) [ PERCENT ] ]   
    [ INTO ] <target_table> [ WITH ( <merge_hint> ) ] [ [ AS ] table_alias ]  
    USING <table_source>   
    ON <merge_search_condition>  
    [ WHEN MATCHED [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ WHEN NOT MATCHED [ BY TARGET ] [ AND <clause_search_condition> ]  
        THEN <merge_not_matched> ]  
    [ WHEN NOT MATCHED BY SOURCE [ AND <clause_search_condition> ]  
        THEN <merge_matched> ] [ ...n ]  
    [ <output_clause> ]  
    [ OPTION ( <query_hint> [ ,...n ] ) ]      
;  
  
<target_table> ::=  
{   
    [ database_name . schema_name . | schema_name . ]  
  target_table  
}  
  
<merge_hint>::=  
{  
    { [ <table_hint_limited> [ ,...n ] ]  
    [ [ , ] INDEX ( index_val [ ,...n ] ) ] }  
}  
  
<table_source> ::=   
{  
    table_or_view_name [ [ AS ] table_alias ] [ <tablesample_clause> ]   
        [ WITH ( table_hint [ [ , ]...n ] ) ]   
  | rowset_function [ [ AS ] table_alias ]   
        [ ( bulk_column_alias [ ,...n ] ) ]   
  | user_defined_function [ [ AS ] table_alias ]  
  | OPENXML <openxml_clause>   
  | derived_table [ AS ] table_alias [ ( column_alias [ ,...n ] ) ]   
  | <joined_table>   
  | <pivoted_table>   
  | <unpivoted_table>   
}  
  
<merge_search_condition> ::=  
    <search_condition>  
  
<merge_matched>::=  
    { UPDATE SET <set_clause> | DELETE }  
  
<set_clause>::=  
SET  
  { column_name = { expression | DEFAULT | NULL }  
  | { udt_column_name.{ { property_name = expression  
                        | field_name = expression }  
                        | method_name ( argument [ ,...n ] ) }  
    }  
  | column_name { .WRITE ( expression , @Offset , @Length ) }  
  | @variable = expression  
  | @variable = column = expression  
  | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
  } [ ,...n ]   
  
<merge_not_matched>::=  
{  
    INSERT [ ( column_list ) ]   
        { VALUES ( values_list )  
        | DEFAULT VALUES }  
}  
  
<clause_search_condition> ::=  
    <search_condition>  
  
<search condition> ::=  
    { [ NOT ] <predicate> | ( <search_condition> ) }   
    [ { AND | OR } [ NOT ] { <predicate> | ( <search_condition> ) } ]   
[ ,...n ]   
  
<predicate> ::=   
    { expression { = | < > | ! = | > | > = | ! > | < | < = | ! < } expression   
    | string_expression [ NOT ] LIKE string_expression   
  [ ESCAPE 'escape_character' ]   
    | expression [ NOT ] BETWEEN expression AND expression   
    | expression IS [ NOT ] NULL   
    | CONTAINS   
  ( { column | * } , '< contains_search_condition >' )   
    | FREETEXT ( { column | * } , 'freetext_string' )   
    | expression [ NOT ] IN ( subquery | expression [ ,...n ] )   
    | expression { = | < > | ! = | > | > = | ! > | < | < = | ! < }   
  { ALL | SOME | ANY} ( subquery )   
    | EXISTS ( subquery ) }   
  
<output_clause>::=  
{  
    [ OUTPUT <dml_select_list> INTO { @table_variable | output_table }  
        [ (column_list) ] ]  
    [ OUTPUT <dml_select_list> ]  
}  
  
<dml_select_list>::=  
    { <column_name> | scalar_expression }   
        [ [AS] column_alias_identifier ] [ ,...n ]  
  
<column_name> ::=  
    { DELETED | INSERTED | from_table_name } . { * | column_name }  
    | $action  
```  
  
## <a name="arguments"></a>Argumentos  
 CON \<common_table_expression >  
 Especifica la vista o el conjunto de resultados temporal indicado, que también se conoce como expresión de tabla común, definido en el ámbito de la instrucción MERGE. El conjunto de resultados se deriva de una consulta simple. La instrucción MERGE hace referencia al conjunto de resultados. Para obtener más información, consulte [con common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Parte superior ( *expresión* ) [%]  
 Especifica el número o porcentaje de filas afectadas. *expresión* puede ser un número o un porcentaje de las filas. Las filas a las que se hace referencia en la expresión TOP no están organizadas en ningún orden. Para obtener más información, vea [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 La cláusula TOP se aplica después de que se combinen toda la tabla de origen y toda la tabla de destino, y se quiten las filas combinadas que no reúnan las condiciones para las acciones de inserción, actualización o eliminación. La cláusula TOP reduce aún más el número de filas combinadas al valor especificado y se aplican las acciones de inserción, actualización o eliminación a las filas combinadas restantes de una manera desordenada. Es decir, no hay ningún orden en el que las filas se distribuyan entre las acciones definidas en las cláusulas WHEN. Por ejemplo, cuando se especifica TOP (10) afecta a 10 filas; de estas filas, 7 se pueden actualizar y 3 insertar, o se pueden eliminar 1, actualizar 5 e insertar 4, etc.  
  
 Dado que la instrucción MERGE realiza exámenes de tabla completos de ambas tablas, de destino y de origen, el rendimiento de E/S puede verse afectado al utilizar la cláusula TOP para modificar una tabla grande mediante la creación de varios lotes. En este escenario, es importante asegurarse de que todos los lotes sucesivos tengan como destino nuevas filas.  
  
 *database_name*  
 Es el nombre de la base de datos en el que *target_table* se encuentra.  
  
 *schema_name*  
 Es el nombre del esquema al que *target_table* pertenece.  
  
 *target_table*  
 Es la tabla o vista en la que los datos de filas de \<table_source > se comparan en función de \<clause_search_condition >. *target_table* es el destino de cualquier operaciones de inserción, actualización o eliminación especificadas por las cláusulas WHEN de la instrucción MERGE.  
  
 Si *target_table* es una vista, cualquier acción con ella debe satisfacer las condiciones para actualizar las vistas. Para obtener más información, consulte [modificar datos mediante una vista](../../relational-databases/views/modify-data-through-a-view.md).  
  
 *target_table* no puede ser una tabla remota. *target_table* no puede tener ninguna regla definida en él.  
  
 [COMO] *aliasTabla*  
 Es un nombre alternativo que se utiliza para hacer referencia a una tabla.  
  
 USAR \<table_source >  
 Especifica el origen de datos que coincide con las filas de datos de *target_table* basado en \<merge_search condition >. El resultado de esta coincidencia dicta las acciones que tomarán las cláusulas WHEN de la instrucción MERGE. \<table_source > puede ser una tabla remota o una tabla derivada que tiene acceso a tablas remotas. 
  
 \<table_source > puede ser una tabla derivada que utiliza la [!INCLUDE[tsql](../../includes/tsql-md.md)] [constructor con valores de tabla](../../t-sql/queries/table-value-constructor-transact-sql.md) para construir una tabla especificando varias filas.  
  
 Para obtener más información sobre la sintaxis y los argumentos de esta cláusula, vea [FROM &#40; Transact-SQL &#41; ](../../t-sql/queries/from-transact-sql.md).  
  
 ON \<merge_search_condition >  
 Especifica las condiciones en la que \<table_source > se une con *target_table* para determinar dónde coinciden. 
  
> [!CAUTION]  
>  Es importante especificar solamente las columnas de la tabla de destino que se utilizan para los propósitos de la coincidencia. Es decir, especifique las columnas de la tabla de destino que se comparan con la correspondiente columna de la tabla de origen. No intente mejorar el rendimiento de las consultas filtrando las filas de la tabla de destino en la cláusula ON, según se especifica con `AND NOT target_table.column_x = value`. Si se hace esto, se pueden devolver resultados inesperados e incorrectos.  
  
 Cuando MATCHED THEN \<merge_matched >  
 Especifica que todas las filas de *target_table* que coincidan con las filas devueltas por \<table_source > ON \<merge_search_condition > y satisfacen alguna condición de búsqueda adicional, se actualizan o eliminan según el \<merge_matched > cláusula.  
  
 La instrucción MERGE puede tener a lo sumo dos cláusulas WHEN MATCHED. Si se especifican dos cláusulas, la primera cláusula debe ir acompañada de una operación AND \<search_condition > cláusula. Para una fila determinada, la segunda cláusula WHEN MATCHED se aplica solamente si no se aplica la primera. Si hay dos cláusulas WHEN MATCHED, una debe especificar una acción UPDATE y la otra una acción DELETE. Si se especifica UPDATE en el \<merge_matched > cláusula y más de una fila de \<table_source > coincide con una fila de *target_table* basado en \<merge_search_condition >, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]devuelve un error. La instrucción MERGE no puede actualizar la misma fila más de una vez, ni actualizar o eliminar la misma fila.  
  
 Cuando no MATCHED [BY TARGET] THEN \<merge_not_matched >  
 Especifica que se inserta una fila en *target_table* para cada fila devuelta por \<table_source > ON \<merge_search_condition > que no coincide con una fila de *target_table*, pero satisface una condición de búsqueda adicional, si está presente. Especifica los valores para insertar el \<merge_not_matched > cláusula. La instrucción MERGE puede tener solamente una cláusula WHEN NOT MATCHED.  
  
 WHEN NOT MATCHED BY SOURCE, a continuación, \<merge_matched >  
 Especifica que todas las filas de *target_table* que no coincidan con las filas devueltas por \<table_source > ON \<merge_search_condition >, y que satisfacen alguna condición de búsqueda adicional, se actualizan cualquiera o eliminan según la \<merge_matched > cláusula.  
  
 La instrucción MERGE puede tener a lo sumo dos cláusulas WHEN NOT MATCHED BY SOURCE. Si se especifican dos cláusulas, la primera cláusula debe ir acompañada de una operación AND \<clause_search_condition > cláusula. Para una fila determinada, la segunda cláusula WHEN NOT MATCHED BY SOURCE se aplica solamente si no se aplica la primera. Si hay dos cláusulas WHEN NOT MATCHED BY SOURCE, una debe especificar una acción UPDATE y la otra una acción DELETE. Solo las columnas de la tabla de destino pueden hacer referencia en \<clause_search_condition >.  
  
 Cuando se devuelve ninguna fila por \<table_source >, no se pueden tener acceso a las columnas de la tabla de origen. Si la acción update o delete especificada en el \<merge_matched > cláusula hace referencia a columnas de la tabla de origen, se devuelve el error 207 (nombre de columna no válido). La cláusula `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` puede hacer que la instrucción genere un error porque `Col1` en la tabla de origen es inaccesible.  
  
 Y \<clause_search_condition >  
 Especifica cualquier condición de búsqueda válida. Para obtener más información, vea [condición de búsqueda &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
 \<sugTablaLimit >  
 Especifica una o más sugerencias de tabla que se aplican en la tabla de destino para cada una de las acciones de inserción, actualización o eliminación que realiza la instrucción MERGE. La palabra clave WITH y los paréntesis son obligatorios.  
  
 No se permiten NOLOCK ni READUNCOMMITTED. Para obtener más información acerca de las sugerencias de tabla, vea [sugerencias de tabla &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Especificar la sugerencia TABLOCK en una tabla que es el destino de una instrucción INSERT tiene el mismo efecto que especificar la sugerencia TABLOCKX. Se realiza un bloqueo exclusivo en la tabla. Cuando se especifica FORCESEEK, se aplica a la instancia implícita de la tabla de destino combinada con la tabla de origen.  
  
> [!CAUTION]  
>  Si se especifica READPAST con WHEN NOT MATCHED [ BY TARGET ] THEN INSERT, pueden producirse operaciones INSERT que infrinjan las restricciones UNIQUE.  
  
 INDEX ( index_val [ ,...n ] )  
 Especifica el nombre o identificador de uno o más índices de la tabla de destino para realizar una combinación implícita con la tabla de origen. Para obtener más información, vea [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 \<output_clause >  
 Devuelve una fila para cada fila de *target_table* que se actualiza, inserta o elimina, sin ningún orden determinado. **$action** se puede especificar en la cláusula output. **$action** es una columna de tipo **nvarchar (10)** que devuelve uno de estos tres valores para cada fila: 'INSERT', 'UPDATE' o 'DELETE', según la acción que se realizó en esa fila. Para obtener más información acerca de los argumentos de esta cláusula, vea [cláusula OUTPUT &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
 OPCIÓN ( \<query_hint > [,.. .n])  
 Especifica que se utilizan las sugerencias del optimizador para personalizar el modo en que el motor de base de datos procesa la instrucción. Para obtener más información, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
 \<merge_matched >  
 Especifica la actualización o eliminación de la acción que se aplica a todas las filas de *target_table* que no coincidan con las filas devueltas por \<table_source > ON \<merge_search_condition >, y que cumplen alguna condición de búsqueda adicional.  
  
 UPDATE configurado \<set_clause >  
 Especifica la lista de nombres de columna o de variable que se van a actualizar en la tabla de destino y los valores con los que se actualizan.  
  
 Para obtener más información acerca de los argumentos de esta cláusula, vea [actualización &#40; Transact-SQL &#41; ](../../t-sql/queries/update-transact-sql.md). No se puede establecer una variable con el mismo valor que una columna.  
  
 DELETE  
 Especifica que las filas que coinciden con filas de *target_table* se eliminan.  
  
 \<merge_not_matched >  
 Especifica los valores que insertar en la tabla de destino.  
  
 (*column_list*)  
 Es una lista de una o varias columnas de la tabla de destino en la que insertar los datos. Las columnas se deben especificar como un nombre de una sola parte o, de lo contrario, se producirá un error en la instrucción MERGE. *column_list* debe incluir entre paréntesis y delimitarse mediante comas.  
  
 VALORES ( *listaValores*)  
 Es una lista separada por comas de constantes, variables o expresiones que devuelve los valores que se insertarán en la tabla de destino. Las expresiones no pueden contener una instrucción EXECUTE.  
  
 DEFAULT VALUES  
 Hace que la fila insertada contenga los valores predeterminados definidos para cada columna.  
  
 Para obtener más información acerca de esta cláusula, vea [INSERT &#40; Transact-SQL &#41; ](../../t-sql/statements/insert-transact-sql.md).  
  
 \<condición de búsqueda >  
 Especifica las condiciones de búsqueda que se utiliza para especificar \<merge_search_condition > o \<clause_search_condition >. Para obtener más información acerca de los argumentos para esta cláusula, vea [condición de búsqueda &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios  
 Al menos se debe especificar una de las tres cláusulas MATCHED, pero se pueden especificar en cualquier orden. Una variable no puede actualizarse más de una vez en la misma cláusula MATCHED.  
  
 Cualquier acción de inserción, actualización o eliminación especificada en la tabla de destino por la instrucción MERGE está limitada por las restricciones definidas en ella, incluidas las restricciones de integridad referencial en cascada. Si IGNORE_DUP_KEY se establece en ON para algún índice único de la tabla de destino, MERGE omite este valor.  
  
 La instrucción MERGE requiere un punto y coma (;) como terminador. Se genera el error 10713 cuando una instrucción MERGE se ejecuta sin el terminador.  
  
 Cuando se utiliza después de la mezcla, [@@ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md) devuelve el número total de filas insertadas, actualizadas y eliminadas al cliente.  
  
 MERGE es una palabra clave totalmente reservada cuando el nivel de compatibilidad de la base de datos se establece en 100 o superior. La instrucción MERGE también está disponible en los niveles de compatibilidad 90 y 100 de la base de datos; sin embargo, la palabra clave no se reserva completamente cuando el nivel de compatibilidad se establece en 90.  
  
 El **mezcla** instrucción no debe usarse al utilizar la replicación de actualización en cola. El **mezcla** y desencadenador de actualización en cola no son compatibles. Reemplace el **mezcla** instrucción con una instrucción insert o una instrucción update.  
  
## <a name="trigger-implementation"></a>Implementación de desencadenadores  
 Para cada acción de inserción, actualización o eliminación especificada en la instrucción MERGE, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] activa los desencadenadores AFTER correspondientes definidos en la tabla de destino, pero no garantiza qué acción activará los desencadenadores primero o último. Los desencadenadores definidos para la misma acción cumplen el orden que especifique. Para obtener más información acerca de cómo establecer el orden de activación de los desencadenadores, vea [especificar primero y último desencadenadores](../../relational-databases/triggers/specify-first-and-last-triggers.md).  
  
 Si la tabla de destino tiene habilitado un desencadenador INSTEAD OF definido en ella para una acción de inserción, actualización o eliminación realizada por una instrucción MERGE, debe tener habilitado un desencadenador INSTEAD OF para todas las acciones especificadas en la instrucción MERGE.  
  
 Si hay INSTEAD OF UPDATE o definir desencadenadores INSTEAD OF DELETE en *target_table*, no se realizan las operaciones update o delete. En su lugar, se activan los desencadenadores y la **insertar** y **eliminado** tablas se rellenan en consecuencia.  
  
 Si hay alguna en lugar de desencadenadores de INSERCIÓN definidos en *target_table*, no se realiza la operación de inserción. En su lugar, se activan los desencadenadores y la **insertar** tabla se rellena en consecuencia.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso SELECT en la tabla de origen y los permisos INSERT, UPDATE o DELETE en la tabla de destino. Para obtener más información, vea la sección de permisos en el [seleccione](../../t-sql/queries/select-transact-sql.md), [insertar](../../t-sql/statements/insert-transact-sql.md), [actualización](../../t-sql/queries/update-transact-sql.md), y [eliminar](../../t-sql/statements/delete-transact-sql.md) temas.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-merge-to-perform-insert-and-update-operations-on-a-table-in-a-single-statement"></a>A. Usar MERGE para realizar operaciones INSERT y UPDATE en una tabla en una sola instrucción  
 Un escenario común es la actualización de una o varias columnas de una tabla si una fila coincidente existe, o la inserción de datos como una fila nueva si no existe ninguna fila coincidente. Normalmente, para hacer esto se pasan los parámetros a un procedimiento almacenado que contiene las instrucciones INSERT y UPDATE adecuadas. Con la instrucción MERGE puede realizar ambas tareas en una sola instrucción. En el ejemplo siguiente se muestra un procedimiento almacenado de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] que contiene una instrucción INSERT y una instrucción UPDATE. A continuación, el procedimiento se modifica para realizar las operaciones equivalentes utilizando una sola instrucción MERGE.  
  
```  
CREATE PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS   
BEGIN  
    SET NOCOUNT ON;  
-- Update the row if it exists.      
    UPDATE Production.UnitMeasure  
SET Name = @Name  
WHERE UnitMeasureCode = @UnitMeasureCode  
-- Insert the row if the UPDATE statement failed.  
IF (@@ROWCOUNT = 0 )  
BEGIN  
    INSERT INTO Production.UnitMeasure (UnitMeasureCode, Name)  
    VALUES (@UnitMeasureCode, @Name)  
END  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Test Value';  
SELECT UnitMeasureCode, Name FROM Production.UnitMeasure  
WHERE UnitMeasureCode = 'ABC';  
GO  
  
-- Rewrite the procedure to perform the same operations using the 
-- MERGE statement.  
-- Create a temporary table to hold the updated or inserted values 
-- from the OUTPUT clause.  
CREATE TABLE #MyTempTable  
    (ExistingCode nchar(3),  
     ExistingName nvarchar(50),  
     ExistingDate datetime,  
     ActionTaken nvarchar(10),  
     NewCode nchar(3),  
     NewName nvarchar(50),  
     NewDate datetime  
    );  
GO  
ALTER PROCEDURE dbo.InsertUnitMeasure  
    @UnitMeasureCode nchar(3),  
    @Name nvarchar(25)  
AS   
BEGIN  
    SET NOCOUNT ON;  
  
    MERGE Production.UnitMeasure AS target  
    USING (SELECT @UnitMeasureCode, @Name) AS source (UnitMeasureCode, Name)  
    ON (target.UnitMeasureCode = source.UnitMeasureCode)  
    WHEN MATCHED THEN   
        UPDATE SET Name = source.Name  
WHEN NOT MATCHED THEN  
    INSERT (UnitMeasureCode, Name)  
    VALUES (source.UnitMeasureCode, source.Name)  
    OUTPUT deleted.*, $action, inserted.* INTO #MyTempTable;  
END;  
GO  
-- Test the procedure and return the results.  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'New Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'XYZ', @Name = 'Test Value';  
EXEC InsertUnitMeasure @UnitMeasureCode = 'ABC', @Name = 'Another Test Value';  
  
SELECT * FROM #MyTempTable;  
-- Cleanup   
DELETE FROM Production.UnitMeasure WHERE UnitMeasureCode IN ('ABC','XYZ');  
DROP TABLE #MyTempTable;  
GO  
```  
  
### <a name="b-using-merge-to-perform-update-and-delete-operations-on-a-table-in-a-single-statement"></a>B. Usar MERGE para realizar operaciones UPDATE y DELETE en una tabla en una sola instrucción  
 En el siguiente ejemplo se usa MERGE para actualizar diariamente la tabla `ProductInventory` de la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], en función de los pedidos procesados en la tabla `SalesOrderDetail`. La columna `Quantity` de la tabla `ProductInventory` se actualiza restando el número de pedidos realizados cada día para cada producto de la tabla `SalesOrderDetail`. Si el número de pedidos de un producto baja el nivel de inventario del mismo hasta 0 o un valor menor, la fila correspondiente a ese producto se elimina de la tabla `ProductInventory`.  
  
```  
CREATE PROCEDURE Production.usp_UpdateInventory  
    @OrderDate datetime  
AS  
MERGE Production.ProductInventory AS target  
USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
    JOIN Sales.SalesOrderHeader AS soh  
    ON sod.SalesOrderID = soh.SalesOrderID  
    AND soh.OrderDate = @OrderDate  
    GROUP BY ProductID) AS source (ProductID, OrderQty)  
ON (target.ProductID = source.ProductID)  
WHEN MATCHED AND target.Quantity - source.OrderQty <= 0  
    THEN DELETE  
WHEN MATCHED   
    THEN UPDATE SET target.Quantity = target.Quantity - source.OrderQty,   
                    target.ModifiedDate = GETDATE()  
OUTPUT $action, Inserted.ProductID, Inserted.Quantity, 
    Inserted.ModifiedDate, Deleted.ProductID,  
    Deleted.Quantity, Deleted.ModifiedDate;  
GO  
  
EXECUTE Production.usp_UpdateInventory '20030501'  
```  
  
### <a name="c-using-merge-to-perform-update-and-insert-operations-on-a-target-table-by-using-a-derived-source-table"></a>C. Usar MERGE para realizar operaciones INSERT y UPDATE en una tabla de destino mediante una tabla de origen derivada  
 En el ejemplo siguiente se usa MERGE para modificar la tabla `SalesReason` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], actualizando o insertando las filas. Cuando el valor de `NewName` de la tabla de origen coincide con un valor de la columna `Name` de la tabla de destino, (`SalesReason`), la columna `ReasonType` se actualiza en la tabla de destino. Cuando el valor de `NewName` no coincide, la fila del origen se inserta en la tabla de destino. La tabla de origen es una tabla derivada que usa la característica de constructor con valores de tabla de [!INCLUDE[tsql](../../includes/tsql-md.md)] para especificar varias filas en la tabla de origen. Para obtener más información acerca de cómo utilizar el constructor con valores de tabla en una tabla derivada, vea [Constructor con valores de tabla &#40; Transact-SQL &#41; ](../../t-sql/queries/table-value-constructor-transact-sql.md). El ejemplo también muestra cómo almacenar los resultados de la cláusula OUTPUT en una variable de tabla y, a continuación, resumir los resultados de la instrucción MERGE realizando una sencilla operación SELECT que devuelve el recuento de las filas insertadas y actualizadas.  
  
```  
-- Create a temporary table variable to hold the output actions.  
DECLARE @SummaryOfChanges TABLE(Change VARCHAR(20));  
  
MERGE INTO Sales.SalesReason AS Target  
USING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), 
              ('Internet', 'Promotion'))  
       AS Source (NewName, NewReasonType)  
ON Target.Name = Source.NewName  
WHEN MATCHED THEN  
UPDATE SET ReasonType = Source.NewReasonType  
WHEN NOT MATCHED BY TARGET THEN  
INSERT (Name, ReasonType) VALUES (NewName, NewReasonType)  
OUTPUT $action INTO @SummaryOfChanges;  
  
-- Query the results of the table variable.  
SELECT Change, COUNT(*) AS CountPerChange  
FROM @SummaryOfChanges  
GROUP BY Change;  
```  
  
### <a name="d-inserting-the-results-of-the-merge-statement-into-another-table"></a>D. Insertar los resultados de la instrucción MERGE en otra tabla  
 En el ejemplo siguiente se capturan los datos devueltos por la cláusula OUTPUT de una instrucción MERGE y se insertan en otra tabla. La instrucción MERGE actualiza diariamente la columna `Quantity` de la tabla `ProductInventory` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], en función de los pedidos procesados en la tabla `SalesOrderDetail`. En el ejemplo se capturan las filas actualizadas y se insertan en otra tabla que se usa para realizar el seguimiento de los cambios del inventario.  
  
```  
CREATE TABLE Production.UpdatedInventory  
    (ProductID INT NOT NULL, LocationID int, NewQty int, PreviousQty int,  
     CONSTRAINT PK_Inventory PRIMARY KEY CLUSTERED (ProductID, LocationID));  
GO  
INSERT INTO Production.UpdatedInventory  
SELECT ProductID, LocationID, NewQty, PreviousQty   
FROM  
(    MERGE Production.ProductInventory AS pi  
     USING (SELECT ProductID, SUM(OrderQty)   
            FROM Sales.SalesOrderDetail AS sod  
            JOIN Sales.SalesOrderHeader AS soh  
            ON sod.SalesOrderID = soh.SalesOrderID  
            AND soh.OrderDate BETWEEN '20030701' AND '20030731'  
            GROUP BY ProductID) AS src (ProductID, OrderQty)  
     ON pi.ProductID = src.ProductID  
    WHEN MATCHED AND pi.Quantity - src.OrderQty >= 0   
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0   
        THEN DELETE  
    OUTPUT $action, Inserted.ProductID, Inserted.LocationID, 
        Inserted.Quantity AS NewQty, Deleted.Quantity AS PreviousQty)  
 AS Changes (Action, ProductID, LocationID, NewQty, PreviousQty) 
 WHERE Action = 'UPDATE';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [Cláusula OUTPUT &#40; Transact-SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md)   
 [MERGE en paquetes Integration Services](../../integration-services/control-flow/merge-in-integration-services-packages.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [Constructor con valores de tabla &#40; Transact-SQL &#41;](../../t-sql/queries/table-value-constructor-transact-sql.md)  
  
  


