---
title: "Resaltar datos en el gráfico agregando franjas (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
ms.assetid: addd6137-4b6e-4e88-a7e8-9600fcd1ccce
caps.latest.revision: "6"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 289fe71637b7930889e3980b65bea89c2dd98447
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="highlight-chart-data-by-adding-strip-lines-report-builder-and-ssrs"></a>Resaltar datos en el gráfico agregando franjas (Generador de informes y SSRS)
  Las franjas son intervalos horizontales o verticales que sombrean el fondo del gráfico a intervalos regulares o personalizados. Puede usar las franjas para:  
  
-   Mejorar la legibilidad y facilitar la búsqueda de valores individuales en el gráfico. Especifique franjas a intervalos regulares para ayudar a separar los puntos de datos durante la lectura del gráfico.  
  
-   Resaltar fechas que tienen lugar a intervalos regulares. Por ejemplo, en un informe de ventas puede usar franjas para identificar los puntos de datos correspondientes a los fines de semana.  
  
-   Resaltar un intervalo con clave concreto. Siguiendo con el ejemplo anterior, podría usar una franja para resaltar el intervalo de ventas más alto, comprendido entre 80 y 100 dólares.  
  
 Las franjas no se pueden aplicar a los gráficos de formas ni a los gráficos polares.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-interlaced-strip-lines-at-regular-intervals-on-a-chart"></a>Mostrar en un gráfico franjas entrelazadas a intervalos regulares  
  
1.  Para mostrar las franjas horizontales, haga clic con el botón derecho en el eje del gráfico vertical y haga clic en **Propiedades del eje vertical**.  
  
     Para mostrar las franjas verticales, haga clic con el botón derecho en el eje del gráfico horizontal y haga clic en **Propiedades del eje horizontal**.  
  
2.  Seleccione la opción **Usar entrelazado** . En el gráfico aparecerán franjas de color gris.  
  
3.  (Opcional) Especifique un color para las franjas; para ello, use la lista desplegable **Color** .  
  
### <a name="to-display-interlaced-strip-lines-at-custom-intervals-on-a-chart"></a>Mostrar en un gráfico franjas entrelazadas a intervalos personalizados  
  
1.  Para mostrar las franjas horizontales, haga clic con el botón derecho en el eje del gráfico vertical y haga clic en **Propiedades del eje vertical**.  
  
     Para mostrar las franjas verticales, haga clic con el botón derecho en el eje del gráfico horizontal y haga clic en **Propiedades del eje horizontal**.  
  
     En la ventana de propiedades se muestran las propiedades del eje.  
  
2.  En la sección **Apariencia** del panel de propiedades, para la propiedad StripLines, haga clic en el botón para editar colecciones (…) con el objeto de abrir el **Editor de la colección ChartStripLine**.  
  
3.  Haga clic en **Agregar** para agregar una nueva franja a la colección.  
  
4.  Haga clic en StripWidth para especificar el ancho de la franja, que se mide en pulgadas en el informe. Si está resaltando fechas u horas, haga clic en StripWidthType y seleccione un intervalo de tiempo.  
  
5.  Escriba un valor o una expresión para Interval para especificar la frecuencia de repetición de la franja.  Por ejemplo, si especifica un intervalo de 10, y el ancho de la franja es 5, las franjas se mostrarán en los valores 0 a 5, 15 a 20, 30 a 35, y así sucesivamente.  
  
> [!NOTE]  
>  De forma predeterminada, Interval está establecido en automático, lo que significa que el gráfico no calculará un intervalo para las franjas personalizadas. El gráfico solamente calcula los intervalos para las franjas si se establece un valor de intervalo.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Agregar una media móvil a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)  
  
  
