---
title: Agregar un marco de borde a un gráfico (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ca0c5040-40bb-4cb7-bc2b-5bcbe73858bb
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 85f87076fc39eec424f92dfff1bb608b02ee1804
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203582"
---
# <a name="add-a-border-frame-to-a-chart-report-builder-and-ssrs"></a>Agregar un marco de borde a un gráfico (Generador de informes y SSRS)
  Para dar un mayor impacto visual a un gráfico, considere la posibilidad de situar un marco de borde alrededor del gráfico. Para seleccionar un marco de borde, puede usar el cuadro de diálogo **Propiedades del gráfico** o el panel de propiedades. Los marcos de borde de gráfico no se pueden aplicar a ninguna otra región de datos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-apply-a-border-to-a-chart"></a>Para aplicar un borde a un gráfico  
  
1.  Haga clic con el botón derecho en cualquier lugar del gráfico y seleccione **Propiedades del gráfico**.  
  
    > [!NOTE]  
    >  Si **Propiedades del gráfico**no está visible, seleccione **Gráfico** en el menú contextual y, después, seleccione **Propiedades del gráfico**.  
  
2.  Seleccione **Borde**y haga clic en el tipo de borde que desea aplicar al gráfico.  
  
3.  (Opcional) Seleccione un valor o escriba una expresión que represente el estilo del borde.  
  
4.  (Opcional) Especifique el color de la línea que se dibujará alrededor del gráfico.  
  
    > [!NOTE]  
    >  La lista **Color de línea** contiene los colores comunes. Si quiere hacer su selección en una lista con más colores, haga clic en **Más colores** en la lista o haga clic en el botón de expresión (**fx**) situado junto a la lista para iniciar el editor **Expresión** .  
  
5.  (Opcional) Especifique el ancho del borde. Los valores válidos van de 0,25 pt a 20 pt. Considere la posibilidad de mantener el tamaño del borde entre 1 y 3 pt para conseguir el mejor efecto visual posible.  
  
6.  (Opcional) Si el informe contiene un color de fondo distinto del blanco, plantéese la posibilidad de definir un color de página con el mismo color. El color de página es el color de fondo que se ve alrededor de la línea de borde.  
  
7.  (Opcional) Si elige un tipo de marco, especifique un estilo y un color para dicho marco. La lista **Color de relleno de marco** contiene los colores comunes.  
  
## <a name="see-also"></a>Vea también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](formatting-a-chart-report-builder-and-ssrs.md)   
 [Agregar estilos con bisel, relieve y textura a un gráfico &#40;Generador de informes y SSRS&#41;](chart-effects-add-bevel-emboss-or-texture-report-builder.md)  
  
  