---
title: Carga los datos con INSERT - almacenamiento de datos paralelos | Documentos de Microsoft
description: Usar la instrucción INSERT de T-SQL para cargar datos en un almacén de datos paralelos (PDW) distribuidas o tabla replicada.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: a505a099e239049aab40c616c9e98e44e328537c
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="load-data-with-insert-into-parallel-data-warehouse"></a>Cargar datos con INSERT en almacenamiento de datos paralelos

Puede usar la instrucción INSERT de tsql para cargar datos en un servidor SQL Server (PDW) de almacenamiento de datos paralelos distribuidas o tabla replicada. Para obtener más información acerca de la INSERCIÓN, vea [insertar](../t-sql/statements/insert-transact-sql.md). Para las tablas replicadas y todas las columnas de distribución no en una tabla distribuida, PDW usa SQL Server para convertir implícitamente los valores de datos especificados en la instrucción para el tipo de datos de la columna de destino. Para obtener más información acerca de las reglas de conversión de datos de SQL Server, vea [datos de conversión de tipos para SQL](http://msdn.microsoft.com/library/ms191530&#40;v=sql11&#40;.aspx). Sin embargo, para las columnas de distribución, PDW sólo admite un subconjunto de las conversiones implícitas que admite SQL Server. Por lo tanto, cuando utiliza la instrucción INSERT para cargar datos en una columna de distribución, los datos de origen deben especificarse en uno de los formatos definidos en las tablas siguientes.  
  
  
## <a name="InsertingLiteralsBinary"></a>Insertar literales en tipos binarios  
La siguiente tabla definen los tipos literales aceptados, formato y reglas de conversión para insertar un valor literal en una columna de distribución de tipo **binario** (*n*) o **varbinary** (*n*).  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal binario|0x*hexidecimal_string*<br /><br />Ejemplo: 0x12Ef|Literales binarios deben ir precedidos por 0 x.<br /><br />La longitud del origen de datos no puede superar el número de bytes especificado para el tipo de datos.<br /><br />Si la longitud del origen de datos es menor que el tamaño de la **binario** tipo de datos, los datos se rellenan a la derecha con ceros para alcanzar el tamaño del tipo de datos.|  
  
## <a name="InsertingLiteralsDateTime"></a>Insertar literales en tipos de fecha y hora  
Literales de fecha y hora se representan mediante el uso de valores de caracteres en formatos específicos, entre comillas simples. En las tablas siguientes se definen los tipos permitidos de literales, formato y reglas de conversión para insertar una fecha u hora literal en una columna de distribución de SQL Server PDW de tipo **datetime**, **smalldatetime**, **fecha**, **tiempo**, **datetimeoffset**, o **datetime2**.  
  
### <a name="datetime-data-type"></a>tipo de datos de fecha y hora  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **datetime**. Cualquier cadena vacía (") se convierte en el valor predeterminado ' 12:00:00.000 1900-01-01'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **datetime** formato|'Aaaa-MM-DD hh [.nnn]'<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123'|Los dígitos fraccionarios que faltan se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35 ' se inserta como ' 2007-05-08 12:35:00.000'.|  
|Literal de cadena de **smalldatetime** formato|'Aaaa-MM-DD hh'<br /><br />Ejemplo: ' 2007-05-08 12:35 '|Segundos y los dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'AAAA-MM-DD'<br /><br />Ejemplo: ' 2007-05-08'|Valores de tiempo (hora, minutos, segundos y fracciones) se establecen en 12:00:00.000 cuando se inserta el valor.|  
|Literal de cadena de **datetime2** formato|'Aaaa-MM-DD. nnnnnnn'<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567'|Los datos de origen no pueden superar los tres dígitos fraccionarios. Por ejemplo, el literal ' 2007-05-08 12:35:29.123' se van a insertar, pero el valor ' 2007-05-08 12:35:29.1234567' genera un error.|  
  
### <a name="smalldatetime-data-type"></a>tipo de datos smalldatetime  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **smalldatetime**. Cualquier cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **smalldatetime** formato|'Aaaa-MM-DD hh: mm' o 'Aaaa-MM-DD hh:mm:00'<br /><br />Ejemplo: ' 2007-05-08 12:00 ' o ' 2007-05-08 12:00:00 '|Los datos de origen deben tener valores de año, mes, fecha, hora y minuto. Segundos son opcionales y, si está presente, deben establecerse en el valor 00. Cualquier otro valor genera un error.|  
|Literal de cadena de **fecha** formato|'AAAA-MM-DD'<br /><br />Ejemplo: ' 2007-05-08'|Valores de tiempo (hora, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor.|  
  
### <a name="date-data-type"></a>tipo de datos Date  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **fecha**. Cualquier cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **fecha** formato|'AAAA-MM-DD'<br /><br />Ejemplo: ' 2007-05-08'|Este es el único formato aceptado.|  
  
### <a name="time-data-type"></a>Tipo de datos de hora  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **tiempo**. Cualquier cadena vacía (") se convierte en el valor predeterminado '00:00:00.0000'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **tiempo** formato|'. nnnnnnn'<br /><br />Ejemplo: '12:35:29.1234567'|Si el origen de datos tiene una precisión menor o igual (número de dígitos fraccionarios) que la precisión de la **tiempo** tipo de datos, los datos se rellenan a la derecha con ceros. Por ejemplo, se inserta un valor literal '12:35:29.123' como '12:35:29.1230000'.<br /><br />Un valor que tiene una precisión mayor que el tipo de datos de destino se rechaza.|  
  
### <a name="datetimeoffset-data-type"></a>tipo de datos DateTimeOffset  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **datetimeoffset** (*n*). El formato predeterminado es '. nnnnnnn aaaa-MM-DD {+ |-} hh: mm '. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00:00.0000000 + 00:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error. El número de dígitos fraccionarios depende de la definición de columna. Por ejemplo, una columna definida como **datetimeoffset** (2) tendrán dos dígitos fraccionarios.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **datetime** formato|'Aaaa-MM-DD hh [.nnn]'<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123'|Los dígitos fraccionarios que faltan y los valores de desplazamiento se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35:29.123' se inserta como ' 2007-05-08 12:35:29.1230000 + 00:00 '.|  
|Literal de cadena de **smalldatetime** formato|'Aaaa-MM-DD hh'<br /><br />Ejemplo: ' 2007-05-08 12:35 '|Segundos, los dígitos fraccionarios restantes y los valores de desplazamiento se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'AAAA-MM-DD'<br /><br />Ejemplo: ' 2007-05-08'|Valores de tiempo (hora, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08' se inserta como ' 2007-05-08 00:00:00.0000000 + 00:00 '.|  
|Literal de cadena de **datetime2** formato|'Aaaa-MM-DD. nnnnnnn'<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567'|Los datos de origen no pueden superar el número especificado de segundos fraccionarios en la columna de datetimeoffset. Si el origen de datos tiene un número igual o menor de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es datetimeoffset (5), el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' se inserta como ' 12:35:29.12300 + 12:15 '.|  
|Literal de cadena de **datetimeoffset** formato|'. Nnnnnnn aaaa-MM-DD {+&#124;-} hh: mm '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567 + 12:15 '|Los datos de origen no pueden superar el número especificado de segundos fraccionarios en la columna de datetimeoffset. Si el origen de datos tiene un número igual o menor de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es datetimeoffset (5), el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' se inserta como ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>tipo de datos datetime2  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **datetime2** (*n*). El formato predeterminado es 'Aaaa-MM-DD. nnnnnnn'. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error. El número de dígitos fraccionarios depende de la definición de columna. Por ejemplo, una columna definida como **datetime2** (2) tendrán dos dígitos fraccionarios.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **datetime** formato|'Aaaa-MM-DD hh [.nnn]'<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123'|Las fracciones de segundo son opcionales y se establecen en 0 cuando se inserta el valor.<br /><br />Un valor que tiene más dígitos fraccionarios que el tipo de datos de destino se rechaza.|  
|Literal de cadena de **smalldatetime** formato|'Aaaa-MM-DD hh'<br /><br />Ejemplo: ' 2007-05-08 12'|Segundos opcionales y los dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'AAAA-MM-DD'<br /><br />Ejemplo: ' 2007-05-08'|Valores de tiempo (hora, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08' se inserta como ' 2007-05-08 12:00:00.0000000'.|  
|Literal de cadena de **datetime2** formato|'Aaaa-MM-DD hh:mm:ss:nnnnnnn'<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567'|Si el origen de datos contiene componentes de fecha y hora que son menores o iguales al valor especificado en **datetime2**(*n*), los datos se insertan; en caso contrario, se genera un error.|  
  
## <a name="InsertLiteralsNumeric"></a>Insertar literales en tipos numéricos  
En las tablas siguientes se definen los formatos aceptados y reglas de conversión para insertar un valor literal en una columna de distribución de PDW de SQL Server que usa un tipo numérico.  
  
### <a name="bit-data-type"></a>bit, tipo de datos  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **bits**. Una cadena vacía (") o una cadena que contiene solo espacios en blanco (' ') se convierte en 0.  
  
|Tipo de literal|format|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **entero** formato|'nnnnnnnnnn'<br /><br />Ejemplo: '1' o '321'|Un valor entero con formato de un literal de cadena no puede contener un valor negativo. Por ejemplo, el valor '-123' genera un error.<br /><br />Un valor mayor que 1 se convierte en 1. Por ejemplo, el valor '123' se convierte en 1.|  
|Literal de cadena|'TRUE' o 'FALSE'<br /><br />Ejemplo: 'true'|El valor 'TRUE' se convierte en 1; el valor 'FALSE' se convierte en 0.|  
|Literal de tipo entero|nnnnnnnn<br /><br />Ejemplo: 1 o 321|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, se convierten los valores 123 y-123 en 1.|  
|Literal decimal|nnnnn.nnnn<br /><br />Ejemplo: 1234.5678|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, los valores 123,45 y sería -123,45 se convierten en 1.|  
  
### <a name="decimal-data-type"></a>tipo de datos decimal  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **decimal** (*p, s*). Las reglas de conversión de datos son las mismas que para SQL Server. Para obtener más información, consulte [conversión de tipos de datos](http://msdn.microsoft.com/library/ms191530&#40;v=sql11&#40;.aspx) en MSDN.  
  
|Tipo de literal|Formato|  
|----------------|----------|  
|Literal de cadena de **entero** formato|'nnnnnnnnnnnn'<br /><br />Ejemplo: '321312313123'|  
|Literal de cadena de **decimal** formato|'nnnnnn.nnnnn'<br /><br />Ejemplo: '123344.34455'|  
|Literal de tipo entero|nnnnnnnnnnnn<br /><br />Ejemplo: 321312313123|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Ejemplo: '123344.34455'|  
  
### <a name="float-and-real-data-types"></a>tipos de datos float y real  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **float** o **real**. Las reglas de conversión de datos son las mismas que para SQL Server. Para obtener más información, consulte [conversión de tipos de datos](http://msdn.microsoft.com/library/ms191530&#40;v=sql11&#40;.aspx) en MSDN.  
  
|Tipo de literal|Formato|  
|----------------|----------|  
|Literal de cadena de **entero** formato|'nnnnnnnnnnnn'<br /><br />Ejemplo: '321312313123'|  
|Literal de cadena de **decimal** formato|'nnnnnn.nnnnn'<br /><br />Ejemplo: '123344.34455'|  
|Literal de cadena de **punto flotante** formato|'n.nnnnnE+nn'<br /><br />Ejemplo: '3.12323E + 14'|  
|Literal de tipo entero|nnnnnnnnnnnn<br /><br />Ejemplo: 321312313123|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Ejemplo: 123344.34455|  
|Literal de punto flotante|n.nnnnnE+nn<br /><br />Ejemplo: 3.12323E + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int, bigint, tinyint, smallint los tipos de datos  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **int**, **bigint**, **tinyint**, o **smallint**. El origen de datos no puede superar el intervalo permitido para el tipo de datos determinado. Por ejemplo, el intervalo de **tinyint** es de 0 a 255 y el intervalo de **int** es -2.147.483.648 a 2.147.483.647.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|------------|------|----------------|
|Literal de cadena de **entero** formato|'nnnnnnnnnnnnnn'<br /><br />Ejemplo: '321312313123'| None |  
|Literal de tipo entero|nnnnnnnnnnnnnn<br /><br />Ejemplo: 321312313123| None|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Ejemplo: 123344.34455|Se truncan los valores a la derecha del separador decimal.|  
  
### <a name="money-and-smallmoney-data-types"></a>tipos de datos Money y smallmoney  
Valores literales Money se representan como números con un punto decimal opcional y un símbolo de moneda como prefijo. El origen de datos no puede superar el intervalo permitido para el tipo de datos determinado. Por ejemplo, el intervalo de **smallmoney** es -214.748,3648 a 214.748,3647 y el intervalo de **dinero** es-922.337.203.685.477,5808 y 922.337.203.685.477,5807. La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **dinero** o **smallmoney**.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena de **entero** formato|'nnnnnnnn'<br /><br />Ejemplo: '123433'|Falta dígitos después del separador decimal se establecen en 0 cuando se inserta el valor. Por ejemplo, se inserta el literal '12345' como 12345.0000.|  
|Literal de cadena de **decimal** formato|'nnnnnn.nnnnn'<br /><br />Ejemplo: '123344.34455'|Si el número de dígitos después del punto decimal superior a 4, el valor se redondea al valor más cercano. Por ejemplo, se inserta el valor '123344.34455' como 123344.3446.|  
|Literal de cadena de **dinero** formato|'$nnnnnn.nnnn'<br /><br />Ejemplo: '$123456.7890'|El símbolo de moneda opcionales no se inserta con el valor.<br /><br />Si el número de dígitos después del punto decimal superior a 4, el valor se redondea al valor más cercano.|  
|Literal de tipo entero|nnnnnnnn<br /><br />Ejemplo: 123433|Falta dígitos después del separador decimal se establecen en 0 cuando se inserta el valor. Por ejemplo, se inserta el literal 12345 como 12345.0000.|  
|Literal decimal|nnnnnn.nnnnn<br /><br />Ejemplo: 123344.34455|Si el número de dígitos después del punto decimal superior a 4, el valor se redondea al valor más cercano. Por ejemplo, se inserta el valor 123344.34455 como 123344.3446.|  
|Money literal|$nnnnnn.nnnn<br /><br />Ejemplo: $123456.7890|El símbolo de moneda opcionales no se inserta con el valor.<br /><br />Si el número de dígitos después del punto decimal superior a 4, el valor se redondea al valor más cercano.|  
  
## <a name="InsertLiteralsString"></a>Insertar literales en tipos de cadena  
En las tablas siguientes se definen los formatos aceptados y reglas de conversión para insertar un valor literal en una columna de PDW de SQL Server que utiliza un tipo de cadena.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>tipos de datos char, varchar, nchar y nvarchar  
La siguiente tabla definen los formatos aceptados y las reglas para insertar valores literales en una columna de distribución de tipo **char**, **varchar**, **nchar** y **nvarchar**. La longitud del origen de datos no puede superar el tamaño especificado para el tipo de datos. Si la longitud del origen de datos es menor que el tamaño de la **char** o **nchar** tipo de datos, los datos se rellenan a la derecha con espacios en blanco para alcanzar el tamaño del tipo de datos.  
  
|Tipo de literal|Formato|Reglas de conversión|  
|----------------|----------|--------------------|  
|Literal de cadena|Formato: 'cadena de caracteres'<br /><br />Ejemplo: 'abc'| None|  
|Literal de cadena Unicode|Formato: Cadena N'character'<br /><br />Ejemplo: Abc '|  None |  
|Literal de tipo entero|Formato: nnnnnnnnnnn<br /><br />Ejemplo: 321312313123| None |  
|Literal decimal|Formato: nnnnnn.nnnnnnn<br /><br />Ejemplo: 12344.34455| None |  
|Money literal|Formato: $nnnnnn.nnnnn<br /><br />Ejemplo: $123456.99|No se inserta el símbolo de moneda con el valor. Para insertar el símbolo de moneda, inserte el valor como un literal de cadena. Esto coincidirá con el formato de la **dwloader** herramienta, que debe tratar cada literal como un literal de cadena.<br /><br />No se permiten comas.<br /><br />Si el número de dígitos después del punto decimal superior a 2, el valor se redondea al valor más cercano. Por ejemplo, se inserta el valor 123.946789 como 123.95.<br /><br />Se permite solo el estilo predeterminado de 0 (sin comas y 2 dígitos después del separador decimal) cuando se usa la función CONVERT para insertar literales de dinero.|  

  
## <a name="see-also"></a>Vea también  
 
[Datos distribuidos](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-distributed-data/)  
[INSERT](../t-sql/statements/insert-transact-sql.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Metadata query examples](metadata-query-examples.md) 
-->
