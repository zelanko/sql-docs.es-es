---
title: "Especificar el tama&#241;o de un indicador utilizando una expresi&#243;n (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ab0b86f1-4882-4258-a2b6-c612faecfa4b
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 7
---
# Especificar el tama&#241;o de un indicador utilizando una expresi&#243;n (Generador de informes y SSRS)
  Además del color, dirección y forma, puede usar el tamaño para maximizar el impacto visual de los indicadores.  
  
 Un indicador tiene una colección de estados de indicador denominada IndicatorStates. La colección IndicatorStates suele tener varios estados. Cada estado es un miembro de la colección y se representa mediante un icono. Juntos, los estados constituyen la colección IndicatorsStates.  
  
 Para configurar dinámicamente el tamaño de los iconos, debe establecer propiedades de los miembros de la colección IndicatorsStates en el panel Propiedades del Generador de informes. Si el panel **Propiedades** no está visible, haga clic en la pestaña **Ver** y seleccione **Propiedades**.  
  
> [!NOTE]  
>  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], utilice la ventana **Propiedades** para establecer las propiedades de miembro. Si la ventana **Propiedades** no está abierta, presione la tecla F4.  
  
 El panel **Propiedades** proporciona acceso a las propiedades de la colección IndicatorStates de un indicador. Para configurar los iconos de forma que tengan tamaños distintos, debe establecer la propiedad ScaleFactor de los miembros de la colección IndicatorStates mediante una expresión. Para obtener más información, vea [Expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
 La expresión usada en este procedimiento se usó también para generar el informe con distintos tamaños de indicadores, como se muestra en [Indicadores &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para especificar el tamaño de icono de indicador mediante una expresión  
  
1.  Haga clic en el indicador que desea cambiar.  
  
2.  En el panel Propiedades, busque la propiedad IndicatorStates.  
  
     Si el panel Propiedades está organizado por categorías, encontrará IndicatorStates en la categoría **Estados**.  
  
3.  Haga clic en el botón de puntos suspensivos **(…)** situado junto a IndicatorStates. Se abre el cuadro de diálogo **Editor de la colección IndicatorState** .  
  
     Seleccione todos los miembros de la colección.  
  
4.  En la lista **Selección múltiple de propiedades**, haga clic en la flecha hacia abajo que hay al lado de ScaleFactor y, después, haga clic en **Expresión**.  
  
5.  En el cuadro de diálogo **Expresión** escriba la expresión.  
  
     La siguiente expresión de ejemplo hace que el icono tenga un tamaño distinto en función del valor del campo **SalesYTD** .  
  
     `=IIF(Fields!SalesYTD.value = 0,0,Fields!SalesYTD.value/Max(Fields!SalesYTD.value,"Indicator"))`  
  
     Para obtener más información, vea [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Vea también  
 [Indicadores &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  