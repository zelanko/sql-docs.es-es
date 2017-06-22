---
title: "Especificar varias condiciones de búsqueda en una columna | Microsoft Docs"
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
- search criteria [SQL Server], multiple conditions
- multiple search conditions
- search conditions [SQL Server], multiple
- OR operator
- AND, Criteria pane
ms.assetid: 2c006e36-56b1-4992-89b4-c6c0b19808f3
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a7b140acf1b00f31df0d8c948cdeca8ff6703726
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="specify-multiple-search-conditions-for-one-column-visual-database-tools"></a>Especificar varias condiciones de búsqueda para una columna (Visual Database Tools)
En algunas ocasiones, es posible que desee aplicar una serie de condiciones de búsqueda a la misma columna de datos. Por ejemplo, podría:  
  
-   Buscar varios nombres diferentes en una tabla `employee` o empleados que tengan distintos salarios. Este tipo de búsqueda requiere una condición OR.  
  
-   Buscar un título de un libro que empiece con la palabra "La" y contenga la palabra "Cocina". Este tipo de búsqueda requiere una condición AND.  
  
> [!NOTE]  
> La información de este tema se aplica a las condiciones de búsqueda en las cláusulas WHERE y HAVING de una consulta. Los ejemplos se centran en las cláusulas WHERE, pero los principios se aplican a ambos tipos de condiciones de búsqueda.  
  
Para buscar valores alternativos en la misma columna de datos, debe especificar una condición OR. Para buscar valores que cumplan varias condiciones, debe especificar una condición AND.  
  
## <a name="specifying-an-or-condition"></a>Especificar una condición OR  
La condición OR permite especificar la búsqueda de varios valores alternativos en una columna. Esta opción expande el ámbito de la búsqueda y puede devolver más filas que cuando se busca un solo valor.  
  
> [!TIP]  
> Con frecuencia, se puede utilizar el operador IN en lugar de buscar varios valores en la misma columna de datos.  
  
#### <a name="to-specify-an-or-condition"></a>Para especificar una condición OR  
  
1.  En el [panel Criterios](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md), agregue la columna en la que desea realizar la búsqueda.  
  
2.  En la columna **Filtro** de la columna de datos que acaba de agregar, especifique la primera condición.  
  
3.  En la columna **O...** de la misma columna de datos, especifique la segunda condición.  
  
El Diseñador de consultas y vistas crea una cláusula WHERE que contiene una condición OR similar a la siguiente:  
  
```  
SELECT fname, lname  
FROM employees  
WHERE (salary < 30000) OR (salary > 100000)  
```  
  
## <a name="specifying-an-and-condition"></a>Especificar una condición AND  
La condición AND permite especificar que los valores de una columna deben satisfacer dos o más condiciones para que la fila se incluya en el conjunto de resultados. Esta opción limita el ámbito de la búsqueda y normalmente devuelve menos filas que cuando se busca un solo valor.  
  
> [!TIP]  
> Si va a buscar un intervalo de valores, puede utilizar el operador BETWEEN en lugar de unir dos condiciones con AND.  
  
#### <a name="to-specify-an-and-condition"></a>Para especificar una condición AND  
  
1.  En el panel Criterios, agregue la columna en la que desea realizar la búsqueda.  
  
2.  En la columna **Filtro** de la columna de datos que acaba de agregar, especifique la primera condición.  
  
3.  Vuelva a agregar la misma columna de datos en el panel Criterios insertándola en una fila vacía de la cuadrícula.  
  
4.  En la columna **Filtro** de la segunda instancia de la columna de datos, especifique la segunda condición.  
  
El Diseñador de consultas crea una cláusula WHERE que contiene una condición AND similar a la siguiente:  
  
```  
SELECT title_id, title  
FROM titles  
WHERE (title LIKE '%Cook%') AND   
  (title LIKE '%Recipe%')  
```  
  
## <a name="see-also"></a>Vea también  
[Convenciones para combinar condiciones de búsqueda en el panel Criterios &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[Especificar criterios de búsqueda &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  

