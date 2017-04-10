---
title: "Agregar un rect&#225;ngulo o un contenedor (Generador de informes y SSRS) | Microsoft Docs"
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
f1_keywords: 
  - "10061"
  - "sql13.rtp.rptdesigner.rectangleproperties.general.f1"
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 9
---
# Agregar un rect&#225;ngulo o un contenedor (Generador de informes y SSRS)
  Agregue un rectángulo a un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] si quiere incluir en él un elemento gráfico para separar distintas áreas, resaltarlas o proporcionar un fondo para uno o más elementos de informe. Los rectángulos también se usan como contenedores para ayudar a controlar la manera en la que se representan las regiones de datos en un informe. Puede personalizar la apariencia de un rectángulo editando sus propiedades, como los colores del borde y de segundo plano. Para más información sobre el uso de un rectángulo como contenedor, vea [Rectángulos y líneas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md) y [Mostrar los mismos datos en una matriz y en un gráfico &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).    
   
## Para agregar un rectángulo    
    
1.  En la pestaña **Insertar** , en el grupo **Elementos de informe** , haga clic en **Rectángulo.**    
    
2.  En la superficie de diseño, haga clic en la ubicación en la que desea que se encuentre la esquina superior izquierda del rectángulo y arrástrelo hasta donde desee que esté la esquina inferior derecha.    
    
     Tenga en cuenta que cuando mueve el cursor, da la impresión de que el cursor se alinea con otros objetos de la superficie de diseño. Esto le será de ayuda si desea que los objetos estén alineados.    
    
## Para crear un contenedor    
    
1.  Agregue un elemento de rectángulo al informe.    
    
2.  Arrastre otros elementos de informe al rectángulo.    
    
    > [!NOTE]    
    >  Un rectángulo es solamente un contenedor para los elementos que crea en el rectángulo o que arrastra hasta él. Si dibuja un rectángulo alrededor de un elemento que ya existe en la superficie de diseño, el rectángulo no actuará como su contenedor.    
    
## Para cambiar propiedades de rectángulo como color, estilo o peso    
    
1.  Seleccione el rectángulo y, a continuación, haga clic en las opciones de color de línea, estilo o peso en la sección **Borde** de la pestaña Inicio.    
    
2.  Haga clic en la flecha situada al lado del botón **Borde** para determinar qué lados del rectángulo va a cambiar.    
    
    > [!NOTE]    
    >  Si establece el estilo de línea en **Doble** y el ancho de línea es de punto y medio o inferior, es posible que la línea no aparezca como doble cuando ejecute el informe en el Generador de informes, el Diseñador de informes o en el portal web de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]. Aparecerá como doble cuando exporte el informe a otros formatos, como Microsoft Word y Acrobat PDF.    
    
## Vea también    
 [Rectángulos y líneas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)     
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)    
    
  