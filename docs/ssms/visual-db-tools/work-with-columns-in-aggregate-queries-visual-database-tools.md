---
title: Trabajar con columnas en consultas de funciones agregadas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- HAVING clause, query summary results
- GROUP BY clause, query summary results
- aggregate queries [SQL Server]
- WHERE clause, query summary results
ms.assetid: 1b82681f-3d4f-4b9a-bb1d-2060e44f2577
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87611561dda34af615da24a7879d6390916d06cf
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="work-with-columns-in-aggregate-queries-visual-database-tools"></a>Trabajar con columnas en consultas de funciones agregadas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Al crear consultas agregadas, el [Diseñador de consultas y vistas](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) asume determinados criterios para poder crear una consulta válida. Por ejemplo, si está creando una consulta de funciones de agregado y marca una columna de datos para los resultados, el Diseñador de consultas y vistas incluye automáticamente la columna en la cláusula GROUP BY para que no intente mostrar sin darse cuenta el contenido de una fila individual en un resumen.  
  
## <a name="using-group-by"></a>Utilizar Agrupar por  
El Diseñador de consultas y vistas utiliza las siguientes instrucciones para trabajar con columnas:  
  
-   Al elegir la opción Agrupar por o al agregar una función agregada a una consulta, se agregan automáticamente a la cláusula GROUP BY todas las columnas marcadas para los resultados o utilizadas para ordenar. Las columnas no se agregan automáticamente a la cláusula GROUP BY si ya forman parte de una función de agregado.  
  
    Si no desea que una columna en particular forme parte de la cláusula GROUP BY, debe cambiarla manualmente mediante la selección de una opción distinta en la columna Agrupar por del panel Criterios. Sin embargo, el Diseñador de consultas y vistas no impedirá que elija una opción que pueda dar como resultado una consulta que no acabe ejecutándose.  
  
-   Si agrega manualmente una columna de resultados de consulta a una función de agregado ya sea en el panel Criterios o en el panel SQL, el Diseñador de consultas y vistas no quita automáticamente las demás columnas de resultados de la consulta. Por lo tanto, debe quitar las columnas restantes de los resultados de la consulta o incluirlas en la cláusula GROUP BY o en una función de agregado.  
  
Al especificar una condición de búsqueda en la columna Filtro del panel Criterios, el Diseñador de consultas y vistas sigue estas reglas:  
  
-   Si no se muestra la columna **Agrupar por** de la cuadrícula (porque todavía no ha especificado una consulta de funciones agregadas), la condición de búsqueda se coloca en la cláusula WHERE.  
  
-   Si ya se encuentra en una consulta de funciones agregadas y ha seleccionado la opción **Ubicación** en la columna **Agrupar por** , la condición de búsqueda se coloca en la cláusula WHERE.  
  
-   Si la columna **Agrupar por** contiene cualquier valor que no sea **Ubicación**, la condición de búsqueda se coloca en la cláusula HAVING.  
  
## <a name="using-the-having-and-where-clauses"></a>Uso de las cláusulas HAVING y WHERE  
Los principios siguientes describen cómo puede hacer referencia a columnas de una consulta de funciones agregadas en condiciones de búsqueda: en general, puede utilizar una columna en una condición de búsqueda para filtrar las filas que deben resumirse (una cláusula WHERE) o determinar qué resultados agrupados aparecen en los resultados finales (una cláusula HAVING).  
  
-   Las columnas de datos individuales pueden aparecer en la cláusula WHERE o HAVING, en función de cómo se utilicen en cualquier otra parte de la consulta.  
  
-   Las cláusulas WHERE se utilizan para seleccionar subconjuntos de filas para resumir y agrupar y, así, se aplican antes de que se realice un agrupamiento. De ahí que pueda utilizar una columna de datos en una cláusula WHERE aunque no forme parte de la cláusula GROUP BY o no esté contenida en una función de agregado. Por ejemplo, la siguiente instrucción selecciona todos los títulos que cuestan más de 10,00 USD y obtiene un promedio del precio:  
  
    ```  
    SELECT AVG(price)  
    FROM titles  
    WHERE price > 10  
    ```  
  
-   Si crea una condición de búsqueda que incluya una columna utilizada también en una cláusula GROUP BY o en una función de agregado, la condición de búsqueda puede aparecer como una cláusula WHERE o como una cláusula HAVING: puede decidir cuál al crear la condición. Por ejemplo, la siguiente instrucción crea un precio medio de los títulos de cada editorial y, a continuación, muestra la media de las editoriales cuyo precio medio supera los 10,00 USD:  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
-   Si utiliza una función de agregado en una condición de búsqueda, la condición requiere un resumen y, por lo tanto, debe formar parte de la cláusula HAVING.  
  
## <a name="see-also"></a>Ver también  
[Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
