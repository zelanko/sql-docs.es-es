---
title: Eliminar una tabla | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e9a9269457d973da6b56f9e7990c31700dafcad9
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
---
# <a name="delete-a-table"></a>Eliminar una tabla 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  En el diseñador de modelos, puede eliminar las tablas de la base de datos del área de trabajo del modelo que no necesite. Eliminar una tabla no afecta a los datos de origen originales, solo a los datos que importó y con los que trabajó. No puede deshacer la eliminación de una tabla.  
  
### <a name="to-delete-a-table"></a>Para eliminar una tabla  
  
-   Haga clic con el botón derecho en la pestaña de la parte inferior del diseñador de modelos para la tabla que quiera eliminar y, después, haga clic en **Eliminar**.  
  
## <a name="considerations-when-deleting-tables"></a>Aspectos que se deben tener en cuenta al eliminar tablas  
  
-   Al eliminar una tabla, se elimina la pestaña completa en la que estaba la tabla.  
  
-   Si hubiera alguna medida asociada a esa tabla, también se eliminará la definición de la medida.  
  
-   Si creó alguna columna calculada usando esa tabla, también se eliminan las columnas de esa tabla; cualquier columna calculada de otras tablas que usen columnas de la tabla eliminada mostrará un error.  
  
## <a name="see-also"></a>Vea también  
 [Tablas y columnas](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
