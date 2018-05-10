---
title: DATEPART (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DATEPART_TSQL
- DATEPART
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- date and time [SQL Server], DATEPART
- dateparts [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
- dateparts [SQL Server], datepart
- comparing dates times [SQL Server]
- DATEPART function [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 15f1a5bc-4c0c-4c48-848d-8ec03473e6c1
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: eee173d268af8e18343c286bda29384b2a327860
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve un entero que representa el parámetro *datepart* especificado del parámetro *date* especificada.
  
Para ver información general sobre todos los tipos de datos y funciones de fecha y hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], vea [Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
Es la parte de *date* (una fecha u hora) para la que se devolverá un valor **integer**. En esta tabla se enumeran los argumentos válidos de *datepart*. Los equivalentes de variables definidas por el usuario no son válidos.
  
|*datepart*|Abreviaturas|  
|---|---|
|**year**|**yy**, **yyyy**|  
|**quarter**|**qq**, **q**|  
|**month**|**mm**, **m**|  
|**dayofyear**|**dy**, **y**|  
|**day**|**dd**, **d**|  
|**week**|**wk**, **ww**|  
|**weekday**|**dw**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss**, **s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**isowk**, **isoww**|  
  
*date*  
Es una expresión que se puede resolver en un valor **time**, **date**, **smalldatetime**, **datetime**, **datetime2** o **datetimeoffset**. *date* puede ser una expresión, una expresión de columna, una variable definida por el usuario o un literal de cadena.  
Para evitar ambigüedades, use años de cuatro dígitos. Para más información, vea [Establecer la opción de configuración del servidor Fecha límite de año de dos dígitos](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Tipo devuelto  
 **int**  
  
## <a name="return-value"></a>Valor devuelto  
Cada *datepart* y sus abreviaturas devuelven el mismo valor.
  
El valor devuelto depende del entorno del idioma definido por [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) y de [Establecer la opción de configuración del servidor Idioma predeterminado](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) del inicio de sesión. Si *date* es un literal de cadena en algunos formatos, el valor devuelto depende del formato especificado mediante [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md). SET DATEFORMAT no afecta al valor devuelto cuando la fecha es una expresión de columna de un tipo de datos de hora o fecha.
  
En la siguiente tabla se enumeran todos los argumentos *datepart* con los correspondientes valores devueltos para la instrucción `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')`. El tipo de datos del argumento *date* es **datetimeoffset(7)**. El valor devuelto **nanosecond***datepart* tiene una escala de 9 (,123456700) y las dos últimas posiciones son siempre 00.
  
|*datepart*|Valor devuelto|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|10|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|45|  
|**weekday, dw**|1|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>Argumentos de la parte de fecha semana y día de la semana
Si *datepart* es **week** (**wk**, **ww**) o **weekday** (**dw**), el valor devuelto depende del valor que se ha definido mediante [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
El 1 de enero de cualquier año define el número inicial de **week***datepart*; por ejemplo: DATEPART (** wk, 'Jan 1, *xxx*x') = 1, donde *xxxx* es cualquier año.
  
En la tabla siguiente se enumeran los valores devueltos para **week** y *weekdaydatepart* para '2007-04-21 ' para cada argumento SET DATEFIRST. El 1 de enero es un lunes del año 2007. El 21 de abril es sábado en el año 2007. El valor predeterminado para inglés de EE.UU. es SET DATEFIRST 7, Sunday Inglés.
  
|SET DATEFIRST<br /><br /> argumento|week<br /><br /> devuelto|weekday<br /><br /> devuelto|  
|---|---|---|
|1|16|6|  
|2|17|5|  
|3|17|4|  
|4|17|3|  
|5|17|2|  
|6|17|1|  
|7|16|7|  
  
## <a name="year-month-and-day-datepart-arguments"></a>Argumentos de datepart year, month y day  
Los valores devueltos mediante DATEPART (**year**, *date*), DATEPART (**month**, *date*) y DATEPART (**day**, *date*) son los mismos que los que devuelven las funciones [YEAR](../../t-sql/functions/year-transact-sql.md), [MONTH](../../t-sql/functions/month-transact-sql.md) y [DAY](../../t-sql/functions/day-transact-sql.md), respectivamente.
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
ISO 8601 incluye el sistema ISO de fecha-semana, un sistema de numeración para las semanas. Cada semana se asocia al año en el que cae el jueves. Por ejemplo, la semana 1 de 2004 (2004W01) abarca del lunes 29 de diciembre de 2003 al domingo 4 de enero de 2004. El número de semana más alto en un año puede ser 52 o 53. Este estilo de numeración se utiliza normalmente en los países europeos, pero es poco frecuente en otros países.
  
Es posible que el sistema de numeración usado en varios países no se ajuste a las normas ISO. Existen por lo menos seis posibilidades, como se muestra en la tabla siguiente
  
|Primer día de la semana|La primera semana del año contiene|Semanas asignadas dos veces|Usado por/en|  
|---|---|---|---|
|Domingo|1 de enero,<br /><br /> El primer sábado,<br /><br /> 1–7 días del año|Sí|United States|  
|Lunes|1 de enero,<br /><br /> El primer domingo,<br /><br /> 1–7 días del año|Sí|La mayoría de los países europeos y Reino Unido|  
|Lunes|4 de enero,<br /><br /> El primer jueves,<br /><br /> 4–7 días del año|no|ISO 8601, Noruega y Suecia|  
|Lunes|7 de enero,<br /><br /> El primer lunes,<br /><br /> 7 días del año|no||  
|Miércoles|1 de enero,<br /><br /> El primer martes,<br /><br /> 1–7 días del año|Sí||  
|Sábado|1 de enero,<br /><br /> El primer viernes,<br /><br /> 1–7 días del año|Sí||  
  
## <a name="tzoffset"></a>TZoffset  
**TZoffset** (**tz**) se devuelve como el número de minutos (con signo). La instrucción siguiente devuelve un ajuste de zona horaria de 310 minutos.
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
El valor TZoffset se representa así:
- Para datetimeoffset y datetime2, TZoffset devuelve el desplazamiento de tiempo en minutos, donde el desplazamiento de datetime2 siempre es 0 minutos.
- Para los tipos de datos que se pueden convertir implícitamente a datetimeoffset o datetime2, con la excepción de los otros tipos de datos de fecha y hora, devuelve el desplazamiento de tiempo en minutos.
- El resto de tipos de parámetros producirán un error.
  
  
## <a name="smalldatetime-date-argument"></a>Argumento date smalldatetime  
Si *date* es [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), los segundos se devuelven como 00.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>Valor predeterminado devuelto por una parte de fecha que no se encuentra en un argumento date  
Si el tipo de datos del argumento *date* no contiene el parámetro *datepart* especificado, se devolverá el valor predeterminado *datepart* solo cuando se especifique un valor literal para *date*.
  
Por ejemplo, el valor predeterminado de año-mes-día de cualquier tipo de datos **date** es 1900-01-01. La instrucción siguiente tiene argumentos de la parte de fecha para *datepart*, un argumento de tiempo para *date* y devuelve `1900, 1, 1, 1, 2`.
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
Si *date* se especifica como variable o como columna de tabla y el tipo de datos de esa variable o columna no tiene especificado *datepart*, se devuelve el error 9810. En el ejemplo de código siguiente se produce un error porque la parte de fecha de año no es válida para el tipo de datos **time** que se declara para la variable *@t*.
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>Fracciones de segundo
Las fracciones de segundo se devuelven como se indica en la instrucción siguiente:
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>Notas  
Se puede utilizar DATEPART en la lista de selección, cláusulas WHERE, HAVING, GROUP BY y ORDER BY.
  
En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATEPART convierte implícitamente los literales de cadena como un tipo **datetime2**. Esto significa que DATEPART no admite el formato año-día-mes cuando se pasa la fecha como cadena. La cadena se debe convertir explícitamente a un tipo **datetime** o **smalldatetime** para poder usar el formato año-día-mes.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se devuelve el año de base. El año de base es útil para calcular fechas. En el ejemplo siguiente, la fecha se especifica como un número. Observe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta 0 como el 1 de enero de 1900.
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
En el siguiente ejemplo se devuelve el día de la fecha `12/20/1974`.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
20
```  
  
En el siguiente ejemplo se devuelve el año de la fecha `12/20/1974`.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
--------
1974
```  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  
