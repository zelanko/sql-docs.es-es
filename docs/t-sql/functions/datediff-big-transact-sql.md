---
title: DATEDIFF_BIG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATEDIFF_BIG
- DATEDIFF_BIG_TSQL
helpviewer_keywords:
- DATEDIFF_BIG function [SQL Server]
- dates [SQL Server]. functions
- date and time [SQL Server], DATEDIFF_BIG
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 19ac1693-3cfa-400d-bf83-20a9cb46599a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6c8228f0db3e37fe3bf6425d60fd4f9067e92220
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="datediffbig-transact-sql"></a>DATEDIFF_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Devuelve el recuento (entero grande con firma) de los límites *datepart* que se han cruzado entre los valores *startdate* y *enddate* especificados.
  
Para ver información general sobre todos los tipos de datos y funciones de fecha y hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], vea [Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
  
DATEDIFF_BIG ( datepart , startdate , enddate )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
Es la parte de *startdate* y *enddate* que especifica el tipo de límite cruzado. En esta tabla se enumeran los argumentos válidos de *datepart*. Los equivalentes de variables definidas por el usuario no son válidos.
  
|*datepart*|Abreviaturas|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
  
*startdate*  
Es una expresión que se puede resolver en un valor **time**, **date**, **smalldatetime**, **datetime**, **datetime2** o **datetimeoffset**. *date* puede ser una expresión, una expresión de columna, una variable definida por el usuario o un literal de cadena. *startdate* se resta de *enddate*.  
Para evitar ambigüedades, use años de cuatro dígitos. Para más información, vea [Establecer la opción de configuración del servidor Fecha límite de año de dos dígitos](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
*enddate*  
Vea *startdate*.
  
## <a name="return-type"></a>Tipo devuelto  
 Firmado   
        **bigint**  
  
## <a name="return-value"></a>Valor devuelto  
Devuelve el recuento (entero grande con firma) de los límites datepart que se han cruzado entre los valores startdate y enddate especificados.
-   Cada *datepart* y sus abreviaturas devuelven el mismo valor.  
  
Si el valor devuelto está fuera del intervalo de **bigint** (de -9.223.372.036.854.775.808 a +9.223.372.036.854.775.807), se devuelve un error. En **millisecond**, la diferencia máxima entre *startdate* y *enddate* es de 24 días, 20 horas, 31 minutos y 23.647 segundos. En **second**, la diferencia máxima es de 68 años.
  
Si *startdate* y *enddate* tienen asignado solo un valor de tiempo y *datepart* no es un *datepart* de tiempo, se devuelve 0.
  
Un componente de ajuste de zona horaria de *startdate* o *endate* no se usa para calcular el valor devuelto.
  
Puesto que [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md) solo es preciso hasta los minutos, cuando se use un valor **smalldatetime** en *startdate* o *enddate*, los segundos y milisegundos siempre se establecen en 0 en el valor devuelto.
  
Si solo se asigna un valor de tiempo a una variable de un tipo de datos de fecha, el valor de la parte de la fecha que falta se establece en el valor predeterminado: 1900-01-01. Si solo se asigna un valor de fecha a una variable de un tipo de datos de fecha u hora, el valor de la parte de la hora que falta se establece en el valor predeterminado: 00:00:00. Si *startdate* o *enddate* tienen solo una parte de hora y el otro solo una parte de la fecha, las partes de la hora que y la fecha que faltan se establecen en los valores predeterminados.
  
Si *startdate* y *enddate* son de tipos de datos de fecha diferentes y uno tiene más partes de hora o precisión de fracciones de segundo que el otro, las partes que faltan del otro se establecen en 0.
  
## <a name="datepart-boundaries"></a>Límites de datepart
Las siguientes instrucciones tienen el mismo valor *startdate* y el mismo valor *endate*. Esas fechas son adyacentes y difieren y tienen una diferencia horaria de 0,0000001 segundos. La diferencia entre *startdate* y *endate* en cada instrucción cruza un límite de calendario u hora de su *datepart*. Cada instrucción devuelve 1. Si se usan años diferentes en este ejemplo y si tanto *startdate* como *endate* están en la misma semana del calendario, el valor devuelto para **week** será 0.

```sql
SELECT DATEDIFF_BIG(year, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(quarter, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(month, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(dayofyear, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(day, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(week, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(hour, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(minute, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(second, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
SELECT DATEDIFF_BIG(millisecond, '2005-12-31 23:59:59.9999999', '2006-01-01 00:00:00.0000000');
```
  
## <a name="remarks"></a>Notas  
DATEDIFF_BIG se puede usar en la lista de selección y en las cláusulas WHERE, HAVING, GROUP BY y ORDER BY.
  
DATEDIFF_BIG convierte implícitamente los literales de cadena como un tipo **datetime2**. Esto significa que DATEDIFF_BIG no admite el formato año-día-mes cuando se pasa la fecha como cadena. La cadena se debe convertir explícitamente a un tipo **datetime** o **smalldatetime** para poder usar el formato año-día-mes.
  
La especificación de SET DATEFIRST no tiene efecto en DATEDIFF_BIG. DATEDIFF_BIG siempre usa Domingo como el primer día de la semana para garantizar que la función es determinística.
  
## <a name="examples"></a>Ejemplos  
En los siguientes ejemplos se usan diferentes tipos de expresiones como argumentos para los parámetros *startdate* y *enddate*.
  
### <a name="specifying-columns-for-startdate-and-enddate"></a>Especificar las columnas para startdate y enddate  
El ejemplo siguiente calcula el número de límites de día que se cruzan entre las fechas en dos columnas de una tabla.
  
```sql
CREATE TABLE dbo.Duration  
    (  
    startDate datetime2  
    ,endDate datetime2  
    );  
INSERT INTO dbo.Duration(startDate,endDate)  
    VALUES('2007-05-06 12:10:09','2007-05-07 12:10:09');  
SELECT DATEDIFF_BIG(day,startDate,endDate) AS 'Duration'  
FROM dbo.Duration;  
-- Returns: 1  
```  
  
Para ver otros muchos ejemplos, vea los ejemplos estrechamente relacionados en [DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md).
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[DATEDIFF &#40;Transact-SQL&#41;](../../t-sql/functions/datediff-transact-sql.md)
  
  
