---
title: Ordenar con ORDER BY (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [Visual Database Tools]
ms.assetid: 459f5640-8058-4c24-97e7-7bbd6168bc39
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 98e5927c691cb1d9b4811cf308b139b205ed3058
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33048602"
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
> Al ordenar los resultados por más de una columna, especifique el orden de prioridad que se seguirá al realizar búsquedas en las columnas utilizando la columna **Criterio de ordenación** . Para más información, consulte **Ordenar varias columnas de las consultas**.  
  
## <a name="see-also"></a>Ver también  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
