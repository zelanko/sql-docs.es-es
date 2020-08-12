---
title: Adición de datos a una región de datos Tablix (Generador de informes) | Microsoft Docs
description: Obtenga información sobre cómo mostrar datos detallados o agrupados, desde un conjunto de datos de informe en una tabla o matriz, en una región de datos Tablix.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 8f1d0a76-afed-480f-98fb-89e2d4eb09b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 27e16e327855ccc2e7092787cefc95f275a1b2b4
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689702"
---
# <a name="adding-data-to-a-tablix-data-region-report-builder-and-ssrs"></a>Agregar datos a una región de datos Tablix (Generador de informes y SSRS)
Para mostrar los datos de un conjunto de datos de informe en una tabla o una matriz en informes paginados de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , especifique en cada celda de datos el nombre del campo de conjunto de datos que se debe mostrar. Puede mostrar datos detallados o datos agrupados. Si agrega grupos a una tabla o matriz, las filas y las columnas para los valores y los datos de grupo se agregan automáticamente. A continuación, puede agregar subtotales y totales para los datos.  
  
 Todos los datos de una región de datos pertenecen al menos a un grupo. Los datos detallados forman parte del grupo de detalles. Para obtener más información sobre los datos detallados y los datos agrupados, vea [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="adding-detail-data"></a>Agregar datos detallados  
 Los datos detallados son todos los datos de un conjunto de datos de informe una vez aplicados los filtros al conjunto de datos, la región de datos y el grupo de detalles. Todos los datos detallados mostrados en una única región de datos Tablix deben proceder del mismo conjunto de datos de informe.  
  
 Para agregar datos detallados de un conjunto de datos de informe a una región de datos Tablix, arrastre un campo de conjunto de datos desde el panel Datos de informe hasta la celda correspondiente en la fila de detalle. Para las celdas existentes en una región de datos Tablix, es posible agregar o modificar una expresión de campo de conjunto de datos usando el selector de campo en cada celda o arrastrando un campo desde el panel Datos de informe hasta la celda. Para crear columnas adicionales, puede arrastrar el campo desde el panel Datos de informe e insertarlo en una región de datos Tablix existente.  
  
 De forma predeterminada, en tiempo de ejecución, una celda de la fila de detalles muestra datos detallados y una celda de la fila de grupo muestra un valor agregado. Para obtener más información sobre las filas y las columnas de Tablix, vea [Celdas, filas y columnas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Las plantillas de tabla y de lista proporcionan una fila de detalles. Las plantillas de matriz carecen de fila de detalles. Si la región de datos Tablix no tiene ninguna fila de detalles, puede agregar una definiendo un grupo de detalles. Para obtener más información, vea [Agregar un grupo de detalles &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-details-group-report-builder-and-ssrs.md).  
  
## <a name="adding-grouped-data"></a>Agregar datos agrupados  
 Los datos agrupados son todos los datos detallados especificados por una expresión de grupo una vez aplicados los filtros al conjunto de datos, la región de datos y el grupo. Para organizar los datos detallados en grupos, arrastre los campos desde el panel Datos de informe hasta el panel Agrupación. Al agregar un grupo, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] agrega automáticamente las filas o columnas relacionadas a la región de datos Tablix en la que se van a mostrar los datos agrupados. Las celdas de estas filas o columnas están asociadas a datos agrupados. Para más información, vea [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md).  
  
 De forma predeterminada, al agregar un campo de conjunto de datos que representa datos numéricos a una celda de una fila o columna de grupo, el valor de la celda es la suma de los datos agrupados cuyo ámbito incluye la pertenencia a los grupos de columna y de fila más interiores para dicha celda. Puede cambiar la función de agregado predeterminada Sum por cualquier otra función de agregado, como Avg o Count. También puede cambiar el ámbito predeterminado para un cálculo agregado, por ejemplo, para calcular el porcentaje con el que un valor contribuye a un grupo de filas. Para obtener más información, vea [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)subyacente.  
  
 De forma predeterminada, todos los datos agrupados proceden del mismo conjunto de datos de informe. En una región de datos Tablix, puede incluir valores agregados de otro conjunto de datos especificando el nombre de éste como un ámbito. También es posible especificar varios valores agregados de varios conjuntos de datos dentro de una única región de datos Tablix. Para más información, vea [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="adding-subtotals-and-totals"></a>Agregar subtotales y totales  
 Para agregar subtotales a un grupo y totales generales a la región de datos, use la característica Agregar total del menú contextual de una celda o del panel Agrupación. Las filas y las columnas en las que se van a mostrar los totales se agregan automáticamente. De forma predeterminada, las expresiones de subtotal y de total usan la función de agregado [Sum](../../reporting-services/report-design/report-builder-functions-sum-function.md) . Una vez agregada la expresión, puede cambiar la función predeterminada. Para obtener más información, vea [Agregar un total a un grupo o a una región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-total-to-a-group-or-tablix-data-region-report-builder-and-ssrs.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="adding-labels"></a>Agregar etiquetas  
 Para agregar etiquetas a un grupo o una región de datos, agregue una fila o columna fuera del grupo que desea etiquetar. Las filas y columnas de etiqueta son similares a las filas y columnas que se agregan para mostrar los totales. Para obtener más información, vea [Insertar o eliminar una fila &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-row-report-builder-and-ssrs.md) o [Insertar o eliminar una columna &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
## <a name="adding-an-existing-tablix-data-region-from-another-report"></a>Agregar una región de datos Tablix existente de otro informe  
 Puede copiar una región de datos de otro informe y pegarla en un informe nuevo o en uno ya existente. Tras pegar la región de datos, debe asegurarse de que el conjunto de datos que usa la región de datos esté definido, y de que los campos de conjunto de datos tengan nombres y tipos de datos idénticos a los del informe original. No puede copiar los conjuntos de datos de un informe en otro, pero si los informes utilizan orígenes de datos compartidos, puede duplicar rápidamente el conjunto de datos en el otro el informe. También puede importar el texto de consulta correspondiente a las consultas que recuperan los datos del conjunto de datos, lo que simplifica la duplicación de las consultas en los informes. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Ordenación interactiva, mapas de documento y vínculos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Agregar, editar y actualizar campos en el panel Datos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)   
 [Agregar una expresión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)  
  
  
