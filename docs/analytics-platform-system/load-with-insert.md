---
title: Carga de datos con INSERT
description: Usar la instrucción INSERT de T-SQL para cargar datos en una tabla distribuida o replicada de almacenamiento de datos paralelo (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c28d15febb08855b914e4cd6ed04a97850ffe02c
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766866"
---
# <a name="load-data-with-insert-into-parallel-data-warehouse"></a>Carga de datos con INSERT en almacenamiento de datos paralelos

Puede usar la instrucción INSERT de TSQL para cargar datos en una SQL Server tabla distribuida o replicada de almacenamiento de datos paralelo (PDW). Para obtener más información acerca de INSERT, vea [Insert](../t-sql/statements/insert-transact-sql.md). En el caso de las tablas replicadas y todas las columnas que no son de distribución en una tabla distribuida, PDW usa SQL Server para convertir implícitamente los valores de datos especificados en la instrucción al tipo de datos de la columna de destino. Para obtener más información sobre SQL Server las reglas de conversión de datos, vea [conversión de tipos de datos para SQL](../t-sql/data-types/data-type-conversion-database-engine.md). Sin embargo, para las columnas de distribución, PDW solo admite un subconjunto de conversiones implícitas que SQL Server admite. Por lo tanto, cuando se utiliza la instrucción INSERT para cargar datos en una columna de distribución, los datos de origen deben especificarse en uno de los formatos definidos en las tablas siguientes.  
  
  
## <a name="insert-literals-into-binary-types"></a><a name="InsertingLiteralsBinary"></a>Insertar literales en tipos binarios  
En la tabla siguiente se definen los tipos literales aceptados, el formato y las reglas de conversión para insertar un valor literal en una columna de distribución de tipo **Binary** (*n*) o **varbinary**(*n*).  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal binario|0x*hexidecimal_string*<br /><br />Ejemplo: 0x12Ef|Los literales binarios deben ir precedidos de 0x.<br /><br />La longitud del origen de datos no puede superar el número de bytes especificado para el tipo de datos.<br /><br />Si la longitud del origen de datos es menor que el tamaño del tipo de datos **binarios** , los datos se rellenan a la derecha con ceros para alcanzar el tamaño del tipo de datos.|  
  
## <a name="insert-literals-into-date-and-time-types"></a><a name="InsertingLiteralsDateTime"></a>Insertar literales en tipos de fecha y hora  
Los literales de fecha y hora se representan mediante valores de caracteres en formatos específicos, incluidos entre comillas simples. En las tablas siguientes se definen los tipos literales, el formato y las reglas de conversión permitidos para insertar un literal de fecha u hora en una PDW de SQL Server columna de distribución de tipo **DateTime**, **smalldatetime**, **Date**, **Time**, **DateTimeOffset**o **datetime2**.  
  
### <a name="datetime-data-type"></a>datetime (tipo de datos)  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **DateTime**. Cualquier cadena vacía (' ') se convierte en el valor predeterminado ' 1900-01-01 12:00:00.000 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena en formato de **fecha y hora**|' AAAA-MM-DD HH: mm: SS [. nnn] '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123 '|Los dígitos fraccionarios que faltan se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35 ' se inserta como ' 2007-05-08 12:35:00.000 '.|  
|Literal de cadena en formato **smalldatetime**|' AAAA-MM-DD HH: mm '<br /><br />Ejemplo: ' 2007-05-08 12:35 '|Los segundos y los dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena en formato de **fecha**|' AAAA-MM-DD '<br /><br />Ejemplo: ' 2007-05-08 '|Los valores de hora (horas, minutos, segundos y fracciones) se establecen en 12:00:00.000 cuando se inserta el valor.|  
|Literal de cadena en formato **datetime2**|' AAAA-MM-DD HH: mm: SS. nnnnnnn '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567 '|Los datos de origen no pueden superar los tres dígitos fraccionarios. Por ejemplo, se insertará el literal ' 2007-05-08 12:35:29.123 ', pero el valor ' 2007-05-08 12:35:29.1234567 ' genera un error.|  
  
### <a name="smalldatetime-data-type"></a>smalldatetime (tipo de datos)  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **smalldatetime**. Cualquier cadena vacía (' ') se convierte en el valor predeterminado ' 1900-01-01 12:00 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena en formato **smalldatetime**|' AAAA-MM-DD HH: mm ' o ' AAAA-MM-DD HH: mm: 00 '<br /><br />Ejemplo: "2007-05-08 12:00" o "2007-05-08 12:00:00"|Los datos de origen deben tener valores para año, mes, fecha, hora y minuto. Los segundos son opcionales y, si están presentes, se deben establecer en el valor 00. Cualquier otro valor genera un error.|  
|Literal de cadena en formato de **fecha**|' AAAA-MM-DD '<br /><br />Ejemplo: ' 2007-05-08 '|Los valores de hora (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor.|  
  
### <a name="date-data-type"></a>date (tipo de datos)  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **Date**. Cualquier cadena vacía (' ') se convierte en el valor predeterminado ' 1900-01-01 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena en formato de **fecha**|' AAAA-MM-DD '<br /><br />Ejemplo: ' 2007-05-08 '|Este es el único formato aceptado.|  
  
### <a name="time-data-type"></a>time (tipo de datos)  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **Time**. Cualquier cadena vacía (' ') se convierte en el valor predeterminado ' 00:00:00.0000 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena en formato de **hora**|' HH: mm: SS. nnnnnnn '<br /><br />Ejemplo: "12:35:29.1234567"|Si el origen de datos tiene una precisión menor o igual (número de dígitos fraccionarios) que la precisión del tipo de datos **Time** , los datos se rellenan a la derecha con ceros. Por ejemplo, un valor literal "12:35:29.123" se inserta como "12:35:29.1230000".<br /><br />Un valor que tiene una precisión mayor que el tipo de datos de destino se rechaza.|  
  
### <a name="datetimeoffset-data-type"></a>datetimeoffset (tipo de datos)  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **DateTimeOffset** (*n*). El formato predeterminado es "AAAA-MM-DD HH: mm: SS. nnnnnnn {+ |-} HH: mm". Una cadena vacía (' ') se convierte en el valor predeterminado ' 1900-01-01 12:00:00.0000000 + 00:00 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error. El número de dígitos fraccionarios depende de la definición de la columna. Por ejemplo, una columna definida como **DateTimeOffset** (2) tendrá dos dígitos fraccionarios.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena en formato de **fecha y hora**|' AAAA-MM-DD HH: mm: SS [. nnn] '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123 '|Los dígitos fraccionarios que faltan y los valores de desplazamiento se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35:29.123 ' se inserta como ' 2007-05-08 12:35:29.1230000 + 00:00 '.|  
|Literal de cadena en formato **smalldatetime**|' AAAA-MM-DD HH: mm '<br /><br />Ejemplo: ' 2007-05-08 12:35 '|Segundos, los dígitos fraccionarios restantes y los valores de desplazamiento se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena en formato de **fecha**|' AAAA-MM-DD '<br /><br />Ejemplo: ' 2007-05-08 '|Los valores de hora (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 ' se inserta como ' 2007-05-08 00:00:00.0000000 + 00:00 '.|  
|Literal de cadena en formato **datetime2**|' AAAA-MM-DD HH: mm: SS. nnnnnnn '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567 '|Los datos de origen no pueden superar el número especificado de fracciones de segundo en la columna DateTimeOffset. Si el origen de datos tiene un número menor o igual de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es DateTimeOffset (5), se inserta el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' como ' 12:35:29.12300 + 12:15 '.|  
|Literal de cadena en formato **DateTimeOffset**|' AAAA-MM-DD HH: mm: SS. nnnnnnn {+&#124;-} HH: mm '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567 + 12:15 '|Los datos de origen no pueden superar el número especificado de fracciones de segundo en la columna DateTimeOffset. Si el origen de datos tiene un número menor o igual de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es DateTimeOffset (5), se inserta el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' como ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>datetime2 (tipo de datos)  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **datetime2** (*n*). El formato predeterminado es ' AAAA-MM-DD HH: mm: SS. nnnnnnn '. Una cadena vacía (' ') se convierte en el valor predeterminado ' 1900-01-01 12:00:00 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error. El número de dígitos fraccionarios depende de la definición de la columna. Por ejemplo, una columna definida como **datetime2** (2) tendrá dos dígitos fraccionarios.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena en formato de **fecha y hora**|' AAAA-MM-DD HH: mm: SS [. nnn] '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123 '|Las fracciones de segundo son opcionales y se establecen en 0 cuando se inserta el valor.<br /><br />Un valor que tiene más dígitos fraccionarios que el tipo de datos de destino se rechaza.|  
|Literal de cadena en formato **smalldatetime**|' AAAA-MM-DD HH: mm '<br /><br />Ejemplo: ' 2007-05-08 12 '|Los segundos opcionales y los dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena en formato de **fecha**|' AAAA-MM-DD '<br /><br />Ejemplo: ' 2007-05-08 '|Los valores de hora (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 ' se inserta como ' 2007-05-08 12:00:00.0000000 '.|  
|Literal de cadena en formato **datetime2**|' AAAA-MM-DD HH: mm: SS: nnnnnnn '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567 '|Si el origen de datos contiene componentes de datos y de hora que son menores o iguales que el valor especificado en **datetime2**(*n*), se insertan los datos; en caso contrario, se genera un error.|  
  
## <a name="insert-literals-into-numeric-types"></a><a name="InsertLiteralsNumeric"></a>Insertar literales en tipos numéricos  
En las tablas siguientes se definen los formatos aceptados y las reglas de conversión para insertar un valor literal en una columna de distribución de PDW de SQL Server que utiliza un tipo numérico.  
  
### <a name="bit-data-type"></a>bit, tipo de datos  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **bit**. Una cadena vacía (' ') o una cadena que solo contenga espacios en blanco (' ') se convierten en 0.  
  
|Tipo de literal|format|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena en formato de **entero**|'nnnnnnnnnn'<br /><br />Ejemplo: ' 1 ' o ' 321 '|Un valor entero con formato de literal de cadena no puede contener un valor negativo. Por ejemplo, el valor "-123" genera un error.<br /><br />Un valor mayor que 1 se convierte en 1. Por ejemplo, el valor "123" se convierte en 1.|  
|Literal de cadena|' TRUE ' o ' FALSE '<br /><br />Ejemplo: "true"|El valor "TRUE" se convierte en 1; el valor "FALSE" se convierte en 0.|  
|Literal entero|nnnnnnnn<br /><br />Ejemplo: 1 o 321|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, los valores 123 y-123 se convierten en 1.|  
|Literal decimal|nnnnn. nnnn<br /><br />Ejemplo: 1234,5678|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, los valores 123,45 y-123,45 se convierten en 1.|  
  
### <a name="decimal-data-type"></a>tipo de datos decimal  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **decimal** (*p, s*). Las reglas de conversión de datos son las mismas que para SQL Server. Para obtener más información, vea [conversión de tipos de datos](../t-sql/data-types/data-type-conversion-database-engine.md) en MSDN.  
  
|Tipo de literal|Formato|  
|----------------|----------|  
|Literal de cadena en formato de **entero**|nnnnnnnnnnnn<br /><br />Ejemplo: ' 321312313123 '|  
|Literal de cadena en formato **decimal**|' nnnnnn. nnnnn '<br /><br />Ejemplo: ' 123344,34455 '|  
|Literal entero|nnnnnnnnnnnn<br /><br />Ejemplo: 321312313123|  
|Literal decimal|nnnnnn. nnnnn<br /><br />Ejemplo: ' 123344,34455 '|  
  
### <a name="float-and-real-data-types"></a>tipos de datos float y real  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **float** o **real**. Las reglas de conversión de datos son las mismas que para SQL Server. Para obtener más información, vea [conversión de tipos de datos](../t-sql/data-types/data-type-conversion-database-engine.md) en MSDN.  
  
|Tipo de literal|Formato|  
|----------------|----------|  
|Literal de cadena en formato de **entero**|nnnnnnnnnnnn<br /><br />Ejemplo: ' 321312313123 '|  
|Literal de cadena en formato **decimal**|' nnnnnn. nnnnn '<br /><br />Ejemplo: ' 123344,34455 '|  
|Literal de cadena en formato de **punto flotante**|' n. nnnnnE + NN '<br /><br />Ejemplo: "3.12323 E + 14"|  
|Literal entero|nnnnnnnnnnnn<br /><br />Ejemplo: 321312313123|  
|Literal decimal|nnnnnn. nnnnn<br /><br />Ejemplo: 123344,34455|  
|Literal de punto flotante|n. nnnnnE + NN<br /><br />Ejemplo: 3.12323 E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>tipos de datos int, bigint, tinyint, smallint  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **int**, **BIGINT**, **tinyint**o **smallint**. El origen de datos no puede superar el intervalo permitido para el tipo de datos especificado. Por ejemplo, el intervalo de **tinyint** es 0 a 255 y el intervalo para **int** es-2.147.483.648 a 2.147.483.647.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|------------|------|----------------|
|Literal de cadena en formato de **entero**|'nnnnnnnnnnnnnn'<br /><br />Ejemplo: ' 321312313123 '| None |  
|Literal entero|nnnnnnnnnnnnnn<br /><br />Ejemplo: 321312313123| None|  
|Literal decimal|nnnnnn. nnnnn<br /><br />Ejemplo: 123344,34455|Los valores a la derecha del separador decimal se truncan.|  
  
### <a name="money-and-smallmoney-data-types"></a>tipos de datos Money y smallmoney  
Los valores literales de moneda se representan como números con un separador decimal y un símbolo de divisa opcionales como prefijo. El origen de datos no puede superar el intervalo permitido para el tipo de datos especificado. Por ejemplo, el intervalo para **smallmoney** es-214.748,3648 a 214.748,3647 y el intervalo para **money** es-922.337.203.685.477,5808 a 922.337.203.685.477,5807. En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **Money** o **smallmoney**.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena en formato de **entero**|nnnnnnnn<br /><br />Ejemplo: ' 123433 '|Los dígitos que faltan después del separador decimal se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 12345 ' se inserta como 12345,0000.|  
|Literal de cadena en formato **decimal**|' nnnnnn. nnnnn '<br /><br />Ejemplo: ' 123344,34455 '|Si el número de dígitos después del separador decimal es superior a 4, el valor se redondea al valor más próximo. Por ejemplo, el valor "123344,34455" se inserta como 123344,3446.|  
|Literal de cadena en formato **Money**|' $nnnnnn. nnnn '<br /><br />Ejemplo: ' $123456,7890 '|El símbolo de divisa opcional no se inserta con el valor.<br /><br />Si el número de dígitos después del separador decimal es superior a 4, el valor se redondea al valor más próximo.|  
|Literal entero|nnnnnnnn<br /><br />Ejemplo: 123433|Los dígitos que faltan después del separador decimal se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal 12345 se inserta como 12345,0000.|  
|Literal decimal|nnnnnn. nnnnn<br /><br />Ejemplo: 123344,34455|Si el número de dígitos después del separador decimal es superior a 4, el valor se redondea al valor más próximo. Por ejemplo, el valor 123344,34455 se inserta como 123344,3446.|  
|Literal de moneda|$nnnnnn. nnnn<br /><br />Ejemplo: $123456,7890|El símbolo de divisa opcional no se inserta con el valor.<br /><br />Si el número de dígitos después del separador decimal es superior a 4, el valor se redondea al valor más próximo.|  
  
## <a name="inserting-literals-into-string-types"></a><a name="InsertLiteralsString"></a>Insertar literales en tipos de cadena  
En las tablas siguientes se definen los formatos aceptados y las reglas de conversión para insertar un valor literal en una PDW de SQL Server columna que utiliza un tipo de cadena.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>tipos de datos char, VARCHAR, nchar y nvarchar  
En la tabla siguiente se definen las reglas y los formatos aceptados para insertar valores literales en una columna de distribución de tipo **Char**, **VARCHAR**, **nchar** y **nvarchar**. La longitud del origen de datos no puede superar el tamaño especificado para el tipo de datos. Si la longitud del origen de datos es menor que el tamaño del tipo de datos **Char** o **nchar** , los datos se rellenan a la derecha con espacios en blanco para alcanzar el tamaño del tipo de datos.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena|Formato: ' cadena de caracteres '<br /><br />Ejemplo: ' ABC '| None|  
|Literal de cadena Unicode|Formato: N'character cadena '<br /><br />Ejemplo: N'abc '|  None |  
|Literal entero|Formato: nnnnnnnnnnn<br /><br />Ejemplo: 321312313123| None |  
|Literal decimal|Formato: nnnnnn. nnnnnnn<br /><br />Ejemplo: 12344,34455| None |  
|Literal de moneda|Formato: $nnnnnn. nnnnn<br /><br />Ejemplo: $123456,99|El símbolo de moneda no se inserta con el valor. Para insertar el símbolo de moneda, inserte el valor como un literal de cadena. Esto coincidirá con el formato de la herramienta **dwloader** , que trata todos los literales como un literal de cadena.<br /><br />No se permiten comas.<br /><br />Si el número de dígitos después del separador decimal es superior a 2, el valor se redondea al valor más próximo. Por ejemplo, el valor 123,946789 se inserta como 123,95.<br /><br />Solo se permite el estilo predeterminado 0 (sin comas y 2 dígitos después del separador decimal) cuando se usa la función CONVERT para insertar literales monetarios.|  

  
## <a name="see-also"></a>Consulte también  
 
[Datos distribuidos](/azure/synapse-analytics/sql-data-warehouse/massively-parallel-processing-mpp-architecture)  
[INSERT](../t-sql/statements/insert-transact-sql.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Metadata query examples](metadata-query-examples.md) 
-->