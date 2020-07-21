---
title: Crear consultas de creación de tabla
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- table creation [SQL Server], Make Table query
- inserting tables
- Make Table query
- adding tables
ms.assetid: 4493cffa-7b2d-4c24-8ef0-d49329198972
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 8b4503c55545867639a3a437371d6265a85706af
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "80271481"
---
# <a name="create-make-table-queries-visual-database-tools"></a>Crear consultas de creación de tabla (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede copiar filas en una nueva tabla mediante una consulta de creación de tabla, que sirve para crear subconjuntos de datos con los que trabajar o para copiar el contenido de una tabla de una base de datos a otra. La consulta de creación de tabla es similar a la consulta de inserción de resultados, con la diferencia de que en la primera se crea una nueva tabla en la que se copian las filas.  
  
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
  
4.  Defina las columnas que se van a copiar agregándolas a la consulta. Para obtener más información, vea [Agregar columnas a las consultas](../../ssms/visual-db-tools/add-columns-to-queries-visual-database-tools.md). Las columnas se copian solo si se agregan a la consulta. Para copiar filas enteras, elija **&#42; (Todas las columnas)** .  
  
    El Diseñador de consultas y vistas agrega las columnas elegidas a la columna **Columna** del panel Criterios.  
  
5.  Si desea copiar las filas en un orden determinado, especifique un criterio de ordenación. Para detalles, consulte **Ordenar y agrupar los resultados de una consulta**.  
  
6.  Indique las filas que desea copiar especificando condiciones de búsqueda. Para obtener detalles, vea [Especificar criterios de búsqueda](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md).  
  
    Si no especifica ninguna condición de búsqueda, se copiarán todas las filas de la tabla de origen en la tabla de destino.  
  
    > [!NOTE]  
    > Cuando se agrega una columna que se desea buscar al panel Criterios, el Diseñador de consultas y vistas la agrega también a la lista de columnas que se van a copiar. Si desea utilizar una columna para realizar una búsqueda, pero sin copiarla, desactive la casilla situada junto al nombre de columna en el rectángulo que representa la tabla o el objeto con estructura de tabla.  
  
7.  Si desea copiar información de resumen, especifique opciones Agrupar por. Para obtener detalles, vea [Resumen de los resultados de una consulta](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md).  
  
Cuando se ejecuta una consulta de creación de tabla, los resultados no se incluyen en el [panel Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). En su lugar, aparece un mensaje que indica cuántas filas se han copiado.  
  
## <a name="see-also"></a>Consulte también  
[Temas de procedimientos de diseño de consultas y vistas](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
Tipos de consultas(../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
