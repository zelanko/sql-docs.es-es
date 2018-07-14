---
title: Mostrar las etiquetas de los puntos de datos fuera de un gráfico circular (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 959b7574-cf43-470b-b592-4944d8a9948f
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 759f9ff43075f5285fba0c3799577855c5e8f20d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208487"
---
# <a name="display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs"></a>Mostrar las etiquetas de los puntos de datos fuera de un gráfico circular (Generador de informes y SSRS)
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], el etiquetado de los gráficos circulares está optimizado, por lo que las etiquetas se muestran solo en varios segmentos de datos. Si el gráfico circular contiene demasiados segmentos, las etiquetas se pueden superponer. Una solución consiste en mostrar las etiquetas fuera del gráfico circular, lo que puede crear más espacio para las etiquetas de datos más largas. Si las etiquetas siguen solapándose, habilite 3D para crear más espacio. Esto reduce el diámetro del gráfico circular, lo que crea más espacio alrededor del gráfico.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-display-data-point-labels-inside-a-pie-chart"></a>Para mostrar las etiquetas de los puntos de datos dentro de un gráfico circular  
  
1.  Agregue un gráfico circular al informe. Para más información, vea [Agregar un gráfico a un informe &#40;Generador de informes y SSRS&#41;](add-a-chart-to-a-report-report-builder-and-ssrs.md).  
  
2.  En la superficie de diseño, haga clic con el botón derecho en el gráfico y seleccione **Mostrar etiquetas de datos**.  
  
### <a name="to-display-data-point-labels-outside-a-pie-chart"></a>Para mostrar las etiquetas de los puntos de datos fuera de un gráfico circular  
  
1.  Cree un gráfico circular y muestre las etiquetas de datos.  
  
2.  Abra el panel de propiedades.  
  
3.  En la superficie de diseño, haga clic en el propio gráfico para mostrar las propiedades **Category** en el panel de propiedades.  
  
4.  Expanda el nodo **CustomAttributes** . Se muestra una lista de atributos para el gráfico circular.  
  
5.  Establezca la propiedad **PieLabelStyle** en **Externa**.  
  
6.  Establecer el `PieLineColor` propiedad **negro**. La propiedad PieLineColor define las líneas de llamada para cada etiqueta de punto de datos.  
  
### <a name="to-prevent-overlapping-labels-displayed-outside-a-pie-chart"></a>Para evitar que las etiquetas mostradas fuera de un gráfico circular se superpongan  
  
1.  Cree un gráfico circular con etiquetas externas.  
  
2.  En la superficie de diseño, haga clic con el botón derecho fuera del gráfico circular pero dentro de los límites del gráfico y seleccione **Propiedades del área de gráfico**. Aparecerá el cuadro de diálogo **Propiedades del área de gráfico** .  
  
3.  En la pestaña **Opciones 3D** , seleccione **Habilitar 3D**.  
  
4.  Si quiere que el gráfico tenga más espacio para las etiquetas, pero que siga pareciendo bidimensional, establezca las propiedades **Rotation** e **Inclination** en **0**.  
  
## <a name="see-also"></a>Vea también  
 [Los gráficos circulares &#40;generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Recopilar segmentos pequeños en un gráfico circular &#40;Generador de informes y SSRS&#41;](collect-small-slices-on-a-pie-chart-report-builder-and-ssrs.md)   
 [Mostrar valores de porcentaje en un gráfico circular &#40;Generador de informes y SSRS&#41;](display-percentage-values-on-a-pie-chart-report-builder-and-ssrs.md)  
  
  
