---
title: DATENAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATENAME_TSQL
- DATENAME
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- DATENAME function [SQL Server
- functions [SQL Server], time
- functions [SQL Server], date and time
- dateparts [SQL Server], datename
- date and time [SQL Server], DATENAME
- comparing dates times [SQL Server]
- dates [SQL Server], dateparts
ms.assetid: 11855b56-c554-495d-aad4-ba446990153b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 22dc10851e3185512527f82f593fdc2cdb2b765f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve una cadena de caracteres que representa el parámetro *datepart* especificado del parámetro *date*.
  
Para ver información general sobre todos los tipos de datos y funciones de fecha y hora de [!INCLUDE[tsql](../../includes/tsql-md.md)], vea [Date and Time Data Types and Functions &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md) [Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*datepart*  
Es una parte del parámetro *date* que se devuelve. En esta tabla se enumeran los argumentos válidos de *datepart*. Los equivalentes de variables definidas por el usuario no son válidos.
  
|*datepart*|Abreviaturas|  
|---|---|
|**year**|**yy, yyyy**|  
|**quarter**|**qq, q**|  
|**month**|**mm, m**|  
|**dayofyear**|**dy, y**|  
|**day**|**dd, d**|  
|**week**|**wk, ww**|  
|**weekday**|**dw, w**|  
|**hour**|**hh**|  
|**minute**|**mi, n**|  
|**second**|**ss, s**|  
|**millisecond**|**ms**|  
|**microsecond**|**mcs**|  
|**nanosecond**|**ns**|  
|**TZoffset**|**tz**|  
|**ISO_WEEK**|**ISOWK, ISOWW**|  
  
*date*  
Es una expresión que se puede resolver en un valor **time**, **date**, **smalldatetime**, **datetime**, **datetime2** o **datetimeoffset**. *date* puede ser una expresión, una expresión de columna, una variable definida por el usuario o un literal de cadena.  
Para evitar ambigüedades, use años de cuatro dígitos. Para más información, vea [Establecer la opción de configuración del servidor Fecha límite de año de dos dígitos](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Tipo devuelto  
**nvarchar**
  
## <a name="return-value"></a>Valor devuelto  
  
-   Cada *datepart* y sus abreviaturas devuelven el mismo valor.  
  
El valor devuelto depende del entorno del idioma definido por [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) y de [Establecer la opción de configuración del servidor Idioma predeterminado](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) del inicio de sesión. El valor devuelto depende de [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) si *date* es un literal de cadena de ciertos formatos. SET DATEFORMAT no afecta al valor devuelto cuando la fecha es una expresión de columna de un tipo de datos de hora o fecha.
  
Cuando el parámetro *date* tiene un argumento de tipo de datos **date**, el valor devuelto depende de la configuración especificada mediante [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
## <a name="tzoffset-datepart-argument"></a>Argumento datepart TZoffset  
Si el argumento *datepart* es **TZoffset** (**tz**) y el argumento *date* no tiene ajuste de zona horaria, se devuelve 0.
  
## <a name="smalldatetime-date-argument"></a>Argumento date smalldatetime  
Si *date* es [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), los segundos se devuelven como 00.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>Valor predeterminado devuelto por datepart que no se encuentra en el argumento date  
Si el tipo de datos del argumento *date* no contiene el parámetro *datepart* especificado, se devolverá el valor predeterminado *datepart* solo cuando se especifique un valor literal para *date*.
  
Por ejemplo, el valor predeterminado de año-mes-día de cualquier tipo de datos **date** es 1900-01-01. La instrucción siguiente tiene argumentos de la parte de fecha para *datepart*, un argumento de tiempo para *date* y devuelve `1900, January, 1, 1, Monday`.
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
Si *date* se especifica como variable o como columna de tabla y el tipo de datos de esa variable o columna no tiene especificado *datepart*, se devuelve el error 9810. En el ejemplo de código siguiente se produce un error porque la parte de fecha de año no es válida para el tipo de datos **time** que se declara para la variable *@t*.
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>Notas  
Se puede usar DATENAME en la lista de selección, cláusulas WHERE, HAVING, GROUP BY y ORDER BY.
  
En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATENAME convierte implícitamente los literales de cadena como un tipo **datetime2**. Esto significa que DATENAME no admite el formato año-día-mes cuando se pasa la fecha como cadena. La cadena se debe convertir explícitamente a un tipo **datetime** o **smalldatetime** para poder usar el formato año-día-mes.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se obtienen las partes de fecha para la fecha especificada.
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|Valor devuelto|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|Octubre|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|Martes|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

En el ejemplo siguiente se obtienen las partes de fecha para la fecha especificada.
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*datepart*|Valor devuelto|  
|---|---|
|**year, yyyy, yy**|2007|  
|**quarter, qq, q**|4|  
|**month, mm, m**|Octubre|  
|**dayofyear, dy, y**|303|  
|**day, dd, d**|30|  
|**week, wk, ww**|44|  
|**weekday, dw**|Martes|  
|**hour, hh**|12|  
|**minute, n**|15|  
|**second, ss, s**|32|  
|**millisecond, ms**|123|  
|**microsecond, mcs**|123456|  
|**nanosecond, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

