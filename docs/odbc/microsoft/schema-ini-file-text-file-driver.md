---
title: Archivo Schema.ini (Controlador de archivo de texto) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365351724f27205e7d460c757f1268d042cefc76
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305516"
---
# <a name="schemaini-file-text-file-driver"></a>Archivo Schema.ini (controlador de archivo de texto)
Cuando se utiliza el controlador de texto, el formato del archivo de texto se determina mediante un archivo de información de esquema. El archivo de información de esquema siempre se denomina Schema.ini y siempre se mantiene en el mismo directorio que el origen de datos de texto. El archivo de información de esquema proporciona a IISAM información sobre el formato general del archivo, el nombre de columna y la información de tipo de datos, y varias otras características de datos. Un archivo Schema.ini siempre es necesario para tener acceso a datos de longitud fija. Debe usar un archivo Schema.ini cuando la tabla de texto contenga datos DateTime, Currency o Decimal, o en cualquier momento en el que desee tener más control sobre el control de los datos de la tabla.  
  
> [!NOTE]  
>  El ISAM de texto obtendrá los valores iniciales del registro, no de Schema.ini. El mismo formato de archivo predeterminado se aplica a todas las tablas de datos de texto nuevas. Todos los archivos creados por la instrucción CREATE TABLE heredan esos mismos valores de formato \<predeterminados, que se establecen seleccionando valores de formato de archivo en el cuadro de diálogo Definir formato de **texto** con el valor predeterminado> elegido en la lista **Tablas.** Si los valores del Registro difieren de los valores de Schema.ini, los valores del Registro se sobrescribirán con los valores de Schema.ini.  
  
## <a name="understanding-schemaini-files"></a>Comprender los archivos Schema.ini  
 Los archivos Schema.ini proporcionan información de esquema sobre los registros de un archivo de texto. Cada entrada Schema.ini especifica una de las cinco características de la tabla:  
  
-   El nombre del archivo de texto  
  
-   El formato de archivo  
  
-   Los nombres de campo, anchos y tipos  
  
-   El juego de caracteres  
  
-   Conversiones especiales de tipos de datos  
  
 En las secciones siguientes se describen estas características.  
  
## <a name="specifying-the-file-name"></a>Especificar el nombre de archivo  
 La primera entrada en Schema.ini siempre es el nombre del archivo de origen de texto entre corchetes. En el ejemplo siguiente se muestra la entrada del archivo Sample.txt:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Especificar el formato de archivo  
 La opción **Formato** de Schema.ini especifica el formato del archivo de texto. El IISAM de texto puede leer el formato automáticamente desde la mayoría de los archivos delimitados por caracteres. Puede utilizar cualquier carácter individual como delimitador en el archivo, excepto la comilla doble ("). El **valor Formato** de Schema.ini reemplaza la configuración del Registro de Windows, archivo por archivo. En la tabla siguiente se enumeran los valores válidos para la opción **Formato.**  
  
|Especificador de formato|Formato de tabla|Schema.ini Instrucción de formato|  
|----------------------|------------------|---------------------------------|  
|**Delimitado por pestañas**|Los campos del archivo están delimitados por pestañas.|Formato-TabDelimitado|  
|**CSV delimitado**|Los campos del archivo están delimitados por comas (valores separados por comas).|Formato-CSVDelimitado|  
|**Delimitado por la costumbre**|Los campos del archivo están delimitados por cualquier carácter que elija introducir en el cuadro de diálogo. Se permiten todas excepto las comillas dobles ("), incluido el espacio en blanco.|Formato-Delimitado *(carácter personalizado)*<br /><br /> o bien<br /><br /> Sin delimitador especificado:<br /><br /> Formato-Delimitado( )|  
|**Longitud fija**|Los campos del archivo tienen una longitud fija.|Formato-Longitud Fija|  
  
## <a name="specifying-the-fields"></a>Especificación de los campos  
 Puede especificar nombres de campo en un archivo de texto delimitado por caracteres de dos maneras:  
  
-   Incluya los nombres de campo en la primera fila de la tabla y establezca **ColNameHeader** en **True.**  
  
-   Especifique cada columna por número y designe el nombre de columna y el tipo de datos.  
  
 Debe especificar cada columna por número y designar el nombre de columna, el tipo de datos y el ancho de los archivos de longitud fija.  
  
> [!NOTE]  
>  El **ColNameHeader** configuración en Schema.ini reemplaza el **FirstRowHasNames** configuración en el registro de Windows, archivo por archivo.  
  
 También se pueden determinar los tipos de datos de los campos. Utilice la opción **MaxScanRows** para indicar cuántas filas se deben examinar al determinar los tipos de columna. Si establece **MaxScanRows** en 0, se analiza todo el archivo. El **valor MaxScanRows** en Schema.ini reemplaza la configuración del Registro de Windows, archivo por archivo.  
  
 La entrada siguiente indica que Microsoft Jet debe utilizar los datos de la primera fila de la tabla para determinar los nombres de campo y debe examinar todo el archivo para determinar los tipos de datos utilizados:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 La siguiente entrada designa campos en una tabla mediante la opción de número de columna (**Col**_n_), que es opcional para los archivos delimitados por caracteres y necesaria para los archivos de longitud fija. En el ejemplo se muestran las entradas Schema.ini para dos campos, un campo de texto CustomerNumber de 10 caracteres y un campo de texto CustomerName de 30 caracteres:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 La sintaxis de **Col**_n_ es:  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>Observaciones  
 En la tabla siguiente se describe cada parte de la entrada **Col**_n._  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*ColumnName*|El nombre de texto de la columna. Si el nombre de columna contiene espacios incrustados, debe incluirlo entre comillas dobles.|  
|*type*|Los tipos de datos son los siguientes:<br /><br /> **Tipos de datos de Microsoft Jet**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> long<br /><br /> Moneda<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Texto<br /><br /> Memorándum<br /><br /> **Tipos de datos ODBC** Carácter (igual que Texto)<br /><br /> Flotar (igual que Doble)<br /><br /> Entero (igual que Short)<br /><br /> LongChar (igual que Memo)<br /><br /> *Formato de fecha de fecha*|  
|**Width**|El valor `Width`de cadena literal . Indica que el número siguiente designa el ancho de la columna (opcional para archivos delimitados por caracteres; necesario para archivos de longitud fija).|  
|*#*|El valor entero que designa el ancho de la columna (obligatorio si se especifica **Width).**|  
  
## <a name="selecting-a-character-set"></a>Selección de un juego de caracteres  
 Puede seleccionar entre dos conjuntos de caracteres: ANSI y OEM. El **CharacterSet** configuración en Schema.ini reemplaza la configuración en el Registro de Windows, archivo por archivo. En el ejemplo siguiente se muestra la entrada Schema.ini que establece el juego de caracteres en ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Especificación de formatos de tipo de datos y conversiones  
 El archivo Schema.ini contiene varias opciones que puede utilizar para especificar cómo se convierten o muestran los datos. En la tabla siguiente se enumeran cada una de estas opciones.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**DateTimeFormat**|Se puede establecer en una cadena de formato que indique fechas y horas. Debe especificar esta entrada si todos los campos de fecha y hora de la importación/exportación se gestionan con el mismo formato. Todos los formatos de Microsoft Jet excepto A.M. cono p.m. se admiten. Si no hay ninguna cadena de formato, se utilizan las opciones de hora y imagen de fecha corta del Panel de control de Windows.|  
|**DecimalSymbol**|Se puede establecer en cualquier carácter único que se utilice para separar el entero de la parte fraccionaria de un número.|  
|**NumberDigits**|Indica el número de dígitos decimales en la parte fraccionaria de un número.|  
|**NumberLeadingZeros**|Especifica si un valor decimal menor que 1 y más de -1 debe contener ceros a la izquierda; este valor puede ser False (sin ceros a la izquierda) o True.|  
|**CurrencySymbol**|Indica el símbolo de moneda que se puede utilizar para los valores de moneda en el archivo de texto. Algunos ejemplos son el signo de dólar ($) y Dm.|  
|**CurrencyPosFormat**|Se puede establecer en cualquiera de los siguientes valores:<br /><br /> - Prefijo de símbolo de moneda sin separación ($1)<br />- Sufijo de símbolo de moneda sin separación (1$)<br />- Prefijo de símbolo de moneda con separación de un carácter ($ 1)<br />- Sufijo de símbolo de moneda con separación de un carácter (1 $)|  
|**CurrencyDigits**|Especifica el número de dígitos utilizados para la parte fraccionaria de un importe de moneda.|  
|**CurrencyNegformat**|Puede ser uno de los siguientes valores:<br /><br /> - ($1)<br />- -$1<br />- $-1<br />- $1-<br />- (1$)<br />- -1$<br />- 1-$<br />- 1$-<br />- -1 $<br />- -$ 1<br />- 1 $-<br />- $ 1-<br />- $ -1<br />- 1- $<br />- ($ 1)<br />- (1 $)<br /><br /> En este ejemplo se muestra el signo de dólar, pero debe reemplazarlo por el valor **CurrencySymbol** adecuado en el programa real.|  
|**CurrencyThousandSymbol**|Indica el símbolo de un solo carácter que se puede utilizar para separar los valores de moneda en el archivo de texto por miles.|  
|**CurrencyDecimalSymbol**|Se puede establecer en cualquier carácter único que se utilice para separar el todo de la parte fraccionaria de un importe de moneda.|  
  
> [!NOTE]  
>  Si omite una entrada, se utiliza el valor predeterminado en el Panel de control de Windows.
