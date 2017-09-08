---
title: Usar PIVOT y UNPIVOT | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PIVOT_TSQL
helpviewer_keywords:
- FROM clause, UNPIVOT operator
- unpivoting tables
- table pivoting [SQL Server]
- UNPIVOT operator
- crosstab query
- PIVOT operator
- rotating table-valued expressions
- pivoting tables
- FROM clause, PIVOT operator
- rotating columns
ms.assetid: 24ba54fc-98f7-4d35-8881-b5158aac1d66
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 413e4e89679358f0c53c82340dcae5640387ddcb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="from---using-pivot-and-unpivot"></a>DE - usar PIVOT y UNPIVOT
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Puede usar el `PIVOT` y `UNPIVOT` operadores relacionales para modificar una expresión con valores de tabla en otra tabla. `PIVOT`gira una expresión con valores de tabla convirtiendo los valores únicos de una columna de la expresión en varias columnas en la salida y realiza agregaciones donde son necesarias en cualquier valor de columna restante que se desee en la salida final. `UNPIVOT`realiza la operación contraria a PIVOT girando las columnas de una expresión con valores de tabla en valores de columna.  
  
 La sintaxis de `PIVOT` proporciona es más sencillo y más legible que la sintaxis que se pueden especificar en una serie compleja de `SELECT...CASE` instrucciones. Para obtener una descripción completa de la sintaxis de `PIVOT`, consulte [de (Transact-SQL)](../../t-sql/queries/from-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
 La sintaxis siguiente resume cómo se utiliza el `PIVOT` operador.  
  
```  
SELECT <non-pivoted column>,  
    [first pivoted column] AS <column name>,  
    [second pivoted column] AS <column name>,  
    ...  
    [last pivoted column] AS <column name>  
FROM  
    (<SELECT query that produces the data>)   
    AS <alias for the source query>  
PIVOT  
(  
    <aggregation function>(<column being aggregated>)  
FOR   
[<column that contains the values that will become column headers>]   
    IN ( [first pivoted column], [second pivoted column],  
    ... [last pivoted column])  
) AS <alias for the pivot table>  
<optional ORDER BY clause>;  
```  

## <a name="remarks"></a>Comentarios  
Los identificadores de columna en la `UNPIVOT` cláusula siga la intercalación del catálogo. Para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], la intercalación es siempre `SQL_Latin1_General_CP1_CI_AS`. Para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] bases de datos parcialmente independientes, la intercalación es siempre `Latin1_General_100_CI_AS_KS_WS_SC`. Si la columna se combina con otras columnas, a continuación, en una cláusula collate (`COLLATE DATABASE_DEFAULT`) es necesaria para evitar conflictos.  

  
## <a name="basic-pivot-example"></a>Ejemplo PIVOT básico  
 En el ejemplo de código siguiente se genera una tabla de dos columnas con cuatro filas.  
  
```  
USE AdventureWorks2014 ;  
GO  
SELECT DaysToManufacture, AVG(StandardCost) AS AverageCost   
FROM Production.Product  
GROUP BY DaysToManufacture;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 DaysToManufacture AverageCost
 ----------------- -----------
 0                 5.0885
 1                 223.88
 2                 359.1082
 4                 949.4105
 ```
  
 No hay productos definidos con tres `DaysToManufacture`.  
  
 En el código siguiente se muestra el mismo resultado, dinamizado para que los valores de `DaysToManufacture` se conviertan en encabezados de columna. Se proporciona una columna para tres `[3]` días, aunque los resultados son `NULL`.  
  
```  
-- Pivot table with one row and five columns  
SELECT 'AverageCost' AS Cost_Sorted_By_Production_Days,   
[0], [1], [2], [3], [4]  
FROM  
(SELECT DaysToManufacture, StandardCost   
    FROM Production.Product) AS SourceTable  
PIVOT  
(  
AVG(StandardCost)  
FOR DaysToManufacture IN ([0], [1], [2], [3], [4])  
) AS PivotTable;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Cost_Sorted_By_Production_Days 0           1           2           3           4         
------------------------------ ----------- ----------- ----------- ----------- -----------
AverageCost                    5.0885      223.88      359.1082    NULL        949.4105
```
  
## <a name="complex-pivot-example"></a>Ejemplo PIVOT complejo  
 Un escenario habitual en el que `PIVOT` puede ser útil es cuando se desea generar informes de tabla cruzada para resumir datos. Por ejemplo, suponga que desea consultar la tabla `PurchaseOrderHeader` en la base de datos de ejemplo `AdventureWorks2014` para determinar el número de pedidos de compra colocados por ciertos empleados. En la siguiente consulta se proporciona este informe, ordenado por proveedor.  
  
```  
USE AdventureWorks2014;  
GO  
SELECT VendorID, [250] AS Emp1, [251] AS Emp2, [256] AS Emp3, [257] AS Emp4, [260] AS Emp5  
FROM   
(SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM Purchasing.PurchaseOrderHeader) p  
PIVOT  
(  
COUNT (PurchaseOrderID)  
FOR EmployeeID IN  
( [250], [251], [256], [257], [260] )  
) AS pvt  
ORDER BY pvt.VendorID;  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
```
VendorID    Emp1        Emp2        Emp3        Emp4        Emp5  
----------- ----------- ----------- ----------- ----------- -----------
1492        2           5           4           4           4
1494        2           5           4           5           4
1496        2           4           4           5           5
1498        2           5           4           4           4
1500        3           4           4           5           4
```
  
 Los resultados devueltos por esta instrucción de subselección se dinamizan en la columna `EmployeeID`.  
  
```  
SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM PurchaseOrderHeader;  
```  
  
 Esto significa que los valores únicos devueltos por la columna `EmployeeID` se convierten en campos del conjunto de resultados finales. Por lo tanto, hay una columna para cada número de `EmployeeID` especificado en la cláusula dinámica: en este caso empleados `164`, `198`, `223`, `231` y `233`. La columna `PurchaseOrderID` se utiliza como columna de valores, respecto a la que se ordenan las columnas del resultado final, denominadas columnas de agrupamiento. En este caso, las columnas de agrupamiento se agregan mediante la función `COUNT`. Tenga presente que aparece un mensaje de advertencia que indica que los valores NULL que aparecen en la columna `PurchaseOrderID` no se tuvieron en cuenta cuando se contabilizó `COUNT` para cada empleado.  
  
> [!IMPORTANT]  
>  Cuando se usan funciones de agregado con `PIVOT`, la presencia de valores null en la columna de valor no se consideran al calcular una agregación.  
  
 `UNPIVOT`realiza casi la operación inversa de `PIVOT`, girando las columnas en filas. Suponga que la tabla producida en el ejemplo anterior se almacena en la base de datos como `pvt` y que desea girar los identificadores de columna `Emp1`, `Emp2`, `Emp3`, `Emp4` y `Emp5` a valores de fila que correspondan a un determinado proveedor. Esto significa que debe identificar dos columnas adicionales. La columna que contendrá los valores de columna que se están girando (`Emp1`, `Emp2`,...) se denominará `Employee` y la columna que contendrá los valores que residen actualmente en las columnas que se giran se denominará `Orders`. Estas columnas corresponden a la *pivot_column* y *value_column*, respectivamente, en la [!INCLUDE[tsql](../../includes/tsql-md.md)] definición. Esta es la consulta.  
  
```  
-- Create the table and insert values as portrayed in the previous example.  
CREATE TABLE pvt (VendorID int, Emp1 int, Emp2 int,  
    Emp3 int, Emp4 int, Emp5 int);  
GO  
INSERT INTO pvt VALUES (1,4,3,5,4,4);  
INSERT INTO pvt VALUES (2,4,1,5,5,5);  
INSERT INTO pvt VALUES (3,4,3,5,4,4);  
INSERT INTO pvt VALUES (4,4,2,5,5,4);  
INSERT INTO pvt VALUES (5,5,1,5,5,5);  
GO  
-- Unpivot the table.  
SELECT VendorID, Employee, Orders  
FROM   
   (SELECT VendorID, Emp1, Emp2, Emp3, Emp4, Emp5  
   FROM pvt) p  
UNPIVOT  
   (Orders FOR Employee IN   
      (Emp1, Emp2, Emp3, Emp4, Emp5)  
)AS unpvt;  
GO  
```  
  
 A continuación se muestra un conjunto parcial de resultados.  
  
```
VendorID    Employee    Orders
----------- ----------- ------
1            Emp1       4
1            Emp2       3 
1            Emp3       5
1            Emp4       4
1            Emp5       4
2            Emp1       4
2            Emp2       1
2            Emp3       5
2            Emp4       5
2            Emp5       5
...
```
  
 Tenga en cuenta que `UNPIVOT` no es justo lo contrario de `PIVOT`. `PIVOT`realiza una agregación y, por lo tanto, combina posibles múltiples filas en una sola fila en la salida. `UNPIVOT`no se reproduce el resultado de expresión con valores de tabla original porque se han mezclado filas. Además, valores nulos en la entrada de `UNPIVOT` desaparecen en la salida, mientras que haya valores null en la entrada antes de la `PIVOT` operación.  
  
 El `Sales.vSalesPersonSalesByFiscalYears` ver en el [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] usos de la base de datos de ejemplo `PIVOT` para devolver el total de ventas de cada vendedor, para cada año fiscal. En la vista de secuencias de comandos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en **Explorador de objetos**, localícela en la **vistas** carpeta para el [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos. Haga clic en el nombre de vista y, a continuación, seleccione **incluir vista como**.  
  
## <a name="see-also"></a>Vea también  
 [DESDE (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [CASO (Transact-SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
  

