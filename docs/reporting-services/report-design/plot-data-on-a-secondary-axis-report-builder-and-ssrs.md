---
title: Trazar datos en un eje secundario (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 094f39bf-3634-4852-9fc3-3adec4b266e5
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d4ca3cc183fb405fc9379f29012a92e39b7ad95b
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---

# <a name="plot-data-on-a-secondary-axis-report-builder-and-ssrs"></a>Trazar datos en un eje secundario (Generador de informes y SSRS)

El gráfico tiene dos tipos de ejes: el principal y el secundario. El eje secundario resulta de gran utilidad cuando se comparan dos conjuntos de valores con dos intervalos de datos definidos que comparten una categoría común.  
  
 Por ejemplo, imagine que tiene un gráfico que calcula los ingresos frente a los impuestos durante el año 2008. En este caso, el período de tiempo 2008 es común a ambos conjuntos de valores. Sin embargo, si ambas series se trazan en el mismo eje Y, no podremos realizar una comparación útil porque la escala del eje Y se optimiza para los valores más altos del conjunto de datos. Si mostramos los ingresos en el eje principal, y los impuestos en el eje secundario, podremos mostrar cada serie en su propio eje Y con su propia escala de valores. Las series siguen compartiendo un eje X común.  
  
 En aquellas situaciones en las que se necesita comparar más de dos series, considere un enfoque diferente para comparar y mostrar dichas series. Para obtener más información, consulte [mostrar varias Series en un gráfico de](../../reporting-services/report-design/multiple-series-on-a-chart-report-builder-and-ssrs.md).  
  
 Un ejemplo de este gráfico está disponible como informe de ejemplo. Para obtener más información acerca de cómo descargar este ejemplo y otros informes, consulte [informes de ejemplo del generador de informes y el Diseñador de informes](http://go.microsoft.com/fwlink/?LinkId=198283).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-plot-a-series-on-the-secondary-axis"></a>Para trazar una serie en el eje secundario  
  
1.  Haga clic con el botón derecho en la serie del gráfico o en un campo del área **Valores** que quiera mostrar en el eje secundario y, después, haga clic en **Propiedades de la serie**. Aparece el cuadro de diálogo **Propiedades de la serie** .  
  
2.  Haga clic en **Ejes y área del gráfico**y seleccione los ejes secundarios que desea habilitar, el eje de valores o el eje de categorías.  

## <a name="next-steps"></a>Pasos siguientes

[Aplicar formato a las etiquetas del eje en un gráfico](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
[Especifique un intervalo de eje](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
