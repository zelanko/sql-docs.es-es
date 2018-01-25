---
title: Especificar condiciones para grupos (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- HAVING clause, query groups
- group query conditions [SQL Server]
ms.assetid: 269ad9c5-3261-4526-badf-7be3c869f229
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 643aa62419885e2708a084cb37d23c95b38305ae
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="specify-conditions-for-groups-visual-database-tools"></a>Especificar condiciones para grupos (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Puede limitar los grupos que aparecen en una consulta especificando una condición que se aplique a los grupos en su totalidad: una cláusula HAVING. Una vez agrupados y agregados los datos, se aplican las condiciones de la cláusula HAVING. Solo aparecen en la consulta los grupos que cumplen las condiciones.  
  
Por ejemplo, es posible que desee ver el precio medio de todos los libros de cada editorial en la tabla `titles` , pero únicamente cuando el precio medio supere los 10,00 USD. En ese caso, podría especificar una cláusula HAVING con una condición como `AVG(price) > 10`.  
  
> [!NOTE]  
> En algunas ocasiones, quizás desee excluir algunas filas de los grupos antes de aplicar una condición a la totalidad de los grupos. Para detalles, consulte [Usar cláusulas HAVING y WHERE en la misma consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md).  
  
Puede crear condiciones complejas para una cláusula HAVING utilizando AND y OR para unir condiciones. Para detalles sobre cómo usar AND y OR en las condiciones de búsqueda, consulte [Especificar varias condiciones de búsqueda para una columna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md).  
  
### <a name="to-specify-a-condition-for-a-group"></a>Para especificar una condición para un grupo  
  
1.  Especifique los grupos de la consulta. Para detalles, consulte [Agrupar filas en los resultados de la consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md).  
  
2.  Si aún no está en el [panel Criterios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), agregue la columna en la que desea basar la condición. Normalmente, la condición se aplica a una columna que ya es un grupo o una columna de resumen. No puede utilizar una columna que no forme parte de una función de agregado o de la cláusula GROUP BY.  
  
3.  En la columna **Filtro**, especifique la condición que se aplica al agrupo.  
  
    El [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) crea automáticamente una cláusula HAVING en la instrucción del [panel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md), como la que se incluye en el ejemplo siguiente:  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
4.  Repita los pasos 2 y 3 para las demás condiciones que desee especificar.  
  
## <a name="see-also"></a>Ver también  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
