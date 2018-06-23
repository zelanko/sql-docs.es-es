---
title: Ocultar elementos de leyenda en el gráfico (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 92256240-0cd5-4be4-8904-d1e3b93cb6b3
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 13064f5d0033a1a4677789c6031b1f9b0f322379
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103962"
---
# <a name="hide-legend-items-on-the-chart-report-builder-and-ssrs"></a>Ocultar elementos de leyenda en el gráfico (Generador de informes y SSRS)
  De forma predeterminada, cualquier serie que se agregue a un gráfico que no sea un gráfico de formas se agregará como elemento en la leyenda. En los gráficos circulares, de anillos, de embudo y piramidales, cualquier serie que se agregue al gráfico agregará puntos de datos individuales a la leyenda.  
  
 Puede ocultar cualquier elemento de la leyenda. Aunque oculte un elemento de leyenda, este seguirá apareciendo en el gráfico. Esto resulta de gran utilidad en situaciones donde no se desea mostrar más información sobre una serie agregada al gráfico. Por ejemplo, si ha agregado al gráfico una serie calculada, como una media móvil, puede ser que le interese ocultar esta entrada en la leyenda para que solo se muestre más información sobre la serie original.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-an-item-from-display-in-the-legend"></a>Para ocultar un elemento en la leyenda  
  
1.  Haga clic con el botón derecho en la serie que quiere ocultar y seleccione **Propiedades de la serie**.  
  
2.  Haga clic en **Leyenda**. Seleccione la opción **No mostrar esta serie en una leyenda** .  
  
    > [!NOTE]  
    >  No puede ocultar una serie para un grupo y dejarla visible para los demás. Si ha agregado un campo al área **Grupos de series** , se ocultarán todas las series que pertenecen a este grupo.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a la leyenda en un gráfico &#40;el generador de informes SSRS&#41;](chart-legend-formatting-report-builder.md)   
 [Aplicar formato a los puntos de datos en un gráfico &#40;el generador de informes SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)   
 [Cambiar el texto de un elemento de leyenda &#40;Generador de informes y SSRS&#41;](chart-legend-change-item-text-report-builder.md)   
 [Agregar una media móvil a un gráfico &#40;Generador de informes y SSRS&#41;](add-a-moving-average-to-a-chart-report-builder-and-ssrs.md)   
 [Cuadro de diálogo de Propiedades de la leyenda, General &#40;Generador de informes y SSRS&#41;](../legend-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  