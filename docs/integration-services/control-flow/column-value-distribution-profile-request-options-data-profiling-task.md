---
title: "Opciones de solicitud (tarea de generación de perfiles de datos) para el perfil de distribución de valor columna | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c1e5f5de-04f5-4d00-a9f0-55817186bdf9
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 79ce587ac6e1f0da8bf0c2ae237b6b9c3ae2623f
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="column-value-distribution-profile-request-options-data-profiling-task"></a>Opciones de Solicitud de perfil de distribución de valores de columna (tarea de generación de perfiles de datos)
  Utilice el panel **Propiedades de la solicitud** de la página **Solicitudes de perfil** para establecer las opciones de **Solicitud de perfil de distribución de valores de columna** seleccionadas en el panel de solicitudes. Un perfil de distribución de valores de columna notifica todos los valores distintos en la columna seleccionada y el porcentaje de filas en la tabla que cada valor representa. El perfil también puede notificar los valores que representan más de un porcentaje especificado de filas en la tabla. Este perfil puede ayudarle a identificar problemas en los datos, por ejemplo un número incorrecto de valores distintos en una columna. Por ejemplo, genera un perfil de una columna de estados de Estados Unidos y detecta más de 50 valores distintos.  
  
> [!NOTE]  
>  Las opciones que se describen en este tema aparecen en la página **Solicitudes de perfil** del **Editor de tareas de generación de perfiles de datos**. Para obtener más información sobre esta página del editor, vea [Editor de tareas de generación de perfiles de datos &#40;página Solicitudes de perfil&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Para obtener más información sobre cómo usar la tarea de generación de perfiles de datos, vea [Configuración de la Tarea de generación de perfiles de datos](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obtener más información sobre cómo usar el Visor de perfil de datos para analizar la salida de la tarea de generación de perfiles de datos, vea [Visor de perfil de datos](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="request-properties-options"></a>Opciones de Propiedades de la solicitud  
 Para una **Solicitud de perfil de distribución de valores de columna**, el panel **Propiedades de la solicitud** muestra los grupos siguientes de opciones:  
  
-   **Data**, que incluye las opciones **TableOrView** y **Column**  
  
-   **General**  
  
-   **Opciones**  
  
### <a name="data-options"></a>Opciones de Data  
 **ConnectionManager**  
 Seleccione el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] existente que usa el Proveedor de datos .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) con el fin de conectarse a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla o la vista con la que se va a generar el perfil.  
  
 **TableOrView**  
 Seleccione la tabla o vista existente que contenga la columna de la que se va a generar un perfil.  
  
 Para obtener más información, vea la sección "Opciones de TableorView" en este tema.  
  
 **Column**  
 Seleccione la columna existente de la que se va a generar un perfil. Seleccione **(\*)** para generar un perfil de todas las columnas.  
  
 Para obtener más información, vea la sección "Opciones de Column" en este tema.  
  
#### <a name="tableorview-options"></a>Opciones de TableOrView  
 **Esquema**  
 Especifica el esquema al que pertenece la tabla seleccionada. Esta opción es de solo lectura.  
  
 **Table**  
 Muestra el nombre de la tabla seleccionada. Esta opción es de solo lectura.  
  
#### <a name="column-options"></a>Opciones de Column  
 **IsWildCard**  
 Especifica si se ha seleccionado el carácter comodín **(\*)**. Esta opción está establecida en **True** si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Es **False** si ha seleccionado una columna individual para la que generar un perfil. Esta opción es de solo lectura.  
  
 **ColumnName**  
 Muestra el nombre de la columna seleccionada. Esta opción está en blanco si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Esta opción es de solo lectura.  
  
 **StringCompareOptions**  
 Seleccione las opciones para comparar los valores de cadena. Esta propiedad presenta las opciones indicadas en la siguiente tabla. El valor predeterminado de esta opción es **Default**.  
  
> [!NOTE]  
>  Si el carácter comodín **(\*)** se usa para **ColumnName**, **CompareOptions** es de solo lectura y se establece en el valor **Default**.  
  
|Value|Description|  
|-----------|-----------------|  
|**Default**|Ordena y compara datos basados en la intercalación de la columna en la tabla de origen.|  
|**BinarySort**|Ordena y compara los datos según los patrones de bits definidos para cada carácter. El orden binario utiliza la distinción de mayúsculas y minúsculas, y de acentos. El orden binario es también el más rápido.|  
|**DictionarySort**|Ordena y compara los datos según el orden y las reglas de comparación definidas en los diccionarios del idioma o alfabeto asociado.|  
  
 Si selecciona **DictionarySort**, también puede seleccionar cualquier combinación de las opciones enumeradas en la tabla siguiente. De forma predeterminada, no se selecciona ninguna de estas opciones adicionales.  
  
|Value|Description|  
|-----------|-----------------|  
|**IgnoreCase**|Especifica si la comparación distingue entre mayúsculas y minúsculas. Si se establece esta opción, la comparación de las cadenas omite la distinción entre mayúsculas y minúsculas. Por ejemplo, "ABC" se interpreta igual que "abc".|  
|**IgnoreNonSpace**|Especifica si la comparación distingue entre caracteres con espacio y signos diacríticos. Si se establece esta opción, la comparación omite los signos diacríticos. Por ejemplo, "å" se considera igual que "a".|  
|**IgnoreKanaType**|Especifica si la comparación distingue entre los dos tipos de caracteres kana japoneses: hiragana y katakana. Si se establece esta opción, la comparación de las cadenas omite los tipos de caracteres kana.|  
|**IgnoreWidth**|Especifica si la comparación distingue entre un carácter de un solo byte y el mismo carácter cuando se representa con un carácter de doble byte. Si se establece esta opción, la comparación de las cadenas trata las representaciones de un solo byte y de doble byte del mismo carácter como idénticas.|  
  
### <a name="general-options"></a>Opciones de General  
 **IdSolicitud**  
 Escriba un nombre descriptivo para identificar esta solicitud de perfil. Generalmente, no tiene que cambiar el valor generado automáticamente.  
  
### <a name="options"></a>Opciones  
 **ValueDistributionOption**  
 Especifique si calcular la distribución para todos los valores de las columna. El valor predeterminado de esta opción es **FrequentValues**.  
  
|Value|Description|  
|-----------|-----------------|  
|**AllValues**|La distribución se calcula para todos los valores de las columnas.|  
|**FrequentValues**|La distribución solo se calcula para los valores cuya frecuencia supera el valor mínimo especificado en **FrequentValueThreshold**. Los valores que no cumplen **FrequentValueThreshold** se excluyen del informe de salida.|  
  
 **FrequentValueThreshold**  
 Especifique el umbral (con un valor entre 0 y 1) por encima del que se debería notificar el valor de la columna. Esta opción está deshabilitada al seleccionar **AllValues** como **ValueDistributionOption**. El valor predeterminado de esta opción es 0.001.  
  
## <a name="see-also"></a>Vea también  
 [Editor de la tarea &#40; de la generación de perfiles de datos Página general &#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Formulario de perfil rápido de tabla única &#40; datos de generación de perfiles de tarea &#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  

