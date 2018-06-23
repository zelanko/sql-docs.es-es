---
title: Visor HTML y barra de herramientas de informe | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- HTML Viewer [Reporting Services]
- report toolbar [Reporting Services]
ms.assetid: cd86b319-babd-45af-a6a4-f659fdcc40c3
caps.latest.revision: 32
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 9671f72321630dc53243d695dca7f943e4685e7b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201112"
---
# <a name="html-viewer-and-the-report-toolbar"></a>Visor HTML y la barra de herramientas del informe
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona un Visor HTML que se usa para mostrar informes a petición conforme se solicitan del servidor de informes. El Visor HTML ofrece un marco para ver informes en HTML. Incluye una barra de herramientas de informe, una sección de parámetros, una sección de credenciales y un mapa del documento. La barra de herramientas de informe del Visor HTML incluye características que se pueden usar para trabajar con un informe, incluidas las opciones de exportación para verlo con formatos distintos de HTML. La sección de parámetros y el mapa del documento solamente aparecen cuando se abren informes configurados para usar parámetros y un control de mapa de documento.  
  
> [!NOTE]  
>  Aunque no se puede modificar la barra de herramientas de informe, puede configurar los parámetros de una URL de informe para ocultarla en un informe. Para obtener más información acerca de cómo ocultar la barra de herramientas de informe, vea [URL Access Parameter Reference](url-access-parameter-reference.md).  
  
## <a name="report-toolbar"></a>Barra de herramientas de informe  
 La barra de herramientas de informe proporciona funcionalidades para navegación, zoom, actualización, búsqueda, exportación, impresión y fuentes de distribución de datos para los informes representados con la extensión de representación HTML.  
  
 La funcionalidad de impresión es opcional. Si está disponible, en la barra de herramientas de informe se mostrará el icono de la impresora. Cuando se use por primera vez, al hacer clic en el icono de la impresora se descargará un control ActiveX que debe instalar. Una vez que haya instalado el control, haga clic en el icono de la impresora para abrir el cuadro de diálogo Imprimir y seleccione las impresoras configuradas para su equipo. La disponibilidad de la impresión viene determinada por la configuración del servidor y del explorador. Para más información, vea [Imprimir informes desde un explorador usando el control de impresión &#40;Generador de informes y SSRS&#41;](report-builder/print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md) y [Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  
  
 La barra de herramientas de informe es similar a la que se muestra en la siguiente ilustración. Es posible que la suya difiera un poco de la que se muestra en la ilustración, dependiendo de las características del informe o las opciones de representación disponibles.  
  
 ![Barra de herramientas de informe](media/htmlviewer-toolbar.gif "Barra de herramientas de informe")  
  
 En la tabla siguiente se describen las características más comunes de la barra de herramientas de informe. Cada característica se identifica con el control que se utiliza para obtener acceso a ella.  
  
|Utilice este icono o control||A|  
|------------------------------|-|--------|  
|![Controles de navegación en páginas](media/htmlviewer-pagenav.gif "controles de navegación en páginas")|**Controles de navegación en páginas**|Abrir la primera o la última página de un informe, ver un informe página a página y abrir una página concreta de un informe. Para ver una página específica, escriba el número de página y presione ENTRAR.|  
|![Controles de presentación de página](media/htmlviewer-pagesize.gif "controles de presentación de página")|**Controles para mostrar páginas**|Aumentar o reducir el tamaño de la página del informe. Además de los cambios basados en porcentajes, puede seleccionar **Ancho de página** para que la página del informe se ajuste al ancho de la ventana del explorador o **Toda la página** para que la página del informe se ajuste al alto de la ventana. **Internet Explorer 5.5 y versiones posteriores admiten la opción** Zoom [!INCLUDE[msCoName](../includes/msconame-md.md)] .|  
|![Campo de búsqueda](media/htmlviewer-search.gif "campo de búsqueda")|**Campo Buscar**|Buscar contenido del informe escribiendo una palabra o una frase que se desee encontrar (la longitud máxima del valor es 256 caracteres). La función de búsqueda distingue entre mayúsculas y minúsculas, y se inicia en la página o sección seleccionada. En una operación de búsqueda, solo se incluye el contenido visible. Para buscar más repeticiones del mismo valor, haga clic en **Siguiente**.|  
|![Formatos de exportación](media/htmlviewer-export.GIF "formatos de exportación")|**Formatos de exportación**|Abrir una nueva ventana del explorador y representar el informe con el formato seleccionado. Los formatos disponibles vienen determinados por las extensiones de representación que se hayan instalado en el servidor de informes. Para imprimir se recomienda TIFF. Haga clic en **Exportar** para ver el informe con el formato seleccionado.|  
|![Icono de mapa de documento](media/htmlviewer-docmap.GIF "icono de mapa de documento")|**Icono de mapa de documento**|Mostrar u ocultar el panel del mapa del documento en un informe que incluya un mapa de documento. Un mapa de documento es un control de navegación en informes similar al panel de navegación de un sitio web. Se puede hacer clic en los elementos del mapa para navegar a un grupo, una página o un subinforme determinado.|  
|![Icono de la impresora](media/printer-icon.gif "icono de la impresora")|**Icono de impresora**|Abrir el cuadro de diálogo Imprimir, en el que puede especificar las opciones de impresión e imprimir un informe. Cuando se use por primera vez, al hacer clic en este icono se le pedirá que descargue el control de impresión.|  
||**Iconos para mostrar y ocultar**|Mostrar u ocultar los campos de valores de parámetros y el botón **Ver informe** en un informe que incluya parámetros.|  
|![Botón para actualizar el explorador de la barra de herramientas](media/htmlviewer-refresh.GIF "Botón para actualizar el explorador de la barra de herramientas")|**Icono para actualizar informe**|Actualizar el informe. Se actualizarán los datos de los informes activos. Los informes almacenados en caché se volverán a cargar desde su lugar de almacenamiento.|  
|![htmlviewer_datafeed](media/htmlviewer-datafeed.gif "htmlviewer_datafeed")|**Icono de fuente de distribución de datos**|Fuentes de distribución de datos generadas a partir de informes.|  
  
### <a name="about-export-formats"></a>Acerca de los formatos de exportación  
 En la barra de herramientas de informe, se pueden seleccionar varios formatos para ver el informe. Los formatos disponibles vienen determinados por las extensiones de representación que se hayan instalado en el servidor de informes. Cuando se selecciona otro formato, se abre una segunda ventana del explorador para mostrar el informe en un visor asociado al formato de exportación seleccionado. Si no hay ningún visor disponible para el formato seleccionado, se puede seleccionar un formato diferente.  
  
 En una instalación de servidor de informes predeterminada, se incluyen los siguientes formatos de exportación. La lista de formatos de exportación disponibles puede ser distinta de la que se muestra aquí.  
  
|Formato de exportación|Descripción|  
|-------------------|-----------------|  
|XML|Muestra el informe con sintaxis XML. Se abrirá una nueva ventana del explorador para mostrar los informes en XML.|  
|CSV|Muestra un informe en formato delimitado por comas. El informe se abre en una aplicación asociada al tipo de archivos CSV.|  
|Archivo PDF de Acrobat|Muestra el informe en un visor PDF del lado cliente. Para utilizar este formato, debe disponer de un visor PDF de terceros (por ejemplo, Adobe Acrobat Reader).|  
|Excel|Muestra el informe en [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel.|  
|Archivo web|Muestra el informe en formato HTML codificado con MIME que guarda las imágenes y el contenido vinculado con el informe.|  
|Archivo TIFF|Muestra el informe en el visor de TIFF predeterminado. Para algunos clientes de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows, es el Visor de imágenes y fax de Windows. Seleccione este formato para ver el informe con un diseño orientado a la página.|  
  
## <a name="parameters"></a>Parámetros  
 Los parámetros son valores que se utilizan para seleccionar datos específicos, especialmente para completar una consulta que selecciona los datos del informe o para filtrar el conjunto de resultados. Los parámetros que suelen utilizarse en los informes incluyen fechas, nombres e identificadores (Id.). Cuando se especifica un valor para un parámetro, el informe contiene solamente los datos que coinciden con el valor; por ejemplo, datos de empleados basados en un parámetro de identificador de empleado. Los parámetros se corresponden con los campos del informe. Después de especificar un parámetro, haga clic en **Ver informe** para obtener los datos.  
  
 El autor del informe define los valores de los parámetros que son válidos para cada informe. El administrador de un informe también puede establecer los valores de los parámetros. Para obtener información acerca de qué valores de parámetros son válidos para un informe, pregunte al diseñador o al administrador del informe.  
  
## <a name="credentials"></a>Credenciales  
 Las credenciales son valores de nombre de usuario y contraseña que conceden acceso a un origen de datos. Después de especificar las credenciales, haga clic en **Ver informe** para obtener los datos. Si un informe requiere que se inicie sesión, los datos que puede ver un usuario pueden ser diferentes de los datos que puede ver otro usuario. En consecuencia, dos usuarios pueden procesar el mismo informe y obtener resultados distintos. Además, algunos informes contienen áreas ocultas que se revelan en función de las credenciales de inicio de sesión del usuario o de las selecciones realizadas en el propio informe. Las áreas ocultas del informe no se incluyen en las operaciones de búsqueda, por lo que se pueden obtener resultados diferentes a cuando están visibles todas las partes del informe.  
  
## <a name="see-also"></a>Vea también  
 [Especificar información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportar informes &#40;el generador de informes SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)  
  
  