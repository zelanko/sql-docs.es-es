---
title: Usar la galería de PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c9ff92d1-787a-4f34-990f-6676b61875d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f8c14a123fcdb23efade07e78dec94d242df7fc7
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175694"
---
# <a name="use-powerpivot-gallery"></a>Usar la galería de PowerPivot
  La Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] es una biblioteca de documentos de SharePoint con una finalidad especial que permite obtener una eficaz vista previa y administrar los documentos de los libros de Excel publicados y los informes de Reporting Services que contienen datos PowerPivot.

> [!NOTE]
>  Según cómo esté configurado el servidor, podría ver mensajes de error o advertencia en el área de vista previa para documentos concretos. Los mensajes pueden aparecer cuando un libro de Excel se establece para actualizar sus datos automáticamente cada vez que se abre. Los mensajes de advertencia de actualización de datos aparecerán como imagen de vista previa si Servicios de Excel está configurado para mostrar mensajes de error de advertencia de actualización de datos. Los administradores de servicios o de la granja pueden modificar la configuración para permitir que aparezca una vista previa de la hoja de cálculo real. Para obtener más información, consulte [Create a trusted location for PowerPivot sites in Central Administration](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).

##  <a name="bkmk_top"></a>En este tema

-   [Iconos de la Galería de PowerPivot](#icons)

-   [Guardar un libro de Excel en la Galería de PowerPivot](#add)

-   [Crear nuevos informes o libros basados en un libro PowerPivot publicado](#newdocs)

-   [Abrir un libro o informe en modo de página completa](#view)

-   [Programar la actualización de datos para los libros PowerPivot publicados en la Galería de PowerPivot](#newdr)

-   [Eliminar un libro o informe en la Galería de PowerPivot](#delete)

-   [Actualizar una imagen en miniatura](#image)

-   [Problemas conocidos](#bkmk_known_issues)

 [Requisitos previos](#prereq)

##  <a name="prereq"></a> Requisitos previos

> [!NOTE]
>  La Galería de Power Pivot requiere Microsoft Silverlight.  El navegador Microsoft Edge no es compatible con Silverlight. Para ver el contenido de la biblioteca en Microsoft Edge, haga clic en la pestaña **biblioteca** de la galería de Power Pivot y, a continuación, cambie la vista biblioteca de documentos a **todos los documentos**.  
> Para cambiar la vista predeterminada, haga clic en la pestaña **Biblioteca** y, después, en Modificar vista. Haga clic en "Establecer esta vista como predeterminada" y, después, en Aceptar para guardar la vista predeterminada.
> Para obtener más información sobre lo que Microsoft Edge admite, vea el blog [de Windows, un salto del pasado, parte 2: decir adiós a ActiveX, VBScript...](https://blogs.windows.com/msedgedev/2015/05/06/a-break-from-the-past-part-2-saying-goodbye-to-activex-vbscript-attachevent/)

 Para obtener una lista completa de los requisitos previos, vea [crear y personalizar la galería de PowerPivot](create-and-customize-power-pivot-gallery.md).

##  <a name="icons"></a>Iconos de la galería de PowerPivot
 Los iconos proporcionan un indicador visual sobre la disponibilidad y el estado del contenido.

|Icono|Descripción|
|----------|-----------------|
|![GMNI_PowerPivotGalleryIcon_Hourglass](../media/gmni-powerpivotgalleryicon-hourglass.gif "GMNI_PowerPivotGalleryIcon_Hourglass")|El icono de reloj de arena aparece cuando se está generando una imagen en miniatura de cada página del documento. Actualice la página para mostrar la actualización la imagen.|
|![GMNI_PowerPivotGalleryIcon_Truncated](../media/gmni-powerpivotgalleryicon-truncated.gif "GMNI_PowerPivotGalleryIcon_Truncated")|El icono de páginas aparece cuando un libro o el informe tiene más páginas de las que se pueden mostrar en la Galería de PowerPivot. Para ver todas las páginas, debe usar una aplicación cliente.|
|![GMNI_PowerPivotGalleryIcon_Error](../media/gmni-powerpivotgalleryicon-error.gif "GMNI_PowerPivotGalleryIcon_Error")|El icono de error aparece cuando no se pudo representar una imagen en miniatura para el documento. El documento se publica en la biblioteca, pero no se puede representar en las vistas personalizadas de la Galería de PowerPivot. Debe poder ver el documento en una aplicación cliente, por ejemplo el complemento PowerPivot para Excel.|
|![GMNI_PowerPivotGalleryIcon_badtype](../media/gmni-powerpivotgalleryicon-badtype.gif "GMNI_PowerPivotGalleryIcon_badtype")|El icono de contenido no disponible aparece cuando el documento que ha cargado no se puede representar en la Galería de PowerPivot. Los tipos de documento compatibles son los libros PowerPivot y los informes creados en el Generador de informes de SQL Server 2008 R2 Reporting Services.<br /><br /> Este icono también aparece si recicla un documento desde la Papelera de reciclaje.<br /><br /> Si va a obtener este icono para un documento que antes presentó una imagen de vista previa válida, puede actualizar la imagen modificando una propiedad de documento y guardando sus cambios a continuación.|
|![GMNI_PowerPivotGalleryIcon_Locked](../media/gmni-powerpivotgalleryicon-locked.gif "GMNI_PowerPivotGalleryIcon_Locked")|El icono de contenido bloqueado aparece cuando las imágenes en miniatura se deshabilitan deliberadamente para este documento. La Galería de PowerPivot no genera imágenes en miniatura para los libros de Excel que no contienen ningún dato de PowerPivot o para los libros PowerPivot o los informes de Reporting Services que no cumplen los requisitos para la generación de instantáneas. Para obtener más información, vea la sección Requisitos previos en este tema.|

##  <a name="add"></a>Guardar un libro de Excel en la galería de PowerPivot
 Puede publicar libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en la biblioteca mediante todas las técnicas de uso compartido que Excel 2010 proporciona. Por ejemplo, en Excel 2010, puede utilizar Guardar como para especificar toda o parte de una ruta de acceso de SharePoint a una biblioteca.

1.  Guarde el archivo.

2.  1.  **Excel 2010:** En el menú Archivo, haga clic en **guardar & enviar**.

    2.  Haga clic en **Guardar en SharePoint**.

    3.  Haga clic en **Opciones de publicación** si desea usar Opciones de Excel Services para seleccionar hojas o parámetros individuales que desee publicar. Por ejemplo, la pestaña Parámetros de Opciones de Excel Services le permite elegir qué segmentaciones de datos aparecen en el libro publicado.

    1.  **Excel 2013:**  En el menú Archivo, haga clic en **Guardar**.

    2.  Haga clic en **Opciones de vista de explorador** si desea usar Opciones de Excel Services para seleccionar hojas o parámetros individuales que desee publicar. Por ejemplo, la pestaña Parámetros de Opciones de Excel Services le permite elegir qué segmentaciones de datos aparecen en el libro publicado.

3.  En el cuadro de diálogo Guardar como, en Nombre de archivo, escriba una dirección URL completa o parcial para la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Si escribe una parte de la dirección URL, como el nombre del servidor, puede examinar el sitio para encontrar la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para ello, haga clic en **Guardar** para abrir una conexión al servidor que especificó.

     ![GMNI_ExcelSaveAs](../media/gmni-excelsaveas.gif "GMNI_ExcelSaveAs")

1.  Con el cuadro de diálogo Guardar como, seleccione la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] del sitio.

2.  Haga clic en **Abrir** para abrir la biblioteca.

3.  Haga clic en **Guardar** para publicar el libro en la biblioteca.

 En una ventana del explorador, compruebe que el documento aparece en la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Los documentos publicados recientemente aparecerán en la lista. La configuración de la biblioteca determina dónde aparece el documento (por ejemplo, clasificado en orden ascendente por fecha o alfabéticamente por nombre). Podría necesitar actualizar la ventana del explorador para ver las incorporaciones más recientes.

#### <a name="upload-a-workbook-into-powerpivot-gallery"></a>Cargar un libro en la Galería de PowerPivot
 También puede cargar un libro si desea partir de SharePoint y seleccionar en el equipo qué archivo publicar.

1.  En un sitio de SharePoint, abra la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .

2.  En la cinta de opciones Biblioteca, haga clic en **Documentos**.

3.  En **Cargar documento**, seleccione una opción de carga y, a continuación, escriba el nombre y la ubicación del archivo que desea cargar. La configuración de la biblioteca determina dónde aparece el documento. Puede que tenga que actualizar la ventana del explorador para ver la incorporación más reciente.

##  <a name="newdocs"></a>Crear nuevos informes o libros basados en un libro PowerPivot publicado
 En el caso de los libros de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que publique en la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , puede crear libros adicionales o informes de Reporting Services que usen el libro publicado como origen de datos conectado.

|||
|-|-|
|![GMNI_btn_NewDocReportGallery](../media/gmni-btn-newdocreportgallery.gif "GMNI_btn_NewDocReportGallery")|Haga clic en la parte de la flecha descendente del botón Nuevo informe para iniciar el Generador de informes o Excel 2010. La Galería de PowerPivot debe usar una de las vistas prediseñadas (Teatro, Galería o Carrusel) para que el botón Nuevo informe esté disponible.|

#### <a name="create-report-builder-report"></a>Crear un informe con el Generador de informes
 Crear un nuevo informe basado en un libro PowerPivot existente en la biblioteca requiere que Reporting Services esté configurado para la integración de SharePoint para los mismos sitios que contienen la Galería de PowerPivot. Al seleccionar la opción Crear informe del Generador de informes, este se descarga del servidor de informes y se instala en la estación de trabajo local cuando se usa por primera vez. Se crea un archivo de informe del marcador de posición para el nuevo informe y se guarda en la Galería de PowerPivot. La información de conexión al libro PowerPivot se crea automáticamente como un nuevo origen de datos en el informe. Como paso siguiente, puede integrar los conjuntos de datos y el diseño del informe en el área de trabajo de diseño. Cuando use el Generador de informes para ensamblar un informe, puede guardar los cambios y el resultado final en el documento de informe, en la galería. Para evitar desconexiones de datos posteriores, asegúrese de mantener unidos los archivos de libro e informe en la misma biblioteca.

#### <a name="open-new-excel-workbook"></a>Abrir nuevo libro de Excel
 Para crear un nuevo libro de Excel a partir de un libro existente, ya debe tener Excel y [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] en el equipo local. Al elegir Abrir nuevo libro de Excel se inicia Excel, se abre un archivo de libro en blanco (.xlsx) y se cargan en segundo plano los datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] como un origen de datos conectado. En el libro nuevo solo se utilizan los datos de la ventana PowerPivot del libro original. Se excluyen las tablas dinámicas o los gráficos dinámicos del libro original. El nuevo libro se vincula a los datos del libro original. Los datos no se copian en el nuevo libro.

##  <a name="view"></a>Abrir un libro o informe en modo de página completa
 Haga clic en cualquier imagen en miniatura visible del documento del que se ha obtenido la vista previa para abrirlo en el modo de página completa, independientemente de la vista previa de la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se abrirán en un explorador. Los informes de Reporting Services se abrirán en el componente web del visor de informes que forma parte de la implementación de Reporting Services en un servidor de SharePoint.

 Una solución alternativa a ver el libro en un explorador es abrirlo en Excel en una estación de trabajo del cliente. Debe tener Excel 2013 o Excel 2010 y el complemento [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] para ver el archivo. Puede utilizar Excel 2007 para abrir el archivo, pero no puede utilizarlo para dinamizar los datos. Por esta razón se recomienda Excel 2013 o Excel 2010 tanto para ver como para crear datos PowerPivot. Si no tiene las aplicaciones necesarias, debe utilizar un explorador para ver el libro de SharePoint.

##  <a name="newdr"></a>Programar la actualización de datos para los libros PowerPivot en la galería de PowerPivot
 
  [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un libro de Excel publicado pueden actualizarse a los intervalos programados.

|||
|-|-|
|![GMNI_btn_NewDataRefreshReportGallery](../media/gmni-btn-newdatarefreshreportgallery.gif "GMNI_btn_NewDataRefreshReportGallery")|Haga clic en el botón Administrar datos para crear o ver una programación que recupere los datos actualizados de los orígenes de datos conectados. Para obtener instrucciones sobre cómo crear una programación, vea [programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md).|

##  <a name="delete"></a>Eliminar un libro o informe en la galería de PowerPivot
 Para eliminar un documento de la biblioteca, cambie primero a la vista Todos los documentos.

1.  En un sitio de SharePoint, abra la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .

2.  En la cinta de opciones, haga clic en **Biblioteca**.

3.  En Administrar vistas, en la lista Vista actual, haga clic en la flecha abajo y seleccione Todos los documentos.

4.  Seleccione el libro o informe que desea eliminar.

5.  En Documentos (archivos), en Administrar, haga clic en el botón **Eliminar documento** .

##  <a name="image"></a>Actualizar una imagen en miniatura
 Utilice los siguientes pasos para regenerar una imagen en miniatura para un documento de la Galería de PowerPivot.

1.  Cambie la Galería de PowerPivot a la vista Todos los documentos. Para ello, haga clic en **Biblioteca** en la cinta de opciones y cambie la **Vista Actual** a **Todos los documentos**.

2.  Seleccione el libro o informe para el que desea actualizar la imagen en miniatura.

3.  Haga clic en la flecha abajo a la derecha y seleccione **Modificar propiedades**.

4.  Haga clic en **Save**(Guardar). Al guardar el documento, obliga al servicio de instantánea a regenerar la imagen de vista previa.

##  <a name="bkmk_known_issues"></a>Problemas conocidos

### <a name="document-type-is-not-supported"></a>El tipo de documento no se admite
 No se admite el tipo de contenido **Documento de galería de PowerPivot** . Si habilita el tipo de contenido **Documento de galería de PowerPivot** para una biblioteca de documentos e intenta crear un nuevo documento de ese tipo, verá un mensaje de error similar al siguiente:

-   ' Nuevo documento ' requiere una aplicación compatible con Microsoft SharePoint Foundation y un explorador Web. Para agregar un documento a esta biblioteca de documentos, haga clic en el botón ' cargar documento '.

-   "La dirección de Internet ' http://[nombre de servidor]/TestSite/PowerPivot Gallery Gallery/ReportGallery/Forms/template. xlsx ' no es válida." " Microsoft Excel no puede acceder al archivo ' http://[nombre de servidor]/TestSite/PowerPivot Gallery Gallery/ReportGallery/Forms/template. xlsx '. Existen varias razones posibles:

 El tipo de contenido **Documento de galería de PowerPivot** no se agrega automáticamente a las bibliotecas de documentos. No encontrará este problema a menos que habilite manualmente el tipo de contenido no admitido.

## <a name="see-also"></a>Consulte también
 [Crear una ubicación de confianza para los sitios de PowerPivot en administración central](create-a-trusted-location-for-power-pivot-sites-in-central-administration.md) [eliminar la galería de PowerPivot](delete-power-pivot-gallery.md) [crear y personalizar la galería de PowerPivot](create-and-customize-power-pivot-gallery.md) [programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)

