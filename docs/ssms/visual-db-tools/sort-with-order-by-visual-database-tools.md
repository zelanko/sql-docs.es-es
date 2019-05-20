---
title: Ordenar con ORDER BY (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [Visual Database Tools]
ms.assetid: 459f5640-8058-4c24-97e7-7bbd6168bc39
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 07fb08547e8a114e9a580b1a13da8b1038b2f3ae
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65099159"
---
# <a name="sort-with-order-by-visual-database-tools"></a>Ordenar con ORDER BY (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede ordenar los resultados de la consulta por una o más de las columnas de las filas devueltas utilizando una cláusula ORDER BY. Puede definir una cláusula ORDER BY eligiendo opciones en el panel Detalles de los criterios.  
  
### <a name="to-sort-a-query-using-an-order-by-clause"></a>Para ordenar una consulta utilizando una cláusula ORDER BY  
  
1.  Abra una consulta o cree una nueva.  
  
2.  En el [panel Criterios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), haga clic en la columna **Tipo de orden** de la fila correspondiente a la columna que desea utilizar para ordenar los resultados de la consulta.  
  
3.  Elija *Ascendente* o *Descendente* en la lista desplegable.  
  
> [!NOTE]  
> Al borrar la entrada **Tipo de orden** de una columna, ésta se quita de la cláusula ORDER BY.  
  
Observe que cuando se trabaja en el panel Criterios, la cláusula UNION de la consulta cambia para coincidir con las acciones más recientes.  
  
> [!NOTE]  
> Al ordenar los resultados por más de una columna, especifique el orden de prioridad que se seguirá al realizar búsquedas en las columnas utilizando la columna **Criterio de ordenación** . Para más información, vea: **Cómo: Ordenar varias columnas en consultas**.  
  
## <a name="see-also"></a>Consulte también  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
