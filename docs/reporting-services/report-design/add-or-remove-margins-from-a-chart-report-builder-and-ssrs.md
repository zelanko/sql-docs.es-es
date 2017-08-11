---
title: "Agregar o quitar márgenes de un gráfico (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 91c43f58-5771-4d33-a54d-0e802d2f5cba
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 795435899de548848ca64cec26d212fd8a80f900
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="add-or-remove-margins-from-a-chart-report-builder-and-ssrs"></a>Agregar o quitar márgenes de un gráfico (Generador de informes y SSRS)
Para los gráficos de columnas y de dispersión de los informes paginados de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , el gráfico agrega automáticamente márgenes laterales en los extremos del eje X. En los gráficos de barras, el gráfico agrega automáticamente márgenes laterales en los extremos del eje Y. En todos los demás tipos de gráficos, el gráfico no agrega márgenes laterales. No puede cambiar el tamaño del margen.  
  
 Este tema no se aplica a los tipos de gráficos circulares, de anillos, de embudo ni piramidales.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-enable-or-disable-side-margins"></a>Habilitar o deshabilitar los márgenes laterales  
  
1.  Haga clic con el botón derecho en el eje y seleccione **Propiedades del eje**. Se abre el cuadro de diálogo **Propiedades del eje vertical** u **horizontal** .  
  
2.  En la página **Opciones del eje** , establezca la propiedad **Márgenes laterales** :  
  
    -   **Automático:** el gráfico determinará si se agrega un margen lateral basado en el tipo de gráfico.  
  
    -   **Deshabilitado:** los gráficos de barras, columna y dispersión no tendrán márgenes laterales.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a las etiquetas del eje en un gráfico de &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Cuadro de diálogo de propiedades de eje, opciones del eje &#40; El generador de informes y SSRS &#41;](http://msdn.microsoft.com/library/b276e210-7a12-48ae-971b-7dabae51df11)   
 [Especificar un intervalo de eje &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [Etiquetas del eje de formato como fechas o monedas &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Gráficos &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
