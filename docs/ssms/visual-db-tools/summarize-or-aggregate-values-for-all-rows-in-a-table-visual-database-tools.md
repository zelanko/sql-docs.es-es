---
title: Resumir o agregar los valores de todas las filas de una tabla | Microsoft Docs
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
- summarizing query results
- aggregate functions [SQL Server], summarizing query results
ms.assetid: f5af876e-f937-4110-ba09-07999c35a699
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 734063422cddceb9ac5fb3b1b44b0d64d07f7d6b
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools"></a>Resumir o agregar los valores de todas las filas de una tabla (Visual Database Tools)
## <a name="aggregate-function"></a>Aggregate, función
Mediante una función de agregado, puede crear un resumen de todos los valores de una tabla. Por ejemplo, se puede crear una consulta como la que se muestra a continuación para mostrar el precio total de todos los libros de la tabla `titles` :  
  
```  
SELECT SUM(price)  
FROM titles  
```  
  
Cree varios tipos de agregaciones en la misma consulta utilizando funciones de agregado con varias columnas. Puede crear, por ejemplo, una consulta que calcule el total de la columna `price` y el valor medio de la columna `discount` .  
  
Puede agregar la misma columna de maneras diferentes (como calculando el total, contando y calculando el promedio) en la misma consulta. Por ejemplo, la siguiente consulta calcula el promedio y resume la columna `price` de la tabla `titles` :  
  
```  
SELECT AVG(price), SUM(price)  
FROM titles  
```  
  
Si agrega una condición de búsqueda, puede agregar el subconjunto de filas que satisfacen esa condición.  

**Nota:** También puede contar todas las filas de la tabla o las que satisfacen una condición específica. Para detalles, consulte [Contar las filas de una tabla &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/count-rows-in-a-table-visual-database-tools.md).  
  
  
Cuando se crea un único valor de agregación para todas las filas de una tabla, solo se muestran los propios valores de agregado. Por ejemplo, si calcula el total del valor de la columna `price` de la tabla `titles` , no se mostrarán los títulos individuales, los nombres de las editoriales, etc.  
 
 **!** Si calcula subtotales (es decir, si crea grupos), puede mostrar los valores de columna de cada grupo. Para detalles, consulte [Agrupar filas en los resultados de la consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md).  

## <a name="aggregate-values-for-all-rows"></a>Valores agregados para todas las filas  
  
1.  Asegúrese de que la tabla que desea agregar ya esté presente en el panel Diagrama.  
  
2.  Haga clic con el botón derecho en el fondo del panel Diagrama y, a continuación, elija **Agrupar por** en el menú contextual. El [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) agrega una columna **Agrupar por** a la cuadrícula en el panel Criterios.  
  
3.  Agregue la columna que desee al panel Criterios. Asegúrese de que la columna está marcada para el resultado.  
  
    El Diseñador de consultas y vistas asigna automáticamente un alias a la columna que va a resumir. Puede sustituir este alias por otro más significativo. Para detalles, consulte [Crear alias de columna &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md).  
  
4.  En la columna de cuadrícula **Agrupar por**, seleccione la función de agregado correspondiente, como: **Sum**, **Avg**, **Min**, **Max** o **Count**. Si solo desea agregar filas únicas en el conjunto de resultados, elija una función de agregado con las opciones DISTINCT, como **Min Distinct**. No elija **Group By**, **Expression**o **Where**, ya que estas opciones no se aplican cuando se agregan todas las filas.  
  
    El Diseñador de consultas y vistas sustituye el nombre de columna en la instrucción del [panel SQL](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) por la función de agregado que especifique. Por ejemplo, la instrucción SQL podría tener el siguiente aspecto:  
  
    ```  
    SELECT SUM(price)  
    FROM titles  
    ```  
  
5.  Si desea crear más de una agregación en la consulta repita los pasos 3 y 4.  
  
    Cuando se agrega otra columna a la lista de resultados de la consulta o la lista de ordenación, el Diseñador de consultas y vistas incluye automáticamente el término **Group By** en la columna **Agrupar por** de la cuadrícula. Seleccione la función de agregado correspondiente.  
  
6.  Agregue condiciones de búsqueda, si es necesario, para especificar el subconjunto de filas que desea resumir.  
  
Cuando ejecute la consulta, en el panel Resultados se mostrarán las agregaciones especificadas.  
  
> [!NOTE]  
> El Diseñador de consultas y vistas mantiene las funciones de agregado como parte de la instrucción SQL en el panel SQL hasta que se desactiva explícitamente el modo Agrupar por. Por tanto, si se modifica una columna asignándole otro tipo distinto o cambiando las tablas o los objetos con valores de tablas que aparecen en el panel Diagrama, la consulta resultante podría incluir funciones de agregado no válidas.  
  
## <a name="see-also"></a>Vea también  
[Ordenar y agrupar los resultados de una consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Resumir los resultados de una consulta &amp;#40;Visual Database Tools&amp;#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  

