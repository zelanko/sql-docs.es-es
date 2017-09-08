---
title: DATENAME (Transact-SQL) | Documentos de Microsoft
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
caps.latest.revision: 59
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d41bbf5a83f0dee8518ece6f074181b8412bad8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="datename-transact-sql"></a>DATENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Devuelve una cadena de caracteres que representa el parámetro *datepart* del elemento especificado *fecha*
  
Para obtener información general de todos los [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de datos de fecha y hora y funciones, vea [funciones y tipos de datos de hora y fecha &#40; Transact-SQL &#41; ](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DATENAME ( datepart , date )  
```  
  
## <a name="arguments"></a>Argumentos  
*parte de fecha*  
Es la parte de la *fecha* para devolver. La siguiente tabla se recogen válidos *datepart* argumentos. Los equivalentes de variables definidas por el usuario no son válidos.
  
|*parte de fecha*|Abreviaturas|  
|---|---|
|**año**|**yy, yyyy**|  
|**trimestre**|**TT, q**|  
|**mes**|**mm, m**|  
|**DAYOFYEAR**|**dy, y**|  
|**día**|**dd, d**|  
|**semana**|**wk, ww**|  
|**día de la semana**|**almacenamiento de datos, w**|  
|**hora**|**hh**|  
|**minuto**|**Mi, n**|  
|**segundo**|**ss, s**|  
|**milisegundo**|**MS**|  
|**microsegundos**|**MCS**|  
|**nanosegundos**|**NS**|  
|**TZoffset**|**TZ**|  
|**ISO_WEEK**|**ISOWK, ISOWW**|  
  
*date*  
Es una expresión que se pueda resolver como un **tiempo**, **fecha**, **smalldatetime**, **datetime**, **datetime2**, o **datetimeoffset** valor. *fecha* puede ser una expresión, la expresión de columna, la variable definida por el usuario o la cadena literal.  
Para evitar ambigüedades, use años de cuatro dígitos. Para obtener información sobre los años de dos dígitos, consulte [configurar two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md).
  
## <a name="return-type"></a>Tipo devuelto  
**nvarchar**
  
## <a name="return-value"></a>Valor devuelto  
  
-   Cada *datepart* y sus abreviaturas devuelven el mismo valor.  
  
El valor devuelto depende del entorno del idioma definido mediante el uso de [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) y la [configurar la opción de configuración de servidor idioma predeterminado](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) del inicio de sesión. El valor devuelto depende de [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) si *fecha* es una cadena literal de ciertos formatos. SET DATEFORMAT no afecta al valor devuelto cuando la fecha es una expresión de columna de un tipo de datos de hora o fecha.
  
Cuando el *fecha* parámetro tiene un **fecha** argumento de tipo de datos, el valor devuelto depende de la configuración especificada mediante el uso de [SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md).
  
## <a name="tzoffset-datepart-argument"></a>Argumento datepart TZoffset  
Si *datepart* argumento es **TZoffset** (**tz**) y la *fecha* argumento no tiene ningún ajuste de zona horaria, se devuelve 0.
  
## <a name="smalldatetime-date-argument"></a>Argumento date smalldatetime  
Cuando *fecha* es [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md), segundos se devuelven como 00.
  
## <a name="default-returned-for-a-datepart-that-is-not-in-the-date-argument"></a>Valor predeterminado devuelto por datepart que no se encuentra en el argumento date  
Si el tipo de datos de la *fecha* argumento no tiene especificado *datepart*, el valor predeterminado de *datepart* se devolverán solo cuando se especifica un literal para *fecha*.
  
Por ejemplo, el valor predeterminado año año-mes-día para cualquier **fecha** tipo de datos es 1900-01-01. La instrucción siguiente tiene argumentos de la parte de fecha para *datepart*, un argumento de tiempo para *fecha*y devuelve `1900, January, 1, 1, Monday`.
  
```sql
SELECT DATENAME(year, '12:10:30.123')  
    ,DATENAME(month, '12:10:30.123')  
    ,DATENAME(day, '12:10:30.123')  
    ,DATENAME(dayofyear, '12:10:30.123')  
    ,DATENAME(weekday, '12:10:30.123');  
```  
  
Si *fecha* no se especifica como una variable o columna de tabla y los datos de tipo para que variable o columna no tiene especificado *datepart*, se devuelve el error 9810. El siguiente código de ejemplo se produce un error porque el año de la parte de fecha no es válida para la **tiempo** tipo de datos declarado de la variable  *@t* .
  
```sql
DECLARE @t time = '12:10:30.123';   
SELECT DATENAME(year, @t);  
```  
  
## <a name="remarks"></a>Comentarios  
Se puede usar DATENAME en la lista de selección, cláusulas WHERE, HAVING, GROUP BY y ORDER BY.
  
En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], DATENAME convierte implícitamente los literales de cadena como un **datetime2** tipo. Esto significa que DATENAME no admite el formato año-día-mes cuando se pasa la fecha como cadena. Se debe convertir explícitamente la cadena a un **datetime** o **smalldatetime** tipo que se usa el formato de ADM.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se obtienen las partes de fecha para la fecha especificada.
  
`SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');`
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*parte de fecha*|Valor devuelto|  
|---|---|
|**año, aaaa, AA**|2007|  
|**trimestre, p, q**|4|  
|**mes, mm, m**|Octubre|  
|**DAYOFYEAR, dy, y**|303|  
|**día, dd, d**|30|  
|**semana, wk, ww**|44|  
|**día de la semana, almacenamiento de datos**|Martes|  
|**hora, hh**|12|  
|**minuto, n**|15|  
|**segundo, ss, s**|32|  
|**milisegundo, ms**|123|  
|**microsegundos, mcs**|123456|  
|**nanosegundos, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]

En el ejemplo siguiente se obtienen las partes de fecha para la fecha especificada.
  
```sql
SELECT DATENAME(datepart,'2007-10-30 12:15:32.1234567 +05:10');  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
|*parte de fecha*|Valor devuelto|  
|---|---|
|**año, aaaa, AA**|2007|  
|**trimestre, p, q**|4|  
|**mes, mm, m**|Octubre|  
|**DAYOFYEAR, dy, y**|303|  
|**día, dd, d**|30|  
|**semana, wk, ww**|44|  
|**día de la semana, almacenamiento de datos**|Martes|  
|**hora, hh**|12|  
|**minuto, n**|15|  
|**segundo, ss, s**|32|  
|**milisegundo, ms**|123|  
|**microsegundos, mcs**|123456|  
|**nanosegundos, ns**|123456700|  
|**TZoffset, tz**|310|  
|**ISO_WEEK, ISOWK, ISOWW**|44|  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  


