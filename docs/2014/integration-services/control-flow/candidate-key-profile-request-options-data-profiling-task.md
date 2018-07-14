---
title: Opciones de Solicitud de perfil de claves candidatas (tarea de generación de perfiles de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 8632dbc4-4394-4dc7-b19c-f9adeb21ba52
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1d3685d6827f8ed57394f6440b018935662fb9e8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37266971"
---
# <a name="candidate-key-profile-request-options-data-profiling-task"></a>Opciones de Solicitud de perfil de claves candidatas (tarea de generación de perfiles de datos)
  Utilice el panel **Propiedades de la solicitud** de la página **Solicitudes de perfil** para establecer las opciones de **Solicitud de perfil de claves candidatas** seleccionadas en el panel de solicitudes. Un perfil de claves candidatas notifica si una columna o conjunto de columnas es una clave, o una clave aproximada, para la tabla seleccionada. Este perfil también puede ayudarle a identificar problemas de los datos, por ejemplo valores duplicados en una posible columna de clave.  
  
> [!NOTE]  
>  Las opciones que se describen en este tema aparecen en la página **Solicitudes de perfil** del **Editor de tareas de generación de perfiles de datos**. Para obtener más información sobre esta página del editor, vea [Editor de tareas de generación de perfiles de datos &#40;página Solicitudes de perfil&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Para más información sobre cómo usar la tarea de generación de perfiles de datos, vea [Configuración de la Tarea de generación de perfiles de datos](data-profiling-task.md). Para más información sobre cómo usar el Visor de perfil de datos para analizar la salida de la tarea de generación de perfiles de datos, vea [Visor de perfil de datos](data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-columns-for-the-keycolumns-property"></a>Selección de columnas para la propiedad KeyColumns  
 Cada **Solicitud de perfil de claves candidatas** calcula el nivel de clave de un único candidato a clave que consta de una sola columna o de varias:  
  
-   Al seleccionar solo una columna en **KeyColumns**, la tarea calcula el nivel de clave de esa columna.  
  
-   Al seleccionar varias columnas en **KeyColumns**, la tarea calcula el nivel de clave de la clave compuesta que consta de todas las columnas seleccionadas.  
  
-   Al seleccionar el carácter comodín, **(\*)**, en **KeyColumns**, la tarea calcula el nivel de clave de cada columna de la tabla o vista.  
  
 Por ejemplo, considere una tabla de ejemplo que contiene las columnas A, B y C. Realiza las selecciones siguientes para **KeyColumns**:  
  
-   Seleccione (\*) y la columna C en **KeyColumns**. La tarea calcula el nivel de clave de la columna C y, a continuación, de los candidatos a clave compuesta (A, C) y (B, C).  
  
-   Seleccione (\*) y (\*) en **KeyColumns**. La tarea calcula el nivel de clave de las columnas individuales A, B y C, y a continuación de los candidatos a clave compuesta (A, B), (A, C) y (B, C).  
  
> [!NOTE]  
>  Si selecciona (*), esta opción podría provocar un gran número de cálculos y disminuir el rendimiento de la tarea. Sin embargo, si la tarea encuentra un subconjunto que satisface el umbral para una clave, no analiza las combinaciones adicionales. Por ejemplo, en la tabla de ejemplo descrita anteriormente, si la tarea determina que la columna C es una clave, no continúa analizando los candidatos a clave compuesta.  
  
## <a name="request-properties-options"></a>Opciones de Propiedades de la solicitud  
 Para cada **Solicitud de perfil de claves candidatas**, el panel **Propiedades de la solicitud** muestra los grupos siguientes de opciones:  
  
-   **Data**, que incluye las opciones **TableOrView** y **KeyColumns**  
  
-   **General**  
  
-   **Opciones**  
  
### <a name="data-options"></a>Opciones de Data  
 **ConnectionManager**  
 Seleccione el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] existente que usa el proveedor de datos .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para conectarse a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla o la vista con la que se generará el perfil.  
  
 **TableOrView**  
 Seleccione la tabla o vista cuyo perfil se va a generar.  
  
 Para obtener más información, vea la sección "Opciones de TableorView" en este tema.  
  
 **KeyColumns**  
 Seleccione la columna o columnas existente que se van a incluir en los perfiles. Seleccione **(\*)** para generar un perfil de todas las columnas.  
  
 Para obtener más información, vea las secciones "Selección de columnas para la propiedad KeyColumns" y "Opciones de KeyColumns" en este tema.  
  
#### <a name="tableorview-options"></a>Opciones de TableOrView  
 **Esquema**  
 Especifique el esquema al que pertenece la tabla seleccionada. Esta opción es de solo lectura.  
  
 **Table**  
 Muestra el nombre de la tabla seleccionada. Esta opción es de solo lectura.  
  
#### <a name="keycolumns-options"></a>Opciones de KeyColumns  
 Las opciones siguientes se presentan para cada columna seleccionada para la generación de perfiles en **KeyColumns** o para la opción **(\*)**.  
  
 Para obtener más información, vea la sección "Selección de columnas para la propiedad KeyColumns" anteriormente en este tema.  
  
 **IsWildcard**  
 Especifica si se ha seleccionado el carácter comodín **(\*)**. Esta opción está establecida en **True** si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Es **False** si ha seleccionado una columna individual para la que generar un perfil. Esta opción es de solo lectura.  
  
 **ColumnName**  
 Muestra el nombre de la columna seleccionada. Esta opción está en blanco si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Esta opción es de solo lectura.  
  
 **StringCompareOptions**  
 Seleccione las opciones para comparar los valores de cadena. Esta propiedad presenta las opciones indicadas en la siguiente tabla. El valor predeterminado de esta opción es **Default**.  
  
> [!NOTE]  
>  Al usar un carácter comodín **(\*)** para **ColumnName**, **CompareOptions** es de solo lectura y se establece en el valor **Default**.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Default**|Ordena y compara datos basados en la intercalación de la columna en la tabla de origen.|  
|**BinarySort**|Ordena y compara los datos según los patrones de bits definidos para cada carácter. El orden binario utiliza la distinción de mayúsculas y minúsculas, y de acentos. El orden binario es también el más rápido.|  
|**DictionarySort**|Ordena y compara los datos según el orden y las reglas de comparación definidas en los diccionarios del idioma o alfabeto asociado.|  
  
 Si selecciona **DictionarySort**, también puede seleccionar cualquier combinación de las opciones enumeradas en la tabla siguiente. De forma predeterminada, no se selecciona ninguna de estas opciones adicionales.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**IgnoreCase**|Especifica si la comparación distingue entre mayúsculas y minúsculas. Si se establece esta opción, la comparación de las cadenas omite la distinción entre mayúsculas y minúsculas. Por ejemplo, "ABC" se interpreta igual que "abc".|  
|**IgnoreNonSpace**|Especifica si la comparación distingue entre caracteres con espacio y signos diacríticos. Si se establece esta opción, la comparación omite los signos diacríticos. Por ejemplo, "å" se considera igual que "a".|  
|**IgnoreKanaType**|Especifica si la comparación distingue entre los dos tipos de caracteres kana japoneses: hiragana y katakana. Si se establece esta opción, la comparación de las cadenas omite los tipos de caracteres kana.|  
|**IgnoreWidth**|Especifica si la comparación distingue entre un carácter de un solo byte y el mismo carácter cuando se representa con un carácter de doble byte. Si se establece esta opción, la comparación de las cadenas trata las representaciones de un solo byte y de doble byte del mismo carácter como idénticas.|  
  
### <a name="general-options"></a>Opciones generales  
 **IdSolicitud**  
 Escriba un nombre descriptivo para identificar esta solicitud de perfil. Generalmente, no tiene que cambiar el valor generado automáticamente.  
  
### <a name="options"></a>Opciones  
 **ThresholdSetting**  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla. El valor predeterminado de esta propiedad es **Specified**.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Ninguno**|No se especificó un umbral. El nivel de la clave se notifica independientemente de su valor.|  
|**Specified**|Un umbral se especifica en **KeyStrengthThreshold**. Solo se notifica el nivel de clave si es mayor que el umbral.|  
|**Exact**|No se especificó un umbral. Solo se notifica el nivel de clave si las columnas seleccionadas son una clave exacta.|  
  
 **KeyStrengthThreshold**  
 Especifique el umbral (con un valor entre 0 y 1) por encima del que se debería notificar un nivel de clave. El valor predeterminado de esta propiedad es 0,95. Esta opción solo se habilita cuando la opción **Specified** se selecciona como **KeyStrengthThresholdSetting**.  
  
 **MaxNumberOfViolations**  
 Especifique el número máximo de infracciones de las claves candidatas que van a notificarse en la salida. El valor predeterminado de esta propiedad es 100. Esta opción está deshabilitada cuando se selecciona **Exact** como **KeyStrengthThresholdSetting**.  
  
## <a name="see-also"></a>Vea también  
 [Editor de la tarea de generación de perfiles de datos &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)   
 [Formulario de perfil rápido de tabla única &#40;tarea de generación de perfiles de datos&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
