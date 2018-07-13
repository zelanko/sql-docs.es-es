---
title: Especificar una escala logarítmica (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f3092c1c-b128-433d-9a95-983508b2a8d4
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c5833b8622d734acf7c2051c7fccc50a424d1560
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37170292"
---
# <a name="specify-a-logarithmic-scale-report-builder-and-ssrs"></a>Especificar una escala logarítmica (Generador de informes y SSRS)
  Si tiene datos que son proporcionales en términos logarítmicos, puede que le interese usar una escala logarítmica en el gráfico. Esto le ayudará a mejorar el aspecto del gráfico haciendo que los datos sean más fáciles de interpretar. La mayoría de las escalas logarítmicas son de base 10.  
  
 Esta característica solo está disponible en el eje de valores. El eje de valores es normalmente el vertical, o eje Y. En los gráficos de barras, sin embargo, es el eje horizontal, o X.  
  
 Si el eje es logarítmico, todas las demás propiedades relativas al eje se ajustarán de acuerdo con una escala logarítmica. Por ejemplo, si especifica una escala logarítmica de base 10 en el eje y establece un intervalo de eje de 2, se generarán intervalos con una magnitud de 10 elevado a 2, es decir, 100. Esto significa que en el eje de valores aparecerán los valores 1, 100, 10000, en lugar del resultado predeterminado 1, 10, 100, 1000, 10000.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-a-logarithmic-scale"></a>Para especificar una escala logarítmica  
  
1.  Haga clic con el botón derecho en el eje Y del gráfico y, después, haga clic en **Propiedades del eje vertical**. Se abrirá el cuadro de diálogo **Propiedades del eje vertical** .  
  
2.  En **Opciones del eje**, seleccione **Usar escala logarítmica**.  
  
3.  En el cuadro de texto **Base logarítmica** , escriba un valor positivo para la base logarítmica. Si no se especifica ningún valor, el valor predeterminado para la base logarítmica es 10.  
  
## <a name="see-also"></a>Vea también  
 [Aplicar formato a las etiquetas de los ejes de un gráfico &#40;Generador de informes y SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Aplicar formato de fecha o de moneda a las etiquetas de los ejes &#40;Generador de informes y SSRS&#41;](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Los gráficos &#40;generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
