---
title: CAST y CONVERT (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CAST_TSQL
- CONVERT_TSQL
- CAST
- CONVERT
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- automatic data type conversion
- varbinary data type
- CONVERT function
- data types [SQL Server], converting
- large value data types
- implicit data type conversions
- image data type, converting
- explicit data type conversions [SQL Server]
- binary [SQL Server], converting
- text data type, converting
- date and time [SQL Server], cast and convert
- truncating conversions
- converting data types [SQL Server], conversion functions
- time zones [SQL Server]
- roundtrip conversions
ms.assetid: a87d0850-c670-4720-9ad5-6f5a22343ea8
caps.latest.revision: 136
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: e1ea8183c7655af863fe5f6267958f4c8df367dc
ms.contentlocale: es-es
ms.lasthandoff: 09/08/2017

---
# <a name="cast-and-convert-transact-sql"></a>CAST y CONVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Convierte una expresión de un tipo de datos en otro.  
Por ejemplo, en los ejemplos siguientes cambian el tipo de datos de entrada, en dos otros tipos de datos, con distintos niveles de precisión.
```sql  
SELECT 9.5 AS Original, CAST(9.5 AS int) AS int, 
    CAST(9.5 AS decimal(6,4)) AS decimal;
SELECT 9.5 AS Original, CONVERT(int, 9.5) AS int, 
    CONVERT(decimal(6,4), 9.5) AS decimal;
```  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
|Texto original en   |int    |decimal |  
|----|----|----|  
|9.5 |9 |9.5000 |  

> [!TIP]
> Muchos [ejemplos](#BKMK_examples) están en la parte inferior de este tema.  
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
-- Syntax for CAST:  
CAST ( expression AS data_type [ ( length ) ] )  
  
-- Syntax for CONVERT:  
CONVERT ( data_type [ ( length ) ] , expression [ , style ] )  
```  
  
## <a name="arguments"></a>Argumentos  
*expression*  
Se trata de cualquier [expresión](../../t-sql/language-elements/expressions-transact-sql.md).
  
*data_type*  
Es el tipo de datos de destino. Esto incluye **xml**, **bigint**, y **sql_variant**. No se pueden utilizar tipos de datos de alias.
  
*length*  
Es un número entero opcional que especifica la longitud del tipo de datos de destino. El valor predeterminado es 30.
  
*estilo*  
Expresión entera que especifica cómo la función CONVERT convertir *expresión*. Si style es NULL, se devuelve NULL. Determina el intervalo por *data_type*. 
  
## <a name="return-types"></a>Tipos de valor devuelto
Devuelve *expresión* traducirse a *data_type*.

## <a name="date-and-time-styles"></a>Estilos de fecha y hora  
Cuando *expresión* es un tipo de datos de fecha u hora, *estilo* puede ser uno de los valores mostrados en la tabla siguiente. Otros valores se procesan como 0. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los únicos estilos que se admiten al convertir de fecha y hora tipos **datetimeoffset** son 0 ó 1. Todos los demás estilos de conversión devuelven el error 9809.
  
>  [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el formato de fecha en estilo árabe mediante el algoritmo kuwaití.
  
|Sin el siglo (AA) (<sup>1</sup>)|Con el siglo (aaaa)|Standard|Entrada/salida (<sup>3</sup>)|  
|---|---|--|---|
|-|**0** o **100** (<sup>1,</sup><sup>2</sup>)|Valor predeterminado para datetime y smalldatetime|mes dd aaaa hh:mia.m. (o p.m.)|  
|**1**|**101**|EE. UU.|1 = mm/dd/aa<br /> 101 = mm/dd/aaaa|  
|**2**|**102**|ANSI|2 = aa.mm.dd<br /> 102 = aaaa.mm.dd|  
|**3**|**103**|Británico/Francés|3 = dd/mm/aa<br /> 103 = dd/mm/aaaa|  
|**4**|**104**|Alemán|4 = dd.mm.aa<br /> 104 = dd.mm.aaaa|  
|**5**|**105**|Italiano|5 = dd-mm-aa<br /> 105 = dd-mm-aaaa|  
|**6**|**106** <sup>(1)</sup>|-|6 = dd mes aa<br /> 106 = dd mes aaaa|  
|**7**|**107** <sup>(1)</sup>|-|7 = Mes dd, aa<br /> 107 = Mes dd, aaaa|  
|**8**|**108**|-|hh:mi:ss|  
|-|**9** o **109** (<sup>1,</sup><sup>2</sup>)|Valor predeterminado + milisegundos|mes dd aaaa hh:mi:ss:mmma.m. (o p.m.)|  
|**10**|**110**|EE. UU.|10 = mm-dd-aa<br /> 110 = mm-dd-aaaa|  
|**11**|**111**|JAPÓN|11 = aa/mm/dd<br /> 111 = aaaa/mm/dd|  
|**12**|**112**|ISO|12 = aammdd<br /> 112 = aaaammdd|  
|-|**13** o **113** (<sup>1,</sup><sup>2</sup>)|Europeo predeterminado + milisegundos|dd mes aaaa hh:mi:ss:mmm(24h)|  
|**14**|**114**|-|hh:mi:ss:mmm(24h)|  
|-|**20** o **120** (<sup>2</sup>)|ODBC canónico|aaaa-mm-dd hh:mi:ss(24h)|  
|-|**21** o **121** (<sup>2</sup>)|ODBC canónico (con milisegundos), valor predeterminado para time, date, datetime2 y datetimeoffset|aaaa-mm-dd hh:mi:ss.mmm(24h)|  
|-|**126** (<sup>4</sup>)|ISO8601|aaaa-mm-ddThh:mi:ss.mmm (sin espacios)<br /> Nota: Si el valor de milisegundos (mmm) es 0, no se muestra el valor de milisegundos. Por ejemplo, el valor '2012-11-07T18:26:20.000' se muestra como '2012-11-07T18:26:20'.|  
|-|**127**(<sup>6, 7</sup>)|ISO8601 con zona horaria Z.|aaaa-mm-ddThh:mi:ss.mmmZ (sin espacios)<br /> Nota: Si el valor de milisegundos (mmm) es 0, no se muestra el valor de milisegundos. Por ejemplo, el valor '2012-11-07T18:26:20.000' se muestra como '2012-11-07T18:26:20'.|  
|-|**130** (<sup>1,</sup><sup>2</sup>)|Hijri (<sup>5</sup>)|dd mes aaaa hh:mi:ss:mmma.m.<br /> En este estilo, mes es una representación Unicode Hijri multitoken del nombre completo del mes. Este valor no se representan correctamente en el valor predeterminado es instalación estadounidense de SSMS.|  
|-|**131** (<sup>2</sup>)|Hijri (<sup>5</sup>)|dd/mm/aaaa hh:mi:ss:mmma.m.|  
  
<sup>1</sup> estos valores de estilo devuelven resultados no deterministas. Incluye todos los estilos (aa) (sin el siglo) y un subconjunto de estilos (aaaa) (con el siglo).
  
<sup>2</sup> los valores predeterminados (*estilo** *0** o **100**, **9** o **109**, **13** o **113**, **20** o **120**, y **21** o **121**) siempre devuelven el siglo (aaaa).
  
<sup>3</sup> entrada cuando se convierte a **datetime**; salida cuando se convierte en datos de caracteres.
  
<sup>4</sup> diseñado para usarse con XML. Para la conversión de **datetime** o **smalldatetime** para datos de caracteres, el formato de salida es como se describe en la tabla anterior.
  
<sup>5</sup> Hijri es un sistema de calendario con varias variaciones. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el algoritmo kuwaití.
  
> [!IMPORTANT]  
>  De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreta los años de dos dígitos según el año límite 2049. Es decir, el año 49 de dos dígitos se interpreta como 2049 y el año 50 de dos dígitos se interpreta como 1950. Muchas aplicaciones cliente, como las que se basan en objetos de Automation, utilizan el año límite de 2030. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]proporciona la opción de configuración límite de año de dos dígitos que cambia el año límite utilizado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y permite el tratamiento coherente de fechas. Se recomienda especificar años de cuatro dígitos.  
  
<sup>6</sup> solo se admite al convertir el tipo de datos de caracteres a **datetime** o **smalldatetime**. Cuando los datos de caracteres que representa solo fecha o únicamente los componentes de hora se convierte en el **datetime** o **smalldatetime** tipos de datos, el componente de hora no especificada se establece en 00:00:00.000 y el no especificado componente de fecha se establece en 1900-01-01.
  
<sup>7</sup>el indicador opcional de zona horaria, Z, se utiliza para que sea más fácil asignar XML **datetime** valores que tienen información de zona horaria para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** valores que no tienen zona horaria . Z es el indicador para la zona horaria UTC-0. Las otras zonas horarias se indican con un desplazamiento de HH:MM en sentido + o -. Por ejemplo: `2006-12-12T23:45:12-08:00`.
  
Cuando se convierte en datos de caracteres de **smalldatetime**, los estilos que incluyen segundos o milisegundos muestran ceros en dichas posiciones. Puede truncar las partes de fecha no deseadas cuando se convierte de **datetime** o **smalldatetime** valores mediante el uso de una adecuada **char** o **varchar** longitud del tipo de datos.
  
Cuando se convierte a **datetimeoffset** de datos de caracteres con un estilo que incluye un tiempo, se anexa un ajuste de zona horaria al resultado.
  
## <a name="float-and-real-styles"></a>estilos float y real
Cuando *expresión* es **float** o **real**, *estilo* puede ser uno de los valores mostrados en la tabla siguiente. Otros valores se procesan como 0.
  
|Valor|Salida|  
|---|---|
|**0** (valor predeterminado)|Un máximo de 6 dígitos. Utilícelo en notación científica cuando proceda.|  
|**1**|Siempre 8 dígitos. Utilícelo siempre en notación científica.|  
|**2**|Siempre 16 dígitos. Utilícelo siempre en notación científica.|  
|**3**|Siempre 17 dígitos. Se usa para la conversión sin pérdida de datos. Con este estilo, se garantiza que todos los distinto float o un valor real para convertir en una cadena de caracteres distintos.<br /> **Se aplica a:** [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]y a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].|  
|**126, 128, 129**|Se incluye por razones heredadas y podría quedar desusado en una versión futura.|  
  
## <a name="money-and-smallmoney-styles"></a>estilos Money y smallmoney
Cuando *expresión* es **dinero** o **smallmoney**, *estilo* puede ser uno de los valores mostrados en la tabla siguiente. Otros valores se procesan como 0.
  
|Valor|Salida|  
|---|---|
|**0** (valor predeterminado)|Sin separadores de millar cada tres dígitos a la izquierda del separador decimal y dos dígitos a la derecha del separador decimal; por ejemplo, 4235,98.|  
|**1**|Separadores de millar cada tres dígitos a la izquierda del separador decimal y dos dígitos a la derecha del separador decimal; por ejemplo, 3.510,92.|  
|**2**|Sin separadores de millar cada tres dígitos a la izquierda del separador decimal y cuatro dígitos a la derecha del separador decimal; por ejemplo, 4235,9819.|  
|**126**|Equivalente al estilo 2 al convertir a char(n) o varchar(n)|  
  
## <a name="xml-styles"></a>estilos de XML
Cuando *expresión* es **xml***, estilo* puede ser uno de los valores mostrados en la tabla siguiente. Otros valores se procesan como 0.
  
|Valor|Salida|  
|---|---|
|**0** (valor predeterminado)|Utiliza el comportamiento de análisis predeterminado que descarta los espacios en blanco insignificantes y no permite un subconjunto DTD interno.<br /> **Nota:** cuando se convierte a la **xml** tipo de datos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espacios en blanco no significativos se tratan de forma diferente que en XML 1.0. Para obtener más información, consulte [crear instancias de datos de XML](../../relational-databases/xml/create-instances-of-xml-data.md).|  
|**1**|Conserva los espacios en blanco insignificantes. Esta configuración establece el valor predeterminado **XML: space** control se comporte de la misma como si **XML: space = "preserve"** se ha especificado en su lugar.|  
|**2**|Habilita el procesamiento limitado de subconjuntos DTD internos.<br /><br /> Si está habilitado, el servidor puede utilizar la siguiente información proporcionada en un subconjunto DTD interno para realizar operaciones de análisis que no se validan.<br /> -Los valores predeterminados para los atributos se aplican.<br /> -Se resuelve las referencias de entidad interno y se expanden.<br /> -El modelo de contenido de DTD se comprueba para la corrección sintáctica.<br /> El analizador pasa por alto los subconjuntos DTD externos. También no se evalúe la declaración XML para ver si el **independiente** se establece el atributo **Sí** o **sin**, pero analiza la instancia XML como si fuera una independiente documento.|  
|**3**|Conserva los espacios en blanco insignificantes y habilita el procesamiento limitado de los subconjuntos DTD internos.|  
  
## <a name="binary-styles"></a>Estilos binarios
Cuando *expresión* es **Binary**, **varbinary**, **char**, o **varchar**, *estilo* puede ser uno de los valores mostrados en la tabla siguiente. Los valores de estilos que no se enumeran en la tabla devuelven un error.
  
|Valor|Salida|  
|---|---|
|**0** (valor predeterminado)|Traduce caracteres ASCII a bytes binarios o bytes binarios a caracteres ASCII. Cada carácter o byte se convierte con una proporción 1:1.<br /> Si el *data_type* es un tipo binario, los caracteres 0 x se agregan a la izquierda del resultado.|  
|**1**, **2**|Si el *data_type* es un tipo binario, la expresión debe ser una expresión de caracteres. El *expresión* debe estar formada por un número par de dígitos hexadecimales (0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F, a, b, c, d, e, f). Si el *estilo* está establecido en 1 los caracteres 0 x deben ser los primeros dos caracteres en la expresión. Si la expresión contiene un número impar de caracteres o si alguno de los caracteres no es válido, se produce un error.<br /> Si la longitud de la expresión convertida es mayor que la longitud de la *data_type* derecha se trunca el resultado.<br /> Longitud fija *data_types* que serán más grandes que el resultado convertido tiene ceros agregados a la derecha del resultado.<br /> Si data_type es un tipo de caracteres, la expresión debe ser binaria. Cada carácter binario se convierte en dos caracteres hexadecimales. Si la longitud de la expresión convertida es mayor que el *data_type* longitud, se truncará derecha.<br /> Si el *data_type* es un tipo de carácter de tamaño fijo y la longitud del resultado convertido es menor que la longitud de la *data_type*; espacios se agregan a la derecha de la expresión convertida para mantener un par número de dígitos hexadecimales.<br /> Los caracteres 0 x se agregarán a la izquierda del resultado convertido para *estilo* 1.|  
  
## <a name="implicit-conversions"></a>Conversiones implícitas
Las conversiones implícitas son aquellas conversiones que tienen lugar sin especificar las funciones CAST o CONVERT. Las conversiones explícitas son aquellas conversiones que requieren la especificación de las funciones CAST o CONVERT. En la ilustración siguiente se muestran todas las conversiones de tipos de datos explícitas e implícitas permitidas para los tipos de datos proporcionados por el sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede tratarse de **xml**, **bigint**, y **sql_variant**. No hay ninguna conversión implícita en la asignación de la **sql_variant** tipo de datos, pero no hay conversión implícita a **sql_variant**.
  
> [!TIP]  
>  Este gráfico está disponible como un archivo PDF para descargar en el [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=35834).  
  
![Tabla de conversión de tipos de datos](../../t-sql/data-types/media/lrdatahd.png "tabla de conversión de tipos de datos")
  
Al convertir entre **datetimeoffset** y los tipos de caracteres **char**, **varchar**, **nchar**, y **nvarchar ** la zona horaria convertida desplazamiento siempre debe dígitos dobles para HH y MM, por ejemplo, -08:00.
  
> [!NOTE]  
>  Dado que los datos Unicode siempre utilizan un número par de bytes, tenga cuidado al convertir **binario** o **varbinary** , o a Unicode admite los tipos de datos. Por ejemplo, la siguiente conversión no devuelve el valor hexadecimal 41, sino 4100: `SELECT CAST(CAST(0x41 AS nvarchar) AS varbinary)`.  
  
## <a name="large-value-data-types"></a>Tipos de datos de valores grandes
Tipos de datos de valores grandes tienen el mismo comportamiento de conversión implícita y explícita como sus equivalentes más pequeños, específicamente el **varchar**, **nvarchar** y **varbinary**tipos de datos. No obstante, se deben tener en cuenta las siguientes directrices:
-   Conversión de **imagen** a **varbinary (max)** y viceversa es una conversión implícita y, por lo tanto, son las conversiones entre **texto** y **varchar (max)**, y **ntext** y **nvarchar (max)**.  
-   Tipos de conversión de datos de valores grandes, como **varchar (max)**, a un menor equivalente de tipo de datos, como **varchar**, es una conversión implícita, pero se produce un truncamiento si el valor grande es demasiado grande para el Especifica la longitud del tipo de datos más pequeño.  
-   Conversión de **varchar**, **nvarchar**, o **varbinary** a sus datos de valor grande correspondientes tipos se realiza de forma implícita.  
-   Conversión de la **sql_variant** tipo de datos a los tipos de datos de valores grandes es una conversión explícita.  
-   No se puede convertir tipos de datos de valor grande para la **sql_variant** tipo de datos.  
  
Para obtener más información sobre cómo convertir desde el **xml** tipo de datos, vea [crear instancias de datos de XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
## <a name="xml-data-type"></a>Tipo de datos XML
Cuando se explícita o implícitamente convierte los **xml** tipo de datos a una cadena o tipo de datos binario, el contenido de la **xml** tipo de datos se serializa en función de un conjunto de reglas. Para obtener información acerca de estas reglas, consulte [definir los datos de serialización de XML](../../relational-databases/xml/define-the-serialization-of-xml-data.md). Para obtener información sobre cómo convertir otros tipos de datos en el **xml** tipo de datos, vea [crear instancias de datos de XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
## <a name="text-and-image-data-types"></a>tipos de datos text e image
No se admite la conversión de tipos de datos automática para la **texto** y **imagen** tipos de datos. Puede convertir explícitamente **texto** datos a datos de caracteres, y **imagen** datos a **binario** o **varbinary**, pero la longitud máxima es 8000 bytes. Si trata de una conversión incorrecta, como convertir una expresión de caracteres que incluya letras a un **int**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un mensaje de error.
  
## <a name="output-collation"></a>Intercalación de salida  
Cuando la salida de CAST o CONVERT es una cadena de caracteres y la entrada es otra, la salida tiene la misma intercalación y etiqueta de intercalación que la entrada. Si la entrada no es una cadena de caracteres, la salida tiene la intercalación predeterminada de la base de datos y una etiqueta de intercalación coaccionable-predeterminada. Para obtener más información, vea [prioridad de intercalación &#40; Transact-SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).
  
Para asignar otra intercalación a la salida, aplique la cláusula COLLATE a la expresión de resultado de las funciones CAST o CONVERT. Por ejemplo:
  
`SELECT CAST('abc' AS varchar(5)) COLLATE French_CS_AS`
  
## <a name="truncating-and-rounding-results"></a>Truncar y redondear resultados
Al convertir caracteres o expresiones binarias (**char**, **nchar**, **nvarchar**, **varchar**, **binario**, o **varbinary**) en una expresión de un tipo de datos diferente, se pueden truncar datos presentar parcialmente o se devuelve un error porque el resultado es demasiado corto para ser mostrado. Las conversiones a **char**, **varchar**, **nchar**, **nvarchar**, **binario**, y ** varbinary** se truncan, excepto para las conversiones que se muestra en la tabla siguiente.
  
|De tipo de datos|En tipo de datos|Resultado|  
|---|---|---|
|**int**, **smallint**, o **tinyint**|**char**|*|  
||**varchar**|*|  
||**nchar**|E|  
||**nvarchar**|E|  
|**Money**, **smallmoney**, **numérico**, **decimal**, **float**, o **real**|**char**|E|  
||**varchar**|E|  
||**nchar**|E|  
||**nvarchar**|E|  
  
\*= La longitud del resultado demasiado corta para ser mostrado. E = Error devuelto porque el resultado es demasiado corto para ser mostrado.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]garantiza que sólo las conversiones circulares, las conversiones que convertir a un tipo de datos de su tipo de datos original y volver a producen los mismos valores de una versión a otra. En el siguiente ejemplo se muestra una conversión circular:
  
```sql
DECLARE @myval decimal (5, 2);  
SET @myval = 193.57;  
SELECT CAST(CAST(@myval AS varbinary(20)) AS decimal(10,5));  
-- Or, using CONVERT  
SELECT CONVERT(decimal(10,5), CONVERT(varbinary(20), @myval));  
```  
  
> [!NOTE]  
>  No intente crear **binario** valores y, a continuación, convertirlos en un tipo de datos de la categoría de tipo de datos numérico. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no garantiza que el resultado de un **decimal** o **numérico** conversión al tipo de datos **binario** será el mismo entre las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
En el siguiente ejemplo se muestra una expresión resultante demasiado corta para ser mostrada.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, SUBSTRING(p.Title, 1, 25) AS Title,
    CAST(e.SickLeaveHours AS char(1)) AS [Sick Leave]  
FROM HumanResources.Employee e JOIN Person.Person p 
    ON e.BusinessEntityID = p.BusinessEntityID  
WHERE NOT e.BusinessEntityID >5;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```   
FirstName   LastName      Title   Sick Leave
---------   ------------- ------- --------`
Ken         Sanchez       NULL   *
Terri       Duffy         NULL   *
Roberto     Tamburello    NULL   *
Rob         Walters       NULL   *
Gail        Erickson      Ms.    *
(5 row(s) affected)  
```
  
Al convertir tipos de datos que difieren en los decimales, algunas veces el valor resultante se trunca y otras se redondea. En la siguiente tabla se muestra el comportamiento.
  
|De|Para|Comportamiento|  
|---|---|---|
|**numeric**|**numeric**|Redondear|  
|**numeric**|**int**|Truncamiento|  
|**numeric**|**money**|Redondear|  
|**money**|**int**|Redondear|  
|**money**|**numeric**|Redondear|  
|**float**|**int**|Truncamiento|  
|**float**|**numeric**|Redondear<br /><br /> Conversión de **float** valores que utiliza la notación científica a **decimal** o **numérico** está restringida a valores de precisión de 17 dígitos solo. Cualquier valor con una precisión mayor de 17 se redondea a cero.|  
|**float**|**datetime**|Redondear|  
|**datetime**|**int**|Redondear|  
  
Por ejemplo, pueden truncar o redondea durante la conversión a los valores 10.6496 y-10.6496 **int** o **numérico** tipos:
  
```sql
SELECT  CAST(10.6496 AS int) as trunc1,
         CAST(-10.6496 AS int) as trunc2,
         CAST(10.6496 AS numeric) as round1,
         CAST(-10.6496 AS numeric) as round2;
 ```
Resultados de la consulta se muestran en la tabla siguiente:
 
|trunc1|trunc2|round1|round2|
|---|---|---|---|
|10|-10|11|-11|
 
Al convertir tipos de datos cuando el tipo de datos de destino tiene menos decimales que el tipo de datos de origen, el valor se redondea. Por ejemplo, el resultado de la siguiente conversión es `$10.3497`:
  
`SELECT CAST(10.3496847 AS money);`
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Devuelve un mensaje de error cuando un valor no numérico **char**, **nchar**, **varchar**, o **nvarchar** datos se convierten en **int **, **float**, **numérico**, o **decimal**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]También devuelve un error cuando una cadena vacía ("") se convierte en **numérico** o **decimal**.
  
## <a name="certain-datetime-conversions-are-nondeterministic"></a>Determinadas conversiones de fecha y hora son no deterministas
En la siguiente tabla se muestran los estilos para los que la conversión de cadena a fecha y hora es no determinista.
  
|||  
|-|-|  
|Todos los estilos por debajo de 100<sup>1</sup>|106|  
|107|109|  
|113|130|  
  
<sup>1</sup> con la excepción de los estilos 20 y 21
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementarios (pares suplentes)
A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], si utiliza intercalaciones de caracteres suplementarios (SC), una operación de conversión de **nchar** o **nvarchar** a una **nchar** o ** nvarchar** tipo de menor longitud no truncará dentro de un par suplente; truncará antes del carácter suplementario. Por ejemplo, el fragmento de código siguiente deja `@x` con solo `'ab'`. No hay espacio suficiente para albergar el carácter suplementario.
  
```sql
DECLARE @x NVARCHAR(10) = 'ab' + NCHAR(0x10000);  
SELECT CAST (@x AS NVARCHAR(3));  
```  
  
Al utilizar intercalaciones de SC, el comportamiento de `CONVERT` es análogo al de `CAST`.
  
## <a name="compatibility-support"></a>Soporte de compatibilidad
En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el estilo predeterminado para las operaciones CAST y CONVERT en **tiempo** y **datetime2** tipos de datos es 121, a menos que se utilizan cualquiera de estos tipos en una expresión de columna calculada. Para las columnas calculadas, el estilo predeterminado es 0. Este comportamiento afecta a las columnas calculadas cuando se crean, cuando se utilizan en las consultas que implican parametrización automática o cuando se usan en definiciones de restricciones.
  
En el nivel de compatibilidad 110 y posterior, el estilo predeterminado de las operaciones CAST y CONVERT en **tiempo** y **datetime2** tipos de datos es siempre 121. Si su consulta se basa en el comportamiento anterior, use un nivel de compatibilidad menor de 110, o especifique explícitamente el estilo 0 en la consulta correspondiente.
  
Actualizar la base de datos al nivel de compatibilidad 110 y posteriores no cambiará los datos de usuario que se hayan almacenado en disco. Debe corregir manualmente estos datos según convenga. Por ejemplo, si utilizara SELECT INTO para crear una tabla de un origen que contuviera una expresión de columna calculada como la descrita anteriormente, se almacenarían los datos (si se usa el estilo 0) en lugar de la propia definición de columna calculada. Debería actualizar manualmente estos datos para que coincidieran con el estilo 121.
  
## <a name="BKMK_examples"></a> Ejemplos  
  
### <a name="a-using-both-cast-and-convert"></a>A. Utilizar CAST y CONVERT  
En cada ejemplo se recupera el nombre de aquellos productos que tienen un `3` como primer dígito del precio y se convierte `ListPrice` en `int`.
  
```sql
-- Use CAST  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CAST(ListPrice AS int) LIKE '3%';  
GO  
  
-- Use CONVERT.  
USE AdventureWorks2012;  
GO  
SELECT SUBSTRING(Name, 1, 30) AS ProductName, ListPrice  
FROM Production.Product  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
GO  
```  
  
### <a name="b-using-cast-with-arithmetic-operators"></a>B. Utilizar CAST con operadores aritméticos  
En el siguiente ejemplo se calcula una única columna (`Computed`) mediante la división de las ventas anuales hasta la fecha (`SalesYTD`) entre el porcentaje de la comisión (`CommissionPCT`). El resultado se convierte en un tipo de datos `int` después de redondearlo al número entero más próximo.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT CAST(ROUND(SalesYTD/CommissionPCT, 0) AS int) AS Computed  
FROM Sales.SalesPerson   
WHERE CommissionPCT != 0;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
```  
Computed
------
379753754
346698349
257144242
176493899
281101272
0  
301872549
212623750
298948202
250784119
239246890
101664220
124511336
97688107
(14 row(s) affected)  
```  
  
### <a name="c-using-cast-to-concatenate"></a>C. Utilizar CAST para concatenar  
En el siguiente ejemplo se concatenan expresiones no binarias que no son de caracteres mediante `CAST`.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice  
FROM Production.Product  
WHERE ListPrice BETWEEN 350.00 AND 400.00;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ListPrice
------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09
(5 row(s) affected)  
```
  
### <a name="d-using-cast-to-produce-more-readable-text"></a>D. Utilizar CAST para obtener texto más legible  
En el siguiente ejemplo se utiliza `CAST` en la lista de selección para convertir la columna `Name` en una columna de tipo `char(10)`.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT DISTINCT CAST(p.Name AS char(10)) AS Name, s.UnitPrice  
FROM Sales.SalesOrderDetail AS s   
JOIN Production.Product AS p   
    ON s.ProductID = p.ProductID  
WHERE Name LIKE 'Long-Sleeve Logo Jersey, M';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name       UnitPrice
---------- -----------
Long-Sleev 31.2437
Long-Sleev 32.4935
Long-Sleev 49.99
(3 row(s) affected)  
```
  
### <a name="e-using-cast-with-the-like-clause"></a>E. Utilizar CAST con la cláusula LIKE  
En el siguiente ejemplo se convierte la columna `money` de tipo `SalesYTD` en una de tipo `int` y, a continuación, en una de tipo `char(20)` para que se pueda utilizar con la cláusula `LIKE`.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT p.FirstName, p.LastName, s.SalesYTD, s.BusinessEntityID  
FROM Person.Person AS p   
JOIN Sales.SalesPerson AS s   
    ON p.BusinessEntityID = s.BusinessEntityID  
WHERE CAST(CAST(s.SalesYTD AS int) AS char(20)) LIKE '2%';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
FirstName        LastName            SalesYTD         SalesPersonID
---------------- ------------------- ---------------- -------------
Tsvi             Reiter              2811012.7151      279
Syed             Abbas               219088.8836       288
Rachel           Valdez              2241204.0424      289
(3 row(s) affected)  
```
  
### <a name="f-using-convert-or-cast-with-typed-xml"></a>F. Utilizar CONVERT o CAST con XML con tipo  
Los siguientes son varios ejemplos que muestran el uso de CONVERT para convertir XML con tipo utilizando la [tipo de datos XML y columnas &#40; SQL Server &#41; ](../../relational-databases/xml/xml-data-type-and-columns-sql-server.md).
  
En este ejemplo se convierte una cadena con espacios en blanco, texto y marcado en XML con tipo y se quitan todos los espacios en blanco insignificantes (espacios en blanco de límite entre los nodos):
  
```sql
CONVERT(XML, '<root><child/></root>')  
```  
  
En este ejemplo se convierte una cadena similar con espacios en blanco, texto y marcado en XML con tipo y se conservan los espacios en blanco insignificantes (espacios en blanco de límite entre los nodos):
  
```sql
CONVERT(XML, '<root>          <child/>         </root>', 1)  
```  
  
En este ejemplo se convierte una cadena con espacios en blanco, texto y marcado en XML con tipo:
  
```sql
CAST('<Name><FName>Carol</FName><LName>Elliot</LName></Name>'  AS XML)  
```  
  
Para obtener más ejemplos, vea [crear instancias de datos de XML](../../relational-databases/xml/create-instances-of-xml-data.md).
  
### <a name="g-using-cast-and-convert-with-datetime-data"></a>G. Utilizar CAST y CONVERT con datos de fecha y hora  
En el ejemplo siguiente se muestra la fecha y la hora actuales, se utiliza `CAST` para cambiarlas a un tipo de datos de caracteres y, a continuación, se utiliza `CONVERT` para mostrar la fecha y la hora en el formato `ISO 8901`.
  
```sql
SELECT   
   GETDATE() AS UnconvertedDateTime,  
   CAST(GETDATE() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), GETDATE(), 126) AS UsingConvertTo_ISO8601  ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast              UsingConvertTo_ISO8601
----------------------- ---------------------- ------------------------------
2006-04-18 09:58:04.570 Apr 18 2006  9:58AM    2006-04-18T09:58:04.570
(1 row(s) affected)  
```
  
El siguiente ejemplo es lo opuesto, aproximadamente, del ejemplo anterior. En el ejemplo se muestra la fecha y la hora como datos de caracteres, se utiliza `CAST` para cambiar los datos de caracteres al tipo de datos `datetime` y, a continuación, se utiliza `CONVERT` para cambiar los datos de caracteres al tipo de datos `datetime`.
  
```sql
SELECT   
   '2006-04-25T15:50:59.997' AS UnconvertedText,  
   CAST('2006-04-25T15:50:59.997' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2006-04-25T15:50:59.997', 126) AS UsingConvertFrom_ISO8601 ;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2006-04-25T15:50:59.997 2006-04-25 15:50:59.997 2006-04-25 15:50:59.997
(1 row(s) affected)  
```
  
### <a name="h-using-convert-with-binary-and-character-data"></a>H. Usar CONVERT con datos binarios y de caracteres  
Los ejemplos siguientes muestran los resultados de convertir datos binarios y de caracteres utilizando estilos diferentes.
  
```sql
--Convert the binary value 0x4E616d65 to a character value.  
SELECT CONVERT(char(8), 0x4E616d65, 0) AS [Style 0, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, binary to character
----------------------------
Name  
(1 row(s) affected)  
```
 
En el ejemplo siguiente se muestra cómo estilo 1 puede forzar el resultado se trunque. El truncamiento se produce por incluidos los caracteres 0 x en el resultado.  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 1) AS [Style 1, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, binary to character
------------------------------
0x4E616D
(1 row(s) affected)  
```  
 
En el ejemplo siguiente se muestra que estilo 2 no trunca el resultado porque los caracteres 0 x no se incluyen en el resultado.  
```sql  
SELECT CONVERT(char(8), 0x4E616d65, 2) AS [Style 2, binary to character];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, binary to character
------------------------------
4E616D65
(1 row(s) affected)  
```
  
Convertir el valor del carácter 'Name' en un valor binario.  
```sql
SELECT CONVERT(binary(8), 'Name', 0) AS [Style 0, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 0, character to binary
----------------------------
0x4E616D6500000000
(1 row(s) affected)  
```
  
```sql
SELECT CONVERT(binary(4), '0x4E616D65', 1) AS [Style 1, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 1, character to binary
---------------------------- 
0x4E616D65
(1 row(s) affected)  
```  

```sql
SELECT CONVERT(binary(4), '4E616D65', 2) AS [Style 2, character to binary];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Style 2, character to binary  
----------------------------------  
0x4E616D65
(1 row(s) affected)  
```  
  
### <a name="i-converting-date-and-time-data-types"></a>I. Convierte tipos de datos de fecha y hora  
El siguiente ejemplo ilustra la conversión de los tipos de datos date, time y datetime.
  
```sql
DECLARE @d1 date, @t1 time, @dt1 datetime;  
SET @d1 = GETDATE();  
SET @t1 = GETDATE();  
SET @dt1 = GETDATE();  
SET @d1 = GETDATE();  
-- When converting date to datetime the minutes portion becomes zero.  
SELECT @d1 AS [date], CAST (@d1 AS datetime) AS [date as datetime];  
-- When converting time to datetime the date portion becomes zero   
-- which converts to January 1, 1900.  
SELECT @t1 AS [time], CAST (@t1 AS datetime) AS [time as datetime];  
-- When converting datetime to date or time non-applicable portion is dropped.  
SELECT @dt1 AS [datetime], CAST (@dt1 AS date) AS [datetime as date], 
   CAST (@dt1 AS time) AS [datetime as time];  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="j-using-cast-and-convert"></a>J. Utilizar CAST y CONVERT  
Este ejemplo recupera el nombre del producto para aquellos productos que tienen un `3` en el primer dígito del precio y convierte su `ListPrice` a **int**. Usa AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(ListPrice AS int) LIKE '3%';  
```  
  
Este ejemplo muestra la misma consulta utilizando CONVERT en lugar de CAST. Usa AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS ProductName, ListPrice  
FROM dbo.DimProduct  
WHERE CONVERT(int, ListPrice) LIKE '3%';  
```  
  
### <a name="k-using-cast-with-arithmetic-operators"></a>K. Utilizar CAST con operadores aritméticos  
En el ejemplo siguiente se calcula un cálculo de columna única dividiendo el precio unitario del producto (`UnitPrice`) por el porcentaje de descuento (`UnitPriceDiscountPct`). El resultado se convierte en un tipo de datos `int` después de redondearlo al número entero más próximo. Usa AdventureWorksDW.
  
```sql
SELECT ProductKey, UnitPrice,UnitPriceDiscountPct,  
       CAST(ROUND (UnitPrice*UnitPriceDiscountPct,0) AS int) AS DiscountPrice  
FROM dbo.FactResellerSales  
WHERE SalesOrderNumber = 'SO47355'   
      AND UnitPriceDiscountPct > .02;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ProductKey  UnitPrice  UnitPriceDiscountPct  DiscountPrice
----------  ---------  --------------------  -------------
323         430.6445   0.05                  22
213         18.5043    0.05                  1
456         37.4950    0.10                  4
456         37.4950    0.10                  4
216         18.5043    0.05                  1  
```  
  
### <a name="l-using-cast-to-concatenate"></a>L. Utilizar CAST para concatenar  
En el ejemplo siguiente se concatenan expresiones que no son caracteres con conversión. Usa AdventureWorksDW.
  
```sql
SELECT 'The list price is ' + CAST(ListPrice AS varchar(12)) AS ListPrice  
FROM dbo.DimProduct  
WHERE ListPrice BETWEEN 350.00 AND 400.00;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
ListPrice
------------------------
The list price is 357.06
The list price is 364.09
The list price is 364.09
The list price is 364.09
The list price is 364.09  
```  
  
### <a name="m-using-cast-to-produce-more-readable-text"></a>M. Utilizar CAST para obtener texto más legible  
En el ejemplo siguiente se utiliza CAST en la lista de selección para convertir el `Name` columna a una **char (10)** columna. Usa AdventureWorksDW.
  
```sql
SELECT DISTINCT CAST(EnglishProductName AS char(10)) AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE EnglishProductName LIKE 'Long-Sleeve Logo Jersey, M';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Name        UnitPrice
----------  ---------
Long-Sleev  31.2437
Long-Sleev  32.4935
Long-Sleev  49.99  
```  
  
### <a name="n-using-cast-with-the-like-clause"></a>N. Utilizar CAST con la cláusula LIKE  
El siguiente ejemplo se convierte el **dinero** columna `ListPrice` a una **int** tipo y, a continuación, en un **char(20)** escriba por lo que se puede utilizar con la cláusula LIKE. Usa AdventureWorksDW.
  
```sql
SELECT EnglishProductName AS Name, ListPrice  
FROM dbo.DimProduct  
WHERE CAST(CAST(ListPrice AS int) AS char(20)) LIKE '2%';  
```  
  
### <a name="o-using-cast-and-convert-with-datetime-data"></a>O. Utilizar CAST y CONVERT con datos de fecha y hora  
En el ejemplo siguiente se muestra la fecha y hora actuales, utiliza CAST para cambiar la fecha y hora actuales a un tipo de datos de caracteres, y, a continuación, utiliza CONVERT mostrar la fecha y hora en el formato ISO 8601. Usa AdventureWorksDW.
  
```sql
SELECT TOP(1)  
   SYSDATETIME() AS UnconvertedDateTime,  
   CAST(SYSDATETIME() AS nvarchar(30)) AS UsingCast,  
   CONVERT(nvarchar(30), SYSDATETIME(), 126) AS UsingConvertTo_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedDateTime     UsingCast                     UsingConvertTo_ISO8601  
---------------------   ---------------------------   ---------------------------  
07/20/2010 1:44:31 PM   2010-07-20 13:44:31.5879025   2010-07-20T13:44:31.5879025  
```  
  
El siguiente ejemplo es lo opuesto, aproximadamente, del ejemplo anterior. En el ejemplo se muestra una fecha y hora como datos de caracteres, utiliza CAST para cambiar los datos de caracteres para la **datetime** tipo de datos y, a continuación, utiliza CONVERT para cambiar los datos de caracteres para la **datetime** tipo de datos. Usa AdventureWorksDW.
  
```sql
SELECT TOP(1)   
   '2010-07-25T13:50:38.544' AS UnconvertedText,  
CAST('2010-07-25T13:50:38.544' AS datetime) AS UsingCast,  
   CONVERT(datetime, '2010-07-25T13:50:38.544', 126) AS UsingConvertFrom_ISO8601  
FROM dbo.DimCustomer;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
UnconvertedText         UsingCast               UsingConvertFrom_ISO8601
----------------------- ----------------------- ------------------------
2010-07-25T13:50:38.544 07/25/2010 1:50:38 PM   07/25/2010 1:50:38 PM  
```  
  
## <a name="see-also"></a>Vea también
[Conversiones de tipos de datos &#40; motor de base de datos &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
[Funciones del sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
[Escribir instrucciones Transact-SQL internacionales](../../relational-databases/collations/write-international-transact-sql-statements.md)
  

