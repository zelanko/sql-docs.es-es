---
title: FORMAT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FORMAT_TSQL
- FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions||=azure-sqldw-latest
ms.openlocfilehash: fd44673ce62d74349e83b09b020c9e20ab6957de
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "70155798"
---
# <a name="format-transact-sql"></a>FORMAT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

Devuelve un valor con formato con el formato y la referencia cultural opcional especificados. Use la función FORMAT para aplicar formato específico de la configuración regional de los valores de fecha/hora y de número como cadenas. Para las conversiones de tipos de datos generales, use CAST o CONVERT.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>Argumentos

 *value*  
 Expresión de un tipo de datos compatible a la que se va a dar formato. Para obtener una lista de tipos válidos, vea la tabla de la sección Comentarios.  
  
 *format*  
 Patrón de formato **nvarchar**.  
  
 El argumento *format* debe contener una cadena de formato de .NET Framework válida, ya sea como una cadena de formato estándar (por ejemplo, "C" o "D") o como un modelo de caracteres personalizados para los valores de fecha y numéricos (por ejemplo, "DD de MMMM, aaaa (dddd)"). No se admite el formato compuesto. Para obtener una explicación completa de estos modelos de formato, vea la documentación de .NET Framework sobre el formato de cadena en general, los formatos de fecha y hora personalizados, y los formatos de número personalizados. Un buen punto de partida es el tema "[Formatting Types](https://go.microsoft.com/fwlink/?LinkId=211776)" (Tipos de formato).  
  
 *referencia cultural*  
 Argumento opcional de tipo **nvarchar** que especifica una referencia cultural.  
  
 Si no se proporciona el argumento *culture*, se usará el idioma de la sesión actual. Este idioma se establece implícitamente, o explícitamente mediante la instrucción SET LANGUAGE. *culture* acepta como argumento cualquier referencia cultural compatible con .NET Framework; no se limita a los idiomas admitidos explícitamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si el argumento *culture* no es válido, FORMAT desencadena un error.  
  
## <a name="return-types"></a>Tipos de valor devuelto

 **nvarchar** o null  
  
 La longitud del valor devuelto viene determinada por *format*.  
  
## <a name="remarks"></a>Observaciones

 FORMAT devuelve NULL para los errores distintos de *culture* que no son *válidos*. Por ejemplo, se devuelve NULL si el valor especificado en *format* no es válido.  

 La función FORMAT es no determinista.
  
 FORMAT se basa en la presencia de Common Language Runtime (CLR) de .NET Framework.  
  
 Esta función no se puede enviar de forma remota puesto que depende de la presencia del CLR. El envío remoto de una función que necesita CLR produciría un error en el servidor remoto.  
  
 FORMAT se basa en las reglas de formato de CLR, que dictan que los signos de punto y de dos puntos deben incluir caracteres de escape. Por tanto, cuando la cadena de formato (segundo parámetro) contiene un signo de punto o de dos puntos, estos deben incluir caracteres de escape, como una barra diagonal inversa, cuando un valor de entrada (primer parámetro) es del tipo de datos **time**. Vea [D. FORMAT con tipos de datos de tiempo](#ExampleD).  
  
 En esta tabla se muestran los tipos de datos aceptables para el argumento *value*, junto con sus tipos equivalentes de asignación de .NET Framework.  
  
|Category|Tipo|Tipo de .NET|  
|--------------|----------|---------------|  
|Numeric|bigint|Int64|  
|Numeric|int|Int32|  
|Numeric|SMALLINT|Int16|  
|Numeric|TINYINT|Byte|  
|Numeric|Decimal|SqlDecimal|  
|Numeric|NUMERIC|SqlDecimal|  
|Numeric|FLOAT|Double|  
|Numeric|real|Single|  
|Numeric|SMALLMONEY|Decimal|  
|Numeric|money|Decimal|  
|Fecha y hora|date|DateTime|  
|Fecha y hora|time|TimeSpan|  
|Fecha y hora|datetime|DateTime|  
|Fecha y hora|smalldatetime|DateTime|  
|Fecha y hora|datetime2|DateTime|  
|Fecha y hora|datetimeoffset|DateTimeOffset|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-simple-format-example"></a>A. Ejemplo de FORMAT sencillo

 En el ejemplo siguiente se devuelve una fecha simple con formato para distintas referencias culturales.  
  
```sql  
DECLARE @d DATETIME = '10/01/2011';  
SELECT FORMAT ( @d, 'd', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'd', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'd', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'd', 'zh-cn' ) AS 'Simplified Chinese (PRC) Result';
  
SELECT FORMAT ( @d, 'D', 'en-US' ) AS 'US English Result'  
      ,FORMAT ( @d, 'D', 'en-gb' ) AS 'Great Britain English Result'  
      ,FORMAT ( @d, 'D', 'de-de' ) AS 'German Result'  
      ,FORMAT ( @d, 'D', 'zh-cn' ) AS 'Chinese (Simplified PRC) Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
US English Result Great Britain English Result  German Result Simplified Chinese (PRC) Result  
----------------  ----------------------------- ------------- -------------------------------------  
10/1/2011         01/10/2011                    01.10.2011    2011/10/1  
  
(1 row(s) affected)  
  
US English Result            Great Britain English Result  German Result                    Chinese (Simplified PRC) Result  
---------------------------- ----------------------------- -----------------------------  ---------------------------------------  
Saturday, October 01, 2011   01 October 2011               Samstag, 1. Oktober 2011        2011年10月1日  
  
(1 row(s) affected)  
```  
  
### <a name="b-format-with-custom-formatting-strings"></a>B. FORMAT con cadenas de formato personalizado

 En el ejemplo siguiente se muestran valores numéricos de formato especificando un formato personalizado. En el ejemplo se da por supuesto que la fecha actual es el 27 de septiembre de 2012. Para más información sobre estos y otros formatos personalizados, vea [Cadenas con formato numérico personalizado](https://msdn.microsoft.com/library/0c899ak8.aspx).  
  
```sql  
DECLARE @d DATETIME = GETDATE();  
SELECT FORMAT( @d, 'dd/MM/yyyy', 'en-US' ) AS 'DateTime Result'  
       ,FORMAT(123456789,'###-##-####') AS 'Custom Number Result';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
DateTime Result  Custom Number Result  
--------------   --------------------  
27/09/2012       123-45-6789  
  
(1 row(s) affected)  
```  
  
### <a name="c-format-with-numeric-types"></a>C. FORMAT con tipos numéricos

 En este ejemplo se devuelven 5 filas de la tabla **Sales.CurrencyRate** de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. La columna **EndOfDateRate** se almacena como el tipo **money** en la tabla. En este ejemplo, la columna se devuelve sin formato y después con formato especificando el formato Number de .NET, el formato General y los tipos de formato Currency. Para más información sobre estos y otros formatos numéricos, vea [Cadenas con formato numérico estándar](https://msdn.microsoft.com/library/dwhawy9k.aspx).  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
            ,FORMAT(EndOfDayRate, 'N', 'en-us') AS 'Number Format'  
            ,FORMAT(EndOfDayRate, 'G', 'en-us') AS 'General Format'  
            ,FORMAT(EndOfDayRate, 'C', 'en-us') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1.00            1.0002          $1.00  
2              1.55          1.55            1.5500          $1.55  
3              1.9419        1.94            1.9419          $1.94  
4              1.4683        1.47            1.4683          $1.47  
5              8.2784        8.28            8.2784          $8.28  
  
(5 row(s) affected)  
  
```  
  
 En este ejemplo se especifica la referencia cultural de alemán (de-de).  
  
```sql  
SELECT TOP(5)CurrencyRateID, EndOfDayRate  
      ,FORMAT(EndOfDayRate, 'N', 'de-de') AS 'Numeric Format'  
      ,FORMAT(EndOfDayRate, 'G', 'de-de') AS 'General Format'  
      ,FORMAT(EndOfDayRate, 'C', 'de-de') AS 'Currency Format'  
FROM Sales.CurrencyRate  
ORDER BY CurrencyRateID;  
```  
  
```
CurrencyRateID EndOfDayRate  Numeric Format  General Format  Currency Format  
-------------- ------------  --------------  --------------  ---------------  
1              1.0002        1,00            1,0002          1,00 €  
2              1.55          1,55            1,5500          1,55 €  
3              1.9419        1,94            1,9419          1,94 €  
4              1.4683        1,47            1,4683          1,47 €  
5              8.2784        8,28            8,2784          8,28 €  
  
 (5 row(s) affected)  
```  
  
### <a name="ExampleD"></a> D. FORMAT con tipos de datos de tiempo

 FORMAT devuelve NULL en estos casos porque `.` y `:` no incluyen caracteres de escape.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 FORMAT devuelve una cadena con formato porque `.` y `:` incluyen caracteres de escape.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  

FORMAT devuelve la hora actual con el formato AM o PM especificado.

```sql
SELECT FORMAT(SYSDATETIME(), N'hh:mm tt'); -- returns 03:46 PM
SELECT FORMAT(SYSDATETIME(), N'hh:mm t'); -- returns 03:46 P
```

FORMAT devuelve el tiempo especificado en formato AM.

```sql
select FORMAT(CAST('2018-01-01 01:00' AS datetime2), N'hh:mm tt') -- returns 01:00 AM
select FORMAT(CAST('2018-01-01 01:00' AS datetime2), N'hh:mm t')  -- returns 01:00 A
```

FORMAT devuelve el tiempo especificado en formato PM.

```sql
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'hh:mm tt') -- returns 02:00 PM
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'hh:mm t') -- returns 02:00 P
```
  
FORMAT devuelve el tiempo especificado en formato 24h.

```sql
select FORMAT(CAST('2018-01-01 14:00' AS datetime2), N'HH:mm') -- returns 14:00
```
  
## <a name="see-also"></a>Consulte también

 [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
 [STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)  
 [Funciones de cadena &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
