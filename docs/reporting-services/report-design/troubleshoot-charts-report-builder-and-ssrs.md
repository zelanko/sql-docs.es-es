---
title: "Solucionar problemas de gráficos (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
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
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 4f7c1005a361e5eae7a7d1b674691df6e7444d46
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>Solucionar problemas de gráficos (Generador de informes y SSRS)
  Estos temas pueden resultar útiles al trabajar con gráficos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>¿Por qué mi gráfico cuenta, y no suma, los valores del eje de valores?  
 Para que se dibujen correctamente, la mayoría de los tipos de gráficos requieren valores numéricos a lo largo del eje de valores, que normalmente es el eje Y. Si el tipo de datos del campo de valores es **String**, el gráfico no puede mostrar un valor numérico, aun cuando haya números en los campos. En su lugar, el gráfico muestra un recuento del número total de filas que contienen un valor en ese campo. Para evitar este comportamiento, asegúrese de que los campos que usa para la serie de valores tienen tipos de datos numéricos, en lugar de cadenas que contienen números con formato.  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
