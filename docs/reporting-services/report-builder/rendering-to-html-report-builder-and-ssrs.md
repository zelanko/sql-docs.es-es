---
title: Representar en HTML (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: cf559b0a-499a-4d74-b520-b382b87e0b17
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bd2ef58b56e1f73d7c86338d042ad8b34b50cc8a
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43267193"
---
# <a name="rendering-to-html-report-builder-and-ssrs"></a>Representar en HTML (Generador de informes y SSRS)
  La extensión de representación en HTML representa un informe paginado en formato HTML. La extensión de representación también puede generar páginas HTML completas o fragmentos de HTML para incrustarlos en otras páginas HTML. Todos los HTML se generan con la codificación UTF-8.  

 La extensión de representación en HTML es la predeterminada para los informes que se visualizan en un explorador, lo que incluye cuando se ejecutan en el portal web de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] . La extensión de representación en HTML puede representar HTML como un fragmento o como un documento HTML completo. Si el HTML es un fragmento, se quitan las etiquetas **HEAD**, **HTML**y **BODY** del documento HTML. Solo se representa el contenido de la etiqueta **BODY** . Esto resulta de gran utilidad para incrustar el HTML en HTML generado en otra aplicación.  
  
 En algunos escenarios, los parámetros de informe se pueden utilizar para iniciar ataques de inserción de script al representar los informes en HTML. Para obtener más información sobre cómo proteger informes, vea [Proteger informes y recursos](../../reporting-services/security/secure-reports-and-resources.md).  
  
 Para más información sobre exploradores, vea [Compatibilidad del explorador de Reporting Services y Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RenderingMHTML"></a> Representación en MHTML  
 La extensión de representación en HTML también puede representar informes en MHTML (Encapsulación MIME de documentos HTML agregados). MHTML extiende HTML para incrustar objetos codificados, como imágenes, en el documento HTML. Con la extensión de representación en MHTML, puede incrustar en un único archivo recursos tales como imágenes, documentos u otros archivos binarios como estructuras MIME incluidas en el informe HTML. Los informes MHTML también resultan útiles para incrustarlos en mensajes de correo electrónico porque todos los recursos se incluyen en el informe. Aunque la extensión de representación en HTML es la que en realidad representa el MHTML, esta funcionalidad también se denomina extensión de representación en MHTML.  
  
  
##  <a name="BrowserSupport"></a> Compatibilidad con exploradores  
 Esta extensión de representación admite las versiones siguientes de los exploradores:  
  
-   Internet Explorer 5.5 y versiones posteriores  
  
-   Firefox 1.5 y versiones posteriores  
  
-   Safari 3.0 y versiones posteriores  
  
 Debido a los distintos comportamientos de los exploradores, el informe representado puede variar ligeramente de un explorador a otro. Por ejemplo, el cuadro de texto contiene una propiedad denominada WritingMode. Esta propiedad no es compatible con Firefox.  
  
  
##  <a name="HTMLSpecificRenderingRules"></a> Reglas de representación específicas de HTML  
 Durante la representación se aplican las siguientes reglas específicas de HTML:  
  
-   El representador genera una estructura de tabla HTML en la que se alojarán todos los elementos existentes en cada colección **ReportItems** , si hubiera más de uno.  
  
-   Cada elemento de la estructura de tabla ocupa una única celda.  
  
-   Las celdas vacías se contraen tanto como es posible para reducir el tamaño del HTML.  
  
-   Para mejorar la velocidad a la que los exploradores pueden representar la tabla, se agrega una fila de celdas vacías en el borde superior y una columna en el borde izquierdo.  
  
-   La filas o las columnas de la tabla que no contienen elementos, tan solo espacios entre los elementos, adoptan anchos y altos fijos.  
  
-   Las demás filas y columnas pueden aumentar en función del tamaño de cada elemento de informe.  
  
-   Todas las coordenadas y los tamaños de los elementos de informe se convierten a milímetros. Todos los demás tamaños, incluidas las propiedades de estilo, conservan sus unidades originales. Cuando la diferencia entre el tamaño y la posición es inferior a 0,2 mm se trata como si fuera 0 mm.  
  
  
##  <a name="Interactivity"></a> Interactividad  
 Algunos elementos interactivos se admiten en HTML. A continuación se describen sus comportamientos específicos.  
  
### <a name="show-and-hide"></a>Mostrar u ocultar  
 Un elemento de informe cuya visibilidad se puede alternar se representa con la imagen de alternancia +/- en la que se puede hacer clic. Cuando se hace clic en el elemento, se vuelve a realizar una llamada al servidor para que vuelva a representar la salida con el estado de mostrar u ocultar cambiado.  
  
### <a name="document-map"></a>Mapa del documento  
 Para representar y navegar por las etiquetas de mapa de documento, use el mapa del documento del control de visor. Para los encabezados de región de datos omitidos, las etiquetas se representan en la primera celda secundaria. Si no hay ninguna celda secundaria, la etiqueta se representa en el elemento secundario que la precede.  
  
### <a name="bookmarks"></a>Marcadores  
 Los vínculos de marcador se representan y aparecen como hipervínculos. Para representar y navegar por los destinos de marcador, debe hacer clic en los vínculos de marcador. Cuando se hace clic en un vínculo de marcador, el informe va a la primera repetición de la etiqueta del marcador de destino y, si es posible, el explorador se desplaza para que el vínculo de marcador aparezca en la parte superior de la ventana. Las etiquetas de delimitador HTML (\<a>) se usan para marcar destinos de marcador.  
  
### <a name="interactive-sorting"></a>Ordenación interactiva  
 Si un cuadro de texto tiene definida la ordenación de usuario, la extensión de representación en HTML representa los iconos de ordenación en el cuadro de texto situado a la derecha de su contenido. Si un informe contiene cualquier cuadro de texto con la ordenación de usuario definida, se representa JavaScript que provoca una devolución de datos al servidor cuando se hace clic en la imagen de ordenación.  
  
### <a name="hyperlinks-and-drillthrough"></a>Hipervínculos y obtención de detalles  
 Los hipervínculos y los vínculos de obtención de detalles se representan como hipervínculos en los elementos de informe que usan las etiquetas de delimitador HTML (\<a>) alrededor del elemento en el que están definidas.  
  
### <a name="search"></a>Buscar  
 La característica Buscar permite a los usuarios buscar una cadena de texto dentro del informe.  
  
 El control ReportViewer de formularios Web Forms proporciona funcionalidad adicional de búsqueda.  
  
  
##  <a name="DeviceInfo"></a> Configuración de la información del dispositivo  
 Para cambiar algunos valores de configuración predeterminados para este representador, incluido el modo de representación, solo tiene que cambiar la configuración de la información del dispositivo. Para más información, consulte [HTML Device Information Settings](../../reporting-services/html-device-information-settings.md).  
  
  
## <a name="see-also"></a>Ver también  
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Representar elementos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
