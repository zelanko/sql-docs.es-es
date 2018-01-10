---
title: "Mostrar encabezados y pies de página con un grupo (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8eb7d648-4df2-491a-96cb-99e55629d617
caps.latest.revision: "8"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 92f7c462be75d4557ab44216af1beb14d101029e
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="display-headers-and-footers-with-a-group-report-builder-and-ssrs"></a>Mostrar encabezados y pies de página con un grupo (Generador de informes y SSRS)
  Puede ayudar a controlar si una fila estática, como un encabezado o un pie de grupo, se representa en filas dinámicas asociadas a un grupo en una región de datos Tablix.  
  
 Para repetir todos los encabezados de columna o de fila en varias páginas, puede establecer propiedades para la región de datos Tablix. Para más información, vea [Mostrar encabezados de fila y de columna en varias páginas (Generador de informes y SSRS)](display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md).  
  
 Para controlar el comportamiento de representación para filas y columnas dinámicas asociadas a grupos anidados, o para filas y columnas estáticas asociadas a etiquetas o subtotales, debe establecer propiedades para el miembro de Tablix. Un miembro de Tablix representa una fila o una columna estática o dinámica. Un miembro estático se repite una vez. Por ejemplo, una fila de total general es una fila estática. Un miembro dinámico se repite una vez para cada instancia de grupo. Por ejemplo, una fila asociada a un grupo con la expresión de grupo [Territory] se repite una vez para cada valor único de territorio. Para más información sobre los miembros de Tablix, vea [Celdas, filas y columnas de la región de datos Tablix &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tablix-data-region-cells-rows-and-columns-report-builder-and-ssrs.md).  
  
 Puede seleccionar un miembro de Tablix en el Panel de agrupación y establecer las propiedades **KeepWithGroup**, **KeepTogether**y **RepeatOnNewPage** en el panel Propiedades. Utilice **KeepWithGroup** para ayudar a mostrar encabezados y pies de grupo en la misma página que el grupo. Utilice **KeepTogether** para ayudar a mostrar miembros estáticos con las filas o columnas de un grupo. Utilice **RepeatOnNewPage** para repetir el encabezado o pie de grupo de página en todas las páginas que muestren al menos una instancia completa del miembro del grupo de la fila designado por el valor **KeepWithGroup** . **RepeatOnNewPage** no se admite para los miembros de grupo de columnas.  
  
> [!NOTE]  
>  **KeepWithGroup**, **KeepTogether** y **RepeatOnNewPage** son propiedades de miembro de grupo que se pueden establecer con el **Modo avanzado** del panel Agrupación. Para más información, vea [Panel de agrupación &#40;Generador de informes&#41;](../../reporting-services/report-design/grouping-pane-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-keep-a-static-row-with-a-set-of-dynamic-rows-associated-with-a-row-group"></a>Para mantener una fila estática con un conjunto de filas dinámicas asociadas con un grupo de filas  
  
1.  En la superficie de diseño, haga clic en cualquier lugar de la región de datos Tablix para seleccionarla. El Panel de agrupación muestra los grupos de filas y de columnas para la región de datos.  
  
2.  En el lado derecho del panel Agrupación, haga clic en la flecha abajo y, a continuación, haga clic en **Modo avanzado**. El panel Grupos de filas muestra los miembros estáticos y dinámicos de la jerarquía de grupos de filas.  
  
3.  Haga clic en el miembro estático correspondiente al encabezado de fila o al pie de página que desea mantener con las filas de grupo. El panel de propiedades muestra las propiedades de **Miembro de Tablix** .  
  
4.  En el panel de propiedades, haga clic en **KeepWithGroup**y, después, elija uno de los valores siguientes en la lista desplegable:  
  
    -   **Ninguno** : seleccione esta opción si no desea indicar ninguna preferencia para mantener este miembro con los miembros del grupo de filas seleccionado.  
  
    -   **Antes** : seleccione esta opción para mantener este miembro con los miembros del grupo anterior. Debería usar esta opción para las filas del pie de página de grupo.  
  
    -   **Después** : seleccione esta opción para mantener este miembro con los miembros del grupo siguiente. Debería usar esta opción para las filas del encabezado de página de grupo.  
  
5.  (Opcional) Obtenga una vista previa del informe. Donde sea posible, el presentador de informes mantendrá este miembro con los miembros de grupo de filas especificados.  
  
### <a name="to-keep-a-static-column-with-a-set-of-dynamic-columns-associated-with-a-column-group"></a>Para mantener una columna estática con un conjunto de columnas dinámicas asociadas con un grupo de columnas  
  
1.  En la superficie de diseño, haga clic en cualquier lugar de la región de datos Tablix para seleccionarla. El Panel de agrupación muestra los grupos de filas y de columnas para la región de datos.  
  
2.  En el lado derecho del panel Agrupación, haga clic en la flecha abajo y, a continuación, haga clic en **Modo avanzado**. El panel Grupos de columnas muestra los miembros estáticos y dinámicos de la jerarquía de grupos de columnas.  
  
3.  Haga clic en el miembro estático correspondiente a la columna estática que desea mantener con las columnas de grupo. El panel de propiedades muestra las propiedades de **Miembro de Tablix** .  
  
4.  En el panel de propiedades, haga clic en **KeepWithGroup**y, después, elija uno de los valores siguientes en la lista desplegable:  
  
    -   **Ninguno** : seleccione esta opción si no desea indicar ninguna preferencia para mantener este miembro con los miembros del grupo de columnas seleccionado.  
  
    -   **Antes** : seleccione esta opción para mantener este miembro con los miembros del grupo anterior. Debería usar esta opción para las etiquetas de columna que se muestran antes de los miembros de grupo de columnas especificados.  
  
    -   **Después** : seleccione esta opción para mantener este miembro con los miembros del grupo siguiente. Debería usar esta opción para los totales de columna que se muestran después de los miembros de grupo de columnas especificados.  
  
5.  (Opcional) Obtenga una vista previa del informe. Donde sea posible, el representador de informes mantendrá este miembro con los miembros de grupo de columnas especificados.  
  
## <a name="see-also"></a>Ver también  
 [Celdas, filas y columnas de la región de datos Tablix (Generador de informes y SSRS)](tablix-data-region-report-builder-and-ssrs.md)   
 
  
  
