---
title: Agregar, cambiar o eliminar un mapa o una capa de mapa (generador de informes y SSRS) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rtp.rptdesigner.maplayerproperties.general.f1
- "10526"
- sql13.rtp.rptdesigner.mappolygonlayerproperties.general.f1
- "10529"
- "10525"
- "10535"
- sql13.rtp.rptdesigner.mappointlayerproperties.general.f1
- sql13.rtp.rptdesigner.shared.layerfilters.f1
- sql13.rtp.rptdesigner.maplinelayerproperties.general.f1
- "10524"
- sql13.rtp.rptdesigner.maptilelayerproperties.general.f1
- "10532"
- sql13.rtp.rptdesigner.maplayerproperties.analyticaldata.f1
- "10528"
- "10527"
- sql13.rtp.rptdesigner.shared.layervisibility.f1
ms.assetid: 6e89815e-187e-45bf-bf63-3d5c4a246360
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8c45b97760006a9939f44b41c018d04321060df9
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs"></a>Agregar, cambiar o eliminar un mapa o una capa de mapa (Generador de informes y SSRS)
  Un mapa es una colección de capas. Al agregar un mapa a un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , define la primera capa. Puede crear capas adicionales con el Asistente para capas de mapa.  
  
 La manera más fácil de agregar, quitar o cambiar las opciones de una capa es utilizar el asistente. También puede cambiar manualmente las opciones del panel Mapa. Para mostrar el panel **Mapa** , haga clic en el mapa en la superficie de diseño del informe. La figura siguiente muestra las partes del panel:  
  
 ![rsMapLayerZone](../../reporting-services/report-design/media/rsmaplayerzone.gif "rsMapLayerZone")  
  
 Las capas de mapa se dibujan desde la parte inferior a la superior en el orden en que aparecen en el panel Capa de mapa. En la figura anterior, la capa de mosaico se dibuja primero y en último lugar se dibuja la capa de polígono. Las capas que se dibujen después podrían ocultar los elementos de mapa de las capas que se dibujaron anteriormente. Puede cambiar el orden de las capas utilizando las teclas de dirección de la barra de herramientas del panel Mapa. Para mostrar u ocultar las capas, alterne el icono de visibilidad. Puede cambiar la transparencia de una capa en la página **Visibilidad** del cuadro de diálogo de propiedades de **Datos de la capa** .  
  
 En la tabla siguiente se muestran los iconos de la barra de herramientas del panel **Mapa** .  
  
|Símbolo|Description|Cuándo se usa|  
|------------|-----------------|-----------------|  
|![rs_IconMapLayerWizard](../../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")|Asistente para capas de mapa|Para agregar una capa con un asistente, haga clic en **Asistente para nueva capa**.|  
|![rs_IconMapAddLayer](../../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer")|Agregar capa|Para agregar una capa manualmente, haga clic en **Agregar capa**y, a continuación, haga clic en el tipo de capa de mapa que desea agregar.|  
|![rs_IconMapPolygonLayer](../../reporting-services/report-design/media/rs-iconmappolygonlayer.gif "rs_IconMapPolygonLayer")|Capa de polígono|Agregue una capa de mapa que muestre áreas o formas basadas en conjuntos de coordenadas de un polígono.|  
|![rs_IconMapLineLayer](../../reporting-services/report-design/media/rs-iconmaplinelayer.gif "rs_IconMapLineLayer")|Capa de línea|Agregue una capa de mapa que muestre los trazados o rutas basados en conjuntos de coordenadas de una línea.|  
|![rs_IconMapPointLayer](../../reporting-services/report-design/media/rs-iconmappointlayer.gif "rs_IconMapPointLayer")|Capa de punto|Agregue una capa de mapa que muestre las ubicaciones basadas en los conjuntos de coordenadas de un punto.|  
|![rs_IconMapTileLayer](../../reporting-services/report-design/media/rs-iconmaptilelayer.gif "rs_IconMapTileLayer")|Capa de mosaico|Agregue una capa de mapa que muestre los mosaicos de Bing Maps que correspondan al área de la vista del mapa actual que se define en la ventanilla.|  
  
 En la parte inferior del panel Mapa es el área de la vista Mapa. Para cambiar las opciones de centro o zoom del mapa, utilice las teclas de dirección para ajustar el centro de la vista y el control deslizante para ajustar el nivel de zoom.  
  
 Para obtener más información sobre las capas, vea [Mapas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="AddLayer"></a> Agregar una capa con el Asistente para capas de mapa  
  
-   De la Cinta de opciones, en el menú **Insertar** , haga clic en **Mapa**y, a continuación, haga clic en **Mapa Wizard.** . El asistente le permite agregar una capa al mapa existente. La mayor parte de las páginas son idénticas en el Asistente para mapas y el Asistente para capas de mapa.  
  
     Para obtener más información, vea [Asistente para mapas y Asistente para capas de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  
  
##  <a name="ChangeLayer"></a> Cambiar las opciones de una capa con el Asistente para capas de mapa  
  
-   Ejecute el Asistente para capas de mapa. Este asistente le permite cambiar las opciones de una capa que creó utilizando el Asistente para capas de mapa. En el panel mapa, haga clic en la capa y, en la barra de herramientas, haga clic en el botón de Asistente de capa (![rs_IconMapLayerWizard](../../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")).  
  
     Para obtener más información, vea [Asistente para mapas y Asistente para capas de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  
  
##  <a name="AddVectorLayer"></a> Agregar una capa de punto, línea o polígono desde la barra de herramientas del panel Mapa  
  
1.  Haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  En la barra de herramientas, haga clic en el botón **Agregar capa** y, en la lista desplegable, haga clic en el tipo de capa que quiere agregar: **Punto**, **Línea**o **Polígono**.  
  
    > [!NOTE]  
    >  Aunque puede agregar una capa de mapa y configurarla manualmente, recomendamos utilizar el Asistente para capas de mapa si desea agregar capas nuevas. Para iniciar el asistente desde la barra de herramientas del panel mapa, haga clic en el botón de Asistente de capa (![rs_IconMapLayerWizard](../../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard")).  
  
3.  Haga clic con el botón derecho en la capa y, después, haga clic en **Datos de la capa**.  
  
4.  En **Usar datos espaciales de**, seleccione el origen de datos espaciales. Las opciones varían en función de la selección.  
  
     Si desea ver los datos analíticos del informe en esta capa, haga lo siguiente:  
  
    1.  Haga clic en **Datos analíticos**.  
  
    2.  En **Conjunto de datos analíticos**, haga clic en el nombre del conjunto de datos que contenga los datos analíticos y en los campos coincidentes para generar una relación entre datos analíticos y datos espaciales.  
  
    3.  Haga clic en **Agregar**.  
  
    4.  Escriba el nombre del campo coincidente desde el conjunto de datos espaciales.  
  
    5.  Escriba el nombre del campo coincidente desde el conjunto de datos analíticos.  
  
     Para obtener más información sobre cómo vincular datos espaciales y analíticos, vea [Personalizar los datos y la presentación de un mapa o una capa de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="FilterAnalyticalData"></a> Para filtrar datos analíticos de la capa  
  
1.  Haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en el panel Mapa y, después, haga clic en  **Datos de la capa**.  
  
3.  Haga clic en **Filtros**.  
  
4.  Defina una ecuación de filtro para limitar los datos analíticos que se usan en la presentación del mapa. Para más información, vea [Ejemplos de ecuaciones de filtro &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
##  <a name="PointProperties"></a> Para controlar las propiedades del punto para una capa de punto o para puntos centrales de polígonos  
  
1.  Seleccione **General** en el cuadro de diálogo **Propiedades de punto de mapa** para cambiar las opciones de etiqueta, información sobre herramientas y tipo de marcador de los elementos de mapa siguientes:  
  
    -   Todos los puntos dinámicos o incrustados de una capa de punto. Las reglas de color, reglas de tamaño y reglas de tipo de marcador de los puntos invalidan estas opciones. Para invalidar las opciones de un punto incrustado concreto, utilice la página [Map Embedded Point Properties Dialog Box, Marker](http://msdn.microsoft.com/library/3c5eb1c5-d40a-424f-aa7c-43b112f42dec) .  
  
    -   El punto central de todos los polígonos dinámicos o incrustados de una capa de polígono. Las reglas de color, reglas de tamaño y reglas de tipo de marcador de los puntos centrales invalidan estas opciones. Para invalidar las opciones de un punto central concreto, use la página [Cuadro de diálogo de Propiedades de punto incrustado de mapa, Marcador](http://msdn.microsoft.com/library/3c5eb1c5-d40a-424f-aa7c-43b112f42dec) .  
  
##  <a name="Embedded"></a> Para especificar datos incrustados como un origen de datos espaciales  
  
1.  Haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa y, después, haga clic en **Datos de la capa**.  
  
3.  En **Usar datos espaciales de**, seleccione **Datos incrustado en informe**.  
  
4.  Para cargar los elementos de mapa de un informe existente o crearlos según un archivo ESRI, haga clic en **Examinar**, señale el archivo y, a continuación, haga clic en **Abrir**. Los elementos de mapa se incrustan en esta definición de informe. Los datos espaciales que señale deben coincidir con el tipo de capa. Por ejemplo, para una capa de punto, debe señalar datos espaciales que especifiquen conjuntos de coordenadas de punto.  
  
5.  En **Campo espacial**, especifique el nombre del campo que contenga los datos espaciales. Puede que tenga que determinar este nombre desde el origen de datos espaciales.  
  
    > [!NOTE]  
    >  Si no sabe el nombre del campo y buscó un archivo de forma ESRI, use la opción **Vínculo a archivo de forma ESRI** en lugar de esta.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="ESRI"></a> Especificar un archivo de forma ESRI como un origen de datos espaciales  
  
1.  Haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa y, después, haga clic en **Datos de la capa**.  
  
3.  En **Usar datos espaciales de**, seleccione **Vínculo a archivo de forma ESRI**.  
  
4.  En **Nombre de archivo**, escriba la ubicación del archivo de forma ESRI o haga clic en **Examinar** para seleccionar un archivo de forma ESRI.  
  
    > [!NOTE]  
    >  Si el archivo de forma está en el equipo local, los datos espaciales se incrustan en la definición de informe. Para recuperar los datos dinámicamente cuando se procesa el informe, debe cargar el archivo de forma ESRI .shp y su archivo auxiliar .dbf en el servidor de informes. Para obtener más información, vea cómo cargar un archivo o informe (Administrador de informes) en la [documentación de Reporting Services](http://go.microsoft.com/fwlink/?linkid=121312) , en los Libros en pantalla de SQL Server.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="DatasetField"></a> Especificar un campo de conjunto de datos de informe como un origen de datos espaciales  
  
1.  Haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa y, después, haga clic en **Datos de la capa**.  
  
3.  En **Usar los datos espaciales de**, seleccione **Campo espacial en un conjunto de datos**.  
  
4.  En **Nombre del conjunto de datos**, haga clic en el nombre de un conjunto de datos en el informe que contenga los datos espaciales que desea.  
  
5.  En **Nombre de campo espacial**, haga clic en el nombre del campo en el conjunto de datos que contenga los datos espaciales.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TileLayer"></a> Agregar una capa de mosaico  
  
1.  Haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  En la barra de herramientas, haga clic en el botón **Agregar capa** y, en la lista desplegable, haga clic en **Capa de mosaico**.  
  
    > [!NOTE]  
    >  Para obtener más información sobre el uso de mosaicos de Bing Maps en un informe, vea [Condiciones adicionales de uso](http://go.microsoft.com/fwlink/?LinkId=151371).  
  
3.  Haga clic con el botón derecho en la capa de mosaico en el panel Mapa y, después, haga clic en **Propiedades del mosaico**.  
  
4.  En **Opciones de mosaico**, seleccione un estilo de mosaico. Si los mosaicos de Bing Maps están disponibles, la capa de la superficie de diseño se actualizará con el estilo que seleccione.  
  
    > [!NOTE]  
    >  Se puede agregar también una capa de mosaico al agregar una capa de polígono, línea o punto en el Asistente para mapas o en el Asistente para capas de mapa. En la página **Elegir opciones de datos espaciales y vista de mapa** , seleccione la opción **Agregar un fondo de Bing Maps a esta vista del mapa**.  
  
##  <a name="DrawingOrder"></a> Cambiar el orden del dibujo de una capa  
  
1.  Haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic en la capa en el panel Mapa para seleccionarla.  
  
3.  En la barra de herramientas del panel Mapa, haga clic en la flecha arriba o abajo para cambiar el orden de dibujo de cada capa.  
  
##  <a name="Transparency"></a> Cambiar la transparencia de una capa de polígono, línea o punto  
  
1.  Haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa y, después, haga clic en **Datos de la capa**.  
  
3.  Haga clic en **Visibilidad**.  
  
4.  En **Opciones de transparencia**, escriba un valor que represente la transparencia en porcentaje, por ejemplo **40**. Un transparencia de cero (0)% significa que la capa es opaca. Una transparencia de 100% significa que la capa no se verá en el informe.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TileTransparency"></a> Cambiar la transparencia de una capa de mosaico  
  
1.  Haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa y, después, haga clic en **Propiedades del mosaico**.  
  
3.  Haga clic en **Visibilidad**.  
  
4.  En **Opciones de transparencia**, escriba un valor que represente la transparencia en porcentaje, por ejemplo **40**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="Secure"></a> Especificar una conexión segura para una capa de mosaico  
  
1.  Haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  En el panel Mapa, haga clic en la capa de mosaico para seleccionarla. El panel Propiedades muestra las propiedades de la capa de mosaico.  
  
3.  En el panel Propiedades, establezca UseSecureConnection en **True**.  
  
 La conexión para el servicio web de Bing Maps utilizará el servicio SSL (Capa de sockets seguros) de HTTP para recuperar mosaicos de Bing Maps para esta capa.  
  
##  <a name="Language"></a> Especificar el idioma de las etiquetas de mosaico  
  
1.  De forma predeterminada, en los estilos de mosaico que muestran etiquetas, el idioma se determina con la configuración regional predeterminada para el Generador de informes. Puede personalizar la configuración de idioma para las etiquetas de mosaico de las maneras siguientes.  
  
    -   Haga clic en el mapa fuera de la ventanilla para seleccionar el mapa. En el panel Propiedades, para la propiedad TileLanguage seleccione un valor de referencia cultural en la lista desplegable.  
  
    -   Haga clic en el fondo del informe para seleccionar el informe. En el panel Propiedades, para la propiedad Language seleccione un valor de referencia cultural en la lista desplegable.  
  
     El orden de prioridad para establecer el idioma de la etiqueta de mosaico es la propiedad de informe Language, la configuración regional predeterminada del Generador de informes y la propiedad de mapa TileLanguage.  
  
##  <a name="ConditionalHide"></a> Para ocultar una capa de forma condicional según el nivel de zoom de la ventanilla  
  
1.  Establezca las opciones de **Visibilidad** para controlar la presentación de una capa de mapa.  
  
    -   En el panel Capas de mapa, haga clic con el botón derecho en una capa para seleccionarla y, después, en la barra de herramientas Capas de mapa, haga clic en Propiedades para abrir **Propiedades de capa de mapa**.  
  
    -   Haga clic en **Visibilidad**.  
  
    -   En Visibilidad de capas, seleccione **Mostrar u ocultar en función del valor de zoom**.  
  
    -   Escriba los valores mínimo y máximo de zoom para cuando se muestre la capa.  
  
    -   Opcional. Escriba un valor para la transparencia.  
  
     También puede ocultar la capa de forma condicional. Para obtener más información, vea [Ocultar un elemento &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/hide-an-item-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Mapas &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Solucionar problemas de informes: Asignar informes &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
