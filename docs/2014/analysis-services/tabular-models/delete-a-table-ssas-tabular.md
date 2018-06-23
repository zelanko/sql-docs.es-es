---
title: Eliminar una tabla (SSAS Tabular) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 360628cb290b30efaf006900dcb16ee7e8cfc8e5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199541"
---
# <a name="delete-a-table-ssas-tabular"></a>Eliminar una tabla (SSAS tabular)
  En el diseñador de modelos, puede eliminar las tablas de la base de datos del área de trabajo del modelo que no necesite. Eliminar una tabla no afecta a los datos de origen originales, solo a los datos que importó y con los que trabajó. No puede deshacer la eliminación de una tabla.  
  
### <a name="to-delete-a-table"></a>Para eliminar una tabla  
  
-   Haga clic con el botón derecho en la pestaña de la parte inferior del diseñador de modelos para la tabla que quiera eliminar y, después, haga clic en **Eliminar**.  
  
## <a name="considerations-when-deleting-tables"></a>Aspectos que se deben tener en cuenta al eliminar tablas  
  
-   Al eliminar una tabla, se elimina la pestaña completa en la que estaba la tabla.  
  
-   Si hubiera alguna medida asociada a esa tabla, también se eliminará la definición de la medida.  
  
-   Si creó alguna columna calculada usando esa tabla, también se eliminan las columnas de esa tabla; cualquier columna calculada de otras tablas que usen columnas de la tabla eliminada mostrará un error.  
  
## <a name="see-also"></a>Vea también  
 [Tablas y columnas &#40;SSAS Tabular&#41;](tables-and-columns-ssas-tabular.md)  
  
  