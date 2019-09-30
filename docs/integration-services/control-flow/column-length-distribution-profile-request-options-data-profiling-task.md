---
title: Opciones de Solicitud de perfil de distribución de longitud de columnas (tarea de generación de perfiles de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 1a4de41f-f38d-40ea-ba1b-6c0ef67ea52a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cbaf50dc98962e1053477b0535054917c3719f19
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294241"
---
# <a name="column-length-distribution-profile-request-options-data-profiling-task"></a>Opciones de Solicitud de perfil de distribución de longitud de columnas (tarea de generación de perfiles de datos)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Utilice el panel **Propiedades de la solicitud** de la página **Solicitudes de perfil** para establecer las opciones de **Solicitud de perfil de distribución de longitud de columna** seleccionadas en el panel de solicitudes. Un perfil de distribución de columnas nulas indica las diferentes longitudes de los valores de cadena de la columna seleccionada y el porcentaje de filas de la tabla que cada longitud representa. Este perfil puede ayudarle a identificar los problemas de los datos, por ejemplo valores que no sean válidos. Por ejemplo, genera un perfil de una columna de códigos de estados de Estados Unidos de dos caracteres y detecta valores menores de dos caracteres.  
  
> [!NOTE]  
>  Las opciones que se describen en este tema aparecen en la página **Solicitudes de perfil** del **Editor de tareas de generación de perfiles de datos**. Para obtener más información sobre esta página del editor, vea [Editor de tareas de generación de perfiles de datos &#40;página Solicitudes de perfil&#41;](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md).  
  
 Para más información sobre cómo usar la tarea de generación de perfiles de datos, vea [Configuración de la Tarea de generación de perfiles de datos](../../integration-services/control-flow/setup-of-the-data-profiling-task.md). Para obtener más información sobre cómo usar el Visor de perfil de datos para analizar la salida de la tarea de generación de perfiles de datos, vea [Visor de perfil de datos](../../integration-services/control-flow/data-profile-viewer.md).  
  
## <a name="request-properties-options"></a>Opciones de Propiedades de la solicitud  
 Para una **Solicitud de perfil de distribución de longitud de columnas**, el panel **Propiedades de la solicitud** muestra los grupos siguientes de opciones:  
  
-   **Data**, que incluye las opciones **TableOrView** y **Column**  
  
-   **General**  
  
-   **Opciones**  
  
### <a name="data-options"></a>Opciones de Data  
 **ConnectionManager**  
 Seleccione el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] existente que usa el proveedor de datos .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) para conectarse a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla o la vista con la que se generará el perfil.  
  
 **TableOrView**  
 Seleccione la tabla o vista existente que contenga la columna de la que se va a generar un perfil.  
  
 Para obtener más información, vea la sección "Opciones de TableorView" en este tema.  
  
 **Column**  
 Seleccione la columna existente de la que se va a generar un perfil. Seleccione **(\*)** para generar un perfil de todas las columnas.  
  
 Para obtener más información, vea la sección "Opciones de Column" en este tema.  
  
#### <a name="tableorview-options"></a>Opciones de TableOrView  
 **Esquema**  
 Especifique el esquema al que pertenece la tabla seleccionada. Esta opción es de solo lectura.  
  
 **Table**  
 Muestra el nombre de la tabla seleccionada. Esta opción es de solo lectura.  
  
#### <a name="column-options"></a>Opciones de Column  
 **IsWildCard**  
 Especifica si se ha seleccionado el carácter comodín **(\*)** . Esta opción está establecida en **True** si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Es **False** si ha seleccionado una columna individual para la que generar un perfil. Esta opción es de solo lectura.  
  
 **ColumnName**  
 Muestra el nombre de la columna seleccionada. Esta opción está en blanco si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Esta opción es de solo lectura.  
  
 **StringCompareOptions**  
 Esta opción no se aplica al Perfil de distribución de longitud de columnas.  
  
### <a name="general-options"></a>Opciones generales  
 **IdSolicitud**  
 Escriba un nombre descriptivo para identificar esta solicitud de perfil. Generalmente, no tiene que cambiar el valor generado automáticamente.  
  
### <a name="options"></a>Opciones  
 **IgnoreLeadingSpaces**  
 Indique si omitir los espacios iniciales cuando el perfil compara valores de cadena. El valor predeterminado de esta opción es **False**.  
  
 **IgnoreTrailingSpaces**  
 Indique si omitir los espacios finales cuando el perfil compara valores de cadena. El valor predeterminado de esta opción es **True**.  
  
## <a name="see-also"></a>Consulte también  
 [Editor de tareas de generación de perfiles de datos &#40;página General&#41;](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)   
 [Formulario de perfil rápido de tabla única &#40;tarea de generación de perfiles de datos&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)  
  
  
