---
title: Solucionar problemas de gráficos (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7462ae28164ed971298e41624455b7fecac55446
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56012496"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>Solucionar problemas de gráficos (Generador de informes y SSRS)
  Estos temas pueden resultar útiles al trabajar con gráficos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>¿Por qué mi gráfico cuenta, y no suma, los valores del eje de valores?  
 Para que se dibujen correctamente, la mayoría de los tipos de gráficos requieren valores numéricos a lo largo del eje de valores, que normalmente es el eje Y. Si el tipo de datos del campo de valores es `String`, el gráfico no puede mostrar un valor numérico, aun cuando haya números en los campos. En su lugar, el gráfico muestra un recuento del número total de filas que contienen un valor en ese campo. Para evitar este comportamiento, asegúrese de que los campos que usa para la serie de valores tienen tipos de datos numéricos, en lugar de cadenas que contienen números con formato.  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
