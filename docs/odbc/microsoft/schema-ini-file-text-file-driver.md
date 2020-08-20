---
description: Archivo Schema.ini (controlador de archivo de texto)
title: Schema.ini archivo (controlador de archivo de texto) | Microsoft Docs
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
ms.openlocfilehash: 8b4bbebfa6eb184bf81cba4a9faf5e3200f428de
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500228"
---
# <a name="schemaini-file-text-file-driver"></a>Archivo Schema.ini (controlador de archivo de texto)
Cuando se utiliza el controlador de texto, el formato del archivo de texto se determina mediante un archivo de información de esquema. El archivo de información de esquema siempre se denomina Schema.ini y siempre se mantiene en el mismo directorio que el origen de datos de texto. El archivo de información de esquema proporciona información sobre el formato general del archivo, el nombre de la columna y la información del tipo de datos, y otras características de datos. Siempre se necesita un archivo Schema.ini para tener acceso a los datos de longitud fija. Debe utilizar un archivo de Schema.ini cuando la tabla de texto contenga datos de fecha y hora, moneda o decimales, o en cualquier momento en el que desee tener más control sobre el control de los datos de la tabla.  
  
> [!NOTE]  
>  El texto ISAM obtendrá los valores iniciales del registro, no de Schema.ini. El mismo formato de archivo predeterminado se aplica a todas las tablas de datos de texto nuevas. Todos los archivos creados por la instrucción CREATE TABLE heredan los mismos valores de formato predeterminados, que se establecen seleccionando los valores de formato de archivo en el cuadro de diálogo **definir formato de texto** con \<default> la opción seleccionada en la lista de **tablas** . Si los valores del registro difieren de los valores de Schema.ini, los valores del registro se sobrescribirán con los valores de Schema.ini.  
  
## <a name="understanding-schemaini-files"></a>Descripción de los archivos de Schema.ini  
 Los archivos Schema.ini proporcionan información de esquema sobre los registros de un archivo de texto. Cada entrada de Schema.ini especifica una de las cinco características de la tabla:  
  
-   Nombre del archivo de texto  
  
-   El formato de archivo  
  
-   Nombres de campo, anchos y tipos  
  
-   El juego de caracteres  
  
-   Conversiones de tipos de datos especiales  
  
 En las secciones siguientes se describen estas características.  
  
## <a name="specifying-the-file-name"></a>Especificar el nombre de archivo  
 La primera entrada de Schema.ini es siempre el nombre del archivo de origen de texto entre corchetes. En el ejemplo siguiente se muestra la entrada del Sample.txt de archivo:  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>Especificar el formato de archivo  
 La opción **Format** en Schema.ini especifica el formato del archivo de texto. El IISAM de texto puede leer el formato automáticamente de la mayoría de los archivos delimitados por caracteres. Puede usar cualquier carácter individual como delimitador en el archivo, excepto las comillas dobles ("). La configuración de **formato** de Schema.ini invalida la configuración del registro de Windows, archivo por archivo. En la tabla siguiente se enumeran los valores válidos para la opción **Format** .  
  
|Especificador de formato|Formato de tabla|Instrucción Schema.ini Format|  
|----------------------|------------------|---------------------------------|  
|**Delimitado por tabulaciones**|Los campos del archivo están delimitados por tabulaciones.|Formato = TabDelimited|  
|**Separado por CSV**|Los campos del archivo se delimitan mediante comas (valores separados por comas).|Formato = CSVDelimited|  
|**Delimitado personalizado**|Los campos del archivo están delimitados por cualquier carácter que elija para escribir en el cuadro de diálogo. Se permiten todas las comillas dobles ("), incluidas las en blanco.|Formato = delimitado (*carácter personalizado*)<br /><br /> o bien<br /><br /> Sin ningún delimitador especificado:<br /><br /> Formato = delimitado ()|  
|**Longitud fija**|Los campos del archivo tienen una longitud fija.|Format = FixedLength|  
  
## <a name="specifying-the-fields"></a>Especificar los campos  
 Puede especificar los nombres de campo en un archivo de texto delimitado por caracteres de dos maneras:  
  
-   Incluya los nombres de campo en la primera fila de la tabla y establezca **ColNameHeader** en **true.**  
  
-   Especifique cada columna por número y designe el nombre y el tipo de datos de la columna.  
  
 Debe especificar cada columna por número y designar el nombre de columna, el tipo de datos y el ancho de los archivos de longitud fija.  
  
> [!NOTE]  
>  El valor de **ColNameHeader** en Schema.ini invalida el valor de **FirstRowHasNames** en el registro de Windows, archivo por archivo.  
  
 También se pueden determinar los tipos de datos de los campos. Use la opción **MaxScanRows** para indicar el número de filas que se deben examinar al determinar los tipos de columna. Si establece **MaxScanRows** en 0, se analiza el archivo completo. El valor **MaxScanRows** de Schema.ini reemplaza la configuración del registro de Windows, archivo por archivo.  
  
 La entrada siguiente indica que Microsoft Jet debe utilizar los datos de la primera fila de la tabla para determinar los nombres de campo y debe examinar todo el archivo para determinar los tipos de datos utilizados:  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 La entrada siguiente designa los campos de una tabla mediante la opción de número de columna (**col**_n_), que es opcional para los archivos delimitados por caracteres y es necesario para los archivos de longitud fija. En el ejemplo se muestran las entradas de Schema.ini para dos campos, un campo de texto de NúmeroCliente de 10 caracteres y un campo de texto de CustomerName de 30 caracteres:  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 La sintaxis de **col**_n_ es:  
  
```  
  
n=ColumnName type [Width] [#]  
```  
  
## <a name="remarks"></a>Observaciones  
 En la tabla siguiente se describe cada una de las partes de la entrada de **col**_n_ .  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|*ColumnName*|Nombre de texto de la columna. Si el nombre de la columna contiene espacios incrustados, debe encerrarlo entre comillas dobles.|  
|*type*|Los tipos de datos son los siguientes:<br /><br /> **Tipos de datos de Microsoft Jet**<br /><br /> bit<br /><br /> Byte<br /><br /> Short<br /><br /> long<br /><br /> Moneda<br /><br /> Single<br /><br /> Double<br /><br /> DateTime<br /><br /> Texto<br /><br /> Memorándum<br /><br /> **Tipos de datos de ODBC** Char (igual que texto)<br /><br /> Float (igual que Double)<br /><br /> Entero (igual que corto)<br /><br /> LongChar (igual que Memo)<br /><br /> *Formato de fecha* de fecha|  
|**Width**|Valor de cadena literal `Width` . Indica que el número siguiente designa el ancho de la columna (opcional para los archivos delimitados por caracteres; se requiere para los archivos de longitud fija).|  
|*#*|Valor entero que designa el ancho de la columna (es obligatorio si se especifica **width** ).|  
  
## <a name="selecting-a-character-set"></a>Seleccionar un juego de caracteres  
 Puede seleccionar entre dos conjuntos de caracteres: ANSI y OEM. El valor de **characterSet** en Schema.ini invalida la configuración en el registro de Windows, archivo por archivo. En el ejemplo siguiente se muestra la entrada Schema.ini que establece el juego de caracteres en ANSI:  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>Especificar formatos y conversiones de tipos de datos  
 El archivo Schema.ini contiene varias opciones que puede usar para especificar cómo se convierten o muestran los datos. En la tabla siguiente se muestra cada una de estas opciones.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**DateTimeFormat**|Se puede establecer en una cadena de formato que indique fechas y horas. Debe especificar esta entrada si todos los campos de fecha y hora de la importación o exportación se controlan con el mismo formato. Todos los formatos de Microsoft Jet excepto la mañana cono p.m. se admiten. Si no hay ninguna cadena de formato, se usan las opciones de fecha y hora cortas del panel de control de Windows.|  
|**DecimalSymbol**|Se puede establecer en cualquier carácter individual que se utilice para separar el entero de la parte fraccionaria de un número.|  
|**NumberDigits**|Indica el número de dígitos decimales en la parte fraccionaria de un número.|  
|**NumberLeadingZeros**|Especifica si un valor decimal menor que 1 y mayor que-1 debe contener ceros a la izquierda; Este valor puede ser false (sin ceros a la izquierda) o true.|  
|**CurrencySymbol**|Indica el símbolo de moneda que se puede utilizar para los valores de divisa en el archivo de texto. Entre los ejemplos se incluyen el signo de dólar ($) y DM.|  
|**CurrencyPosFormat**|Se puede establecer en cualquiera de los siguientes valores:<br /><br /> -Prefijo de símbolo de moneda sin separación ($1)<br />-Sufijo de símbolo de moneda sin separación ($1)<br />-Prefijo de símbolo de moneda con separación de un carácter ($1)<br />-Sufijo de símbolo de moneda con separación de caracteres ($1)|  
|**CurrencyDigits**|Especifica el número de dígitos que se usan para la parte fraccionaria de una cantidad de moneda.|  
|**CurrencyNegFormat**|Puede ser uno de los siguientes valores:<br /><br /> -($1)<br />--$1<br />-$-1<br />-$1-<br />-($1)<br />--$1<br />-1-$<br />-$1-<br />--$1<br />--$1<br />-$1-<br />-$1-<br />-$-1<br />-1-$<br />-($1)<br />-($1)<br /><br /> Este ejemplo muestra el signo de dólar, pero debe reemplazarlo por el valor de **CurrencySymbol** adecuado en el programa real.|  
|**CurrencyThousandSymbol**|Indica el símbolo de un solo carácter que se puede usar para separar los valores de divisa en el archivo de texto por miles.|  
|**CurrencyDecimalSymbol**|Se puede establecer en cualquier carácter individual que se utilice para separar el conjunto de la parte fraccionaria de una cantidad de moneda.|  
  
> [!NOTE]  
>  Si omite una entrada, se utiliza el valor predeterminado en el panel de control de Windows.
