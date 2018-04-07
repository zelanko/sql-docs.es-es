---
title: Tipo de datos de reglas de conversión para dwloader
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Este tema describe los formatos de datos de entrada y conversiones de tipos de datos implícitas que dwloader que admite el cargador de línea de comandos cuando se carga datos en PDW.
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 79c48520-b08b-4b15-a943-a551cc90a2c4
caps.latest.revision: 30
ms.openlocfilehash: 6910358803673c34d2381d071340e2ec7c8f2a0b
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="data-type-conversion-rules-for-dwloader"></a>Tipo de datos de reglas de conversión para dwloader
En este tema se describe los formatos de datos de entrada y conversiones de tipos de datos implícitas que [dwloader cargador de línea de comandos](dwloader.md) admite cuando se carga datos en PDW. Las conversiones de datos implícitas se producen cuando los datos de entrada no coincide con el tipo de datos en la tabla de destino de SQL Server PDW. Utilice esta información al diseñar el proceso de carga para garantizar que sus datos se cargará correctamente en PDW de SQL Server.  
   
  
## <a name="InsertBinaryTypes"></a>Insertar literales en tipos binarios  
La siguiente tabla definen los tipos literales aceptados, formato y las reglas de conversión para cargar un valor literal en una columna de SQL Server PDW de tipo **binario** (*n*) o **varbinary** (*n*).  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a binary o varbinary, tipo de datos|  
|-------------------|-----------------------|-----------------------------------------------|  
|Literal binario|[0x]*hexidecimal_string*<br /><br />Ejemplo: 12Ef o 0x12Ef|El prefijo 0 x es opcional.<br /><br />La longitud del origen de datos no puede superar el número de bytes especificado para el tipo de datos.<br /><br />Si la longitud del origen de datos es menor que el tamaño de la **binario** tipo de datos, los datos se rellenan a la derecha con ceros para alcanzar el tamaño del tipo de datos.|  
  
## <a name="InsertDateTimeTypes"></a>Insertar literales en tipos de fecha y hora  
Literales de fecha y hora se representan mediante el uso de literales de cadena en formatos específicos, entre comillas simples. En las tablas siguientes se definen los tipos permitidos de literales, formato y las reglas de conversión para cargar una fecha u hora literal en una columna de tipo **datetime**, **smalldatetime**, **fecha**, **tiempo**, **datetimeoffset**, o **datetime2**. Las tablas definen el formato predeterminado para el tipo de datos determinado. Otros formatos que se pueden especificar se definen en la sección [formatos de fecha y hora](#DateFormats). Literales de fecha y hora no pueden incluir espacios iniciales ni finales. **fecha**, **smalldatetime**, y valores null no se puede cargar en modo de ancho fijo.  
  
### <a name="datetime-data-type"></a>Tipo de datos datetime  
En la tabla siguiente define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **datetime**. Una cadena vacía (") se convierte en el valor predeterminado ' 12:00:00.000 1900-01-01'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos datetime|  
|-------------------|-----------------------|------------------------------------|  
|Literal de cadena de **datetime** formato|'aaaa-MM-dd hh [.fff]'<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123'|Los dígitos fraccionarios que faltan se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35 ' se inserta como ' 2007-05-08 12:35:00.000'.|  
|Literal de cadena de **smalldatetime** formato|'aaaa-MM-dd hh'<br /><br />Ejemplo: ' 2007-05-08 12:35 '|Segundos y los dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'yyyy-MM-dd'<br /><br />Ejemplo: ' 2007-05-08'|Valores de tiempo (hora, minutos, segundos y fracciones) se establecen en 12:00:00.000 cuando se inserta el valor.|  
|Literal de cadena de **datetime2** formato|se ss 'aaaa-MM-dd. 'fffffff<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567'|Los datos de origen no pueden superar los tres dígitos fraccionarios. Por ejemplo, el literal ' 2007-05-08 12:35:29.123' se van a insertar, pero el valor ' 2007-05-8 12:35:29.1234567' genera un error.|  
  
### <a name="smalldatetime-data-type"></a>Tipo de datos smalldatetime  
En la tabla siguiente define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **smalldatetime**. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos smalldatetime|  
|-------------------|-----------------------|-----------------------------------------|  
|Literal de cadena de **smalldatetime** formato|'aaaa-MM-dd hh: mm' o 'aaaa-MM-dd hh'<br /><br />Ejemplo: ' 2007-05-08 12:00 ' o ' 2007-05-08 12:00:15 '|Los datos de origen deben tener valores de año, mes, fecha, hora y minuto. Segundos son opcionales y, si está presente, deben establecerse en el valor 00. Cualquier otro valor genera un error.<br /><br />Los segundos son opcionales. Cuando se carga en una columna de smalldatetime, dwloader redondeará hacia arriba los segundos y fracciones de segundo. Por ejemplo, 1999-01-05 20:10:35.123 se cargará como 01-05 20:11.|  
|Literal de cadena de **fecha** formato|'yyyy-MM-dd'<br /><br />Ejemplo: ' 2007-05-08'|Valores de tiempo (hora, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor.|  
  
### <a name="date-data-type"></a>Tipo de datos date  
En la tabla siguiente define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **fecha**. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos de fecha|  
|-------------------|-----------------------|--------------------------------|  
|Literal de cadena de **fecha** formato|'yyyy-MM-dd'<br /><br />Ejemplo: ' 2007-05-08'||  
  
### <a name="time-data-type"></a>Tipo de datos de tiempo  
En la tabla siguiente define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **tiempo**. Una cadena vacía (") se convierte en el valor predeterminado '00:00:00.0000'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos de tiempo|  
|-------------------|-----------------------|--------------------------------|  
|Literal de cadena de **tiempo** formato|'hh:mm:ss.fffffff'<br /><br />Ejemplo: '12:35:29.1234567'|Si el origen de datos tiene una precisión menor o igual (número de dígitos fraccionarios) que la precisión de la **tiempo** tipo de datos, los datos se rellenan a la derecha con ceros. Por ejemplo, se inserta un valor literal '12:35:29.123' como '12:35:29.1230000'.|  
  
### <a name="datetimeoffset-data-type"></a>Tipo de datos DateTimeOffset  
En la tabla siguiente define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **datetimeoffset** (*n*). El formato predeterminado es ' aaaa-MM-dd ss. fffffff {+ |-} hh: mm '. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00:00.0000000 + 00:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error. El número de dígitos fraccionarios depende de la definición de columna. Por ejemplo, una columna definida como **datetimeoffset** (2) tendrán dos dígitos fraccionarios.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos datetimeoffset|  
|-------------------|-----------------------|------------------------------------------|  
|Literal de cadena de **datetime** formato|'aaaa-MM-dd hh [.fff]'<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123'|Los dígitos fraccionarios que faltan y los valores de desplazamiento se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35:29.123' se inserta como ' 2007-05-08 12:35:29.1230000 + 00:00 '.|  
|Literal de cadena de **smalldatetime** formato|'aaaa-MM-dd hh'<br /><br />Ejemplo: ' 2007-05-08 12:35 '|Segundos, los dígitos fraccionarios restantes y los valores de desplazamiento se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'yyyy-MM-dd'<br /><br />Ejemplo: ' 2007-05-08'|Valores de tiempo (hora, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08' se inserta como ' 2007-05-08 00:00:00.0000000 + 00:00 '.|  
|Literal de cadena de **datetime2** formato|se ss 'aaaa-MM-dd. 'fffffff<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567'|Los datos de origen no pueden superar el número especificado de segundos fraccionarios en la columna de datetimeoffset. Si el origen de datos tiene un número igual o menor de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es datetimeoffset (5), el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' se inserta como ' 12:35:29.12300 + 12:15 '.|  
|Literal de cadena de **datetimeoffset** formato|' aaaa-MM-dd ss. fffffff {+&#124;-} hh: mm '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567 + 12:15 '|Los datos de origen no pueden superar el número especificado de segundos fraccionarios en la columna de datetimeoffset. Si el origen de datos tiene un número igual o menor de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es datetimeoffset (5), el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' se inserta como ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>Tipo de datos datetime2  
En la tabla siguiente define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **datetime2** (*n*). El formato predeterminado es 'se ss aaaa-MM-dd. ' fffffff. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error. El número de dígitos fraccionarios depende de la definición de columna. Por ejemplo, una columna definida como **datetime2** (2) tendrán dos dígitos fraccionarios.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos datetime2|  
|-------------------|-----------------------|-------------------------------------|  
|Literal de cadena de **datetime** formato|'aaaa-MM-dd hh [.fff]'<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123'|Las fracciones de segundo son opcionales y se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **smalldatetime** formato|'aaaa-MM-dd hh'<br /><br />Ejemplo: ' 2007-05-08 12'|Segundos opcionales y los dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'yyyy-MM-dd'<br /><br />Ejemplo: ' 2007-05-08'|Valores de tiempo (hora, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08' se inserta como ' 2007-05-08 12:00:00.0000000'.|  
|Literal de cadena de **datetime2** formato|'aaaa-MM-dd hh:mm:ss:fffffff'<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567'|Si el origen de datos contiene componentes de fecha y hora que son menores o iguales al valor especificado en **datetime2**(*n*), los datos se insertan; en caso contrario, se genera un error.|  
  
### <a name="DateFormats"></a>Formatos de fecha y hora  
Dwloader admite los siguientes formatos de datos para los datos de entrada que se está cargando en PDW de SQL Server. Obtener más detalles se muestran después de la tabla.  
  
|datetime|smalldatetime|date|datetime2|datetimeoffset|  
|------------|-----------------|--------|-------------|------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[yy]yy HH:mm[:00]|[M[M]]M-[d]d-[yy]yy|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm[:00][tt]||[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm[:00][tt]||[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm[:00][tt]||[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[yy]yy-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm[:00][tt]||[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fff]|[d]d-[M[M]]M-[yy]yy HH:mm[:00]|[d]d-[M[M]]M-[yy]yy|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm[:00][tt]||[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm[:00][tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
Detalles:  
  
-   Para separar los valores de mes, día y año, puede usar ':', '/' o '. '. Para simplificar, en la tabla solo se usa el separador ' – '.  
  
-   Para especificar el mes como texto use tres o más caracteres. Meses con caracteres de 1 ó 2 se interpretará como un número.  
  
-   Para separar los valores de hora, use el ': ' símbolo.  
  
-   Las letras entre corchetes son opcionales.  
  
-   Las letras "tt" designan [a.m. | p.m.]. a.m. es el valor predeterminado. Cuando se especifica 'tt', el valor de hora (hh) debe estar comprendido entre 0 y 12.  
  
-   Las letras 'zzz' designan el desfase de zona horaria de la zona horaria actual del sistema en el formato {+|-}HH:ss].  
  
## <a name="InsertNumerictypes"></a>Insertar literales en tipos numéricos  
En las tablas siguientes se definen las reglas de conversión y formato predeterminado para cargar un valor literal en una columna de PDW de SQL Server que usa un tipo numérico.  
  
### <a name="bit-data-type"></a>Tipo de datos bit  
En la tabla siguiente define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **bits**. Una cadena vacía (") o una cadena que contiene solo espacios en blanco (' ') se convierte en 0.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión de tipo de datos bit|  
|-------------------|-----------------------|-------------------------------|  
|Literal de cadena de **entero** formato|'ffffffffff'<br /><br />Ejemplo: '1' o '321'|Un valor entero con formato de un literal de cadena no puede contener un valor negativo. Por ejemplo, el valor '-123' genera un error.<br /><br />Un valor mayor que 1 se convierte en 1. Por ejemplo, el valor '123' se convierte en 1.|  
|Literal de cadena|'TRUE' o 'FALSE'<br /><br />Ejemplo: 'true'|El valor 'TRUE' se convierte en 1; el valor 'FALSE' se convierte en 0.|  
|Literal de tipo entero|fffffffn<br /><br />Ejemplo: 1 o 321|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, se convierten los valores 123 y-123 en 1.|  
|Literal decimal|fffnn.fffn<br /><br />Ejemplo: 1234.5678|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, los valores 123,45 y sería -123,45 se convierten en 1.|  
  
### <a name="decimal-data-type"></a>Tipo de datos decimal  
En la tabla siguiente define las reglas para cargar los valores literales en una columna de tipo **decimal** (*p, s*). Las reglas de conversión de datos son las mismas que para SQL Server. Para obtener más información, consulte [conversión de tipos de datos (Database Engine)](http://go.microsoft.com/fwlink/?LinkId=202128) en MSDN.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|  
|-------------------|-----------------------|  
|Literal de tipo entero|321312313123|  
|Literal decimal|123344.34455|  
  
### <a name="float-and-real-data-types"></a>Tipos de datos float y real  
En la tabla siguiente define las reglas para cargar los valores literales en una columna de tipo **float** o **real**. Las reglas de conversión de datos son las mismas que para SQL Server. Para obtener más información, consulte [conversión de tipos de datos (Database Engine)](../t-sql/data-types/data-type-conversion-database-engine.md) en MSDN.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|  
|-------------------|-----------------------|  
|Literal de tipo entero|321312313123|  
|Literal decimal|123344.34455|  
|Literal de punto flotante|3.12323E+14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int, bigint, tinyint, smallint los tipos de datos  
En la tabla siguiente define las reglas para cargar los valores literales en una columna de tipo **int**, **bigint**, **tinyint**, o **smallint**. El origen de datos no puede superar el intervalo permitido para el tipo de datos determinado. Por ejemplo, el intervalo de **tinyint** es de 0 a 255 y el intervalo de **int** es -2.147.483.648 a 2.147.483.647.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión de tipos de datos enteros|  
|-------------------|-----------------------|------------------------------------|  
|Literal de tipo entero|321312313123||  
|Literal decimal|123344.34455|Se truncan los valores a la derecha del separador decimal.|  
  
### <a name="money-and-smallmoney-data-types"></a>Tipos de datos Money y smallmoney  
Valores literales Money se representan como una cadena de números con un punto decimal opcional y un símbolo de moneda opcionales como prefijo. El origen de datos no puede superar el intervalo permitido para el tipo de datos determinado. Por ejemplo, el intervalo de **smallmoney** es -214.748,3648 a 214.748,3647 y el intervalo de **dinero** es-922.337.203.685.477,5808 y 922.337.203.685.477,5807. En la tabla siguiente define las reglas para cargar los valores literales en una columna de tipo **dinero** o **smallmoney**.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a money o smallmoney, tipo de datos|  
|-------------------|-----------------------|-----------------------------------------------|  
|Literal de tipo entero|321312|Falta dígitos después del separador decimal se establecen en 0 cuando se inserta el valor. Por ejemplo, se inserta el literal 12345 como 12345.0000|  
|Literal decimal|123344.34455|Si el número de dígitos después del punto decimal superior a 4, el valor se redondea al valor más cercano. Por ejemplo, se inserta el valor 123344.34455 como 123344.3446.|  
|Money literal|$123456.7890|No se inserta el símbolo de moneda con el valor.<br /><br />Si el número de dígitos después del punto decimal superior a 4, el valor se redondea al valor más cercano.|  
  
## <a name="InsertStringTypes"></a>Insertar literales en tipos de cadena  
En las tablas siguientes se definen las reglas de conversión y formato predeterminado para cargar un valor literal en una columna de PDW de SQL Server que usa un tipo de cadena.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>Tipos de datos char, varchar, nchar y nvarchar  
En la tabla siguiente define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **char**, **varchar**, **nchar** y **nvarchar** . La longitud del origen de datos no puede superar el tamaño especificado para el tipo de datos. Si la longitud del origen de datos es menor que el tamaño de la **char** o **nchar** tipo de datos, los datos se rellenan a la derecha con espacios en blanco para alcanzar el tamaño del tipo de datos.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión de tipos de datos de caracteres|  
|---------------|-------------------|----------------------------------|  
|Literal de cadena|Formato: 'cadena de caracteres'<br /><br />Ejemplo: 'abc'| N/D |  
|Literal de cadena Unicode|Formato: Cadena N'character'<br /><br />Ejemplo: Abc '| N/D |  
|Literal de tipo entero|Formato: ffffffffffn<br /><br />Ejemplo: 321312313123| N/D |  
|Literal decimal|Formato: ffffff.fffffff<br /><br />Ejemplo: 12344.34455| N/D |  
|Money literal|Formato: $ffffff.fffnn<br /><br />Ejemplo: $123456.99|El símbolo de moneda opcionales no se inserta con el valor. Para insertar el símbolo de moneda, inserte el valor como un literal de cadena. Esto coincidirá con el formato del cargador, lo que debe tratar cada literal como un literal de cadena.<br /><br />No se permiten comas.<br /><br />Si el número de dígitos después del punto decimal superior a 2, el valor se redondea al valor más cercano. Por ejemplo, se inserta el valor 123.946789 como 123.95.<br /><br />Se permite solo el estilo predeterminado de 0 (sin comas y 2 dígitos después del separador decimal) cuando se usa la función CONVERT para insertar literales de dinero.|  
  
### <a name="general-remarks"></a>Notas generales  
**dwloader** realiza las mismas conversiones implícitas que SMP de SQL Server realiza, pero no admiten todas las conversiones implícitas que admite SMP de SQL Server.  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
