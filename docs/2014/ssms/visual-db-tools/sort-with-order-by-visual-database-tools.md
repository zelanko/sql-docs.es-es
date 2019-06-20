---
title: Ordenar con ORDER BY (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [Visual Database Tools]
ms.assetid: 459f5640-8058-4c24-97e7-7bbd6168bc39
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30a2fca3dd0f2fcc6f22f2330c37fb8e333d9994
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049167"
---
# <a name="sort-with-order-by-visual-database-tools"></a>Ordenar con ORDER BY (Visual Database Tools)
  Puede ordenar los resultados de la consulta por una o más de las columnas de las filas devueltas utilizando una cláusula ORDER BY. Puede definir una cláusula ORDER BY eligiendo opciones en el panel Detalles de los criterios.  
  
### <a name="to-sort-a-query-using-an-order-by-clause"></a>Para ordenar una consulta utilizando una cláusula ORDER BY  
  
1.  Abra una consulta o cree una nueva.  
  
2.  En el [panel Criterios](visual-database-tools.md), haga clic en la columna **Tipo de orden** de la fila correspondiente a la columna que desea utilizar para ordenar los resultados de la consulta.  
  
3.  Elija *Ascendente* o *Descendente* en la lista desplegable.  
  
> [!NOTE]  
>  Al borrar la entrada **Tipo de orden** de una columna, ésta se quita de la cláusula ORDER BY.  
  
 Observe que cuando se trabaja en el panel Criterios, la cláusula UNION de la consulta cambia para coincidir con las acciones más recientes.  
  
> [!NOTE]  
>  Al ordenar los resultados por más de una columna, especifique el orden de prioridad que se seguirá al realizar búsquedas en las columnas utilizando la columna **Criterio de ordenación** . Para obtener más información, vea **Cómo: Ordenar varias columnas en consultas**.  
  
## <a name="see-also"></a>Vea también  
 [Ordenar y agrupar los resultados de consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)   
 [Resumir los resultados de consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
