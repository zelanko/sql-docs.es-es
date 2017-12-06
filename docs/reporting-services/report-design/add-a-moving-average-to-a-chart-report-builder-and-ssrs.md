---
title: "Agregar una media móvil a un gráfico (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 166cf9c1-0750-4866-8381-542e4fbfe65a
caps.latest.revision: "13"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ca0481acd68e544f999440c54eef04eb933504d0
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="add-a-moving-average-to-a-chart-report-builder-and-ssrs"></a>Agregar una media móvil a un gráfico (Generador de informes y SSRS)
Una media móvil es una media de los datos de la serie, calculada en un período de tiempo definido. En los informes paginados de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , la media móvil se puede mostrar en el gráfico para identificar tendencias significativas.  

![report-builder-column-chart-tutorial](../../reporting-services/media/report-builder-column-chart-tutorial.png)
  
 La fórmula de la media móvil es el indicador de precio más habitual en los análisis técnicos. También se pueden derivar de una serie del gráfico muchas otras fórmulas, como el promedio, la mediana y la desviación estándar. Al especificar una media móvil, cada fórmula puede tener uno o varios parámetros que deberá especificar.  
 
 En [Tutorial: agregar un gráfico de columnas a un informe (Generador de informes)](Tutorial:%20Add%20a%20Column%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md) se explica cómo agregar una media móvil a un gráfico, en el caso de que quiera probarlo con datos de ejemplo.
  
 Cuando se agrega una fórmula de media móvil en modo de diseño, la serie de líneas que se agrega es solo un marcador de posición visual. El gráfico calculará los puntos de datos de cada fórmula durante el procesamiento del informe.  
  
 En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], no está disponible la compatibilidad integrada para las líneas de tendencia.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-calculated-moving-average-to-a-series-on-the-chart"></a>Para agregar una media móvil calculada a una serie del gráfico  
  
1.  Haga clic con el botón secundario en el área **Valores** y, a continuación, haga clic en **Agregar serie calculada**. Se abre el cuadro de diálogo **Propiedades de la serie calculada** .  
  
2.  Seleccione la opción **Media móvil** en la lista desplegable **Fórmula** .  
  
3.  Especifique un valor entero para el **Período** que representa el período de la media móvil.  
  
    > [!NOTE]  
    >  El período es el número de días usado para calcular una media móvil. Si en el eje X no se especifican valores de fecha y hora, el período de tiempo lo representa el número de puntos de datos usados para calcular una media móvil. Si solo hay un punto de datos, la fórmula de la media móvil no se calcula. La media móvil se calcula a partir del segundo punto. Si especifica la opción **Empezar desde el primer punto** , el gráfico iniciará la media móvil en el primer punto. Si solo hay un punto de datos, el punto de la media móvil calculada será idéntico al primer punto de la serie original.  
  
## <a name="see-also"></a>Vea también  
* [Tutorial: agregar un gráfico de columnas a un informe (Generador de informes)](Tutorial:%20Add%20a%20Column%20Chart%20to%20Your%20Report%20\(Report%20Builder\).md)
*  [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
*  [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
*  [Agregar puntos vacíos al gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)  
  
  
