---
title: Descripción de los grupos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10056"
- "10424"
ms.assetid: c32d4d89-45e4-4f77-a3e9-0429f53f9d6f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ccdef0ccb338f268abd205a95421382eb554fce9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104538"
---
# <a name="understanding-groups-report-builder-and-ssrs"></a>Descripción de los grupos (Generador de informes y SSRS)
  En el Generador de informes, un grupo es un conjunto de datos con nombre del conjunto de datos de informe que está enlazado a una región de datos. Básicamente, un grupo organiza una vista de un conjunto de datos de informe. Todos los grupos de una región de datos especifican vistas diferentes del mismo conjunto de datos de informe.  
  
 Para poder visualizar lo que es un grupo, consulte la ilustración siguiente que muestra la región de datos Tablix en la vista previa. En esta ilustración, los grupos de filas ordenan el conjunto de datos por tipo de producto y los grupos de columnas ordenan el conjunto de datos por región geográfica y año.  
  
 ![Tablix data region areas](../media/rs-tablixareas.gif "Tablix data region areas")  
  
 Las secciones siguientes sirven de ayuda para describir los distintos aspectos de los grupos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="what-makes-a-group"></a>¿En qué consiste un grupo?  
 Un grupo tiene un nombre y un conjunto de expresiones de grupo especificadas por el usuario. El conjunto de expresiones de grupo puede ser una referencia a un único campo de conjunto de datos o una combinación de varias expresiones. En tiempo de ejecución, las expresiones de grupo se combinan, si el grupo tiene varias expresiones, y se aplican a los datos de un grupo. Por ejemplo, imagine que tiene un grupo que usa un campo de fecha para organizar los datos de la región de datos. En tiempo de ejecución, los datos se organizan por fecha y, a continuación, se muestran con los totales de otros valores del conjunto de datos para cada fecha.  
  
## <a name="when-do-i-create-groups"></a>¿Cuándo debo crear grupos?  
 En la mayoría de los casos, el Generador de informes y el Diseñador de informes crean automáticamente un grupo al diseñar una región de datos. En una tabla, matriz o lista, se crean grupos al colocar campos en el panel Agrupación. En un gráfico, se crean grupos al colocar campos en las zonas de colocación del gráfico. En un medidor, debe usar el cuadro de diálogo de propiedades de medidor. En una tabla, matriz o lista, también es posible crear un grupo manualmente. Para más información, vea [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md). Para ver un ejemplo de cómo agregar grupos al crear un informe, consulte el [Tutorial: Creación de un informe de tabla básico &#40;Generador de informes&#41; ](../tutorial-creating-a-basic-table-report-report-builder.md) o [Creación de un informe de tabla básico &#40;Tutorial de SSRS&#41;](../create-a-basic-table-report-ssrs-tutorial.md).  
  
## <a name="how-can-i-modify-a-group"></a>¿Cómo puedo modificar un grupo?  
 Después de crear un grupo, puede establecer propiedades específicas de las regiones de datos, como expresiones de filtro y de ordenación, saltos de página y variables de grupo que contengan datos específicos del ámbito. Para obtener más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 Para modificar un grupo existente, abra el cuadro de diálogo de propiedades de grupo correspondiente. Puede cambiar el nombre del grupo. Asimismo, puede especificar expresiones de grupo basadas en un campo único o en varios campos, o en un parámetro de informe que especifique un valor en tiempo de ejecución. También puede basar un grupo en un conjunto de expresiones, como el conjunto de expresiones que especifican los intervalos de edad para los datos demográficos. Para obtener más información, vea [Ejemplos de expresión de grupo &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Si cambia el nombre de un grupo, debe actualizar manualmente las expresiones de grupo que hagan referencia al nombre anterior del grupo.  
  
## <a name="how-are-groups-organized"></a>¿Cómo se organizan los grupos?  
 Entender la organización de los grupos puede ayudarle a diseñar regiones de datos que muestran vistas diferentes de los mismos datos especificando expresiones de grupo idénticas.  
  
 Los grupos se organizan internamente como miembros de una o más jerarquías para cada región de datos. Una jerarquía de grupos consta de grupos primarios y secundarios que están anidados y que pueden tener grupos adyacentes.  
  
 Si piensa en los grupos primarios y secundarios como si se tratara de una estructura de árbol, cada jerarquía de grupos es un bosque de estructuras de árbol. Una región de datos Tablix incluye una jerarquía de grupos de filas y una jerarquía de grupos de columnas. Los datos asociados a los miembros del grupo de filas se expanden horizontalmente por la página, y los datos asociados a los miembros del grupo de columnas se expanden verticalmente por la página. El panel Agrupación muestra los miembros de los grupos de filas y de columnas para la región de datos Tablix seleccionada actualmente en la superficie de diseño. Para más información, vea [Panel de agrupación &#40;Generador de informes&#41;](grouping-pane-report-builder.md).  
  
 Una región de datos de gráfico incluye una jerarquía de grupos de categorías y una jerarquía de grupos de series. Los miembros del grupo de categorías se muestran en el eje de categorías y los miembros del grupo de series se muestran en el eje de serie.  
  
 Aunque normalmente no es necesario en las regiones de datos del medidor, los grupos le permiten especificar cómo agrupar los datos para agregarlos al medidor.  
  
## <a name="what-types-of-groups-are-available-per-data-region"></a>¿Qué tipos de grupos están disponibles por cada región de datos?  
 Las regiones de datos que se expanden como una cuadrícula no admiten los mismos grupos que las regiones de datos que muestran visualmente datos de resumen. Por lo tanto, una región de datos Tablix y las tablas, listas y matrices que están basadas en ella, admiten grupos distintos de los de un gráfico o medidor. En las secciones siguientes se describe el tipo y el propósito de la agrupación para cada tipo de región de datos.  
  
> [!NOTE]  
>  Aunque los grupos tienen nombres diferentes en regiones de datos diferentes, los principios en los que se basa la creación y el uso de los grupos son los mismos. Cuando se crea un grupo para una región de datos, se especifica una manera de organizar los datos detallados del conjunto de datos que está vinculado a la región de datos. Cada región de datos admite una estructura de grupo en la que mostrar los datos agrupados.  
  
### <a name="groups-in-a-tablix-data-region-details-row-and-column-groups"></a>Grupos de una región de datos Tablix: grupos de detalles, filas y columnas  
 Como se explicó anteriormente en este tema, una región de datos Tablix le permite organizar los datos en grupos por filas o por columnas. Sin embargo, los grupos de filas y de columnas no son los únicos grupos disponibles en una región de datos Tablix. Esta región de datos puede tener los tipos de grupos siguientes:  
  
-   **Grupo de detalles** : el grupo de detalles está compuesto por todos los datos de un conjunto de datos de informe después de que el Generador de informes o el Diseñador de informes apliquen filtros de conjuntos de datos y de regiones de datos. Por lo tanto, el grupo de detalles es el único grupo que no tiene ninguna expresión de grupo.  
  
     Básicamente, el grupo de detalles especifica los datos que se verían al ejecutar una consulta de conjunto de datos en un diseñador de consultas. Por ejemplo, imagine que tiene una consulta que recupera todas las columnas de una tabla de pedidos de venta. Por lo tanto, los datos de este grupo de detalles incluyen todos los valores para cada fila y para todas las columnas de la tabla. Los datos de este grupo de detalles también incluyen los valores para cualquier campo de conjunto de datos calculado que se haya creado.  
  
    > [!NOTE]  
    >  Los datos de un grupo de detalles también pueden incluir los agregados de servidor, que son agregados que se calculan en el origen de datos y se recuperan en la consulta. De forma predeterminada, el Generador de informes y el Diseñador de informes tratan los agregados de servidor como datos detallados a menos que el informe incluya una expresión que use la función Aggregate. Para obtener más información, vea [Aggregate](report-builder-functions-aggregate-function.md).  
  
     De forma predeterminada, al agregar una tabla o una lista al informe, el Generador de informes o el Diseñador de informes crean automáticamente el grupo de detalles y agregan una fila para mostrar los datos detallados. De forma predeterminada, al agregar campos de conjunto de datos a las celdas de esta fila, verá expresiones simples para los campos, por ejemplo, [Sales]. Al ver la región de datos, la fila de detalles se repite una vez para cada valor del conjunto de resultados.  
  
-   **Grupos de filas y grupos de columnas** : puede organizar los datos en grupos por filas o por columnas. Los grupos de filas se expanden verticalmente en una página. Los grupos de columnas se expanden horizontalmente en una página. Los grupos se pueden anidar; por ejemplo, agrupe primero por [Year], a continuación por [Quarter] y, por último, por [Month]. Los grupos también pueden ser adyacentes; por ejemplo, agrupe por [Territory] y, de forma independientemente, por [ProductCategory].  
  
     Al crear un grupo para una región de datos, el Generador de informes y el Diseñador de informes agregan automáticamente filas o columnas a dicha región de datos y usan estas filas o columnas para mostrar los datos del grupo.  
  
-   **Grupos de jerarquía recursiva** : un grupo de jerarquía recursiva organiza los datos de un único conjunto de datos de informe que incluye varios niveles. Por ejemplo, un grupo de jerarquía recursiva podría mostrar la jerarquía de una organización: [Empleado] que depende de [Empleado]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona propiedades de grupo y funciones integradas para permitirle crear grupos para este tipo de datos de informe. Para obtener más información, vea [Crear grupos de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
 La lista siguiente resume la forma de trabajar con grupos para cada región de datos:  
  
-   **Tabla** : defina grupos de filas anidados, adyacentes y de jerarquía recursiva (como en el caso de un organigrama). De forma predeterminada, una tabla incluye un grupo de detalles. Agregue los grupos arrastrando campos de conjunto de datos hasta el panel Agrupación para una tabla seleccionada.  
  
-   **Matriz** : defina grupos de filas y de columnas anidados, así como grupos de filas y columnas adyacentes. Agregue los grupos arrastrando campos de conjunto de datos hasta el panel Agrupación para una matriz seleccionada.  
  
-   **Lista** : de forma predeterminada, admite el grupo de detalles. Un uso típico consiste en admitir un nivel de agrupación. Agregue los grupos arrastrando campos de conjunto de datos hasta el panel Agrupación para una lista seleccionada.  
  
 Después de agregar un grupo, los identificadores de columna y de fila de la región de datos cambian para reflejar la pertenencia al grupo. Al eliminar un grupo, puede elegir entre eliminar únicamente la definición de grupo o eliminar el grupo y todas sus filas y columnas asociadas. Para más información, vea [Celdas, filas y columnas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Para limitar los datos que se deben mostrar o usar en los cálculos para los datos detallados o de grupo, establezca filtros en el grupo. Para obtener más información, vea [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md).  
  
 De forma predeterminada, al crear un grupo, la expresión de ordenación para éste es igual que la expresión de grupo. Para cambiar el criterio de ordenación, cambie la expresión de ordenación. Para obtener más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
#### <a name="understanding-group-membership-for-tablix-cells"></a>Descripción de la pertenencia a grupo para las celdas de Tablix  
 Las celdas de una fila o columna de una región de datos de Tablix pueden pertenecer a varios grupos de filas y de columnas. Al definir una expresión en el cuadro de texto de una celda que usa una función de agregado (por ejemplo, `=Sum(Fields!FieldName.Value`), el ámbito de grupo predeterminado para una celda es el grupo secundario más interior al que pertenece. Cuando una celda pertenece a grupos de filas y de columnas, el ámbito lo forman los dos grupos más interiores. También puede escribir expresiones que calculen subtotales agregados en el ámbito de un grupo relativo a otro conjunto de datos. Por ejemplo, puede calcular el porcentaje de un grupo relativo al grupo de columnas o a todos los datos de la región de datos (como `=Sum(Fields!FieldName.Value)/Sum(Fields!FieldName.Value,"ColumnGroup")`). Para más información, vea [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="see-also"></a>Vea también  
 [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)   
 [Agregar un total a un grupo o a una región de datos Tablix &#40;Generador de informes y SSRS&#41;](add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)   
 [Ordenar datos en una región de datos &#40;Generador de informes y SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Acción de obtención de detalles &#40;generador de informes y SSRS&#41;](drilldown-action-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
