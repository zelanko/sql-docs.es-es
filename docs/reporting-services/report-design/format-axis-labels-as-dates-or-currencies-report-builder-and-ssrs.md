---
title: Aplicar formato de fecha o de moneda a las etiquetas de los ejes (Generador de informes y SSRS)| Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: e9a01a74-2f51-4b35-be3a-a6138568f6cf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 23232d80433584635ce9bc751893366d76b29a41
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56285863"
---
# <a name="format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs"></a>Aplicar formato de fecha o de moneda a las etiquetas de los ejes (Generador de informes y SSRS)
Cuando se muestren valores DateTime con el formato correcto en un eje de un informe paginado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , un gráfico mostrará automáticamente dichos valores como días. Para especificar un intervalo de fechas u horas para el eje X, como un intervalo de meses o de horas, debe dar formato a las etiquetas del eje y establecer el tipo de intervalo de éste en un intervalo de fechas u horas válido.  
  
> [!NOTE]  
>  En gráficos de columnas y de dispersión, el eje horizontal, o eje X, es el eje de categorías. En los gráficos de barras, el vertical, o eje Y, es el eje de categoría.  
  
 Para dar el formato correcto a los intervalos de tiempo, los valores mostrados en el eje X se deben evaluar como un tipo de datos <xref:System.DateTime> . Si el campo tiene un tipo de datos <xref:System.String>, el gráfico no calculará los intervalos como fechas u horas. Para más información, vea [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md).  
  
 Cuando se agrega un valor numérico al eje Y, de forma predeterminada, el gráfico no da formato al número antes de mostrarlo. Si el campo numérico es una cifra de ventas, considere la posibilidad de dar formato de moneda a los números para aumentar la legibilidad del gráfico.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-format-x-axis-labels-as-monthly-intervals"></a>Para dar formato de intervalo mensual a las etiquetas del eje X  
  
1.  Haga clic con el botón derecho en el eje horizontal, o X, del gráfico y, después, seleccione **Propiedades del eje horizontal**.  
  
2.  En el cuadro de diálogo **Propiedades del eje horizontal** , seleccione **Número**.  
  
3.  En la lista **Categoría** , seleccione **Fecha**. En la lista **Tipo** , seleccione un formato de fecha para aplicarlo a las etiquetas del eje X.  
  
4.  Seleccione **Opciones del eje**.  
  
5.  En **Intervalo**, escriba **1**. En la propiedad **Tipo de intervalo** , seleccione **Meses**.  
  
    > [!NOTE]  
    >  Si no especifica un tipo de intervalo, el gráfico calculará los intervalos en días.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-format-y-axis-labels-using-a-currency-format"></a>Para dar formato de moneda a las etiquetas del eje Y  
  
1.  Haga clic con el botón derecho en el eje vertical, o Y, del gráfico y, después, haga clic en **Propiedades del eje vertical**.  
  
2.  En el cuadro de diálogo **Propiedades del eje vertical** , seleccione **Número**.  
  
3.  En la lista **Categoría** , seleccione **Moneda**. En la lista **Símbolo** , seleccione un formato de moneda para aplicarlo a las etiquetas del eje Y.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Especificar una escala logarítmica &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/specify-a-logarithmic-scale-report-builder-and-ssrs.md)   
 [Especificar un intervalo de eje &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  
