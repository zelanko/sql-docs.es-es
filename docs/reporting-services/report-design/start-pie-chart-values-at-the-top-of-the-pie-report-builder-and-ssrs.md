---
title: Iniciar los valores del gráfico circular desde la parte superior del gráfico (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 32a16b4738a5cbcb963dea1a425ab92b72e6660b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47836113"
---
# <a name="start-pie-chart-values-at-the-top-of-the-pie-report-builder-and-ssrs"></a>Iniciar los valores del gráfico circular desde la parte superior del gráfico (Generador de informes y SSRS)
En los gráficos circulares de los informes paginados de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , el primer valor del conjunto de datos se inicia de forma predeterminada en 90 grados desde la parte superior del círculo. 

![generador-informes-gráfico-circular-inicia-en-90](../../reporting-services/media/report-builder-pie-chart-start-at-90.png)

*Los valores del gráfico se inician en 90 grados.*

En su lugar, podría interesarle que el primer valor se inicie en la parte superior. 

![generador-informes-gráfico-circular-inicia-parte-superior](../../reporting-services/media/report-builder-pie-chart-start-at-top.png)

*Los valores del gráfico se inician en la parte superior del gráfico.*
  
## <a name="to-start-the-pie-chart-at-the-top-of-the-pie"></a>Iniciar el gráfico circular desde la parte superior del círculo  
  
1.  Haga clic en el círculo.  
  
2.  Si el panel **Propiedades** no está abierto, en la pestaña **Ver** haga clic en **Propiedades**.  
  
3.  En el panel **Propiedades** , en **Atributos personalizados**, cambie **PieStartAngle** de **0** a **270**.  
  
4.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
 El primer valor se inicia ahora en la parte superior del gráfico circular.  
  
## <a name="see-also"></a>Ver también  
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Gráficos circulares &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
