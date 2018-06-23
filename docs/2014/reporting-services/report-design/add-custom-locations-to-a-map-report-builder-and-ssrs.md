---
title: Agregar ubicaciones personalizadas a un mapa (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- MICROSOFT.REPORTDESIGNER.MAPPOINT.POINTTEMPLATE
ms.assetid: 7d36faae-5bcc-446a-9eba-f42349cafacb
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 50a1037a5465e1e22d5c70def2b005fdbac0ec4d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109416"
---
# <a name="add-custom-locations-to-a-map-report-builder-and-ssrs"></a>Agregar ubicaciones personalizadas a un mapa (Generador de informes y SSRS)
  Después de agregar un mapa a un informe, puede agregar sus propias ubicaciones de punto.  
  
 Las propiedades de presentación de todos los puntos de una capa se controlan estableciendo opciones para las propiedades de punto de la capa. En un punto incrustado seleccionado, puede invalidar las propiedades de presentación.  
  
> [!NOTE]  
>  Al invalidar las propiedades de presentación de capa para el punto incrustado, las modificaciones que realice no son reversibles.  
  
 Para obtener más información, vea [Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos &#40;Generador de informes y SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-point-layer"></a>Para agregar una capa de punto  
  
1.  En la superficie de diseño del informe, haga clic en el mapa para seleccionarlo y muestre el panel Mapa.  
  
2.  En la barra de herramientas, haga clic en **Agregar capa**.  
  
3.  En la lista desplegable, haga clic en **Agregar capa de punto**. Una capa de punto sin puntos se agrega al mapa. De forma predeterminada, la capa de punto está lista para los puntos incrustados.  
  
### <a name="to-add-a-custom-point"></a>Para agregar un punto personalizado  
  
1.  En la superficie de diseño del informe, haga clic en el mapa para seleccionarlo y muestre el panel Mapa.  
  
2.  En el panel Mapa, haga clic con el botón derecho en una capa de punto que tenga el tipo **Incrustado**y luego haga clic en **Agregar punto**. El cursor cambia a la forma de cruz.  
  
3.  Para agregar un punto, haga clic en una ubicación del mapa. Un punto incrustado se agrega a la capa seleccionada en la ubicación donde haga clic.  
  
### <a name="to-customize-the-display-for-an-embedded-point"></a>Para personalizar la presentación de un punto incrustado  
  
1.  Haga clic con el botón derecho en el punto y luego haga clic en **Propiedades del punto**. Se abre el cuadro de diálogo **Propiedades de punto incrustado de mapa** .  
  
2.  Haga clic en **Invalidar opciones de punto para esta capa**. Varias páginas de propiedad aparecen en el panel izquierdo.  
  
3.  Haga clic en las páginas y establezca las propiedades de presentación que desee aplicar a este punto.  
  
## <a name="see-also"></a>Vea también  
 [Mapas &#40;Generador de informes y SSRS&#41;](maps-report-builder-and-ssrs.md)   
 [Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos &#40;Generador de informes y SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  