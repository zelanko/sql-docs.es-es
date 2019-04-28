---
title: Acción de obtención de detalles (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10249"
- "10186"
- sql12.rtp.rptdesigner.calculatedseriesproperties.visibility.f1
- sql12.rtp.rptdesigner.seriesproperties.visibility.f1
- sql12.rtp.rptdesigner.chartareaproperties.visibility.f1
- "10092"
- sql12.rtp.rptdesigner.textboxproperties.visibility.f1
- sql12.rtp.rptdesigner.charttitleproperties.visibility.f1
- "10167"
- sql12.rtp.rptdesigner.rectangleproperties.visibility.f1
- "10174"
- sql12.rtp.rptdesigner.majorgridlineproperties.visibility.f1
- "10155"
- "10123"
- sql12.rtp.rptdesigner.subreportproperties.visibility.f1
- "10425"
- sql12.rtp.rptdesigner.minorgridlineproperties.visibility.f1
- "10217"
- sql12.rtp.rptdesigner.axisproperties.visibility.f1
- sql12.rtp.rptdesigner.serieslabelproperties.visibility.f1
- "10161"
- sql12.rtp.rptdesigner.chartproperties.visibility.f1
- sql12.rtp.rptdesigner.legendproperties.visibility.f1
- sql12.rtp.rptdesigner.pictureproperties.visibility.f1
- "10215"
- "10258"
- "10144"
- "10062"
- "10053"
ms.assetid: 1f8d1ef2-0daf-40c6-9ba7-3b391249bcd4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0b939882e5021eb08925f974bad71d1720c6eff7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62825318"
---
# <a name="drilldown-action-report-builder-and-ssrs"></a>Acción de obtención de detalles (generador de informes y SSRS)
  Si desea que los usuarios puedan ocultar y mostrar elementos de forma interactiva, incluya iconos más y menos en un cuadro de texto. Esto se denomina acción *de obtención de detalles* . En una tabla o matriz, puede mostrar u ocultar filas y columnas estáticas, o filas y columnas que están asociadas a grupos.  
  
 ![rs_drilldown](../media/rs-drilldown.gif "rs_drilldown")  
  
 En esta ilustración, el usuario hace clic en los signos más (+) del informe para mostrar datos detallados.  
  
 Por ejemplo, en una tabla con grupos de filas puede ocultar inicialmente todas las filas excepto la fila de resumen del grupo externo. Para cada grupo interno (incluido el grupo de detalles), agregue un icono de expansión/contracción a la celda de agrupamiento del grupo contenedor. Cuando se representa el informe, el usuario puede hacer clic en el cuadro de texto para expandir y contraer los datos detallados. Para más información, vea [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md).  
  
 Para permitir a los usuarios expandir o contraer un elemento, debe establecer las propiedades de visibilidad del elemento.  
  
> [!NOTE]  
>  Cuando se crea un informe con una acción de obtención de detalles, la información de visibilidad debe establecerse para el grupo, la columna o la fila que se desee ocultar, no para un único cuadro de texto de la fila o de la columna. Además, el cuadro de texto que se use para el control de alternancia debe estar en un ámbito contenedor que controle el elemento que se desee mostrar u ocultar.  
>   
>  Por ejemplo, para ocultar una fila asociada a un grupo anidado, el cuadro de texto debe estar en una fila asociada con el grupo primario o uno superior en la jerarquía de inclusión.  
>   
>  Para más información sobre cómo configurar la información de visibilidad en el grupo, la columna o la fila, vea [Agregar una acción de expandir y contraer a un elemento &#40;Generador de informes y SSRS&#41;](add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md).  
  
 Para más información sobre cómo ocultar elementos de informes, vea [Ocultar un elemento &#40;Generador de informes y SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="comparing-drilldown-and-drillthrough-reports"></a>Comparar informes de obtención de detalles con informes detallados  
 En un informe de obtención de detalles, un usuario hace clic en un botón de más o menos para expandir o contraer una sección de un informe para mostrar los datos detallados. En un informe detallado, el usuario hace clic en un vínculo para obtener un valor de resumen y este abre un informe relacionado independiente con los datos detallados. Estos datos solo se recuperan al ejecutar el informe de detalles. Generalmente, los informes detallados requieren menos recursos que los informes de obtención de detalles. Para obtener más información, vea [Obtención de detalles, informes detallados, subinformes y regiones de datos anidadas &#40;Generador de informes y SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
## <a name="rendering-extension-support-for-hidden-report-items"></a>Compatibilidad con extensiones de representación para elementos de informe ocultos  
 La alternancia mostrar u ocultar en los elementos de informe solo es compatible con las extensiones de representación que admiten la interactividad del usuario como, por ejemplo, la extensión de representación en HTML que se utiliza cuando se ejecuta un informe en el Generador de informes o en el Administrador de informes. Otras extensiones de representación muestran elementos ocultos. En la lista siguiente se describe la compatibilidad para los elementos de informe con visibilidad condicional:  
  
-   En HTML, si los elementos están ocultos, no estarán visibles en el código fuente HTML.  
  
-   La extensión de representación en XML muestra todos los elementos de informe, independientemente de si están ocultos o no.  
  
-   La extensión de representación en Excel muestra y expande filas y columnas ocultas en una tabla, matriz o lista. Todas las filas y columnas están visibles.  
  
 Para más información, vea [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Obtención de detalles, informes detallados, subinformes y regiones de datos anidadas &#40;Generador de informes y SSRS&#41;](drillthrough-drilldown-subreports-and-nested-data-regions.md)   
 [Ordenación interactiva, mapas de documento y vínculos &#40;Generador de informes y SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
