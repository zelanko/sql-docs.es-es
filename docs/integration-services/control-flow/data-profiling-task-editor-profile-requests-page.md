---
title: "Editor de tareas de generación de perfiles de datos (página Solicitudes de perfil) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataprofilingtask.profilerequests.f1
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: c72acb3d-380e-436e-8041-ed364eddfabd
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e6883b8ec802392c0ae4d3a92a41f54433d403f8
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="data-profiling-task-editor-profile-requests-page"></a>Editor de tareas de generación de perfiles de datos (página Solicitudes de perfil)
  Use la página **Solicitudes de perfil** del **Editor de tareas de generación de perfiles de datos** para seleccionar y configurar los perfiles que desee calcular. En una única tarea de generación de perfiles puede calcular varias filas para varias columnas o combinaciones de columnas en varias tablas o vistas.  
  
 Para obtener más información sobre cómo usar la tarea de generación de perfiles de datos, vea [Configuración de la Tarea de generación de perfiles de datos](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obtener más información sobre cómo usar el Visor de perfil de datos para analizar la salida de la tarea de generación de perfiles de datos, vea [Visor de perfil de datos](../../integration-services/control-flow/data-profile-viewer.md).  
  
 **Para abrir la página Solicitudes de perfil del Editor de tareas de generación de perfiles de datos**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que tiene la tarea de generación de perfiles de datos.  
  
2.  En la pestaña **Flujo de control** , haga doble clic en la tarea de generación de perfiles de datos.  
  
3.  En el **Editor de tareas de generación de perfiles de datos**, haga clic en **Solicitudes de perfil**.  
  
## <a name="using-the-requests-pane"></a>Usar el panel de solicitudes  
 El panel de solicitudes es el que aparece en la parte superior de la página. En este panel se enumeran todos los perfiles configurados para la tarea de generación de perfiles de datos actual. Si no se ha configurado ningún perfil, el panel de solicitudes está vacío. Para agregar un perfil nuevo, haga clic en un área vacía en la columna **Tipo de perfil** y seleccione un tipo de perfil en la lista. Para configurar un perfil, selecciónelo en el panel de solicitudes y, a continuación, establezca las propiedades del perfil en el panel **Propiedades de la solicitud** .  
  
### <a name="requests-pane-options"></a>Opciones del panel de solicitudes  
 El panel de solicitudes tiene las opciones siguientes:  
  
 **Ver**  
 Seleccione si ver todos los perfiles configurados para la tarea o simplemente uno de los perfiles.  
  
 Las columnas del panel de solicitudes cambia según la **Vista** que seleccione. Para obtener más información sobre cada una de esas columnas, consulte la sección siguiente, "Columnas del panel de solicitudes".  
  
### <a name="requests-pane-columns"></a>Columnas del panel de solicitudes  
 Las columnas que muestra el panel de solicitudes dependen de la **Vista** que haya seleccionado:  
  
-   Si selecciona ver **Todas las solicitudes**, el panel de solicitudes tiene dos columnas: **Tipo de perfil** e **Id. de solicitud**.  
  
-   Si selecciona ver uno de los cinco perfiles de columna, el panel de solicitud tiene cuatro columnas: **Tipo de perfil**, **Tabla o vista**, **Columna**e **Id. de solicitud**.  
  
-   Si selecciona ver un perfil de claves candidatas, el panel de solicitudes tiene cuatro columnas: **Tipo de perfil**, **Tabla o vista**, **Columnas de clave**e **Id. de solicitud**.  
  
-   Si selecciona ver un perfil de dependencia funcional, el panel de solicitudes tiene cinco columnas: **Tipo de perfil**, **Tabla o vista**, **Columnas determinantes**, **Columna dependiente**e **Id. de solicitud**.  
  
-   Si selecciona ver un perfil de inclusión de valores, el panel de solicitudes tiene seis columnas: **Tipo de perfil**, **Tabla o vista de subconjuntos**, **Tabla o vista de superconjuntos**, **Columnas de subconjunto**, **Columnas de superconjunto**e **Id. de solicitud**.  
  
 En las secciones siguientes se describe cada una de esas columnas.  
  
#### <a name="columns-common-to-all-views"></a>Columnas comunes a todas las vistas  
 **Tipo de perfil**  
 Seleccione un perfil de datos en las opciones siguientes:  
  
|Valor|Description|  
|-----------|-----------------|  
|**Solicitud de perfil de claves candidatas**|Calcule un perfil de claves candidatas.<br /><br /> Este perfil notifica si una columna o conjunto de columnas es una clave, o una clave aproximada, para la tabla seleccionada. Este perfil también puede ayudarle a identificar problemas de los datos, por ejemplo valores en una posible columna de clave.|  
|**Solicitud de perfil de distribución de longitud de columnas**|Calcule un perfil de distribución de longitud de columnas.<br /><br /> El perfil de distribución de longitud de columnas indica las diferentes longitudes de los valores de cadena de la columna seleccionada y el porcentaje de filas de la tabla que cada longitud representa. Este perfil puede ayudarle a identificar los problemas de los datos, por ejemplo valores que no sean válidos. Por ejemplo, genera un perfil de una columna de códigos de estados de Estados Unidos de dos caracteres y detecta valores menores de dos caracteres.|  
|**Solicitud de perfil de proporción de columnas nulas**|Calcule un perfil de proporción de columnas nulas.<br /><br /> El perfil de proporción de columnas nulas notifica el porcentaje de valores nulos en la columna seleccionada. Este perfil puede ayudarle a identificar problemas en los datos, por ejemplo una proporción inesperadamente alta de valores nulos en una columna. Por ejemplo, genera un perfil de una columna de códigos postales y detecta un porcentaje inaceptablemente alto de códigos que faltan.|  
|**Solicitud de perfil de patrón de columnas**|Calcule un perfil de patrón de columnas.<br /><br /> El perfil de patrón de columnas notifica un conjunto de expresiones regulares que cubren el porcentaje especificado de valores en una columna de cadenas. Este perfil puede ayudarle también a identificar problemas de los datos, por ejemplo cadenas que no sean válidas. Este perfil también puede sugerir expresiones regulares que se pueden usar en el futuro para validar los valores nuevos. Por ejemplo, un perfil de patrón de una columna de códigos postales podría generar las expresiones regulares \d{5}-\d{4}, \d{5} y \d{9}. Si ve otras expresiones regulares, es posible que los datos contengan valores no válidos o tengan un formato incorrecto.|  
|**Solicitud de perfil de estadísticas de columnas**|Seleccione esta opción para calcular un perfil de estadísticas de columnas utilizando la configuración predeterminada para todas las columnas aplicables de la tabla o vista seleccionada.<br /><br /> El perfil de estadísticas de columnas notifica estadísticas, como los valores mínimo, máximo y promedio, y la desviación estándar para las columnas numéricas, y los valores mínimo y máximo para las columnas **datetime** . Este perfil puede ayudarle a identificar problemas de los datos, por ejemplo fechas que no sean válidas. Por ejemplo, genera un perfil de una columna de fechas históricas y detecta una fecha máxima futura.|  
|**Solicitud de perfil de distribución de valores de columna**|Calcule un perfil de distribución de valores de columnas.<br /><br /> El perfil de distribución de valores de columnas notifica todos los valores distintos en la columna seleccionada y el porcentaje de filas en la tabla que cada valor representa. Este perfil también puede notificar valores que representan más de un porcentaje especificado en la tabla. Este perfil puede ayudarle a identificar problemas en los datos, por ejemplo un número incorrecto de valores distintos en una columna. Por ejemplo, suponga que genera un perfil de una columna que contiene los estados de Estados Unidos y detecta más de 50 valores distintos.|  
|**Solicitud de perfil de dependencia funcional**|Calcule un perfil de dependencia funcional.<br /><br /> El perfil de dependencia funcional notifica hasta qué punto los valores de una columna (la columna dependiente) dependen de los valores de otra columna o de un conjunto de columnas (la columna determinante). Este perfil puede ayudarle también a identificar problemas de los datos, por ejemplo valores que no sean válidos. Por ejemplo, suponga que genera un perfil de la dependencia entre una columna de códigos postales de Estados Unidos y una columna de los estados. El mismo código postal debería tener siempre el mismo estado, pero el perfil detecta infracciones de esta dependencia.|  
|**Solicitud de perfil de inclusión de valores**|Calcule un perfil de inclusión de valores.<br /><br /> El perfil de inclusión de valores calcula la superposición en los valores entre dos columnas o conjuntos de columnas. Este perfil también puede determinar si una columna o un conjunto de columnas es adecuado para actuar como una clave externa entre las tablas seleccionadas. Este perfil puede ayudarle igualmente a identificar problemas de los datos, por ejemplo valores que no sean válidos. Por ejemplo, puede generar el perfil de una columna de identificadores de producto de una tabla de ventas y detectar que dicha columna contiene valores que no se encuentran en la columna de identificadores de producto de la tabla de productos.|  
  
 **IdSolicitud**  
 Muestra el identificador de la solicitud. Generalmente, no tiene que cambiar el valor generado automáticamente.  
  
#### <a name="columns-common-to-all-individual-profiles"></a>Columnas comunes a todos los perfiles individuales  
 **Connection Manager**  
 Muestra el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que conecta con la base de datos de origen.  
  
 **Id. de solicitud**  
 Muestra un identificador para la solicitud. Generalmente, no tiene que cambiar el valor generado automáticamente.  
  
#### <a name="columns-common-to-the-five-individual-column-profiles"></a>Columnas comunes a los cinco perfiles de columnas individuales  
 **Tabla o vista**  
 Muestra la tabla o la vista que contiene la columna seleccionada.  
  
 **Columna**  
 Muestra la columna seleccionada para generar perfiles.  
  
#### <a name="columns-specific-to-the-candidate-key-profile"></a>Columnas específicas del perfil de claves candidatas  
 **Tabla o vista**  
 Muestra la tabla o la vista que contiene las columnas seleccionadas.  
  
 **Columnas de clave**  
 Muestra las columnas seleccionada para generar perfiles.  
  
#### <a name="columns-specific-to-the-functional-dependency-profile"></a>Columnas específicas del perfil de dependencia funcional  
 **Tabla o vista**  
 Muestra la tabla o la vista que contiene las columnas seleccionadas.  
  
 **Columnas determinantes**  
 Muestra las columnas seleccionadas para generar el perfil como columna o columnas determinantes. En el ejemplo en el que el código postal de Estados Unidos determina el estado, la columna determinante es la columna de código postal.  
  
 **Dependent column**  
 Muestra las columnas seleccionadas para generar el perfil como columna dependiente. En el ejemplo en el que el código postal de Estados Unidos determina el estado, la columna dependiente es la columna de estado.  
  
#### <a name="columns-specific-to-the-value-inclusion-profile"></a>Columnas específicas del perfil de inclusión de valores  
 **Tabla o vista de subconjuntos**  
 Muestra la tabla o vista que contiene la columna o columnas seleccionadas como columnas de subconjunto.  
  
 **Tabla o vista de superconjuntos**  
 Muestra la tabla o vista que contiene la columna o columnas seleccionadas como columnas de subconjunto.  
  
 **Columnas de subconjunto**  
 Muestra la columna o columnas seleccionadas para generar el perfil como columnas de subconjunto. En el ejemplo en el que se comprueba que los valores de una columna de estados de Estados Unidos se encuentran en una tabla de referencia de códigos de estados de dos caracteres, la columna de subconjunto es la columna de estado de la tabla de origen.  
  
 **Columnas de superconjunto**  
 Muestra la columna o columnas seleccionadas para generar el perfil como columnas de superconjunto. En el ejemplo en el que se comprueba que los valores de una columna de estados de Estados Unidos se encuentran en una tabla de referencia de códigos de estados de dos caracteres, la columna de superconjunto es la columna de códigos de estado de la tabla de referencia.  
  
## <a name="using-the-request-properties-pane"></a>Usar el panel Propiedades de la solicitud  
 El panel **Propiedades de la solicitud** aparece debajo del panel de solicitudes. Este panel muestra las opciones para el perfil que ha seleccionado en el panel de solicitudes.  
  
> [!NOTE]  
>  Después de seleccionar un **Tipo de perfil**, debe seleccionar el campo **Id. de solicitud** para ver las propiedades de la solicitud del perfil en el panel **Propiedades de la solicitud** .  
  
 Estas opciones varían según el perfil seleccionado. Para obtener información acerca de las opciones de tipos de perfiles individuales, vea los temas siguientes:  
  
-   [Opciones de Solicitud de perfil de claves candidatas &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [Opciones de Solicitud de perfil de proporción de columnas nulas &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [Opciones de Solicitud de perfil de estadísticas de columnas &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [Opciones de Solicitud de perfil de distribución de valores de columna &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Opciones de Solicitud de perfil de distribución de longitud de columna &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [Opciones de Solicitud de perfil de patrón de columnas &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [Opciones de Solicitud de perfil de dependencia funcional &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [Opciones de Solicitud de perfil de inclusión de valores &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/value-inclusion-profile-request-options-data-profiling-task.md)  
  
## <a name="see-also"></a>Ver también  
 [Editor de tareas de generación de perfiles de datos &#40;página General&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Formulario de perfil rápido de tabla única &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
