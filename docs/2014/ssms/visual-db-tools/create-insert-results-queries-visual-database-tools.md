---
title: Crear consultas de inserción de resultados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- queries [SQL Server], types
- result sets [SQL Server], queries
- results [SQL Server], query
- Insert Results query
- queries [SQL Server], results
ms.assetid: 8770d630-09cc-47ec-a0e9-e9de2d7bbc89
author: stevestein
ms.author: sstein
ms.openlocfilehash: c5dfd7df8104519cf09ad72ffee3c5214af2a3d8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058167"
---
# <a name="create-insert-results-queries-visual-database-tools"></a>Crear consultas de inserción de resultados (Visual Database Tools)
  Puede copiar filas de una tabla a otra o dentro de una misma tabla utilizando una consulta de inserción de resultados. Por ejemplo, en una tabla `titles` , puede utilizar una consulta de inserción de resultados para copiar la información de todos los títulos de una editorial en una segunda tabla y proporcionar esa tabla a la editorial. Una consulta de inserción de resultados es similar a una consulta de creación de tabla, con la diferencia de que la primera copia las filas en una tabla existente.  
  
> [!TIP]  
>  También puede copiar filas de una tabla a otra mediante las funciones de cortar y pegar. Cree una consulta para cada tabla y ejecútelas. Copie las filas que desee de una cuadrícula de resultados a la otra.  
  
 Cuando se crea una consulta de inserción de resultados, se especifica:  
  
-   La tabla de base de datos en la que se van a copiar las filas (la tabla de destino).  
  
-   Las tablas de las que se van a copiar filas (tabla de origen). Las tablas de origen forman parte de una subconsulta. Si va a copiar datos dentro de una tabla, la tabla de origen es la misma que la tabla de destino.  
  
-   Las columnas de la tabla de origen cuyo contenido desea copiar.  
  
-   Las columnas de la tabla de destino en las que se van a copiar los datos.  
  
-   Las condiciones de búsqueda que definen las filas que desea copiar.  
  
-   El criterio de ordenación, si desea copiar las filas en un orden determinado.  
  
-   Las opciones Agrupar por, si solo desea copiar información de resumen.  
  
 Por ejemplo, la siguiente consulta copia la información de títulos de la tabla `titles` a una tabla de almacenamiento denominada `archivetitles`. La consulta copia el contenido de cuatro columnas de todos los títulos que pertenecen a una determinada editorial:  
  
```  
INSERT INTO archivetitles   
   (title_id, title, type, pub_id)  
SELECT title_id, title, type, pub_id  
FROM titles  
WHERE (pub_id = '0766')  
```  
  
> [!NOTE]  
>  Para insertar valores en una nueva fila, utilice una consulta de inserción de valores.  
  
 Puede copiar el contenido de columnas seleccionadas o de todas las columnas de una fila. En ambos casos, los datos que se copian deben ser compatibles con las columnas de las filas en las que se van a copiar estos datos. Por ejemplo, si copia el contenido de una columna como `price`, la columna de la fila donde realice la copia debe aceptar datos numéricos con decimales. Si copia una fila entera, la tabla de destino debe tener columnas compatibles en la misma posición física que la tabla de origen.  
  
 Cuando se crea una consulta de inserción de resultados, el panel Criterios varía para reflejar las opciones disponibles para la copia de datos. Se agrega una columna Anexar que permite especificar las columnas en las que deben copiarse los datos.  
  
> [!CAUTION]  
>  No se puede deshacer la operación de ejecutar una consulta de inserción de resultados. Como medida de precaución, haga una copia de seguridad de los datos antes de ejecutar la consulta.  
  
### <a name="to-create-an-insert-results-query"></a>Para crear una consulta de inserción de resultados  
  
1.  Cree una nueva consulta y agregue la tabla cuyas filas desea copiar (la tabla de origen). Si va a copiar datos dentro de una tabla, puede agregar la tabla de origen como tabla de destino.  
  
2.  En el menú **Diseñador de consultas** , seleccione **Cambiar tipo**y, a continuación, haga clic en **Insertar resultados**.  
  
3.  En el [cuadro de diálogo Elegir tabla de destino para Insertar resultados](visual-database-tools.md), seleccione la tabla en la que va a copiar filas (la tabla de destino).  
  
    > [!NOTE]  
    >  El Diseñador de consultas y vistas no puede determinar con antelación las tablas y vistas que se pueden actualizar. Por tanto, en la lista **Nombre de la tabla** del cuadro de diálogo **Elegir tabla de destino para Insertar resultados** , se muestran todas las tablas y vistas disponibles en la conexión de datos que está consultando, incluso aquellas en las que no se pueden copiar filas.  
  
4.  En el rectángulo que representa la tabla o el objeto con valores de tabla, elija los nombres de las columnas cuyo contenido desea copiar. Para copiar filas enteras, elija ** \* (todas las columnas)**.  
  
     El Diseñador de consultas y vistas agrega las columnas elegidas a la columna **Columna** del panel Criterios.  
  
5.  En la columna **Anexar** del panel Criterios, seleccione una columna de la tabla de destino para cada columna que vaya a copiar. Elija *TableName. \* * si va a copiar filas enteras. Las columnas de la tabla de destino deben tener el mismo tipo de datos que las columnas de la tabla de origen o un tipo de datos compatible.  
  
6.  Si desea copiar las filas en un orden determinado, especifique un criterio de ordenación. Para detalles, consulte [Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md).  
  
7.  Indique las filas que desea copiar especificando condiciones de búsqueda en la columna **Filtro** . Para detalles, consulte [Especificar criterios de búsqueda &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md).  
  
     Si no especifica ninguna condición de búsqueda, se copiarán todas las filas de la tabla de origen en la tabla de destino.  
  
    > [!NOTE]  
    >  Cuando se agrega una columna que se desea buscar al panel Criterios, el Diseñador de consultas y vistas la agrega también a la lista de columnas que se van a copiar. Si desea utilizar una columna para realizar una búsqueda, pero sin copiarla, desactive la casilla situada junto al nombre de columna en el rectángulo que representa la tabla o el objeto con valores de tabla.  
  
8.  Si desea copiar información de resumen, especifique opciones Agrupar por. Para detalles, consulte [Resumir los resultados de una consulta &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md).  
  
 Cuando se ejecuta una consulta de inserción de resultados, los resultados no se incluyen en el [panel Resultados](results-pane-visual-database-tools.md). En su lugar, aparece un mensaje que indica cuántas filas se han copiado.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de consultas &#40;Visual Database Tools&#41;](types-of-queries-visual-database-tools.md)   
 [Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
