---
title: Carga de datos con INSERT - almacenamiento de datos paralelos | Microsoft Docs
description: Con la instrucción INSERT de T-SQL para cargar datos en un almacén de datos paralelos (PDW) distribuidas o tabla replicada.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b13daf2d32cc41d63deea6c612dde247d541e4d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63128565"
---
# <a name="load-data-with-insert-into-parallel-data-warehouse"></a>Cargar datos con INSERT en el almacenamiento de datos paralelos

Puede usar la instrucción INSERT de tsql para cargar datos en un servidor SQL Server distribuidos de almacenamiento de datos paralelos (PDW) o tabla replicada. Para obtener más información acerca de la INSERCIÓN, vea [insertar](../t-sql/statements/insert-transact-sql.md). Para las tablas replicadas y todas las columnas de distribución que no son de una tabla distribuida, PDW usa SQL Server para convertir implícitamente los valores de datos especificados en la instrucción para el tipo de datos de la columna de destino. Para obtener más información acerca de las reglas de conversión de datos de SQL Server, vea [datos de conversión de tipos para SQL](../t-sql/data-types/data-type-conversion-database-engine.md). Sin embargo, para las columnas de distribución, PDW admite solo un subconjunto de las conversiones implícitas que admite SQL Server. Por lo tanto, cuando utiliza la instrucción INSERT para cargar datos en una columna de distribución, los datos de origen deben especificarse en uno de los formatos definidos en las tablas siguientes.  
  
  
## <a name="InsertingLiteralsBinary"></a>Insertar literales en tipos binarios  
La siguiente tabla define los tipos literales aceptados, formato y las reglas de conversión para insertar un valor literal en una columna de distribución de tipo **binario** (*n*) o **varbinary** (*n*).  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal binario|0x*hexidecimal_string*<br /><br />Ejemplo: 0x12Ef|Literales binarios deben tener el prefijo 0 x.<br /><br />La longitud del origen de datos no puede superar el número de bytes especificado para el tipo de datos.<br /><br />Si la longitud del origen de datos es menor que el tamaño de la **binario** tipo de datos, los datos se rellenan a la derecha con ceros para alcanzar el tamaño del tipo de datos.|  
  
## <a name="InsertingLiteralsDateTime"></a>Insertar literales en tipos de fecha y hora  
Literales de fecha y hora se representan mediante valores de caracteres en formatos específicos, entrecomillados comillas simples. Las siguientes tablas definen los tipos literales permitidos, formato y las reglas de conversión para insertar una fecha u hora literal en una columna de distribución de PDW de SQL Server de tipo **datetime**, **smalldatetime**, **fecha**, **tiempo**, **datetimeoffset**, o **datetime2**.  
  
### <a name="datetime-data-type"></a>tipo de datos de fecha y hora  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **datetime**. Cualquier cadena vacía (") se convierte en el valor predeterminado ' 12:00:00.000 1900-01-01'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **datetime** formato|'Aaaa-MM-DD hh: mm: [.nnn]'<br /><br />Ejemplo: '2007-05-08 12:35:29.123'|Los dígitos fraccionarios que faltan se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35 ' se inserta como ' 2007-05-08 12:35:00.000'.|  
|Literal de cadena de **smalldatetime** formato|"Aaaa-MM-DD hh: mm"<br /><br />Ejemplo: '2007-05-08 12:35'|Segundos y dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'AAAA-MM-DD'<br /><br />Ejemplo: '2007-05-08'|Cuando se inserta el valor, se establecen los valores de tiempo (horas, minutos, segundos y fracciones) en 12:00:00.000.|  
|Literal de cadena de **datetime2** formato|'Aaaa-MM-DD nnnnnnn'<br /><br />Ejemplo: '2007-05-08 12:35:29.1234567'|Los datos de origen no pueden superar los tres dígitos fraccionarios. Por ejemplo, el literal ' 2007-05-08 12:35:29.123' se van a insertar, pero el valor ' 2007-05-08 12:35:29.1234567' genera un error.|  
  
### <a name="smalldatetime-data-type"></a>tipo de datos smalldatetime  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **smalldatetime**. Cualquier cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **smalldatetime** formato|'Aaaa-MM-DD hh: mm' o 'Aaaa-MM-DD hh:mm:00'<br /><br />Ejemplo: ' 2007-05-08 12:00 ' o ' 2007-05-08:00-12:00 '|Los datos de origen deben tener los valores de año, mes, fecha, hora y minuto. Segundos son opcionales y, si está presente, se deben establecer en el valor 00. Cualquier otro valor genera un error.|  
|Literal de cadena de **fecha** formato|'AAAA-MM-DD'<br /><br />Ejemplo: '2007-05-08'|Los valores de tiempo (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor.|  
  
### <a name="date-data-type"></a>Tipo de datos Date  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **fecha**. Cualquier cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **fecha** formato|'AAAA-MM-DD'<br /><br />Ejemplo: '2007-05-08'|Este es el único formato aceptado.|  
  
### <a name="time-data-type"></a>tipo de datos Time  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **tiempo**. Cualquier cadena vacía (") se convierte en el valor predeterminado '00:00:00.0000'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **tiempo** formato|'hh:mm:ss.nnnnnnn'<br /><br />Ejemplo: '12:35:29.1234567'|Si el origen de datos tiene una precisión menor o igual (número de dígitos fraccionarios) que la precisión de la **tiempo** tipo de datos, los datos se rellenan a la derecha con ceros. Por ejemplo, se inserta un valor literal '12:35:29.123' como '12:35:29.1230000'.<br /><br />Un valor que tiene una precisión mayor que el tipo de datos de destino se rechaza.|  
  
### <a name="datetimeoffset-data-type"></a>tipo de datos DateTimeOffset  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **datetimeoffset** (*n*). El formato predeterminado es ' aaaa-MM-DD nnnnnnn {+ |-} hh: mm '. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00:00.0000000 + 00:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error. El número de dígitos fraccionarios depende de la definición de columna. Por ejemplo, una columna definida como **datetimeoffset** (2) tendrán dos dígitos fraccionarios.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **datetime** formato|'Aaaa-MM-DD hh: mm: [.nnn]'<br /><br />Ejemplo: '2007-05-08 12:35:29.123'|Los dígitos fraccionarios que faltan y valores de desplazamiento se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35:29.123' se inserta como ' 2007-05-08 12:35:29.1230000 + 00:00 '.|  
|Literal de cadena de **smalldatetime** formato|"Aaaa-MM-DD hh: mm"<br /><br />Ejemplo: '2007-05-08 12:35'|Segundos, los dígitos fraccionarios restantes y valores de desplazamiento se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'AAAA-MM-DD'<br /><br />Ejemplo: '2007-05-08'|Los valores de tiempo (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08' se inserta como ' 2007-05-08 00:00:00.0000000 + 00:00 '.|  
|Literal de cadena de **datetime2** formato|'Aaaa-MM-DD nnnnnnn'<br /><br />Ejemplo: '2007-05-08 12:35:29.1234567'|Los datos de origen no pueden superar el número especificado de segundos fraccionarios en la columna de datetimeoffset. Si el origen de datos tiene un número igual o menor de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es datetimeoffset (5), el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' se inserta como ' 12:35:29.12300 + 12:15 '.|  
|Literal de cadena de **datetimeoffset** formato|' Aaaa-MM-DD nnnnnnn {+&#124;-} hh: mm '<br /><br />Ejemplo: '2007-05-08 12:35:29.1234567 +12:15'|Los datos de origen no pueden superar el número especificado de segundos fraccionarios en la columna de datetimeoffset. Si el origen de datos tiene un número igual o menor de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es datetimeoffset (5), el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' se inserta como ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>tipo de datos datetime2  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **datetime2** (*n*). El formato predeterminado es 'Aaaa-MM-DD nnnnnnn'. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error. El número de dígitos fraccionarios depende de la definición de columna. Por ejemplo, una columna definida como **datetime2** (2) tendrán dos dígitos fraccionarios.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **datetime** formato|'Aaaa-MM-DD hh: mm: [.nnn]'<br /><br />Ejemplo: '2007-05-08 12:35:29.123'|Fracciones de segundo son opcionales y se establecen en 0 cuando se inserta el valor.<br /><br />Un valor que tiene más dígitos fraccionarios que el tipo de datos de destino se rechaza.|  
|Literal de cadena de **smalldatetime** formato|"Aaaa-MM-DD hh: mm"<br /><br />Ejemplo: '2007-05-08 12'|Segundos opcionales y dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'AAAA-MM-DD'<br /><br />Ejemplo: '2007-05-08'|Los valores de tiempo (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08' se inserta como ' 2007-05-08 12:00:00.0000000'.|  
|Literal de cadena de **datetime2** formato|'Aaaa-MM-DD hh:mm:ss:nnnnnnn'<br /><br />Ejemplo: '2007-05-08 12:35:29.1234567'|Si el origen de datos contiene datos y la hora de los componentes que son menores o iguales al valor especificado en **datetime2**(*n*), se insertan los datos; en caso contrario, se genera un error.|  
  
## <a name="InsertLiteralsNumeric"></a>Insertar literales en tipos numéricos  
Las tablas siguientes definen los formatos aceptados y reglas de conversión para insertar un valor literal en una columna de distribución de PDW de SQL Server que utiliza un tipo numérico.  
  
### <a name="bit-data-type"></a>bit, tipo de datos  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **bits**. Una cadena vacía (") o una cadena que contiene solo espacios en blanco (' ') se convierte en 0.  
  
|Tipo de literal|format|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **entero** formato|'nnnnnnnnnn'<br /><br />Ejemplo: '1' o '321'|Un valor entero con formato de un literal de cadena no puede contener un valor negativo. Por ejemplo, el valor '-' 123 genera un error.<br /><br />Un valor mayor que 1 se convierte en 1. Por ejemplo, el valor '123' se convierte en 1.|  
|Literal de cadena|'TRUE' o 'FALSE'<br /><br />Ejemplo: 'true'|El valor 'TRUE' se convierte en 1; el valor 'FALSE' se convierte en 0.|  
|Literal entero|nnnnnnnn<br /><br />Ejemplo: 1 o 321|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, los valores 123 y -123 se convierten en 1.|  
|Literal decimal|nnnnn.nnnn<br /><br />Ejemplo: 1234.5678|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, los valores 123,45 y sería -123,45 se convierten en 1.|  
  
### <a name="decimal-data-type"></a>tipo de datos decimal  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **decimal** (*p, s*). Las reglas de conversión de datos son los mismos que para SQL Server. Para obtener más información, consulte [conversión de tipos de datos](../t-sql/data-types/data-type-conversion-database-engine.md) en MSDN.  
  
|Tipo de literal|Formato|  
|----------------|----------|  
|Literal de cadena de **entero** formato|'nnnnnnnnnnnn'<br /><br />Ejemplo: '321312313123'|  
|Literal de cadena de **decimal** formato|'nnnnnn.nnnnn'<br /><br />Ejemplo: '123344.34455'|  
|Literal entero|nnnnnnnnnnnn<br /><br />Ejemplo: 321312313123|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Ejemplo: '123344.34455'|  
  
### <a name="float-and-real-data-types"></a>tipos de datos float y real  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **float** o **real**. Reglas de conversión de datos son los mismos que para SQL Server. Para obtener más información, consulte [conversión de tipos de datos](../t-sql/data-types/data-type-conversion-database-engine.md) en MSDN.  
  
|Tipo de literal|Formato|  
|----------------|----------|  
|Literal de cadena de **entero** formato|'nnnnnnnnnnnn'<br /><br />Ejemplo: '321312313123'|  
|Literal de cadena de **decimal** formato|'nnnnnn.nnnnn'<br /><br />Ejemplo: '123344.34455'|  
|Literal de cadena de **punto flotante** formato|'n.nnnnnE+nn'<br /><br />Ejemplo: '3.12323E+14'|  
|Literal entero|nnnnnnnnnnnn<br /><br />Ejemplo: 321312313123|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Ejemplo: 123344.34455|  
|Literal de punto flotante|n.nnnnnE+nn<br /><br />Ejemplo: 3.12323E+14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int, bigint, tinyint, smallint los tipos de datos  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **int**, **bigint**, **tinyint**, o **smallint**. El origen de datos no puede superar el intervalo permitido para el tipo de datos determinado. Por ejemplo, el intervalo para **tinyint** es de 0 a 255 y el intervalo de **int** es de -2.147.483.648 a 2.147.483.647.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|------------|------|----------------|
|Literal de cadena de **entero** formato|'nnnnnnnnnnnnnn'<br /><br />Ejemplo: '321312313123'| None |  
|Literal entero|nnnnnnnnnnnnnn<br /><br />Ejemplo: 321312313123| None|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Ejemplo: 123344.34455|Se truncan los valores a la derecha del separador decimal.|  
  
### <a name="money-and-smallmoney-data-types"></a>tipos de datos Money y smallmoney  
Valores literales dinero se representan como números con un separador decimal opcional y el símbolo de moneda como prefijo. El origen de datos no puede superar el intervalo permitido para el tipo de datos determinado. Por ejemplo, el intervalo para **smallmoney** es-214.748,3648 y 214.748,3647 y el intervalo para **dinero** es -922.337.203.685.477,5808 y 922.337.203.685.477,5807. La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **dinero** o **smallmoney**.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **entero** formato|'nnnnnnnn'<br /><br />Ejemplo: '123433'|Falta de dígitos después del separador decimal se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal "12345" se inserta como 12345.0000.|  
|Literal de cadena de **decimal** formato|'nnnnnn.nnnnn'<br /><br />Ejemplo: '123344.34455'|Si el número de dígitos después del punto decimal supera los 4, el valor se redondea al valor más cercano. Por ejemplo, se inserta el valor '123344.34455' como 123344.3446.|  
|Literal de cadena de **dinero** formato|'$nnnnnn.nnnn'<br /><br />Ejemplo: "$123456.7890'|El símbolo de moneda opcionales no se inserta con el valor.<br /><br />Si el número de dígitos después del punto decimal supera los 4, el valor se redondea al valor más cercano.|  
|Literal entero|nnnnnnnn<br /><br />Ejemplo: 123433|Falta de dígitos después del separador decimal se establecen en 0 cuando se inserta el valor. Por ejemplo, se inserta el literal 12345 como 12345.0000.|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Ejemplo: 123344.34455|Si el número de dígitos después del punto decimal supera los 4, el valor se redondea al valor más cercano. Por ejemplo, se inserta el valor 123344.34455 como 123344.3446.|  
|Literal Money|$nnnnnn.nnnn<br /><br />Ejemplo: $123456.7890|El símbolo de moneda opcionales no se inserta con el valor.<br /><br />Si el número de dígitos después del punto decimal supera los 4, el valor se redondea al valor más cercano.|  
  
## <a name="InsertLiteralsString"></a>Insertar literales en tipos de cadena  
Las tablas siguientes definen los formatos aceptados y reglas de conversión para insertar un valor literal en una columna de PDW de SQL Server que utiliza un tipo de cadena.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>tipos de datos char, varchar, nchar y nvarchar  
La siguiente tabla define los formatos aceptados y reglas para insertar valores literales en una columna de distribución de tipo **char**, **varchar**, **nchar** y **nvarchar**. La longitud del origen de datos no puede superar el tamaño especificado para el tipo de datos. Si la longitud del origen de datos es menor que el tamaño de la **char** o **nchar** tipo de datos, los datos se rellenan a la derecha con espacios en blanco para alcanzar el tamaño del tipo de datos.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena|Formato: 'cadena de caracteres'<br /><br />Ejemplo: 'abc'| None|  
|Literal de cadena Unicode|Formato: Cadena N'character'<br /><br />Ejemplo: Abc '|  None |  
|Literal entero|Formato: nnnnnnnnnnn<br /><br />Ejemplo: 321312313123| None |  
|Literal decimal|Formato: nnnnnn.nnnnnnn<br /><br />Ejemplo: 12344.34455| None |  
|Literal Money|Formato: $nnnnnn.nnnnn<br /><br />Ejemplo: $123456.99|No se inserta el símbolo de moneda con el valor. Para insertar el símbolo de moneda, insertar ese valor como un literal de cadena. Esto coincidirá con el formato de la **dwloader** herramienta, que trata todos los literales como un literal de cadena.<br /><br />No se permiten las comas.<br /><br />Si el número de dígitos después del punto decimal supera los 2, el valor se redondea al valor más cercano. Por ejemplo, se inserta el valor 123.946789 como 123.95.<br /><br />Se permite solo el estilo predeterminado de 0 (sin separadores de millar y 2 dígitos después del separador decimal) cuando se usa la función CONVERT para insertar literales de dinero.|  

  
## <a name="see-also"></a>Vea también  
 
[Datos distribuidos](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-distributed-data/)  
[INSERT](../t-sql/statements/insert-transact-sql.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Metadata query examples](metadata-query-examples.md) 
-->
