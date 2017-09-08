---
title: DATEPART (Transact-SQL) | Documentos de Microsoft
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 05547f2dd50d7f130438d6a07b6952b8c29ec816
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="datepart-transact-sql"></a>DATEPART (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve un entero que representa el parámetro *datepart* del elemento especificado *fecha*.
  
Para obtener información general de todos los [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de datos de fecha y hora y funciones, vea [funciones y tipos de datos de hora y fecha &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DATEPART ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*parte de fecha*  
Es la parte de *fecha* (un valor de fecha u hora) para el que un **entero** se devolverá. La siguiente tabla se recogen válidos *datepart* argumentos. Los equivalentes de variables definidas por el usuario no son válidos.
  
|*parte de fecha*|Abreviaturas|  
|---|---|
|**año**|**AA**, **aaaa**|  
|**trimestre**|**TT**, **preguntas**|  
|**mes**|**mm**, **m**|  
|**DAYOFYEAR**|**dy**, **y**|  
|**día**|**dd**, **d.**|  
|**semana**|**wk**, **ww**|  
|**día de la semana**|**almacenamiento de datos**|  
|**hora**|**hh**|  
|**minuto**|**Mi, n**|  
|**segundo**|**ss**, **s**|  
|**milisegundo**|**MS**|  
|**microsegundos**|**MCS**|  
|**nanosegundos**|**NS**|  
|**TZoffset**|**TZ**|  
|**ISO_WEEK**|**isowk**, **isoww**|  
  
*date*  
Es una expresión que se pueda resolver como un **tiempo**, **fecha**, **smalldatetime**, **datetime**, **datetime2**, o **datetimeoffset** valor. *fecha* puede ser una expresión, la expresión de columna, la variable definida por el usuario o la cadena literal.  
Para evitar ambigüedades, use años de cuatro dígitos. Para obtener información sobre los años de dos dígitos, consulte [configurar two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Tipo devuelto  
 **int**  
  
## <a name="return-value"></a>Valor devuelto  
Cada *datepart* y sus abreviaturas devuelven el mismo valor.
  
El valor devuelto depende del entorno del idioma definido mediante el uso de [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) y la [configurar la opción de configuración de servidor idioma predeterminado](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) del inicio de sesión. Si *fecha* es una cadena literal en algunos formatos, el valor devuelto depende del formato especificado mediante el uso de [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md). SET DATEFORMAT no afecta al valor devuelto cuando la fecha es una expresión de columna de un tipo de datos de hora o fecha.
  
En la tabla siguiente se enumera todos los *datepart* argumentos con el correspondiente devuelven valores para la instrucción `SELECT DATEPART(datepart,'2007-10-30 12:15:32.1234567 +05:10')`. Tipo de datos de la *fecha* argumento es **datetimeoffset(7)**. El **nanosegundos***datepart* devolver valor tiene una escala de 9 (. 123456700) y las dos últimas posiciones son siempre 00.
  
|*parte de fecha*|Valor devuelto|  
|---|---|
|**año, aaaa, AA**|2007|  
|**trimestre, p, q**|4|  
|**mes, mm, m**|10|  
|**DAYOFYEAR, dy, y**|303|  
|**día, dd, d**|30|  
|**semana, wk, ww**|45|  
|**día de la semana, almacenamiento de datos**|1|  
|**hora, hh**|12|  
|**minuto, n**|15|  
|**segundo, ss, s**|32|  
|**milisegundo, ms**|123|  
|**microsegundos, mcs**|123456|  
|**nanosegundos, ns**|123456700|  
|**TZoffset, tz**|310|  
  
## <a name="week-and-weekday-datepart-arguments"></a>Argumentos de datepart de la semana y día de la semana
Cuando *datepart* es **semana** (**wk**, **ww**) o **weekday** (**dw**), el valor devuelto depende del valor que se establece mediante [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
El 1 de enero de cualquier año define el número inicial de la **semana***datepart*, por ejemplo: DATEPART (**wk**, ' 1 de Jan, *xxx*x') = 1, donde *xxxx* es cualquier año.
  
En la tabla siguiente enumera el valor devuelto de **semana** y **weekday***datepart* para ' 2007-04-21' para cada argumento de SET DATEFIRST. El 1 de enero es un lunes del año 2007. El 21 de abril es sábado en el año 2007. El valor predeterminado para inglés de EE.UU. es SET DATEFIRST 7, Sunday Inglés.
  
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
Los valores que se devuelven para DATEPART (**año**, *fecha*), DATEPART (**mes**, *fecha*) y DATEPART (**día** , *fecha*) son los mismos que los devueltos por las funciones [año](../../t-sql/functions/year-transact-sql.md), [mes](../../t-sql/functions/month-transact-sql.md), y [día](../../t-sql/functions/day-transact-sql.md), f respectivamente.
  
## <a name="isoweek-datepart"></a>ISO_WEEK datepart  
ISO 8601 incluye el sistema ISO de fecha-semana, un sistema de numeración para las semanas. Cada semana se asocia al año en el que cae el jueves. Por ejemplo, la semana 1 de 2004 (2004W01) abarca del lunes 29 de diciembre de 2003 al domingo 4 de enero de 2004. El número de semana más alto en un año puede ser 52 o 53. Este estilo de numeración se utiliza normalmente en los países europeos, pero es poco frecuente en otros países.
  
Es posible que el sistema de numeración usado en varios países no se ajuste a las normas ISO. Existen por lo menos seis posibilidades, como se muestra en la tabla siguiente
  
|Primer día de semana|La primera semana del año contiene|Semanas asignadas dos veces|Usado por/en|  
|---|---|---|---|
|Domingo|1 de enero,<br /><br /> El primer sábado,<br /><br /> 1–7 días del año|Sí|United States|  
|Lunes|1 de enero,<br /><br /> El primer domingo,<br /><br /> 1–7 días del año|Sí|La mayoría de los países europeos y Reino Unido|  
|Lunes|4 de enero,<br /><br /> El primer jueves,<br /><br /> 4 a 7 días del año|No|ISO 8601, Noruega y Suecia|  
|Lunes|7 de enero,<br /><br /> El primer lunes,<br /><br /> 7 días del año|No||  
|Miércoles|1 de enero,<br /><br /> El primer martes,<br /><br /> 1–7 días del año|Sí||  
|Sábado|1 de enero,<br /><br /> El primer viernes,<br /><br /> 1–7 días del año|Sí||  
  
## <a name="tzoffset"></a>TZoffset  
El **TZoffset** (**tz**) se devuelve como el número de minutos (con signo). La instrucción siguiente devuelve un ajuste de zona horaria de 310 minutos.
  
```sql
SELECT DATEPART (TZoffset, '2007-05-10  00:00:01.1234567 +05:10');  
```  
El valor de TZoffset se representa como sigue:
- Para obtener datetime2 y datetimeoffset, TZoffset devuelve el desplazamiento de tiempo en minutos, donde el desplazamiento para datetime2 siempre es 0 minutos.
- Para los tipos de datos que pueden convertirse implícitamente a datetimeoffset o datetime2, con la excepción de los otros tipos de datos de fecha y hora, devuelve el desplazamiento de tiempo en minutos.
- Parámetros de todos los demás tipos producirá un error.
  
  
## <a name="smalldatetime-date-argument"></a>Argumento date smalldatetime  
Cuando *fecha* es [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), segundos se devuelven como 00.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-a-date-argument"></a>Valor predeterminado devuelto por una parte de fecha que no se encuentra en un argumento date  
Si el tipo de datos de la *fecha* argumento no tiene especificado *datepart*, el valor predeterminado de *datepart* se devolverán solo cuando se especifica un literal para *fecha*.
  
Por ejemplo, el valor predeterminado año año-mes-día para cualquier **fecha** tipo de datos es 1900-01-01. La instrucción siguiente tiene argumentos de la parte de fecha para *datepart*, un argumento de tiempo para *fecha*y devuelve `1900, 1, 1, 1, 2`.
  
```sql
SELECT DATEPART(year, '12:10:30.123')  
    ,DATEPART(month, '12:10:30.123')  
    ,DATEPART(day, '12:10:30.123')  
    ,DATEPART(dayofyear, '12:10:30.123')  
    ,DATEPART(weekday, '12:10:30.123');  
```  
  
Si *fecha* no se especifica como una variable o columna de tabla y los datos de tipo para que variable o columna no tiene especificado *datepart*, se devuelve el error 9810. El siguiente código de ejemplo se produce un error porque el año de la parte de fecha no es válida para la **tiempo** tipo de datos declarado de la variable  *@t* .
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATEPART(year, @t);  
```  
  
## <a name="fractional-seconds"></a>Las fracciones de segundo
Las fracciones de segundo se devuelven como se indica en la instrucción siguiente:
  
```sql
SELECT DATEPART(millisecond, '00:00:01.1234567'); -- Returns 123  
SELECT DATEPART(microsecond, '00:00:01.1234567'); -- Returns 123456  
SELECT DATEPART(nanosecond,  '00:00:01.1234567'); -- Returns 123456700  
```  
  
## <a name="remarks"></a>Comentarios  
Se puede utilizar DATEPART en la lista de selección, cláusulas WHERE, HAVING, GROUP BY y ORDER BY.
  
En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATEPART convierte implícitamente los literales de cadena como un **datetime2** tipo. Esto significa que DATEPART no admite el formato año-día-mes cuando se pasa la fecha como cadena. Se debe convertir explícitamente la cadena a un **datetime** o **smalldatetime** tipo que se usa el formato de ADM.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se devuelve el año de base. El año de base es útil para calcular fechas. En el ejemplo siguiente, la fecha se especifica como un número. Observe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta 0 como el 1 de enero de 1900.
  
```sql
SELECT DATEPART(year, 0), DATEPART(month, 0), DATEPART(day, 0);  
-- Returns: 1900    1    1 */  
```  
  
En el ejemplo siguiente se devuelve la parte del día de la fecha `12/20/1974`.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (day,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`--------`
  
 `20`  
  
En el ejemplo siguiente se devuelve la parte del año de la fecha `12/20/1974`.
  
```sql
-- Uses AdventureWorks  
  
SELECT TOP(1) DATEPART (year,'12/20/1974') FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
`--------`
  
 `1974`  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

