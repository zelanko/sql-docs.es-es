---
title: COALESCE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COALESCE
- COALESCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], nonnull
- COALESCE function
- first nonnull expressions [SQL Server]
- nonnull expressions
ms.assetid: fafc0dba-f8a8-4aad-9b7f-908e34b74d88
caps.latest.revision: 52
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d597c347b0b608b69c5d435fbf58b2779d462a32
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="coalesce-transact-sql"></a>COALESCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Evalúa los argumentos en orden y devuelve el valor actual de la primera expresión que inicialmente no se evalúa como `NULL`. Por ejemplo, `SELECT COALESCE(NULL, NULL, 'third_value', 'fourth_value');` devuelve el tercer valor porque el tercer valor es el primer valor que no sea null. 
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
COALESCE ( expression [ ,...n ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es un [expresión](../../t-sql/language-elements/expressions-transact-sql.md) de cualquier tipo.  
  
## <a name="return-types"></a>Tipos devueltos  
 Devuelve el tipo de datos de *expresión* con la mayor prioridad de tipo de datos. Si ninguna de las expresiones admiten valores NULL, el resultado tiene un tipo que no admite valores NULL.  
  
## <a name="remarks"></a>Comentarios  
 Si todos los argumentos son `NULL`, `COALESCE` devuelve `NULL`. Al menos uno de los valores null debe ser un tipo `NULL`.  
  
## <a name="comparing-coalesce-and-case"></a>Comparar COALESCE y CASE  
 El `COALESCE` expresión es un método abreviado sintáctico de la `CASE` expresión.  Es decir, el código `COALESCE`(*expression1*,*.. .n*) se ha reescrito por el optimizador de consultas de la siguiente `CASE` expresión:  
  
 ```sql  
 CASE  
 WHEN (expression1 IS NOT NULL) THEN expression1  
 WHEN (expression2 IS NOT NULL) THEN expression2  
 ...  
 ELSE expressionN  
 END  
 ```  
  
 Esto significa que los valores de entrada (*expression1*, *expression2*, *expresiónn*, etc.) se evalúan varias veces. Además, de acuerdo con el estándar SQL, si una expresión de valor contiene una subconsulta se considera no determinista, y la subconsulta se evalúa dos veces. En cualquier caso, se pueden devolver resultados diferentes entre la primera evaluación y las evaluaciones posteriores.  
  
 Por ejemplo, cuando se ejecuta el código `COALESCE((subquery), 1)`, la subconsulta se evalúa dos veces. En consecuencia, podrá obtener resultados diferentes en función del nivel de aislamiento de la consulta. Por ejemplo, puede devolver el código `NULL` en el `READ COMMITTED` nivel de aislamiento en un entorno multiusuario. Para asegurarse de que se devuelven resultados estables, use la `SNAPSHOT ISOLATION` nivel de aislamiento o reemplazar `COALESE` con el `ISNULL` función. Como alternativa, puede volver a escribir la consulta para insertar la subconsulta en una subselección como se muestra en el ejemplo siguiente:  
  
```sql  
SELECT CASE WHEN x IS NOT NULL THEN x ELSE 1 END  
from  
(  
SELECT (SELECT Nullable FROM Demo WHERE SomeCol = 1) AS x  
) AS T;  
  
```  
  
## <a name="comparing-coalesce-and-isnull"></a>Comparar COALESCE e ISNULL  
 El `ISNULL` función y el `COALESCE` expresión tienen una finalidad similar pero pueden comportarse de manera diferente.  
  
1.  Dado que `ISNULL` es una función, se evalúa solo una vez.  Como se describió anteriormente, los valores de la entrada para el `COALESCE` expresiones se pueden evaluar varias veces.  
  
2.  La determinación del tipo de datos de la expresión resultante es diferente. `ISNULL`usa el tipo de datos del primer parámetro, `COALESCE` sigue el `CASE` reglas de expresión y devuelve el tipo de datos del valor con la prioridad más alta.  
  
3.  La nulabilidad de la expresión de resultado es diferente para `ISNULL` y `COALESCE`. El `ISNULL` devuelven el valor siempre se considera no acepta valores null (suponiendo que el valor devuelto es uno que no aceptan valores NULL), mientras que `COALESCE` con parámetros distintos de null se considera `NULL`. Por lo que las expresiones `ISNULL(NULL, 1)` y `COALESCE(NULL, 1)`, aunque equivalentes, tienen valores de nulabilidad diferentes. Esto hace que una diferencia si se utiliza estas expresiones en las columnas calculadas, crear restricciones de clave o hacer que el valor devuelto de una UDF escalar determinista para que se pueden indizar como se muestra en el ejemplo siguiente:  
  
    ```sql  
    USE tempdb;  
    GO  
    -- This statement fails because the PRIMARY KEY cannot accept NULL values  
    -- and the nullability of the COALESCE expression for col2   
    -- evaluates to NULL.  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0) PRIMARY KEY,   
    col3 AS ISNULL(col1, 0)   
    );   
  
    -- This statement succeeds because the nullability of the   
    -- ISNULL function evaluates AS NOT NULL.  
  
    CREATE TABLE #Demo   
    (   
    col1 integer NULL,   
    col2 AS COALESCE(col1, 0),   
    col3 AS ISNULL(col1, 0) PRIMARY KEY   
    );  
    ```  
  
4.  Validaciones de `ISNULL` y `COALESCE` también son diferentes. Por ejemplo, un `NULL` valor `ISNULL` se convierte en **int** , mientras que para `COALESCE`, debe proporcionar un tipo de datos.  
  
5.  `ISNULL`toma dos parámetros, mientras que `COALESCE` toma un número variable de parámetros.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-running-a-simple-example"></a>A. Ejecutar un ejemplo sencillo  
 En el ejemplo siguiente se muestra cómo `COALESCE` selecciona los datos de la primera columna que tiene un valor no nulo. En este ejemplo se usa la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
SELECT Name, Class, Color, ProductNumber,  
COALESCE(Class, Color, ProductNumber) AS FirstNotNull  
FROM Production.Product;  
```  
  
### <a name="b-running-a-complex-example"></a>B. Ejecutar un ejemplo complejo  
 En este ejemplo, la tabla `wages` incluye tres columnas con información acerca del sueldo anual de los empleados: la tarifa por hora, el salario y la comisión. No obstante, un empleado recibe solo un tipo de sueldo. Para determinar el importe total pagado a todos los empleados, utilice `COALESCE` para obtener solo los valores no NULL que se encuentran en `hourly_wage`, `salary` y `commission`.  
  
```sql  
SET NOCOUNT ON;  
GO  
USE tempdb;  
IF OBJECT_ID('dbo.wages') IS NOT NULL  
    DROP TABLE wages;  
GO  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   identity,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
GO  
INSERT dbo.wages (hourly_wage, salary, commission, num_sales)  
VALUES  
    (10.00, NULL, NULL, NULL),  
    (20.00, NULL, NULL, NULL),  
    (30.00, NULL, NULL, NULL),  
    (40.00, NULL, NULL, NULL),  
    (NULL, 10000.00, NULL, NULL),  
    (NULL, 20000.00, NULL, NULL),  
    (NULL, 30000.00, NULL, NULL),  
    (NULL, 40000.00, NULL, NULL),  
    (NULL, NULL, 15000, 3),  
    (NULL, NULL, 25000, 2),  
    (NULL, NULL, 20000, 6),  
    (NULL, NULL, 14000, 4);  
GO  
SET NOCOUNT OFF;  
GO  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS money) AS 'Total Salary'   
FROM dbo.wages  
ORDER BY 'Total Salary';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```   
 Total Salary  
 ------------  
 10000.00  
 20000.00  
 20800.00  
 30000.00  
 40000.00  
 41600.00  
 45000.00  
 50000.00  
 56000.00  
 62400.00  
 83200.00  
 120000.00  
  
 (12 row(s) affected)
 ```  
  
### <a name="c-simple-example"></a>C: ejemplo sencillo de  
 En el ejemplo siguiente se muestra cómo `COALESCE` selecciona los datos de la primera columna que tiene un valor distinto de null. Para este ejemplo, supongamos que la `Products` tabla contiene estos datos:  
  
 ```  
 Name         Color      ProductNumber  
 ------------ ---------- -------------  
 Socks, Mens  NULL       PN1278  
 Socks, Mens  Blue       PN1965  
 NULL         White      PN9876
 ```  
  
 A continuación, ejecutar la siguiente consulta de combinación:  
  
```sql  
SELECT Name, Color, ProductNumber, COALESCE(Color, ProductNumber) AS FirstNotNull   
FROM Products ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 Name         Color      ProductNumber  FirstNotNull  
 ------------ ---------- -------------  ------------  
 Socks, Mens  NULL       PN1278         PN1278  
 Socks, Mens  Blue       PN1965         Blue  
 NULL         White      PN9876         White
 ```  
  
 Observe que en la primera fila, el `FirstNotNull` valor es `PN1278`, no `Socks, Mens`. Esto es porque el `Name` columna no se especifica como un parámetro para `COALESCE` en el ejemplo.  
  
### <a name="d-complex-example"></a>D: ejemplo complejo  
 En el ejemplo siguiente se utiliza `COALESCE` para comparar los valores de tres columnas y devolver solo el valor de no null que se encuentran en las columnas.  
  
```sql  
CREATE TABLE dbo.wages  
(  
    emp_id        tinyint   NULL,  
    hourly_wage   decimal   NULL,  
    salary        decimal   NULL,  
    commission    decimal   NULL,  
    num_sales     tinyint   NULL  
);  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (1, 10.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (2, 20.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (3, 30.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (4, 40.00, NULL, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (5, NULL, 10000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (6, NULL, 20000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (7, NULL, 30000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (8, NULL, 40000.00, NULL, NULL);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (9, NULL, NULL, 15000, 3);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (10,NULL, NULL, 25000, 2);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (11, NULL, NULL, 20000, 6);  
  
INSERT INTO dbo.wages (emp_id, hourly_wage, salary, commission, num_sales)  
VALUES (12, NULL, NULL, 14000, 4);  
  
SELECT CAST(COALESCE(hourly_wage * 40 * 52,   
   salary,   
   commission * num_sales) AS decimal(10,2)) AS TotalSalary   
FROM dbo.wages  
ORDER BY TotalSalary;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Total Salary  
 ------------  
 10000.00  
 20000.00  
 20800.00  
 30000.00  
 40000.00  
 41600.00  
 45000.00  
 50000.00  
 56000.00  
 62400.00  
 83200.00  
 120000.00
 ```  
  
## <a name="see-also"></a>Vea también  
 [ISNULL &#40; Transact-SQL &#41;](../../t-sql/functions/isnull-transact-sql.md)   
 [CASE &#40;Transact-SQL&#41;](../../t-sql/language-elements/case-transact-sql.md)  
  
  

