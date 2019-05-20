---
title: Solucionar problemas de gráficos (Generador de informes y SSRS) | Microsoft Docs
ms.date: 01/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 365128fe0fd67f1b270481f827eef6871acccb5d
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65573749"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>Solucionar problemas de gráficos (Generador de informes y SSRS)
  Estos temas pueden resultar útiles al trabajar con gráficos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>¿Por qué mi gráfico cuenta, y no suma, los valores del eje de valores?  
 Para que se dibujen correctamente, la mayoría de los tipos de gráficos requieren valores numéricos a lo largo del eje de valores, que normalmente es el eje Y. Si el tipo de datos del campo de valores es **String**, el gráfico no puede mostrar un valor numérico, aun cuando haya números en los campos. En su lugar, el gráfico muestra un recuento del número total de filas que contienen un valor en ese campo. Para evitar este comportamiento, asegúrese de que los campos que usa para la serie de valores tienen tipos de datos numéricos, en lugar de cadenas que contienen números con formato.  

## <a name="need-more-help"></a>¿Necesita ayuda?  
   
  Pruebe:  
 * [SQL Server Reporting Services](https://stackoverflow.com/questions/tagged/reporting-services) en Stack Overflow  
 * Registre un problema o sugerencia en [UserVoice de Microsoft SQL Server](https://feedback.azure.com/forums/908035-sql-server).  
  
## <a name="see-also"></a>Consulte también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
