---
title: Exportar a Microsoft Word (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 0cd8ae26-4682-4473-8f15-af084951defd
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0e040fe0b31f9cead8843987199164e45767db82
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224705"
---
# <a name="exporting-to-microsoft-word-report-builder-and-ssrs"></a>Exportar a Microsoft Word (Generador de informes y SSRS)
  La extensión de representación de Word representa informes en el formato nativo de [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010. El formato es Office Open XML.  
  
 El representador de Word es compatible con [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010, así como con [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 con el Paquete de compatibilidad de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office para Word, Excel y PowerPoint instalado. Para obtener más información sobre el Paquete de compatibilidad, vea [Paquete de compatibilidad de Microsoft Office para formatos de archivo de Word, Excel y PowerPoint](http://go.microsoft.com/fwlink/?LinkID=205622).  
  
 El tipo de contenido de los archivos generados por este representador es **application/vnd.openxmlformats-officedocument.wordprocessingml.document** y la extensión de los archivos es .docx.  
  
 El nombre de la versión anterior de la extensión de representación de Word, solo compatible con [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003, cambia a Word 2003. Solo la extensión de representación de Word está disponible de forma predeterminada. Debe actualizar los archivos de configuración de Reporting Services para que la extensión de representación de Word 2003 esté disponible. El tipo de contenido de los archivos generados por el representador de Word 2003 es **application/vnd.ms-word** y la extensión del nombre de los archivos es .doc.  
  
> [!IMPORTANT]  
>  El [!INCLUDE[ofprword](../../includes/ofprword-md.md)] extensión de representación 2003 está en desuso. Para obtener más información, consulte [características desusadas de SQL Server Reporting Services en SQL Server 2014](../deprecated-features-in-sql-server-reporting-services-ssrs.md).  
  
 Después de exportar el informe a un documento de Word, puede modificar su contenido y diseñar informes con estilo de documento, como etiquetas postales, pedidos de compra o circulares.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ReportItemsWord"></a> Elementos de informe en Word  
 Los informes exportados a Word aparecen como una tabla anidada que representa el cuerpo del informe. Una región de datos Tablix se representa como una tabla anidada que refleja la estructura de la región de datos en el informe. Los cuadros de texto y los rectángulos se representan como una celda de la tabla. El valor del cuadro de texto se muestra dentro de la celda.  
  
 Las imágenes, gráficos, barras de datos, minigráficos, mapas, indicadores y medidores se representan como una imagen estática dentro de una celda de la tabla. Los hipervínculos y los vínculos de obtención de detalles de estos elementos de informe también se representan. No se admiten los mapas interactivos y otras áreas en las que se puede hacer clic dentro de un gráfico.  
  
 Los informes con columnas de estilo boletín no se representan en Word. Las imágenes y los colores de fondo de página y del cuerpo del informe no se representan.  
  
##  <a name="Pagination"></a> Paginación  
 Cuando el informe se abre en Word, Word repagina de nuevo el informe completo basándose en el tamaño de página. La repaginación puede hacer que se inserten saltos de página en ubicaciones en las que no se pretendía agregarlos y, en algunos casos, puede hacer que el informe exportado tenga dos saltos de página seguidos en una fila o que se agreguen páginas en blanco. Puede intentar cambiar la paginación de Word ajustando los márgenes de página.  
  
 Este representador admite solamente saltos de página lógicos.  
  
### <a name="page-sizing"></a>Tamaño de página  
 Cuando se representa el informe, el alto y el ancho de página de Word se establecen mediante las propiedades RDL siguientes: alto y ancho del tamaño del papel, márgenes izquierdo y derecho de la página, y márgenes superior e inferior de la página.  
  
### <a name="page-width"></a>Ancho de página  
 Word admite hasta 22 pulgadas para el ancho de página. Si el informe tiene más de 22 pulgadas de ancho, el representador representará el informe, pero Word no mostrará el contenido del informe desde la vista Diseño de impresión o la vista de diseño de lectura. Para ver los datos, cambie a la vista Normal o a la vista Diseño web. En estas vistas, Word reduce la cantidad de espacio en blanco, lo que le permite ver más contenido del informe.  
  
 Cuando se representa, el informe crece a lo ancho tanto como se necesite, hasta 22 pulgadas, para mostrar el contenido. El ancho mínimo del informe se basa en la propiedad RDL Width del panel de propiedades.  
  
##  <a name="DocumentProperties"></a> Propiedades de documento  
 El representador de Word escribe los metadatos siguientes en el archivo DOCX.  
  
|Propiedades del elemento de informe|Descripción|  
|-------------------------------|-----------------|  
|Título del informe|Title|  
|Autor del informe|Autor|  
|Descripción del informe|Comentarios|  
  
##  <a name="ReportHeadersFooters"></a> Encabezados y pies de página  
 Los encabezados y pies de página se representan como regiones de encabezado y pie de página en Word. Si en el encabezado o en el pie de página aparece un número de página del informe o una expresión que indica el número total de páginas del informe, se convierten en un campo de Word para que se muestre el número de página correcto en el informe representado. Si se ha establecido el alto del encabezado o del pie de página en el informe, Word no puede admitir este valor. En algunas circunstancias, la propiedad PrintOnFirstPage puede especificar si el texto de un encabezado o un pie de página se imprime o no en la primera página de un informe. Si el informe representado tiene varias páginas y cada una de ellas contiene solo una sección, puede establecer el valor de PrintOnFirstPage en False y el texto se eliminará de la primera página; en caso contrario, el texto se imprimirá, independientemente del valor de la propiedad PrintOnFirstPage.  
  
 El representador de Word intenta analizar todas las expresiones de los encabezados y pies de página cuando los informes se exportan a Word. Muchos tipos de expresiones se analizan correctamente y aparecen los valores esperados en los encabezados y en los pies de página de todas las páginas del informe.  
  
 Sin embargo, cuando un encabezado o un pie de página contiene una expresión compleja que se evalúa en valores distintos en páginas diferentes de un informe, puede aparecer el mismo valor en todas las páginas del informe. En las dos expresiones siguientes, los números de página no se incrementan en el informe exportado. El número de página se traduce al mismo valor en todas las páginas del informe.  
  
-   `="Page: " + Globals!PageNumber.ToString + " of " + Globals!TotalPages.ToString`  
  
-   `=Avg(Fields!YTDPurchase.Value, "Sales") & " Page Number " & Globals!PageNumber`  
  
 Esto ocurre porque el representador de Word analiza el informe para ver si hay campos relacionados con la paginación, como **PageNumber** y **TotalPages** , y solo administra referencias simples, no llamadas a una función. En este caso, la expresión llama a la función **ToString** . Las dos expresiones siguientes son equivalentes y ambas se representan correctamente al obtener una vista previa del informe en el Generador de informes o en el Diseñador de informes, o al representar el informe publicado en el Administrador de informes o en una biblioteca de SharePoint. Sin embargo, el representador de Word solo analiza correctamente la segunda expresión y representa los números de página correctos.  
  
-   **Expresión compleja:**  la expresión es `="Average Sales " & Avg(Fields!YTDPurchase.Value, "Sales") & " Page Number " & Globals!PageNumber`  
  
-   **Expresión con ejecuciones de texto:** Texto, **Average Sales**, y expresión,  `=Avg(Fields!YTDPurchase.Value, "Sales)`, y texto, **Page Number**, y expresión `=Globals!PageNumber`  
  
 Para evitar este problema, use varias ejecuciones de texto en vez de una expresión compleja cuando use expresiones en encabezados y pies de página. Las dos siguientes expresiones son equivalentes. La primera es una expresión compleja y la segunda usa ejecuciones de texto. El representador de Word solo analiza correctamente la segunda expresión.  
  
##  <a name="Interactivity"></a> Interactividad  
 En Word se admiten algunos elementos interactivos. A continuación se describen sus comportamientos específicos.  
  
### <a name="show-and-hide"></a>Mostrar u ocultar  
 El representador de Word representa los elementos del informe basándose en su estado en el momento de generar la representación. Si un elemento del informe está oculto, no se representa en el documento de Word. Si un elemento del informe está visible, se representa en el documento de Word. La funcionalidad de alternar no se admite en Word.  
  
### <a name="document-map"></a>Mapa del documento  
 Las etiquetas de mapa del documento que existan en el informe se representan como etiquetas de Tabla de contenido (TOC) de Word en los respectivos elementos y grupos del informe. La etiqueta del mapa del documento se utiliza como texto del rótulo para las etiquetas TOC. El vínculo de destino se coloca cerca del elemento en el que se establece la etiqueta. Aunque no se crea una tabla de contenido automáticamente en el documento de Word, puede generarla mediante las etiquetas de mapa del documento que se representan en el informe.  
  
### <a name="hyperlink-and-drillthrough-links"></a>Hipervínculos y vínculos de obtención de detalles  
 Los hipervínculos y los vínculos de obtención de detalles de los elementos de cuadro de texto e imagen de los informes se representan como hipervínculos en el documento de Word. Cuando se hace clic en el hipervínculo, el explorador web predeterminado abre la dirección URL y navega a ella. Cuando se hace clic en el hipervínculo de obtención de detalles, se tiene acceso al servidor de informes de origen.  
  
### <a name="interactive-sorting"></a>Ordenación interactiva  
 El contenido del informe se representa teniendo en cuenta el modo en que está ordenado actualmente en la región de datos del informe. Word no admite la ordenación interactiva. Una vez que se representa el informe, puede ordenar la tabla dentro de Word.  
  
### <a name="bookmarks"></a>Marcadores  
 Los marcadores del informe se representan como marcadores de Word. Los vínculos de marcador se representan como hipervínculos que conectan con las etiquetas de marcador del documento. Las etiquetas de marcador deben tener menos de 40 caracteres. El único carácter especial que se puede utilizar en una etiqueta de marcador es el carácter de subrayado (_). Los caracteres especiales no compatibles se quitan del nombre de la etiqueta de marcador y, si el nombre tiene más de 40 caracteres, se trunca. Si hay nombres de marcador duplicados en el informe, los marcadores no se representan en Word.  
  
##  <a name="WordStyleRendering"></a> Representación de estilos en Word  
 A continuación se describe brevemente el modo en que se representan los estilos en Word.  
  
### <a name="color-palette"></a>Paleta de colores  
 Los colores representados en el informe se representan en el documento de Word.  
  
### <a name="border"></a>Borde  
 Los bordes de los elementos de informe, excepto el borde de página, se representan como bordes de celdas de tabla de Word.  
  
##  <a name="SquigglyLines"></a> Líneas onduladas en los informes exportados  
 Cuando se exportan y se ven en Word, los datos o las constantes del informe podrían estar subrayados con líneas onduladas rojas o verdes. Las líneas onduladas rojas identifican errores de ortografía. Las líneas onduladas verdes identifican errores gramaticales. Esto ocurre cuando el informe incluye palabras que no cumplen con la revisión (ortográfica y gramatical) del idioma de edición que se especifica en Word. Por ejemplo, los títulos de columna del informe en inglés probablemente aparecerán subrayados con líneas onduladas rojas cuando el informe se represente en una versión en español de Word. Los errores ortográficos percibidos en los informes son más comunes que los gramaticales porque los informes suelen incluir un texto breve, y no frases completas o párrafos.  
  
 La presencia de líneas onduladas en los informes implica que el informe tiene errores, que probablemente no lo sean. Puede quitar las líneas onduladas cambiando el idioma de revisión del informe. Para ello, seleccione el contenido del informe y especifique el idioma apropiado para el contenido. Puede seleccionar todo el contenido o una parte del mismo. En Word 2010, la opción de idioma, **Establecer idioma de revisión**, está en el área **Idioma** de la pestaña **Revisión** . Cuando actualice el contenido, tendrá que volver a guardar el documento.  
  
 Según la versión de idioma del programa de Office, las herramientas de revisión (por ejemplo, el diccionario) del idioma que elija se incluyen con el programa o se proporcionan en un paquete de idioma de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office que puede adquirir.  
  
 En los temas siguientes se proporciona información adicional sobre cómo configurar las opciones de Word y Office.  
  
-   Cambie el idioma de revisión en **Preferencias de idioma de Microsoft Office 2010** o en el cuadro de diálogo **Opciones de Word** de Word. Para obtener más información, vea [Habilitar el uso de otros idiomas en los programas de Office](http://office.microsoft.com/word-help/enable-the-use-of-other-languages-in-your-office-programs-HA010354783.aspx?CTT=1).  
  
-   Agregue paquetes de idioma de Office y, después, cambie el idioma de revisión. Para obtener más información, vea [Habilitar el uso de otros idiomas en los programas de Office](http://office.microsoft.com/word-help/enable-the-use-of-other-languages-in-your-office-programs-HA010354783.aspx?CTT=1) y [Opciones de idioma de Office 2010](http://office.microsoft.com/language/).  
  
> [!NOTE]  
>  Cuando cambie el idioma de revisión en **Preferencias de idioma de Microsoft Office 2010** o en el cuadro de diálogo **Opciones de Word** en Word, el cambio se aplicará a todos los programas de Office.  
  
##  <a name="WordLimitations"></a> Limitaciones de Word  
 [!INCLUDE[ofprword](../../includes/ofprword-md.md)]aplica las limitaciones siguientes:  
  
-   Las tablas de Word admiten un máximo de 63 columnas. Si se intenta representar un informe que tiene más de 63 columnas, Word divide la tabla. Las columnas adicionales se colocan junto a las 63 columnas que se muestran en el cuerpo del informe. Por consiguiente, es posible que las columnas del informe no se alineen como se esperaba.  
  
-   Word admite un ancho de página máximo de 22 pulgadas de ancho y 22 pulgadas de alto. Si el contenido ocupa más de 22 pulgadas de ancho, es posible que algunos datos no se muestren en la vista Diseño de impresión.  
  
-   Word omite la configuración de alto de los encabezados y pies de página.  
  
-   Una vez exportado el informe, Word lo pagina de nuevo. Esto puede hacer que aparezcan saltos de página adicionales en el informe representado.  
  
-   Word no repite las filas de encabezado en la página dos y siguientes, aunque se establezca la propiedad RepeatOnNewPage de la fila de encabezado estático en un tablix (tabla, matriz o lista) en `True`. Puede definir saltos de página explícitos en su informe para obligar a las filas de encabezado a aparecer en nuevas páginas. Sin embargo, dado que Word aplica su propia paginación al informe representado exportado a Word, los resultados podrían variar y la fila de encabezado podría no repetirse previsiblemente. La fila de encabezado estática es la fila que contiene los encabezados de columna.  
  
-   Los cuadros de texto aumentan de tamaño cuando contienen espacios de no separación.  
  
-   Cuando se exporta texto a Word, el texto con decoración en determinadas fuentes puede generar glifos inesperados en el informe representado o la pérdida de glifos en el mismo.  
  
##  <a name="WordBenefits"></a> Ventajas de usar el representador de Word  
 Además de las características que son nuevas en [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010 estén disponibles para exportar informes, los archivos *.docx de los informes exportados suelen ser menores. Los informes exportados mediante el representador de Word suelen ser mucho menores que los mismos informes exportados mediante el representador de Word 2003.  
  
## <a name="backward-compatibility-of-exported-reports"></a>Compatibilidad con versiones anteriores de los informes exportados  
 Puede seleccionar un modo de compatibilidad de Word y establecer opciones de compatibilidad. El representador de Word crea documentos con el modo de compatibilidad activado. Al volver a guardar los documentos con el modo de compatibilidad desactivado, el diseño del documento puede verse afectado.  
  
 Si desactiva el modo de compatibilidad y después vuelve a guardar un informe, el diseño del informe puede cambiar de maneras inesperadas.  
  
##  <a name="AvailabilityWord"></a> Disponibilidad del representador de Word 2003  
 En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], el representador de Word predeterminado es la versión que se representa en el formato nativo de [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010. Es la opción **Word** que aparece en los menús **Exportar** del Administrador de informes y SharePoint. La versión anterior, compatible solo con [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003, se denomina a partir de ahora Word 2003 y aparece en los menús con ese nombre. La opción de menú **Word 2003** no es visible de forma predeterminada, pero el administrador puede hacer que lo esté actualizando el archivo de configuración RSReportServer. Si desea exportar informes de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] con el representador de Word 2003, debe actualizar el archivo de configuración RSReportDesigner. Sin embargo, aunque se haga que el representador de Word 2003 esté visible, no está disponible en todos los escenarios. El archivo de configuración RSReportServer reside en el servidor de informes, por lo que las herramientas o productos desde los que exporte informes se deben conectar con un servidor de informes para leer el archivo de configuración. Si usa herramientas o productos en modo sin conexión o local, hacer que el representador de Word 2003 esté visible no tiene ningún efecto. La opción de menú **Word 2003** sigue sin estar disponible. Si hace que el representador de Word 2003 esté visible en el archivo de configuración RSReportDesigner, la opción de menú **Word 2003** siempre está disponible en la vista previa de informes de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
 La opción de menú **Word 2003** nunca está visible en los escenarios siguientes:  
  
-   El Generador de informes está en modo sin conexión y se obtiene la vista previa de un informe en el Generador de informes. Esto es así en el [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] y versiones independientes del generador de informes.  
  
-   El elemento web Visor de informes está en modo local y la granja de servidores de SharePoint no está integrada en un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para más información, vea [Informes en modo local frente al modo conectado en el Visor de informes &#40;Reporting Services en modo de SharePoint&#41;](../local-vs-connected-mode-report-viewer-reporting-services-sharepoint-mode.md)  
  
 Si el representador **Word 2003** se configura para que esté visible, las opciones de menú **Word** y **Word 2003** estarán disponibles en los escenarios siguientes:  
  
-   Administrador de informes si Reporting Services está instalado en modo nativo.  
  
-   Sitio de SharePoint si Reporting Services está instalado en modo integrado de SharePoint.  
  
-   [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y obtiene una vista previa del informe.  
  
-   Generador de informes está conectado a un servidor de informes. Esto puede ser un [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] o una versión independiente del generador de informes.  
  
-   El elemento web Visor de informes en modo remoto.  
  
 En el código XML siguiente se muestran los elementos para las dos extensiones de representación de Word en los archivos de configuración RSReportServer y RSReportDesigner:  
  
 `<Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>`  
  
 `<Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>`  
  
 La extensión WORDOPENXML define el representador de Word para [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010. La extensión WORD define la versión de [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003. `Visible = “false”` indica que el representador de Word 2003 está oculto. Para obtener más información, consulte [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md) y [RSReportDesigner Configuration File](../report-server/rsreportdesigner-configuration-file.md).  
  
##  <a name="Differences"></a> Diferencias entre los representadores de 2003 de Word y Word  
 Los informes representados mediante el representador de Word o Word 2003 no se suelen distinguir visualmente. Sin embargo, puede observar pequeñas diferencias entre los dos formatos de Word o Word 2003.  
  
##  <a name="DeviceInfo"></a> Configuración de la información del dispositivo  
 Puede cambiar parte de la configuración predeterminada de este representador si cambia la configuración de la información del dispositivo; por ejemplo, puede omitir los hipervínculos y los vínculos de obtención de detalles o expandir todos los elementos que se pueden alternar, independientemente de su estado original en el momento de generar la representación. Para obtener más información, consulte [Word Device Information Settings](../word-device-information-settings.md).  
  
## <a name="see-also"></a>Vea también  
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;generador de informes y SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Representar elementos de informe &#40;Generador de informes y SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
