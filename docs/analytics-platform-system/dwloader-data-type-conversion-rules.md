---
title: Reglas de conversión de tipos de datos Dwloader
description: En este tema se describen los formatos de datos de entrada y las conversiones de tipos de datos implícitos que admite el cargador de línea de comandos de dwloader cuando carga datos en el almacenamiento de datos paralelos (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fe5d8790b5adb8477c994d265f458cdb1ceda61a
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401178"
---
# <a name="data-type-conversion-rules-for-dwloader---parallel-data-warehouse"></a>Reglas de conversión de tipos de datos para dwloader-almacenamiento de datos paralelos
En este tema se describen los formatos de datos de entrada y las conversiones de tipos de datos implícitos que admite el [cargador de línea de comandos de dwloader](dwloader.md) cuando carga datos en PDW. Las conversiones de datos implícitas se producen cuando los datos de entrada no coinciden con el tipo de datos de la PDW de SQL Server tabla de destino. Use esta información al diseñar el proceso de carga para asegurarse de que los datos se cargarán correctamente en PDW de SQL Server.  
   
  
## <a name="InsertBinaryTypes"></a>Insertar literales en tipos binarios  
En la tabla siguiente se definen los tipos literales aceptados, el formato y las reglas de conversión para cargar un valor literal en una PDW de SQL Server columna de tipo **Binary** (*n*) o **varbinary**(*n*).  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos binary o varbinary|  
|-------------------|-----------------------|-----------------------------------------------|  
|Literal binario|sean *hexidecimal_string*<br /><br />Ejemplo: 12Ef o 0x12Ef|El prefijo 0x es opcional.<br /><br />La longitud del origen de datos no puede superar el número de bytes especificado para el tipo de datos.<br /><br />Si la longitud del origen de datos es menor que el tamaño del tipo de datos **binarios** , los datos se rellenan a la derecha con ceros para alcanzar el tamaño del tipo de datos.|  
  
## <a name="InsertDateTimeTypes"></a>Insertar literales en tipos de fecha y hora  
Los literales de fecha y hora se representan mediante literales de cadena en formatos específicos, entre comillas simples. En las tablas siguientes se definen los tipos de literales, el formato y las reglas de conversión permitidos para cargar un literal de fecha u hora en una columna de tipo **DateTime**, **smalldatetime**, **Date**, **Time**, **DateTimeOffset**o **datetime2**. Las tablas definen el formato predeterminado para el tipo de datos especificado. Otros formatos que se pueden especificar se definen en la sección [formatos de fecha y hora](#DateFormats). Los literales de fecha y hora no pueden incluir espacios iniciales ni finales. los valores **Date**, **smalldatetime**y NULL no se pueden cargar en el modo de ancho fijo.  
  
### <a name="datetime-data-type"></a>Tipo de datos datetime  
En la tabla siguiente se definen el formato y las reglas predeterminadas para cargar valores literales en una columna de tipo **DateTime**. Una cadena vacía (' ') se convierte en el valor predeterminado ' 1900-01-01 12:00:00.000 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos DateTime|  
|-------------------|-----------------------|------------------------------------|  
|Literal de cadena en formato de **fecha y hora**|' AAAA-MM-DD HH: mm: SS [. FFF] '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123 '|Los dígitos fraccionarios que faltan se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35 ' se inserta como ' 2007-05-08 12:35:00.000 '.|  
|Literal de cadena en formato **smalldatetime**|' AAAA-MM-DD HH: mm '<br /><br />Ejemplo: ' 2007-05-08 12:35 '|Los segundos y los dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena en formato de **fecha**|' AAAA-MM-DD '<br /><br />Ejemplo: ' 2007-05-08 '|Los valores de hora (horas, minutos, segundos y fracciones) se establecen en 12:00:00.000 cuando se inserta el valor.|  
|Literal de cadena en formato **datetime2**|' AAAA-MM-DD HH: mm: SS. FFFFFFF '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567 '|Los datos de origen no pueden superar los tres dígitos fraccionarios. Por ejemplo, se insertará el literal ' 2007-05-08 12:35:29.123 ', pero el valor ' 2007-05-8 12:35:29.1234567 ' genera un error.|  
  
### <a name="smalldatetime-data-type"></a>Tipo de datos smalldatetime  
En la tabla siguiente se definen el formato y las reglas predeterminadas para cargar valores literales en una columna de tipo **smalldatetime**. Una cadena vacía (' ') se convierte en el valor predeterminado ' 1900-01-01 12:00 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos smalldatetime|  
|-------------------|-----------------------|-----------------------------------------|  
|Literal de cadena en formato **smalldatetime**|' AAAA-MM-DD HH: mm ' o ' AAAA-MM-DD HH: mm: SS '<br /><br />Ejemplo: "2007-05-08 12:00" o "2007-05-08 12:00:15"|Los datos de origen deben tener valores para año, mes, fecha, hora y minuto. Los segundos son opcionales y, si están presentes, se deben establecer en el valor 00. Cualquier otro valor genera un error.<br /><br />Los segundos son opcionales. Cuando se carga en una columna smalldatetime, dwloader redondeará los segundos y las fracciones de segundo. Por ejemplo, 1999-01-05 20:10:35.123 se cargará como 01-05 20:11.|  
|Literal de cadena en formato de **fecha**|' AAAA-MM-DD '<br /><br />Ejemplo: ' 2007-05-08 '|Los valores de hora (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor.|  
  
### <a name="date-data-type"></a>Tipo de datos date  
En la tabla siguiente se definen el formato y las reglas predeterminadas para cargar valores literales en una columna de tipo **Date**. Una cadena vacía (' ') se convierte en el valor predeterminado ' 1900-01-01 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos Date|  
|-------------------|-----------------------|--------------------------------|  
|Literal de cadena en formato de **fecha**|' AAAA-MM-DD '<br /><br />Ejemplo: ' 2007-05-08 '||  
  
### <a name="time-data-type"></a>Time (tipo de datos)  
En la tabla siguiente se definen el formato y las reglas predeterminadas para cargar valores literales en una columna de tipo **Time**. Una cadena vacía (' ') se convierte en el valor predeterminado ' 00:00:00.0000 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos Time|  
|-------------------|-----------------------|--------------------------------|  
|Literal de cadena en formato de **hora**|' HH: mm: SS. FFFFFFF '<br /><br />Ejemplo: "12:35:29.1234567"|Si el origen de datos tiene una precisión menor o igual (número de dígitos fraccionarios) que la precisión del tipo de datos **Time** , los datos se rellenan a la derecha con ceros. Por ejemplo, un valor literal "12:35:29.123" se inserta como "12:35:29.1230000".|  
  
### <a name="datetimeoffset-data-type"></a>DateTimeOffset (tipo de datos)  
En la tabla siguiente se definen el formato y las reglas predeterminadas para cargar valores literales en una columna de tipo **DateTimeOffset** (*n*). El formato predeterminado es "AAAA-MM-DD HH: mm: SS. FFFFFFF {+ |-} HH: mm". Una cadena vacía (' ') se convierte en el valor predeterminado ' 1900-01-01 12:00:00.0000000 + 00:00 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error. El número de dígitos fraccionarios depende de la definición de la columna. Por ejemplo, una columna definida como **DateTimeOffset** (2) tendrá dos dígitos fraccionarios.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos DateTimeOffset|  
|-------------------|-----------------------|------------------------------------------|  
|Literal de cadena en formato de **fecha y hora**|' AAAA-MM-DD HH: mm: SS [. FFF] '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123 '|Los dígitos fraccionarios que faltan y los valores de desplazamiento se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 12:35:29.123 ' se inserta como ' 2007-05-08 12:35:29.1230000 + 00:00 '.|  
|Literal de cadena en formato **smalldatetime**|' AAAA-MM-DD HH: mm '<br /><br />Ejemplo: ' 2007-05-08 12:35 '|Segundos, los dígitos fraccionarios restantes y los valores de desplazamiento se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena en formato de **fecha**|' AAAA-MM-DD '<br /><br />Ejemplo: ' 2007-05-08 '|Los valores de hora (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 ' se inserta como ' 2007-05-08 00:00:00.0000000 + 00:00 '.|  
|Literal de cadena en formato **datetime2**|' AAAA-MM-DD HH: mm: SS. FFFFFFF '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567 '|Los datos de origen no pueden superar el número especificado de fracciones de segundo en la columna DateTimeOffset. Si el origen de datos tiene un número menor o igual de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es DateTimeOffset (5), se inserta el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' como ' 12:35:29.12300 + 12:15 '.|  
|Literal de cadena en formato **DateTimeOffset**|' AAAA-MM-DD HH: mm: SS. FFFFFFF {+&#124;-} HH: mm '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567 + 12:15 '|Los datos de origen no pueden superar el número especificado de fracciones de segundo en la columna DateTimeOffset. Si el origen de datos tiene un número menor o igual de fracciones de segundo, los datos se rellenan a la derecha con ceros. Por ejemplo, si el tipo de datos es DateTimeOffset (5), se inserta el valor literal ' 2007-05-08 12:35:29.123 + 12:15 ' como ' 12:35:29.12300 + 12:15 '.|  
  
### <a name="datetime2-data-type"></a>Tipo de datos datetime2  
En la tabla siguiente se definen el formato y las reglas predeterminadas para cargar valores literales en una columna de tipo **datetime2** (*n*). El formato predeterminado es ' AAAA-MM-DD HH: mm: SS. FFFFFFF '. Una cadena vacía (' ') se convierte en el valor predeterminado ' 1900-01-01 12:00:00 '. Las cadenas que solo contienen espacios en blanco (' ') generan un error. El número de dígitos fraccionarios depende de la definición de la columna. Por ejemplo, una columna definida como **datetime2** (2) tendrá dos dígitos fraccionarios.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos datetime2|  
|-------------------|-----------------------|-------------------------------------|  
|Literal de cadena en formato de **fecha y hora**|' AAAA-MM-DD HH: mm: SS [. FFF] '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.123 '|Las fracciones de segundo son opcionales y se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena en formato **smalldatetime**|' AAAA-MM-DD HH: mm '<br /><br />Ejemplo: ' 2007-05-08 12 '|Los segundos opcionales y los dígitos fraccionarios restantes se establecen en 0 cuando se inserta el valor.|  
|Literal de cadena en formato de **fecha**|' AAAA-MM-DD '<br /><br />Ejemplo: ' 2007-05-08 '|Los valores de hora (horas, minutos, segundos y fracciones) se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal ' 2007-05-08 ' se inserta como ' 2007-05-08 12:00:00.0000000 '.|  
|Literal de cadena en formato **datetime2**|' AAAA-MM-DD HH: mm: SS: FFFFFFF '<br /><br />Ejemplo: ' 2007-05-08 12:35:29.1234567 '|Si el origen de datos contiene componentes de datos y de hora que son menores o iguales que el valor especificado en **datetime2**(*n*), se insertan los datos; en caso contrario, se genera un error.|  
  
### <a name="DateFormats"></a>Formatos de fecha y hora  
Dwloader admite los siguientes formatos de datos para los datos de entrada que se cargan en PDW de SQL Server. Después de la tabla, se muestran más detalles.  
  
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
  
-   Para especificar el mes como texto, use tres o más caracteres. Los meses con 1 o 2 caracteres se interpretarán como un número.  
  
-   Para separar los valores de hora, use el símbolo ': '.  
  
-   Las letras entre corchetes son opcionales.  
  
-   Las letras "tt" designan [a.m. | p.m.]. a.m. es el valor predeterminado. Cuando se especifica 'tt', el valor de hora (hh) debe estar comprendido entre 0 y 12.  
  
-   Las letras 'zzz' designan el desfase de zona horaria de la zona horaria actual del sistema en el formato {+|-}HH:ss].  
  
## <a name="InsertNumerictypes"></a>Insertar literales en tipos numéricos  
En las tablas siguientes se definen el formato y las reglas de conversión predeterminados para cargar un valor literal en una columna de PDW de SQL Server que utiliza un tipo numérico.  
  
### <a name="bit-data-type"></a>bit (tipo de datos)  
En la tabla siguiente se definen el formato y las reglas predeterminadas para cargar valores literales en una columna de tipo **bit**. Una cadena vacía (' ') o una cadena que solo contenga espacios en blanco (' ') se convierten en 0.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos bit|  
|-------------------|-----------------------|-------------------------------|  
|Literal de cadena en formato de **entero**|'ffffffffff'<br /><br />Ejemplo: ' 1 ' o ' 321 '|Un valor entero con formato de literal de cadena no puede contener un valor negativo. Por ejemplo, el valor "-123" genera un error.<br /><br />Un valor mayor que 1 se convierte en 1. Por ejemplo, el valor "123" se convierte en 1.|  
|Literal de cadena|' TRUE ' o ' FALSE '<br /><br />Ejemplo: "true"|El valor "TRUE" se convierte en 1; el valor "FALSE" se convierte en 0.|  
|Literal entero|fffffffn<br /><br />Ejemplo: 1 o 321|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, los valores 123 y-123 se convierten en 1.|  
|Literal decimal|fffnn.fffn<br /><br />Ejemplo: 1234,5678|Un valor mayor que 1 o menor que 0 se convierte en 1. Por ejemplo, los valores 123,45 y-123,45 se convierten en 1.|  
  
### <a name="decimal-data-type"></a>decimal (tipo de datos)  
En la tabla siguiente se definen las reglas para cargar valores literales en una columna de tipo **decimal** (*p, s*). Las reglas de conversión de datos son las mismas que para SQL Server. Para obtener más información, vea [conversión de tipos de datos (motor de base de datos)](https://go.microsoft.com/fwlink/?LinkId=202128) en MSDN.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|  
|-------------------|-----------------------|  
|Literal entero|321312313123|  
|Literal decimal|123344,34455|  
  
### <a name="float-and-real-data-types"></a>Tipos de datos float y real  
En la tabla siguiente se definen las reglas para cargar valores literales en una columna de tipo **float** o **real**. Las reglas de conversión de datos son las mismas que para SQL Server. Para obtener más información, vea [conversión de tipos de datos (motor de base de datos)](../t-sql/data-types/data-type-conversion-database-engine.md) en MSDN.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|  
|-------------------|-----------------------|  
|Literal entero|321312313123|  
|Literal decimal|123344,34455|  
|Literal de punto flotante|3.12323 e + 14|  
  
### <a name="int-bigint-tinyint-smallint-data-types"></a>Tipos de datos int, bigint, tinyint, smallint  
En la tabla siguiente se definen las reglas para cargar valores literales en una columna de tipo **int**, **BIGINT**, **tinyint**o **smallint**. El origen de datos no puede superar el intervalo permitido para el tipo de datos especificado. Por ejemplo, el intervalo de **tinyint** es 0 a 255 y el intervalo para **int** es-2.147.483.648 a 2.147.483.647.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipos de datos enteros|  
|-------------------|-----------------------|------------------------------------|  
|Literal entero|321312313123||  
|Literal decimal|123344,34455|Los valores a la derecha del separador decimal se truncan.|  
  
### <a name="money-and-smallmoney-data-types"></a>Tipos de datos Money y smallmoney  
Los valores literales de moneda se representan como una cadena de números con un separador decimal opcional y un símbolo de divisa opcional como prefijo. El origen de datos no puede superar el intervalo permitido para el tipo de datos especificado. Por ejemplo, el intervalo para **smallmoney** es-214.748,3648 a 214.748,3647 y el intervalo para **money** es-922.337.203.685.477,5808 a 922.337.203.685.477,5807. En la tabla siguiente se definen las reglas para cargar valores literales en una columna de tipo **Money** o **smallmoney**.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión al tipo de datos Money o smallmoney|  
|-------------------|-----------------------|-----------------------------------------------|  
|Literal entero|321312|Los dígitos que faltan después del separador decimal se establecen en 0 cuando se inserta el valor. Por ejemplo, el literal 12345 se inserta como 12345,0000|  
|Literal decimal|123344,34455|Si el número de dígitos después del separador decimal es superior a 4, el valor se redondea al valor más próximo. Por ejemplo, el valor 123344,34455 se inserta como 123344,3446.|  
|Literal de moneda|$123456,7890|El símbolo de moneda no se inserta con el valor.<br /><br />Si el número de dígitos después del separador decimal es superior a 4, el valor se redondea al valor más próximo.|  
  
## <a name="InsertStringTypes"></a>Insertar literales en tipos de cadena  
En las tablas siguientes se definen el formato y las reglas de conversión predeterminados para cargar un valor literal en una columna de PDW de SQL Server que utiliza un tipo de cadena.  
  
### <a name="char-varchar-nchar-and-nvarchar-data-types"></a>Tipos de datos char, VARCHAR, nchar y nvarchar  
En la tabla siguiente se definen el formato y las reglas predeterminadas para cargar valores literales en una columna de tipo **Char**, **VARCHAR**, **nchar** y **nvarchar**. La longitud del origen de datos no puede superar el tamaño especificado para el tipo de datos. Si la longitud del origen de datos es menor que el tamaño del tipo de datos **Char** o **nchar** , los datos se rellenan a la derecha con espacios en blanco para alcanzar el tamaño del tipo de datos.  
  
|Tipo de datos de entrada|Ejemplos de datos de entrada|Conversión a tipos de datos de caracteres|  
|---------------|-------------------|----------------------------------|  
|Literal de cadena|Formato: ' cadena de caracteres '<br /><br />Ejemplo: ' ABC '| N/D |  
|Literal de cadena Unicode|Formato: N'character cadena '<br /><br />Ejemplo: N'abc '| N/D |  
|Literal entero|Formato: ffffffffffn<br /><br />Ejemplo: 321312313123| N/D |  
|Literal decimal|Formato: FFFFFF. FFFFFFF<br /><br />Ejemplo: 12344,34455| N/D |  
|Literal de moneda|Formato: $ffffff. fffnn<br /><br />Ejemplo: $123456,99|El símbolo de divisa opcional no se inserta con el valor. Para insertar el símbolo de moneda, inserte el valor como un literal de cadena. Esto coincidirá con el formato del cargador, que trata todos los literales como un literal de cadena.<br /><br />No se permiten comas.<br /><br />Si el número de dígitos después del separador decimal es superior a 2, el valor se redondea al valor más próximo. Por ejemplo, el valor 123,946789 se inserta como 123,95.<br /><br />Solo se permite el estilo predeterminado 0 (sin comas y 2 dígitos después del separador decimal) cuando se usa la función CONVERT para insertar literales monetarios.|  
  
### <a name="general-remarks"></a>Notas generales  
**dwloader** realiza las mismas conversiones implícitas que realiza SMP SQL Server, pero no admite todas las conversiones implícitas que admite SMP SQL Server.  
 
<!-- MISSING LINKS 
## See Also  
[Grant Permissions to Load Data &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-load-data-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  

-->
  
