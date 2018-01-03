---
title: "Crear consultas de creación de tabla (Visual Database Tools) | Microsoft Docs"
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
- queries [SQL Server], types
- table creation [SQL Server], Make Table query
- inserting tables
- Make Table query
- adding tables
ms.assetid: 4493cffa-7b2d-4c24-8ef0-d49329198972
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4c9b53ac6d1a3840f182bf58096a8595c941c8f3
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="create-make-table-queries-visual-database-tools"></a>Crear consultas de creación de tabla (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Puede copiar filas en una nueva tabla mediante una consulta de creación de tabla, que sirve para crear subconjuntos de datos con los que trabajar o copiar el contenido de una tabla de una base de datos a otra. La consulta de creación de tabla es similar a la consulta de inserción de resultados, con la diferencia de que en la primera se crea una nueva tabla en la que se copian las filas.  
  
Cuando se crea una consulta de creación de tabla, se especifica:  
  
-   El nombre de la nueva tabla de base de datos (la tabla de destino).  
  
-   Las tablas de las que se van a copiar filas (tabla de origen). Puede copiar de una sola tabla o de tablas combinadas.  
  
-   Las columnas de la tabla de origen cuyo contenido desea copiar.  
  
-   El criterio de ordenación, si desea copiar las filas en un orden determinado.  
  
-   Las condiciones de búsqueda que definen las filas que desea copiar.  
  
-   Las opciones Agrupar por, si solo desea copiar información de resumen.  
  
Por ejemplo, en la consulta siguiente se crea una nueva tabla denominada `uk_customers` y se copia en ella información de la tabla `customers`:  
  
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
  
4.  Defina las columnas que se van a copiar agregándolas a la consulta. Para detalles, consulte [Agregar columnas a las consultas (Visual Database Tools)](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md). Las columnas se copian solo si se agregan a la consulta. Para copiar filas enteras, elija **\&#42; (Todas las columnas)**.  
  
    El Diseñador de consultas y vistas agrega las columnas elegidas a la columna **Columna** del panel Criterios.  
  
5.  Si desea copiar las filas en un orden determinado, especifique un criterio de ordenación. Para detalles, consulte **Ordenar y agrupar los resultados de una consulta**.  
  
6.  Indique las filas que desea copiar especificando condiciones de búsqueda. Para detalles, consulte [Especificar criterios de búsqueda (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
    Si no especifica ninguna condición de búsqueda, se copiarán todas las filas de la tabla de origen en la tabla de destino.  
  
    > [!NOTE]  
    > Cuando se agrega una columna que se desea buscar al panel Criterios, el Diseñador de consultas y vistas la agrega también a la lista de columnas que se van a copiar. Si desea utilizar una columna para realizar una búsqueda, pero sin copiarla, desactive la casilla situada junto al nombre de columna en el rectángulo que representa la tabla o el objeto con estructura de tabla.  
  
7.  Si desea copiar información de resumen, especifique opciones Agrupar por. Para detalles, consulte [Resumir los resultados de una consulta (Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md).  
  
Cuando se ejecuta una consulta de creación de tabla, los resultados no se incluyen en el [panel Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). En su lugar, aparece un mensaje que indica cuántas filas se han copiado.  
  
## <a name="see-also"></a>Ver también  
[Temas de procedimientos de diseño de consultas y vistas (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Tipos de consultas (Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
