---
title: Opciones de Solicitud de perfil de dependencia funcional (tarea de generación de perfiles de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 6eb853aa-8016-490c-be4f-06ab8d7f5021
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a1117cc82dee86fa845dc817a7c98eaefe7e4548
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="functional-dependency-profile-request-options-data-profiling-task"></a>Opciones de Solicitud de perfil de dependencia funcional (tarea de generación de perfiles de datos)
  Utilice el panel **Propiedades de la solicitud** de la página **Solicitudes de perfil** para establecer las opciones de **Solicitud de perfil de dependencia funcional** seleccionadas en el panel de solicitudes. Un perfil de dependencia funcional informa de hasta qué punto los valores de una columna (la columna dependiente) dependen de los valores de otra columna o de un conjunto de columnas (la columna determinante). Este perfil también puede ayudarle a identificar problemas de los datos, por ejemplo valores que no sean válidos. Por ejemplo, imagine que genera un perfil de la dependencia entre una columna de código postal y una columna de estados de Estados Unidos. En este perfil, el mismo código postal debería tener siempre el mismo estado, pero el perfil detecta infracciones de la dependencia.  
  
> [!NOTE]  
>  Las opciones que se describen en este tema aparecen en la página **Solicitudes de perfil** del **Editor de tareas de generación de perfiles de datos**. Para obtener más información sobre esta página del editor, vea [Editor de tareas de generación de perfiles de datos &#40;página Solicitudes de perfil&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Para más información sobre cómo usar la tarea de generación de perfiles de datos, vea [Configuración de la Tarea de generación de perfiles de datos](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obtener más información sobre cómo usar el Visor de perfil de datos para analizar la salida de la tarea de generación de perfiles de datos, vea [Visor de perfil de datos](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="understanding-the-selection-of-determinant-and-dependent-columns"></a>Selección de las columnas determinante y dependiente  
 Una **Solicitud de perfil de dependencia funcional** calcula el grado en que la columna o conjunto de columnas del lado determinante (especificadas en la propiedad **DeterminantColumns** ) determina el valor de la columna del lado dependiente (que se especifica en la propiedad **DependentColumn** ). Por ejemplo, una columna de estados de Estados Unidos debería ser funcionalmente dependiente de una columna de códigos postales de Estados Unidos. Es decir, si el código postal (columna determinante) es 98052, el estado (columna dependiente) siempre debería ser Washington.  
  
 Para el lado determinante, puede especificar una columna o un conjunto de columnas en la propiedad **DeterminantColumns** . Por ejemplo, considere una tabla de ejemplo que contenga las columnas A, B y C. Puede hacer las selecciones siguientes para la propiedad **DeterminantColumns** :  
  
-   Al seleccionar el carácter comodín **(\*)**, la tarea de generación de perfiles de datos prueba cada columna como lado determinante de la dependencia.  
  
-   Al seleccionar el carácter comodín **(\*)** y otra columna o columnas, la tarea de generación de perfiles de datos prueba cada combinación de columnas como lado determinante de la dependencia. Por ejemplo, considere una tabla de ejemplo que contiene las columnas A, B y C. Si especifica **(\*)** y la columna C como el valor de la propiedad **DeterminantColumns**, la tarea de generación de perfiles de datos prueba las combinaciones (A, C) y (B, C) como el lado determinante de la dependencia.  
  
 Para el lado dependiente, puede especificar una columna única o el carácter comodín **(\*)** en la propiedad **DependentColumn**. Al seleccionar **(\*)**, la tarea de generación de perfiles de datos prueba la columna o conjunto de columnas del lado determinante con cada columna.  
  
> [!NOTE]  
>  Si selecciona **(\*)**, esta opción podría provocar un gran número de cálculos y disminuir el rendimiento de la tarea. Sin embargo, si la tarea encuentra un subconjunto que satisface el umbral para una dependencia funcional, la tarea no analiza las combinaciones adicionales. Por ejemplo, en la tabla de ejemplo descrita anteriormente, si la tarea determina que la columna C es una columna determinante, no sigue analizando los candidatos compuestos.  
  
## <a name="request-properties-options"></a>Opciones de Propiedades de la solicitud  
 Para cada **Solicitud de perfil de dependencia funcional**, el panel **Propiedades de la solicitud** muestra los grupos de opciones siguientes:  
  
-   **Data**, que incluye las opciones **DeterminantColumns** y **DependentColumn** .  
  
-   **General**  
  
-   **Opciones**  
  
### <a name="data-options"></a>Opciones de Data  
 **ConnectionManager**  
 Seleccione el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] existente que usa el proveedor de datos .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para conectarse a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla o la vista con la que se generará el perfil.  
  
 **TableOrView**  
 Seleccione la tabla o vista cuyo perfil se va a generar.  
  
 **DeterminantColumns**  
 Seleccione la columna o conjunto de columnas determinantes. Es decir, seleccione la columna o conjunto de columnas cuyos valores determinan el valor de la columna dependiente.  
  
 Para obtener más información, vea las secciones, "Selección de las columnas determinante y dependiente" y "Opciones DeterminantColumns y DependentColumn", en este tema.  
  
 **DependentColumn**  
 Seleccione la columna dependiente. Es decir, seleccione la columna cuyo valor se determina mediante el valor de la columna o conjunto de columnas del lado determinante.  
  
 Para obtener más información, vea las secciones, "Selección de las columnas determinante y dependiente" y "Opciones DeterminantColumns y DependentColumn", en este tema.  
  
#### <a name="determinantcolumns-and-dependentcolumn-options"></a>Opciones DeterminantColumns y DependentColumn  
 Las opciones siguientes se presentan para cada columna seleccionada para generar un perfil en **DeterminantColumns** y **DependentColumn**.  
  
 Para obtener más información, vea la sección "Selección de las columnas determinante y dependiente" anteriormente en este tema.  
  
 **IsWildCard**  
 Especifica si se ha seleccionado el carácter comodín **(\*)**. Esta opción está establecida en **True** si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Es **False** si ha seleccionado una columna individual para la que generar un perfil. Esta opción es de solo lectura.  
  
 **ColumnName**  
 Muestra el nombre de la columna seleccionada. Esta opción está en blanco si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Esta opción es de solo lectura.  
  
 **StringCompareOptions**  
 Seleccione las opciones para comparar los valores de cadena. Esta propiedad presenta las opciones indicadas en la siguiente tabla. El valor predeterminado de esta opción es **Default**.  
  
> [!NOTE]  
>  Cuando use el carácter comodín **(\*)** para **ColumnName**, **CompareOptions** es de solo lectura y se establece en el valor **Default**.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Default**|Ordena y compara datos basados en la intercalación de la columna en la tabla de origen.|  
|**BinarySort**|Ordena y compara los datos según los patrones de bits definidos para cada carácter. El orden binario utiliza la distinción de mayúsculas y minúsculas, y de acentos. El orden binario es también el más rápido.|  
|**DictionarySort**|Ordena y compara los datos según el orden y las reglas de comparación definidas en los diccionarios del idioma o alfabeto asociado.|  
  
 Si selecciona **DictionarySort**, también puede seleccionar cualquier combinación de las opciones enumeradas en la tabla siguiente. De forma predeterminada, no se selecciona ninguna de estas opciones adicionales.  
  
|Valor|Description|  
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
 Especifique el valor de umbral. El valor predeterminado de esta propiedad es **Specified**.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Ninguno**|No especifica un umbral. El nivel de dependencia funcional se indica independientemente de su valor.|  
|**Specified**|Utilice el umbral que se especifica en **FDStrengthThreshold**. Solo se indica el nivel de dependencia funcional si es mayor que el umbral.|  
|**Exact**|No especifica un umbral. El nivel de dependencia funcional solo se indica si la dependencia funcional entre las columnas seleccionadas es exacta.|  
  
 **FDStrengthThreshold**  
 Especifique el umbral (con un valor entre 0 y 1) por encima del que se debería notificar un nivel de dependencia funcional. El valor predeterminado de esta propiedad es 0,95. Esta opción solo se habilita cuando la opción **Specified** se selecciona como **ThresholdSetting**.  
  
 **MaxNumberOfViolations**  
 Especifique el número máximo de infracciones de la dependencia funcional que va a notificarse en la salida. El valor predeterminado de esta propiedad es 100. Esta opción se deshabilita cuando la opción **Exact** se selecciona como **ThresholdSetting**.  
  
## <a name="see-also"></a>Ver también  
 [Editor de tareas de generación de perfiles de datos &#40;página General&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Formulario de perfil rápido de tabla única &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
