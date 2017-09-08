---
title: DATEADD (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEADD
- DATEADD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- add interval to date or time [SQL Server]
- subtract interval from date or time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dates [SQL Server], intervals
- date and time [SQL Server], DATEADD
- DATEADD function [SQL Server]
ms.assetid: 89c5ae32-89c6-47e1-979e-15d97908b9f1
caps.latest.revision: 71
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6a90b51a1ef2156a2a05b8d3dd4e15111872edf6
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="dateadd-transact-sql"></a>DATEADD (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve un valor *fecha* con los valores especificados *número* intervalo (entero con signo) agregado a un determinado *datepart* de ese *fecha*.
  
Para obtener información general de todos los [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de datos de fecha y hora y funciones, vea [funciones y tipos de datos de hora y fecha &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATEADD (datepart , number , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*parte de fecha*  
Es la parte de *fecha* a la que un **entero***número* se agrega. La siguiente tabla se recogen válidos *datepart* argumentos. Los equivalentes de variables definidas por el usuario no son válidos.
  
|*parte de fecha*|Abreviaturas|  
|---|---|
|**año**|**AA**, **aaaa**|  
|**trimestre**|**TT**, **preguntas**|  
|**mes**|**mm**, **m**|  
|**DAYOFYEAR**|**dy**, **y**|  
|**día**|**dd**, **d.**|  
|**semana**|**wk**, **ww**|  
|**día de la semana**|**almacenamiento de datos**, **w**|  
|**hora**|**hh**|  
|**minuto**|**Mi**,**n**|  
|**segundo**|**ss**, **s**|  
|**milisegundo**|**MS**|  
|**microsegundos**|**MCS**|  
|**nanosegundos**|**NS**|  
  
*number*  
Es una expresión que se pueda resolver como un [int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md) que se agrega a un *datepart* de *fecha*. Las variables definidas por el usuario son válidas.  
Si especifica un valor con una fracción decimal, la fracción se trunca y no se redondea.
  
*date*  
Es una expresión que se pueda resolver como un **tiempo**, **fecha**, **smalldatetime**, **datetime**, **datetime2**, o **datetimeoffset** valor. *fecha* puede ser una expresión, la expresión de columna, la variable definida por el usuario o la cadena literal. Si la expresión es un literal de cadena, debe resolverse en un **datetime**. Para evitar ambigüedades, use años de cuatro dígitos. Para obtener información sobre los años de dos dígitos, consulte [configurar two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-types"></a>Tipos de valor devuelto
El tipo de datos devuelto es el tipo de datos de la *fecha* argumento, salvo los literales de cadena.
Tipo de datos devueltos para un literal de cadena es **datetime**. Se producirá un error si la escala de segundos del literal de cadena tiene más de tres posiciones (.nnn) o contiene la parte del ajuste de zona horaria.
  
## <a name="return-value"></a>Valor devuelto  
  
## <a name="datepart-argument"></a>Argumento datepart  
**DAYOFYEAR**, **día**, y **weekday** devuelven el mismo valor.
  
Cada *datepart* y sus abreviaturas devuelven el mismo valor.
  
Si *datepart* es **mes** y *fecha* mes tiene más días que el mes de retorno y la *fecha* día no existe en el mes de retorno se devuelve el último día del mes de retorno. Por ejemplo, septiembre tiene 30 días; por consiguiente, las dos instrucciones siguientes devuelven 2006-09-30 00:00:00.000:
  
```sql
SELECT DATEADD(month, 1, '2006-08-30');
SELECT DATEADD(month, 1, '2006-08-31');
```
  
## <a name="number-argument"></a>Argumento number  
El *número* argumento no puede superar el intervalo de **int**. En las instrucciones siguientes, el argumento para *número* supera el intervalo de **int** en 1. Se devuelve un mensaje de error que indica lo siguiente: "`Msg 8115, Level 16, State 2, Line 1. Arithmetic overflow error converting expression to data type int."`
  
```sql
SELECT DATEADD(year,2147483648, '2006-07-31');  
SELECT DATEADD(year,-2147483649, '2006-07-31');  
```  
  
## <a name="date-argument"></a>Argumento date  
El *fecha* no se puede incrementar el argumento en un valor fuera del intervalo de su tipo de datos. En las instrucciones siguientes, el *número* valor que se agrega a la *fecha* valor supera el intervalo de la *fecha* tipo de datos. Se devuelve un mensaje de error que indica lo siguiente: "`Msg 517, Level 16, State 1, Line 1 Adding a value to a 'datetime' column caused overflow`".
  
```sql
SELECT DATEADD(year,2147483647, '2006-07-31');  
SELECT DATEADD(year,-2147483647, '2006-07-31');  
```  
  
## <a name="return-values-for-a-smalldatetime-date-and-a-second-or-fractional-seconds-datepart"></a>Valores devueltos para una fecha smalldatetime y datepart de un segundo o fracciones de segundo  
La segunda parte de un [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) valor siempre es 00. Si *fecha* es **smalldatetime**, los casos siguientes:
-   Si *datepart* es **segundo** y *número* está comprendido entre-30 y +29, se realiza ninguna suma.  
-   Si *datepart* es **segundo** y *número* es menor que 30 o más de +29, adición se realiza a partir de un minuto.  
-   Si *datepart* es **milisegundo** y *número* está comprendido entre-30001 y + 29998, no se realiza ninguna suma.  
-   Si *datepart* es **milisegundo** y *número* es menor que -30001 o superior a + 29998, adición se realiza a partir de un minuto.  
  
## <a name="remarks"></a>Comentarios  
DATEADD se puede utilizar en la instrucción SELECT \<lista >, donde tiene, cláusulas GROUP BY y ORDER BY.
  
## <a name="fractional-seconds-precision"></a>Precisión de fracciones de segundo
Adición de un *datepart* de **microsegundos** o **nanosegundos** para *fecha* tipos de datos **smalldatetime**, **fecha**, y **datetime** no está permitido.
  
Los milisegundos tienen una escala de 3 (0,123), los microsegundos tienen una escala de 6 (0,123456) y los nanosegundos tienen una escala de 9 (0,123456789). El **tiempo**, **datetime2**, y **datetimeoffset** tipos de datos tienen una escala máxima de 7 (. 1234567). Si *datepart* es **nanosegundos**, *número* debe ser 100 antes de las fracciones de segundo de *fecha* aumentar. A *número* entre 1 y 49 se redondea hacia abajo a 0 y un número de 50 a 99 es redondeado hasta 100.
  
Las instrucciones siguientes agregan un *datepart* de **milisegundo**, **microsegundos**, o **nanosegundos**.
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT '1 millisecond', DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT '2 milliseconds', DATEADD(millisecond,2,@datetime2)  
UNION ALL  
SELECT '1 microsecond', DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT '2 microseconds', DATEADD(microsecond,2,@datetime2)  
UNION ALL  
SELECT '49 nanoseconds', DATEADD(nanosecond,49,@datetime2)  
UNION ALL  
SELECT '50 nanoseconds', DATEADD(nanosecond,50,@datetime2)  
UNION ALL  
SELECT '150 nanoseconds', DATEADD(nanosecond,150,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
1 millisecond     2007-01-01 13:10:10.1121111  
2 milliseconds    2007-01-01 13:10:10.1131111  
1 microsecond     2007-01-01 13:10:10.1111121  
2 microseconds    2007-01-01 13:10:10.1111131  
49 nanoseconds    2007-01-01 13:10:10.1111111  
50 nanoseconds    2007-01-01 13:10:10.1111112  
150 nanoseconds   2007-01-01 13:10:10.1111113  
```  
  
## <a name="time-zone-offset"></a>Ajuste de zona horaria
La suma no se permite para el ajuste de zona horaria.
  
## <a name="examples"></a>Ejemplos  

### <a name="a-incrementing-datepart-by-an-interval-of-1"></a>A. Aumentar datepart en un intervalo de 1  
Cada una de las instrucciones siguientes incrementa *datepart* en un intervalo de 1.
  
```sql
DECLARE @datetime2 datetime2 = '2007-01-01 13:10:10.1111111';  
SELECT 'year', DATEADD(year,1,@datetime2)  
UNION ALL  
SELECT 'quarter',DATEADD(quarter,1,@datetime2)  
UNION ALL  
SELECT 'month',DATEADD(month,1,@datetime2)  
UNION ALL  
SELECT 'dayofyear',DATEADD(dayofyear,1,@datetime2)  
UNION ALL  
SELECT 'day',DATEADD(day,1,@datetime2)  
UNION ALL  
SELECT 'week',DATEADD(week,1,@datetime2)  
UNION ALL  
SELECT 'weekday',DATEADD(weekday,1,@datetime2)  
UNION ALL  
SELECT 'hour',DATEADD(hour,1,@datetime2)  
UNION ALL  
SELECT 'minute',DATEADD(minute,1,@datetime2)  
UNION ALL  
SELECT 'second',DATEADD(second,1,@datetime2)  
UNION ALL  
SELECT 'millisecond',DATEADD(millisecond,1,@datetime2)  
UNION ALL  
SELECT 'microsecond',DATEADD(microsecond,1,@datetime2)  
UNION ALL  
SELECT 'nanosecond',DATEADD(nanosecond,1,@datetime2);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
Year         2008-01-01 13:10:10.1111111  
quarter      2007-04-01 13:10:10.1111111  
month        2007-02-01 13:10:10.1111111  
dayofyear    2007-01-02 13:10:10.1111111  
day          2007-01-02 13:10:10.1111111  
week         2007-01-08 13:10:10.1111111  
weekday      2007-01-02 13:10:10.1111111  
hour         2007-01-01 14:10:10.1111111  
minute       2007-01-01 13:11:10.1111111  
second       2007-01-01 13:10:11.1111111  
millisecond  2007-01-01 13:10:10.1121111  
microsecond  2007-01-01 13:10:10.1111121  
nanosecond   2007-01-01 13:10:10.1111111  
```  
  
### <a name="b-incrementing-more-than-one-level-of-datepart-in-one-statement"></a>B. Aumentar más de un nivel de datepart en una instrucción  
Cada una de las instrucciones siguientes incrementa *datepart* por una *número* lo suficientemente grande para también incrementar la próxima superior *datepart* de *fecha*.
  
```sql
DECLARE @datetime2 datetime2;  
SET @datetime2 = '2007-01-01 01:01:01.1111111';  
--Statement                                 Result     
-------------------------------------------------------------------   
SELECT DATEADD(quarter,4,@datetime2);     --2008-01-01 01:01:01.110  
SELECT DATEADD(month,13,@datetime2);      --2008-02-01 01:01:01.110  
SELECT DATEADD(dayofyear,365,@datetime2); --2008-01-01 01:01:01.110  
SELECT DATEADD(day,365,@datetime2);       --2008-01-01 01:01:01.110  
SELECT DATEADD(week,5,@datetime2);        --2007-02-05 01:01:01.110  
SELECT DATEADD(weekday,31,@datetime2);    --2007-02-01 01:01:01.110  
SELECT DATEADD(hour,23,@datetime2);       --2007-01-02 00:01:01.110  
SELECT DATEADD(minute,59,@datetime2);     --2007-01-01 02:00:01.110  
SELECT DATEADD(second,59,@datetime2);     --2007-01-01 01:02:00.110  
SELECT DATEADD(millisecond,1,@datetime2); --2007-01-01 01:01:01.110  
```  
  
### <a name="c-using-expressions-as-arguments-for-the-number-and-date-parameters"></a>C. Utilizar las expresiones como argumentos para los parámetros number y date  
Los ejemplos siguientes usan diferentes tipos de expresiones como argumentos para la *número* y *fecha* parámetros. Los ejemplos utilizan la base de datos de AdventureWorks.
  
#### <a name="specifying-a-column-as-date"></a>Especificar una columna como fecha  
En el ejemplo siguiente se agregan `2` días a cada valor de la columna `OrderDate` para derivar una nueva columna denominada `PromisedShipDate`.
  
```sql
SELECT SalesOrderID  
    ,OrderDate   
    ,DATEADD(day,2,OrderDate) AS PromisedShipDate  
FROM Sales.SalesOrderHeader;  
```  
  
A continuación se muestra un conjunto parcial de resultados.
  
```sql
SalesOrderID OrderDate               PromisedShipDate  
------------ ----------------------- -----------------------  
43659        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43660        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
43661        2005-07-01 00:00:00.000 2005-07-03 00:00:00.000  
...  
43702        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43703        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43704        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43705        2005-07-02 00:00:00.000 2005-07-04 00:00:00.000  
43706        2005-07-03 00:00:00.000 2005-07-05 00:00:00.000  
...  
43711        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
43712        2005-07-04 00:00:00.000 2005-07-06 00:00:00.000  
...  
43740        2005-07-11 00:00:00.000 2005-07-13 00:00:00.000  
43741        2005-07-12 00:00:00.000 2005-07-14 00:00:00.000  
  
```  
  
#### <a name="specifying-user-defined-variables-as-number-and-date"></a>Especificar las variables definidas por el usuario como number y date  
En el ejemplo siguiente se especifica variables definidas por el usuario como argumentos para *número* y *fecha*.
  
```sql
DECLARE @days int = 365,   
        @datetime datetime = '2000-01-01 01:01:01.111'; /* 2000 was a leap year */;  
SELECT DATEADD(day, @days, @datetime);  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
-----------------------  
2000-12-31 01:01:01.110  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-system-function-as-date"></a>Especificar la función de sistema escalar como date  
En el ejemplo siguiente se especifica `SYSDATETIME` para *fecha*.
  
```sql
SELECT DATEADD(month, 1, SYSDATETIME());  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
---------------------------  
2013-02-06 14:29:59.6727944  
  
(1 row(s) affected)  
```  
  
#### <a name="specifying-scalar-subqueries-and-scalar-functions-as-number-and-date"></a>Especificar subconsultas y funciones escalares como number y date  
En el ejemplo siguiente se usa subconsultas escalares, `MAX(ModifiedDate)`, como argumentos para *número* y *fecha*. `(SELECT TOP 1 BusinessEntityID FROM Person.Person)`es un argumento artificial para el parámetro de número mostrar cómo seleccionar una *número* argumento de una lista de valores.
  
```sql
SELECT DATEADD(month,(SELECT TOP 1 BusinessEntityID FROM Person.Person),  
    (SELECT MAX(ModifiedDate) FROM Person.Person));  
```  
  
#### <a name="specifying-numeric-expressions-and-scalar-system-functions-as-number-and-date"></a>Especificar expresiones numéricas y funciones del sistema escalares como number y date  
En el ejemplo siguiente se utiliza una expresión numérica (-`(10/2))`, [operadores unarios](../../mdx/unary-operators.md) (`-`), una [operador aritmético](../../mdx/arithmetic-operators.md) (`/`) y funciones de sistema escalares (`SYSDATETIME`) como argumentos para *número* y *fecha*.
  
```sql
SELECT DATEADD(month,-(10/2), SYSDATETIME());  
```  
  
#### <a name="specifying-ranking-functions-as-number"></a>Especificar las funciones de clasificación como number  
En el ejemplo siguiente se usa una función de clasificación como argumentos para *número*.
  
```sql
SELECT p.FirstName, p.LastName  
    ,DATEADD(day,ROW_NUMBER() OVER (ORDER BY  
        a.PostalCode),SYSDATETIME()) AS 'Row Number'  
FROM Sales.SalesPerson AS s   
    INNER JOIN Person.Person AS p   
        ON s.BusinessEntityID = p.BusinessEntityID  
    INNER JOIN Person.Address AS a   
        ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
```  
  
#### <a name="specifying-an-aggregate-window-function-as-number"></a>Especificar una función de ventana agregada como number  
En el ejemplo siguiente se utiliza una función de ventana agregada como un argumento para *número*.
  
```sql
SELECT SalesOrderID, ProductID, OrderQty  
    ,DATEADD(day,SUM(OrderQty)   
        OVER(PARTITION BY SalesOrderID),SYSDATETIME()) AS 'Total'  
FROM Sales.SalesOrderDetail   
WHERE SalesOrderID IN(43659,43664);  
GO  
```  
  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


