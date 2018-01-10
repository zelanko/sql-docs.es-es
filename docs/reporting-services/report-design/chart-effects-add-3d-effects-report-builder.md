---
title: "Agregar efectos 3D a un gráfico (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab9625d8-6557-4a4d-8123-eefa7c066ff5
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ec6a2c4e4b26069d25874fabb0e3222b778c50ee
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="chart-effects---add-3d-effects-report-builder"></a>Efectos de gráfico: agregar efectos 3D (Generador de informes)
  Se pueden usar efectos tridimensionales (3D) para dar profundidad y agregar impacto visual a los gráficos de los informes paginados de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Por ejemplo, si desea resaltar un sector específico de un gráfico circular seccionado, puede girar y cambiar la perspectiva del gráfico para que los usuarios se fijen primero en dicho sector. Cuando se aplican efectos 3D al gráfico, se deshabilitan todos los colores de degradado y los estilos de sombreado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-apply-3d-effects-to-a-range-area-line-scatter-or-polar-chart"></a>Para aplicar efectos 3D a un gráfico de intervalos, áreas, líneas, dispersión o polar  
  
1.  Haga clic con el botón derecho en cualquier parte dentro del área del gráfico y seleccione **Efectos 3D**. Aparecerá el cuadro de diálogo **Propiedades del área de gráfico** .  
  
2.  En **Opciones 3D**, seleccione la opción **Habilitar 3D** .  
  
3.  (Opcional) En **Opciones 3D**, puede establecer diversas propiedades relacionadas con opciones de ángulos y escenas 3D. Para obtener más información sobre estas propiedades, vea [Aplicar 3D, bisel y otros efectos a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/chart-effects-3d-bevel-and-other-report-builder.md).  
  
4.  Haga clic en **Aceptar**.  
  
## <a name="to-apply-3d-effects-to-a-funnel-chart"></a>Para aplicar efectos 3D a un gráfico de embudo  
  
1.  Haga clic con el botón derecho en cualquier parte dentro del área del gráfico y seleccione **Efectos 3D**. Aparecerá el cuadro de diálogo **Propiedades del área de gráfico** .  
  
2.  En **Opciones 3D**, seleccione la opción **Habilitar 3D** . Haga clic en **Aceptar**.  
  
3.  (Opcional) Para personalizar el aspecto visual del gráfico de embudo, puede ir al panel Propiedades y cambiar propiedades específicas para ese tipo de gráfico.  
  
    1.  Abra el panel de propiedades.  
  
    2.  En la superficie de diseño, haga clic en cualquier parte del gráfico de embudo. Se muestran las propiedades de las series del gráfico de embudo en el panel de propiedades.  
  
    3.  En la sección **General** , expanda el nodo **CustomAttributes** .  
  
    4.  Para la propiedad **Funnel3DDrawingStyle** , seleccione si el embudo se mostrará como circular o cuadrado.  
  
    5.  Para la propiedad **Funnel3DRotationAngle** , establezca un valor entre -10 y 10. Esto determinará el grado de inclinación que se mostrará en el gráfico de embudo 3D.  
  
## <a name="to-apply-3d-effects-to-a-pie-chart"></a>Para aplicar efectos 3D a un gráfico circular  
  
1.  Haga clic con el botón secundario en cualquier parte dentro del área del gráfico y seleccione Efectos 3D. Aparecerá el cuadro de diálogo **Propiedades del área de gráfico** .  
  
2.  En **Opciones 3D**, seleccione la opción **Habilitar 3D** . Haga clic en **Aceptar**.  
  
3.  (Opcional) En **Giro**, escriba un valor entero que represente el giro horizontal del gráfico circular.  
  
4.  (Opcional) En **Inclinación**, escriba un valor entero que represente el giro de inclinación vertical del gráfico circular.  
  
5.  Haga clic en **Aceptar**.  
  
## <a name="to-apply-3d-effects-to-a-bar-or-column-chart"></a>Para aplicar efectos 3D a un gráfico de barras o de columnas  
  
1.  Haga clic con el botón derecho en cualquier parte dentro del área del gráfico y seleccione **Efectos 3D**. Aparecerá el cuadro de diálogo **Propiedades del área de gráfico** .  
  
2.  Seleccione la opción **Habilitar 3D** . Haga clic en **Aceptar**.  
  
3.  (Opcional) Seleccione la opción **Habilitar agrupación en clústeres** . Si el gráfico contiene varias series de gráficos de barras o de columnas, esta opción mostrará las series agrupadas en clústeres. De forma predeterminada, cuando hay varias series de barras o de columnas se muestran unas al lado de otras.  
  
4.  Haga clic en **Aceptar**.  
  
5.  (Opcional) Para agregar efectos de cilindro a un gráfico de barras o de columnas, siga estos pasos:  
  
    1.  Abra el panel de propiedades.  
  
    2.  En la superficie de diseño, haga clic en cualquiera de las barras en la serie. Las propiedades de la serie se muestran en el panel de propiedades.  
  
    3.  En la sección **General** , expanda el nodo **CustomAttributes** .  
  
    4.  Para la propiedad **DrawingStyle** , especifique el valor **Cylinder** .  
  
## <a name="see-also"></a>Ver también  
 [Aplicar 3D, bisel y otros efectos a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/chart-effects-3d-bevel-and-other-report-builder.md)   
 [Aplicar formato a un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
 [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  
