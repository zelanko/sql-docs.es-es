---
title: Agrupar por (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
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
- GROUP
- CUBE
- ROLLUP
- GROUPING_SETS_TSQL
- GROUP BY
- GROUPING SETS
- GROUP_BY_TSQL
- GROUP_TSQL
- CUBE_TSQL
- ROLLUP_TSQL
dev_langs: TSQL
helpviewer_keywords:
- GROUP BY clause, about GROUP BY clause
- dividing tables into groups
- GROUPING SETS
- GROUP BY clause
- table groups [SQL Server]
- groups [SQL Server], tables divided into groups
- summary values [SQL Server]
ms.assetid: 40075914-6385-4692-b4a5-62fe44ae6cb6
caps.latest.revision: "80"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 49b572a8ce91287faa4c162efa8de8e7f0113235
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="select---group-by--transact-sql"></a>Seleccione - GROUP BY de Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Una cláusula de la instrucción SELECT que divide el resultado de la consulta en grupos de filas, normalmente con el fin de realizar una o varias agregaciones en cada grupo. La instrucción SELECT devuelve una fila por cada grupo.  
  
## <a name="syntax"></a>Sintaxis  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
```  
-- Syntax for SQL Server and Azure SQL Database   
-- ISO-Compliant Syntax  
  
GROUP BY {
      column-expression  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
    | GROUPING SETS ( <grouping_set> [ ,...n ]  )  
    | () --calculates the grand total 
} [ ,...n ] 
 
<group_by_expression> ::=  
      column-expression  
    | ( column-expression [ ,...n ] )    
   
<grouping_set> ::=  
      () --calculates the grand total  
    | <grouping_set_item>  
    | ( <grouping_set_item> [ ,...n ] )  
  
<grouping_set_item> ::=  
      <group_by_expression>  
    | ROLLUP ( <group_by_expression> [ ,...n ] )  
    | CUBE ( <group_by_expression> [ ,...n ] )  
  

-- For backward compatibility only.
-- Non-ISO-Compliant Syntax for SQL Server and Azure SQL Database 
  
GROUP BY 
      [ ALL ] column-expression [ ,...n ] 
    | column-expression [ ,...n ] [ WITH { CUBE | ROLLUP } ]   

```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
GROUP BY {
      column-name [ WITH (DISTRIBUTED_AGG) ]  
    | column-expression
} [ ,...n ]

```  
  
## <a name="arguments"></a>Argumentos 
 
### <a name="column-expression"></a>*expresión de columna*  
Especifica una columna o un cálculo de agregado no en una columna. Esta columna puede pertenecer a una tabla, una tabla derivada o una vista. La columna debe aparecer en la cláusula FROM de la instrucción SELECT, pero no es necesaria que aparezcan en la lista de selección. 

Para las expresiones válidas, vea [expresión](~/t-sql/language-elements/expressions-transact-sql.md).    

La columna debe aparecer en la cláusula FROM de la instrucción SELECT, pero no es necesaria que aparezcan en la lista de selección. Sin embargo, cada tabla o vista de columna en una expresión no agregada en el \<seleccione > lista debe incluirse en la lista GROUP BY:  
  
Están permitidas las siguientes instrucciones:  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA, ColumnB;  
    SELECT ColumnA + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + ColumnB + constant FROM T GROUP BY ColumnA, ColumnB;  
    ```  
  
No están permitidas las siguientes instrucciones:  
  
    ```  
    SELECT ColumnA, ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    SELECT ColumnA + constant + ColumnB FROM T GROUP BY ColumnA + ColumnB;  
    ```  
La expresión de columna no puede contener:

- Un alias de columna que se define en la lista de selección. Puede usar un alias de columna para una tabla derivada que se define en la cláusula FROM.
- Una columna de tipo **texto**, **ntext**, o **imagen**. Sin embargo, puede usar una columna de text, ntext o image como argumento a una función que devuelve un valor de un tipo de datos válido. Por ejemplo, puede usar la expresión SUBSTRING() y CAST(). Esto también se aplica a las expresiones de la cláusula HAVING.
- métodos de tipo de datos XML. Puede incluir una función definida por el usuario que utiliza los métodos de tipo de datos xml. Puede incluir una columna calculada que usa los métodos de tipo de datos xml. 
- Una subconsulta. Se devuelve el error 144. 
- Una columna de una vista indizada. 
 
### <a name="group-by-column-expression--n-"></a>GROUP BY *expresión de columna* [,.. .n] 

Agrupa los resultados de la instrucción SELECT según los valores en una lista de una o varias expresiones de columna. 

Por ejemplo, esta consulta crea una tabla de ventas con las columnas de país, región y ventas. Inserta cuatro filas y dos de las filas tienen valores coincidentes para el país y región.  

```
CREATE TABLE Sales ( Country varchar(50), Region varchar(50), Sales int );

INSERT INTO sales VALUES (N'Canada', N'Alberta', 100);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 200);
INSERT INTO sales VALUES (N'Canada', N'British Columbia', 300);
INSERT INTO sales VALUES (N'United States', N'Montana', 100);
```
La tabla de ventas contiene estas filas:

| País | Region | Sales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | Columbia Británica | 200 |
| Canada | Columbia Británica | 300 |
| United States | Montana | 100 |

La siguiente consulta agrupa país y región y devuelve la suma de agregados para cada combinación de valores.  
 
``` 
SELECT Country, Region, SUM(sales) AS TotalSales
FROM Sales
GROUP BY Country, Region;
```
El resultado de la consulta tiene 3 filas puesto que hay 3 combinaciones de valores de país y región. El valor de TotalSales para Canadá y Columbia Británica es la suma de dos filas. 

| País | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| Canada | Columbia Británica | 500 |
| United States | Montana | 100 |

### <a name="group-by-rollup"></a>AGRUPAR POR EL PAQUETE ACUMULATIVO DE ACTUALIZACIONES

Crea un grupo para cada combinación de expresiones de columna. Además, "acumulan" los resultados en subtotales y totales generales. Para ello, mueve de derecha a izquierda reduciendo así el número de expresiones de columna en la que crea grupos y la aggregation(s). 

El orden de las columnas afecta a la salida del paquete acumulativo de actualizaciones y puede afectar al número de filas del conjunto de resultados.  

Por ejemplo, `GROUP BY ROLLUP (col1, col2, col3, col4)` crea grupos para cada combinación de expresiones de columna en las listas siguientes.  

- col1, col2, col3, col4 
- col1, col2, col3, NULL
- col1, col2, NULL, NULL
- col1, NULL, NULL, NULL
- NULL, NULL, NULL, NULL--este es el total general

Con la tabla del ejemplo anterior, este código ejecuta una operación GROUP BY ROLLUP en lugar de una cláusula GROUP BY simple.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region);
```

El resultado de la consulta tiene las mismas agregaciones como simple GROUP BY sin el paquete acumulativo de actualizaciones. Además, crea subtotales para cada valor de país. Por último, le ofrece un total general para todas las filas. El resultado tiene el siguiente aspecto:

| País | Region | TotalSales |
| :------ | :----- | ---------: |
| Canada | Alberta | 100 |
| Canada | Columbia Británica | 500 |
| Canada | NULL | 600 |
| United States | Montana | 100 |
| United States | NULL | 100 |
| NULL | NULL | 700 |

### <a name="group-by-cube--"></a>AGRUPAR POR () DE CUBO  

GROUP BY CUBE crea grupos para todas las posibles combinaciones de columnas. Para GROUP BY CUBE (a, b) los resultados tiene grupos de valores únicos (a, b), (NULL, b), (a, NULL) y (NULL, NULL).

Con la tabla de los ejemplos anteriores, este código ejecuta una operación GROUP BY CUBE en país y región. 

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region);
```

El resultado de la consulta tiene grupos de valores únicos de (país, región), (NULL, región), (país, NULL) y (NULL, NULL). El resultado tendrá este aspecto:

| País | Region | TotalSales |
|---------|--------|-------|
| Canada | Alberta | 100 |
| NULL | Alberta | 100 |
| Canada | Columbia Británica | 500 |
| NULL | Columbia Británica | 500 |
| United States | Montana | 100 |
| NULL | Montana | 100 |
| NULL | NULL | 700
| Canada | NULL | 600 |
| United States | NULL | 100 |
   
 ### <a name="group-by-grouping-sets--"></a>AGRUPAR POR () DE CONJUNTOS DE AGRUPACIÓN  
 
La opción de GROUPING SETS le ofrece la capacidad de combinar varias cláusulas GROUP BY en una cláusula GROUP BY. Los resultados son equivalentes a usar la instrucción UNION ALL en los grupos especificados. 

Por ejemplo, `GROUP BY ROLLUP (Country, Region)` y `GROUP BY GROUPING SETS ( ROLLUP (Country, Region) )` devuelven los mismos resultados. 

Cuando los conjuntos de agrupación tiene dos o más elementos, los resultados son la unión de los elementos. Este ejemplo devuelve la unión de los resultados ROLLUP y CUBE para país y región.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( ROLLUP (Country, Region), CUBE (Country, Region) );
```

Los resultados son los mismos que la consulta que devuelve la unión de las dos instrucciones GROUP BY.

```
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY ROLLUP (Country, Region)
UNION ALL
SELECT Country, Region, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY CUBE (Country, Region)
;
```

SQL no Consolide grupos duplicados generados para obtener una lista GROUPING SETS. Por ejemplo, en `GROUP BY ( (), CUBE (Country, Region) )`, ambos elementos devolver una fila para el total general y ambas filas se mostrarán en los resultados. 

 ### <a name="group-by-"></a>GROUP BY ()  
Especifica el grupo vacío que genera el total general. Esto resulta útil como uno de los elementos de un conjunto de agrupación. Por ejemplo, esta instrucción da como resultado el total de ventas de cada país y, a continuación, proporciona el total general para todos los países.

```
SELECT Country, SUM(Sales) AS TotalSales
FROM Sales
GROUP BY GROUPING SETS ( Country, () );
```

### <a name="group-by--all--column-expression--n-"></a>GROUP BY [ALL]-expresión de columna [,.. .n] 

Se aplica a: SQL Server y base de datos SQL Azure

Nota: Esta sintaxis se proporciona por razones de compatibilidad. Se quitará en una versión futura. Evite utilizar esta sintaxis en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta sintaxis.

Especifica que se incluyen todos los grupos en los resultados independientemente de que cumplan los criterios de búsqueda en la cláusula WHERE. Grupos que no cumplen los criterios de búsqueda tienen el valor NULL para la agregación. 

AGRUPAR POR TODOS:
- No se admite en las consultas que tienen acceso a tablas remotas si también hay una cláusula WHERE en la consulta.
- Se producirá un error en las columnas que tienen el atributo FILESTREAM.
  
### <a name="with-distributedagg"></a>CON (DISTRIBUTED_AGG)
Se aplica a: almacenamiento de datos SQL Azure y almacenamiento de datos paralelos

La sugerencia de consulta DISTRIBUTED_AGG obliga al sistema de procesamiento paralelo masivo (MPP) para redistribuir una tabla en una columna específica antes de realizar una agregación. Solo una columna en la cláusula GROUP BY puede tener una sugerencia de consulta DISTRIBUTED_AGG. Una vez finalizada la consulta, se quita la tabla redistribuida. No se cambia la tabla original.  

Nota: La sugerencia de consulta DISTRIBUTED_AGG se proporciona para ofrecer compatibilidad con versiones anteriores de almacenamiento de datos paralelo y no mejorará el rendimiento para la mayoría de las consultas. De forma predeterminada, MPP redistribuye ya los datos según sea necesario para mejorar el rendimiento de las agregaciones. 
  
## <a name="general-remarks"></a>Notas generales

### <a name="how-group-by-interacts-with-the-select-statement"></a>Cómo agrupar por interactúa con la instrucción SELECT
Lista de selección:
- Agregados vectoriales. Si se incluyen funciones de agregado en la lista SELECT, GROUP BY calcula un valor de resumen para cada grupo. Se conocen como agregados vectoriales. 
- Agregados DISTINCT. Los agregados AVG (DISTINCT *column_name*), COUNT (DISTINCT *column_name*) y SUM (DISTINCT *column_name*) son compatibles con ROLLUP, CUBE y GROUPING SETS.
  
Cláusula WHERE:
- SQL quita las filas que no cumplen las condiciones de la cláusula WHERE antes de realiza cualquier operación de agrupación.  
  
Cláusula HAVING:
- SQL utiliza el tener cláusula para filtrar los grupos del conjunto de resultados. 
  
Cláusula ORDER BY:
- En su lugar, use la cláusula ORDER BY para ordenarlo. La cláusula GROUP BY no ordena el conjunto de resultados. 
  
Valores NULL:
- Si una columna de agrupamiento contiene valores NULL, todos los valores NULL se consideran iguales y que se recopilan en un único grupo.   
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones

Se aplica a: SQL Server (a partir de 2008) y almacenamiento de datos de SQL Azure

### <a name="maximum-capacity"></a>Capacidad máxima

Para una cláusula GROUP BY que utiliza ROLLUP, CUBE o GROUPING SETS, el número máximo de expresiones es 32. El número máximo de grupos es 4.096 (2<sup>12</sup>). Los ejemplos siguientes producirá un error porque la cláusula GROUP BY tiene más de 4096 grupos.  
 
-   En el ejemplo siguiente se genera 4.097 (2<sup>12</sup> + 1) conjuntos de agrupamiento y se producirá un error.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), b )  
    ```  
  
-   En el ejemplo siguiente se genera 4.097 (2<sup>12</sup> + 1) agrupa y se producirá un error. Los conjuntos de agrupación `CUBE ()` y `()` generan una fila de total general y los conjuntos de agrupación duplicados no se eliminan.  
  
    ```  
    GROUP BY GROUPING SETS( CUBE(a1, ..., a12), ())  
    ```  

-   Este ejemplo utiliza la sintaxis compatible con versiones anteriores. Genera 8192 (2<sup>13</sup>) conjuntos de agrupamiento y se producirá un error.  
  
    ```  
    GROUP BY CUBE (a1, ..., a13)   
    GROUP BY a1, ..., a13 WITH CUBE   
    ```    
    Compatible con versiones anteriores con las cláusulas GROUP BY que no contengan CUBE o ROLLUP, el número de grupo de elementos está limitado por el grupo por tamaño de las columnas, las columnas de agregado y los valores de agregado implicados en la consulta. Este límite procede del límite de 8.060 bytes de la tabla de trabajo intermedia que se necesita para contener los resultados intermedios de la consulta. Se permite un máximo de 12 expresiones de agrupamiento cuando se especifica CUBE o ROLLUP.

### <a name="support-for-iso-and-ansi-sql-2006-group-by-features"></a>Compatibilidad con las características GROUP BY de ISO y ANSI SQL-2006

La cláusula GROUP BY es compatible con todas las características GROUP BY que se incluyen en el estándar SQL-2006 con las siguientes excepciones de sintaxis:  
  
-   Los conjuntos de agrupamiento no se pueden usar en la cláusula GROUP BY a menos que formen parte de una lista GROUPING SETS explícita. Por ejemplo, `GROUP BY Column1, (Column2, ...ColumnN`) se admite en el estándar, pero no en Transact-SQL.  Transact-SQL admite `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))` y `GROUP BY Column1, Column2, ... ColumnN`, que son semánticamente equivalentes. Éstos son equivalentes semánticamente al ejemplo de `GROUP BY` anterior. Esto es para evitar la posibilidad de que `GROUP BY Column1, (Column2, ...ColumnN`) se pueda malinterpretar como `GROUP BY C1, GROUPING SETS ((Column2, ...ColumnN))`, que no son semánticamente equivalentes.  
  
-   No se pueden usar conjuntos de agrupamiento dentro de conjuntos de agrupamiento. Por ejemplo, `GROUP BY GROUPING SETS (A1, A2,…An, GROUPING SETS (C1, C2, ...Cn))` se permite en el estándar SQL-2006 pero no en Transact-SQL. Transact-SQL permite `GROUP BY GROUPING SETS( A1, A2,...An, C1, C2, ...Cn )` o `GROUP BY GROUPING SETS( (A1), (A2), ... (An), (C1), (C2), ... (Cn) )`, que son semánticamente equivalentes para el primer ejemplo de GROUP BY y tienen una sintaxis más clara.  
  
-   GROUP BY [ALL/DISTINCT] solo se permite en una cláusula GROUP BY simple que contiene expresiones de columna. No se permite con las construcciones GROUPING SETS, ROLLUP, CUBE, WITH CUBE o WITH ROLLUP. ALL es el valor predeterminado y es implícito. Solo se permite en la sintaxis compatible con versiones anteriores.
  
### <a name="comparison-of-supported-group-by-features"></a>Comparación de las características GROUP BY compatibles  
 En la tabla siguiente describe las características GROUP BY que son compatibles en función de las versiones de SQL y el nivel de compatibilidad de base de datos.  
  
|Característica|SQL Server Integration Services|Nivel de compatibilidad 100 o superior con SQL Server|SQL Server 2008 o posterior con el nivel de compatibilidad 90.|  
|-------------|-------------------------------------|--------------------------------------------------|-----------------------------------------------------------|  
|Agregados DISTINCT|No se admite en WITH CUBE ni en WITH ROLLUP.|Se admite en WITH CUBE, WITH ROLLUP, GROUPING SETS, CUBE o ROLLUP.|Igual que el nivel de compatibilidad 100.|  
|Función definida por el usuario con un nombre CUBE o ROLLUP en la cláusula GROUP BY|Función definida por el usuario **dbo.cube (***arg1***,***.. .argN***)** o  **dbo.Rollup (***arg1***,**... *argN***)** en GROUP BY se permite la cláusula.<br /><br /> Por ejemplo, `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|Función definida por el usuario **dbo.cube (***arg1***,**.. .argN**)** o **dbo.rollup (**arg1**,***.. .argN***)** en GROUP BY no se permite la cláusula.<br /><br /> Por ejemplo, `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`<br /><br /> Se devuelve el siguiente mensaje de error: "sintaxis incorrecta cerca de la palabra clave"cubo"' &#124;' paquete acumulativo de actualizaciones '. "<br /><br /> Para evitar este problema, reemplace `dbo.cube` por `[dbo].[cube]` o `dbo.rollup` por `[dbo].[rollup]`.<br /><br /> Se permite en el ejemplo siguiente:`SELECT SUM (x) FROM T  GROUP BY [dbo].[cube](y);`|Función definida por el usuario **dbo.cube (***arg1***,***.. .argN*) o **dbo.rollup (** *arg1***,***.. .argN***)** en GROUP BY se permite la cláusula<br /><br /> Por ejemplo, `SELECT SUM (x) FROM T  GROUP BY dbo.cube(y);`|  
|GROUPING SETS|No compatible|Admitida|Admitida|  
|CUBE|No compatible|Admitida|No compatible|  
|ROLLUP|No compatible|Admitida|No compatible|  
|Total general, como GROUP BY ()|No compatible|Admitida|Admitida|  
|GROUPING_ID, función|No compatible|Admitida|Admitida|  
|GROUPING, función|Admitida|Admitida|Admitida|  
|WITH CUBE|Admitida|Admitida|Admitida|  
|WITH ROLLUP|Admitida|Admitida|Admitida|  
|Eliminación de grupos duplicados de WITH CUBE o WITH ROLLUP|Admitida|Admitida|Admitida| 
 
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-use-a-simple-group-by-clause"></a>A. Usar una cláusula GROUP BY simple  
 En el ejemplo siguiente se recupera el total de cada `SalesOrderID` de la tabla `SalesOrderDetail`. Este ejemplo utiliza AdventureWorks.  
  
```  
SELECT SalesOrderID, SUM(LineTotal) AS SubTotal  
FROM Sales.SalesOrderDetail AS sod  
GROUP BY SalesOrderID  
ORDER BY SalesOrderID;  
```  
  
### <a name="b-use-a-group-by-clause-with-multiple-tables"></a>B. Utilice una cláusula GROUP BY con varias tablas  
 En el ejemplo siguiente se recupera el número de empleados de cada `City` de la tabla `Address` combinada con la tabla `EmployeeAddress`. Este ejemplo utiliza AdventureWorks. 
  
```  
SELECT a.City, COUNT(bea.AddressID) EmployeeCount  
FROM Person.BusinessEntityAddress AS bea   
    INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
GROUP BY a.City  
ORDER BY a.City;  
```  
  
### <a name="c-use-a-group-by-clause-with-an-expression"></a>C. Usar una cláusula GROUP BY con una expresión  
 En el ejemplo siguiente se recuperan las ventas totales de cada año con la función `DATEPART`. Debe incluirse la misma expresión en la lista `SELECT` y en la cláusula `GROUP BY`.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
### <a name="d-use-a-group-by-clause-with-a-having-clause"></a>D. Utilice una cláusula GROUP BY con una cláusula HAVING  
 En el ejemplo siguiente se usa la cláusula `HAVING` para especificar cuáles de los grupos generados en la cláusula `GROUP BY` deben incluirse en el conjunto de resultados.  
  
```  
SELECT DATEPART(yyyy,OrderDate) AS N'Year'  
    ,SUM(TotalDue) AS N'Total Order Amount'  
FROM Sales.SalesOrderHeader  
GROUP BY DATEPART(yyyy,OrderDate)  
HAVING DATEPART(yyyy,OrderDate) >= N'2003'  
ORDER BY DATEPART(yyyy,OrderDate);  
```  
  
## <a name="examples-sql-data-warehouse-and-parallel-data-warehouse"></a>Ejemplos: Almacenamiento de datos SQL y almacenamiento de datos paralelos  
  
### <a name="e-basic-use-of-the-group-by-clause"></a>E. Uso básico de la cláusula GROUP BY  
 En el ejemplo siguiente se busca la cantidad total de todas las ventas de cada día. Se devuelve una fila que contiene la suma de todas las ventas para cada día.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales FROM FactInternetSales  
GROUP BY OrderDateKey ORDER BY OrderDateKey;  
```  
  
### <a name="f-basic-use-of-the-distributedagg-hint"></a>F. Uso básico de la sugerencia DISTRIBUTED_AGG  
 Este ejemplo utiliza la sugerencia de consulta DISTRIBUTED_AGG para forzar que el dispositivo a la selección aleatoria de la tabla en la `CustomerKey` columna antes de realizar la agregación.  
  
```  
-- Uses AdventureWorksDW  
  
SELECT CustomerKey, SUM(SalesAmount) AS sas  
FROM FactInternetSales  
GROUP BY CustomerKey WITH (DISTRIBUTED_AGG)  
ORDER BY CustomerKey DESC;  
```  
  
### <a name="g-syntax-variations-for-group-by"></a>G. Variaciones de sintaxis para agrupar por  
 Cuando la lista de selección no tiene ninguna agregación, cada columna de la lista de selección debe incluirse en la lista GROUP BY. Las columnas calculadas de la lista de selección pueden ser que se muestran, pero no son necesarias, en la lista GROUP BY. Estos son algunos ejemplos de instrucciones SELECT sintácticamente válidas:  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, FirstName FROM DimCustomer GROUP BY LastName, FirstName;  
SELECT NumberCarsOwned FROM DimCustomer GROUP BY YearlyIncome, NumberCarsOwned;  
SELECT (SalesAmount + TaxAmt + Freight) AS TotalCost FROM FactInternetSales GROUP BY SalesAmount, TaxAmt, Freight;  
SELECT SalesAmount, SalesAmount*1.10 SalesTax FROM FactInternetSales GROUP BY SalesAmount;  
SELECT SalesAmount FROM FactInternetSales GROUP BY SalesAmount, SalesAmount*1.10;  
```  
  
### <a name="h-using-a-group-by-with-multiple-group-by-expressions"></a>H. Usar GROUP BY con varias expresiones de GROUP BY  
 En el ejemplo siguiente se agrupa los resultados utilizando varias `GROUP BY` criterios. If, dentro de cada `OrderDateKey` grupo, hay subgrupos que se pueden diferenciar por `DueDateKey`, se definirá una nueva agrupación para el conjunto de resultados.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, DueDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSalesGROUP BY OrderDateKey, DueDateKey   
ORDER BY OrderDateKey;  
```  
  
### <a name="i-using-a-group-by-clause-with-a-having-clause"></a>I. Utilizar una cláusula GROUP BY con una cláusula HAVING  
 En el ejemplo siguiente se usa el `HAVING` cláusula para especificar los grupos generados en el `GROUP BY` cláusula que debe incluirse en el conjunto de resultados. Sólo los grupos con fechas de pedidos en 2004 o una versión posterior se incluirán en los resultados.  
  
```  
-- Uses AdventureWorks  
  
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales   
FROM FactInternetSales  
GROUP BY OrderDateKey   
HAVING OrderDateKey > 20040000   
ORDER BY OrderDateKey;  
```  
  
## <a name="see-also"></a>Vea también  
 [GROUPING_ID &#40; Transact-SQL &#41;](~/t-sql/functions/grouping-id-transact-sql.md)   
 [AGRUPACIÓN &#40; Transact-SQL &#41;](~/t-sql/functions/grouping-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)   
 [Cláusula SELECT &#40; Transact-SQL &#41;](~/t-sql/queries/select-clause-transact-sql.md)  
  
  




