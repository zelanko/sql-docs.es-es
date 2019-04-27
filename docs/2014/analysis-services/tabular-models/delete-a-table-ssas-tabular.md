---
title: Eliminar una tabla (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: be4ed45f-fde3-466c-9869-49bd3ddb505e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 142a775415da489e67bc00b048651209a2a30179
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62757242"
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
 [Definir tablas y columnas &#40;SSAS tabular&#41;](tables-and-columns-ssas-tabular.md)  
  
  
