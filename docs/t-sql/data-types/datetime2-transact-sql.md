---
title: datetime2 (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- datetime2
- datetime2_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- dates [SQL Server], data types
- date and time [SQL Server], datetime2
- data types [SQL Server], date and time
- datetime2 data type [SQL Server]
ms.assetid: 868017f3-214f-43ef-8536-cc1632a2288f
caps.latest.revision: 58
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13766b3d0cb86780c2eca55c7f36e8fd16e973c5
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="datetime2-transact-sql"></a>datetime2 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define una fecha que se combina con una hora del día basada en un reloj de 24 horas. **datetime2** puede considerarse como una extensión de las existentes **datetime** tipo que tiene un intervalo de fechas mayor, una mayor precisión de fracciones predeterminada y precisión opcional especificada por el usuario.
  
## <a name="datetime2-description"></a>Descripción de datetime2
  
|Propiedad|Valor|  
|--------------|-----------|  
|Sintaxis|**datetime2** [(*precisión de fracciones de segundo*)]|  
|Uso|DECLARAR @MyDatetime2 **datetime2(7)**<br /><br /> Crear tabla Table1 (Column1 **datetime2(7)** )|  
|Formato de literal de cadena predeterminado<br /><br /> (se usa para el cliente de nivel inferior)|AAAA-MM-DD hh:mm:ss[.fracciones de segundos]<br /><br /> Para obtener más información, vea la sección "Compatibilidad con versiones anteriores de clientes de nivel inferior" que sigue.|  
|Intervalo de fechas|De 0001-01-01 a 31.12.99<br /><br /> Enero 1,1 CE hasta el 31 de diciembre de 9999 CE|  
|Intervalo de horas|De 00:00:00 a 23:59:59.9999999|  
|Intervalo de ajuste de zona horaria|Ninguno|  
|Intervalos de elementos|AAAA es un número de cuatro dígitos, comprendida entre 0001 y 9999 que representa un año.<br /><br /> MM es un número de dos dígitos comprendido entre 01 y 12, que representa un mes del año especificado.<br /><br /> DD es un número de dos dígitos, comprendida entre 01 y 31 dependiendo del mes, que representa un día del mes especificado.<br /><br /> HH es un número de dos dígitos, comprendida entre 00 y 23, que representa la hora.<br /><br /> mm es un número de dos dígitos comprendidos entre 00 y 59, que representa el minuto.<br /><br /> ss es una cifra de dos dígitos comprendida entre 00 y 59 que representa los segundos.<br /><br /> n * es un número cero a siete dígitos comprendido entre 0 y 9999999 que representa las fracciones de segundo. En informática, las fracciones de segundo se truncan cuando n > 3.|  
|Longitud en caracteres|19 posiciones como mínimo (AAAA-MM-DD hh:mm:ss) a 27 como máximo (AAAA-MM-DD hh:mm:ss .0000000)|  
|Precisión, escala|De 0 a 7 dígitos, con una precisión de 100 ns. La precisión predeterminada es 7 dígitos.|  
|Tamaño de almacenamiento|6 bytes para precisiones inferiores a 3; 7 bytes para precisiones 3 y 4. Todas las demás precisiones requieren 8 bytes.|  
|Precisión|100 nanosegundos|  
|Valor predeterminado|1900-01-01 00:00:00|  
|Calendario|Gregoriano|  
|Precisión de fracciones de segundo definida por el usuario|Sí|  
|Conservación y reconocimiento del ajuste de zona horaria|No|  
|Reconocimiento del horario de verano|No|  
  
Para los metadatos de tipo de datos, vea [sys.systypes &#40; Transact-SQL &#41; ](../../relational-databases/system-compatibility-views/sys-systypes-transact-sql.md) o [TYPEPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/typeproperty-transact-sql.md). La precisión y escala son variables para algunos tipos de datos de hora y fecha. Para obtener la precisión y escala de una columna, vea [COLUMNPROPERTY &#40; Transact-SQL &#41; ](../../t-sql/functions/columnproperty-transact-sql.md), [COL_LENGTH &#40; Transact-SQL &#41; ](../../t-sql/functions/col-length-transact-sql.md), o [sys.columns &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).
  
## <a name="supported-string-literal-formats-for-datetime2"></a>Admite los formatos de literal de cadena para datetime2
Las tablas siguientes enumeran los ISO 8601 y ODBC cadena literales formatos admitidos para **datetime2**. Para obtener información acerca de los formatos alfabético, numéricos, sin separación y tiempo para las partes de fecha y hora de **datetime2**, consulte [inte &#40; Transact-SQL &#41; ](../../t-sql/data-types/date-transact-sql.md) y [tiempo &#40; Transact-SQL &#41; ](../../t-sql/data-types/time-transact-sql.md).
  
|ISO 8601|Descripciones|  
|---|---|
|AAAA-MM-DDThh:mm:ss[.nnnnnnn]<br /><br /> AAAA-MM-DDThh:mm:ss[.nnnnnnn]|Este formato no se ve afectado por la configuración regional de sesión de SET LANGUAGE y SET DATEFORMAT. El **T**, los dos puntos (:) y el punto (.) se incluyen en el literal de cadena, por ejemplo ' 2007-05-02T19:58:47.1234567'.|  
  
|ODBC|Description|  
|---|---|
|{ ts 'aaaa-mm-dd hh:mm:ss[.fracciones de segundo]' }|Específico de ODBC API:<br /><br /> El número de dígitos a la derecha del separador decimal, que representa las fracciones de segundo, se puede especificar de 0 a 7 (100 nanosegundos).|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Cumplimiento de normas ANSI e ISO 8601  
La compatibilidad ANSI e ISO 8601 de [fecha](../../t-sql/data-types/date-transact-sql.md) y [tiempo](../../t-sql/data-types/time-transact-sql.md) se aplican a **datetime2**.
  
##  <a name="backward-compatibility-for-down-level-clients"></a>Compatibilidad con versiones anteriores de los clientes de niveles inferiores  
Algunos clientes de nivel inferior no admiten la **tiempo**, **fecha**, **datetime2** y **datetimeoffset** tipos de datos. En la tabla siguiente se muestra la asignación de tipo entre una instancia de nivel superior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los clientes de nivel inferior.
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de datos|El formato del literal de cadena predeterminado se pasó al cliente de nivel inferior|ODBC de nivel inferior|OLEDB de nivel inferior|JDBC de nivel inferior|SQLCLIENT de nivel inferior|  
| --- | --- | --- | --- | --- | --- |
|**time**|hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR o SQL_VARCHAR|DBTYPE_WSTR o DBTYPE_STR|Java.sql.String|Cadena o SqString|  
|**date**|YYYY-MM-DD|SQL_WVARCHAR o SQL_VARCHAR|DBTYPE_WSTR o DBTYPE_STR|Java.sql.String|Cadena o SqString|  
|**datetime2**|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|SQL_WVARCHAR o SQL_VARCHAR|DBTYPE_WSTR o DBTYPE_STR|Java.sql.String|Cadena o SqString|  
|**datetimeoffset**|AAAA-MM-DD hh [.nnnnnnn] [+ &#124;-] hh: mm|SQL_WVARCHAR o SQL_VARCHAR|DBTYPE_WSTR o DBTYPE_STR|Java.sql.String|Cadena o SqString|  
  
## <a name="converting-date-and-time-data"></a>Convertir datos de fecha y hora
Cuando se convierte a los tipos de datos de fecha y hora, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rechaza todos los valores que no reconoce como fechas u horas. Para obtener información acerca de cómo utilizar las funciones CAST y CONVERT con datos de fecha y hora, vea [CAST y CONVERT &#40; Transact-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)
  
### <a name="converting-other-date-and-time-types-to-the-datetime2-data-type"></a>Convertir a otros tipos de fecha y hora para el tipo de datos datetime2
Esta sección describe lo que ocurre cuando los otros tipos de datos de fecha y hora se convierten a la **datetime2** tipo de datos.  
  
Cuando la conversión es de **fecha**, se copian el año, mes y día.  El componente de hora se establece en 00:00:00.0000000.  En el código siguiente se muestran los resultados de convertir un valor `date` en un valor `datetime2`.  
  
```sql
DECLARE @date date = '12-21-16';
DECLARE @datetime2 datetime2 = @date;

SELECT @datetime2 AS '@datetime2', @date AS '@date';
  
--Result  
--@datetime2                  @date
----------------------------- ----------
--2016-12-21 00:00:00.0000000 2016-12-21
```  
  
Cuando la conversión es de **Time (n)**, se copia el componente de hora, y el componente de fecha se establece en ' 1900-01-01'. En el siguiente ejemplo se muestran los resultados de convertir un valor `time(7)` en un valor `datetime2`.  
  
```sql
DECLARE @time time(7) = '12:10:16.1234567';
DECLARE @datetime2 datetime2 = @time;

SELECT @datetime2 AS '@datetime2', @time AS '@time';
  
--Result  
--@datetime2                  @time
----------------------------- ----------------
--1900-01-01 12:10:16.1234567 12:10:16.1234567
```  
  
Cuando la conversión es de **smalldatetime**, se copian las horas y minutos. Los segundos y las fracciones de segundo se establecen en 0. En el código siguiente se muestran los resultados de convertir un valor `smalldatetime` en un valor `datetime2`.  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';
DECLARE @datetime2 datetime2 = @smalldatetime;

SELECT @datetime2 AS '@datetime2', @smalldatetime AS '@smalldatetime'; 
  
--Result  
--@datetime2                  @smalldatetime
----------------------------- -----------------------
--2016-12-01 12:32:00.0000000 2016-12-01 12:32:00 
```  
  
Cuando la conversión es de **DateTimeOffset (n)**, se copian los componentes de fecha y hora. Se trunca la zona horaria. En el siguiente ejemplo se muestran los resultados de convertir un valor `datetimeoffset(7)` en un valor `datetime2`.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(7) = '2016-10-23 12:45:37.1234567 +10:0';
DECLARE @datetime2 datetime2 = @datetimeoffset;

SELECT @datetime2 AS '@datetime2', @datetimeoffset AS '@datetimeoffset'; 
  
--Result  
--@datetime2                  @datetimeoffset
----------------------------- ----------------------------------
--2016-10-23 12:45:37.1234567 2016-10-23 12:45:37.1234567 +10:00
```  

Cuando la conversión es de **datetime**, se copian a la fecha y hora.  La precisión fraccionaria se extiende a 7 dígitos.  En el siguiente ejemplo se muestran los resultados de convertir un valor `datetime` en un valor `datetime2`.

```sql
DECLARE @datetime datetime = '2016-10-23 12:45:37.333';
DECLARE @datetime2 datetime2 = @datetime;

SELECT @datetime2 AS '@datetime2', @datetime AS '@datetime';
   
--Result  
--@datetime2                  @datetime
------------------------- ---------------------------
--2016-10-23 12:45:37.3333333 2016-10-23 12:45:37.333
```  
  
### <a name="converting-string-literals-to-datetime2"></a>Convertir literales de cadena a datetime2  
Las conversiones de literales de cadena en tipos de fecha y hora son posibles cuando todas las partes de las cadenas están en formatos válidos. En caso contrario, se generará un error en el tiempo de ejecución. Las conversiones implícitas o explícitas que no especifican un estilo (desde tipos de fecha y hora hasta literales de cadena) estarán en el formato predeterminado de la sesión actual. La siguiente tabla muestra las reglas para convertir una cadena literal la **datetime2** tipo de datos.
  
|Literal de cadena de entrada|**datetime2**|  
|---|---|
|DATE de ODBC|Literales de cadena ODBC se asignan a la **datetime** tipo de datos. Cualquier operación de asignación de literales de DATETIME de ODBC en **datetime2** tipos provocará una conversión implícita entre **datetime** y este tipo de acuerdo con las reglas de conversión.|  
|TIME de ODBC|Vea la regla anterior de DATE de ODBC.|  
|DATETIME DE ODBC|Vea la regla anterior de DATE de ODBC.|  
|Solo DATE|La parte de TIME tiene como valor predeterminado 00:00:00.|  
|Solo TIME|La parte de DATE tiene como valor predeterminado 1900-1-1.|  
|Solo TIMEZONE|Se proporcionan los valores predeterminados.|  
|DATE + TIME|Trivial|  
|DATE + TIMEZONE|No permitido.|  
|TIME + TIMEZONE|La parte de DATE tiene como valor predeterminado 1900-1-1. Se omite la entrada de TIMEZONE.|  
|DATE + TIME + TIMEZONE|Se usará DATETIME local.|  
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se compara los resultados de convertir una cadena a cada uno de ellos **fecha** y **tiempo** tipo de datos.
  
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
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
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
  
  

