---
title: Especificar el tamaño de un indicador mediante una expresión (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: ab0b86f1-4882-4258-a2b6-c612faecfa4b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a77a96d57a1ea9489697a415e96fb52165b8270f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967201"
---
# <a name="specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs"></a>Especificar el tamaño de un indicador utilizando una expresión (Generador de informes y SSRS)
  Además del color, dirección y forma, puede usar el tamaño para maximizar el impacto visual de los indicadores.  
  
 Un indicador tiene una colección de estados de indicador denominada IndicatorStates. La colección IndicatorStates suele tener varios estados. Cada estado es un miembro de la colección y se representa mediante un icono. Juntos, los estados constituyen la colección IndicatorsStates.  
  
 Para configurar dinámicamente el tamaño de los iconos, debe establecer propiedades de los miembros de la colección IndicatorsStates en el panel Propiedades del Generador de informes. Si el panel **Propiedades** no está visible, haga clic en la pestaña **Ver** y seleccione **Propiedades**.  
  
> [!NOTE]  
>  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], utilice la ventana **Propiedades** para establecer las propiedades de miembro. Si la ventana **Propiedades** no está abierta, presione la tecla F4.  
  
 El panel **Propiedades** proporciona acceso a las propiedades de la colección IndicatorStates de un indicador. Para configurar los iconos de forma que tengan tamaños distintos, debe establecer la propiedad ScaleFactor de los miembros de la colección IndicatorStates mediante una expresión. Para más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
 La expresión usada en este procedimiento se usó también para generar el informe con distintos tamaños de indicadores, como se muestra en [Indicadores &#40;Generador de informes y SSRS&#41;](indicators-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-the-indicator-icon-size-using-an-expression"></a>Para especificar el tamaño de icono de indicador mediante una expresión  
  
1.  Haga clic en el indicador que desea cambiar.  
  
2.  En el panel Propiedades, busque la propiedad IndicatorStates.  
  
     Si el panel Propiedades está organizado por categorías, encontrará IndicatorStates en la categoría **Estados** .  
  
3.  Haga clic en el botón de puntos suspensivos **(…)** situado junto a IndicatorStates. Se abre el cuadro de diálogo **Editor de la colección IndicatorState** .  
  
     Seleccione todos los miembros de la colección.  
  
4.  En la lista **Selección múltiple de propiedades** , haga clic en la flecha hacia abajo que hay al lado de ScaleFactor y, después, haga clic en **Expresión**.  
  
5.  En el cuadro de diálogo **Expresión** escriba la expresión.  
  
     La siguiente expresión de ejemplo hace que el icono tenga un tamaño distinto en función del valor del campo **SalesYTD** .  
  
     `=IIF(Fields!SalesYTD.value = 0,0,Fields!SalesYTD.value/Max(Fields!SalesYTD.value,"Indicator"))`  
  
     Para más información, vea [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Indicadores &#40;Generador de informes y SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  
