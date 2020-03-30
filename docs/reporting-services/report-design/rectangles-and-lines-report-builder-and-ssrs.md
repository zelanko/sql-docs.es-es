---
title: Rectángulos y líneas (Generador de informes) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d6226b0c-0398-4185-8565-96099876fc21
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8d4448fba4e9faf1c3d51bb6233723385d111230
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082341"
---
# <a name="rectangles-and-lines-report-builder-and-ssrs"></a>Rectángulos y líneas (Generador de informes y SSRS)
  Los rectángulos y las líneas pueden crear efectos visuales en un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . Puede configurar las propiedades de presentación de estos elementos de informe desde la sección Borde de la pestaña Inicio, así como configurar otras propiedades en el panel Propiedades. Puede agregar a un rectángulo características como un color o una imagen de fondo, una información sobre herramientas o un marcador.  
  
##  <a name="rectangles-and-lines-as-report-parts"></a><a name="RectanglesLinesReportParts"></a> Rectángulos y líneas como elementos de informe  
 Puede publicar rectángulos con los elementos que contienen por separado del informe como elementos de informe. Los elementos de informe son elementos de informe independientes que se almacenan en el servidor de informes y se pueden incluir en otros informes.  
  
 No puede publicar los elementos de informe contenidos en un rectángulo como elementos de informe. Cuando los usuarios agregan el rectángulo a un informe, obtienen el rectángulo y los elementos que contiene.  Para más información, vea [Elementos de informe](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
##  <a name="using-a-rectangle-as-a-container"></a><a name="RectangleAsContainer"></a> Usar un rectángulo como contenedor  
 Puede usar un rectángulo como contenedor de otros elementos. Cuando se mueve un rectángulo, los elementos que contiene se mueven con él. Un elemento del rectángulo muestra el nombre del rectángulo en su propiedad **Parent** . Para más información sobre el uso de un rectángulo como contenedor, vea [Agregar un rectángulo o un contenedor &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md) y [Mostrar los mismos datos en una matriz y en un gráfico &#40;Generador de informes&#41;](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).  
  
> [!NOTE]  
>  Un rectángulo es solamente un contenedor para los elementos que crea en el rectángulo o que arrastra hasta él. Si dibuja un rectángulo alrededor de un elemento que ya existe en la superficie de diseño, el rectángulo no actuará como su contenedor. El rectángulo no aparecerá enumerado en la propiedad Parent del elemento.  
  
 Cuando utilice rectángulos para contener elementos de informe, valore cómo se verán afectados los elementos en conjunto durante la representación de un informe. Los elementos de informe que contienen filas de datos repetidas (por ejemplo, tablas) se expandirán para alojar los datos devueltos por una consulta. Esto afectará a la ubicación de otros elementos dentro del rectángulo. Una tabla desplazará los elementos hacia abajo si están ubicados debajo de la región de datos. Para fijarlos en su sitio, se puede incluir el elemento de informe en un rectángulo cuyo borde superior esté por encima del borde inferior de la tabla. Para más información, vea [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
##  <a name="adding-a-report-border"></a><a name="ReportBorder"></a> Agregar un borde al informe  
 Puede agregar un borde a un informe agregando bordes a los encabezados, pies de página y cuerpo del informe, sin tener que agregar líneas o rectángulos. Para más información, vea [Agregar un borde a un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md).  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a> Temas de procedimientos  
 [Agregar un borde a un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-border-to-a-report-report-builder-and-ssrs.md)  
  
 [Agregar un rectángulo o un contenedor &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
 [Agregar y modificar una línea &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-and-modify-a-line-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Consulte también  
 [Agregar un rectángulo o un contenedor &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
  
