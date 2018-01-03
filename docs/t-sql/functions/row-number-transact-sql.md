---
title: ROW_NUMBER (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROW_NUMBER
- ROW_NUMBER_TSQL
- ROW_NUMBER()_TSQL
dev_langs: TSQL
helpviewer_keywords:
- ROW_NUMBER function
- row numbers [SQL Server]
- sequential row numbers [SQL Server]
ms.assetid: 82fa9016-77db-4b42-b4c8-df6095b81906
caps.latest.revision: "50"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 6ddb3472f19ce2fda8bc368cd07f7ea602d74a02
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="rownumber-transact-sql"></a>ROW_NUMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Establecen números de la salida de un resultado. Más específicamente, devuelve el número secuencial de una fila dentro de una partición de un conjunto de resultados, comenzando en 1 para la primera fila de cada partición. 
  
`ROW_NUMBER`y `RANK` son similares. `ROW_NUMBER`números de todas las filas secuencialmente (por ejemplo 1, 2, 3, 4, 5). `RANK`proporciona el mismo valor numérico valores equivalentes (por ejemplo 1, 2, 2, 4, 5).   
  
> [!NOTE]
> `ROW_NUMBER`un valor temporal, que se calcula cuando se ejecuta la consulta. Para conservar los números de una tabla, vea [propiedad IDENTITY](../../t-sql/statements/create-table-transact-sql-identity-property.md) y [secuencia](../../t-sql/statements/create-sequence-transact-sql.md). 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
  
## <a name="syntax"></a>Sintaxis  
  
```  
ROW_NUMBER ( )   
    OVER ( [ PARTITION BY value_expression , ... [ n ] ] order_by_clause )  
```  
  
## <a name="arguments"></a>Argumentos  
 PARTITION BY *value_expression*  
 Divide el conjunto de resultados generado por la [FROM](../../t-sql/queries/from-transact-sql.md) cláusula en particiones a los que se aplica la función ROW_NUMBER. *value_expression* especifica la columna mediante el cual se particiona el conjunto de resultados. Si `PARTITION BY` no se especifica, la función trata todas las filas del conjunto como un único grupo de resultados de consulta. Para obtener más información, consulte [la cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 *order_by_clause*  
 El `ORDER BY` cláusula determina la secuencia en que las filas se asignan su único `ROW_NUMBER` dentro de una partición especificada. Es obligatorio. Para obtener más información, consulte [la cláusula OVER &#40; Transact-SQL &#41; ](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>Tipos devueltos  
 **bigint**  
  
## <a name="general-remarks"></a>Notas generales  
 No hay ninguna garantía de que las filas devueltas por una consulta mediante `ROW_NUMBER()` se ordenarán exactamente lo mismo con cada ejecución, a menos que las condiciones siguientes son verdaderas.  
  
1.  Los valores de la columna de la partición sean únicos.  
  
2.  Los valores de la `ORDER BY` columnas son únicas.  
  
3.  Combinaciones de valores de la columna de partición y `ORDER BY` columnas son únicas.  
  
 `ROW_NUMBER()`es no determinista. Para obtener más información, consulte [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-examples"></a>A. Ejemplos sencillos 

La siguiente consulta devuelve las tablas del cuatro sistema en orden alfabético.

```sql
SELECT 
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5
ORDER BY name ASC;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|NAME    |recovery_model_desc |  
|-----------  |------------ |  
|maestra |SIMPLE |
|model |FULL |
|msdb |SIMPLE |
|tempdb |SIMPLE |

Para agregar una columna de número de fila delante de cada fila, agregue una columna con el `ROW_NUMBER` función, en este caso denominada `Row#`. Debe mover el `ORDER BY` cláusula hasta el `OVER` cláusula.

```sql
SELECT 
  ROW_NUMBER() OVER(ORDER BY name ASC) AS Row#,
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|Fila # |NAME    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |maestra |SIMPLE |
|2 |model |FULL |
|3 |msdb |SIMPLE |
|4 |tempdb |SIMPLE |

Agregar un `PARTITION BY` en la cláusula de la `recovery_model_desc` columna, se reiniciará la numeración cuando el `recovery_model_desc` cambia el valor. 
 
```sql
SELECT 
  ROW_NUMBER() OVER(PARTITION BY recovery_model_desc ORDER BY name ASC) 
    AS Row#,
  name, recovery_model_desc
FROM sys.databases WHERE database_id < 5;
```  

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|Fila # |NAME    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |model |FULL |
|1 |maestra |SIMPLE |
|2 |msdb |SIMPLE |
|3 |tempdb |SIMPLE |


### <a name="b-returning-the-row-number-for-salespeople"></a>B. Devolver el número de fila de vendedor  
 En el ejemplo siguiente se calcula un número de fila para los vendedores de [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] según la categoría de ventas anuales hasta la fecha.  
  
```sql  
USE AdventureWorks2012;   
GO  
SELECT ROW_NUMBER() OVER(ORDER BY SalesYTD DESC) AS Row,   
    FirstName, LastName, ROUND(SalesYTD,2,1) AS "Sales YTD"   
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Row FirstName    LastName               SalesYTD  
--- -----------  ---------------------- -----------------  
1   Linda        Mitchell               4251368.54  
2   Jae          Pak                    4116871.22  
3   Michael      Blythe                 3763178.17  
4   Jillian      Carson                 3189418.36  
5   Ranjit       Varkey Chudukatil      3121616.32  
6   José         Saraiva                2604540.71  
7   Shu          Ito                    2458535.61  
8   Tsvi         Reiter                 2315185.61  
9   Rachel       Valdez                 1827066.71  
10  Tete         Mensa-Annan            1576562.19  
11  David        Campbell               1573012.93  
12  Garrett      Vargas                 1453719.46  
13  Lynn         Tsoflias               1421810.92  
14  Pamela       Ansman-Wolfe           1352577.13  
```  
  
### <a name="c-returning-a-subset-of-rows"></a>C. Devolver un subconjunto de filas  
 En el ejemplo siguiente se calculan los números de fila para todas las filas de la tabla `SalesOrderHeader` en el orden de `OrderDate` y solo se devuelven las filas `50` a `60` inclusive.  
  
```sql  
USE AdventureWorks2012;  
GO  
WITH OrderedOrders AS  
(  
    SELECT SalesOrderID, OrderDate,  
    ROW_NUMBER() OVER (ORDER BY OrderDate) AS RowNumber  
    FROM Sales.SalesOrderHeader   
)   
SELECT SalesOrderID, OrderDate, RowNumber    
FROM OrderedOrders   
WHERE RowNumber BETWEEN 50 AND 60;  
```  
  
### <a name="d-using-rownumber-with-partition"></a>D. Usar ROW_NUMBER() con PARTITION  
 En el ejemplo siguiente se usa el argumento `PARTITION BY` para crear particiones del conjunto de resultados de la consulta por la columna `TerritoryName`. La cláusula `ORDER BY` especificada en la cláusula `OVER` ordena las filas de cada partición por la columna `SalesYTD`. La cláusula `ORDER BY` de la instrucción `SELECT` ordena todo el conjunto de resultados de la consulta por `TerritoryName`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT FirstName, LastName, TerritoryName, ROUND(SalesYTD,2,1) AS SalesYTD,  
ROW_NUMBER() OVER(PARTITION BY TerritoryName ORDER BY SalesYTD DESC) 
  AS Row  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0  
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
FirstName  LastName             TerritoryName        SalesYTD      Row  
---------  -------------------- ------------------   ------------  ---  
Lynn       Tsoflias             Australia            1421810.92    1  
José       Saraiva              Canada               2604540.71    1  
Garrett    Vargas               Canada               1453719.46    2  
Jillian    Carson               Central              3189418.36    1  
Ranjit     Varkey Chudukatil    France               3121616.32    1  
Rachel     Valdez               Germany              1827066.71    1  
Michael    Blythe               Northeast            3763178.17    1  
Tete       Mensa-Annan          Northwest            1576562.19    1  
David      Campbell             Northwest            1573012.93    2  
Pamela     Ansman-Wolfe         Northwest            1352577.13    3  
Tsvi       Reiter               Southeast            2315185.61    1  
Linda      Mitchell             Southwest            4251368.54    1  
Shu        Ito                  Southwest            2458535.61    2  
Jae        Pak                  United Kingdom       4116871.22    1  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-returning-the-row-number-for-salespeople"></a>E. Devolver el número de fila de vendedor  
 El ejemplo siguiente devuelve el `ROW_NUMBER` para los representantes de ventas en función de sus cuotas de ventas asignado.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) 
    AS RowNumber,  
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

### <a name="f-using-rownumber-with-partition"></a>F. Usar ROW_NUMBER() con PARTITION  
 El ejemplo siguiente muestra cómo utilizar la función `ROW_NUMBER` con el argumento `PARTITION BY`. Esto hace que el `ROW_NUMBER` función para numerar las filas de cada partición.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(PARTITION BY SalesTerritoryKey 
        ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    LastName, SalesTerritoryKey AS Territory,  
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName, SalesTerritoryKey;  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
 
```  
 
RowNumber  LastName            Territory  SalesQuota  
---------  ------------------  ---------  -------------  
1          Campbell            1           4,025,000.00  
2          Ansman-Wolfe        1           3,551,000.00  
3          Mensa-Annan         1           2,275,000.00  
1          Blythe              2          11,162,000.00  
1          Carson              3          12,198,000.00  
1          Mitchell            4          11,786,000.00  
2          Ito                 4           7,804,000.00  
```
  
## <a name="see-also"></a>Vea también  
 [RANGO &#40; Transact-SQL &#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK &#40; Transact-SQL &#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [NTILE &#40; Transact-SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)  
  
  


