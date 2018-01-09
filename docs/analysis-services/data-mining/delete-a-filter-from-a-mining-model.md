---
title: "Eliminar un filtro de un modelo de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: filters [Analysis Services]
ms.assetid: 91220b21-adbc-49a9-b200-8bf0a724eff1
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6352491a172ce751ed2cec28038a085a22c96654
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="delete-a-filter-from-a-mining-model"></a>Eliminar un filtro de un modelo de minería de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Al crear un filtro en un modelo de minería de datos, puede crear modelos en un subconjunto de los datos en la vista del origen de datos. Los filtros también son útiles para probar la precisión del modelo en un subconjunto de los datos originales.  
  
 Sin embargo, debe eliminar el filtro si desea ver de nuevo el conjunto completo de casos. Este procedimiento describe cómo quitar las condiciones de un filtro o eliminar éste por completo.  
  
### <a name="to-delete-a-condition-from-a-filter-on-a-mining-model"></a>Para eliminar una condición de un filtro en un modelo de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el Explorador de soluciones, haga clic en la estructura de minería de datos que contiene el modelo de minería que desea filtrar.  
  
2.  Haga clic en la pestaña **Modelos de minería de datos** .  
  
3.  Seleccione el modelo y haga clic con el botón secundario del mouse para abrir el menú contextual.  
  
     O bien  
  
     Seleccione el modelo. En el menú **Minería de datos** , seleccione **Establecer filtro de modelos**.  
  
4.  En el cuadro de diálogo **Filtro del modelo** , haga clic con el botón derecho en la fila de la cuadrícula que contiene la condición que quiere eliminar.  
  
5.  Seleccione **Eliminar**.  
  
### <a name="to-clear-the-filter-on-a-mining-model-in-the-filter-editor-dialog-box"></a>Para borrar el filtro de un modelo de minería de datos en el cuadro de diálogo Editor de filtros  
  
-   En el cuadro de diálogo **Editor de filtros** , haga clic con el botón derecho en cualquier fila de la cuadrícula y seleccione **Eliminar todos**.  
  
## <a name="working-with-model-filters-using-the-properties-window"></a>Trabajar con filtros de modelo utilizando la ventana Propiedades  
 Si desea eliminar todo el filtro, no necesita abrir los cuadros de diálogo del editor de filtros. Las condiciones de filtrado que creó están disponibles en la propiedad **Filter** del modelo de minería de datos.  
  
> [!NOTE]  
>  Puede ver las propiedades de un modelo de minería de datos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], pero no en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-clear-the-filter-on-a-mining-model-in-solution-explorer"></a>Para borrar el filtro de un modelo de minería de datos en el Explorador de soluciones  
  
1.  En el Explorador de soluciones, haga clic en el modelo de minería de datos que contiene el filtro.  
  
2.  En la ventana **Propiedades** , haga clic con el botón derecho en el texto del filtro en la propiedad **Filter** y seleccione **Seleccionar todo**.  
  
3.  Presione la tecla Retroceso o Suprimir.  
  
## <a name="see-also"></a>Vea también  
 [Obtener detalles de datos de caso a partir de un modelo de minería de datos](../../analysis-services/data-mining/drill-through-to-case-data-from-a-mining-model.md)   
 [Tareas y procedimientos de los modelos de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)   
 [Filtros para modelos de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
