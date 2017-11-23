---
title: SELECT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SELECT_TSQL
- SELECT
dev_langs: TSQL
helpviewer_keywords:
- retrieving rows
- SELECT statement [SQL Server]
- SELECT statement [SQL Server], about SELECT statement
- row retrieval [SQL Server], SELECT statement
- DML [SQL Server], SELECT statement
- data manipulation language [SQL Server], SELECT statement
- row retrieval [SQL Server]
- queries [SQL Server], results
ms.assetid: dc85caea-54d1-49af-b166-f3aa2f3a93d0
caps.latest.revision: "51"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 012853c97e01250bf5aee62d95ae7971549f5094
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="select-transact-sql"></a>SELECT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Recupera filas de la base de datos y habilita la selección de una o varias filas o columnas de una o varias tablas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La sintaxis completa de la instrucción SELECT es compleja, aunque las cláusulas principales se pueden resumir del modo siguiente:  
  
[Con {[XMLNAMESPACES], [ \<common_table_expression >]}]
  
 Seleccione *select_list* [INTO *new_table* ]  
  
 [Desde *table_source* ] [donde *search_condition* ]  
  
 [GROUP BY *group_by_expression* ]  
  
 [Tener *search_condition* ]  
  
 [ORDER BY *expresiónOrden* [ASC | DESC]]  
  
 La UNION, EXCEPT y operadores INTERSECT se pueden utilizar entre consultas para combinar o comparar sus resultados en un conjunto de resultados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
<SELECT statement> ::=    
    [ WITH { [ XMLNAMESPACES ,] [ <common_table_expression> [,...n] ] } ]  
    <query_expression>   
    [ ORDER BY { order_by_expression | column_position [ ASC | DESC ] }   
  [ ,...n ] ]   
    [ <FOR Clause>]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]   
<query_expression> ::=   
    { <query_specification> | ( <query_expression> ) }   
    [  { UNION [ ALL ] | EXCEPT | INTERSECT }  
        <query_specification> | ( <query_expression> ) [...n ] ]   
<query_specification> ::=   
SELECT [ ALL | DISTINCT ]   
    [TOP ( expression ) [PERCENT] [ WITH TIES ] ]   
    < select_list >   
    [ INTO new_table ]   
    [ FROM { <table_source> } [ ,...n ] ]   
    [ WHERE <search_condition> ]   
    [ <GROUP BY> ]   
    [ HAVING < search_condition > ]   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
[ WITH <common_table_expression> [ ,...n ] ]  
SELECT <select_criteria>  
[;]  
  
<select_criteria> ::=  
    [ TOP ( top_expression ) ]   
    [ ALL | DISTINCT ]   
    { * | column_name | expression } [ ,...n ]   
    [ FROM { table_source } [ ,...n ] ]  
    [ WHERE <search_condition> ]   
    [ GROUP BY <group_by_clause> ]   
    [ HAVING <search_condition> ]   
    [ ORDER BY <order_by_expression> ]  
    [ OPTION ( <query_option> [ ,...n ] ) ]  
  
```  
  
## <a name="remarks"></a>Comentarios  
 Debido a la complejidad de la instrucción SELECT, se muestran elementos y argumentos detallados de la sintaxis de cada cláusula:  
  
|||  
|-|-|  
|[WITH XMLNAMESPACES](../../t-sql/xml/with-xmlnamespaces.md)<br /><br /> [WITH common_table_expression](../../t-sql/queries/with-common-table-expression-transact-sql.md)|[TENER](../../t-sql/queries/select-having-transact-sql.md)|  
|[Cláusula SELECT](../../t-sql/queries/select-clause-transact-sql.md)|[UNIÓN](../../t-sql/language-elements/set-operators-union-transact-sql.md)|  
|[Cláusula INTO](../../t-sql/queries/select-into-clause-transact-sql.md)|[EXCEPT e INTERSECT](../../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)|  
|[FROM](../../t-sql/queries/from-transact-sql.md)|[ORDENAR POR](../../t-sql/queries/select-order-by-clause-transact-sql.md)|  
|[WHERE](../../t-sql/queries/where-transact-sql.md)|[Cláusula FOR](../../t-sql/queries/select-for-clause-transact-sql.md)|  
|[AGRUPAR POR](../../t-sql/queries/select-group-by-transact-sql.md)|[Cláusula OPTION](../../t-sql/queries/option-clause-transact-sql.md)|  
  
 El orden de las cláusulas en la instrucción SELECT es importante. Se puede omitir cualquiera de las cláusulas opcionales pero, cuando se utilizan, deben aparecer en el orden apropiado.  
  
 Las instrucciones SELECT se permiten en las funciones definidas por el usuario solo si las listas de selección de estas instrucciones contienen expresiones que asignan valores a variables locales de las funciones.  
  
 Un nombre de cuatro partes generado con la función OPENDATASOURCE como la parte del nombre de servidor se puede usar como origen de tabla siempre que sea un nombre de tabla puede aparecer en una instrucción SELECT. No se puede especificar un nombre de cuatro partes para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Existen algunas restricciones sintácticas en las instrucciones SELECT relacionadas con las tablas remotas.  
  
## <a name="logical-processing-order-of-the-select-statement"></a>Orden de procesamiento lógico de la instrucción SELECT  
 Los pasos siguientes muestran el orden de procesamiento lógico, u orden de enlaces, de una instrucción SELECT. Este orden determina cuándo los objetos definidos en un paso están disponibles para las cláusulas en pasos posteriores. Por ejemplo, si el procesador de consultas puede enlazar (obtener acceso) a las tablas o las vistas definidas en la cláusula FROM, estos objetos y sus columnas están disponibles para todos los pasos siguientes. Por el contrario, dado que la cláusula SELECT es el paso 8, las cláusulas anteriores no pueden hacer referencia a los alias de columna o columnas derivadas definidas en esa cláusula. Sin embargo, las cláusulas siguientes, tales como la cláusula ORDER BY, sí pueden hacer referencia. La ejecución física real de la instrucción viene determinada por el procesador de consultas y el orden puede variar en esta lista.  
  
1.  FROM  
2.  ON  
3.  JOIN  
4.  WHERE  
5.  GROUP BY  
6.  WITH CUBE o WITH ROLLUP  
7.  HAVING  
8.  SELECT  
9. DISTINCT  
10. ORDER BY  
11. ARRIBA  

> [!WARNING]
> La secuencia anterior es generalmente true. Sin embargo, hay casos poco comunes que puede diferir la secuencia.
>
> Por ejemplo, suponga que tiene un índice agrupado en una vista, la vista excluye algunas filas de la tabla y la lista de columnas SELECT de la vista utiliza una conversión que cambia un tipo de datos de *varchar* a *entero*. En esta situación, puede ejecutar la función CONVERT antes de la cláusula WHERE se ejecuta. De hecho raro. Suele haber una manera de modificar la vista para evitar la secuencia diferente, si es importante en su caso. 

## <a name="permissions"></a>Permissions  
 La selección de datos necesita el permiso **SELECT** en la tabla o en la vista, que se puede heredar de un ámbito superior como el permiso **SELECT** en el esquema o el permiso **CONTROL** en la tabla. O debe pertenecer a la **db_datareader** o **db_owner** funciones fijas de base de datos, o la **sysadmin** rol fijo de servidor. Crear una nueva tabla mediante **SELECTINTO** también necesita tanto el **CREATETABLE** permiso y el **ALTERSCHEMA** permiso en el esquema al que pertenece la nueva tabla.  
  
## <a name="examples"></a>Ejemplos:   
Los ejemplos siguientes usan la base de datos [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].
  
### <a name="a-using-select-to-retrieve-rows-and-columns"></a>A. Usar SELECT para recuperar filas y columnas  
 En esta sección se muestra tres ejemplos de código. Este primer ejemplo de código devuelve todas las filas (no se especifica ninguna cláusula WHERE) y todas las columnas (mediante el `*`) desde el `DimEmployee` tabla.  
  
```sql  
SELECT *  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
 El siguiente ejemplo utilizando el alias de tabla para lograr el mismo resultado.  
  
```sql  
SELECT e.*  
FROM DimEmployee AS e  
ORDER BY LastName;  
```  
  
 Este ejemplo devuelve todas las filas (no se especifica ninguna cláusula WHERE) y un subconjunto de las columnas (`FirstName`, `LastName`, `StartDate`) desde el `DimEmployee` tabla el `AdventureWorksPDW2012` base de datos. El tercer encabezado de columna ha cambiado a `FirstDay`.  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
ORDER BY LastName;  
```  
  
 Este ejemplo devuelve solo las filas de `DimEmployee` que tienen un `EndDate` que no sea NULL y un `MaritalStatus` de ' m ' (casado).  
  
```sql  
SELECT FirstName, LastName, StartDate AS FirstDay  
FROM DimEmployee   
WHERE EndDate IS NOT NULL   
AND MaritalStatus = 'M'  
ORDER BY LastName;  
```  
  
### <a name="b-using-select-with-column-headings-and-calculations"></a>B. Usar SELECT con encabezados de columna y cálculos  
 El ejemplo siguiente devuelve todas las filas de la `DimEmployee` de tabla y calcula el sueldo bruto de cada empleado en función de sus `BaseRate` y una semana laboral de 40 horas.  
  
```sql  
SELECT FirstName, LastName, BaseRate, BaseRate * 40 AS GrossPay  
FROM DimEmployee  
ORDER BY LastName;  
```  
  
### <a name="c-using-distinct-with-select"></a>C. Usar DISTINCT con SELECT  
 En el ejemplo siguiente se utiliza `DISTINCT` para generar una lista de todos los títulos únicos en el `DimEmployee` tabla.  
  
```sql  
SELECT DISTINCT Title  
FROM DimEmployee  
ORDER BY Title;  
```  
  
### <a name="d-using-group-by"></a>D. Usar GROUP BY  
 En el ejemplo siguiente se busca la cantidad total de todas las ventas de cada día.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
 Causa de la `GROUP BY` cláusula, se devuelve una única fila que contiene la suma de todas las ventas para cada día.  
  
### <a name="e-using-group-by-with-multiple-groups"></a>E. Usar GROUP BY con varios grupos  
 En el ejemplo siguiente se busca el precio medio y la suma de ventas por Internet para cada día, agrupadas por fecha de pedido y la clave de promoción.  
  
```sql  

SELECT OrderDateKey, PromotionKey, AVG(SalesAmount) AS AvgSales, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey, PromotionKey  
ORDER BY OrderDateKey;   
```  
  
### <a name="f-using-group-by-and-where"></a>F. Usar GROUP BY y WHERE  
 En el ejemplo siguiente se coloca los resultados en grupos después de recuperar únicamente las filas con las fechas de pedidos a más tardar el 1 de agosto de 2002.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
WHERE OrderDateKey > '20020801'  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="g-using-group-by-with-an-expression"></a>G. Usar GROUP BY con una expresión  
 En este ejemplo se agrupa por una expresión. Puede agrupar por una expresión si ésta no incluye funciones de agregado.  
  
```sql  
SELECT SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY (OrderDateKey * 10);  
```  
  
### <a name="h-using-group-by-with-order-by"></a>H. Usar GROUP BY con ORDER BY  
 En el ejemplo siguiente se busca la suma de las ventas por día y los pedidos por día.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-the-having-clause"></a>I. Usar la cláusula HAVING  
 Esta consulta utiliza la `HAVING` cláusula para restringir los resultados.  
  
```sql  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales  
FROM FactInternetSales  
GROUP BY OrderDateKey  
HAVING OrderDateKey > 20010000  
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos SELECT &#40; Transact-SQL &#41;](../../t-sql/queries/select-examples-transact-sql.md)  
 [Sugerencias de &#40; Transact-SQL &#41;](../../t-sql/queries/hints-transact-sql.md)
  

