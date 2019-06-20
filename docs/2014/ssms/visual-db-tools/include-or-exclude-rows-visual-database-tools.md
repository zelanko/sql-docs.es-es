---
title: Incluir o excluir filas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- included rows
- search conditions [SQL Server], HAVING clause
- search criteria [SQL Server], including rows
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- search conditions [SQL Server], WHERE clause
- row included in search [SQL Server]
- excluding rows
ms.assetid: ba4e1202-31a2-444d-8365-c68a530ef223
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3785a777571ef7659b1ae21a693e6754659a80e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298590"
---
# <a name="include-or-exclude-rows-visual-database-tools"></a>Incluir o excluir filas (Visual Database Tools)
  Para restringir el número de filas que debe devolver una consulta SELECT, puede crear condiciones de búsqueda o criterios de filtro. En SQL, las condiciones de búsqueda aparecen en la cláusula WHERE de la instrucción o, si está creando una consulta de funciones agregadas, en la cláusula HAVING.  
  
> [!NOTE]  
>  También puede utilizar condiciones de búsqueda para indicar qué filas están afectadas por una consulta Update, Insert Results, Insert Values, Delete o Make Table.  
  
 Cuando se ejecuta la consulta, [!INCLUDE[ssDE](../../includes/ssde-md.md)] examina y aplica la condición de búsqueda a cada fila de las tablas en las que el usuario está buscando. Si la fila cumple la condición, se incluye en la consulta. Por ejemplo, una condición de búsqueda que encuentre todos los empleados de una región determinada podría ser:  
  
```  
region = 'UK'  
```  
  
 Para establecer los criterios para incluir una fila en un resultado, puede utilizar varias condiciones de búsqueda. Por ejemplo, el siguiente criterio de búsqueda consta de dos condiciones de búsqueda. La consulta incluye una fila en el conjunto de resultados solo si dicha fila satisface ambas condiciones.  
  
```  
region = 'UK' AND product_line = 'Housewares'  
```  
  
 Puede combinar estas condiciones con AND u OR. El ejemplo anterior utiliza AND. En contraposición, el criterio siguiente utiliza OR. El conjunto de resultados incluirá cualquier fila que satisfaga una de las condiciones de búsqueda o ambas:  
  
```  
region = 'UK' OR product_line = 'Housewares'  
```  
  
 Puede incluso combinar condiciones de búsqueda en una sola columna. Por ejemplo, el siguiente criterio combina dos condiciones en la columna región:  
  
```  
region = 'UK' OR region = 'US'  
```  
  
 Para obtener más detalles sobre cómo combinar condiciones de búsqueda, vea los temas siguientes:  
  
-   [Convenciones para combinar condiciones de búsqueda en el panel Criterios &#40;Visual Database Tools&#41;](conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
  
-   [Especificar varias condiciones de búsqueda para una columna &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
-   [Especificar varias condiciones de búsqueda para varias columnas &#40;Visual Database Tools&#41;](specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)  
  
-   [Combinar condiciones cuando AND tiene prioridad &#40;Visual Database Tools&#41;](combine-conditions-when-and-has-precedence-visual-database-tools.md)  
  
-   [Combinar condiciones cuando OR tiene prioridad &#40;Visual Database Tools&#41;](combine-conditions-when-or-has-precedence-visual-database-tools.md)  
  
## <a name="examples"></a>Ejemplos  
 A continuación se muestran algunos ejemplos de consultas que utilizan varios operadores y criterios de fila:  
  
-   **Literal** Valor único de texto, numérico, de fecha o lógico. El ejemplo siguiente utiliza un literal para buscar todas las filas de empleados del Reino Unido:  
  
    ```  
    WHERE region = 'UK'  
    ```  
  
-   **Referencia de columna** Compara los valores de una columna con los valores de la otra. El ejemplo siguiente busca en una tabla `products` todas las filas en las que el valor del costo de producción es inferior al costo de envío:  
  
    ```  
    WHERE prod_cost < ship_cost  
    ```  
  
-   **Función** Referencia a una función que el back-end de la base de datos puede resolver para calcular un valor de la búsqueda. La función puede ser una función definida por el servidor de base de datos o una función definida por el usuario que devuelve un valor escalar. El siguiente ejemplo busca pedidos realizados hoy (la función GETDATE( ) devuelve la fecha actual):  
  
    ```  
    WHERE order_date = GETDATE()  
    ```  
  
-   **NULL** El siguiente ejemplo busca en una tabla `authors` todos los autores que tengan un nombre en el archivo:  
  
    ```  
    WHERE au_fname IS NOT NULL  
    ```  
  
-   **Cálculo** Resultado de un cálculo que puede incluir literales, referencias de columna u otras expresiones. El siguiente ejemplo busca en una tabla `products` todas las filas en las que el precio de venta al público sea más del doble del costo de producción:  
  
    ```  
    WHERE sales_price > (prod_cost * 2)  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Diseñar temas de procedimientos de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [Realizar consultas con parámetros &#40;Visual Database Tools&#41;](query-with-parameters-visual-database-tools.md)  
  
  
