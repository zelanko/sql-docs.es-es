---
title: Tipo de datos de Dwloader reglas de conversión de - almacenamiento de datos paralelos | Microsoft Docs
description: En este tema se describe los formatos de datos de entrada y las conversiones de tipos de datos implícitas dicho cuando carga datos en el almacenamiento de datos paralelos (PDW) admite el cargador de línea de comandos de dwloader."
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 46d092ee5d3b981c60d7bd5bde49f9994dab4b08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042586"
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>Tipo de datos de reglas de conversión de dwloader - almacenamiento de datos paralelos
En este tema se describe los formatos de datos de entrada y las conversiones de tipos de datos implícitas que [del cargador de la línea de comandos de dwloader](dwloader.md) admite cuando carga datos en PDW. Las conversiones de datos implícitas se producen cuando los datos de entrada no coincide con el tipo de datos en la tabla de destino PDW de SQL Server. Utilice esta información al diseñar el proceso de carga para garantizar que los datos se cargará correctamente en PDW de SQL Server.  
   
  
## <a name="InsertBinaryTypes"></a>Insertar literales en tipos binarios  
La siguiente tabla define los tipos literales aceptados, formato y las reglas de conversión para cargar un valor literal en una columna de PDW de SQL Server de tipo **binario** (*n*) o **varbinary** (*n*).  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a binary o varbinary, tipo de datos|  
|-------------------|-----------------------|-----------------------------------------------|  
|Literal binario|[0x]*hexidecimal_string*<br /><br />Ejemplo: 12Ef o 0x12Ef|El prefijo 0 x es opcional.<br /><br />La longitud del origen de datos no puede superar el número de bytes especificado para el tipo de datos.<br /><br />Si la longitud del origen de datos es menor que el tamaño de la **binario** tipo de datos, los datos se rellenan a la derecha con ceros para alcanzar el tamaño del tipo de datos.|  
  
## <a name="InsertDateTimeTypes"></a>Insertar literales en tipos de fecha y hora  
Literales de fecha y hora se representan mediante el uso de literales de cadena en formatos específicos, entrecomillados comillas simples. Las siguientes tablas definen los tipos literales permitidos, formato y las reglas de conversión para cargar una fecha u hora literal en una columna de tipo **datetime**, **smalldatetime**, **fecha**, **tiempo**, **datetimeoffset**, o **datetime2**. Las tablas definen el formato predeterminado para el tipo de datos determinado. Otros formatos que se pueden especificar se definen en la sección [formatos de fecha y hora](#DateFormats). Literales de fecha y hora no pueden incluir espacios iniciales o finales. **fecha**, **smalldatetime**, y los valores null no se puede cargar en modo de ancho fijo.  
  
### <a name="datetime-data-type"></a>Tipo de datos datetime  
La siguiente tabla define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **datetime**. Una cadena vacía (") se convierte en el valor predeterminado ' 12:00:00.000 1900-01-01'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipo de datos datetime|  
|-------------------|-----------------------|------------------------------------|  
|Literal de cadena de **datetime** formato|'yyyy-MM-dd hh:mm:ss[.fff]'<br /><br />Ejemplo: '2007-05-08 12:35:29.123'|Los dígitos fraccionarios que faltan se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35 ' se inserta como ' 2007-05-08 12:35:00.000'.|  
|Literal de cadena de **smalldatetime** formato|"aaaa-MM-dd hh: mm"<br /><br />Ejemplo: '2007-05-08 12:35'|Segundos y dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'yyyy-MM-dd'<br /><br />Ejemplo: '2007-05-08'|Cuando se inserta el valor, se establecen los valores de tiempo (horas, minutos, segundos y fracciones) en 12:00:00.000.|  
|Literal de cadena de **datetime2** formato|'yyyy-MM-dd hh:mm:ss.fffffff'<br /><br />Ejemplo: '2007-05-08 12:35:29.1234567'|Los datos de origen no pueden superar los tres dígitos fraccionarios. Por ejemplo, el literal ' 2007-05-08 12:35:29.123' se van a insertar, pero el valor ' 2007-05-8 12:35:29.1234567' genera un error.|  
  
### <a name="smalldatetime-data-type"></a>Tipo de datos smalldatetime  
La siguiente tabla define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **smalldatetime**. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipo de datos smalldatetime|  
|-------------------|-----------------------|-----------------------------------------|  
|Literal de cadena de **smalldatetime** formato|'aaaa-MM-dd hh: mm' o 'aaaa-MM-dd hh: mm:'<br /><br />Ejemplo: "2007-05-08 12:00 ' o ' 2007-05-08:00-12:15"|Los datos de origen deben tener los valores de año, mes, fecha, hora y minuto. Segundos son opcionales y, si está presente, se deben establecer en el valor 00. Cualquier otro valor genera un error.<br /><br />Los segundos son opcionales. Cuando se cargan en una columna de smalldatetime, dwloader redondeará hacia arriba los segundos y fracciones de segundo. Por ejemplo, se cargará 20:10:35.123 1999-05-01 como 01-05 20:11.|  
|Literal de cadena de **fecha** formato|'yyyy-MM-dd'<br /><br />Ejemplo: '2007-05-08'|Los valores de tiempo (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor.|  
  
### <a name="date-data-type"></a>Tipo de datos date  
La siguiente tabla define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **fecha**. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipo de datos de fecha|  
|-------------------|-----------------------|--------------------------------|  
|Literal de cadena de **fecha** formato|'yyyy-MM-dd'<br /><br />Ejemplo: '2007-05-08'||  
  
### <a name="time-data-type"></a>Tipo de datos Time  
La siguiente tabla define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **tiempo**. Una cadena vacía (") se convierte en el valor predeterminado '00:00:00.0000'. Las cadenas que contienen solo espacios en blanco (' ') generará un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipo de datos de tiempo|  
|-------------------|-----------------------|--------------------------------|  
|Literal de cadena de **tiempo** formato|'hh:mm:ss.fffffff'<br /><br />Ejemplo: '12:35:29.1234567'|Si el origen de datos tiene una precisión menor o igual (número de dígitos fraccionarios) que la precisión de la **tiempo** tipo de datos, los datos se rellenan a la derecha con ceros. Por ejemplo, se inserta un valor literal '12:35:29.123' como '12:35:29.1230000'.|  
  
### <a name="datetimeoffset-data-type"></a>Tipo de datos DateTimeOffset  
La siguiente tabla define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **datetimeoffset** (*n*). El formato predeterminado es ' aaaa-MM-dd fffffff {+ |-} hh: mm '. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00:00.0000000 + 00:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error. El número de dígitos fraccionarios depende de la definición de columna. Por ejemplo, una columna definida como **datetimeoffset** (2) tendrán dos dígitos fraccionarios.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipo de datos datetimeoffset|  
|-------------------|-----------------------|------------------------------------------|  
|Literal de cadena de **datetime** formato|'yyyy-MM-dd hh:mm:ss[.fff]'<br /><br />Ejemplo: '2007-05-08 12:35:29.123'|Los dígitos fraccionarios que faltan y valores de desplazamiento se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35:29.123' se inserta como ' 2007-05-08 12:35:29.1230000 + 00:00 '.|  
|Literal de cadena de **smalldatetime** formato|"aaaa-MM-dd hh: mm"<br /><br />Ejemplo: '2007-05-08 12:35'|Segundos, los dígitos fraccionarios restantes y valores de desplazamiento se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'yyyy-MM-dd'<br /><br />Ejemplo: '2007-05-08'|Los valores de tiempo (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08' se inserta como ' 2007-05-08 00:00:00.0000000 + 00:00 '.|  
|Literal de cadena de **datetime2** formato|'yyyy-MM-dd hh:mm:ss.fffffff'<br /><br />Ejemplo: '2007-05-08 12:35:29.1234567'|Los datos de origen no pueden superar el número especificado de segundos fraccionarios en la columna de datetimeoffset. Si el origen de datos tiene un número igual o menor de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es datetimeoffset (5), el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' se inserta como ' 12:35:29.12300 + 12:15 '.|  
|Literal de cadena de **datetimeoffset** formato|' aaaa-MM-dd fffffff {+&#124;-} hh: mm '<br /><br />Ejemplo: '2007-05-08 12:35:29.1234567 +12:15'|Los datos de origen no pueden superar el número especificado de segundos fraccionarios en la columna de datetimeoffset. Si el origen de datos tiene un número igual o menor de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es datetimeoffset (5), el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' se inserta como ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>Tipo de datos datetime2  
La siguiente tabla define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **datetime2** (*n*). El formato predeterminado es 'aaaa-MM-dd fffffff'. Una cadena vacía (") se convierte en el valor predeterminado ' 1900-01-01 12:00:00 '. Las cadenas que contienen solo espacios en blanco (' ') generará un error. El número de dígitos fraccionarios depende de la definición de columna. Por ejemplo, una columna definida como **datetime2** (2) tendrán dos dígitos fraccionarios.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipo de datos datetime2|  
|-------------------|-----------------------|-------------------------------------|  
|Literal de cadena de **datetime** formato|'yyyy-MM-dd hh:mm:ss[.fff]'<br /><br />Ejemplo: '2007-05-08 12:35:29.123'|Fracciones de segundo son opcionales y se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **smalldatetime** formato|"aaaa-MM-dd hh: mm"<br /><br />Ejemplo: '2007-05-08 12'|Segundos opcionales y dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena de **fecha** formato|'yyyy-MM-dd'<br /><br />Ejemplo: '2007-05-08'|Los valores de tiempo (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08' se inserta como ' 2007-05-08 12:00:00.0000000'.|  
|Literal de cadena de **datetime2** formato|'aaaa-MM-dd hh:mm:ss:fffffff'<br /><br />Ejemplo: '2007-05-08 12:35:29.1234567'|Si el origen de datos contiene datos y la hora de los componentes que son menores o iguales al valor especificado en **datetime2**(*n*), se insertan los datos; en caso contrario, se genera un error.|  
  
### <a name="DateFormats"></a>Formatos de fecha y hora  
Dwloader admite los siguientes formatos de datos para los datos de entrada que se está cargando en PDW de SQL Server. Después de la tabla, se muestran más detalles.  
  
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
  
-   Para separar los valores de mes, día y año, puede usar '-', '/' o '. '. Para simplificar, en la tabla solo se usa el separador “-”.  
  
-   Para especificar el mes como texto use tres o más caracteres. Los meses con 1 o 2 caracteres se interpretará como un número.  
  
-   Para separar los valores de hora, use el ': ' símbolo.  
  
-   Las letras entre corchetes son opcionales.  
  
-   Las letras "tt" designan [a.m. | p.m.]. a.m. es el valor predeterminado. Cuando se especifica 'tt', el valor de hora (hh) debe estar comprendido entre 0 y 12.  
  
-   Las letras 'zzz' designan el desfase de zona horaria de la zona horaria actual del sistema en el formato {+|-}HH:ss].  
  
## <a name="InsertNumerictypes"></a>Insertar literales en tipos numéricos  
Las tablas siguientes definen las reglas predeterminadas de conversión y formato para cargar un valor literal en una columna de PDW de SQL Server que usa un tipo numérico.  
  
### <a name="bit-data-type"></a>Tipo de datos bit  
La siguiente tabla define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **bits**. Una cadena vacía (") o una cadena que contiene solo espacios en blanco (' ') se convierte en 0.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipo de datos bit|  
|-------------------|-----------------------|-------------------------------|  
|Literal de cadena de **entero** formato|'ffffffffff'<br /><br />Ejemplo: '1' o '321'|Un valor entero con formato de un literal de cadena no puede contener un valor negativo. Por ejemplo, el valor '-' 123 genera un error.<br /><br />Un valor mayor que 1 se convierte en 1. Por ejemplo, el valor '123' se convierte en 1.|  
|Literal de cadena|'TRUE' o 'FALSE'<br /><br />Ejemplo: 'true'|El valor 'TRUE' se convierte en 1; el valor 'FALSE' se convierte en 0.|  
|Literal entero|fffffffn<br /><br />Ejemplo: 1 o 321|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, los valores 123 y -123 se convierten en 1.|  
|Literal decimal|fffnn.fffn<br /><br />Ejemplo: 1234.5678|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, los valores 123,45 y sería -123,45 se convierten en 1.|  
  
### <a name="decimal-data-type"></a>Tipo de datos decimal  
En la tabla siguiente define las reglas para cargar los valores literales en una columna de tipo **decimal** (*p, s*). Reglas de conversión de datos son los mismos que para SQL Server. Para obtener más información, consulte [conversión de tipos de datos (motor de base de datos)](https://go.microsoft.com/fwlink/?LinkId=202128) en MSDN.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|  
|-------------------|-----------------------|  
|Literal entero|321312313123|  
|Literal decimal|123344.34455|  
  
### <a name="float-and-real-data-types"></a>Tipos de datos float y real  
En la tabla siguiente define las reglas para cargar los valores literales en una columna de tipo **float** o **real**. Reglas de conversión de datos son los mismos que para SQL Server. Para obtener más información, consulte [conversión de tipos de datos (motor de base de datos)](../t-sql/data-types/data-type-conversion-database-engine.md) en MSDN.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|  
|-------------------|-----------------------|  
|Literal entero|321312313123|  
|Literal decimal|123344.34455|  
|Literal de punto flotante|3.12323E+14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>int, bigint, tinyint, smallint los tipos de datos  
En la tabla siguiente define las reglas para cargar los valores literales en una columna de tipo **int**, **bigint**, **tinyint**, o **smallint**. El origen de datos no puede superar el intervalo permitido para el tipo de datos determinado. Por ejemplo, el intervalo para **tinyint** es de 0 a 255 y el intervalo de **int** es de -2.147.483.648 a 2.147.483.647.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipos de datos enteros|  
|-------------------|-----------------------|------------------------------------|  
|Literal entero|321312313123||  
|Literal decimal|123344.34455|Se truncan los valores a la derecha del separador decimal.|  
  
### <a name="money-and-smallmoney-data-types"></a>Tipos de datos Money y smallmoney  
Valores literales dinero se representan como una cadena de números con un separador decimal opcional y un símbolo de moneda opcionales como prefijo. El origen de datos no puede superar el intervalo permitido para el tipo de datos determinado. Por ejemplo, el intervalo para **smallmoney** es-214.748,3648 y 214.748,3647 y el intervalo para **dinero** es -922.337.203.685.477,5808 y 922.337.203.685.477,5807. En la tabla siguiente define las reglas para cargar los valores literales en una columna de tipo **dinero** o **smallmoney**.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a money o smallmoney, tipo de datos|  
|-------------------|-----------------------|-----------------------------------------------|  
|Literal entero|321312|Falta de dígitos después del separador decimal se establecen en 0 cuando se inserta el valor. Por ejemplo, se inserta el literal 12345 como 12345.0000|  
|Literal decimal|123344.34455|Si el número de dígitos después del punto decimal supera los 4, el valor se redondea al valor más cercano. Por ejemplo, se inserta el valor 123344.34455 como 123344.3446.|  
|Literal Money|$123456.7890|No se inserta el símbolo de moneda con el valor.<br /><br />Si el número de dígitos después del punto decimal supera los 4, el valor se redondea al valor más cercano.|  
  
## <a name="InsertStringTypes"></a>Insertar literales en tipos de cadena  
Las tablas siguientes definen las reglas predeterminadas de conversión y formato para cargar un valor literal en una columna de PDW de SQL Server que usa un tipo de cadena.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>Tipos de datos char, varchar, nchar y nvarchar  
La siguiente tabla define el formato predeterminado y las reglas para cargar los valores literales en una columna de tipo **char**, **varchar**, **nchar** y **nvarchar** . La longitud del origen de datos no puede superar el tamaño especificado para el tipo de datos. Si la longitud del origen de datos es menor que el tamaño de la **char** o **nchar** tipo de datos, los datos se rellenan a la derecha con espacios en blanco para alcanzar el tamaño del tipo de datos.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipos de datos de caracteres|  
|---------------|-------------------|----------------------------------|  
|Literal de cadena|Formato: 'cadena de caracteres'<br /><br />Ejemplo: 'abc'| N/D |  
|Literal de cadena Unicode|Formato: Cadena N'character'<br /><br />Ejemplo: Abc '| N/D |  
|Literal entero|Formato: ffffffffffn<br /><br />Ejemplo: 321312313123| N/D |  
|Literal decimal|Formato: ffffff.fffffff<br /><br />Ejemplo: 12344.34455| N/D |  
|Literal Money|Format: $ffffff.fffnn<br /><br />Ejemplo: $123456.99|El símbolo de moneda opcionales no se inserta con el valor. Para insertar el símbolo de moneda, insertar ese valor como un literal de cadena. Esto hará coincidir el formato del cargador, que trata todos los literales como un literal de cadena.<br /><br />No se permiten las comas.<br /><br />Si el número de dígitos después del punto decimal supera los 2, el valor se redondea al valor más cercano. Por ejemplo, se inserta el valor 123.946789 como 123.95.<br /><br />Se permite solo el estilo predeterminado de 0 (sin separadores de millar y 2 dígitos después del separador decimal) cuando se usa la función CONVERT para insertar literales de dinero.|  
  
### <a name="general-remarks"></a>Notas generales  
**dwloader** realiza las mismas conversiones implícitas que realiza SMP de SQL Server, pero no admite todas las conversiones implícitas que admite SQL Server de SMP.  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
