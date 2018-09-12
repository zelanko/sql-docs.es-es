---
title: Crear consultas de creación de tabla (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- table creation [SQL Server], Make Table query
- inserting tables
- Make Table query
- adding tables
ms.assetid: 4493cffa-7b2d-4c24-8ef0-d49329198972
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5784a37090427564be20e2c43bb7df351a38fa8d
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43809861"
---
# <a name="create-make-table-queries-visual-database-tools"></a>Crear consultas de creación de tabla (Visual Database Tools)
  Puede copiar filas en una nueva tabla mediante una consulta de creación de tabla, que sirve para crear subconjuntos de datos con los que trabajar o para copiar el contenido de una tabla de una base de datos a otra. La consulta de creación de tabla es similar a la consulta de inserción de resultados, con la diferencia de que en la primera se crea una nueva tabla en la que se copian las filas.  
  
 Cuando se crea una consulta de creación de tabla, se especifica:  
  
-   El nombre de la nueva tabla de base de datos (la tabla de destino).  
  
-   Las tablas de las que se van a copiar filas (tabla de origen). Puede copiar de una sola tabla o de tablas combinadas.  
  
-   Las columnas de la tabla de origen cuyo contenido desea copiar.  
  
-   El criterio de ordenación, si desea copiar las filas en un orden determinado.  
  
-   Las condiciones de búsqueda que definen las filas que desea copiar.  
  
-   Las opciones Agrupar por, si solo desea copiar información de resumen.  
  
 Por ejemplo, en la consulta siguiente se crea una nueva tabla llamada `uk`_`customers` y se copia en ella información de la tabla `customers` .  
  
```  
SELECT *   
INTO uk_customers  
FROM customers  
WHERE country = 'UK'  
```  
  
 Para utilizar una consulta de creación de tabla correctamente:  
  
-   La base de datos debe ser compatible con la sintaxis SELECT...INTO.  
  
-   Debe tener permiso para crear una tabla en la base de datos de destino.  
  
### <a name="to-create-a-make-table-query"></a>Para crear una consulta de creación de tabla  
  
1.  Agregue la tabla o tablas de origen al panel Diagrama.  
  
2.  En el menú **Diseñador de consultas** , seleccione **Tipo de cambio**y, a continuación, haga clic en **Crear tabla**.  
  
3.  En el cuadro de diálogo **Crear tabla** , escriba el nombre de la tabla de destino. El Diseñador de consultas y vistas no comprueba si el nombre ya está en uso o si se dispone de permiso para crear la tabla.  
  
     Para crear una tabla de destino en otra base de datos, especifique un nombre de tabla completo, incluido el nombre de la base de datos de destino, el propietario (si es necesario) y el nombre de la tabla.  
  
4.  Defina las columnas que se van a copiar agregándolas a la consulta. Para detalles, consulte [Agregar columnas a las consultas &#40;Visual Database Tools&#41;](visual-database-tools.md). Las columnas se copian solo si se agregan a la consulta. Para copiar filas enteras, elija  **\* (todas las columnas)**.  
  
     El Diseñador de consultas y vistas agrega las columnas elegidas a la columna **Columna** del panel Criterios.  
  
5.  Si desea copiar las filas en un orden determinado, especifique un criterio de ordenación. Para detalles, consulte **Ordenar y agrupar los resultados de una consulta**.  
  
6.  Indique las filas que desea copiar especificando condiciones de búsqueda. Para detalles, consulte [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md).  
  
     Si no especifica ninguna condición de búsqueda, se copiarán todas las filas de la tabla de origen en la tabla de destino.  
  
    > [!NOTE]  
    >  Cuando se agrega una columna que se desea buscar al panel Criterios, el Diseñador de consultas y vistas la agrega también a la lista de columnas que se van a copiar. Si desea utilizar una columna para realizar una búsqueda, pero sin copiarla, desactive la casilla situada junto al nombre de columna en el rectángulo que representa la tabla o el objeto con estructura de tabla.  
  
7.  Si desea copiar información de resumen, especifique opciones Agrupar por. Para detalles, consulte [Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md).  
  
 Cuando se ejecuta una consulta de creación de tabla, los resultados no se incluyen en el [panel Resultados](results-pane-visual-database-tools.md). En su lugar, aparece un mensaje que indica cuántas filas se han copiado.  
  
## <a name="see-also"></a>Vea también  
 [Diseñar temas de procedimientos de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Tipos de consultas (Visual Database Tools)](types-of-queries-visual-database-tools.md)  
  
  
