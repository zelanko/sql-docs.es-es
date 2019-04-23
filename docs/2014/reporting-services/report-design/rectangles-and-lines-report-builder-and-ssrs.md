---
title: Rectángulos y líneas (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d6226b0c-0398-4185-8565-96099876fc21
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d0933593220b73b8d57d76645ebea05d733e5661
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59966241"
---
# <a name="rectangles-and-lines-report-builder-and-ssrs"></a>Rectángulos y líneas (Generador de informes y SSRS)
  Los rectángulos y las líneas pueden crear efectos visuales en un informe. Puede configurar las propiedades de presentación de estos elementos de informe desde la sección Borde de la pestaña Inicio, así como configurar otras propiedades utilizando el panel Propiedades. Puede agregar a un rectángulo características como un color o una imagen de fondo, una información sobre herramientas o un marcador.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RectanglesLinesReportParts"></a> Rectángulos y líneas como elementos de informe  
 Puede publicar rectángulos con los elementos que contienen por separado del informe como elementos de informe. [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
 No puede publicar los elementos de informe contenidos en el rectángulo como elementos de informe. Cuando los usuarios agregan el rectángulo a un informe, obtienen el rectángulo y los elementos que contiene.  
  

  
##  <a name="RectangleAsContainer"></a> Usar un rectángulo como contenedor  
 Puede usar un rectángulo como contenedor de otros elementos. Cuando se mueve un rectángulo, los elementos que contiene se mueven con él. Un elemento del rectángulo muestra el nombre del rectángulo en su propiedad **Parent** . Para más información sobre el uso de un rectángulo como contenedor, vea [Agregar un rectángulo o un contenedor &#40;Generador de informes y SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md) y [Mostrar los mismos datos en una matriz y en un gráfico &#40;Generador de informes&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).  
  
> [!NOTE]  
>  Un rectángulo es solamente un contenedor para los elementos que crea en el rectángulo o que arrastra hasta él. Si dibuja un rectángulo alrededor de un elemento que ya existe en la superficie de diseño, el rectángulo no actuará como su contenedor. El rectángulo no aparecerá enumerado en la propiedad Parent del elemento.  
  
 Cuando utilice rectángulos para contener elementos de informe, valore cómo se verán afectados los elementos en conjunto durante la representación de un informe. Los elementos de informe que contienen filas de datos repetidas (por ejemplo, tablas) se expandirán para alojar los datos devueltos por una consulta. Esto afectará a la ubicación de otros elementos dentro del rectángulo. Una tabla desplazará los elementos hacia abajo si están ubicados debajo de la región de datos. Para fijarlos en su sitio, se puede incluir el elemento de informe en un rectángulo cuyo borde superior esté por encima del borde inferior de la tabla. Para más información, vea [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md).  
  

  
##  <a name="ReportBorder"></a> Agregar un borde al informe  
 Puede agregar un borde a un informe agregando bordes a los encabezados, pies de página y cuerpo del informe, sin tener que agregar líneas o rectángulos. Para más información, vea [Agregar un borde a un informe &#40;Generador de informes y SSRS&#41;](add-a-border-to-a-report-report-builder-and-ssrs.md).  
  

  
##  <a name="HowTo"></a> Temas de procedimientos  
 [Agregar un borde a un informe &#40;Generador de informes y SSRS&#41;](add-a-border-to-a-report-report-builder-and-ssrs.md)  
  
 [Agregar un rectángulo o un contenedor &#40;Generador de informes y SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
 [Agregar y modificar una línea &#40;Generador de informes y SSRS&#41;](add-and-modify-a-line-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vea también  
 [Agregar un rectángulo o un contenedor &#40;Generador de informes y SSRS&#41;](add-a-rectangle-or-container-report-builder-and-ssrs.md)  
  
  
