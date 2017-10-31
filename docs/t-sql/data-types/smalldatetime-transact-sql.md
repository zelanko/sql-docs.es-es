---
title: smalldatetime (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- smalldatetime_TSQL
- smalldatetime
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- smalldatetime data type [SQL Server]
- dates [SQL Server], data types
- date and time [SQL Server], smalldatetime
- data types [SQL Server], date and time
ms.assetid: 68b74610-d54c-4c8e-b4b2-7e3747546ee0
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 07012d85a54292fa763a7b291d1b7318b6969ca4
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="smalldatetime-transact-sql"></a>smalldatetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define una fecha que se combina con una hora del día. La hora está en un formato de día de 24 horas , con segundos siempre a cero (: 00) y sin fracciones de segundo.
  
> [!NOTE]  
>  Use la **tiempo**, **fecha**, **datetime2** y **datetimeoffset** tipos de datos para el nuevo trabajo. Estos tipos se alinean con el estándar SQL. Son más portátiles. **tiempo**, **datetime2** y **datetimeoffset** proporcionan una mayor precisión de segundos. **DateTimeOffset** proporciona compatibilidad de zona horaria para las aplicaciones implementadas globalmente.  
  
## <a name="smalldatetime-description"></a>Descripción de smalldatetime
  
|||  
|-|-|  
|Sintaxis|**smalldatetime**|  
|Uso|DECLARAR @MySmalldatetime **smalldatetime**<br /><br /> Crear tabla Table1 (Column1 **smalldatetime** )|  
|Formatos de literal de cadena predeterminados<br /><br /> (se usa para el cliente de nivel inferior)|No aplicable|  
|Intervalo de fechas|De 1900-01-01 a 2079-06-06<br /><br /> Del 1 de enero de 1900 hasta el 6 de junio de 2079|  
|Intervalo de horas|De 00:00:00 a 23:59:59<br /><br /> 2007-05-09 23:59:59 se redondeará a<br /><br /> 2007-05-10 00:00:00|  
|Intervalos de elementos|AAAA es una cifra de cuatro dígitos comprendida entre 1900 y 2079 que representa un año.<br /><br /> MM es una cifra de dos dígitos comprendido entre 01 y 12, que representa un mes del año especificado.<br /><br /> DD es cifra de dos dígitos comprendido entre 01 y 31 dependiendo del mes, que representa un día del mes especificado.<br /><br /> hh es una cifra de dos dígitos comprendida entre 00 y 23 que representa la hora.<br /><br /> mm es una cifra de dos dígitos comprendida entre 00 y 59 que representa los minutos.<br /><br /> s es una cifra de dos dígitos comprendida entre 00 y 59 que representa los segundos. Los valores de 29,998 segundos o menos se redondean a la baja hasta el minuto más cercano; los valores de 29,999 segundos o más se redondean al alza hasta el minuto más cercano.|  
|Longitud en caracteres|19 posiciones como máximo|  
|Tamaño de almacenamiento|4 bytes, fijo.|  
|Precisión|Un minuto|  
|Valor predeterminado|1900-01-01 00:00:00|  
|Calendario|Gregoriano<br /><br /> (no incluye el intervalo completo de años.)|  
|Precisión de fracciones de segundo definida por el usuario|No|  
|Conservación y reconocimiento del ajuste de zona horaria|No|  
|Reconocimiento del horario de verano|No|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Compatibilidad con ANSI e ISO 8601  
**smalldatetime** no es ANSI o ISO 8601 compatible.
  
## <a name="converting-date-and-time-data"></a>Convertir datos de fecha y hora
Cuando se convierte a los tipos de datos de fecha y hora, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rechaza todos los valores que no reconoce como fechas u horas. Para obtener información acerca de cómo utilizar las funciones CAST y CONVERT con datos de fecha y hora, vea [CAST y CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-smalldatetime-to-other-date-and-time-types"></a>Convertir tipos smalldatetime a otros tipos de fecha y hora
Esta sección describe lo que ocurre cuando un **smalldatetime** tipo de dato se convierte a otros tipos de datos de fecha y hora.
  
En el caso de la conversión a **fecha**, se copian el año, mes y día. En el código siguiente se muestran los resultados de convertir un valor `smalldatetime` en un valor `date`.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @date date = @smalldatetime  
  
SELECT @smalldatetime AS '@smalldatetime', @date AS 'date';  
  
--Result  
--@smalldatetime          date  
------------------------- ----------  
--1955-12-13 12:43:00     1955-12-13  
--  
--(1 row(s) affected)  
```  
  
Cuando la conversión es a **Time (n)**, se copian las horas, minutos y segundos. Las fracciones de segundo se establecen en 0. En el código siguiente se muestran los resultados de convertir un valor `smalldatetime` en un valor `time(4)`.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @time time(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @time AS 'time';  
  
--Result  
--@smalldatetime          time  
------------------------- -------------  
--1955-12-13 12:43:00     12:43:00.0000  
--  
--(1 row(s) affected)  
```  
  
Cuando la conversión es a **datetime**, **smalldatetime** valor se copia en el **datetime** valor. Las fracciones de segundo se establecen en 0. En el código siguiente se muestran los resultados de convertir un valor `smalldatetime` en un valor `datetime`.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetime AS 'datetime';  
  
--Result  
--@smalldatetime          datetime  
------------------------- -----------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.000  
--  
--(1 row(s) affected)  
```  
  
En el caso de la conversión a **DateTimeOffset (n)**, **smalldatetime** valor se copia en el **DateTimeOffset (n)** valor. Las fracciones de segundo se establecen en 0 y el ajuste de zona horaria se establece en +00: 0. En el código siguiente se muestran los resultados de convertir un valor `smalldatetime` en un valor `datetimeoffset(4)`.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetimeoffset datetimeoffset(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetimeoffset AS 'datetimeoffset(4)';  
  
--Result  
--@smalldatetime          datetimeoffset(4)  
------------------------- ------------------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.0000 +00:0  
--  
--(1 row(s) affected)  
```  
  
Para la conversión a **datetime2**, **smalldatetime** valor se copia en el **datetime2** valor. Las fracciones de segundo se establecen en 0. En el código siguiente se muestran los resultados de convertir un valor `smalldatetime` en un valor `datetime2(4)`.
  
```sql
DECLARE @smalldatetime smalldatetime = '1955-12-13 12:43:10';  
DECLARE @datetime2 datetime2(4) = @smalldatetime;  
  
SELECT @smalldatetime AS '@smalldatetime', @datetime2 AS ' datetime2(4)';  
  
--Result  
--@smalldatetime           datetime2(4)  
------------------------- ------------------------  
--1955-12-13 12:43:00     1955-12-13 12:43:00.0000  
--  
--(1 row(s) affected)  
```  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-casting-string-literals-with-seconds-to-smalldatetime"></a>A. Convertir literales de cadena con segundos a smalldatetime  
En el ejemplo siguiente se compara la conversión de los segundos presentes en los literales de cadena a `smalldatetime`.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29'     AS smalldatetime)  
    ,CAST('2007-05-08 12:35:30'     AS smalldatetime)  
    ,CAST('2007-05-08 12:59:59.998' AS smalldatetime);  
```  
  
|Entrada|Salida|  
|---|---|
|2007-05-08 12:35:29|2007-05-08 12:35:00|  
|2007-05-08 12:35:30|2007-05-08 12:36:00|  
|2007-05-08 12:59:59.998|2007-05-08 13:00:00|  
  
### <a name="b-comparing-date-and-time-data-types"></a>B. Comparar tipos de datos de fecha y hora  
En el ejemplo siguiente se comparan los resultados de convertir una cadena a cada tipo de datos de fecha y hora.
  
```sql
SELECT   
     CAST('2007-05-08 12:35:29. 1234567 +12:15' AS time(7)) AS 'time'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS date) AS 'date'   
    ,CAST('2007-05-08 12:35:29.123' AS smalldatetime) AS   
        'smalldatetime'   
    ,CAST('2007-05-08 12:35:29.123' AS datetime) AS 'datetime'   
    ,CAST('2007-05-08 12:35:29. 1234567 +12:15' AS datetime2(7)) AS   
        'datetime2'  
    ,CAST('2007-05-08 12:35:29.1234567 +12:15' AS datetimeoffset(7)) AS   
        'datetimeoffset';  
```  
  
|Tipo de datos|Salida|  
|---|---|
|**time**|12:35:29. 1234567|  
|**date**|2007-05-08|  
|**smalldatetime**|2007-05-08 12:35:00|  
|**datetime**|2007-05-08 12:35:29.123|  
|**datetime2**|2007-05-08 12:35:29. 1234567|  
|**datetimeoffset**|2007-05-08 12:35:29.1234567 +12:15|  
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
  

