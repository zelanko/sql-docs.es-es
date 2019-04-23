---
title: Exportar a un archivo PDF (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f22497b7-f6c1-4c7b-b831-8c731e26ae37
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1675221a4d6cfc8ad61a975610113435423ae05b
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59940591"
---
# <a name="exporting-to-a-pdf-file-report-builder-and-ssrs"></a>Exportar a un archivo PDF (Generador de informes y SSRS)
  La extensión de representación en PDF representa un informe en archivos que se pueden abrir en Adobe Acrobat y en visores de PDF de otros fabricantes que admiten PDF 1.3. Aunque PDF 1.3 es compatible con Adobe Acrobat 4.0 y versiones posteriores, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite Adobe Acrobat 6 o posterior. La extensión de representación no requiere el software Adobe para representar el informe. Sin embargo, se necesitan visores de PDF, como Adobe Acrobat, para ver o imprimir un informe en formato PDF.  
  
 La extensión de representación en PDF admite caracteres ANSI y puede traducir caracteres Unicode del japonés, coreano, chino tradicional, chino simplificado, cirílico, hebreo y árabe, con ciertas limitaciones. Para obtener más información acerca de las limitaciones, consulte [exportar informes &#40;generador de informes y SSRS&#41;](export-reports-report-builder-and-ssrs.md).  
  
 El representador de PDF es un representador en página física y, por consiguiente, tiene un comportamiento de paginación que difiere del de otros representadores como HTML y Excel. En este tema se proporciona información específica del representador de PDF y se describen las excepciones a las reglas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="FontRequirements"></a> Incrustación de fuentes  
 Siempre que sea posible, la extensión de representación en PDF incrustará el subconjunto de cada una de las fuentes que sea necesaria para mostrar el informe en el archivo PDF. Las fuentes que se utilicen en el informe deberán instalarse en el servidor de informes. Cuando el servidor de informes genera un informe en formato PDF, usa la información almacenada en la fuente a la que hace referencia el informe para crear asignaciones de caracteres en el archivo PDF. Si la fuente a la que se hace referencia no está instalada en el servidor de informes, es posible que el archivo PDF resultante no contenga las asignaciones correctas y, por lo tanto, no se muestre correctamente cuando se visualice.  
  
 Las fuentes se incrustan en el archivo PDF cuando se dan las siguientes condiciones:  
  
-   El autor de la fuente concede privilegios de incrustación para la fuente. Las fuentes instaladas incluyen una propiedad que indica si el autor de la fuente tiene intención de permitir la incrustación de una fuente en un documento. Si el valor de la propiedad es EMBED_NOEMBEDDING, la fuente no se incrustará en el archivo PDF. Para obtener más información, vea "TTGetEmbeddingType" en msdn.microsoft.com.  
  
-   La propiedad Font es TrueType.  
  
-   Hacen referencia a las fuentes los elementos visibles de un informe. Si se hace referencia a una fuente mediante un elemento que tiene la propiedad Hidden establecida en True, no es necesario que la fuente muestre los datos representados y no se incluirá en el archivo. Las fuentes solamente se incrustan cuando tienen que mostrar los datos de informe representados.  
  
 Si se cumplen todas estas condiciones para una fuente, la fuente se incrusta en el archivo PDF. Si no se cumple alguna de estas condiciones, o varias, la fuente no se incrusta en el archivo PDF.  
  
> [!NOTE]  
>  Aunque se cumplan las condiciones, hay una circunstancia en la que no se incrustan fuentes en el archivo PDF. Si las fuentes usadas son las de la especificación de PDF que se conoce normalmente como fuentes estándar de tipo 1 o fuentes de base catorce, no se incrustan fuentes para el contenido ANSI.  
  
  
  
### <a name="fonts-on-the-client-computer"></a>Fuentes en el equipo cliente  
 Cuando una fuente se incrusta en el archivo PDF, el equipo que se usa para ver el informe (equipo cliente) no necesita tener la fuente instalada para que el informe se muestre correctamente.  
  
 Cuando una fuente no se incrusta en el archivo PDF, el equipo cliente debe tener instalada la fuente correcta para que el informe se muestre correctamente. Si la fuente no está instalada en el equipo cliente, el archivo PDF muestra un carácter de signo de interrogación de cierre (?) para los caracteres no compatibles.  
  
### <a name="verifying-fonts-in-a-pdf-file"></a>Comprobar las fuentes de un archivo PDF  
 Suelen producirse diferencias en la salida en PDF si se usa una fuente que no admite caracteres no latinos en un informe y, a continuación, se agregan caracteres no latinos al informe. Se debe comprobar la salida de representación en PDF tanto en el servidor de informes como en los equipos cliente para comprobar que el informe se representa correctamente.  
  
 No confíe en la visualización del informe en vista previa ni en la exportación a HTML, ya que el informe parece correcto por la sustitución de fuentes automática realizada por la interfaz de diseño gráfico o por Microsoft Internet Explorer, respectivamente. Si faltan glifos de Unicode en el servidor, es posible que vea caracteres reemplazados por un signo de interrogación de cierre (?). Si falta una fuente en el cliente, puede ver que algunos caracteres se reemplazan con cuadros (□).  
  
 Las fuentes incrustadas en el archivo PDF se incluyen en la propiedad Fonts que se guarda con el archivo, en forma de metadatos.  
  
##  <a name="Metadata"></a> Metadatos  
 Además del diseño del informe, la extensión de representación en PDF escribe los metadatos siguientes en el diccionario de información del documento PDF.  
  
|Propiedad de PDF|Creada a partir de|  
|------------------|------------------|  
|`Title`|El atributo `Name` del elemento RDL `Report`.|  
|`Author`|El elemento RDL `Author`.|  
|`Subject`|El elemento RDL `Description`.|  
|`Creator`|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
|`Producer`|El nombre y la versión de la extensión de representación.|  
|`CreationDate`|La hora de ejecución del informe en el formato `datetime` de PDF.|  
  
  
  
##  <a name="Interactivity"></a> Interactividad  
 Algunos elementos interactivos se admiten en PDF. A continuación se describen sus comportamientos específicos.  
  
### <a name="show-and-hide"></a>Mostrar u ocultar  
 El formato PDF no permite mostrar y ocultar elementos dinámicamente. El documento PDF se representa para que coincida con el estado actual de cualquier elemento del informe. Por ejemplo, si el elemento se mostraba cuando se ejecutó inicialmente el informe, el elemento se representará. Las imágenes que pueden alternarse no se representarán si estaban ocultas al exportar el informe.  
  
### <a name="document-map"></a>Mapa del documento  
 Si hay alguna etiqueta de mapa del documento presente en el informe, se agrega un esquema de documento al archivo PDF. Cada etiqueta de mapa del documento aparece como una entrada en el esquema de documento en el orden en el que figura en el informe. En Acrobat, solo se agrega un marcador de destino al esquema del documento si se representa la página en la que aparece.  
  
 Si solo se representa una página, no se agrega ningún esquema de documento. El mapa del documento se organiza jerárquicamente para reflejar el nivel de anidamiento del informe. En Acrobat, puede obtenerse acceso al esquema de documento debajo de la pestaña Marcadores. Haga clic en una entrada dentro del esquema de documento para que el documento se desplace a la ubicación marcada.  
  
### <a name="bookmarks"></a>Marcadores  
 No se admiten marcadores en la representación en PDF.  
  
### <a name="drillthrough-links"></a>Vínculos de obtención de detalles  
 Los vínculos de obtención de detalles no se admiten en representación de PDF. Los vínculos de obtención de detalles no se representan como vínculos en los que se puede hacer clic y los informes detallados no se pueden conectar con el destino de la obtención de detalles.  
  
### <a name="hyperlinks"></a>Hipervínculos  
 Los hipervínculos de los informes se representan como vínculos en los que puede hacerse clic en el archivo PDF. Al hacer clic en ellos, Acrobat abrirá el explorador predeterminado del cliente y navegará a la dirección URL del hipervínculo.  
  
  
  
##  <a name="Compression"></a> Compresión  
 La compresión de imágenes está basada en el tipo de archivo original de la imagen. La extensión de representación en PDF comprime los archivos PDF de forma predeterminada.  
  
 Para conservar la compresión de las imágenes incluidas en el archivo PDF siempre que sea posible, las imágenes JPEG se almacenan como JPEG y el resto de tipos de imagen se almacenan como BMP.  
  
> [!NOTE]  
>  Los archivos PDF no admiten la inserción de imágenes PNG.  
  
  
  
##  <a name="DeviceInfo"></a> Configuración de la información del dispositivo  
 Puede cambiar parte de la configuración predeterminada de este representador cambiando los valores de configuración de la información del dispositivo. Para obtener más información, consulte [PDF Device Information Settings](../pdf-device-information-settings.md).  
  
  
  
## <a name="see-also"></a>Vea también  
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;Generador de informes y SSRS&#41;](interactive-functionality-different-report-rendering-extensions.md)   
 [Representar elementos de informe &#40;Generador de informes y SSRS&#41;](../report-design/rendering-report-items-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
  
