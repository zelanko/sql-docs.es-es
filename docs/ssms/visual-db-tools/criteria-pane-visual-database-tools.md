---
title: Panel de criterios
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], Criteria pane
- View Designer, Criteria pane
- entering query options into grid [SQL Server]
- Criteria pane
- inserting query options into grid
- grid showing query options [SQL Server]
- adding query options into grid
ms.assetid: 6291affe-580e-482f-a7ff-45ce3837956a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 6f1df4856844b162560f562e487f970dc1974d04
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999959"
---
# <a name="criteria-pane-visual-database-tools"></a>Panel Criterios (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
El panel Criterios permite definir las opciones de consulta (como qué columnas de datos se van a mostrar, cómo se van a ordenar los resultados y qué filas se van a seleccionar); para ello, las opciones se deben escribir en una cuadrícula con forma de hoja de cálculo. En el panel Criterios, puede especificar:  
  
-   Las columnas que se van a mostrar y los alias de nombre de columna.  
  
-   La tabla a la que pertenece una columna.  
  
-   Las expresiones de columnas calculadas.  
  
-   El criterio de ordenación de la consulta.  
  
-   Las condiciones de búsqueda.  
  
-   El agrupamiento de criterios, incluidas las funciones de agregado que se van a utilizar para los informes de resumen.  
  
-   Los valores nuevos para las consultas UPDATE o INSERT INTO.  
  
-   Los nombres de columna de destino para las consultas INSERT FROM.  
  
Los cambios que realice en el panel Criterios se reflejarán automáticamente en el panel Diagrama y en el panel SQL. Asimismo, el panel Criterios se actualizará automáticamente para reflejar los cambios que se realicen en otros paneles.  
  
## <a name="about-the-criteria-pane"></a>Acerca del panel Criterios  
En el panel Criterios, las filas muestran las columnas de datos que se utilizan en la consulta y las columnas muestran las opciones de consulta.  
  
La información específica que aparezca en el panel Criterios dependerá del tipo de consulta que cree.  
  
Si no se ve el panel Criterios, haga clic con el botón derecho en el diseñador, seleccione **Panel**y haga clic en **Criterios**.  
  
## <a name="options"></a>Opciones  
  
|**Columna**|**Tipo de consulta**|**Descripción**|  
|--------------|------------------|-------------------|  
|Columna|All|Muestra el nombre de una columna de datos utilizada para la consulta o la expresión de una columna calculada. Esta columna está bloqueada de modo que sea siempre visible a medida que se desplaza horizontalmente.|  
|Alias|SELECT, INSERT FROM, UPDATE, MAKE TABLE|Especifica un nombre alternativo para una columna o el nombre que puede utilizar para una columna calculada.|  
|Tabla|SELECT, INSERT FROM, UPDATE, MAKE TABLE|Especifica el nombre de la tabla u objeto con estructura de tabla para la columna de datos asociada. Esta columna está en blanco para las columnas calculadas.|  
|Output|SELECT, INSERT FROM, MAKE TABLE|Especifica si una columna de datos aparece en los resultados de consulta.<br /><br />Nota: Si la base de datos lo permite, puede utilizar una columna de datos para las cláusulas de orden o búsqueda sin mostrarla en el conjunto de resultados.|  
|Tipo de orden|SELECT, INSERT FROM|Especifica que se utiliza la columna de datos asociada para ordenar los resultados de una consulta y si el orden es ascendente o descendente.|  
|Criterio de ordenación|SELECT, INSERT FROM|Especifica la prioridad de orden de las columnas de datos utilizadas para ordenar el conjunto de resultados. Cuando cambia el criterio de ordenación de una columna de datos, el criterio de ordenación del resto de las columnas se actualiza en consecuencia.|  
|Agrupar por|SELECT, INSERT FROM, MAKE TABLE|Especifica que la columna de datos asociada se está utilizando para crear una consulta de funciones agregadas. Esta columna de cuadrícula aparece solamente si ha elegido **Agrupar por** en el menú **Herramientas** o si ha agregado una cláusula GROUP BY al panel SQL.<br /><br />De forma predeterminada, el valor de esta columna se establece en **Agrupar por**y la columna se incluye en la cláusula GROUP BY.<br /><br />Al moverse a una celda de esta columna y seleccionar una función de agregado para aplicar a la columna de datos asociada, se agrega la expresión resultante de forma predeterminada como una columna de resultados para el conjunto de resultados.|  
|Criterios|All|Especifica una condición de búsqueda (filtro) para la columna de datos asociada. Escriba un operador (el predeterminado es "=") y el valor que haya que buscar. Incluya los valores de texto entre comillas simples.<br /><br />Si la columna de datos asociada forma parte de una cláusula GROUP BY, la expresión especificada se utilizará para una cláusula HAVING.<br /><br />Si especifica valores para más de una celda de la columna de cuadrícula **Criterios**, las condiciones de búsqueda resultantes se vinculan de forma automática con un operador lógico AND.<br /><br />Para especificar varias expresiones de condición de búsqueda para una sola columna de base de datos, por ejemplo (fname > 'A') AND (fname < 'M'), agregue la columna de datos al panel Criterios dos veces y especifique valores independientes en la columna de cuadrícula **Criterios** para cada instancia de la columna de datos.|  
|O...|All|Especifica una expresión de condición de búsqueda adicional para la columna de datos, vinculada a expresiones previas con un operador lógico OR. Puede agregar más columnas de cuadrícula **O…** presionando la tecla TAB en la columna **O…** situada más a la derecha.|  
|Append|INSERT FROM|Especifica el nombre de la columna de datos de destino de la columna de datos asociada. Al crear una consulta Insert From, el Diseñador de consultas y vistas intenta hacer coincidir el origen con una columna de datos de destino adecuada. Si el Diseñador de consultas y vistas no puede elegir una columna coincidente, se deberá proporcionar el nombre de columna.|  
|Valor nuevo|UPDATE, INSERT INTO|Especifica el valor que se va a colocar en la columna asociada. Escriba un valor literal o una expresión.|  
  
## <a name="see-also"></a>Consulte también  
[Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Panel Diagrama &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md)  
[Reglas para especificar valores de búsqueda &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Ordenar y agrupar los resultados de una consulta &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Panel Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)  
[Panel SQL &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)  
  
