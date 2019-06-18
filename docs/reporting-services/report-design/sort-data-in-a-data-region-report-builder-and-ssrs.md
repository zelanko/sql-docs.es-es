---
title: Ordenar datos en una región de datos (Generador de informes y SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 2fcb9be2-1daa-4c92-ad00-5f63cdf39f70
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6ad5600def990457834d858b61ba3bad4a241158
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570743"
---
# <a name="sort-data-in-a-data-region-report-builder-and-ssrs"></a>Ordenar datos en una región de datos (Generador de informes y SSRS)
  Para cambiar el criterio de ordenación de los datos de una región de datos cuando se ejecuta un informe por primera vez, es necesario establecer la expresión de ordenación en la región de datos o el grupo. De forma predeterminada, la expresión de ordenación de un grupo se establece automáticamente en el mismo valor que la expresión de grupo.  
  
-   En una región de datos Tablix, establezca la expresión de ordenación para la región de datos o para cada grupo, incluido el grupo de detalles. Si solo tiene un grupo de detalles en una región de datos Tablix, puede definir una expresión de ordenación en la consulta, en la región de datos o en el grupo de detalles con el mismo resultado.  
  
-   En una región de datos de gráfico, establezca la expresión de ordenación para los grupos de categorías y de series para controlar el criterio de ordenación para cada grupo. El orden de los colores en una leyenda de gráfico está determinado por la expresión de ordenación para los puntos de datos del grupo de categorías.  
  
-   Normalmente, en una región de datos de medidor, no es necesario ordenar los datos, ya que el medidor muestra un único valor relativo a un intervalo. Si necesita ordenar los datos de un medidor, primero debe definir un grupo y, a continuación, establecer la expresión de ordenación para el grupo.  
  
 Para obtener más información, vea [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
 En una región de datos Tablix, también puede agregar un botón de ordenación interactiva a la parte superior de un encabezado de columna para permitir a los usuarios cambiar el criterio de ordenación de los grupos o las filas de detalles. Para obtener más información, vea [Ordenación interactiva &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/interactive-sort-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-sort-data-in-a-tablix-data-region"></a>Para ordenar los datos de una región de datos Tablix  
  
1.  En la superficie de diseño, haga clic con el botón derecho en un identificador de fila y, después, haga clic en **Propiedades de Tablix**.  
  
2.  Haga clic en **Ordenar**.  
  
3.  Para cada expresión de ordenación, siga estos pasos:  
  
    1.  Haga clic en **Agregar**.  
  
    2.  Escriba o seleccione la expresión por la que desea ordenar los datos.  
  
    3.  En la lista desplegable de la columna **Ordenar** , elija el sentido de la ordenación para cada expresión. **A-Z** ordena la expresión en orden ascendente. **Z-A** ordena la expresión en orden descendente.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-values-in-a-group-including-the-details-group-for-a-tablix"></a>Para ordenar los valores de un grupo, incluido el grupo de detalles, para un Tablix  
  
1.  En la superficie de diseño, haga clic en la región de datos Tablix para seleccionarla. El panel Agrupación muestra los grupos de filas y de columnas para la región de datos Tablix.  
  
2.  En el panel Grupos de filas, haga clic con el botón derecho en el nombre del grupo y, después, haga clic en **Editar grupo**.  
  
3.  En el cuadro de diálogo **Grupo de Tablix** , haga clic en **Ordenar**.  
  
4.  Para cada expresión de ordenación, siga estos pasos:  
  
    1.  Haga clic en **Agregar**.  
  
    2.  Escriba o seleccione la expresión por la que desea ordenar los datos.  
  
    3.  En la lista desplegable de la columna **Ordenar** , elija el sentido de la ordenación para cada expresión. **A-Z** ordena la expresión en orden ascendente. **Z-A** ordena la expresión en orden descendente.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-x-axis-labels-in-alphabetical-order-on-a-chart"></a>Para ordenar las etiquetas del eje X en orden alfabético en un gráfico  
  
1.  Haga clic con el botón derecho en la zona de colocación de campos de categorías y, después, haga clic en **Propiedades del grupo de categorías**.  
  
2.  En el cuadro de diálogo **Propiedades del grupo de categorías** , haga clic en **Ordenar**.  
  
3.  Para cada expresión de ordenación, siga estos pasos:  
  
    1.  Haga clic en **Agregar**.  
  
    2.  Seleccione la expresión que coincide con el campo de agrupación. Puede comprobar la expresión para el campo de agrupación haciendo clic en **Agrupación**.  
  
    3.  En la lista desplegable de la columna **Ordenar** , elija el sentido de la ordenación para cada expresión. **A-Z** ordena la expresión en orden alfabético ascendente. **Z-A** ordena la expresión en orden alfabético descendente.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-the-data-points-in-ascending-or-descending-order-on-a-chart"></a>Para ordenar los puntos de datos de forma ascendente o descendente en un gráfico  
  
1.  Haga clic con el botón derecho en la zona de colocación de campos de categorías y, después, haga clic en **Propiedades del grupo de categorías**.  
  
2.  En el cuadro de diálogo **Propiedades del grupo de categorías** , haga clic en **Ordenar**.  
  
3.  Para cada expresión de ordenación, siga estos pasos:  
  
    1.  Haga clic en **Agregar**.  
  
    2.  Seleccione la expresión que coincide con el campo de datos. En la mayoría de los casos, es un valor agregado, como `=Sum(Fields!Quantity.Value)`.  
  
    3.  En la lista desplegable de la columna **Ordenar** , elija el sentido de la ordenación para cada expresión. **A-Z** ordena la expresión en orden ascendente. **Z-A** ordena la expresión en orden descendente.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-sort-data-in-ascending-or-descending-order-for-display-on-a-gauge"></a>Para ordenar los datos de forma ascendente o descendente para su presentación en un medidor  
  
1.  Haga clic con el botón derecho en el medidor y, después, haga clic en **Agregar grupo de datos**.  
  
2.  En el cuadro de diálogo **Propiedades de grupo del panel de medidores** , haga clic en **General** si es necesario.  
  
3.  En **Expresiones de grupo**, haga clic en **Agregar**.  
  
4.  En **Agrupar por**, escriba o seleccione la expresión por la que se agruparán los datos.  
  
5.  Repita los pasos 3 y 4 hasta que haya agregado todas las expresiones de grupo que desee usar.  
  
6.  Haga clic en **Ordenar**.  
  
7.  Para cada expresión de ordenación, siga estos pasos:  
  
    1.  Haga clic en **Agregar**.  
  
    2.  Seleccione la expresión que coincide con el campo de agrupación. Puede comprobar la expresión para el campo de agrupación haciendo clic en **Agrupación**.  
  
    3.  En la lista desplegable de la columna **Ordenar** , elija el sentido de la ordenación para cada expresión. **A-Z** ordena la expresión en orden ascendente. **Z-A** ordena la expresión en orden descendente.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Para más información sobre cómo se agrupan los datos en un medidor, vea [Medidores &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Especificar colores coherentes en varios gráficos de formas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/specify-consistent-colors-across-multiple-shape-charts-report-builder-and-ssrs.md)  
  
  
