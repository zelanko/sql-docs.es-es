---
title: Ordenar en orden ascendente o descendente (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- descending sorts
- ascending sorts
ms.assetid: d61cc55b-9ee8-4ecf-a32f-6459ae43910b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cdf37ab5b61e74ab04b9b58162325b580675c493
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52822159"
---
# <a name="sort-in-ascending-or-descending-order-visual-database-tools"></a>Ordenar en orden ascendente o descendente (Visual Database Tools)
  Puede ordenar los resultados de la consulta en orden ascendente o descendente en una o más columnas del conjunto de resultados utilizando las palabras clave `ASC` o `DESC` con la cláusula `ORDER BY`.  
  
> [!NOTE]  
>  La secuencia de intercalación de la columna determina en parte el criterio de ordenación. La secuencia de intercalación se puede modificar en el [cuadro de diálogo Intercalación](visual-database-tools.md).  
  
 El procedimiento siguiente asume que en el Diseñador de consultas y vistas hay una consulta abierta que utiliza la cláusula ORDER BY para ordenar una o más columnas.  
  
### <a name="to-specify-or-change-the-order-in-which-results-are-sorted"></a>Para especificar o cambiar el criterio de ordenación de los resultados  
  
1.  En el [panel Criterios](criteria-pane-visual-database-tools.md), haga clic en el campo **Tipo de orden** de la columna que desea reordenar.  
  
2.  Elija **Ascendente** o **Descendente** para especificar el criterio de ordenación de la columna.  
  
 Observe que cuando se trabaja en el panel Criterios, la cláusula UNION de la consulta cambia para coincidir con las acciones más recientes.  
  
> [!NOTE]  
>  Al ordenar los resultados por más de una columna, especifique el orden de prioridad que se seguirá al realizar búsquedas en las columnas utilizando la columna Criterio de ordenación. Para más información, consulte [Ordenar varias columnas en las consultas &#40;Visual Database Tools&#41;](sort-multiple-columns-in-queries-visual-database-tools.md).  
  
## <a name="see-also"></a>Vea también  
 [Ordenar y agrupar los resultados de consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Resumir los resultados de consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
