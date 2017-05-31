---
title: Ordenar con ORDER BY (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ORDER BY clause [Visual Database Tools]
ms.assetid: 459f5640-8058-4c24-97e7-7bbd6168bc39
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 01bb085d1946c5e6ac407c6baa8a9049892bc4df
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="sort-with-order-by-visual-database-tools"></a>Ordenar con ORDER BY (Visual Database Tools)
Puede ordenar los resultados de la consulta por una o más de las columnas de las filas devueltas utilizando una cláusula ORDER BY. Puede definir una cláusula ORDER BY eligiendo opciones en el panel Detalles de los criterios.  
  
### <a name="to-sort-a-query-using-an-order-by-clause"></a>Para ordenar una consulta utilizando una cláusula ORDER BY  
  
1.  Abra una consulta o cree una nueva.  
  
2.  En el [panel Criterios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), haga clic en la columna **Tipo de orden** de la fila correspondiente a la columna que desea utilizar para ordenar los resultados de la consulta.  
  
3.  Elija *Ascendente* o *Descendente* en la lista desplegable.  
  
> [!NOTE]  
> Al borrar la entrada **Tipo de orden** de una columna, ésta se quita de la cláusula ORDER BY.  
  
Observe que cuando se trabaja en el panel Criterios, la cláusula UNION de la consulta cambia para coincidir con las acciones más recientes.  
  
> [!NOTE]  
> Al ordenar los resultados por más de una columna, especifique el orden de prioridad que se seguirá al realizar búsquedas en las columnas utilizando la columna **Criterio de ordenación** . Para más información, consulte **Ordenar varias columnas de las consultas**.  
  
## <a name="see-also"></a>Vea también  
[Ordenar y agrupar los resultados de una consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  

