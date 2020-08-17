---
description: Definir el formato de texto (controlador de archivo de texto)
title: Definir el formato de texto (controlador de archivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text format [ODBC]
- text file driver [ODBC], text format
ms.assetid: 3af46dad-52cc-4d5c-a27e-6315d65a74e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe992d4ea7cf81387bc56ef9c384404b015b52a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340951"
---
# <a name="defining-text-format-text-file-driver"></a>Definir el formato de texto (controlador de archivo de texto)
Cuando se utiliza el controlador de texto, puede usar el cuadro de diálogo **definir formato de texto** para definir el formato de las columnas de un archivo seleccionado. Este cuadro de diálogo permite especificar el esquema de cada tabla de datos. Esta información se escribe en un archivo Schema.ini en el directorio de origen de datos. Se crea un archivo de Schema.ini independiente para cada directorio de origen de datos de texto.  
  
> [!NOTE]  
>  El mismo formato de archivo predeterminado se aplica a todas las tablas de datos de texto nuevas. Todos los archivos creados por la instrucción CREATE TABLE heredan los mismos valores de formato predeterminados, que se establecen seleccionando valores de formato de archivo en el cuadro de diálogo **definir formato de texto** \<default> seleccionado en la lista **tablas** . El controlador de texto no cambia el formato de un archivo de texto existente para que coincida con el formato definido en este cuadro de diálogo, pero devuelve un error cuando usa el formato, como cuando intenta recuperar datos del archivo de texto.  
  
 Las siguientes opciones están disponibles en el cuadro de diálogo **definir formato de texto** :  
  
|Opción|Información|  
|------------|-----------------|  
|**Add (Agregar)**|Agrega una columna con los valores del **tipo de datos**, **el nombre y el** **ancho** del cuadro de diálogo y, si procede, el valor del separador de fecha de Schema.ini.|  
|**Caracteres**|**ANSI** o **OEM**. OEM especifica un juego de caracteres que no es ANSI. El valor predeterminado es OEM si el formato del elemento seleccionado en la lista de **tablas** no se ha definido previamente en este cuadro de diálogo.|  
|**Encabezado de nombre de columna**|Indica si las columnas de la primera fila de la tabla seleccionada se van a utilizar como nombres de columna. **Es true** o **false**. El valor predeterminado es FALSE si el formato del elemento seleccionado en la lista de **tablas** no se ha definido previamente en este cuadro de diálogo.|  
|**Columnas**|Muestra los nombres de columna de cada columna de la tabla seleccionada. El orden de las columnas refleja el orden de las columnas de la tabla. Esta lista se habilita si se ha seleccionado un archivo en la lista de **tablas** .|  
|**Tipo de datos**|Puede ser BIT, BYTE, CHAR, CURRENCY, DATE, FLOAT, integer, LONGCHAR, SHORT o SINGLE. Los tipos de datos de fecha pueden tener los siguientes formatos: "dd-mmm-AA", "MM-DD-AA", "MMM-DD-AA", "AAAA-MM-DD" o "AAAA-MMM-DD". "mm" denota números en meses; "MMM" denota las letras de los meses.|  
|**Delimitador**|Especifica el carácter delimitador personalizado que se va a utilizar para separar las columnas. Habilitado cuando se selecciona el formato **delimitado personalizado** . El delimitador solo puede tener un carácter de longitud, y las comillas dobles (") no se pueden utilizar como carácter delimitador. (El delimitador no se puede especificar en formato hexadecimal o decimal).|  
|**Formato**|Delimitado o longitud fija. Si está delimitado, indica el tipo de delimitador usado: coma (CSV), tabulación o carácter especial (personalizado). El valor predeterminado es **CSV delimitado** si el formato del elemento seleccionado en la lista de **tablas** no se ha definido previamente en este cuadro de diálogo.<br /><br /> Si el **formato** es de longitud fija y el **encabezado de nombre de columna** es true, la primera línea debe estar delimitada por comas.|  
|**Adivinar**|Genera automáticamente los valores de tipo de datos, nombre y ancho de las columnas de la tabla seleccionada examinando el contenido de la tabla de acuerdo con la selección del cuadro **formato** . Habilitado cuando el formato de tabla está delimitado. Las columnas definidas anteriormente en la lista de **columnas** se borran y se reemplazan por entradas nuevas. Si **el encabezado de nombre de columna** no está seleccionado, los nombres de columna se generan automáticamente como "F1", "F2", etc. No se muestra ningún valor predeterminado en el cuadro **tipo de datos** .<br /><br /> Esta funcionalidad solo funciona en columnas que tienen menos de 64.513 bytes.|  
|**Modificar**|Modifica la columna seleccionada usando los valores de **tipo de datos**, **nombre**y **ancho**.|  
|**Nombre**|Muestra el nombre de la columna seleccionada. Se puede utilizar para especificar un nuevo nombre de columna para una columna existente o una nueva columna.<br /><br /> Si el **encabezado de nombre de columna** es true, se omite el nombre de columna que se muestra.|  
|**Remove**|Elimina la columna seleccionada.|  
|**Filas que se van a examinar**|El número de filas que el programa de instalación o el controlador examinará al establecer los tipos de datos de columnas y columnas basándose en los datos existentes.<br /><br /> Puede escribir un número comprendido entre 1 y 32767 para el número de filas que se van a examinar. El valor predeterminado es 25 si el formato del elemento seleccionado en la lista de **tablas** no se ha definido previamente en este cuadro de diálogo. (Un número fuera del límite devolverá un error).|  
|**Tablas**|Contiene una lista de todos los archivos del directorio seleccionado en el cuadro de diálogo de **configuración de texto** que coinciden con la lista de extensiones especificadas.<br /><br /> Cuando \<default> se selecciona y se cumple una de las siguientes condiciones, los valores de los atributos de tabla del grupo **tablas** se escriben en Schema.ini (no se tocan otras entradas en Schema.ini):<br /><br /> -No hay ningún Schema.ini en el directorio especificado.<br />-El archivo de Schema.ini existe, pero no hay ninguna sección en Schema.ini para uno de los archivos de texto (con la extensión especificada) en el directorio.<br />-La sección de un archivo de texto existe en Schema.ini, pero el cuerpo está vacío.<br /><br /> Cuando \<default> se selecciona, el grupo **columnas** está deshabilitado.|  
|**Width**|El ancho de la columna se puede cambiar para las columnas CHAR o LONGCHAR. El ancho predeterminado es 1 si el formato del elemento seleccionado en la lista de **tablas** no se ha definido previamente en este cuadro de diálogo.<br /><br /> Para otros tipos de datos, el control de ancho está deshabilitado y no se muestra ningún valor.|
