---
title: Filtrar, agrupar y ordenar datos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.categorygroupproperties.sorting.f1
- "10403"
- sql12.rtp.rptdesigner.seriesgroupproperties.sorting.f1
- "10402"
- sql12.rtp.rptdesigner.seriesgroupproperties.general.f1
- "10410"
- sql12.rtp.rptdesigner.categorygroupproperties.general.f1
- "10412"
ms.assetid: 4dda2a7f-3f31-47e9-a88b-28d770ebd65e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 776b240f17d40c64c63648175b2c5c15a532fb48
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294693"
---
# <a name="filter-group-and-sort-data-report-builder-and-ssrs"></a>Filtrar, agrupar y ordenar datos (Generador de informes y SSRS)
  En un informe, las expresiones sirven para ayudar a controlar, organizar y ordenar los datos de informe. De forma predeterminada, cuando se crean conjuntos de datos y se diseñan informes, las propiedades de los elementos de informe están se establecen de forma automática en las expresiones basadas en los campos de conjunto de datos, los parámetros y otros elementos que aparecen en el panel Datos de informe. Puede agregar también un botón de ordenación interactivo a una tabla o a una celda de la matriz para permitir a los usuarios cambiar el criterio de ordenación de las filas para los grupos o las filas dentro de los grupos.  
  
-   **Expresiones de filtro** : las expresiones de filtro prueban los datos para incluirlos o excluirlos en función de una comparación especificada por el usuario. Los filtros se aplican a los datos de un informe una vez recuperados de una conexión de datos. Puede agregar cualquier combinación de filtros a los siguientes elementos: una definición de conjunto de datos compartido del servidor de informes; una instancia de un conjunto de datos compartido o incrustado de un informe; una región de datos, como una tabla o un gráfico, o un grupo de regiones de datos, como un grupo de filas de una tabla o un grupo de categorías de un gráfico.  
  
-   **Expresiones de grupo** : una expresión de grupo organiza los datos en base a un campo de conjunto de datos u otro valor. Las expresiones de grupo se crean automáticamente a medida que se diseña el informe. El procesador de informes evalúa las expresiones de grupo una vez aplicados los filtros a los datos y a medida que se combinan los datos del informe y las regiones de datos. Podrá personalizar una expresión de grupo una vez creada.  
  
-   **Expresiones de ordenación** : una expresión de ordenación controla el orden en el que aparecen los datos en una región de datos. Las expresiones de ordenación se crean automáticamente a medida que se diseña el informe. De forma predeterminada, la expresión de ordenación de un grupo se establece en el mismo valor que la expresión de grupo. Podrá personalizar una expresión de ordenación una vez creada.  
  
-   **Ordenación interactiva** : para permitir a los usuarios ordenar o invertir el criterio de ordenación de una columna, puede agregar un botón de ordenación interactivo a un encabezado de columna o a una celda del encabezado de grupo en una tabla o matriz.  
  
 Para ayudar a los usuarios a personalizar las expresiones de filtro, grupo u ordenación, puede cambiar una expresión para agregar una referencia a un parámetro de informe. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-parameters-report-builder-and-report-designer.md).  
  
 Para obtener más información y ejemplos, vea los siguientes temas:  
  
-   [Ejemplos de expresión de grupo &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
-   [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [Tutoriales &#40;generador de informes&#41;](../report-builder-tutorials.md)  
  
-   [Tutoriales de Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
-   [Ejemplos de informes (Generador de informes y SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Filtering"></a> Filtrar los datos del informe  
 Los filtros son las partes de un informe que ayudan a controlar los datos del informe una vez recuperados de la conexión de datos. Utilice filtros cuando no pueda cambiar una consulta de conjunto de datos para filtrar datos antes de recuperarlos de un origen de datos externo.  
  
 Siempre que resulte posible, cree consultas de conjunto de datos que devuelvan solo los datos que necesite mostrar en el informe. Al reducir la cantidad de los datos que se deben recuperar y procesar, contribuirá a mejorar el rendimiento del informe. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Una vez recuperados los datos del origen de datos externo, podrá agregar filtros a los conjuntos de datos, regiones de datos y grupos de regiones de datos, incluidos los grupos de detalles. Los filtros se aplican en tiempo de ejecución y en este orden: primero en el conjunto de datos, a continuación, en la región de datos y, por último, en el grupo; en las jerarquías de grupo, se aplican en orden descendente. En una tabla, matriz o lista, los filtros de los grupos de filas, los grupos de columnas y los grupos adyacentes se aplican de forma independiente. En un gráfico, también se aplican de forma independiente los filtros de los grupos de categorías y los grupos de series. Para obtener más información, vea [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md).  
  
 Para cada filtro, especifique una *ecuación de filtro*. Una ecuación de filtro incluye un campo de conjunto de datos o una expresión que especifica los datos que se van a filtrar, un operador y un valor con el que realizar la comparación. Cuando se procese el elemento, solo se incluirán los valores de datos que coincidan con la condición de filtro.  
  
 Para permitir a los usuarios controlar los datos de un informe, puede incluir parámetros en las expresiones de filtro. Para más información, vea [Usar referencias a la colección de parámetros &#40;Generador de informes y SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md).  
  
 Para personalizar una vista para cada usuario, puede incluir una referencia al campo integrado UserID en un filtro. Para obtener más información, vea [Referencias a campos globales y de usuario integrados &#40;Generador de informes y SSRS&#41;](built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Grouping"></a> Agrupar los datos del informe  
 Los grupos organizan los datos de un informe para mostrarlos o calcular los valores agregados. Entender cómo se definen los grupos y se utilizan las características de grupo le ayudará a diseñar informes más concisos.  
  
 Las expresiones de grupo se crean automáticamente cuando se realiza una de las siguientes acciones:  
  
-   Organice los campos de conjunto de datos en un tabla, matriz, asistente para gráficos o campos coincidentes en el Asistente para mapas.  
  
-   En una tabla, matriz o lista, agregue un campo al área Grupos de filas o Grupos de columnas del panel Agrupación.  
  
-   En un gráfico, agregue un campo al área Grupos de categorías o Grupos de series en el panel Datos del gráfico.  
  
-   En un mapa, especifique un campo para comparar los elementos del mapa con datos analíticos en el elemento de menú contextual de datos de capa.  
  
 Un grupo forma parte de la definición de informe. Cada grupo tiene un nombre. De forma predeterminada, el nombre de grupo es el campo de conjunto de datos en el que se basa.  
  
 En una región de datos de tabla o de matriz, puede crear varios grupos de filas y de columnas. Para mostrar los datos en una jerarquía visual, organice grupos anidados, grupos adyacentes y grupos de jerarquía recursiva (por ejemplo, un organigrama).  
  
 El nombre de grupo identifica un ámbito de expresión. Puede especificar el nombre de un grupo como un ámbito en el que calcular agregados, organizar datos jerárquicamente y alternar la presentación de los nodos secundarios de los nodos primarios en un informe detallado, mostrar vistas diferentes de los mismos datos en varias regiones de datos y visualizar datos de resumen en una tabla, matriz, gráfico, medidor o mapa. Para obtener más información, vea [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)subyacente.  
  
 Para realizar la agrupación según varios campos de conjunto de datos, agregue cada campo al conjunto de expresiones de grupo. También puede escribir sus propias expresiones de grupo en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Por ejemplo, puede agrupar por un intervalo de valores o usando un parámetro de informe que permita al usuario seleccionar el modo de agrupar los datos de una región de datos. Para obtener más información, vea [Ejemplos de expresión de grupo &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
 En la presentación del informe, puede agregar saltos de página antes y después de cada grupo, o de cada instancia de un grupo, para reducir la cantidad de datos mostrados en cada página y administrar el rendimiento del proceso de representación de informes. Para más información, vea [Agregar un salto de página &#40;Generador de informes y SSRS&#41;](add-a-page-break-report-builder-and-ssrs.md).  
  
 Crear grupos de regiones de datos es una manera de organizar los datos en un informe. Existen otras maneras de organizar los datos, cada una de ellas con sus propias ventajas. Para obtener más información, vea [Obtención de detalles, informes detallados, subinformes y regiones de datos anidadas &#40;Generador de informes y SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
### <a name="defining-group-variables"></a>Definir variables de grupo  
 Al definir un grupo, puede crear una variable de grupo para utilizar en expresiones cuyo ámbito es el grupo y a las que se puede obtener acceso desde los grupos anidados. Una variable de grupo se calcula una vez por instancia de grupo y se puede obtener acceso a ella desde expresiones en grupos secundarios. Por ejemplo, para los datos que están agrupados por región y subregión, se puede calcular un impuesto para cada región y utilizarlo en los cálculos del grupo de subregiones.  
  
 Para obtener más información, vea [Referencias a las colecciones de variables de informe y de grupo &#40;Generador de informes y SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
### <a name="groups-and-scope-in-data-regions"></a>Grupos y ámbitos de regiones de datos  
 Para proporcionar varias vistas de los datos del mismo conjunto de datos, puede especificar las mismas expresiones de grupo para cada región de datos. Por ejemplo, puede mostrar los datos por categorías en una tabla para mostrar todos los datos detallados y mostrar los agregados en un gráfico circular para ayudar a visualizar cada categoría en relación con el conjunto de datos completo. Para obtener más información, vea [Vincular varias regiones de datos al mismo conjunto de datos &#40;Generador de informes y SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md).  
  
 Al anidar una región de datos en la celda de una tabla, una matriz o una lista, el ámbito de los datos se establecerá automáticamente en las pertenencias de grupo más internas de la celda. Por ejemplo, supongamos que agrega un gráfico a una celda que se encuentra en un grupo de filas y en un grupo de columnas. Los datos disponibles para ese gráfico pertenecerán al ámbito de la instancia del grupo de filas más interior y de la instancia del grupo de columnas más interior en tiempo de ejecución. Para obtener más información, vea [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)subyacente.  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="Sorting"></a> Ordenar los datos del informe  
 Para controlar el criterio de ordenación de los datos del informe, puede ordenar los datos en una consulta de conjunto de datos o definir una expresión de ordenación para un grupo o una región de datos. También puede agregar botones de ordenación interactiva a las tablas y matrices para que los usuarios puedan cambiar el criterio de ordenación de las filas.  
  
 Los tres tipos de ordenaciones se pueden combinar en el mismo informe. De forma predeterminada, el orden en el que la consulta de conjunto de datos devuelve los datos determina el criterio de ordenación. Las expresiones de ordenación se aplican en la región de datos y el grupo de regiones de datos. Las ordenaciones interactivas se aplican después de las expresiones de ordenación.  
  
 El criterio de ordenación no afecta a la mayoría de los resultados de las expresiones que contienen funciones de agregado. Los valores devueltos para las siguientes funciones de agregado se ven afectadas por el criterio de ordenación:: Primero, último y anterior. Para más información, vea [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
### <a name="sorting-data-in-a-dataset-query"></a>Ordenar datos en una consulta de conjunto de datos  
 Incluya el criterio de ordenación en la consulta de conjunto de datos para preordenar los datos antes de que estos se recuperen para un informe. La ordenación de los datos en la consulta permite que el trabajo de ordenación lo realice el origen de datos en lugar del procesador de informes.  
  
 Puede agregar una cláusula ORDER BY a la consulta de conjunto de datos para un tipo de origen de datos [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por ejemplo, la consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] siguiente ordena las columnas Sales y Region por la columna Sales en orden descendente en la tabla SalesOrders: `SELECT Sales, Region FROM SalesOrders ORDER BY Sales DESC`. Para obtener más información, vea el tema que explica cómo ordenar filas con ORDER BY en los [Libros en pantalla de SQL Server](https://go.microsoft.com/fwlink/?linkid=98335).  
  
> [!NOTE]  
>  No todos los orígenes de datos permiten especificar el criterio de ordenación en la consulta.  
  
### <a name="sorting-data-with-sort-expressions"></a>Ordenar datos con expresiones de ordenación  
 Para ordenar los datos del informe una vez recuperados del origen de datos, puede establecer expresiones de ordenación en una región de datos Tablix o en un grupo, incluyendo el grupo de detalles. En la lista siguiente se describe el efecto de establecer expresiones de ordenación en elementos diferentes:  
  
-   **Región de datos Tablix** : establezca expresiones de ordenación en una región de datos de tabla, matriz o lista para controlar el criterio de ordenación de los datos en la región de datos, una vez aplicados los filtros de conjuntos de datos y de regiones de datos en tiempo de ejecución.  
  
-   **Grupo de región de datos Tablix** : establezca expresiones de ordenación para cada grupo, incluyendo el grupo de detalles, para controlar el criterio de ordenación de las instancias de grupo. Por ejemplo, para el grupo de detalles, puede controlar el orden de las filas de detalles. Para un grupo secundario, puede controlar el orden de las instancias de grupo para el grupo secundario dentro del grupo primario. De forma predeterminada, al crear un grupo, la expresión de ordenación se establece en la expresión de grupo y en orden ascendente.  
  
     Si solo tiene un grupo de detalles, puede definir una expresión de ordenación en la consulta, en la región de datos o en el grupo de detalles, obteniendo el mismo resultado.  
  
-   **Región de datos Gráfico** : establezca una expresión de ordenación para los grupos de categorías y de series con el fin de controlar el criterio de ordenación para los puntos de datos. De forma predeterminada, el orden de los puntos de datos coincide con el orden de los colores de la leyenda del gráfico. Para obtener más información, vea [Aplicar formato a los colores de serie de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md).  
  
-   **Elemento de informe de mapa** : normalmente, no necesitará ordenar los datos de una región de datos de mapa porque el mapa agrupa los datos para mostrar en elementos de mapa.  
  
-   **Región de datos Medidor** : normalmente, no es necesario ordenar los datos para una región de datos del medidor, ya que este muestra un único valor relativo a un intervalo. Si necesita ordenar los datos de un medidor, primero debe definir un grupo y, a continuación, establecer una expresión de ordenación para el grupo.  
  
#### <a name="sorting-by-a-different-value"></a>Ordenar por un valor diferente  
 Quizás prefiera ordenar las filas de una región de datos por un valor que no sea el de campo. Por ejemplo, supongamos que el campo Tamaño contiene valores de texto que se corresponden con pequeño, mediano, grande y muy grande. De forma predeterminada, la expresión de ordenación para un grupo de filas basado en Tamaño también es [Size]. Para tener más control sobre la manera en que se ordenan los datos, puede agregar un campo a la consulta de conjunto de datos que define el criterio de ordenación que desea.  
  
 O también puede definir un conjunto de datos que incluya solo los tamaños y un valor que especifique el orden que desea. Puede cambiar la expresión de ordenación para utilizar la función Lookup para el valor del criterio de ordenación.  
  
 Por ejemplo, supongamos que la siguiente consulta [!INCLUDE[tsql](../../../includes/tsql-md.md)] define un conjunto de datos denominado Sizes. La consulta utiliza una instrucción CASE para definir un valor de criterio de ordenación SizeSortOrder para cada valor de Tamaño:  
  
```  
SELECT Size,   
  CASE Size  
        WHEN 'S' THEN 1  
        WHEN 'M' THEN 2    
        WHEN 'L' THEN 3  
        WHEN 'XL' THEN 4  
        ELSE 0  
  END as SizeSortOrder  
FROM Production.Product  
```  
  
 En una tabla que tenga un grupo de filas basado en `[Size]`, podrá cambiar la expresión de ordenación de grupo para utilizar una función Lookup con el fin de buscar el campo numérico que corresponde al valor de tamaño. La expresión sería similar a:  
  
```  
=Lookup(Fields!Size.Value, Fields!Size.Value, Fields!SizeSortOrder.Value, "Sizes")  
```  
  
 Para obtener más información, vea [Ordenar datos en una región de datos &#40;Generador de informes y SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md) y [Función Lookup &#40;Generador de informes y SSRS&#41;](report-builder-functions-lookup-function.md).  
  
###  <a name="Interactive"></a> Agregar ordenación interactiva para los usuarios  
 Para permitir a los usuarios cambiar el criterio de ordenación de los datos de informe de una tabla o matriz, puede agregar botones de ordenación interactivos a encabezados de columna o encabezados de grupo. Los usuarios podrán hacer clic en el botón para alternar el criterio de ordenación. La ordenación interactiva es compatible con los formatos de representación que permiten la interacción del usuario, como HTML.  
  
 Agregue botones de ordenación interactivos a un cuadro de texto de una celda de región de datos Tablix. De forma predeterminada, cada celda de Tablix contiene un cuadro de texto. En las propiedades del cuadro de texto, debe especificar qué parte de una región de datos de tabla o de matriz desea ordenar (los valores del grupo primario, los valores del grupo secundario o las filas de detalles), la expresión por la que desea realizar la ordenación y si se debe aplicar la expresión de ordenación a otros elementos de informe que tienen una relación del mismo nivel. Por ejemplo, si una tabla y un gráfico que proporcionan vistas del mismo conjunto de datos están incluidos en un rectángulo, son regiones de datos del mismo nivel. Cuando un usuario alterna el criterio de ordenación en la tabla, también se alterna el criterio de ordenación para el gráfico. Para obtener más información, vea [Ordenación interactiva &#40;Generador de informes y SSRS&#41;](interactive-sort-report-builder-and-ssrs.md).  
  
 ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Volver al principio](#BackToTop)  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 [Mantener visibles los encabezados al desplazarse a través de un informe &#40;Generador de informes y SSRS&#41;](keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
 [Mostrar encabezados y pies de página con un grupo &#40;Generador de informes y SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [Agregar una ordenación interactiva a una tabla o una matriz &#40;Generador de informes y SSRS&#41;](add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
 [Establecer un mensaje para cuando no hay datos en una región de datos &#40;Generador de informes y SSRS&#41;](../report-data/set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [Crear un grupo de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md)  
  
 [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)  
  
 [Mostrar encabezados y pies de página con un grupo &#40;Generador de informes y SSRS&#41;](display-headers-and-footers-with-a-group-report-builder-and-ssrs.md)  
  
 [Agregar o eliminar un grupo en un gráfico &#40;Generador de informes y SSRS&#41;](add-or-delete-a-group-in-a-chart-report-builder-and-ssrs.md)  
  
 [Agregar un total a un grupo o a una región de datos Tablix &#40;Generador de informes y SSRS&#41;](add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md)  
  
##  <a name="Section"></a> En esta sección  
 [Ejemplos de expresión de grupo &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
 [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)  
  
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)  
  
##  <a name="Related"></a> Secciones relacionadas  
 [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](understanding-groups-report-builder-and-ssrs.md)  
  
 [Crear grupos de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)  
  
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
 [Referencias a las colecciones de variables de informe y de grupo &#40;Generador de informes y SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md)  
  
 [Mostrar una serie con varios rangos de datos en un gráfico &#40;Generador de informes y SSRS&#41;](displaying-a-series-with-multiple-data-ranges-on-a-chart.md)  
  
 [Vincular varias regiones de datos al mismo conjunto de datos &#40;Generador de informes y SSRS&#41;](linking-multiple-data-regions-to-the-same-dataset-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vea también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Mapas &#40;Generador de informes y SSRS&#41;](maps-report-builder-and-ssrs.md)   
 [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [Medidores &#40;Generador de informes y SSRS&#41;](gauges-report-builder-and-ssrs.md)   
 [Indicadores &#40;Generador de informes y SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  
