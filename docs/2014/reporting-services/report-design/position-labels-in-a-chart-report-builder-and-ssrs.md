---
title: Colocar etiquetas en un gráfico (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5db74e0b-8be8-4b47-b386-faab56dffa9b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fc04d47058c1ef1bc3929d941a6680eb013fcc53
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66105438"
---
# <a name="position-labels-in-a-chart-report-builder-and-ssrs"></a>Colocar etiquetas en un gráfico (Generador de informes y SSRS)
  Dado que cada tipo de gráfico tiene una forma diferente, las etiquetas de punto de datos se colocan en una ubicación óptima para no interferir en el gráfico. La posición predeterminada de las etiquetas depende del tipo de gráfico:  
  
-   En los gráficos apilados, las etiquetas solo se pueden colocar dentro de la serie.  
  
-   En los gráficos de embudo o piramidales, las etiquetas se colocan fuera de una columna.  
  
-   En los gráficos circulares, las etiquetas se colocan dentro de los sectores.  
  
-   En los gráficos de barras, las etiquetas se colocan fuera de las barras que representan los puntos de datos.  
  
-   En los gráficos polares, las etiquetas se colocan fuera del área circular que representa los puntos de datos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-position-of-point-labels-in-a-pie-chart"></a>Para cambiar la posición de las etiquetas de punto de datos de un gráfico circular  
  
1.  Cree un gráfico circular.  
  
2.  En la superficie de diseño, haga clic con el botón derecho en el gráfico y seleccione **Mostrar etiquetas de datos**.  
  
3.  Abra el panel de propiedades. En la pestaña **Ver** , haga clic en **Propiedades**.  
  
4.  En la superficie de diseño, haga clic en el gráfico. Las propiedades del gráfico se muestran en el panel de propiedades.  
  
5.  En la sección **General** , expanda el nodo **CustomAttributes** . Se muestra una lista de atributos para el gráfico circular.  
  
6.  Seleccione un valor para la propiedad PieLabelStyle.  
  
### <a name="to-change-the-position-of-point-labels-in-a-funnel-or-pyramid-chart"></a>Para cambiar la posición de las etiquetas de punto de datos en un gráfico de embudo o piramidal  
  
1.  Cree un gráfico de embudo o piramidal.  
  
2.  En la superficie de diseño, haga clic con el botón derecho en el gráfico y seleccione **Mostrar etiquetas de datos**.  
  
3.  Abra el panel de propiedades. En la pestaña **Ver** , haga clic en **Propiedades**.  
  
4.  En la superficie de diseño, haga clic en el gráfico. Las propiedades del gráfico se muestran en el panel de propiedades.  
  
5.  En la sección **General** , expanda el nodo **CustomAttributes** . Se muestra una lista de atributos para el gráfico de embudo.  
  
6.  Si se trata de un gráfico de embudo, seleccione un valor para la propiedad FunnelLabelStyle. Si se trata de un gráfico piramidal, seleccione un valor para la propiedad PyramidLabelStyle.  
  
    > [!NOTE]  
    >  Cuando esta propiedad se establece en un valor `OutsideInColumn`, las etiquetas se representan en una columna vertical. No hay ninguna manera de cambiar la posición de la columna.  
  
### <a name="to-change-the-position-of-point-labels-in-a-bar-chart"></a>Para cambiar la posición de las etiquetas de punto de datos de un gráfico de barras  
  
1.  Cree un gráfico de barras.  
  
2.  En la superficie de diseño, haga clic con el botón derecho en el gráfico y seleccione **Mostrar etiquetas de datos**.  
  
3.  Abra el panel de propiedades. En la pestaña **Ver** , haga clic en **Propiedades**.  
  
4.  En la superficie de diseño, haga clic en el gráfico. Las propiedades del gráfico se muestran en el panel de propiedades.  
  
5.  En la sección **General** , expanda el nodo **CustomAttributes** . Se muestra una lista de atributos para el gráfico de barras.  
  
6.  Seleccione un valor para la propiedad BarLabelStyle.  
  
 Si el estilo de la etiqueta de la barra se establece en `Outside`, la etiqueta se colocará fuera de la barra, siempre y cuando quepa en el área del gráfico. Si la etiqueta no se puede colocar fuera de la barra, pero sí dentro del área del gráfico, la etiqueta se situará dentro de la barra en la posición más próxima al extremo de la misma.  
  
### <a name="to-change-the-position-of-point-labels-in-an-area-column-line-or-scatter-chart"></a>Para cambiar la posición de las etiquetas de punto de datos en una gráfico de áreas, de columnas, de líneas o de dispersión  
  
1.  Cree un gráfico de áreas, de columnas, de líneas o de dispersión.  
  
2.  En la superficie de diseño, haga clic con el botón derecho en el gráfico y seleccione **Mostrar etiquetas de datos**.  
  
3.  Abra el panel de propiedades. En la pestaña **Ver** , haga clic en **Propiedades**.  
  
4.  En la superficie de diseño, haga clic en la serie. Las propiedades de la serie se muestran en el panel de propiedades.  
  
5.  En la sección **Datos** , expanda el nodo **DataPoint** y, a continuación, expanda el nodo **Etiqueta**.  
  
6.  Seleccione un valor para la propiedad Position.  
  
## <a name="see-also"></a>Vea también  
 [Gráficos circulares &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Gráficos de barras &#40;Generador de informes y SSRS&#41;](bar-charts-report-builder-and-ssrs.md)   
 [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Aplicar formato de fecha o de moneda a las etiquetas de los ejes &#40;Generador de informes y SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Mostrar las etiquetas de los puntos de datos fuera de un gráfico circular &#40;Generador de informes y SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Aplicar formato a los puntos de datos de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
  
  
