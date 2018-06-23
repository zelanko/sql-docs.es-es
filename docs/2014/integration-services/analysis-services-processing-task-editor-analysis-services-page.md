---
title: Editor de la tarea de procesamiento (página Analysis Services) de Analysis Services | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing Task Editor
ms.assetid: 5612be78-57cf-4e4e-92cf-6bfa9f971040
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 2501594838b9113b8ec787030033272d3e011682
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203464"
---
# <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Editor de la tarea de procesamiento de Analysis Services (página Analysis Services)
  Utilice la página **Analysis Services** del cuadro de diálogo **Editor de la tarea de procesamiento de Analysis Services** para especificar un administrador de conexiones de Analysis Services, seleccionar los objetos analíticos que se deben procesar y establecer opciones de procesamiento y control de errores.  
  
 Al procesar modelos tabulares, tenga en cuenta lo siguiente:  
  
1.  No puede realizar análisis de impacto en modelos tabulares.  
  
2.  Algunas opciones de procesamiento para el modo tabular no están expuestas como, por ejemplo, el proceso de desfragmentación y el proceso de recálculo. Puede llevar a cabo estas funciones mediante la tarea Ejecutar DDL.  
  
3.  Algunas opciones de procesamiento proporcionadas, como índices de proceso, no son adecuadas para los modelos tabulares y no deben utilizarse.  
  
4.  Los valores de las operaciones por lotes se omiten para los modelos tabulares.  
  
 Para obtener información acerca de esta tarea, vea [Analysis Services Processing Task](control-flow/analysis-services-processing-task.md).  
  
## <a name="options"></a>Opciones  
 **administrador de conexiones de Analysis Services**  
 Seleccione un administrador de conexiones de Analysis Services de la lista o haga clic en **Nuevo** para crear uno.  
  
 **Nueva**  
 Cree un administrador de conexiones de Analysis Services nuevo.  
  
 **Temas relacionados:** [Analysis Services Connection Manager](connection-manager/analysis-services-connection-manager.md), [Referencia de la interfaz de usuario del cuadro de diálogo Agregar administrador de conexiones con Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Lista de objetos**  
 |Property|Descripción|  
|--------------|-----------------|  
|**Nombre de objeto**|Enumera los nombres de los objetos especificados.|  
|**Tipo**|Enumera los tipos de los objetos especificados.|  
|**Opciones de proceso**|Seleccione una opción de procesamiento de la lista.<br /><br /> **Temas relacionados**: [procesamiento de objetos de modelo Multidimensional](../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)|  
|**Configuración**|Enumera los valores de configuración de procesamiento para los objetos especificados.|  
  
 **Agregar**  
 Agregue un objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a la lista.  
  
 **Quitar**  
 Seleccione un objeto y haga clic en **Eliminar**.  
  
 **Análisis de impacto**  
 Lleve a cabo el análisis de impacto en el objeto seleccionado.  
  
 **Temas relacionados:** [Cuadro de diálogo Análisis de impacto &#40;Analysis Services - Datos multidimensionales&#41;](../../2014/analysis-services/impact-analysis-dialog-box-analysis-services-multidimensional-data.md)  
  
 **Resumen de configuración de lotes**  
 |Property|Descripción|  
|--------------|-----------------|  
|**Orden de procesamiento**|Especifica si los objetos se procesan de manera secuencial o en un lote; si se utiliza el procesamiento paralelo, especifica el número de objetos que se deben procesar simultáneamente.|  
|**Modo de transacción**|Especifica el modo de transacción para el procesamiento secuencial.|  
|**Errores de dimensión**|Especifica el comportamiento de la tarea cuando se produce un error.|  
|**Ruta del registro de errores de claves de dimensiones**|Especifica la ruta de acceso del archivo en el que se registran los errores.|  
|**Procesar objetos afectados**|Indica si los objetos afectados o dependientes también se deben procesar.|  
  
 **Cambiar configuración**  
 Cambie las opciones de procesamiento y el control de errores en las claves de dimensiones.  
  
 **Temas relacionados:** [Cuadro de diálogo Cambiar configuración &#40;Analysis Services - Datos multidimensionales&#41;](../../2014/analysis-services/change-settings-dialog-box-analysis-services-multidimensional-data.md)  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de la tarea de procesamiento de Analysis Services &#40;página General&#41;](general-page-of-integration-services-designers-options.md)   
 [Tarea Ejecutar DDL de Analysis Services](control-flow/analysis-services-execute-ddl-task.md)  
  
  