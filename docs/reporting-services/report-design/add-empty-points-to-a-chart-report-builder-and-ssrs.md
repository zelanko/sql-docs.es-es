---
title: "Agregar puntos vacíos a un gráfico (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b056119-439f-494f-83cf-ee0c05dc6487
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: acc67d54c387097785317456b70a5936abf05d43
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="add-empty-points-to-a-chart-report-builder-and-ssrs"></a>Add Empty Points to a Chart (Report Builder and SSRS)
Los valores NULL se muestran en el gráfico como espacios vacíos o como intervalos entre los puntos de datos de una serie. En los informes paginados de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , los puntos vacíos son los puntos de datos que se pueden insertar en el espacio vacío que crean los valores NULL.  
  
 De forma predeterminada, los puntos vacíos se calculan tomando el promedio de los puntos de datos anterior y siguiente que contienen un valor. Puede cambiar esta circunstancia para que todos los puntos vacíos se inserten en la posición cero.  
  
 Para más información, vea [Puntos de datos vacíos y nulos en los gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/empty-and-null-data-points-in-charts-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-specify-empty-points-on-a-chart"></a>Para especificar puntos vacíos en un gráfico  
  
1.  Abra el panel de propiedades.  
  
2.  En la superficie de diseño, haga clic con el botón secundario en la serie que contiene los valores NULL. Las propiedades de la serie se muestran en el panel de propiedades.  
  
3.  Expanda el nodo **EmptyPoint** .  
  
4.  Seleccione un valor de color para la propiedad Color.  
  
5.  En el nodo **EmptyPoint** , expanda el nodo Marcador.  
  
6.  Seleccione un tipo de marcador para la propiedad MarkerType.  
  
    > [!NOTE]  
    >  Deberá seleccionar un tipo de marcador siempre que desee agregar puntos vacíos a un gráfico de barras, de columnas o de dispersión. Sin embargo, para los gráficos de áreas, de líneas y radiales, la selección de un tipo de marcador es opcional porque el gráfico rellena el espacio vacío sin que sea necesario especificar un marcador.  
  
7.  Establezca el valor del punto vacío.  
  
    1.  En el panel de propiedades, expanda el nodo **CustomAttributes** .  
  
    2.  Establezca la propiedad EmptyPointValue. Para insertar puntos vacíos en el promedio de los puntos de datos anterior y siguiente, seleccione **Promedio**. Para insertar puntos vacíos en la posición cero, seleccione **Cero**.  
  
## <a name="see-also"></a>Vea también  
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Tipos de gráfico &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/chart-types-report-builder-and-ssrs.md)   
 [Agregar quiebres de escala a un gráfico de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/add-scale-breaks-to-a-chart-report-builder-and-ssrs.md)   
 [Gráficos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
