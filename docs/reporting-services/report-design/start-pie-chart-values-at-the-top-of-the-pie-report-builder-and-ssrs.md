---
title: Inicio de los valores del gráfico circular desde la parte superior del gráfico (Generador de informes) | Microsoft Docs
description: Obtenga información sobre cómo iniciar los valores de gráficos circulares en la parte superior del gráfico en lugar de a 90 grados desde la parte superior, el valor predeterminado.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d0e6fb59-ca4e-4d70-97cb-0ad183da21d3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b1158cf4a88bb491b8ed1cb492eec1c3021cb6f9
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907063"
---
# <a name="start-pie-chart-values-at-the-top-of-the-pie-report-builder-and-ssrs"></a>Iniciar los valores del gráfico circular desde la parte superior del gráfico (Generador de informes y SSRS)
En los gráficos circulares de los informes paginados de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , el primer valor del conjunto de datos se inicia de forma predeterminada en 90 grados desde la parte superior del círculo. 

![Captura de pantalla del gráfico circular de un generador de informes con el conjunto de datos que se inicia en 90 grados.](../../reporting-services/media/report-builder-pie-chart-start-at-90.png)

*Los valores del gráfico se inician en 90 grados.*

En su lugar, es posible que le interese que el primer valor se inicie en la parte superior. 

![Captura de pantalla del gráfico circular de un generador de informes con el conjunto de datos que se inicia desde la parte superior.](../../reporting-services/media/report-builder-pie-chart-start-at-top.png)

*Los valores del gráfico se inician en la parte superior del gráfico.*
  
## <a name="to-start-the-pie-chart-at-the-top-of-the-pie"></a>Iniciar el gráfico circular desde la parte superior del círculo  
  
1.  Haga clic en el círculo.  
  
2.  Si el panel **Propiedades** no está abierto, en la pestaña **Ver** haga clic en **Propiedades**.  
  
3.  En el panel **Propiedades** , en **Atributos personalizados** , cambie **PieStartAngle** de **0** a **270**.  
  
4.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
 El primer valor se inicia ahora en la parte superior del gráfico circular.  
  
## <a name="see-also"></a>Consulte también  
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Gráficos circulares &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pie-charts-report-builder-and-ssrs.md)  
  
  
