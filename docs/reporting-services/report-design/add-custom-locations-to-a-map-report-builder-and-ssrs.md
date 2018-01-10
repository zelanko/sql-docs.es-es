---
title: Agregar ubicaciones personalizadas a un mapa (Generador de informes y SSRS) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: MICROSOFT.REPORTDESIGNER.MAPPOINT.POINTTEMPLATE
ms.assetid: 7d36faae-5bcc-446a-9eba-f42349cafacb
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d4f6fe4d4ba90117cbb6db930419e272d210ccb5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="add-custom-locations-to-a-map-report-builder-and-ssrs"></a>Agregar ubicaciones personalizadas a un mapa (Generador de informes y SSRS)
  Después de agregar un mapa a un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , puede agregar sus propias ubicaciones de punto.  
  
 Las propiedades de presentación de todos los puntos de una capa se controlan estableciendo opciones para las propiedades de punto de la capa. En un punto incrustado seleccionado, puede invalidar las propiedades de presentación.  
  
> [!NOTE]  
>  Al invalidar las propiedades de presentación de capa para el punto incrustado, las modificaciones que realice no son reversibles.  
  
 Para más información, vea [Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-add-a-point-layer"></a>Para agregar una capa de punto  
  
1.  En la superficie de diseño del informe, haga clic en el mapa para seleccionarlo y muestre el panel Mapa.  
  
2.  En la barra de herramientas, haga clic en **Agregar capa**.  
  
3.  En la lista desplegable, haga clic en **Agregar capa de punto**. Una capa de punto sin puntos se agrega al mapa. De forma predeterminada, la capa de punto está lista para los puntos incrustados.  
  
## <a name="to-add-a-custom-point"></a>Para agregar un punto personalizado  
  
1.  En la superficie de diseño del informe, haga clic en el mapa para seleccionarlo y muestre el panel Mapa.  
  
2.  En el panel Mapa, haga clic con el botón derecho en una capa de punto que tenga el tipo **Incrustado**y luego haga clic en **Agregar punto**. El cursor cambia a la forma de cruz.  
  
3.  Para agregar un punto, haga clic en una ubicación del mapa. Un punto incrustado se agrega a la capa seleccionada en la ubicación donde haga clic.  
  
## <a name="to-customize-the-display-for-an-embedded-point"></a>Para personalizar la presentación de un punto incrustado  
  
1.  Haga clic con el botón derecho en el punto y luego haga clic en **Propiedades del punto**. Se abre el cuadro de diálogo **Propiedades de punto incrustado de mapa** .  
  
2.  Haga clic en **Invalidar opciones de punto para esta capa**. Varias páginas de propiedad aparecen en el panel izquierdo.  
  
3.  Haga clic en las páginas y establezca las propiedades de presentación que desee aplicar a este punto.  
  
## <a name="see-also"></a>Ver también  
 [Mapas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
