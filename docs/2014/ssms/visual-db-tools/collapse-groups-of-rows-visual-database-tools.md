---
title: Contraer grupos de filas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- group collapsing [SQL Server]
- collapsing rows
- row collapsing [SQL Server]
ms.assetid: 7338dad0-965d-44ba-8c1a-b993acb7156d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0534d416d6d821e2d1870e98a42e8281648c6af1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066190"
---
# <a name="collapse-groups-of-rows-visual-database-tools"></a>Contraer grupos de filas (Visual Database Tools)
  Puede crear un resultado de consulta en el que cada fila de resultados se corresponda con un grupo de filas completo de los datos originales. Cuando se contraen filas, conviene tener en cuenta lo siguiente:  
  
-   **Puede eliminar filas duplicadas** Algunas consultas pueden crear conjuntos de resultados en los que aparezcan varias filas idénticas. Por ejemplo, puede crear un conjunto de resultados en el que cada fila contenga la ciudad y el nombre del estado de una ciudad que contiene un autor; pero si una ciudad contiene varios autores, habrá varias filas idénticas. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT city, state  
    FROM authors  
    ```  
  
     El conjunto de resultados generado por la consulta anterior no es muy útil. Si una ciudad contiene cuatro autores, el conjunto de resultados incluirá cuatro filas idénticas. Como el conjunto de resultados no incluye otras columnas que no sean ciudad y estado, no hay manera de distinguir las filas idénticas unas de otras. Una manera de evitar filas duplicadas de este tipo es incluir columnas adicionales que pueden hacer que las filas sean diferentes. Por ejemplo, si incluye el nombre del autor, cada fila será diferente (siempre y cuando no haya dos autores que se llamen igual y que vivan en la misma ciudad). El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT city, state, fname, minit, lname  
    FROM authors  
  
    ```  
  
     Es evidente que la consulta anterior elimina el síntoma, pero no soluciona realmente el problema. Es decir, el conjunto de resultados no tiene duplicados, pero ya no es un conjunto de resultados de ciudades. Para eliminar elementos duplicados en el conjunto de resultados original y que cada fila siga describiendo una ciudad, puede crear una consulta que devuelva únicamente filas diferentes. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT DISTINCT city, state  
    FROM authors  
  
    ```  
  
     Para detalles sobre cómo eliminar los elementos duplicados, consulte [Excluir filas duplicadas &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
-   **Puede calcular por grupos de filas** Es decir, puede resumir información en grupos de filas. Por ejemplo, puede crear un conjunto de resultados en el que cada fila contenga la ciudad y el nombre del estado de una ciudad que contenga un autor, además de un recuento del número de autores que hay en esa ciudad. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
  
    ```  
  
     Para detalles sobre cómo realizar cálculos en grupos de filas, consulte [Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md) y [Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md).  
  
-   **Puede utilizar criterios de selección para incluir grupos de filas** Por ejemplo, puede crear un conjunto de resultados en el que cada fila contenga la ciudad y el nombre del estado de una ciudad que contenga varios autores, además de un recuento del número de autores que hay en esa ciudad. El código SQL resultante puede presentar el siguiente aspecto:  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    HAVING COUNT(*) > 1  
  
    ```  
  
     Para detalles sobre cómo aplicar los criterios de selección en grupos de filas, consulte [Especificar condiciones para grupos &#40;Visual Database Tools&#41;](specify-conditions-for-groups-visual-database-tools.md) y [Usar cláusulas HAVING y WHERE en la misma consulta &#40;Visual Database Tools&#41;](use-having-and-where-clauses-in-the-same-query-visual-database-tools.md).  
  
## <a name="see-also"></a>Consulte también  
 [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
