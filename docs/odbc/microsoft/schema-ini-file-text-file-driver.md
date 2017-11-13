---
title: El archivo Schema.ini (controlador de archivo de texto) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 709df0de2e0191c0f03026afdad7b8e9b8480cae
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="schemaini-file-text-file-driver"></a>Archivo Schema.ini (controlador de archivo de texto)
Cuando se utiliza el controlador de texto, el formato del archivo de texto se determina mediante un archivo de información de esquema. El archivo de información de esquema es siempre denominado Schema.ini y se mantiene siempre en el mismo directorio que el origen de datos de texto. El archivo de información de esquema proporciona el IISAM con información sobre el formato general del archivo, el nombre de columna y la información de tipo de datos y varias otras características de datos. Un archivo Schema.ini siempre es necesario para tener acceso a datos de longitud fija. Debe utilizar un archivo Schema.ini cuando la tabla de texto contiene la fecha y hora, moneda, o datos Decimal o siempre que desee más control sobre el tratamiento de los datos de la tabla.  
  
> [!NOTE]  
>  El ISAM de texto obtendrá los valores iniciales del registro, no de Schema.ini. El mismo formato de archivo predeterminado se aplica a todas las tablas de datos de texto nuevo. Todos los archivos creados por la instrucción CREATE TABLE heredan los mismos valores de formato predeterminado, que se establecen mediante la selección de valores de formato de archivo en el **Definir formato de texto** cuadro de diálogo con \<predeterminado > elegido en el  **Tablas** lista. Si los valores del registro difieren de los valores de Schema.ini, los valores de Schema.ini sobrescribirá los valores en el registro.  
  
## <a name="understanding-schemaini-files"></a>Descripción de los archivos de Schema.ini  
 Archivos de Schema.ini proporcionan información del esquema acerca de los registros en un archivo de texto. Cada entrada de Schema.ini especifica uno de los cinco características de la tabla:  
  
-   El nombre de archivo de texto  
  
-   El formato de archivo  
  
-   Los nombres de campo, ancho y tipos  
  
-   El juego de caracteres  
  
-   Conversiones de tipos de datos especiales  
  
 Las secciones siguientes tratan estas características.  
  
## <a name="specifying-the-file-name"></a>Especifica el nombre de archivo  
 La primera entrada de Schema.ini siempre es el nombre del archivo de origen de texto entre corchetes. En el ejemplo siguiente se muestra la entrada para el archivo Sample.txt:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Especificar el formato de archivo  
 El **formato** opción en Schema.ini especifica el formato del archivo de texto. Los IISAM de texto puede leer el formato automáticamente de archivos más delimitada por un carácter. Puede usar cualquier carácter individual como un delimitador en el archivo, excepto las comillas dobles ("). El **formato** configuración de Schema.ini reemplaza la configuración en el registro de Windows, por cada archivo. En la tabla siguiente se enumera los valores válidos para la **formato** opción.  
  
|Especificador de formato|Formato de tabla|Instrucción de formato Schema.ini|  
|----------------------|------------------|---------------------------------|  
|**Delimitado por tabulaciones**|Campos en el archivo están delimitados por tabulaciones.|Formato = TabDelimited|  
|**CSV delimitado**|Campos en el archivo están delimitados por comas (valores separados por comas).|Formato = CSVDelimited|  
|**Personalizado**|Campos en el archivo se delimitan mediante cualquier carácter que se elija para introducir en el cuadro de diálogo. Todas excepto las comillas dobles (") se permiten, incluidos en blanco.|Formato = delimitado (*carácter personalizado*)<br /><br /> -O bien-<br /><br /> Sin delimitador especificado:<br /><br /> Formato = delimitado)|  
|**Longitud fija**|Campos en el archivo son de longitud fija.|Formato = FixedLength|  
  
## <a name="specifying-the-fields"></a>Especifica los campos  
 Puede especificar nombres de campo en un archivo de texto delimitado por el carácter de dos maneras:  
  
-   Incluya los nombres de campo en la primera fila de la tabla y establezca **ColNameHeader** a **es True.**  
  
-   Especificar cada columna por número y designar el tipo de datos y el nombre de columna.  
  
 Debe especificar cada columna por número y designar el nombre de columna, el tipo de datos y el ancho para los archivos de longitud fija.  
  
> [!NOTE]  
>  El **ColNameHeader** configuración de invalidaciones de Schema.ini el **FirstRowHasNames** del registro de Windows, por cada archivo.  
  
 También se pueden determinar los tipos de datos de los campos. Use la **MaxScanRows** opción para indicar el número de filas se debe examinar para determinar los tipos de columna. Si establece **MaxScanRows** en 0, se analiza el archivo completo. El **MaxScanRows** configuración de Schema.ini reemplaza la configuración en el registro de Windows, por cada archivo.  
  
 La entrada siguiente indica que Microsoft Jet debe usar los datos de la primera fila de la tabla para determinar los nombres de campo y debe examinar todo el archivo para determinar los datos de tipos que se utilizan:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 La entrada siguiente designa campos de una tabla con el número de columna (**Col***n*) opción, que es opcional para archivos delimitados por el carácter obligatorio para los archivos de longitud fija. El ejemplo muestra las entradas de Schema.ini para dos campos, un campo de texto de CustomerNumber de 10 caracteres y un campo de texto de 30 caracteres CustomerName:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 La sintaxis de **Col**  *n*  es:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente describe cada parte de la **Col**  *n*  entrada.  
  
|Parámetro|Description|  
|---------------|-----------------|  
|*ColumnName*|El nombre de la columna de texto. Si el nombre de columna contiene espacios en blanco incrustados, debe encerrarlo entre comillas dobles.|  
|*Tipo*|Tipos de datos son los siguientes:<br /><br /> **Tipos de datos de Microsoft Jet**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> Long<br /><br /> Moneda<br /><br /> Único<br /><br /> Doble<br /><br /> DateTime<br /><br /> Texto<br /><br /> Memorándum<br /><br /> **Tipos de datos ODBC** Char (igual que el texto)<br /><br /> Float (igual que Double)<br /><br /> Integer (igual que Short)<br /><br /> LongChar (igual que Memo)<br /><br /> Fecha *formato de fecha*|  
|**Ancho**|El valor de cadena literal `Width`. Indica que el número siguiente designa el ancho de la columna (opcional para archivos delimitados por el carácter; necesario para los archivos de longitud fija).|  
|*#*|El valor entero que indica el ancho de la columna (obligatorio si **ancho** se especifica).|  
  
## <a name="selecting-a-character-set"></a>Al seleccionar un juego de caracteres  
 Puede seleccionar entre dos conjuntos de caracteres: ANSI y OEM. El **CharacterSet** configuración de Schema.ini reemplaza la configuración en el registro de Windows, por cada archivo. En el ejemplo siguiente se muestra la entrada de Schema.ini que establece el juego de caracteres que ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Especificar formatos de tipo de datos y conversiones  
 El archivo Schema.ini contiene varias opciones que puede usar para especificar cómo se convierten o muestran los datos. La tabla siguiente enumera cada una de estas opciones.  
  
|Opción|Description|  
|------------|-----------------|  
|**DateTimeFormat**|Puede establecerse en una cadena de formato que indica las fechas y horas. Debe especificar esta entrada si todos los campos de fecha y hora de la importación y exportación se administran con el mismo formato. Todos los formatos de Microsoft Jet excepto a. M. y p. M. se admiten. Si no hay ninguna cadena de formato, se usan las opciones de imagen y la hora de fecha corta de Panel de Control de Windows.|  
|**DecimalSymbol**|Se puede establecer en cualquier carácter individual que se utiliza para separar el entero de la parte fraccionaria de un número.|  
|**NumberDigits**|Indica el número de dígitos decimales en la parte fraccionaria de un número.|  
|**NumberLeadingZeros**|Especifica si un valor decimal menor que 1 y más de – 1 debe contener ceros a la izquierda; Este valor puede ser False (sin ceros a la izquierda) o True.|  
|**CurrencySymbol**|Indica el símbolo de moneda que se puede usar para los valores de moneda en el archivo de texto. Algunos ejemplos son el signo de dólar ($) y minería de datos.|  
|**CurrencyPosFormat**|Puede establecerse en cualquiera de los siguientes valores:<br /><br /> -Prefijo de símbolo de moneda sin separación ($1)<br />-Sufijo de símbolo de moneda sin separación (1$)<br />-Prefijo de símbolo de moneda con separación de un carácter ($ 1)<br />-Sufijo de símbolo de moneda con separación de un carácter (1 $)|  
|**CurrencyDigits**|Especifica el número de dígitos que se usan para la parte fraccionaria de una cantidad de moneda.|  
|**CurrencyNegFormat**|Puede ser uno de los siguientes valores:<br /><br /> -   ($1)<br />-   –$1<br />-   $–1<br />-   $1–<br />-   (1$)<br />-   –1$<br />-   1–$<br />-   1$–<br />-   –1 $<br />-   –$ 1<br />-   1 $–<br />-   $ 1–<br />-   $ –1<br />-   1– $<br />-   ($ 1)<br />-   (1 $)<br /><br /> Este ejemplo muestra el signo de dólar, pero se debe reemplazar con el adecuado **CurrencySymbol** valor en el programa real.|  
|**CurrencyThousandSymbol**|Indica el símbolo de carácter único que puede usarse para separar los valores de moneda en el archivo de texto en miles.|  
|**CurrencyDecimalSymbol**|Se puede establecer en cualquier carácter individual que se utiliza para separar la totalidad de la parte fraccionaria de una cantidad de moneda.|  
  
> [!NOTE]  
>  Si se omite una entrada, se utiliza el valor predeterminado en el Panel de Control de Windows.

