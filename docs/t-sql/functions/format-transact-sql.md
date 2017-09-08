---
title: FORMATO (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FORMAT_TSQL
- FORMAT
dev_langs:
- TSQL
helpviewer_keywords:
- FORMAT function
ms.assetid: dad6f24c-b8d9-4dbe-a561-9b167b8f20c8
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 75f944ad28bc56300db7ca9dd7220036faaea711
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="format-transact-sql"></a>FORMAT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve un valor con formato con el formato y la referencia cultural opcional especificados en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Use la función FORMAT para aplicar formato específico de la configuración regional de los valores de fecha/hora y de número como cadenas. Para las conversiones de tipos de datos generales, use CAST o CONVERT.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
FORMAT ( value, format [, culture ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *value*  
 Expresión de un tipo de datos compatible a la que se va a dar formato. Para obtener una lista de tipos válidos, vea la tabla de la sección Comentarios.  
  
 *formato*  
 **nvarchar** modelo de formato.  
  
 El *formato* argumento debe contener una cadena de formato de .NET Framework válida, como una cadena de formato estándar (por ejemplo, "C" o "D") o como un modelo de caracteres personalizados para las fechas y los valores numéricos (por ejemplo, "DD de MMMM, aaaa (dddd)") . No se admite el formato compuesto. Para obtener una explicación completa de estos modelos de formato, consulte la documentación de .NET Framework en la cadena de formato en general, fechas personalizado y formatos de hora y formatos de número personalizados. Un buen punto de partida es el tema "[aplicar formato a tipos](http://go.microsoft.com/fwlink/?LinkId=211776)."  
  
 *referencia cultural*  
 Opcional **nvarchar** argumento especifica una referencia cultural.  
  
 Si el *referencia cultural* no se proporciona un argumento, se utiliza el idioma de la sesión actual. Este idioma se establece implícitamente, o explícitamente mediante la instrucción SET LANGUAGE. *referencia cultural* acepta cualquier referencia cultural compatible con .NET Framework como argumento; no se limita a los idiomas admitidos explícitamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si el *referencia cultural* argumento no es válido, FORMAT producirá un error.  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar** o null  
  
 La longitud del valor devuelto viene determinada por la *formato*.  
  
## <a name="remarks"></a>Comentarios  
 FORMAT devuelve NULL para los errores distintos de un *referencia cultural* que no es *válido*. Por ejemplo, se devuelve NULL si el valor especificado en *formato* no es válido.  
 
 La función de formato es no determinista.   
  
 FORMATO se basa en la presencia del .NET Framework Common Language Runtime (CLR).  
  
 Esta función no puede ser remota, ya que depende de la presencia de CLR. Comunicación remota de una función que requiere el CLR, podría producirse un error en el servidor remoto.  
  
 FORMATO se basa en formato reglas que dictan que deben convertirse dos puntos y los períodos CLR. Por lo tanto, cuando la cadena de formato (segundo parámetro) contiene un coma o punto, los dos puntos o período deben convertirse con barra diagonal inversa cuando un valor de entrada (primer parámetro) es de la **tiempo** tipo de datos. Vea [formatoD.con tipos de datos de tiempo](#ExampleD).  
  
 En la tabla siguiente se enumera los tipos de datos aceptables para el *valor* argumento junto con sus tipos equivalentes de asignación de .NET Framework.  
  
|Categoría|Tipo|Tipo de .NET|  
|--------------|----------|---------------|  
|Numérico|bigint|Int64|  
|Numérico|int|Int32|  
|Numérico|smallint|Int16|  
|Numérico|tinyint|Byte|  
|Numérico|decimal|SqlDecimal|  
|Numérico|numeric|SqlDecimal|  
|Numérico|float|Double|  
|Numérico|real|Single|  
|Numérico|smallmoney|Decimal|  
|Numérico|money|Decimal|  
|Fecha y hora|date|DateTime|  
|Fecha y hora|time|Timespan|  
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
 En el ejemplo siguiente se muestran valores numéricos de formato especificando un formato personalizado. En el ejemplo se da por supuesto que la fecha actual es el 27 de septiembre de 2012. Para obtener más información sobre estos y otros formatos personalizados, vea [cadenas de formato numérico personalizado](http://msdn.microsoft.com/library/0c899ak8.aspx).  
  
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
 En el ejemplo siguiente se devuelve 5 filas de la **Sales.CurrencyRate** tabla el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos. La columna **EndOfDateRate** se almacena como tipo **dinero** en la tabla. En este ejemplo, la columna se devuelve sin formato y después con formato especificando el formato Number de .NET, el formato General y los tipos de formato Currency. Para obtener más información sobre estos y otros formatos numéricos, vea [cadenas de formato numérico estándar](http://msdn.microsoft.com/library/dwhawy9k.aspx).  
  
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
  
###  <a name="ExampleD"></a> D. FORMAT con tipos de datos de tiempo  
 FORMAT devuelve NULL en estos casos porque `.` y `:` sin escape.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh.mm');   --> returns NULL  
SELECT FORMAT(cast('07:35' as time), N'hh:mm');   --> returns NULL  
```  
  
 Format devuelve una cadena con formato porque la `.` y `:` son caracteres de escape.  
  
```sql  
SELECT FORMAT(cast('07:35' as time), N'hh\.mm');  --> returns 07.35  
SELECT FORMAT(cast('07:35' as time), N'hh\:mm');  --> returns 07:35  
```  
  
## <a name="see-also"></a>Vea también  
 [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  

