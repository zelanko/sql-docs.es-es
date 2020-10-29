---
description: Panel Diagrama (Visual Database Tools)
title: panel Diagrama
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Diagram pane
- View Designer, Diagram pane
- joins [SQL Server], Query and View Designer
- Diagram pane [Visual Database Tools]
ms.assetid: 399dfc7b-e2e7-47d3-bd11-163cbe0ce13c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: eaba2d8acd2a0443bfe2ed97fc53b50fcb667629
ms.sourcegitcommit: fb8724fb99c46ecf3a6d7b02a743af9b590402f0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2020
ms.locfileid: "92439389"
---
# <a name="diagram-pane-visual-database-tools"></a>Panel Diagrama (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
El panel Diagrama muestra una presentación gráfica de las tablas o de los objetos con valores de tabla que ha seleccionado en la conexión de datos. También muestra todas las relaciones de combinación entre ellos.  
  
En el panel Diagrama puede:  
  
-   Agregar o quitar tablas y objetos con valores de tabla y especificar columnas de datos para los resultados.  
  
-   Crear o modificar combinaciones entre tablas y objetos con valores de tabla.  
  
Al realizar un cambio en el panel Diagrama, el panel Criterios y el panel SQL se actualizan para reflejar dicho cambio. Por ejemplo, si selecciona una columna en los resultados de una ventana de tabla o de objeto con valores de tabla en el panel Diagrama, el Diseñador de consultas y vistas agregará la columna de datos al panel Criterios y la instrucción SQL al panel SQL.  
  
Cada tabla u objeto con valores de tabla aparece como una ventana independiente en el panel Diagrama. El icono de la barra de título de cada rectángulo indica qué tipo de objeto representa el rectángulo, tal y como se ilustra en la tabla siguiente.  
  
## <a name="options"></a>Opciones  
**Tablas**  
Muestra las tablas que puede agregar al panel Diagrama. Para agregar una tabla, selecciónela y haga clic en **Agregar** . Para agregar varias tablas al mismo tiempo, selecciónelas y haga clic en **Agregar** .  
  
**Vistas**  
Muestra las vistas que puede agregar al panel Diagrama. Para agregar una vista, selecciónela y haga clic en **Agregar** . Para agregar varias vistas al mismo tiempo, selecciónelas y haga clic en **Agregar** .  
  
**Funciones**  
Muestra las funciones definidas por el usuario que puede agregar al panel Diagrama. Para agregar una función, selecciónela y haga clic en **Agregar** . Para agregar varias funciones al mismo tiempo, selecciónelas y haga clic en **Agregar** .  
  
**Tablas locales**  
Muestra las tablas creadas mediante consultas en lugar de mostrar las que pertenecen a la base de datos.  
  
**Sinónimos**  
Muestra los sinónimos que se pueden agregar en el panel Diagrama. Para agregar un sinónimo, selecciónelo y haga clic en **Agregar** . Para agregar varios sinónimos al mismo tiempo, selecciónelos y haga clic en **Agregar** .  
  
|Icono|Tipo de objeto|  
|--------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi1.gif":::|Tabla|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi2.gif":::|Consulta o vista|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi3.gif":::|Tabla vinculada|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dvudficon.gif":::|Función definida por el usuario|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi5.gif":::|Vista vinculada|  
  
Cada rectángulo muestra las columnas de datos de la tabla o del objeto con valores de tabla. Al lado de los nombres de las columnas aparecen casillas y símbolos que indican cómo utilizar las columnas en la consulta. La información sobre herramientas muestra información como el tamaño y el tipo de datos de las columnas.  
  
La tabla siguiente muestra las casillas y los símbolos utilizados en el rectángulo de cada tabla o de cada objeto con valores de tabla.  
  
|casilla o símbolo|Description|  
|-----------------------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi7.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi8.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbi9.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbia.gif":::|Especifica si una columna de datos aparece en el conjunto de resultados de consulta (consulta Select) o si se utiliza en una consulta Update, Insert From, Make Table o Insert Into. Seleccione la columna para agregarla a los resultados. Si selecciona **(Todas las columnas)** , aparecerán todas las columnas de datos en los resultados.<br /><br />El icono utilizado con la casilla cambia según el tipo de consulta que esté creando. Al crear una consulta Eliminar, no puede seleccionar columnas individuales.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbib.gif":::<br /><br />:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbic.gif":::|Indica que la columna de datos se está utilizando para ordenar los resultados de una consulta (forma parte de una cláusula ORDER BY). El icono aparece como A-Z si el criterio de ordenación es ascendente o como Z-A si el criterio de ordenación es descendente.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbid.gif":::|Indica que la columna de datos se está utilizando para crear un conjunto de resultados agrupado (forma parte de una cláusula GROUP BY) en una consulta de funciones agregadas.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbie.gif":::|Indica que la columna de datos está incluida en una condición de búsqueda de la consulta (forma parte de una cláusula WHERE o HAVING).|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbif.gif":::|Indica que el contenido de la columna de datos se está resumiendo para obtener los resultados (está incluida en SUM, AVG u otra función de agregado).|  
  
> [!NOTE]  
> El Diseñador de consultas no mostrará las columnas de datos de una tabla o un objeto con valores de tabla si no tiene suficientes derechos de acceso o si el controlador de base de datos no puede devolver información acerca de la tabla o del objeto. En estos casos, el Diseñador de consultas y vistas muestra solamente una barra de título para la tabla u objeto con estructura de tabla.  
  
## <a name="joined-tables-on-the-diagram-pane"></a>Tablas combinadas en el panel Diagrama  
Si la consulta requiere una combinación, aparece una línea de combinación entre las columnas de datos implicadas en ella. Si no se muestran las columnas de datos combinadas (por ejemplo, si la ventana de la tabla o del objeto con valores de tabla está minimizada o la combinación incluye una expresión), el Diseñador de consultas y vistas coloca la línea de combinación en la barra de título del rectángulo que representa la tabla o el objeto con valores de tabla. El Diseñador de consultas y vistas muestra una línea de combinación para cada condición de combinación.  
  
La forma del icono situado en el centro de la línea de combinación indica cómo se combinan las tablas u objetos con estructura de tabla. Si la cláusula de combinación utiliza un operador distinto de igual (=), el operador se muestra en el icono de línea de combinación. La tabla siguiente muestra los iconos que pueden aparecer en una línea de combinación.  
  
|Icono de línea de combinación|Description|  
|------------------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbih.gif":::|Combinación interna (creada mediante el signo igual).|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbii.gif":::|Combinación interna basada en el operador "mayor que". (El operador mostrado en el icono de línea de combinación refleja el operador utilizado en la combinación.)|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbij.gif":::|Combinación externa en la que se incluirán todas las filas de la tabla representada a la izquierda, incluso si no tienen coincidencias en la tabla relacionada.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbik.gif":::|Combinación externa en la que se incluirán todas las filas de la tabla representada a la derecha, incluso si no tienen coincidencias en la tabla relacionada.|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbil.gif":::|Combinación externa completa en la que se incluirán todas las filas de ambas tablas, incluso si no tienen coincidencias en la tabla relacionada.|  
  
Los iconos situados en los extremos de la línea de combinación indican el tipo de combinación. La tabla siguiente muestra los tipos de combinaciones y los iconos que pueden aparecer en los extremos de la línea de combinación.  
  
|Icono situado en los extremos de la línea de combinación|Description|  
|-----------------------------|---------------|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbim.gif":::|Combinación uno a uno|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbin.gif":::|Combinación uno a varios|  
|:::image type="icon" source="../../ssms/visual-db-tools/media/dv3wbio.gif ":::|El Diseñador de consultas y vistas no puede determinar el tipo de combinación|  
  
## <a name="see-also"></a>Consulte también  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Panel Criterios &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
