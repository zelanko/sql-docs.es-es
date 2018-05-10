---
title: Representación y diseño de páginas (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e2358653-35bc-4496-810a-d3ccf02f229f
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0a86b6298699730dcac81f9309acb856997ec80b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="page-layout-and-rendering-report-builder-and-ssrs"></a>Representación y diseño de páginas (Generador de informes y SSRS)
Obtenga información sobre las extensiones de representación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para los informes paginados, de forma que esté seguro de que su informe tiene el aspecto que quiere, incluidos el diseño y los saltos de página, y el tamaño del papel. 

 Al ver los informes en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o en el panel de vista previa del Generador de informes o del Diseñador de informes, el informe se representa primero mediante el representador de HTML. Después, puede exportar el informe a formatos diferentes, por ejemplo a Excel o a un archivo delimitado por comas (CSV). El informe exportado se puede usar entonces para realizar un análisis más extenso en Excel o como un origen de datos para las aplicaciones que pueden importar y usar archivos CSV.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye un conjunto de representadores para exportar los informes a diferentes formatos. Cada representador aplica reglas al representar los informes. Al exportar un informe a un formato de archivo diferente, sobre todo en el caso de representadores como el de Adobe Acrobat (PDF) que usa una paginación basada en el tamaño de página físico, puede que tenga que cambiar el diseño del informe para hacer que la apariencia y la impresión del informe exportado sean correctas una vez aplicadas las reglas de representación.  
  
 Para conseguir los mejores resultados con los informes exportados suele ser necesario un proceso reiterativo; se crea un informe en el Generador de informes o en el Diseñador de informes y se obtiene una vista previa del mismo, se exporta al formato preferido, se revisa el informe exportado y, a continuación, se realizan cambios en él.  
    
##  <a name="PageLayout"></a> Elementos de informe  
 Los elementos de informe son elementos de diseño que están asociados a distintos tipos de datos de informe. 
 
* Tabla, matriz, lista, gráfico y medidor son elementos de informe de la región de datos, cada uno de los cuales establece un vínculo a un conjunto de datos de informe. Cuando se procesa el informe, la región de datos se expande a lo ancho y hacia abajo por la página del informe para mostrar datos. 

Otros elementos de informe establecen un vínculo a un solo elemento y lo muestran. 
* Un elemento de informe **Imagen** establece un vínculo a una imagen. 
* Un elemento de informe **Cuadro de texto** contiene texto simple como un título o una expresión que puede incluir referencias a campos integrados, parámetros de informe o campos del conjunto de datos. 
* Los elementos de informe **Línea** y **Rectángulo** proporcionan elementos gráficos simples en la página de informe. El **Rectángulo** también puede ser un contenedor para otros elementos de informe. 

Un informe también puede contener subinformes.  
  
## <a name="page-layout"></a>Diseño de página

 Con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede colocar elementos de informe en cualquier parte de la superficie de diseño. Puede colocar y ampliar o reducir interactivamente la forma inicial del elemento de informe usando las líneas de ajuste y cambiando los controladores de tamaño. Puede colocar regiones de datos con conjuntos de datos distintos o incluso los mismos datos en formatos diferentes, uno al lado de otro. Cuando se coloca un elemento de informe en la superficie de diseño, tiene un tamaño y una forma predeterminados y una relación inicial con todos los demás elementos de informe. 
 
 Puede colocar elementos de informe en otros para crear diseños de informe más complejos. Por ejemplo, gráficos o imágenes en celdas de tabla, tablas en celdas de tabla, y varias imágenes en un rectángulo. Además de proporcionar al informe la organización y la apariencia deseadas, la colocación de elementos de informe en contenedores tales como rectángulos ayuda a controlar la forma en que los elementos de informe se muestran en la página del informe.  
  
 Un informe puede abarcar varias páginas, e incluir un encabezado y un pie de página que se repiten en cada página. También puede contener elementos gráficos como imágenes y líneas, y puede contener fuentes, colores y estilos diversos, que pueden estar basados en expresiones.  
  
##  <a name="ReportSections"></a> Secciones del informe  
 Un informe consta de tres secciones principales: un encabezado de *página* opcional, un pie de *página* opcional y un cuerpo del informe. El encabezado y el pie de página del *informe* no son secciones independientes del informe, sino que se componen de los elementos de informe que se colocan en la parte superior y en la parte inferior del cuerpo del informe. El encabezado y el pie de página repiten el mismo contenido en la parte superior e inferior de cada página del informe. Puede situar imágenes, cuadros de texto y líneas en los encabezados y pies de página. Puede colocar cualquier tipo de elemento de informe en el cuerpo del informe.  
  
 Se pueden establecer las propiedades de los elementos de informe para que los oculten o los muestren inicialmente en la página. Puede establecer las propiedades de visibilidad de filas, columnas o grupos para las regiones de datos y proporcionar botones de alternancia para permitir al usuario mostrar u ocultar interactivamente datos del informe. Puede establecer la visibilidad o la visibilidad inicial usando expresiones, incluso expresiones basadas en parámetros de informe.  
  
 Cuando se procesa un informe, los datos del informe se combinan con los elementos de diseño del informe y los datos combinados se envían a un representador de informes. El representador sigue las reglas predefinidas para la expansión de los elementos de informe y determina la cantidad de datos que caben en cada página. Para diseñar un informe que resulte fácil de leer y que esté optimizado para el representador que va a usar, debe comprender las reglas que se usan para controlar la paginación en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para más información, vea [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
##  <a name="RenderingExtensions"></a> Representadores  
 Reporting Services incluye un conjunto de representadores, denominados también extensiones de representación, que puede utilizar para exportar los informes a diferentes formatos. Hay tres tipos de representadores:  
  
-   **Representadores de datos** : los representadores de datos quitan todo el formato e información de diseño del informe y muestran solo los datos. El archivo resultante se puede usar para importar los datos del informe sin formato en otro tipo de archivo, como Excel; en otra base de datos; en un mensaje de datos XML o en una aplicación personalizada. Los datos disponibles se representan como CSV y XML.  
  
    > [!NOTE]  
    >  Aunque no permite la exportación directa a un formato diferente, la representación de Atom genera los archivos de datos de los informes.  
  
-   **Representadores de saltos de página automáticos** Los representadores de saltos de página automáticos mantienen el diseño y el formato de los informes. El archivo resultante se optimiza para la visualización y la entrega basada en la presentación en pantalla, como en una página web. Los representadores de saltos de página automáticos disponibles son los siguientes: [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word, MHTML (archivo web) y HTML.  
  
-   **Representadores de saltos de página manuales** Los representadores de saltos de página manuales mantienen el diseño y el formato de los informes. El archivo resultante se optimiza para que su aspecto no varíe al imprimirlo o para ver el informe en pantalla con formato de libro. Los representadores de saltos de página manuales disponibles son TIFF y PDF.  
  
 Cuando se obtiene una vista previa de un informe en el Generador de informes o el Diseñador de informes o se ejecuta un informe en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , siempre se representa primero en HTML. Después de ejecutar el informe, puede exportarlo a otros formatos de archivo. Para más información, vea [Exportación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md).  
  
##  <a name="RenderingBehaviors"></a> Comportamiento de la representación  
 En función del representador que seleccione, se aplican ciertas reglas al representar el informe. La forma en la que los elementos de informe se ajustan en una página viene determinada por la combinación de estos factores:  
  
-   Reglas de representación.  
-   El ancho y alto de los elementos de informe.  
-   El tamaño del cuerpo del informe.  
-   El ancho y alto de la página.  
-   La compatibilidad específica del representador con la paginación.  
  
 Por ejemplo, los informes representados con los formatos HTML y MHTML están optimizados para una visualización en pantalla en la que las páginas pueden tener distintas longitudes.  
  
 Para más información, vea [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md).  
   
##  <a name="Pagination"></a> Paginación  
 La paginación hace referencia al número de páginas de un informe y al modo en que los elementos de informe se organizan en dichas páginas. La paginación en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] varía en función de la extensión de representación usada para ver y entregar el informe, y de las opciones para mantener juntos los elementos del informe y de salto de página que configure para usar en él.  
  
 Para diseñar correctamente un informe que resulte fácil de leer y que esté optimizado para el representador que va a usar para su entrega, es preciso que comprenda las reglas que se usan para controlar la paginación en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Los informes que se exportan al usar las extensiones de representación de **páginas automáticas** y **datos** normalmente no se ven afectados por la paginación. Al utilizar una extensión de representación de datos, el informe se representa como un conjunto de filas tabular en formato XML o CSV. Para asegurarse de que los datos del informe exportado son utilizables, debería conocer las reglas que se aplican a la representación de un conjunto de filas tabulares planas de un informe.  
  
 Si se usa una extensión de representación de **páginas automáticas** como la extensión de representación de HTML, puede ser aconsejable saber cómo aparece impreso el informe y también si se representa bien con un procesador de páginas automático como PDF. Durante la creación o actualización de un informe, puede obtener una vista previa del mismo y exportarlo en el Generador de informes y el Diseñador de informes.  
  
 Los procesadores de saltos de**página manuales** son los que más afectan al diseño del informe y al tamaño físico de página. Para más información, vea [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
   
##  <a name="HowTo"></a> Temas de procedimientos  
 En esta sección se enumeran procedimientos que muestran, paso a paso, cómo trabajar con la paginación en los informes.  
  
-   [Agregar un salto de página &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-a-page-break-report-builder-and-ssrs.md)  
  
-   [Mostrar encabezados de fila y de columna en varias páginas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/display-row-and-column-headers-on-multiple-pages-report-builder-and-ssrs.md)  
  
-   [Agregar o quitar un encabezado o un pie de página &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-or-remove-a-page-header-or-footer-report-builder-and-ssrs.md)  
  
-   [Mantener visibles los encabezados al desplazarse a través de un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/keep-headers-visible-when-scrolling-through-a-report-report-builder-and-ssrs.md)  
  
-   [Mostrar números de página u otras propiedades del informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/display-page-numbers-or-other-report-properties-report-builder-and-ssrs.md)  
  
-   [Ocultar un encabezado o un pie de página en la primera o en la última página &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/hide-a-page-header-or-footer-on-the-first-or-last-page-report-builder-and-ssrs.md)  
  
##  <a name="InThisSection"></a> En esta sección  
 En los temas siguientes se proporciona información adicional sobre el diseño y la representación de páginas.  
  
 [Encabezados y pies de página &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)  
 Proporciona información sobre cómo utilizar encabezados y pies de página en informes, y cómo controlar la paginación al usarlos.  
  
 [Controlar saltos de página, encabezados, columnas y filas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)  
 Proporciona información sobre cómo utilizar saltos de página.  
  
## <a name="see-also"></a>Ver también  
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Exportación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
