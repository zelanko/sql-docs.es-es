---
title: Agregar o quitar márgenes de un gráfico (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c9f3ec8448c379cf57cb31f7724cc5596a4769a5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150346"
---
# <a name="add-or-remove-margins-from-a-chart-report-builder-and-ssrs"></a>Agregar o quitar márgenes de un gráfico (Generador de informes y SSRS)
  En los gráficos de dispersión y de columnas, el gráfico agrega automáticamente márgenes laterales en los extremos del eje X. En los gráficos de barras, el gráfico agrega automáticamente márgenes laterales en los extremos del eje Y. En todos los demás tipos de gráficos, el gráfico no agrega márgenes laterales. No puede cambiar el tamaño del margen.  
  
 Este tema no se aplica a los tipos de gráficos circulares, de anillos, de embudo ni piramidales.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-enable-or-disable-side-margins"></a>Habilitar o deshabilitar los márgenes laterales  
  
1.  Haga clic con el botón derecho en el eje y seleccione **Propiedades del eje**. Se abre el cuadro de diálogo **Propiedades del eje vertical** u **horizontal** .  
  
2.  En la página **Opciones del eje** , establezca la propiedad **Márgenes laterales** :  
  
    -   **Automático:** el gráfico determinará si se agrega un margen lateral basado en el tipo de gráfico.  
  
    -   **Deshabilitado:** los gráficos de barras, columna y dispersión no tendrán márgenes laterales.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Cuadro de diálogo Propiedades del eje, Opciones del eje &#40;Generador de informes y SSRS&#41;](../axis-properties-dialog-box-axis-options-report-builder-and-ssrs.md)   
 [Especificar un intervalo de eje &#40;Generador de informes y SSRS&#41;](specify-an-axis-interval-report-builder-and-ssrs.md)   
 [Aplicar formato de fecha o de moneda a las etiquetas de los ejes &#40;Generador de informes y SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Los gráficos &#40;generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
