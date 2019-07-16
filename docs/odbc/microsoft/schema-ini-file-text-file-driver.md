---
title: Archivo Schema.ini (controlador de archivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd95329c91c69af38b1ffc7951191498fcc40479
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987948"
---
# <a name="schemaini-file-text-file-driver"></a>Archivo Schema.ini (controlador de archivo de texto)
Cuando se usa el controlador de texto, el formato del archivo de texto se determina mediante el uso de un archivo de información de esquema. El archivo de información de esquema es siempre denominado Schema.ini y siempre se mantiene en el mismo directorio que el origen de datos de texto. El archivo de información de esquema proporciona la IISAM con información sobre el formato general del archivo, el nombre de columna y la información de tipo de datos y varias otras características de datos. Un archivo Schema.ini siempre es necesario para tener acceso a datos de longitud fija. Debe usar un archivo Schema.ini cuando la tabla de texto contiene la fecha y hora, moneda, o datos Decimal o siempre que desee más control sobre la administración de los datos en la tabla.  
  
> [!NOTE]  
>  El texto de ISAM obtendrá los valores iniciales desde el registro, pero no desde Schema.ini. El mismo formato de archivo predeterminado se aplica a todas las tablas de datos de texto nuevo. Todos los archivos creados por la instrucción CREATE TABLE heredan esos mismos valores de formato predeterminado, que se establecen mediante la selección de valores de formato de archivo en el **Definir formato de texto** cuadro de diálogo con \<predeterminado > elegido en el  **Las tablas** lista. Si los valores del registro difieren de los valores de Schema.ini, se sobrescribirán los valores en el registro por los valores de Schema.ini.  
  
## <a name="understanding-schemaini-files"></a>Descripción de los archivos de Schema.ini  
 Archivos de Schema.ini proporcionan información acerca de los registros en un archivo de texto del esquema. Cada entrada Schema.ini especifica uno de cinco características de la tabla:  
  
-   El nombre de archivo de texto  
  
-   El formato de archivo  
  
-   Los nombres de campo, ancho y tipos  
  
-   El juego de caracteres  
  
-   Conversiones de tipos de datos especiales  
  
 Las secciones siguientes tratan estas características.  
  
## <a name="specifying-the-file-name"></a>Especifica el nombre de archivo  
 La primera entrada de Schema.ini siempre es el nombre del archivo de origen de texto entre corchetes. El ejemplo siguiente muestra la entrada para el archivo Sample.txt:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Especifica el formato de archivo  
 El **formato** opción en Schema.ini especifica el formato del archivo de texto. El IISAM de texto puede leer el formato automáticamente desde archivos más delimitados por caracteres. Puede usar cualquier carácter individual como un delimitador en el archivo, excepto las comillas dobles ("). El **formato** configuración de Schema.ini reemplaza la configuración en el registro de Windows, el archivo por archivo. La tabla siguiente enumeran los valores válidos para el **formato** opción.  
  
|Especificador de formato|Formato de tabla|En la instrucción Schema.ini Format|  
|----------------------|------------------|---------------------------------|  
|**Delimitado por tabulaciones**|Campos en el archivo están delimitados por tabulaciones.|Formato = TabDelimited|  
|**COMAS**|Campos en el archivo están delimitados por comas (valores separados por comas).|Formato = CSVDelimited|  
|**Personalizado**|Campos en el archivo se delimitan mediante cualquier carácter que se elija para introducir en el cuadro de diálogo. Todos excepto las comillas dobles (") se permiten, incluidos en blanco.|Formato = delimitado (*carácter personalizado*)<br /><br /> -o bien-<br /><br /> Sin delimitador especificado:<br /><br /> Formato = delimitado (de)|  
|**Longitud fija**|Son campos en el archivo de longitud fija.|Format=FixedLength|  
  
## <a name="specifying-the-fields"></a>Especificar los campos  
 Puede especificar los nombres de campo en un archivo de texto delimitado por el carácter de dos maneras:  
  
-   Incluya los nombres de campo en la primera fila de la tabla y establezca **ColNameHeader** a **es True.**  
  
-   Especifique cada columna por número y designar el tipo de datos y el nombre de columna.  
  
 Debe especificar cada columna por número y designar el nombre de columna, tipo de datos y ancho para los archivos de longitud fija.  
  
> [!NOTE]  
>  El **ColNameHeader** en invalidaciones Schema.ini el **FirstRowHasNames** configuración en el registro de Windows, el archivo por archivo.  
  
 También se pueden determinar los tipos de datos de los campos. Use la **MaxScanRows** opción para indicar cuántas filas se deben examinar para determinar los tipos de columna. Si establece **MaxScanRows** en 0, se analiza todo el archivo. El **MaxScanRows** configuración de Schema.ini reemplaza la configuración en el registro de Windows, el archivo por archivo.  
  
 La entrada siguiente indica que Microsoft Jet debe utilizar los datos en la primera fila de la tabla para determinar los nombres de campo y debe examinar todo el archivo para determinar los datos de tipos que se usan:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 La entrada siguiente designa los campos de una tabla utilizando el número de columna (**Col**_n_) opción, que es opcional para archivos delimitados por caracteres y es necesario para los archivos de longitud fija. El ejemplo muestra las entradas de Schema.ini para dos campos, un campo de texto CustomerNumber de 10 caracteres y un campo de texto de 30 caracteres CustomerName:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 La sintaxis de **Col**_n_ es:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente describe cada parte de la **Col**_n_ entrada.  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*ColumnName*|El nombre de la columna de texto. Si el nombre de columna contiene espacios incrustados, debe encerrarlo entre comillas dobles.|  
|*type*|Tipos de datos son los siguientes:<br /><br /> **Tipos de datos Microsoft Jet**<br /><br /> Bit<br /><br /> Byte<br /><br /> Breve<br /><br /> long<br /><br /> Currency<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Text<br /><br /> Memorándum<br /><br /> **Tipos de datos ODBC** Char (igual que el texto)<br /><br /> Float (igual que Double)<br /><br /> Entero (igual que Short)<br /><br /> LongChar (igual que Memo)<br /><br /> Fecha *formato de fecha*|  
|**Width**|El valor de cadena literal `Width`. Indica que el número siguiente designa el ancho de la columna (opcional para archivos delimitados por caracteres; necesario para los archivos de longitud fija).|  
|*#*|El valor entero que designa el ancho de la columna (obligatorio si **ancho** se especifica).|  
  
## <a name="selecting-a-character-set"></a>Seleccionar un juego de caracteres  
 Puede seleccionar entre dos conjuntos de caracteres: ANSI y OEM. El **CharacterSet** configuración de Schema.ini reemplaza la configuración en el registro de Windows, el archivo por archivo. El ejemplo siguiente muestra la entrada de Schema.ini que establece el juego de caracteres que ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Especificar formatos de tipo de datos y conversiones  
 El archivo Schema.ini contiene varias opciones que puede usar para especificar cómo se puede convertir o muestra los datos. La tabla siguiente muestra cada una de estas opciones.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**DateTimeFormat**|Puede establecerse en una cadena de formato que indica las fechas y horas. Debe especificar esta entrada si se administran todos los campos de fecha y hora en la importación y exportación con el mismo formato. Todos los formatos de Microsoft Jet excepto a. M. y p. M. se admiten. Si no hay ninguna cadena de formato, se usan las opciones de imagen y la hora de fecha corta de Panel de Control de Windows.|  
|**DecimalSymbol**|Puede establecerse en cualquier carácter individual que se usa para separar el entero de la parte fraccionaria de un número.|  
|**NumberDigits**|Indica el número de dígitos decimales en la parte fraccionaria de un número.|  
|**NumberLeadingZeros**|Especifica si un valor decimal inferior a 1 y -más de 1 debe contener ceros; Este valor puede ser cualquiera (sin ceros) False o True.|  
|**CurrencySymbol**|Indica el símbolo de moneda que se puede usar para los valores de moneda en el archivo de texto. Algunos ejemplos son el signo de dólar ($) y minería de datos.|  
|**CurrencyPosFormat**|Se puede establecer en cualquiera de los siguientes valores:<br /><br /> -Prefijo de símbolo de moneda sin separación ($1)<br />-Sufijo de símbolo de moneda sin separación (1$)<br />-Prefijo de símbolo de moneda con separación de un carácter ($ 1)<br />-Sufijo con separación de un carácter de símbolo de moneda (1 $)|  
|**CurrencyDigits**|Especifica el número de dígitos utilizados para la parte fraccionaria de un importe de divisa.|  
|**CurrencyNegFormat**|Puede presentar uno de los siguientes valores:<br /><br /> -   ($1)<br />-   -$1<br />-   $-1<br />-$1:<br />-   (1$)<br />--1$<br />-1$<br />-$- de 1<br />--1 $<br />--$ 1<br />-$- de 1<br />-$ 1:<br />-$ -1<br />-1 $<br />-   ($ 1)<br />-   (1 $)<br /><br /> En este ejemplo se muestra el signo de dólar, pero se debe reemplazar con los valores adecuados **CurrencySymbol** valor en el programa real.|  
|**CurrencyThousandSymbol**|Indica el símbolo de carácter único que puede usarse para separar los valores de moneda en el archivo de texto miles.|  
|**CurrencyDecimalSymbol**|Puede establecerse en cualquier carácter individual que se usa para separar la totalidad de la parte fraccionaria de un importe de divisa.|  
  
> [!NOTE]  
>  Si se omite una entrada, se usa el valor predeterminado en el Panel de Control de Windows.
