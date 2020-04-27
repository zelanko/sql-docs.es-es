---
title: Exportar informes (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10437"
ms.assetid: a2bab8c1-505d-4da3-b1db-ea0ae13b2336
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d8b4fe6e791f84f0949b0657b890c79db99dfbf9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107946"
---
# <a name="exporting-reports-report-builder-and-ssrs"></a>Exportar informes (Generador de informes y SSRS)
  Después de ejecutar un informe, puede exportarlo a otro formato, como Excel o PDF, o exportarlo generando un documento de servicio de Atom, enumerando las fuentes de distribución de datos que cumplen con Atom y están disponibles en informe.  
  
 Exporte un informe para hacer lo siguiente:  
  
-   Trabajar con los datos del informe en otra aplicación. Por ejemplo, puede exportar el informe a Excel y, a continuación, continuar trabajando con los datos en Excel.  
  
-   Imprimir el informe en un formato diferente. Por ejemplo, puede exportar el informe al formato de archivo PDF y, a continuación, imprimirlo.  
  
-   Guardar una copia del informe como otro tipo de archivo. Por ejemplo, puede exportar un informe a Word y guardarlo, creando una copia del informe.  
  
-   Usar los datos del informe como fuentes de distribución de datos de las aplicaciones. Por ejemplo, puede generar fuentes de datos compatibles con Atom que pueda [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] consumir el cliente y, a continuación, trabajar con los [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]datos de.  
  
 La opción de exportación está disponible en la barra de herramientas del visor de informes en el Administrador de informes, que aparece en la parte superior de cada informe al ver un informe en el servidor de informes, y en la cinta del Generador de informes al obtener una vista previa de un informe. La opción de fuente de distribución de datos solo está disponible en el Administrador de informes.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona muchas extensiones de presentación, admitiendo exportaciones de informes a formatos de archivo comunes. Las extensiones de presentación admiten formatos de archivo con saltos de página automáticos (por ejemplo, Word o Excel), saltos de página duros (por ejemplo, PDF o TIFF) o solo datos (por ejemplo, CSV o XML que admita Atom).  
  
 Para empezar a trabajar rápidamente con la exportación de informes y la generación de fuentes de datos compatibles con Atom a partir de informes, vea [exportar un informe como otro tipo de archivo &#40;generador de informes y ssrs&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md) y [generar fuentes de datos a partir de un informe &#40;Generador de informes y SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="rendering-extension-types"></a><a name="RendererTypes"></a>Tipos de extensión de representación  
 Hay tres tipos de extensiones de presentación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   **Extensiones de presentador de datos:** las extensiones de presentación de datos quitan del informe toda la información de formato y muestran solo los datos. El archivo resultante se puede usar para importar los datos del informe sin formato en otro tipo de archivo, como Excel, en otra base de datos, en un mensaje de datos XML o en una aplicación personalizada. Los presentadores de datos no admiten los saltos de página.  
  
     Se admiten las siguientes extensiones de presentación de datos: CSV, XML y Atom.  
  
-   **Extensiones del representador de saltos de página automáticos:** las extensiones del representador de saltos de página automáticos mantienen el diseño y el formato del informe. El archivo resultante se optimiza para la visualización y la entrega basadas en pantalla, como en una página web o en los controles **ReportViewer** .  
  
     Se admiten las siguientes extensiones de presentador de saltos de página automáticos: [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word y archivos de web (MHTML).  
  
-   **Extensiones del representador de saltos de página manuales:** las extensiones del representador de saltos de página manuales mantienen el diseño y el formato del informe. El archivo resultante se optimiza para que su aspecto no varíe al imprimirlo o para ver el informe en pantalla con formato de libro.  
  
     Se admiten las siguientes extensiones de presentador de saltos de página duros: TIFF y PDF.  
  
##  <a name="export-formats"></a><a name="ExportFormats"></a>Formatos de exportación  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona extensiones de presentación que presentan los informes en formatos diferentes. Si piensa utilizar esta característica, debería optimizar el diseño del informe para su formato de archivo elegido. El tema sobre cada extensión de representación proporciona información detallada sobre cómo se presenta el informe en ese formato.  
  
 En la tabla siguiente se enumeran los formatos disponibles.  
  
|Formato|Tipo de extensión de presentación|Descripción|  
|------------|------------------------------|-----------------|  
|CSV|Datos|La extensión de representación de valores separados por comas (CSV) representa los informes como una representación sin estructura jerárquica de los datos a partir de un informe estándar y sin formato para que resulten fáciles de leer e intercambiar con muchas aplicaciones.<br /><br /> Para obtener más información, vea [Exportar a Microsoft Excel &#40;Generador de informes y SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md).|  
|Excel|Salto de página automático|La extensión de representación en Excel procesa un informe como documento de Excel compatible con [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007-2010 así como con [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003, gracias al Paquete de compatibilidad de Microsoft Office para formatos de archivos de Word, Excel y PowerPoint instalado. El informe se exporta a una hoja de cálculo de Excel con algún diseño y elementos de diseño originales quitados. Las propiedades del informe y los grupos del informe se pueden establecer para habilitar la denominación de las pestañas de la hoja de cálculo al exportar a Excel. La extensión de nombre de archivo de los archivos generados por este representador es .xlsx.<br /><br /> Para obtener más información, vea [Exportar a Microsoft Excel &#40;Generador de informes y SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md).<br /><br /> Nota: la extensión de representación de Excel 2003 que se representa en el formato nativo [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] de 2003 está disponible en algunos escenarios de informes.|  
|Word|Salto de página automático|La extensión de representación en Word procesa un informe como documento de Word compatible con [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010 así como con [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003, gracias al Paquete de compatibilidad de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office para formatos de archivos de Word, Excel y PowerPoint instalado. Después de exportar el informe a un documento de Word, puede modificar su contenido y diseñar informes con estilo de documento, como etiquetas postales, pedidos de compra o circulares. La extensión de nombre de archivo de los archivos generados por este representador es .docx.<br /><br /> Para obtener más información, vea [Exportar a Microsoft Word &#40;Generador de informes y SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md).<br /><br /> Nota: la extensión de representación de Word 2003 que se representa en el formato nativo [!INCLUDE[ofprword](../../includes/ofprword-md.md)] de 2003 está disponible en algunos escenarios de informes.|  
|Archivo web|Salto de página automático|La extensión de representación en HTML representa un informe en formato HTML. La extensión de representación también puede generar páginas HTML completas o fragmentos de HTML para incrustarlos en otras páginas HTML. Todos los HTML se generan con la codificación UTF-8.<br /><br /> La extensión de presentación en HTML es la predeterminada para los informes que se visualizan en el Generador de informes y en un explorador, lo que incluye también cuando se ejecutan en el Administrador de informes.<br /><br /> Para obtener más información, vea [Representar en HTML &#40;Generador de informes y SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md).|  
|Archivo PDF de Acrobat|Salto de página duro|La extensión de representación en PDF representa un informe en archivos que se pueden abrir en Adobe Acrobat y en visores de PDF de otros fabricantes que admiten PDF 1.3. Aunque PDF 1.3 es compatible con Adobe Acrobat 4.0 y versiones posteriores, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite Adobe Acrobat 6 o posterior. La extensión de representación no requiere el software Adobe para representar el informe. Sin embargo, se necesitan visores de PDF, como Adobe Acrobat, para ver o imprimir un informe en formato PDF.<br /><br /> Para obtener más información, vea [Exportar a un archivo PDF &#40;Generador de informes y SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md).|  
|Archivo TIFF|Salto de página duro|La extensión de presentación en imágenes presenta un informe en un mapa de bits o metarchivo. De manera predeterminada, una extensión de representación en imágenes genera un archivo TIFF del informe, que se puede ver en varias páginas. Cuando el cliente recibe la imagen, se puede mostrar en un visor de imágenes y se puede imprimir.<br /><br /> La extensión de presentación en imágenes puede generar archivos en cualquiera de los formatos que admite [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG y TIFF.<br /><br /> Para obtener más información, vea [Exportar a Microsoft Excel &#40;Generador de informes y SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md).|  
|XML|Datos|La extensión de presentación en XML devuelve un informe en formato XML. El esquema XML del informe es específico de éste y solamente contiene datos. La extensión de representación en XML no representa la información de diseño ni mantiene la paginación. El XML que genera esta extensión se puede importar a una base de datos, se puede usar como mensaje de datos XML o se puede enviar a una aplicación personalizada.<br /><br /> Para obtener más información, vea [Exportar a Microsoft Excel &#40;Generador de informes y SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md).|  
|Atom|Datos|La extensión de presentación Atom genera fuentes de distribución de datos compatibles con Atom desde los informes. Las fuentes de datos se pueden leer e intercambiar con aplicaciones como el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cliente que puede consumir fuentes de datos compatibles con Atom.<br /><br /> El resultado es un documento de servicio de Atom que enumera las fuentes de los datos disponibles de un informe. Se crea al menos una fuente de datos para cada región de datos de un informe. Según el tipo de región de datos y los datos que esta muestra, podrían generarse varias fuentes de distribución de datos.<br /><br /> Para obtener más información, vea [generar fuentes de datos a partir de informes &#40;generador de informes y SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md).|  
  
##  <a name="exporting-a-report"></a><a name="ExportingReport"></a>Exportar un informe  
 Para exportar un informe, ejecútelo en el Administrador de informes o el Generador de informes y, a continuación, seleccione un formato en la lista desplegable Exportar. Se le solicita que decida si guardar o abrir el archivo. Si elige **Abrir**, el informe se abre en la aplicación asociada al formato de representación que eligió. Por ejemplo, si selecciona **Excel** , el informe se abre en Excel. Si elige **Guardar**, el informe se guarda. Por ejemplo, si está exportando a Excel, el informe se guarda como archivo .xls. Las asociaciones de archivo definidas para el equipo local determinan la aplicación que se utilizará con cada formato de presentación. Para obtener más información, vea [exportar un informe como otro tipo de archivo &#40;generador de informes y SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md).  
  
 El servidor de informes exporta el informe tal como se encuentra en la sesión del usuario actual. Si se publica una versión actualizada de un informe mientras otro usuario lo tiene abierto, o cambian los datos que presenta el informe, el informe exportado no se actualizará.  
  
 Exportar un informe a un formato diferente podría afectar a su paginación. Al obtener una vista previa de un informe, lo ve tal como es presentado por la extensión de presentación HTML, que sigue las reglas de salto de página automático. Al exportar un informe a un formato de archivo diferente, como Adobe Acrobat (PDF), la paginación está basada en el tamaño de página físico, que sigue las reglas de salto de página forzado. Las páginas también pueden separarse mediante saltos de página lógicos que se agregan al informe, pero la longitud real de una página varía en función del tipo de representador que se utiliza. Para cambiar la paginación de su informe, debe entender el comportamiento de la paginación de la extensión de presentación que elija. Podría necesitar ajustar el diseño de su informe para esta extensión de presentación. Para obtener más información, vea [Representación y diseño de páginas &#40;Generador de informes y SSRS&#41;](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md).  
  
##  <a name="generating-data-feeds-from-a-report"></a><a name="GeneratingDataFeedsFromReport"></a>Generar fuentes de datos a partir de un informe  
 Para generar las fuentes de distribución de datos desde un informe, ejecute el informe en el Administrador de informes y, a continuación, haga clic en el icono **Generar la fuente de los datos** en la barra de herramientas del Administrador de informes. Se le solicita que decida si guardar o abrir el archivo. Si elige **Abrir**, el documento de servicio de Atom se abre en la aplicación que está asociada a la extensión de archivo .atomsvc. Si elige **Guardar**, el documento se guarda como un archivo .atomsvc. De forma predeterminada, el nombre del archivo es el nombre del informe. Puede cambiar el nombre a uno que sea más significativo.  
  
 Guarde el documento de servicio de Atom en su equipo. Después puede cargarlo a un servidor de informes o a otro servidor para que esté disponible para que otros lo utilicen. Para obtener más información, vea [Generar fuentes de distribución de datos a partir de informes &#40;Generador de informes y SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md) y [Generar fuentes de distribución de datos a partir de un informe &#40;Generador de informes y SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md).  
  
##  <a name="troubleshooting-exported-reports"></a><a name="Troubleshooting"></a>Solucionar problemas de informes exportados  
 A veces, los informes parecen diferentes o no funcionan como desea tras exportarlos a un formato diferente. Esto se debe a que podrían aplicarse ciertas reglas y limitaciones al representador. Puede solucionar muchas limitaciones teniéndolas en cuenta al crear el informe. Podría necesitar usar un diseño ligeramente diferente en el informe, alinear cuidadosamente los elementos dentro del mismo, restringir los pies de página del informe a una sola línea de texto, etc.  
  
 Si un informe contiene texto Unicode y números arábigos, o contiene fechas arábigas, las fechas y los números no se representan correctamente cuando el informe se imprime o cuando se exporta cualquiera de los formatos siguientes.  
  
-   PDF  
  
-   Word  
  
-   Excel  
  
-   Imagen/TIFF  
  
 Si se exporta el informe a HTML, las fechas y los números se representan correctamente.  
  
 Los temas acerca de los representadores concretos describen cómo se representan los elementos de informe y las regiones de datos, así como las limitaciones y soluciones de cada procesador.  
  
-   [Exportar a un archivo CSV &#40;Generador de informes y SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md)  
  
-   [Exportar a Microsoft Excel &#40;Generador de informes y SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md)  
  
-   [Exportar a Microsoft Word &#40;Generador de informes y SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md)  
  
-   [Representar en HTML &#40;Generador de informes y SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md)  
  
-   [Exportar a un archivo PDF &#40;Generador de informes y SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md)  
  
-   [Exportar a un archivo de imagen &#40;Generador de informes y SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md)  
  
-   [Exportar a XML &#40;Generador de informes y SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md)  
  
-   [Generar fuentes de distribución de datos a partir de informes &#40;Generador de informes y SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona características adicionales para ayudarle a crear informes que funcionen bien en otros formatos. Los saltos de página en las regiones de datos Tablix (tabla, matriz y lista), los grupos y los rectángulos proporcionan un mayor control sobre la paginación del informe. Las páginas del informe, delimitadas mediante saltos de página, pueden tener nombres de página diferentes y restablecer la numeración de las páginas. Mediante el uso de expresiones, los nombres de página y los números de página se pueden actualizar dinámicamente cuando se ejecuta el informe. Para más información, vea [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
 Además, puede usar la función RenderFormat integrada para aplicar condicionalmente diseños de informe diferentes para representadores distintos. Para obtener más información, vea [Referencias a campos globales y de usuario integrados &#40;Generador de informes y SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
##  <a name="other-ways-of-exporting-reports"></a><a name="OtherWaysExportingReports"></a>Otras maneras de exportar informes  
 La exportación de un informe es una tarea a petición que se realiza cuando el informe está abierto en el Administrador de informes o el Generador de informes. Si desea automatizar una operación de exportación (por ejemplo, exportar periódicamente un informe a una carpeta compartida como un tipo de archivo específico), cree una suscripción que entregue el informe a una carpeta compartida. Para obtener más información, vea [File Share Delivery in Reporting Services](../subscriptions/file-share-delivery-in-reporting-services.md).  
  
 De forma predeterminada, los informes cuya vista previa se obtiene en las herramientas de elaboración de informes o que se abren en una aplicación de explorador, como el Administrador de informes, siempre se presentan primero en HTML. No es posible especificar una extensión de representación diferente como opción predeterminada para la vista. Sin embargo, puede crear una suscripción que genere un informe en el formato de representación que desee para que se envíe posteriormente a una bandeja de entrada de correo electrónico o una carpeta compartida. Para obtener más información, vea [crear, modificar y eliminar suscripciones estándar &#40;Reporting Services en modo nativo&#41;](../subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) y [crear, modificar y eliminar una suscripción controlada por datos](../subscriptions/data-driven-subscriptions.md).  
  
 También puede tener acceso a un informe a través de una dirección URL que especifique una extensión de presentación como un parámetro URL y presente directamente el informe en el formato especificado sin presentarlo primero en HTML. En el ejemplo siguiente se presenta un informe en formato Excel:  
  
```  
http://<Server Name>/reportserver?/Sales/YearlySalesSummary&rs:Format=Excel&rs:Command=Render  
```  
  
 Para obtener más información, consulte [Export a Report Using URL Access](../export-a-report-using-url-access.md).  
  
## <a name="see-also"></a>Consulte también  
 [Controlar saltos de página, encabezados, columnas y filas &#40;Generador de informes y SSRS&#41;](../report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS &#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Imprimir informes &#40;Generador de informes y SSRS&#41;](print-reports-report-builder-and-ssrs.md)   
 [Guardar informes &#40;Generador de informes&#41;](saving-reports-report-builder.md)  
  
  
