---
title: fecha y hora (Transact-SQL) | Documentos de Microsoft
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
- datetime_TSQL
- datetime
dev_langs:
- TSQL
helpviewer_keywords:
- time [SQL Server], data types
- date and time [SQL Server], datetime
- dates [SQL Server], data types
- datetime data type [SQL Server]
- data types [SQL Server], date and time
ms.assetid: 9bd1cc5b-227b-4032-95d6-7581ddcc9924
caps.latest.revision: 64
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ae40eaacd6fd441ce0bdbadd3af02b7b189704a2
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="datetime-transact-sql"></a>datetime (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Define una fecha que se combina con una hora del día con fracciones de segundos basada en un reloj de 24 horas.
  
> [!NOTE]  
>  Use la **tiempo**, **fecha**, **datetime2** y **datetimeoffset** tipos de datos para el nuevo trabajo. Estos tipos se alinean con el estándar SQL. Son más portátiles. **tiempo**, **datetime2** y **datetimeoffset** proporcionan una mayor precisión de segundos. **DateTimeOffset** proporciona compatibilidad de zona horaria para las aplicaciones implementadas globalmente.  
  
## <a name="datetime-description"></a>Descripción de datetime  
  
|Propiedad|Valor|  
|---|---|
|Sintaxis|**datetime**|  
|Uso|DECLARAR @MyDatetime **fecha y hora**<br /><br /> Crear tabla Table1 (Column1 **datetime** )|  
|Formatos de literal de cadena predeterminados<br /><br /> (se usa para el cliente de nivel inferior)|No aplicable|  
|Intervalo de fechas|Del 01.01.53 hasta el 31.12.99|  
|Intervalo de horas|00:00:00 a 23:59:59.997|  
|Intervalo de ajuste de zona horaria|Ninguno|  
|Intervalos de elementos|AAAA es una cifra de cuatro dígitos comprendida entre 1753 y 9999 que representa un año.<br /><br /> MM es una cifra de dos dígitos comprendido entre 01 y 12, que representa un mes del año especificado.<br /><br /> DD es cifra de dos dígitos comprendido entre 01 y 31 dependiendo del mes, que representa un día del mes especificado.<br /><br /> hh es una cifra de dos dígitos comprendida entre 00 y 23 que representa la hora.<br /><br /> mm es una cifra de dos dígitos comprendida entre 00 y 59 que representa los minutos.<br /><br /> s es una cifra de dos dígitos comprendida entre 00 y 59 que representa los segundos.<br /><br /> n* es una cifra de cero a tres dígitos comprendida entre 0 y 999 que representa las fracciones de segundos.|  
|Longitud en caracteres|19 posiciones como mínimo a 23 como máximo|  
|Tamaño de almacenamiento|8 bytes|  
|Precisión|Se redondea en incrementos de 0,000, 0,003 o 0.007 segundos|  
|Valor predeterminado|1900-01-01 00:00:00|  
|Calendario|Gregoriano (no incluye el intervalo completo de años.)|  
|Precisión de fracciones de segundo definida por el usuario|No|  
|Conservación y reconocimiento del ajuste de zona horaria|No|  
|Reconocimiento del horario de verano|No|  
  
## <a name="supported-string-literal-formats-for-datetime"></a>Formatos del literales de cadena compatibles para datetime  
Las tablas siguientes enumeran los formatos de literales de cadena admitidos para **datetime**. Excepto para ODBC, **datetime** literales de cadena son comillas simples ('), por ejemplo, 'string_literaL'. Si el entorno no es **us_english**, los literales de cadena deben estar en el formato N 'string_literaL'.
  
|Numérico|Description|  
|---|---|
|Formatos de fecha:<br /><br /> [0]4/15/[19]96 -- (mda)<br /><br /> [0]4-15-[19]96 -- (mda)<br /><br /> [0]4.15.[19]96 -- (mda)<br /><br /> [0]4/[19]96/15 -- (mad)<br /><br /> 15/[0]4/[19]96 -- (dma)<br /><br /> 15/[19]96/[0]4 -- (dam)<br /><br /> [19]96/15/[0]4 -- (adm)<br /><br /> [19]96/[0]4/15 -- (amd)<br /><br /> Formatos de hora:<br /><br /> 14:30<br /><br /> 14:30[:20:999]<br /><br /> 14:30[:20.9]<br /><br /> 4am<br /><br /> 4 PM|Puede especificar datos de fecha con un mes en forma de número. Por ejemplo, 5/20/97 representa el veinte de mayo de 1997. Cuando use un formato numérico de fecha, especifique el mes, el día y el año en una cadena con barras diagonales (/), guiones (-) o puntos (.) como separadores. Esta cadena debe aparecer de la forma siguiente:<br /><br /> *número separador número separador número [time] [time]*<br /><br /> <br /><br /> Cuando el idioma está establecido en **us_english**, el orden predeterminado de la fecha es mdy. Puede cambiar el orden de fecha mediante el [SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md) instrucción.<br /><br /> La configuración de SET DATEFORMAT determina cómo se interpretan los valores de fecha. Si el orden no coincide con esta configuración, los valores no se interpretarán como fechas porque se encuentran fuera del intervalo, o bien se interpretarán incorrectamente. Por ejemplo, 12/10/08 se puede interpretar de seis formas distintas, en función de la configuración de DATEFORMAT. Un año en cuatro partes se interpreta como el año.|  
  
|Orden alfabético|Description|  
|---|---|
|Abr[il] [15][,] 1996<br /><br /> Abr[il] 15[,] [19]96<br /><br /> Abr[il] 1996 [15]<br /><br /> [15] Abr[il][,] 1996<br /><br /> 15 Abr[il][,][19]96<br /><br /> 15 [19]96 abr[il]<br /><br /> [15] 1996 abr[il]<br /><br /> 1996 ABR[IL] [15]<br /><br /> 1996 [15] ABR[IL]|Puede especificar los datos de la fecha con un mes especificado como el nombre completo del mes. Por ejemplo, abril o la abreviatura del mes Abr especificada en el idioma actual; las comas son opcionales y se omite el uso de mayúsculas.<br /><br /> Éstas son algunas directrices para utilizar los formatos alfabéticos de fecha:<br /><br /> (1) incluya los datos de fecha y hora entre comillas simples ('). Para los idiomas distintos de inglés, utilice N'<br /><br /> (2) los caracteres incluidos entre corchetes son opcionales.<br /><br /> (3) si especifica solamente los dos últimos dígitos del año, los valores inferiores a los dos últimos dígitos del valor de la [configurar two digit year cutoff Server Configuration Option](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) opción de configuración que se encuentran en el mismo siglo que el año límite . Valores mayores que o iguales que el valor de esta opción pertenecen al siglo anterior al año límite. Por ejemplo, si **límite de año de dos dígitos** es 2050 (valor predeterminado), 25 se interpreta como 2025 y 50 se interpreta como 1950. Para evitar ambigüedades, use años de cuatro dígitos.<br /><br /> (4) si falta el día, se proporciona el primer día del mes.<br /><br /> <br /><br /> El parámetro de sesión SET DATEFORMAT no se aplica cuando se especifica el mes de forma alfabética.|  
  
|ISO 8601|Description|  
|---|---|
|AAAA-MM-DDThh:mm:ss[.mmm]<br /><br /> AAAMMDD[ hh:mm:ss[.mmm]]|Ejemplos:<br /><br /> (1) 2004-05-23T14:25:10<br /><br /> (2) 2004-05-23T14:25:10.487<br /><br /> <br /><br /> Para utilizar el formato ISO 8601, debe especificar todos los elementos del formato. Esto también incluye el **T**, los dos puntos (:) y el punto (.) que se muestran en el formato.<br /><br /> Los corchetes indican que el componente de fracción de segundo es opcional. El componente de hora se especifica en el formato de 24 horas.<br /><br /> La T indica el inicio de la parte de hora la **datetime** valor.<br /><br /> La ventaja de utilizar el formato ISO 8601 es que se trata de un estándar internacional con una especificación que evita ambigüedades. Además, este formato no afecta a los parámetros SET DATEFORMAT o [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md) configuración.|  
  
|Sin separación|Description|  
|---|---|
|AAAAMMDD hh:mm:ss[.mmm]||  
  
|ODBC|Description|  
|---|---|
|{ ts '1998-05-02 01:23:56.123' }<br /><br /> { d '1990-10-02' }<br /><br /> { t '13:33:41' }|La API de ODBC define secuencias de escape para representar valores de fecha y de hora que ODBC llama datos de marca de tiempo. Este formato de marca de tiempo ODBC también es compatible con la definición del lenguaje OLE DB (DBGUID-SQL) compatible con la [!INCLUDE[msCoName](../../includes/msconame-md.md)] proveedor OLE DB para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las aplicaciones que usan las API basadas en ODBC, OLE DB y ADO pueden usar este formato de marca de tiempo de ODBC para representar fechas y horas.<br /><br /> Secuencias de escape de marca de tiempo ODBC de tienen el formato: { *literal_type* '*constant_value*'}:<br /><br /> <br /><br /> - *literal_type* especifica el tipo de la secuencia de escape. Las marcas de tiempo tienen tres *literal_type* especificadores:<br />(1) d. = solo fecha<br />(2) t = solo hora<br />(3) ts = marca de tiempo (hora + fecha)<br /><br /> <br /><br /> -'*constant_value*' es el valor de la secuencia de escape. *constant_value* debe seguir estos formatos para cada *literal_type*.<br />d.: aaaa-mm-dd<br />t: hh [.fff]<br />TS: aaaa-mm-dd hh [.fff]|  
  
## <a name="rounding-of-datetime-fractional-second-precision"></a>Redondeo de precisión de las fracciones de segundo de datetime  
**fecha y hora** valores se redondean con incrementos de.000,.003 o.007 segundos, tal como se muestra en la tabla siguiente.
  
|Valor especificado por el usuario|Valor almacenado por el sistema|  
|---|---|
|01/01/98 23:59:59.999|1998-01-02 00:00:00.000|  
|01/01/98 23:59:59.995<br /><br /> 01/01/98 23:59:59.996<br /><br /> 01/01/98 23:59:59.997<br /><br /> 01/01/98 23:59:59.998|1998-01-01 23:59:59.997|  
|01/01/98 23:59:59.992<br /><br /> 01/01/98 23:59:59.993<br /><br /> 01/01/98 23:59:59.994|1998-01-01 23:59:59.993|  
|01/01/98 23:59:59.990<br /><br /> 01/01/98 23:59:59.991|1998-01-01 23:59:59.990|  
  
## <a name="ansi-and-iso-8601-compliance"></a>Compatibilidad con ANSI e ISO 8601  
**fecha y hora** no es ANSI o ISO 8601 compatible.
  
##  <a name="_datetime"></a>Convertir datos de fecha y hora  
Cuando se convierte a los tipos de datos de fecha y hora, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rechaza todos los valores que no reconoce como fechas u horas. Para obtener información acerca de cómo utilizar las funciones CAST y CONVERT con datos de fecha y hora, vea [CAST y CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).
  
### <a name="converting-other-date-and-time-types-to-the-datetime-data-type"></a>Convertir otros tipos de fecha y hora para el tipo de datos de fecha y hora 
Esta sección describe lo que ocurre cuando los otros tipos de datos de fecha y hora se convierten a la **datetime** tipo de datos.  
  
Cuando la conversión es de **fecha**, se copian el año, mes y día. El componente de hora se establece en 00:00:00.000. En el código siguiente se muestran los resultados de convertir un valor `date` en un valor `datetime`.  
  
```sql
DECLARE @date date = '12-21-16';  
DECLARE @datetime datetime = @date;  
  
SELECT @datetime AS '@datetime', @date AS '@date';  
  
--Result  
--@datetime               @date  
------------------------- ----------  
--2016-12-21 00:00:00.000 2016-12-21  
```  
  
Cuando la conversión es de **Time (n)**, se copia el componente de hora, y el componente de fecha se establece en ' 1900-01-01'. Cuando la precisión fraccionaria de los **Time (n)** valor es superior a tres dígitos, el valor se truncará para ajustarse. En el siguiente ejemplo se muestran los resultados de convertir un valor `time(4)` en un valor `datetime`.  
  
```sql
DECLARE @time time(4) = '12:10:05.1237';  
DECLARE @datetime datetime = @time;  
  
SELECT @datetime AS '@datetime', @time AS '@time';  
  
--Result  
--@datetime               @time  
------------------------- -------------  
--1900-01-01 12:10:05.123 12:10:05.1237  
```  
  
Cuando la conversión es de **smalldatetime**, se copian las horas y minutos. Los segundos y las fracciones de segundo se establecen en 0. En el código siguiente se muestran los resultados de convertir un valor `smalldatetime` en un valor `datetime`.  
  
```sql
DECLARE @smalldatetime smalldatetime = '12-01-16 12:32';  
DECLARE @datetime datetime = @smalldatetime;  
  
SELECT @datetime AS '@datetime', @smalldatetime AS '@smalldatetime';  
  
--Result  
--@datetime               @smalldatetime  
------------------------- -----------------------  
--2016-12-01 12:32:00.000 2016-12-01 12:32:00  
```  
  
Cuando la conversión es de **DateTimeOffset (n)**, se copian los componentes de fecha y hora. Se trunca la zona horaria. Cuando la precisión fraccionaria de los **DateTimeOffset (n)** valor es superior a tres dígitos, el valor se truncará. En el siguiente ejemplo se muestran los resultados de convertir un valor `datetimeoffset(4)` en un valor `datetime`.  
  
```sql
DECLARE @datetimeoffset datetimeoffset(4) = '1968-10-23 12:45:37.1234 +10:0';  
DECLARE @datetime datetime = @datetimeoffset;  
  
SELECT @datetime AS '@datetime', @datetimeoffset AS '@datetimeoffset';  
  
--Result  
--@datetime               @datetimeoffset  
------------------------- ------------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237 +01:0   
```  
  
Cuando la conversión es de **datetime2**, se copian a la fecha y hora. Cuando la precisión fraccionaria de los **datetime2** valor es superior a tres dígitos, el valor se truncará. En el siguiente ejemplo se muestran los resultados de convertir un valor `datetime2(4)` en un valor `datetime`.  
  
```sql
DECLARE @datetime2 datetime2(4) = '1968-10-23 12:45:37.1237';  
DECLARE @datetime datetime = @datetime2;  
  
SELECT @datetime AS '@datetime', @datetime2 AS '@datetime2';  
  
--Result  
--@datetime               @datetime2  
------------------------- ------------------------  
--1968-10-23 12:45:37.123 1968-10-23 12:45:37.1237  
```  
  
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
  
  

