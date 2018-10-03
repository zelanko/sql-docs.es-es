---
title: Trazar datos en un eje secundario (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 094f39bf-3634-4852-9fc3-3adec4b266e5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: e86c8ebb206ac6aefb6a68ccc1da02de88e48fe2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48123555"
---
# <a name="plot-data-on-a-secondary-axis-report-builder-and-ssrs"></a>Trazar datos en un eje secundario (Generador de informes y SSRS)
  El gráfico tiene dos tipos de ejes: el principal y el secundario. El eje secundario resulta de gran utilidad cuando se comparan dos conjuntos de valores con dos intervalos de datos definidos que comparten una categoría común.  
  
 Por ejemplo, imagine que tiene un gráfico que calcula los ingresos frente a los impuestos durante el año 2008. En este caso, el período de tiempo 2008 es común a ambos conjuntos de valores. Sin embargo, si ambas series se trazan en el mismo eje Y, no podremos realizar una comparación útil porque la escala del eje Y se optimiza para los valores más altos del conjunto de datos. Si mostramos los ingresos en el eje principal, y los impuestos en el eje secundario, podremos mostrar cada serie en su propio eje Y con su propia escala de valores. Las series siguen compartiendo un eje X común.  
  
 En aquellas situaciones en las que se necesita comparar más de dos series, considere un enfoque diferente para comparar y mostrar dichas series. Para más información, vea [Mostrar varias series en un gráfico &#40;Generador de informes y SSRS&#41;](multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
 Un ejemplo de este gráfico está disponible como informe de ejemplo. Para más información acerca de cómo descargar este y otros informes de ejemplo, consulte el tema sobre [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][informes de ejemplo del Generador de informes y el Diseñador de informes](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-plot-a-series-on-the-secondary-axis"></a>Para trazar una serie en el eje secundario  
  
1.  Haga clic con el botón derecho en la serie del gráfico o en un campo del área **Valores** que quiera mostrar en el eje secundario y, después, haga clic en **Propiedades de la serie**. Aparece el cuadro de diálogo **Propiedades de la serie** .  
  
2.  Haga clic en **Ejes y área del gráfico**y seleccione los ejes secundarios que desea habilitar, el eje de valores o el eje de categorías.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Especifique un intervalo de eje &#40;generador de informes y SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)  
  
  
