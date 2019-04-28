---
title: Especificar un intervalo de eje (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ae46712d-a5bf-44c0-9929-e30ccc1e7e33
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 46984681329be6e236cac6271d3768705a26dd7b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62720283"
---
# <a name="specify-an-axis-interval-report-builder-and-ssrs"></a>Especificar un intervalo de eje (Generador de informes y SSRS)
  El intervalo de eje define el número de etiquetas y marcas de graduación asociadas que aparecen en un eje. En el eje de valores, los intervalos de eje proporcionan una medida coherente de los puntos de datos representados en el gráfico. Sin embargo, en el eje de categorías, esta funcionalidad puede provocar que las categorías aparezcan sin etiquetas en los ejes. Puede especificar el número de intervalos que quiere en la propiedad Intervalo del eje. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] calcula el número de intervalos en tiempo de ejecución, según los datos del conjunto de resultados. Para más información sobre cómo se calculan los intervalos de los ejes, vea [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
 Este tema no se aplica a los valores de fecha u hora del eje de categorías. De forma predeterminada, los valores de tipo `DateTime` aparecen como días. Para especificar otro intervalo de fechas u horas, como un mes o un intervalo de horas, debe dar formato a las etiquetas del eje y establecer este para que muestre instancias de los tipos `DateTime` y no de los tipos `String`. Además, necesita establecer la propiedad Intervalo. Para más información, vea [Aplicar formato de fecha o de moneda a las etiquetas de los ejes &#40;Generador de informes y SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md).  
  
 Este tema no se aplica a los gráficos circulares, de anillo, de embudo ni piramidales, ya que carecen de ejes.  
  
> [!NOTE]  
>  El eje de categorías normalmente es el eje horizontal o eje X. Sin embargo, en el caso de los gráficos de barras, el eje de categorías es el eje vertical o eje Y.  
  
 Un ejemplo de gráfico que especifica intervalos de eje diferentes está disponible como informe de ejemplo. Para obtener más información acerca de cómo descargar este y otros informes de ejemplo, consulte el tema sobre [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][informes de ejemplo del Generador de informes y el Diseñador de informes](https://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-show-all-category-labels-on-the-x-axis"></a>Para mostrar todas las etiquetas de categoría en el eje X  
  
1.  Haga clic con el botón secundario en el eje de categorías y, a continuación, haga clic en **Propiedades del eje**. Se abre el cuadro de diálogo **Propiedades del eje** .  
  
2.  En **opciones del eje**, establezca `Interval` a **1**. Se mostrarán todas las etiquetas de grupo de categorías. Si desea mostrar una de cada dos etiquetas de grupo de categorías en el eje X, escriba **2**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Cuando se establece un intervalo de eje, se deshabilita todo el etiquetado automático. Si especifica un valor para el intervalo de eje, puede notar un comportamiento imprevisible del etiquetado en función del número de categorías existentes en el eje de categorías.  
  
### <a name="to-enable-a-variable-interval-calculation-on-an-axis"></a>Para habilitar el cálculo de un intervalo variable en un eje  
  
1.  Haga clic con el botón secundario en el eje del gráfico que desea cambiar y, a continuación, haga clic en **Propiedades del eje**. Se abre el cuadro de diálogo **Propiedades del eje** .  
  
2.  En **opciones del eje**, establezca `Interval` a **automática**. El gráfico mostrará el número óptimo de etiquetas de categoría que quepan a lo largo del eje.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Aplicar formato a los puntos de datos de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Ordenar datos en una región de datos &#40;Generador de informes y SSRS&#41;](sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Cuadro de diálogo Propiedades del eje, Opciones del eje &#40;Generador de informes y SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [Especificar una escala logarítmica &#40;Generador de informes y SSRS&#41;](specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [Trazar datos en un eje secundario &#40;Generador de informes y SSRS&#41;](plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)  
  
  
