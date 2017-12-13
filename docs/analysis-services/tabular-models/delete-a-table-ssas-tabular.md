---
title: Eliminar una tabla (SSAS Tabular) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 36438a8871c90ac00bcaf0e16ca184b4d9286a81
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="delete-a-table-ssas-tabular"></a>Eliminar una tabla (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]En el Diseñador de modelos, puede eliminar las tablas de la base de datos del área de trabajo de modelo que ya no necesite. Eliminar una tabla no afecta a los datos de origen originales, solo a los datos que importó y con los que trabajó. No puede deshacer la eliminación de una tabla.  
  
### <a name="to-delete-a-table"></a>Para eliminar una tabla  
  
-   Haga clic con el botón derecho en la pestaña de la parte inferior del diseñador de modelos para la tabla que quiera eliminar y, después, haga clic en **Eliminar**.  
  
## <a name="considerations-when-deleting-tables"></a>Aspectos que se deben tener en cuenta al eliminar tablas  
  
-   Al eliminar una tabla, se elimina la pestaña completa en la que estaba la tabla.  
  
-   Si hubiera alguna medida asociada a esa tabla, también se eliminará la definición de la medida.  
  
-   Si creó alguna columna calculada usando esa tabla, también se eliminan las columnas de esa tabla; cualquier columna calculada de otras tablas que usen columnas de la tabla eliminada mostrará un error.  
  
## <a name="see-also"></a>Vea también  
 [Definir tablas y columnas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
