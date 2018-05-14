---
title: Ordenar datos en una tabla | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ef0a5de0958fbea806063c17dd5f9f1912449be4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="sort-data-in-a-table"></a>Ordenar datos en una tabla 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Puede ordenar los datos por texto (de A a Z o de Z a A) y los números (de menor a mayor o viceversa) en una o varias columnas.  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-text-column"></a>Para ordenar los datos de una tabla según una columna de texto  
  
1.  En el Diseñador de modelos, seleccione una columna de datos alfanuméricos o un rango de celdas de una columna, o asegúrese de que la celda activa está en una columna de la tabla que contenga datos alfanuméricos; a continuación, haga clic en la flecha del encabezado de la columna que desea usar para el filtrado.  
  
2.  En el menú Autofiltro, siga uno de estos procedimientos:  
  
    -   Para clasificar en orden alfanumérico ascendente, haga clic en **Ordenar de A a Z**.  
  
    -   Para clasificar en orden alfanumérico descendente, haga clic en **Ordenar de Z a A.**  
  
    > [!NOTE]  
    >  En algunos casos, los datos importados de otra aplicación podrían tener espacios iniciales incrustados antes de los datos. Debe quitar los espacios iniciales para ordenar los datos correctamente.  
  
### <a name="to-sort-the-data-in-a-table-based-on-a-numeric-column"></a>Para ordenar los datos en una tabla según una columna numérica  
  
1.  En el Diseñador de modelos, seleccione una columna de datos alfanuméricos o un rango de celdas de una columna, o asegúrese de que la celda activa está en una columna de la tabla que contenga datos alfanuméricos; a continuación, haga clic en la flecha del encabezado de la columna que desea usar para el filtrado.  
  
2.  En el menú Autofiltro, siga uno de estos procedimientos:  
  
    -   Para ordenar de los números bajos a los números altos, haga clic en **Ordenar de menor a mayor**.  
  
    -   Para ordenar de los números altos a los números bajos, haga clic en **Ordenar de mayor a menor**.  
  
    > [!NOTE]  
    >  Si los resultados no son los que esperaba, la columna podría contener números almacenados como texto y no como números. Por ejemplo, los números negativos importados de algunos sistemas contables o un número escrito con un símbolo ' inicial (apóstrofo) se almacenan en forma de texto.  
  
## <a name="see-also"></a>Vea también  
 [Filtrar y ordenar datos](http://msdn.microsoft.com/library/55ebd7a6-2458-4398-911f-fcfeb2413f1b)   
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
