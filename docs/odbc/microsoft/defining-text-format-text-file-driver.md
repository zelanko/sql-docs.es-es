---
title: Definición del formato de texto (controlador de archivo de texto) Microsoft Docs
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
ms.openlocfilehash: 29dc46525f3c81e5abffe5076988716a01df06df
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307666"
---
# <a name="defining-text-format-text-file-driver"></a>Definir el formato de texto (controlador de archivo de texto)
Cuando se utiliza el controlador de texto, puede utilizar el cuadro de diálogo **Definir formato** de texto para definir el formato de las columnas de un archivo seleccionado. Este cuadro de diálogo le permite especificar el esquema para cada tabla de datos. Esta información se escribe en un archivo Schema.ini en el directorio del origen de datos. Se crea un archivo Schema.ini independiente para cada directorio de origen de datos de texto.  
  
> [!NOTE]  
>  El mismo formato de archivo predeterminado se aplica a todas las tablas de datos de texto nuevas. Todos los archivos creados por la instrucción CREATE TABLE heredan esos mismos valores de \<formato predeterminados, que se establecen seleccionando valores de formato de archivo en el cuadro de diálogo Definir formato de **texto** con el valor predeterminado> elegido en la lista **Tablas.** El controlador de texto no cambia el formato de un archivo de texto existente para que coincida con el formato definido en este cuadro de diálogo, pero devuelve un error cuando utiliza el formato, como cuando intenta recuperar datos del archivo de texto.  
  
 Las siguientes opciones están disponibles en el cuadro de diálogo Definir formato de **texto:**  
  
|Opción|Information|  
|------------|-----------------|  
|**Agregar**|Agrega una columna utilizando los valores de **Tipo**de datos , **Nombre**y **Ancho** en el cuadro de diálogo y, si procede, el valor Separador de fecha de Schema.ini.|  
|**Caracteres**|**ANSI** u **OEM**. OEM especifica un juego de caracteres que no es ANSI. Este valor predeterminado es OEM si el formato del elemento seleccionado en la lista **Tablas** no se ha definido previamente en este cuadro de diálogo.|  
|**Encabezado del nombre de columna**|Indica si las columnas de la primera fila de la tabla seleccionada se van a utilizar como nombres de columna. TRUE **TRUE** o **FALSE**. El valor predeterminado es FALSE si el formato del elemento seleccionado en la lista **Tablas** no se ha definido previamente en este cuadro de diálogo.|  
|**Columnas**|Enumera los nombres de columna para cada columna de la tabla seleccionada. El orden de las columnas refleja el orden de las columnas de la tabla. Esta lista está habilitada si se ha seleccionado un archivo en la lista **Tablas.**|  
|**Tipo de datos**|Puede ser BIT, BYTE, CHAR, CURRENCY, DATE, FLOAT, INTEGER, LONGCHAR, SHORT o SINGLE. Los tipos de datos de fecha pueden estar en los siguientes formatos: "dd-mmm-yy", "mm-dd-aa", "mmm-dd-aa", "aaaa-mm-dd" o "aaaa-mmm-dd". "mm" denota números durante meses; "mmm" denota cartas durante meses.|  
|**Delimitador**|Especifica el carácter delimitador personalizado que se utilizará para separar columnas. Se habilita cuando se selecciona el formato **Delimitado por** la costumbre. El delimitador puede tener un solo carácter de longitud y las comillas dobles (") no se pueden utilizar como carácter delimitador. (El delimitador no se puede especificar en formato hexadecimal o decimal.)|  
|**Formato**|Longitud delimitada o fija. Si está delimitado, indica el tipo de delimitador utilizado: coma (CSV), tabulación o carácter especial (personalizado). El valor predeterminado es **CSV Delimitado** si el formato del elemento seleccionado en la lista **Tablas** no se ha definido previamente en este cuadro de diálogo.<br /><br /> Si **Format** es de longitud fija y **El encabezado** de nombre de columna es TRUE, la primera línea debe estar delimitada por comas.|  
|**Adivinar**|Genera automáticamente los valores de tipo de datos, nombre y ancho de la columna para las columnas de la tabla seleccionada escaneando el contenido de la tabla según la selección del cuadro **Formato.** Habilitado cuando se delimita el formato de tabla. Las columnas definidas anteriormente en la lista **Columnas** se borran y se reemplazan por nuevas entradas. Si no se selecciona Encabezado de **nombre** de columna, los nombres de columna se generan automáticamente como "F1", "F2", etc. No se muestra ningún valor predeterminado en el cuadro **Tipo** de datos.<br /><br /> Esta funcionalidad solo funciona en columnas que tienen menos de 64.513 bytes.|  
|**Modify**|Modifica la columna seleccionada utilizando los valores de **Tipo**de datos , **Nombre**y **Ancho**.|  
|**Nombre**|Muestra el nombre de la columna seleccionada. Se puede utilizar para especificar un nuevo nombre de columna para una columna existente o una columna nueva.<br /><br /> Si **el encabezado** del nombre de columna es TRUE, se omite el nombre de columna que se muestra.|  
|**Quitar**|Elimina la columna seleccionada.|  
|**Filas para escanear**|El número de filas que el programa de instalación o el controlador analizarán al establecer las columnas y los tipos de datos de columna en función de los datos existentes.<br /><br /> Puede introducir un número del 1 al 32767 para el número de filas que desea escanear. Este valor predeterminado es 25 si el formato del elemento seleccionado en la lista **Tablas** no se ha definido previamente en este cuadro de diálogo. (Un número fuera del límite devolverá un error.)|  
|**Tablas**|Contiene una lista de todos los archivos del directorio seleccionado en el cuadro de diálogo Configuración de **texto** que coinciden con la lista de extensiones especificadas.<br /><br /> Cuando \<se selecciona el valor predeterminado> y se cumple una de las siguientes opciones, los valores de los atributos de tabla del grupo **Tablas** se escriben en Schema.ini (no se toca ninguna otra entrada en Schema.ini):<br /><br /> - No hay ningún Schema.ini en el directorio especificado.<br />- El archivo Schema.ini existe, pero no hay ninguna sección en Schema.ini para uno de los archivos de texto (con la extensión especificada) en el directorio.<br />- La sección de un archivo de texto existe en Schema.ini, pero el cuerpo está vacío.<br /><br /> Cuando \<se selecciona el> predeterminado, el grupo **Columnas** está deshabilitado.|  
|**Width**|El ancho de la columna se puede cambiar para las columnas CHAR o LONGCHAR. El valor predeterminado de ancho es 1 si el formato del elemento seleccionado en la lista **Tablas** no se ha definido previamente en este cuadro de diálogo.<br /><br /> Para otros tipos de datos, el control de ancho está deshabilitado y no se muestra ningún valor.|
