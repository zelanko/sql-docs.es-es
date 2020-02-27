---
title: Adición de un rectángulo o un contenedor (Generador de informes) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10061"
- sql13.rtp.rptdesigner.rectangleproperties.general.f1
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fc7cba2147dbcc781a5764173bbd09699ab74385
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "77080691"
---
# <a name="add-a-rectangle-or-container-report-builder-and-ssrs"></a>Agregar un rectángulo o un contenedor (Generador de informes y SSRS)
  Agregue un rectángulo a un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] si quiere incluir en él un elemento gráfico para separar distintas áreas, resaltarlas o proporcionar un fondo para uno o más elementos de informe. Los rectángulos también se usan como contenedores para ayudar a controlar la manera en la que se representan las regiones de datos en un informe. Puede personalizar la apariencia de un rectángulo editando sus propiedades, como los colores del borde y de segundo plano. Para más información sobre el uso de un rectángulo como contenedor, vea [Rectángulos y líneas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md) y [Mostrar los mismos datos en una matriz y en un gráfico &#40;Generador de informes&#41;](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).    
   
## <a name="to-add-a-rectangle"></a>Para agregar un rectángulo    
    
1.  En la pestaña **Insertar** , en el grupo **Elementos de informe** , haga clic en **Rectángulo.**    
    
2.  En la superficie de diseño, haga clic en la ubicación en la que desea que se encuentre la esquina superior izquierda del rectángulo y arrástrelo hasta donde desee que esté la esquina inferior derecha.    
    
     Tenga en cuenta que cuando mueve el cursor, da la impresión de que el cursor se alinea con otros objetos de la superficie de diseño. Esto le será de ayuda si desea que los objetos estén alineados.    
    
## <a name="to-create-a-container"></a>Para crear un contenedor    
    
1.  Agregue un elemento de rectángulo al informe.    
    
2.  Arrastre otros elementos de informe al rectángulo.    
    
    > [!NOTE]    
    >  Un rectángulo es solamente un contenedor para los elementos que crea en el rectángulo o que arrastra hasta él. Si dibuja un rectángulo alrededor de un elemento que ya existe en la superficie de diseño, el rectángulo no actuará como su contenedor.    
    
## <a name="to-change-rectangle-properties-such-as-color-style-or-weight"></a>Para cambiar propiedades de rectángulo como color, estilo o peso    
    
1.  Seleccione el rectángulo y, a continuación, haga clic en las opciones de color de línea, estilo o peso en la sección **Borde** de la pestaña Inicio.    
    
2.  Haga clic en la flecha situada al lado del botón **Borde** para determinar qué lados del rectángulo va a cambiar.    
    
    > [!NOTE]    
    >  Si establece el estilo de línea en **Doble** y el ancho de línea es de punto y medio o inferior, es posible que la línea no aparezca como doble cuando ejecute el informe en el Generador de informes, el Diseñador de informes o en el portal web de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . Aparecerá como doble cuando exporte el informe a otros formatos, como Microsoft Word y Acrobat PDF.    
    
## <a name="see-also"></a>Consulte también    
 [Rectángulos y líneas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)     
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)    
    
  
