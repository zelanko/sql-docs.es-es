---
title: Especificar condiciones para grupos (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query groups
- group query conditions [SQL Server]
ms.assetid: 269ad9c5-3261-4526-badf-7be3c869f229
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bc0f9319e4d598548111b44b1a10542773a7daa4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63049159"
---
# <a name="specify-conditions-for-groups-visual-database-tools"></a>Especificar condiciones para grupos (Visual Database Tools)
  Puede limitar los grupos que aparecen en una consulta si especifica una condición que se aplique a los grupos en su totalidad: una cláusula HAVING. Una vez agrupados y agregados los datos, se aplican las condiciones de la cláusula HAVING. Solo aparecen en la consulta los grupos que cumplen las condiciones.  
  
 Por ejemplo, es posible que desee ver el precio medio de todos los libros de cada editorial en la tabla `titles` , pero únicamente cuando el precio medio supere los 10,00 USD. En ese caso, podría especificar una cláusula HAVING con una condición como `AVG(price) > 10`.  
  
> [!NOTE]  
>  En algunas ocasiones, quizás desee excluir algunas filas de los grupos antes de aplicar una condición a la totalidad de los grupos. Para detalles, consulte [Usar cláusulas HAVING y WHERE en la misma consulta &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
 Puede crear condiciones complejas para una cláusula HAVING utilizando AND y OR para unir condiciones. Para detalles sobre cómo usar AND y OR en las condiciones de búsqueda, consulte [Especificar varias condiciones de búsqueda para una columna &#40;Visual Database Tools&#41;](specify-multiple-search-conditions-for-one-column-visual-database-tools.md).  
  
### <a name="to-specify-a-condition-for-a-group"></a>Para especificar una condición para un grupo  
  
1.  Especifique los grupos de la consulta. Para detalles, consulte [Agrupar filas en los resultados de la consulta &#40;Visual Database Tools&#41;](group-rows-in-query-results-visual-database-tools.md).  
  
2.  Si aún no está en el [panel Criterios](criteria-pane-visual-database-tools.md), agregue la columna en la que desea basar la condición. Normalmente, la condición se aplica a una columna que ya es un grupo o una columna de resumen. No puede utilizar una columna que no forme parte de una función de agregado o de la cláusula GROUP BY.  
  
3.  En la columna **Filtro**, especifique la condición que se aplica al agrupo.  
  
     El [Diseñador de consultas y vistas](query-and-view-designer-tools-visual-database-tools.md) crea automáticamente una cláusula HAVING en la instrucción del [panel SQL](sql-pane-visual-database-tools.md), como la que se incluye en el ejemplo siguiente:  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
  
    ```  
  
4.  Repita los pasos 2 y 3 para las demás condiciones que desee especificar.  
  
## <a name="see-also"></a>Consulte también  
 [Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  
