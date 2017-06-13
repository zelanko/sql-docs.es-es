---
title: "Funcionalidad interactiva - diferentes extensiones de representación de informes | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f0bd1c4c-e8b5-467f-b5a1-541f19c7e3e2
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 9a422c1619ae284ec49643465bd8b84efda1910b
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="interactive-functionality---different-report-rendering-extensions"></a>Funcionalidad interactiva - diferentes extensiones de representación de informes
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona características para interactuar con un informe paginado en tiempo de ejecución. No todos los formatos de representación de informes son compatibles con todas las características interactivas. Use la tabla siguiente para comprender el funcionamiento de las características interactivas en los diferentes formatos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="interactive-features-in-different-output-formats"></a>Características interactivas en diferentes formatos de salida  
 Los informes paginados que se representan en el formato de salida XML, CSV o Imagen no admiten características interactivas.  
  
 Los informes que se ven en el portal web de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , en los elementos web de SharePoint o en un explorador se representan en HTML. HTML y Windows Forms son los únicos formatos de salida de informes que admiten todas las características interactivas. Otros formatos HTML alternativos (como MHTML) admiten muchas características interactivas. En la siguiente tabla también se incluyen las excepciones que puedan existir para el formato MHTML.  
  
### <a name="document-maps"></a>Mapas de documento  
  
|Opción de exportación|Información complementaria|  
|-------------------|-------------------------|  
|Vista previa/Visor de informes, HTML|El mapa del documento interactivo ofrece un panel de navegación de vínculos jerárquicos que pueden utilizarse para navegar a distintas secciones del informe.|  
|PDF|PDF representa un mapa del documento como el panel Marcadores. Todos los elementos del mapa del documento se enumeran uno detrás de otro en el panel. Incluye una jerarquía de vínculos. Si se especifica un intervalo de páginas, solo aparecen en la jerarquía los marcadores representados.|  
|Excel|Excel representa un mapa del documento como la primera hoja de cálculo del libro. Incluye una jerarquía de vínculos. Cuando se hace clic en el vínculo del mapa del documento, se abre la celda de destino adecuada en la hoja de cálculo correspondiente.|  
|Word|Word representa el mapa del documento como etiquetas de la Tabla de contenido.|  
|Otros (por ejemplo, TIFF, XML y CSV)|No disponible en MHTML, XML, CSV ni Image.|  
  
### <a name="drillthrough-links-to-other-reports"></a>Vínculos de obtención de detalles a otros informes  
  
|Opción de exportación|Información complementaria|  
|-------------------|-------------------------|  
|Vista previa/Visor de informes, HTML|Los usuarios hacen clic en valores de datos del informe para ver los datos relacionados en otro informe.|  
|PDF|Los vínculos de obtención de detalles no están disponibles en PDF. Considere la posibilidad de utilizar hipervínculos para informes en PDF que se vinculan a otras páginas.|  
|Excel|Los vínculos de obtención de detalles se representan en Excel.<br /><br /> El vínculo se convierte en un hipervínculo que apunta al informe al que hace referencia el vínculo de obtención de detalles. Al hacer clic en el vínculo se abre un informe en una ventana del explorador.|  
|Word|Los vínculos de obtención de detalles se representan en Word.<br /><br /> El vínculo se convierte en un hipervínculo que apunta al informe al que hace referencia el vínculo de obtención de detalles. Al hacer clic en el vínculo se abre un informe en una ventana del explorador.|  
|Otro|No disponible en XML, CSV ni Image.|  
  
### <a name="toggle-items-within-a-report"></a>Alternar elementos dentro de un informe  
  
|Opción de exportación|Información complementaria|  
|-------------------|-------------------------|  
|Vista previa/Visor de informes, HTML|Los usuarios hacen clic en iconos de expansión y contracción para ver las secciones de un informe.|  
|PDF|El servidor de informes exporta el estado de mostrar u ocultar actual del informe a formato PDF. No se admite la alternancia interactiva.|  
|Excel|Los vínculos y los elementos de obtención de detalles que pueden alternarse se representan como esquemas contraíbles en Excel. Excel permite expandir y contraer secciones del informe. Para más información sobre las limitaciones impuestas por Excel, vea [Exportar a Microsoft Excel &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md).|  
|Word|El servidor de informes exporta el estado de mostrar u ocultar actual del informe a formato PDF. No se admite la alternancia interactiva.|  
|Otro|No disponible en MHTML, XML ni CSV. Al exportar a un formato Imagen, el servidor de informes exporta el estado de mostrar u ocultar actual del informe al formato PDF. No se admite la alternancia interactiva.|  
  
### <a name="interactive-sorting"></a>Ordenar de manera interactiva  
  
|Opción de exportación|Información complementaria|  
|-------------------|-------------------------|  
|Vista previa/Visor de informes, HTML|En los informes tabulares, el usuario hace clic en las flechas de ordenación de una columna para cambiar la forma de ordenar los datos.|  
|PDF|No disponible en PDF.|  
|Excel|No disponible en Excel.|  
|Word|No disponible en Word.|  
|Otro|No disponible en MHTML, XML, CSV ni Image.|  
  
### <a name="hyperlinks-to-external-web-content-or-images"></a>Hipervínculos a imágenes o contenido web de tipo externo  
  
|Opción de exportación|Información complementaria|  
|-------------------|-------------------------|  
|Vista previa/Visor de informes, HTML|Los usuarios hacen clic en vínculos para abrir páginas web externas en una nueva ventana del explorador.|  
|PDF|Los hipervínculos se representan mediante la extensión de representación en PDF. Cuando un usuario hace clic en un hipervínculo, se abren las páginas vinculadas en el explorador.|  
|Excel|Los hipervínculos se representan en Excel.|  
|Word|Los hipervínculos se representan en Word.|  
|Otro|Los hipervínculos no están disponibles en MHTML, XML, CSV ni Image.<br /><br /> En MHTML e Imagen, las imágenes externas se representan de forma estática.|  
  
### <a name="bookmark-or-anchor"></a>Marcador o delimitador  
  
|Opción de exportación|Información complementaria|  
|-------------------|-------------------------|  
|Vista previa/Visor de informes, HTML|Los usuarios hacen clic en vínculos para navegar a otra sección del mismo informe.|  
|PDF|No disponible en PDF.|  
|Excel|Los marcadores se representan en Excel.<br /><br /> El marcador se convierte en un hipervínculo que apunta al nombre del elemento de informe.|  
|Word|Los marcadores se representan en Word.<br /><br /> El marcador se convierte en un hipervínculo que apunta al elemento de informe marcado. Al exportar el informe, solo se convierten 40 caracteres de los nombres de los marcadores o los delimitadores, lo que puede generar nombres de marcadores o de delimitadores duplicados. Los espacios se convierten en caracteres de subrayado (_).|  
|Otro|No disponible en XML, CSV ni Image.|  
  
### <a name="prompted-parameters-obtained-at-run-time"></a>Parámetros solicitados obtenidos en tiempo de ejecución  
  
|Opción de exportación|Información complementaria|  
|-------------------|-------------------------|  
|Vista previa/Visor de informes, HTML|En la parte superior del informe, aparece un área de entrada de parámetros. Esta área es parte del Visor HTML que se utiliza para mostrar informes en un explorador.|  
|PDF|El servidor de informes exporta el informe a PDF utilizando los valores de parámetros que están activos para el informe.|  
|Excel|El servidor de informes exporta el informe a Excel utilizando los valores de parámetros que están activos para el informe.|  
|Word|El servidor de informes exporta el informe a Word usando los valores de los parámetros que están activos para el informe.|  
|Otro|El servidor de informes exporta el informe a otros formatos utilizando los valores de parámetros que están activos para el informe.|  
  
### <a name="filters-applied-at-run-time"></a>Filtros aplicados en tiempo de ejecución  
  
|Opción de exportación|Información complementaria|  
|-------------------|-------------------------|  
|Vista previa/Visor de informes, HTML|Los datos filtrados se muestran al usuario en tiempo de ejecución.|  
|PDF|El servidor de informes exporta el informe a PDF utilizando los datos filtrados en el informe actual.|  
|Excel|El servidor de informes exporta el informe a Excel utilizando los datos filtrados en el informe actual.|  
|Word|El servidor de informes exporta el informe a Word utilizando los datos filtrados en el informe actual.|  
|Otro|El servidor de informes exporta el informe a otros formatos utilizando los datos filtrados en el informe actual.|  
  
## <a name="see-also"></a>Vea también  
 [Exportación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Ordenación interactiva, mapas de documento y vínculos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
    
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Gráficos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)  
  
  

