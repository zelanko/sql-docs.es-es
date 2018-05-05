---
title: Definir el formato de texto (controlador de archivo de texto) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: 3af46dad-52cc-4d5c-a27e-6315d65a74e6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b8d87785ccb63796698e164b36728301d3c35e5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="defining-text-format-text-file-driver"></a>Definir el formato de texto (controlador de archivo de texto)
Cuando se utiliza el controlador de texto, puede usar el **Definir formato de texto** cuadro de diálogo para definir el formato de columnas en un archivo seleccionado. Este cuadro de diálogo permite especificar el esquema para cada tabla de datos. Esta información se escribe en un archivo Schema.ini en el directorio de origen de datos. Se crea un archivo Schema.ini independiente para cada directorio de origen de datos de texto.  
  
> [!NOTE]  
>  El mismo formato de archivo predeterminado se aplica a todas las tablas de datos de texto nuevo. Todos los archivos creados por la instrucción CREATE TABLE heredan los mismos valores de formato predeterminado, que se establecen mediante la selección de valores de formato de archivo en el **Definir formato de texto** cuadro de diálogo con \<predeterminado > elegido en el **Tablas** lista. El controlador de texto no cambia el formato de un archivo de texto existente para que coincida con el formato definido en este cuadro de diálogo, pero devuelve un error cuando utiliza el formato, por ejemplo, cuando intenta recuperar los datos del archivo de texto.  
  
 Las siguientes opciones están disponibles en la **Definir formato de texto** cuadro de diálogo:  
  
|Opción|Información|  
|------------|-----------------|  
|**Agregar**|Agrega una columna con los valores de **tipo de datos**, **nombre**, y **ancho** desde el cuadro de diálogo, y si procede, el separador de fecha valor de Schema.ini.|  
|**Caracteres**|**ANSI** o **OEM**. OEM especifica un juego de caracteres no ANSI. El valor predeterminado es OEM si el formato del elemento seleccionado en el **tablas** lista no se ha definido anteriormente en este cuadro de diálogo.|  
|**Encabezado de nombre de columna**|Indica si las columnas de la primera fila de la tabla seleccionada se usará como nombres de columna. Cualquier **TRUE** o **FALSE**. Valor predeterminado es FALSE si el formato del elemento seleccionado en el **tablas** lista no se ha definido anteriormente en este cuadro de diálogo.|  
|**Columnas**|Enumera los nombres de columna para cada columna de la tabla seleccionada. El orden de las columnas refleja el orden de las columnas de la tabla. Esta lista se habilita si se ha seleccionado un archivo en el **tablas** lista.|  
|**Tipo de datos**|Puede ser BIT, BYTE, CHAR, moneda, fecha, FLOAT, entero, LONGCHAR, SHORT o único. Tipos de datos de fecha pueden estar en los siguientes formatos: "dd-mmm-aa", "mm-dd-aa", "mmm-dd-aa", "aaaa-mm-dd" o "aaaa-mmm-dd". "mm" denota números para meses; "mmm" denota letras para los meses.|  
|**Delimitador**|Especifica el carácter delimitador personalizado que se usará para separar las columnas. Cuando habilita la **delimitado personalizado** se selecciona el formato. El delimitador puede ser un único carácter de longitud y no se puede usar comillas dobles (") como el carácter delimitador. (El delimitador no pueden especificarse en formato decimal o hexadecimal).|  
|**Formato**|Longitud delimitado o fijo. Si es delimitado, indica el tipo de delimitador utilizado: por comas (CSV), ficha o carácter especial (personalizado). El valor predeterminado es **delimitado CSV** si el formato del elemento seleccionado en el **tablas** lista no se ha definido anteriormente en este cuadro de diálogo.<br /><br /> Si **formato** tiene una longitud fija y **encabezado nombre de columna** es TRUE, la primera línea debe estar delimitada por comas.|  
|**Estimación**|Genera automáticamente los valores de tipo, nombre y ancho de datos de la columna de las columnas en la tabla seleccionada mediante el análisis de contenido de la tabla según el **formato** cuadro de selección. Habilitado cuando el formato de tabla es delimitado. Cualquiera de las columnas en definidas previamente el **columnas** lista se borran y se reemplazan con nuevas entradas. Si **encabezado nombre de columna** está desactivada, los nombres de columna se generan automáticamente como "F1", "F2" y así sucesivamente. Ningún valor predeterminado se muestra en el **tipo de datos** cuadro.<br /><br /> Esta funcionalidad solo funciona en las columnas que son menos de 64,513 bytes.|  
|**Modificar**|Modifica la columna seleccionada usando los valores de **tipo de datos**, **nombre**, y **ancho**.|  
|**Nombre**|Muestra el nombre de la columna seleccionada. Puede utilizarse para especificar un nuevo nombre de columna para una columna existente o una nueva columna.<br /><br /> Si **encabezado nombre de columna** es TRUE, la columna se omite el nombre que se muestra.|  
|**Quitar**|Elimina la columna seleccionada.|  
|**Filas para explorar**|El número de filas que el programa de instalación o el controlador explorarán cuando se establezcan las columnas y los tipos de datos de columna basados en datos existentes.<br /><br /> Puede escribir un número entre 1 y 32767 para el número de filas que se va a buscar. El valor predeterminado es 25 if el formato del elemento seleccionado en el **tablas** lista no se ha definido anteriormente en este cuadro de diálogo. (Un número que está fuera del límite devolverá un error.)|  
|**Tablas**|Contiene una lista de todos los archivos en el directorio seleccionado en el **el programa de instalación de texto** cuadro de diálogo que coinciden con la lista de las extensiones especificadas.<br /><br /> Cuando \<predeterminado > está seleccionada, y uno de los siguientes es true, los valores de los atributos de tabla en la **tablas** grupo se escriben en Schema.ini (no hay otras entradas de Schema.ini modificadas):<br /><br /> -No hay ningún Schema.ini en el directorio especificado.<br />-El archivo Schema.ini existe, pero no hay ninguna sección de Schema.ini para uno de los archivos de texto (con la extensión especificada) en el directorio.<br />-La sección de un archivo de texto existe en Schema.ini, pero el cuerpo está vacío.<br /><br /> Cuando \<predeterminado > está seleccionada, el **columnas** grupo está deshabilitado.|  
|**Ancho**|El ancho de la columna se puede cambiar para columnas CHAR o LONGCHAR. El ancho predeterminado es 1 si el formato del elemento seleccionado en el **tablas** lista no se ha definido anteriormente en este cuadro de diálogo.<br /><br /> Para otros tipos de datos, el ancho del control está deshabilitado y se muestra ningún valor.|
