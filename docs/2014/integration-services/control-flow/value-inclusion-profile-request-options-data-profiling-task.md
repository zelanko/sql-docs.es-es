---
title: Opciones de Solicitud de perfil de inclusión de valores (tarea de generación de perfiles de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: ca94da82-a4c9-4e87-9cba-c2d85bd31f01
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e524fcb3a107384853a5c6fa2114cadb58f80636
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84917795"
---
# <a name="value-inclusion-profile-request-options-data-profiling-task"></a>Opciones de Solicitud de perfil de inclusión de valores (tarea de generación de perfiles de datos)
  Utilice el panel **Propiedades de la solicitud** de la página **Solicitudes de perfil** para establecer las opciones de **Solicitud de perfil de inclusión de valores** seleccionadas en el panel de solicitudes. Un perfil de inclusión de valores calcula la superposición en los valores entre dos columnas o conjuntos de columnas. Por lo tanto, también puede determinar si una columna o un conjunto de columnas es adecuado para actuar como una clave externa entre las tablas seleccionadas. Este perfil también puede ayudarle a identificar problemas de los datos, por ejemplo valores que no sean válidos. Por ejemplo, suponga que utiliza un perfil de inclusión de valores para generar el perfil de la columna de identificadores de producto de una tabla de ventas. El perfil detecta que la columna contiene valores que no están en la columna IdProducto de la tabla Productos.  
  
> [!NOTE]  
>  Las opciones que se describen en este tema aparecen en la página **Solicitudes de perfil** del **Editor de tareas de generación de perfiles de datos**. Para obtener más información sobre esta página del editor, vea [Editor de tareas de generación de perfiles de datos &#40;página Solicitudes de perfil&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Para más información sobre cómo usar la tarea de generación de perfiles de datos, vea [Configuración de la Tarea de generación de perfiles de datos](data-profiling-task.md). Para obtener más información sobre cómo usar el Visor de perfil de datos para analizar la salida de la tarea de generación de perfiles de datos, vea [Visor de perfil de datos](data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-columns-for-the-inclusioncolumns-property"></a>Selección de columnas para la propiedad InclusionColumns  
 Una **Solicitud de perfil de inclusión de valores** calcula si todos los valores de un subconjunto se encuentran en el superconjunto. El superconjunto suele ser una tabla de referencia o búsqueda. Por ejemplo, la columna de estado de una tabla de direcciones es la tabla de subconjunto. Cada código de estado de dos caracteres de esta columna también se debería encontrar en la tabla de códigos de estado del servicio postal de Estados Unidos, que es la tabla de superconjunto.  
  
 Cuando se usa el carácter comodín (*) como valor de la columna de subconjunto o de superconjunto, la tarea de generación de perfiles de datos compara cada columna de ese lado con la columna especificada en el otro.  
  
> [!NOTE]  
>  Si selecciona (*), esta opción podría provocar un gran número de cálculos y disminuir el rendimiento de la tarea.  
  
## <a name="understanding-the-threshold-settings"></a>Descripción de los valores del umbral  
 Puede utilizar dos valores de umbral diferentes para precisar la salida de una solicitud de perfil de inclusión de valores.  
  
 Al especificar un valor distinto de **None** para **InclusionThresholdSetting**, el perfil solo notifica el nivel de inclusión del subconjunto en el superconjunto bajo una de las condiciones siguientes:  
  
-   Cuando el perfil de inclusión supera el umbral que se especifica en **InclusionStrengthThreshold**.  
  
-   Cuando el perfil de inclusión tiene un valor de 1.0 e **InclusionStrengthThreshold** se establece en **Exact**.  
  
 Puede precisar más la salida si filtra las combinaciones en las que la columna de superconjunto no sea una clave adecuada para la tabla de superconjunto debido a que contenga valores no únicos. Cuando especifica un valor distinto de **None** para **SupersetColumnsKeyThresholdSetting**, el perfil solo notifica el nivel de inclusión del subconjunto en el superconjunto en una de las condiciones siguientes:  
  
-   Cuando la conveniencia de las columnas de superconjunto como una clave en la tabla de superconjunto supera el umbral especificado en **SupersetColumnsKeyThreshold**  
  
-   Cuando el nivel de inclusión tiene un valor ó 1.0 y el valor de **SupersetColumnsKeyThreshold** está establecido en **Exact**.  
  
## <a name="request-properties-options"></a>Opciones de Propiedades de la solicitud  
 Para cada **Solicitud de perfil de inclusión de valores**, el panel **Propiedades de la solicitud** muestra los grupos siguientes de opciones:  
  
-   **Data**, que incluye las opciones **SubsetTableOrView**, **SupersetTableOrView**e **InclusionColumns**  
  
-   **General**  
  
-   **Opciones**  
  
### <a name="data-options"></a>Opciones de Data  
 **ConnectionManager**  
 Seleccione el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] existente que usa el proveedor de datos .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para conectarse a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla o la vista con la que se generará el perfil.  
  
 **SubsetTableOrView**  
 Seleccione la tabla o vista cuyo perfil se va a generar.  
  
 Para obtener más información, vea la sección, "Opciones de SubsetTableOrView y SupersetTableOrView" en este tema.  
  
 **SupersetTableOrView**  
 Seleccione la tabla o vista cuyo perfil se va a generar.  
  
 Para obtener más información, vea la sección, "Opciones de SubsetTableOrView y SupersetTableOrView" en este tema.  
  
 **InclusionColumns**  
 Seleccione las columnas o conjuntos de columnas en las tablas de superconjunto y subconjunto.  
  
 Para obtener más información, vea las secciones "Selección de columnas para la propiedad InclusionColumns" y "Opciones de InclusionColumns" en este tema.  
  
#### <a name="subsettableorview-and-supersettableorview-options"></a>Opciones de SubsetTableOrView y SupersetTableOrView  
 **Esquema**  
 Especifica el esquema al que pertenece la tabla seleccionada. Esta opción es de solo lectura.  
  
 **TableOrView**  
 Muestra el nombre de la tabla seleccionada. Esta opción es de solo lectura.  
  
#### <a name="inclusioncolumns-options"></a>Opciones de InclusionColumns  
 Las opciones siguientes se presentan para cada conjunto de columnas seleccionado para generar perfiles en **InclusionColumns**.  
  
 Para obtener más información, vea la sección "Selección de columnas para la propiedad InclusionColumns" anteriormente en este tema.  
  
 **IsWildcard**  
 Especifica si se ha seleccionado el carácter comodín **(\*)** . Esta opción está establecida en **True** si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Es **False** si ha seleccionado una columna individual para la que generar un perfil. Esta opción es de solo lectura.  
  
 **ColumnName**  
 Muestra el nombre de la columna seleccionada. Esta opción está en blanco si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Esta opción es de solo lectura.  
  
 **StringCompareOptions**  
 Seleccione las opciones para comparar los valores de cadena. Esta propiedad presenta las opciones indicadas en la siguiente tabla. El valor predeterminado de esta opción es **Default**.  
  
> [!NOTE]  
>  Cuando use el carácter comodín **(\*)** para **ColumnName**, **CompareOptions** es de solo lectura y se establece en el valor **Default**.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Valor predeterminado**|Ordena y compara datos basados en la intercalación de la columna en la tabla de origen.|  
|**BinarySort**|Ordena y compara los datos según los patrones de bits definidos para cada carácter. El orden binario utiliza la distinción de mayúsculas y minúsculas, y de acentos. El orden binario es también el más rápido.|  
|**DictionarySort**|Ordena y compara los datos según el orden y las reglas de comparación definidas en los diccionarios del idioma o alfabeto asociado.|  
  
 Si selecciona **DictionarySort**, también puede seleccionar cualquier combinación de las opciones enumeradas en la tabla siguiente. De forma predeterminada, no se selecciona ninguna de estas opciones adicionales.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**IgnoreCase**|Especifica si la comparación distingue entre mayúsculas y minúsculas. Si se establece esta opción, la comparación de las cadenas omite la distinción entre mayúsculas y minúsculas. Por ejemplo, "ABC" se interpreta igual que "abc".|  
|**IgnoreNonSpace**|Especifica si la comparación distingue entre caracteres con espacio y signos diacríticos. Si se establece esta opción, la comparación omite los signos diacríticos. Por ejemplo, "å" se considera igual que "a".|  
|**IgnoreKanaType**|Especifica si la comparación distingue entre los dos tipos de caracteres kana japoneses: hiragana y katakana. Si se establece esta opción, la comparación de las cadenas omite los tipos de caracteres kana.|  
|**IgnoreWidth**|Especifica si la comparación distingue entre un carácter de un solo byte y el mismo carácter cuando se representa con un carácter de doble byte. Si se establece esta opción, la comparación de las cadenas trata las representaciones de un solo byte y de doble byte del mismo carácter como idénticas.|  
  
### <a name="general-options"></a>Opciones generales  
 **IdSolicitud**  
 Escriba un nombre descriptivo para identificar esta solicitud de perfil. Generalmente, no tiene que cambiar el valor generado automáticamente.  
  
### <a name="options"></a>Opciones  
 **InclusionThresholdSetting**  
 Seleccione el valor de umbral para precisar la salida del perfil. El valor predeterminado de esta propiedad es **Specified**. Para obtener más información, vea la sección "Descripción de los valores del umbral" anteriormente en este tema.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**None**|No especifica un umbral. El nivel de la clave se notifica independientemente de su valor.|  
|**Specified**|Utilice el umbral que se especifica en **InclusionStrengthThreshold**. Solo se notifica el nivel de inclusión si es mayor que el umbral.|  
|**Exact**|No especifica un umbral. Solo se notifica el nivel de inclusión si los valores del subconjunto están completamente incluidos en los valores del superconjunto.|  
  
 **InclusionStrengthThreshold**  
 Especifique el umbral (con un valor entre 0 y 1) por encima del que se debería indicar un nivel de inclusión. El valor predeterminado de esta propiedad es 0,95. Esta opción solo se habilita cuando la opción **Specified** se selecciona como **InclusionThresholdSetting**.  
  
 Para obtener más información, vea la sección "Descripción de los valores del umbral" anteriormente en este tema.  
  
 **SupersetColumnsKeyThresholdSetting**  
 Especifique el umbral del superconjunto. El valor predeterminado de esta propiedad es **Specified**. Para obtener más información, vea la sección "Descripción de los valores del umbral" anteriormente en este tema.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**None**|No especifica un umbral. El nivel de inclusión se notifica sin tener en cuenta el nivel de clave de la columna de superconjunto.|  
|**Specified**|Utilice el umbral que se especifica en **SupersetColumnsKeyThreshold**. Solo se notifica el nivel de inclusión si el nivel de clave de la columna de superconjunto es mayor que el umbral.|  
|**Exact**|No especifica un umbral. Solo se notifica el nivel de inclusión si las columnas de superconjunto son una clave exacta en la tabla de superconjunto.|  
  
 **SupersetColumnsKeyThreshold**  
 Especifique el umbral (con un valor entre 0 y 1) por encima del que se debería indicar un nivel de inclusión. El valor predeterminado de esta propiedad es 0,95. Esta opción solo está habilitada cuando **Specified** está seleccionado como **SupersetColumnsKeyThresholdSetting**.  
  
 Para obtener más información, vea la sección "Descripción de los valores del umbral" anteriormente en este tema.  
  
 **MaxNumberOfViolations**  
 Especifique el número máximo de infracciones de la inclusión que va a notificarse en la salida. El valor predeterminado de esta propiedad es 100. Esta opción se deshabilita cuando la opción **Exact** se selecciona como **InclusionThresholdSetting**.  
  
## <a name="see-also"></a>Consulte también  
 [Editor de tareas de generación de perfiles de datos &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)   
 [Formulario de perfil rápido de tabla única &#40;tarea de generación de perfiles de datos&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
