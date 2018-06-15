---
title: Cláusula OVER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OVER_TSQL
- OVER
dev_langs:
- TSQL
helpviewer_keywords:
- order of rowsets [SQL Server]
- rowsets [SQL Server], windowing
- window function
- partitions [SQL Server], rowsets
- clauses [SQL Server], OVER
- rowsets [SQL Server], partitioning
- rowsets [SQL Server], ordering
- OVER clause
ms.assetid: ddcef3a6-0341-43e0-ae73-630484b7b398
caps.latest.revision: 75
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: af253859d4756afdc1c07f5022662f33874a5d75
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064832"
---
# <a name="select---over-clause-transact-sql"></a>SELECT: cláusula OVER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Determina las particiones y el orden de un conjunto de filas antes de que se aplique la función de ventana asociada. Es decir, la cláusula OVER define una ventana o un conjunto de filas definido por el usuario en un conjunto de resultados de la consulta. Una función de ventana calcula entonces un valor para cada fila de la ventana. Puede utilizar la cláusula OVER con funciones para calcular valores agregados tales como medias móviles, agregados acumulados, totales acumulados o N elementos superiores por resultados del grupo.  
  
-   [Funciones de categoría](../../t-sql/functions/ranking-functions-transact-sql.md)  
  
-   [Funciones de agregado](../../t-sql/functions/aggregate-functions-transact-sql.md)  
  
-   [Funciones analíticas](../../t-sql/functions/analytic-functions-transact-sql.md)  
  
-   [Función NEXT VALUE FOR](../../t-sql/functions/next-value-for-transact-sql.md)  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server, Azure SQL Database, and Azure SQL Data Warehouse  
  
OVER (   
       [ <PARTITION BY clause> ]  
       [ <ORDER BY clause> ]   
       [ <ROW or RANGE clause> ]  
      )  
  
<PARTITION BY clause> ::=  
PARTITION BY value_expression , ... [ n ]  
  
<ORDER BY clause> ::=  
ORDER BY order_by_expression  
    [ COLLATE collation_name ]   
    [ ASC | DESC ]   
    [ ,...n ]  
  
<ROW or RANGE clause> ::=  
{ ROWS | RANGE } <window frame extent>  
  
<window frame extent> ::=   
{   <window frame preceding>  
  | <window frame between>  
}  
<window frame between> ::=   
  BETWEEN <window frame bound> AND <window frame bound>  
  
<window frame bound> ::=   
{   <window frame preceding>  
  | <window frame following>  
}  
  
<window frame preceding> ::=   
{  
    UNBOUNDED PRECEDING  
  | <unsigned_value_specification> PRECEDING  
  | CURRENT ROW  
}  
  
<window frame following> ::=   
{  
    UNBOUNDED FOLLOWING  
  | <unsigned_value_specification> FOLLOWING  
  | CURRENT ROW  
}  
  
<unsigned value specification> ::=   
{  <unsigned integer literal> }  
  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
OVER ( [ PARTITION BY value_expression ] [ order_by_clause ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 PARTITION BY  
 Divide el conjunto de resultados de la consulta en particiones. La función se aplica a cada partición por separado y el cálculo se reinicia para cada partición.  
  
 *value_expression*  
 Especifica la columna a partir de la cual se particiona el conjunto de filas. *value_expression* solo puede hacer referencia a columnas disponibles a través de la cláusula FROM. *value_expression* no puede hacer referencia a expresiones ni a alias de la lista de selección. *value_expression* puede ser una expresión de columna, una subconsulta escalar, una función escalar o una variable definida por el usuario.  
  
 \<ORDER BY clause>  
 Define el orden lógico de las filas dentro de cada partición del conjunto de resultados. Es decir, especifica el orden lógico en el que se realiza el cálculo de la función de ventana.  
  
 *order_by_expression*  
 Especifica la columna o expresión según la cual se va a realizar la ordenación. *order_by_expression* solo puede hacer referencia a columnas disponibles a través de la cláusula FROM. No se puede especificar un número entero para representar un nombre de columna o alias.  
  
 COLLATE *collation_name*  
 Especifica que la operación ORDER BY se debe realizar según la intercalación especificada en *collation_name*. *collation_name* puede ser un nombre de intercalación de Windows o un nombre de intercalación de SQL. Para más información, consulte [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md). COLLATE se aplica a las columnas de tipo **char**, **varchar**, **nchar** y **nvarchar**.  
  
 **ASC** | DESC  
 Indica que los valores de la columna especificada se deben ordenar en sentido ascendente o descendente. ASC es el criterio de ordenación predeterminado. Los valores NULL se tratan como los valores más bajos posibles.  
  
 ROWS | RANGE  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Limita aún más las filas de la partición especificando los puntos inicial y final. Para ello, se especifica un rango de filas con respecto a la fila actual mediante asociación lógica o asociación física. La asociación física se realiza mediante la cláusula ROWS.  
  
 La cláusula ROWS restringe las filas dentro de una partición especificando un número fijo de filas delante y detrás de la fila actual. La cláusula RANGE también puede restringir lógicamente las filas de una partición especificando un rango de valores con respecto al valor de la fila actual. Las filas precedentes y siguientes se definen en función de la ordenación de la cláusula ORDER BY. El marco de ventana “RANGE … CURRENT ROW …” incluye todas las filas que tienen los mismos valores en la expresión ORDER BY que la fila actual. Por ejemplo, ROWS BETWEEN 2 PRECEDING AND CURRENT ROW indica que la ventana de filas en la que opera la función tiene un tamaño de tres filas, con dos filas delante hasta e inclusive la fila actual.  
  
> [!NOTE]  
>  ROWS o RANGE requieren que se especifique la cláusula ORDER BY. Si ORDER BY contiene varias expresiones de orden, CURRENT ROW FOR RANGE considera todas las columnas de la lista ORDER BY al determinar la fila actual.  
  
 UNBOUNDED PRECEDING  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica que la ventana comienza en la primera fila de la partición. UNBOUNDED PRECEDING solo se puede especificar como punto inicial de la ventana.  
  
 \<especificación de valor sin signo> PRECEDING  
 Se especifica con \<especificación de valor sin signo> para indicar el número de filas o valores que preceden a la fila actual. Esta especificación no se permite para RANGE.  
  
 CURRENT ROW  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Especifica que la ventana comienza o termina en la fila actual cuando se utiliza con ROWS, o el valor actual cuando se utiliza con RANGE. CURRENT ROW se puede especificar como punto inicial o final.  
  
 BETWEEN \<límite del marco de ventana> AND \<límite del marco de ventana>  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Se utiliza con ROWS o RANGE para especificar los puntos de límite inferior (inicio) y superior (final) de la ventana. \<límite del marco de ventana> define el punto inicial del límite y \<límite del marco de ventana> define el punto final. El límite superior no puede ser menor que el límite inferior.  
  
 UNBOUNDED FOLLOWING  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. 
  
 Especifica que la ventana termina en la última fila de la partición. UNBOUNDED FOLLOWING solo se puede especificar como punto final de una ventana. Por ejemplo, RANGE BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING define una ventana que empieza en la fila actual y termina en la última fila de la partición.  
  
 \<especificación de valor sin signo> FOLLOWING  
 Se especifica con \<especificación de valor sin signo> para indicar el número de filas o valores detrás de la fila actual. Cuando \<especificación de valor sin signo> FOLLOWING se especifica como punto inicial de la ventana, el punto final debe ser \<especificación de valor sin signo> FOLLOWING. Por ejemplo, ROWS BETWEEN 2 FOLLOWING AND 10 FOLLOWING define una ventana que empieza en la segunda fila a partir de la fila actual y termina en la décima fila a partir de la fila actual. Esta especificación no se permite para RANGE.  
  
 literal entero sin signo  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Es un literal entero positivo (incluido el 0) que especifica el número de filas o de valores delante o detrás de la fila o el valor actual. Esta especificación es válida solamente para ROWS.  
  
## <a name="general-remarks"></a>Notas generales  
 Se pueden utilizar varias funciones de ventana en una sola consulta con una única cláusula FROM. La cláusula OVER de cada función puede diferir en particiones y también en orden.  
  
 Si no se especifica PARTITION BY, la función trata todas las filas del conjunto de resultados de la consulta como un único grupo. 
 
### <a name="important"></a>Importante:

Si se especifica ROWS/RANGE y se usa \<marco de ventana precedente> para \<extensión de marco de ventana> (sintaxis abreviada), esta especificación se usa para el punto inicial del límite del marco de ventana y CURRENT ROW se usa para el punto final. Por ejemplo, “ROWS 5 PRECEDING” es igual a “ROWS BETWEEN 5 PRECEDING AND CURRENT ROW”.  
  
> [!NOTE]
> Si no se especifica ORDER BY, se utiliza la partición completa para el marco de ventana. Esto se aplica únicamente a las funciones que no requieren la cláusula ORDER BY. Si no se especifica ROWS/RANGE pero sí ORDER BY, RANGE UNBOUNDED PRECEDING AND CURRENT ROW se utiliza como valor predeterminado para el marco de ventana. Esto se aplica solamente a las funciones que pueden aceptar la especificación opcional de ROWS/RANGE. Por ejemplo, las funciones de clasificación no pueden aceptar ROWS/RANGE; por lo tanto, este marco de ventana no se aplica aunque se especifique ORDER BY y no se especifique ROWS/RANGE.  
    
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 No se puede utilizar la cláusula OVER con la función de agregado CHECKSUM.  
  
 No se puede usar RANGE con \<especificación de valor sin signo> PRECEDING o \<especificación de valor sin signo> FOLLOWING.  
  
 Dependiendo de la función de clasificación, de agregado o analítica usada con la cláusula OVER, puede que no se admitan la \<cláusula ORDER BY> o la \<cláusula ROWS y RANGE>.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-the-over-clause-with-the-rownumber-function"></a>A. Utilizar la cláusula OVER con la función ROW_NUMBER  
 En el ejemplo siguiente se muestra cómo usar la cláusula OVER con la función ROW_NUMBER para mostrar un número de fila para cada fila de una partición. La cláusula ORDER BY especificada en la cláusula OVER ordena las filas de cada partición por la columna `SalesYTD`. La cláusula ORDER BY en la instrucción SELECT determina el orden en que se devuelve el conjunto completo de resultados de la consulta.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT ROW_NUMBER() OVER(PARTITION BY PostalCode ORDER BY SalesYTD DESC) AS "Row Number",   
    p.LastName, s.SalesYTD, a.PostalCode  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0  
ORDER BY PostalCode;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Row Number      LastName                SalesYTD              PostalCode 
 --------------- ----------------------- --------------------- ---------- 
 1               Mitchell                4251368.5497          98027 
 2               Blythe                  3763178.1787          98027 
 3               Carson                  3189418.3662          98027 
 4               Reiter                  2315185.611           98027 
 5               Vargas                  1453719.4653          98027  
 6               Ansman-Wolfe            1352577.1325          98027  
 1               Pak                     4116871.2277          98055  
 2               Varkey Chudukatil       3121616.3202          98055  
 3               Saraiva                 2604540.7172          98055  
 4               Ito                     2458535.6169          98055  
 5               Valdez                  1827066.7118          98055  
 6               Mensa-Annan             1576562.1966          98055  
 7               Campbell                1573012.9383          98055  
 8               Tsoflias                1421810.9242          98055
 ```  
  
### <a name="b-using-the-over-clause-with-aggregate-functions"></a>B. Utilizar la cláusula OVER con funciones de agregado  
 En el ejemplo siguiente se utiliza la cláusula `OVER` con funciones de agregado en todas las filas devueltas por la consulta. En este ejemplo, el uso de `OVER` es más eficaz que usar subconsultas para obtener los valores agregados.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT SalesOrderID, ProductID, OrderQty  
    ,SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS Total  
    ,AVG(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Avg"  
    ,COUNT(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Count"  
    ,MIN(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Min"  
    ,MAX(OrderQty) OVER(PARTITION BY SalesOrderID) AS "Max"  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
SalesOrderID ProductID   OrderQty Total       Avg         Count       Min    Max  
------------ ----------- -------- ----------- ----------- ----------- ------ ------  
43659        776         1        26          2           12          1      6  
43659        777         3        26          2           12          1      6  
43659        778         1        26          2           12          1      6  
43659        771         1        26          2           12          1      6  
43659        772         1        26          2           12          1      6  
43659        773         2        26          2           12          1      6  
43659        774         1        26          2           12          1      6  
43659        714         3        26          2           12          1      6  
43659        716         1        26          2           12          1      6  
43659        709         6        26          2           12          1      6  
43659        712         2        26          2           12          1      6  
43659        711         4        26          2           12          1      6  
43664        772         1        14          1           8           1      4  
43664        775         4        14          1           8           1      4  
43664        714         1        14          1           8           1      4  
43664        716         1        14          1           8           1      4  
43664        777         2        14          1           8           1      4  
43664        771         3        14          1           8           1      4  
43664        773         1        14          1           8           1      4  
43664        778         1        14          1           8           1      4  
```  
  
 En el ejemplo siguiente se muestra el uso de la cláusula `OVER` con una función de agregado en un valor calculado.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT SalesOrderID, ProductID, OrderQty  
    ,SUM(OrderQty) OVER(PARTITION BY SalesOrderID) AS Total  
    ,CAST(1. * OrderQty / SUM(OrderQty) OVER(PARTITION BY SalesOrderID)   
        *100 AS DECIMAL(5,2))AS "Percent by ProductID"  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Tenga en cuenta que los agregados se calculan mediante `SalesOrderID` y se calcula `Percent by ProductID` para cada línea de cada `SalesOrderID`.  
  
```  
SalesOrderID ProductID   OrderQty Total       Percent by ProductID  
------------ ----------- -------- ----------- ---------------------------------------  
43659        776         1        26          3.85  
43659        777         3        26          11.54  
43659        778         1        26          3.85  
43659        771         1        26          3.85  
43659        772         1        26          3.85  
43659        773         2        26          7.69  
43659        774         1        26          3.85  
43659        714         3        26          11.54  
43659        716         1        26          3.85  
43659        709         6        26          23.08  
43659        712         2        26          7.69  
43659        711         4        26          15.38  
43664        772         1        14          7.14  
43664        775         4        14          28.57  
43664        714         1        14          7.14  
43664        716         1        14          7.14  
43664        777         2        14          14.29  
43664        771         3        14          21.4  
43664        773         1        14          7.14  
43664        778         1        14          7.14  
  
 (20 row(s) affected)  
```  
  
### <a name="c-producing-a-moving-average-and-cumulative-total"></a>C. Producir una media móvil y un total acumulativo  
 En el ejemplo siguiente se usan las funciones AVG y SUM con la cláusula OVER para proporcionar una media móvil y un total acumulado de ventas anuales para cada territorio de la tabla `Sales.SalesPerson`. Se crean particiones de los datos por `TerritoryID` y se ordenan lógicamente por `SalesYTD`. Esto significa que la función AVG se calcula para cada territorio en función del año de ventas. Observe que para `TerritoryID` 1, solo hay dos filas para el año de ventas 2005, que representan los dos vendedores con ventas durante ese año. Se calculan las ventas medias de estas dos filas y la tercera fila que representa las ventas durante el año 2006 se incluye en el cálculo.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                           ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                            ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY TerritoryID,SalesYear;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           559,697.56           559,697.56  
287              NULL        2006        519,905.93           539,801.75           1,079,603.50  
285              NULL        2007        172,524.45           417,375.98           1,252,127.95  
283              1           2005        1,573,012.94         1,462,795.04         2,925,590.07  
280              1           2005        1,352,577.13         1,462,795.04         2,925,590.07  
284              1           2006        1,576,562.20         1,500,717.42         4,502,152.27  
275              2           2005        3,763,178.18         3,763,178.18         3,763,178.18  
277              3           2005        3,189,418.37         3,189,418.37         3,189,418.37  
276              4           2005        4,251,368.55         3,354,952.08         6,709,904.17  
281              4           2005        2,458,535.62         3,354,952.08         6,709,904.17  
  
(10 row(s) affected)  
  
```  
  
 En este ejemplo, la cláusula OVER no incluye PARTITION BY. Esto significa que la función se aplicará a todas las filas devueltas por la consulta. La cláusula ORDER BY especificada en la cláusula OVER determina el orden lógico al que se aplica la función AVG. La consulta devuelve una media móvil de ventas por año para todos los territorios de ventas especificados en la cláusula WHERE. La cláusula ORDER BY especificada en la instrucción SELECT determina el orden en que se muestran las filas de la consulta.  
  
```sql  
SELECT BusinessEntityID, TerritoryID   
   ,DATEPART(yy,ModifiedDate) AS SalesYear  
   ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
   ,CONVERT(varchar(20),AVG(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS MovingAvg  
   ,CONVERT(varchar(20),SUM(SalesYTD) OVER (ORDER BY DATEPART(yy,ModifiedDate)   
                                            ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5  
ORDER BY SalesYear;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYear   SalesYTD             MovingAvg            CumulativeTotal  
---------------- ----------- ----------- -------------------- -------------------- --------------------  
274              NULL        2005        559,697.56           2,449,684.05         17,147,788.35  
275              2           2005        3,763,178.18         2,449,684.05         17,147,788.35  
276              4           2005        4,251,368.55         2,449,684.05         17,147,788.35  
277              3           2005        3,189,418.37         2,449,684.05         17,147,788.35  
280              1           2005        1,352,577.13         2,449,684.05         17,147,788.35  
281              4           2005        2,458,535.62         2,449,684.05         17,147,788.35  
283              1           2005        1,573,012.94         2,449,684.05         17,147,788.35  
284              1           2006        1,576,562.20         2,138,250.72         19,244,256.47  
287              NULL        2006        519,905.93           2,138,250.72         19,244,256.47  
285              NULL        2007        172,524.45           1,941,678.09         19,416,780.93  
(10 row(s) affected)  
```  
  
### <a name="d-specifying-the-rows-clause"></a>D. Especificar la cláusula ROWS  
  
**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 En el siguiente ejemplo se usa la cláusula ROWS para definir una ventana de cuyas filas se calcula la fila actual y el número *N* de filas incluidas aquí (1 fila en este ejemplo).  
  
```sql  
SELECT BusinessEntityID, TerritoryID   
    ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
    ,DATEPART(yy,ModifiedDate) AS SalesYear  
    ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                             ORDER BY DATEPART(yy,ModifiedDate)   
                                             ROWS BETWEEN CURRENT ROW AND 1 FOLLOWING ),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYTD             SalesYear   CumulativeTotal  
---------------- ----------- -------------------- ----------- --------------------  
274              NULL        559,697.56           2005        1,079,603.50  
287              NULL        519,905.93           2006        692,430.38  
285              NULL        172,524.45           2007        172,524.45  
283              1           1,573,012.94         2005        2,925,590.07  
280              1           1,352,577.13         2005        2,929,139.33  
284              1           1,576,562.20         2006        1,576,562.20  
275              2           3,763,178.18         2005        3,763,178.18  
277              3           3,189,418.37         2005        3,189,418.37  
276              4           4,251,368.55         2005        6,709,904.17  
281              4           2,458,535.62         2005        2,458,535.62  
```  
  
 En el ejemplo siguiente, la cláusula ROWS se especifica con UNBOUNDED PRECEDING. El resultado es que la ventana comienza en la primera fila de la partición.  
  
```sql  
SELECT BusinessEntityID, TerritoryID   
    ,CONVERT(varchar(20),SalesYTD,1) AS  SalesYTD  
    ,DATEPART(yy,ModifiedDate) AS SalesYear  
    ,CONVERT(varchar(20),SUM(SalesYTD) OVER (PARTITION BY TerritoryID   
                                             ORDER BY DATEPART(yy,ModifiedDate)   
                                             ROWS UNBOUNDED PRECEDING),1) AS CumulativeTotal  
FROM Sales.SalesPerson  
WHERE TerritoryID IS NULL OR TerritoryID < 5;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
BusinessEntityID TerritoryID SalesYTD             SalesYear   CumulativeTotal  
---------------- ----------- -------------------- ----------- --------------------  
274              NULL        559,697.56           2005        559,697.56  
287              NULL        519,905.93           2006        1,079,603.50  
285              NULL        172,524.45           2007        1,252,127.95  
283              1           1,573,012.94         2005        1,573,012.94  
280              1           1,352,577.13         2005        2,925,590.07  
284              1           1,576,562.20         2006        4,502,152.27  
275              2           3,763,178.18         2005        3,763,178.18  
277              3           3,189,418.37         2005        3,189,418.37  
276              4           4,251,368.55         2005        4,251,368.55  
281              4           2,458,535.62         2005        6,709,904.17  
  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-the-over-clause-with-the-rownumber-function"></a>E. Utilizar la cláusula OVER con la función ROW_NUMBER  
 En este ejemplo se devuelve ROW_NUMBER para los representantes de ventas en función de su cuota de ventas asignada.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    FirstName, LastName,   
CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName;  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
 ```
 RowNumber  FirstName  LastName            SalesQuota  
 ---------  ---------  ------------------  -------------  
 1          Jillian    Carson              12,198,000.00  
 2          Linda      Mitchell            11,786,000.00  
 3          Michael    Blythe              11,162,000.00  
 4          Jae        Pak                 10,514,000.00  
 ```
 
### <a name="f-using-the-over-clause-with-aggregate-functions"></a>F. Utilizar la cláusula OVER con funciones de agregado  
 En el siguiente ejemplo se muestra el uso de la cláusula OVER con funciones de agregado. En este ejemplo, es más eficaz usar la cláusula OVER que subconsultas.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT SalesOrderNumber AS OrderNumber, ProductKey,   
       OrderQuantity AS Qty,   
       SUM(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Total,  
       AVG(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Avg,  
       COUNT(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Count,  
       MIN(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Min,  
       MAX(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Max  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN(N'SO43659',N'SO43664') AND  
      ProductKey LIKE '2%'  
ORDER BY SalesOrderNumber,ProductKey;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 OrderNumber  Product  Qty  Total  Avg  Count  Min  Max  
 -----------  -------  ---  -----  ---  -----  ---  ---  
 SO43659      218      6    16     3    5      1    6  
 SO43659      220      4    16     3    5      1    6  
 SO43659      223      2    16     3    5      1    6  
 SO43659      229      3    16     3    5      1    6  
 SO43659      235      1    16     3    5      1    6  
 SO43664      229      1     2     1    2      1    1  
 SO43664      235      1     2     1    2      1    1  
 ```
 
 En el siguiente ejemplo se muestra el uso de la cláusula OVER con una función de agregado en un valor calculado. Tenga en cuenta que los agregados se calculan por medio de `SalesOrderNumber` y el porcentaje del pedido de ventas totales se calcula para cada línea de cada `SalesOrderNumber`.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT SalesOrderNumber AS OrderNumber, ProductKey AS Product,   
       OrderQuantity AS Qty,   
       SUM(OrderQuantity) OVER(PARTITION BY SalesOrderNumber) AS Total,  
       CAST(1. * OrderQuantity / SUM(OrderQuantity)   
        OVER(PARTITION BY SalesOrderNumber)   
            *100 AS DECIMAL(5,2)) AS PctByProduct  
FROM dbo.FactResellerSales   
WHERE SalesOrderNumber IN(N'SO43659',N'SO43664') AND  
      ProductKey LIKE '2%'  
ORDER BY SalesOrderNumber,ProductKey;  
```  
  
 El primer inicio de este conjunto de resultados es:  
  
 ```
 OrderNumber  Product  Qty  Total  PctByProduct  
 -----------  -------  ---  -----  ------------  
 SO43659      218      6    16     37.50  
 SO43659      220      4    16     25.00  
 SO43659      223      2    16     12.50  
 SO43659      229      2    16     18.75  
 ```
 
## <a name="see-also"></a>Ver también  
 [Funciones de agregado &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)   
 [Funciones analíticas &#40;Transact-SQL&#41;](../../t-sql/functions/analytic-functions-transact-sql.md)   
 [Excelente entrada de blog de Itzik Ben-Gan sobre las funciones de ventana y OVER en sqlmag.com](http://sqlmag.com/sql-server-2012/how-use-microsoft-sql-server-2012s-window-functions-part-1)  
  
  
