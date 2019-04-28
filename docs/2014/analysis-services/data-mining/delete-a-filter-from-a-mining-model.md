---
title: Eliminar un filtro de un modelo de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- filters [Analysis Services]
ms.assetid: 91220b21-adbc-49a9-b200-8bf0a724eff1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9cb98e29f320a64518c968f3bbc35b590c96a891
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62722557"
---
# <a name="delete-a-filter-from-a-mining-model"></a>Eliminar un filtro de un modelo de minería de datos
  Al crear un filtro en un modelo de minería de datos, puede crear modelos en un subconjunto de los datos en la vista del origen de datos. Los filtros también son útiles para probar la precisión del modelo en un subconjunto de los datos originales.  
  
 Sin embargo, debe eliminar el filtro si desea ver de nuevo el conjunto completo de casos. Este procedimiento describe cómo quitar las condiciones de un filtro o eliminar éste por completo.  
  
### <a name="to-delete-a-condition-from-a-filter-on-a-mining-model"></a>Para eliminar una condición de un filtro en un modelo de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el Explorador de soluciones, haga clic en la estructura de minería de datos que contiene el modelo de minería que desea filtrar.  
  
2.  Haga clic en la pestaña **Modelos de minería de datos** .  
  
3.  Seleccione el modelo y haga clic con el botón secundario del mouse para abrir el menú contextual.  
  
     -o bien-  
  
     Seleccione el modelo. En el menú **Minería de datos** , seleccione **Establecer filtro de modelos**.  
  
4.  En el cuadro de diálogo **Filtro del modelo** , haga clic con el botón derecho en la fila de la cuadrícula que contiene la condición que quiere eliminar.  
  
5.  Seleccione **Eliminar**.  
  
### <a name="to-clear-the-filter-on-a-mining-model-in-the-filter-editor-dialog-box"></a>Para borrar el filtro de un modelo de minería de datos en el cuadro de diálogo Editor de filtros  
  
-   En el cuadro de diálogo **Editor de filtros** , haga clic con el botón derecho en cualquier fila de la cuadrícula y seleccione **Eliminar todos**.  
  
## <a name="working-with-model-filters-using-the-properties-window"></a>Trabajar con filtros de modelo utilizando la ventana Propiedades  
 Si desea eliminar todo el filtro, no necesita abrir los cuadros de diálogo del editor de filtros. Las condiciones de filtrado que creó están disponibles en la propiedad `Filter` del modelo de minería de datos.  
  
> [!NOTE]  
>  Puede ver las propiedades de un modelo de minería de datos en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], pero no en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-clear-the-filter-on-a-mining-model-in-solution-explorer"></a>Para borrar el filtro de un modelo de minería de datos en el Explorador de soluciones  
  
1.  En el Explorador de soluciones, haga clic en el modelo de minería de datos que contiene el filtro.  
  
2.  En el **propiedades** ventana, haga clic en el texto del filtro en el `Filter` propiedad y seleccione **seleccionar todo**.  
  
3.  Presione la tecla Retroceso o Suprimir.  
  
## <a name="see-also"></a>Vea también  
 [Obtener detalles de datos de caso a partir de un modelo de minería de datos](drill-through-to-case-data-from-a-mining-model.md)   
 [Tareas y procedimientos de los modelos de minería de datos](mining-model-tasks-and-how-tos.md)   
 [Filtros para modelos de minería &#40;Analysis Services - Minería de datos&#41;](mining-models-analysis-services-data-mining.md)  
  
  
