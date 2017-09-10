---
title: AVG (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVG_TSQL
- AVG
dev_langs:
- TSQL
helpviewer_keywords:
- AVG function [Transact-SQL]
- GROUP BY clause, AVG function
- DISTINCT keyword
- values [SQL Server], average
- average values
ms.assetid: 4534b705-d946-441b-9b5d-5fbe561c9131
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 710e588843de71aadbb6675baba8f29a7686f3e1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="avg-transact-sql"></a>AVG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve el promedio de los valores de un grupo. Se omiten los valores NULL.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
AVG ( [ ALL | DISTINCT ] expression )  
   OVER ( [ partition_by_clause ] order_by_clause )    
```  
  
## <a name="arguments"></a>Argumentos  
ALL  
Aplica la función de agregado a todos los valores. ALL es el valor predeterminado.
  
DISTINCT  
Especifica que AVG se ejecute solo en cada instancia única de un valor, sin importar el número de veces que aparezca el valor.
  
*expression*  
Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de exactos categoría de tipos de datos numéricos o numéricos aproximados excepto para la **bits** tipo de datos. No se permiten funciones de agregado ni subconsultas.
  
SOBRE **(** [ *partition_by_clause* ] *order_by_clause***)**  
*partition_by_clause* divide el conjunto de resultados generado por la cláusula FROM en particiones al que se aplica la función. Si no se especifica, la función trata todas las filas del conjunto de resultados de la consulta como un único grupo. *order_by_clause* determina el orden lógico en el que se realiza la operación. *order_by_clause* es necesario. Para obtener más información, consulte [la cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).
  
## <a name="return-types"></a>Tipos de valor devuelto
El tipo de valor devuelto viene determinado por el tipo del resultado evaluado de *expresión*.
  
|Resultado de la expresión|Tipo de valor devuelto|  
|---|---|
|**tinyint**|**int**|  
|**smallint**|**int**|  
|**int**|**int**|  
|**bigint**|**bigint**|  
|**decimal** categoría (p, s)|**decimal (38, s)** dividido por **decimal (10, 0)**|  
|**Money** y **smallmoney** categoría|**money**|  
|**float** y **real** categoría|**float**|  
  
## <a name="remarks"></a>Comentarios  
Si el tipo de datos de *expresión* es un alias de datos tipo, el tipo de valor devuelto también es del tipo de datos del alias. Sin embargo, si la base de datos de tipo del tipo de datos de alias se promueve, por ejemplo de **tinyint** a **int**, el valor devuelto es de datos ascendido tipo y no el tipo de datos de alias.
  
AVG () calcula la media de un conjunto de valores dividiendo la suma de estos valores por el recuento de valores no NULL. Si la suma supera el valor máximo para el tipo de datos del valor devuelto, se devolverá un error.
  
AVG es una función determinista cuando se utiliza con las cláusulas OVER y ORDER BY. Es no determinista si se especifica con las cláusulas OVER y ORDER BY. Para obtener más información, consulte [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-the-sum-and-avg-functions-for-calculations"></a>A. Usar las funciones SUM y AVG para los cálculos  
En el ejemplo siguiente se calcula el promedio de horas de vacaciones y la suma de horas de baja por enfermedad que han utilizado los vicepresidentes de [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]. Cada una de estas funciones de agregado produce un valor único de resumen para todas las filas recuperadas. En el ejemplo se usa la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
SELECT AVG(VacationHours)AS 'Average vacation hours',   
    SUM(SickLeaveHours) AS 'Total sick leave hours'  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Vice President%';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`Average vacation hours       Total sick leave hours`
  
`----------------------       ----------------------`
  
`25                           97`
  
`(1 row(s) affected)`
  
### <a name="b-using-the-sum-and-avg-functions-with-a-group-by-clause"></a>B. Usar las funciones SUM y AVG con una cláusula GROUP BY  
Cuando se utiliza con una cláusula `GROUP BY`, cada función de agregado produce un solo valor para cada grupo, en vez de para toda la tabla. En el ejemplo siguiente se obtienen valores de resumen para cada territorio de ventas de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. El resumen muestra el promedio de bonificaciones recibidas por los vendedores de cada territorio y la suma de las ventas realizadas hasta la fecha en cada territorio.
  
```sql
SELECT TerritoryID, AVG(Bonus)as 'Average bonus', SUM(SalesYTD) as 'YTD sales'  
FROM Sales.SalesPerson  
GROUP BY TerritoryID;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
TerritoryID Average Bonus         YTD Sales  
----------- --------------------- ---------------------  
NULL        0.00                  1252127.9471  
1           4133.3333             4502152.2674  
2           4100.00               3763178.1787  
3           2500.00               3189418.3662  
4           2775.00               6709904.1666  
5           6700.00               2315185.611  
6           2750.00               4058260.1825  
7           985.00                3121616.3202  
8           75.00                 1827066.7118  
9           5650.00               1421810.9242  
10          5150.00               4116871.2277  
  
(11 row(s) affected)  
```  
  
### <a name="c-using-avg-with-distinct"></a>C. Usar AVG con DISTINCT  
En la instrucción siguiente se devuelve el precio de venta promedio de los productos de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Si se especifica DISTINCT, solo se tienen en cuenta valores únicos en el cálculo.
  
```sql
SELECT AVG(DISTINCT ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`------------------------------`
  
`437.4042`
  
`(1 row(s) affected)`
  
### <a name="d-using-avg-without-distinct"></a>D. Usar AVG sin DISTINCT  
Sin DISTINCT, la función `AVG` busca el precio de venta promedio de todos los productos de la tabla `Product` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], incluidos los valores duplicados.
  
```sql
SELECT AVG(ListPrice)  
FROM Production.Product;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`------------------------------`
  
`438.6662`
  
`(1 row(s) affected)`
  
### <a name="e-using-the-over-clause"></a>E. Usar la cláusula OVER  
En el ejemplo siguiente se usa la función AVG con la cláusula OVER para proporcionar una media móvil de ventas anuales para cada territorio de la tabla `Sales.SalesPerson` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Se crean particiones de los datos por `TerritoryID` y se ordenan lógicamente por `SalesYTD`. Esto significa que la función AVG se calcula para cada territorio en función del año de ventas. Observe que para `TerritoryID` 1, solo hay dos filas para el año de ventas 2005, que representan los dos vendedores con ventas durante ese año. Se calculan las ventas medias de estas dos filas y la tercera fila que representa las ventas durante el año 2006 se incluye en el cálculo.
  
```sql
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
  
```sql
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
  
```sql
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
  
## <a name="see-also"></a>Vea también
[Las funciones de agregado &#40; Transact-SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md)  
[EN cláusula &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

