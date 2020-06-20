---
title: Opciones de Solicitud de perfil de proporción de columnas nulas (tarea de generación de perfiles de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling Task Editor
ms.assetid: 157ef8e4-fd23-4f81-8194-eebf74e9fd86
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2c8efa2db8a602b2cbed08e8731c4137a132495f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84919631"
---
# <a name="column-null-ratio-profile-request-options-data-profiling-task"></a>Opciones de Solicitud de perfil de proporción de columnas nulas (tarea de generación de perfiles de datos)
  Utilice el panel **Propiedades de la solicitud** de la página **Solicitudes de perfil** para establecer las opciones de **Solicitud de perfil de proporción de columnas nulas** seleccionadas en el panel de solicitudes. Un perfil de proporción de columnas nulas indica el porcentaje de valores nulos de la columna seleccionada. Este perfil puede ayudarle a identificar problemas en los datos, por ejemplo una proporción inesperadamente alta de valores nulos en una columna. Por ejemplo, un perfil de proporción de columnas nulas puede generar un perfil de una columna de códigos postales y detectar que falta un porcentaje inaceptablemente alto de códigos postales.  
  
> [!NOTE]  
>  Las opciones que se describen en este tema aparecen en la página **Solicitudes de perfil** del **Editor de tareas de generación de perfiles de datos**. Para obtener más información sobre esta página del editor, vea [Editor de tareas de generación de perfiles de datos &#40;página Solicitudes de perfil&#41;](data-profiling-task-editor-profile-requests-page.md).  
  
 Para más información sobre cómo usar la tarea de generación de perfiles de datos, vea [Configuración de la Tarea de generación de perfiles de datos](data-profiling-task.md). Para obtener más información sobre cómo usar el Visor de perfil de datos para analizar la salida de la tarea de generación de perfiles de datos, vea [Visor de perfil de datos](data-profile-viewer.md).  
  
## <a name="request-properties-options"></a>Opciones de Propiedades de la solicitud  
 Para cada **Solicitud de perfil de proporción de columnas nulas**, el panel **Propiedades de la solicitud** muestra los grupos de opciones siguientes:  
  
-   **Data**, que incluye las opciones **TableOrView** y **Column**  
  
-   **General**  
  
### <a name="data-options"></a>Opciones de Data  
 **ConnectionManager**  
 Seleccione el administrador de conexiones de [!INCLUDE[vstecado](../../includes/vstecado-md.md)] existente que usa el proveedor de datos .NET para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) con el fin de conectarse a la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene la tabla o la vista con la que se va a generar el perfil.  
  
 **TableOrView**  
 Seleccione la tabla o vista existente que contenga la columna de la que se va a generar un perfil.  
  
 Para obtener más información, vea la sección "Opciones de TableorView" en este tema.  
  
 **Columna**  
 Seleccione la columna existente de la que se va a generar un perfil. Seleccione **(\*)** para generar un perfil de todas las columnas.  
  
 Para obtener más información, vea la sección "Opciones de Column" en este tema.  
  
#### <a name="tableorview-options"></a>Opciones de TableOrView  
 **Esquema**  
 Especifica el esquema al que pertenece la tabla seleccionada. Esta opción es de solo lectura.  
  
 **Table**  
 Muestra el nombre de la tabla seleccionada. Esta opción es de solo lectura.  
  
#### <a name="column-options"></a>Opciones de Column  
 **IsWildCard**  
 Especifica si se ha seleccionado el carácter comodín **(\*)** . Esta opción está establecida en **True** si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Es **False** si ha seleccionado una columna individual para la que generar un perfil. Esta opción es de solo lectura.  
  
 **ColumnName**  
 Muestra el nombre de la columna seleccionada. Esta opción está en blanco si ha seleccionado **(\*)** para generar un perfil de todas las columnas. Esta opción es de solo lectura.  
  
 **StringCompareOptions**  
 Esta opción no se aplica al Perfil de proporción de columnas nulas.  
  
### <a name="general-options"></a>Opciones generales  
 **IdSolicitud**  
 Escriba un nombre descriptivo para identificar esta solicitud de perfil. Generalmente, no tiene que cambiar el valor generado automáticamente.  
  
## <a name="see-also"></a>Consulte también  
 [Editor de tareas de generación de perfiles de datos &#40;página General&#41;](../general-page-of-integration-services-designers-options.md)   
 [Formulario de perfil rápido de tabla única &#40;tarea de generación de perfiles de datos&#41;](single-table-quick-profile-form-data-profiling-task.md)  
  
  
