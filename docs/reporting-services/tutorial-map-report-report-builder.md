---
title: 'Tutorial: Informe de asignaciones (Generador de informes) | Microsoft Docs'
description: Obtenga información sobre las características de mapa que puede usar para mostrar datos sobre un fondo geográfico en un informe paginado de Reporting Services.
ms.date: 08/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a8977a2b0b90a83e920452d2a843d0c035440113
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945231"
---
# <a name="tutorial-map-report-report-builder"></a>Tutorial: Informe de asignaciones (Generador de informes)
En este tutorial de [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] , obtendrá información sobre las características de mapa que puede usar para mostrar datos en un fondo geográfico de un informe paginado de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . 
  
Los mapas están basados en datos espaciales que normalmente está compuestos de puntos, líneas y polígonos. Por ejemplo, un polígono puede representar el perfil de un condado, una línea puede representar una carretera y un punto puede representar la ubicación de una ciudad. Cada tipo de datos espaciales se muestra en una capa de mapa independiente, como un conjunto de elementos de mapa.  
  
Para variar la apariencia de los elementos de mapa, especifique un campo que tenga valores que hagan coincidir los elementos de mapa con los datos analíticos de un conjunto de datos. También puede definir las reglas que varían el color, tamaño u otras propiedades basadas en rangos de datos.  

![report-builder-map-final-map-only](../reporting-services/media/report-builder-map-final-map-only.png)
  
En este tutorial, compilará un informe de mapa que muestre ubicaciones de almacenes en los condados del Estado de Nueva York.  
   
> [!NOTE]  
> En este tutorial, los pasos del asistente se fusionan en dos procedimientos: uno para crear el conjunto de datos y otro para crear una tabla. Para obtener instrucciones paso a paso sobre cómo ir hasta un servidor de informes, elegir un origen de datos, crear un conjunto de datos y ejecutar el asistente, vea el primer tutorial de esta serie: [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tiempo estimado para completar este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para este tutorial, deberá configurarse el servidor de informes para que admita los mapas de Bing como fondo. Para obtener más información, consulte [Planear la compatibilidad de informe de mapa](https://docs.microsoft.com/sql/reporting-services/report-design/plan-a-map-report-report-builder-and-ssrs). 

Para obtener información sobre otros requisitos, consulte [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="1-create-a-map-with-a-polygon-layer-from-the-map-wizard"></a><a name="Map"></a>1. Crear un mapa con una capa de polígono desde el Asistente para mapas  
En esta sección, agregará un mapa al informe desde la galería de mapas. El mapa tiene una capa que muestra los condados del Estado de Nueva York. La forma de cada condado es un polígono basado en los datos espaciales que se incrustan en el mapa desde la galería de mapas.  
  
### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>Para agregar un mapa con el Asistente para mapas en un informe nuevo  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el equipo, el portal web de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o el modo integrado de SharePoint.  
  
    Se abre el cuadro de diálogo **Nuevo informe o conjunto de datos** .  
  
    Si no ve el cuadro de diálogo **Nuevo informe o conjunto de datos**, vaya al menú **Archivo** > **Nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel derecho, haga clic en **Asistente para mapas**.  
  
4.  En la página **Elegir un origen de datos espaciales** , compruebe que está seleccionado **Galería de mapas** .  
  
6.  En el cuadro Galería de mapas, expanda **Estados por condado** en **EE.UU.** y haga clic en **Nueva York**.  
  
    El panel Vista previa del mapa muestra el mapa del condado de Nueva York.  
    
    ![report-builder-map-ny-counties](../reporting-services/media/report-builder-map-ny-counties.png)
  
7.  Haga clic en **Next**.  
  
8.  En la página **Elegir opciones de datos espaciales y vista de mapa** , acepte los valores predeterminados y haga clic en **Siguiente**. 
 
    De forma predeterminada, los elementos de mapa de una galería de mapas se incrustan automáticamente en la definición de informe.  
  
9. En la página **Elegir visualización de mapa** , compruebe que la opción **Mapa básico** está seleccionada y haga clic en **Siguiente**.  
  
11. En la página **Elegir tema de color y visualización de datos** , seleccione la opción **Mostrar etiquetas** .  
  
12. Si está seleccionada, desactive la opción **Mapa de un color** .  
  
13. En la lista desplegable **Campo de datos** , haga clic en **#COUNTYNAME**. El panel Vista previa del mapa del asistente muestra los elementos siguientes:  
  
    -   Un título con el texto **Título del mapa**.  
  
    -   Un mapa que muestra los condados de Nueva York, donde cada condado es de un color diferente y su nombre aparece siempre que se pasa el puntero sobre el área del condado.  
  
    -   Una leyenda que contiene un título y una lista de los elementos 1 a 5.  
  
    -   Una escala de colores que contiene los valores 0 a 160 y ningún color.  
  
    -   Una escala de distancia que muestra kilómetros (km) y millas (mi).  
    
    ![report-builder-map-choose-color-theme](../reporting-services/media/report-builder-map-choose-color-theme.png)
  
14. Haga clic en **Finalizar**  
  
    Se agrega el mapa a la superficie de diseño.  
  
13. Seleccione el texto "Título del mapa" y escriba **Ventas por almacén** > ENTRAR.  

15. Haga doble clic en el mapa para mostrar el panel **Capas de mapa**. El panel **Capas de mapa** muestra una capa de polígono, PolygonLayer1, del tipo **Insertada**. Cada condado es un elemento de mapa incrustado en esta capa.  
  
    > [!NOTE]  
    > Si no ve el panel **Capas de mapa** , quizá se esté mostrando fuera de su vista actual. Use la barra de desplazamiento de la parte inferior de la ventana de la vista Diseño para cambiar la vista. O bien, en la pestaña **Ver** , desactive la opción **Datos del informe** para proporcionar una mayor área de diseño expuesta.   

15. Seleccione la flecha situada junto a PolygonLayer1 > **Propiedades del polígono**.

16. En la pestaña **Fuente** , modifique el color por **Gris pálido**.

17. En la pestaña **Inicio** > **Ejecutar** para obtener una vista previa del informe.  
  
    ![report-builder-map-first-preview](../reporting-services/media/report-builder-map-first-preview.png)
  
El informe representado muestra el título del mapa, el mapa y la escala de distancia. Los condados están en una capa de polígono de mapa. Cada condado es un polígono que varía según el color de una paleta de colores, pero los colores no están asociados a ningún dato. La escala de distancia muestra las distancias en kilómetros y millas.  
  
La leyenda de mapa y la escala del color no aparecen todavía, porque no hay datos analíticos asociados a cada condado. Agregará los datos analíticos posteriormente en este tutorial.  
  
## <a name="2-add-a-map-point-layer-to-display-store-locations"></a><a name="PointLayer"></a>2. Agregar una capa de punto de mapa para mostrar las ubicaciones del almacén  
En esta sección, usará el asistente para capas de mapa para agregar una capa de punto que muestre las ubicaciones de almacenes.  
  
> [!NOTE]  
> En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>Para agregar una capa de punto según una consulta espacial de SQL Server  
  
1.  En la pestaña **Ejecutar** > **Diseño** para volver a cambiar a la vista Diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capas de mapa** . En la barra de herramientas, haga clic en el botón **Asistente para nueva capa** ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard"). 

    ![report-builder-map-new-layer-wizard-icon](../reporting-services/media/report-builder-map-new-layer-wizard-icon.png) 
  
3.  En la página **Elegir un origen de datos espaciales** , seleccione **Consulta espacial de SQL Server**y haga clic en **Siguiente**.  
  
4.  En la página **Elija un conjunto de datos con datos espaciales de SQL Server** , haga clic en **Agregar un nuevo conjunto de datos con datos espaciales de SQL Server** > **Siguiente**.  
  
5.  En la página **Elegir una conexión con un origen de datos espaciales de SQL Server** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos.  

    > [!NOTE]  
    > El origen de datos que elija no importa, con tal de que tenga los permisos adecuados. No está recibiendo datos del origen de datos. Para obtener más información, consulte [Maneras alternativas de obtener una conexión de datos &#40;Generador de informes&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  Haga clic en **Next**.  
  
7.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
8.  Copie el texto siguiente y péguelo en el panel de consulta:  
  
    ```  
    Select 114 as StoreKey, 'Contoso Albany Store' as StoreName, 1125 as SellingArea, 'Albany' as City, 'Albany' as County,   
     CAST(1000000 as money) as Sales, CAST('POINT(-73.7472924218681 42.6564617079878)' as geography) AS SpatialLocation  
    UNION ALL SELECT 115 AS StoreKey, 'Contoso New York No.1 Store' AS  StoreName, 500 as SellingArea, 'New York' AS City, 'New York City' as County,  
     CAST('2000000' as money) as Sales, CAST('POINT(-73.9922069374483 40.7549638237402)' as geography) AS SpatialLocation  
    UNION ALL Select 116 as StoreKey, 'Contoso Rochester No.1 Store' as StoreName, 462 as SellingArea, 'Rochester' as City,  'Monroe' as County,    
     CAST(3000000 as money) as Sales, CAST('POINT(-77.624041566786 43.1547066024338)' as geography)  AS SpatialLocation  
    UNION ALL Select 117 as StoreKey, 'Contoso New York No.2 Store' as StoreName, 700 as SellingArea, 'New York' as City,'New York City' as County,    
      CAST(4000000 as money) as Sales, CAST('POINT(-73.9712488 40.7830603)' as geography) AS SpatialLocation  
    UNION ALL Select 118 as StoreKey, 'Contoso Syracuse Store' as StoreName, 680 as SellingArea, 'Syracuse' as City, 'Onondaga' as County,  
     CAST(5000000 as money) as Sales, CAST('POINT(-76.1349120532546 43.0610223535974)' as geography) AS SpatialLocation  
    UNION ALL Select 120 as StoreKey, 'Contoso Plattsburgh Store' as StoreName, 560 as SellingArea, 'Plattsburgh' as City,  'Clinton' as County,  
     CAST(6000000 as money) as Sales, CAST('POINT(-73.4728622833178 44.7028831413324)' as geography) AS SpatialLocation  
    UNION ALL Select 121 as StoreKey, 'Contoso Brooklyn Store' as StoreName, 1125 as SellingArea, 'Brooklyn' as City, 'New York City' as County,  
     CAST(7000000 as money) as Sales, CAST('POINT (-73.9638533447143 40.6785123489351)' as geography) AS SpatialLocation  
    UNION ALL Select 122 as StoreKey, 'Contoso Oswego Store' as StoreName, 500 as SellingArea, 'Oswego' as City, 'Oswego' as County,    
     CAST(8000000 as money) as Sales, CAST('POINT(-76.4602850815536 43.4353224527794)' as geography) AS SpatialLocation  
    UNION ALL Select 123 as StoreKey, 'Contoso Ithaca Store' as StoreName, 460 as SellingArea, 'Ithaca' as City, 'Tompkins' as County,  
     CAST(9000000 as money) as Sales, CAST('POINT(-76.5001866085881 42.4310489934743)' as geography) AS SpatialLocation  
    UNION ALL Select 124 as StoreKey, 'Contoso Buffalo Store' as StoreName, 700 as SellingArea, 'Buffalo' as City, 'Erie' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-78.8784 42.8864)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. En la barra de herramientas del diseñador de consultas, haga clic en **Ejecutar** ( **!** ).  
  
    El conjunto de resultados contiene siete columnas que representan un conjunto de almacenes del estado de Nueva York que venden bienes de consumo. Aquí tiene una lista, con explicaciones de las que quizás no sean obvias: 
    *   **StoreKey**: un identificador del almacén.  
    *   **StoreName**.
    *   **SellingArea**: el área disponible para la visualización del producto, que va de 138 a 342 metros cuadrados.
    *   **City**.
    *   **County**.
    *   **Ventas**: Ventas totales. 
    *   **SpatialLocation**: ubicación en longitud y latitud. 

    ![report-builder-map-design-query](../reporting-services/media/report-builder-map-design-query.png) 
  
10. Haga clic en **Next**.  
  
    Se ha creado el conjunto de datos de informe denominado DataSet1. Después de completar el asistente, puede usar la colección de campos del panel Datos de informe.  
  
11. En la página **Elegir opciones de datos espaciales y vista de mapa** , compruebe que el **Campo espacial** es **SpatialLocation** y que el **Tipo de capa** es **Punto**. Acepte los demás valores predeterminados de esta página.  
  
    La vista de mapa muestra círculos para marcar la ubicación de cada almacén.  
  
12. Haga clic en **Next**.  
  
13. En la página Elegir visualización de mapa, haga clic en **Mapa de burbujas** para un tipo de mapa que muestra marcadores que varían de tamaño, según los datos. Haga clic en **Next**.  
  
14. En la página **Elegir el conjunto de datos analíticos** , haga clic en DataSet1 y, después, en **Siguiente**. Este conjunto de datos contiene datos analíticos y datos espaciales que se mostrarán en la nueva capa de punto.   
  
16. En la página **Elegir tema de color y visualización de datos** , seleccione **Usar tamaño de burbuja para visualizar datos**.  
  
17. En **Campo de datos**, seleccione `[Sum(SellingArea)]` para variar los tamaños de burbuja según el tamaño del área que un almacén separa para mostrar productos.  
  
18. Seleccione **Mostrar etiquetas**y, en **Campo de datos**, seleccione `[City]`.

18. Haga clic en **Finalizar**  
  
    La capa de mapa se agrega al informe. La leyenda muestra los tamaños de burbuja según los valores de SellingArea.  
  
 19. Haga doble clic en el mapa para mostrar el panel **Capa de mapa** . El panel **Capa de mapa** muestra una nueva capa, PointLayer1, con el tipo de origen de datos espaciales **DataRegion**.  
  
19. Agregue un título a la leyenda. En la leyenda, seleccione el texto **Título**, escriba **Área de visualización (metros cuadrados)** y pulse ENTRAR.  
  
21. En el **panel Capas de mapa**, haga clic en la flecha situada junto a PointLayer1 y luego haga clic en **Propiedades del punto**.  

    ![report-builder-map-point-properties](../reporting-services/media/report-builder-map-point-properties.png)
  
22. En la pestaña **Fuente** , elija el estilo **Negrita** y el tamaño **10pt**.

    ![report-builder-map-point-properties-font](../reporting-services/media/report-builder-map-point-properties-font.png)
  
23. En la pestaña **General** , seleccione **Inferior** en **Colocación**.

24. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. Haga clic en **Ejecutar** para obtener la vista previa del informe.  

    ![report-builder-map-city-names](../reporting-services/media/report-builder-map-city-names.png)
  
    El mapa muestra las ubicaciones de los almacenes del Estado de Nueva York. El tamaño de marcador para cada almacén se basa en el área de visualización. Se calcularon automáticamente para usted cinco rangos de área de presentación.


  
## <a name="3-add-a-map-line-layer-to-display-a-route"></a><a name="LineLayer"></a>3. Agregar una capa de línea de mapa para mostrar una ruta  
Use el Asistente para capas de mapa para agregar una capa de mapa que muestre una ruta entre dos almacenes. En este tutorial, la ruta de acceso se crea a partir de tres ubicaciones de almacén. En una aplicación empresarial, la ruta podría ser la ruta mejor entre los almacenes.  
  
### <a name="to-add-a-line-layer-to-map"></a>Para agregar una capa de línea al mapa  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** . En la barra de herramientas, haga clic en el botón **Asistente para nueva capa** ![rs_IconMapLayerWizard](../reporting-services/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard").  
  
3.  En la página **Elegir un origen de datos espaciales** , seleccione **Consulta espacial de SQL Server** y haga clic en **Siguiente**.  
  
4.  En la página **Elija un conjunto de datos con datos espaciales de SQL Server** , haga clic en **Agregar un nuevo conjunto de datos con datos espaciales de SQL Server** y haga clic en **Siguiente**.  
  
5.  En **Elegir una conexión con un origen de datos espaciales de SQL Server**, seleccione el origen de datos que ha usado en el primer procedimiento.  
  
6.  Haga clic en **Next**.  
  
7.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**. El diseñador de consultas cambia al modo basado en texto.  
  
8.  Pegue el texto siguiente en el panel de consulta:  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. Haga clic en **Next**.  
  
    En el mapa aparece una ruta de acceso que conecta tres almacenes.  
  
10. En la página **Elegir opciones de datos espaciales y vista de mapa** , compruebe que el **Campo espacial** es **Route** y que el **Tipo de capa** es **Línea**. Acepte los otros valores predeterminados.  
  
    La vista de mapa muestra una ruta desde un almacén de la parte septentrional del Estado de Nueva York a otro de la parte meridional.  
  
11. Haga clic en **Next**.  
  
12. En la página **Elegir visualización de mapa** , haga clic en **Mapa de líneas básico**y, después, en **Siguiente**.  
  
13. En **Elegir tema de color y visualización de datos**, seleccione la opción **Mapa de un color**. La ruta aparece en un color basado en el tema seleccionado.  
  
14. Haga clic en **Finalizar**  

    ![report-builder-map-line](../reporting-services/media/report-builder-map-line.png)
  
     El mapa muestra una nueva capa de línea con el tipo de origen de datos espaciales **DataRegion**. En este ejemplo, los datos espaciales proceden de un conjunto de datos, pero ningún dato analítico se asocia a la línea.  

## <a name="adjust-the-zoom"></a>Ajustar el zoom
1. Si no puede ver el estado completo de Nueva York, puede ajustar el zoom. Con el mapa seleccionado, en el panel Propiedades verá propiedades de **MapViewport** . 

15. Expanda la sección **Ver** y, después, expanda **Ver** para que pueda ver la propiedad **Zoom** . Establézcalo en **125**. 

    ![report-builder-map-zoom](../reporting-services/media/report-builder-map-zoom.png)

      Este es el porcentaje de zoom. En 125 %, debería ver el estado completo.
  
## <a name="4-add-a-bing-maps-tile-background"></a><a name="TileLayer"></a>4. Agregar un fondo de mosaico de Bing Maps  
En esta sección, agregará una capa de mapa que muestre un fondo de mosaico de Mapas de Bing.  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** . En la barra de herramientas, haga clic en **Agregar capa** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer").  
  
3.  En la lista desplegable, haga clic en **Capa de mosaico**.  
  
    La última capa del panel **Capa de mapa** es TileLayer1. De forma predeterminada, la capa de mosaico muestra el estilo de mapa de carreteras.  
  
    > [!NOTE]  
    > En el asistente, también puede agregar una capa de mosaico en la página **Elegir opciones de datos espaciales y vista de mapa** . Para ello, seleccione **Agregar un fondo de Bing Maps a esta vista de mapa**. En un informe representado, el fondo de mosaico muestra mosaicos de Bing Maps en el centro de la ventanilla del mapa actual y en el nivel de zoom.  
  
4.  Haga clic en la flecha situada junto a TileLayer1 > **Propiedades del mosaico**.  
  
5.  En la pestaña **General** , en **Tipo**, seleccione **Aéreo**. La vista aérea no contiene texto.  

    ![report-builder-map-bing-aerial](../reporting-services/media/report-builder-map-bing-aerial.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="5-make-a-layer-transparent"></a><a name="Transparent"></a>5. Hacer una capa transparente  
En esta sección, para permitir que los elementos de una capa se muestren a través de otra capa, puede ajustar el orden y la transparencia de las capas para obtener el efecto que quiere. Empiece con la primera capa que ha creado, PolygonLayer1. 
  
1.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** .  
  
3.  Haga clic en la flecha situada junto a PolygonLayer1 > **Datos de la capa**. Se abre el cuadro de diálogo **Propiedades de capa de polígono de mapa** .  
  
4.  En la pestaña **Visibilidad** , en **Transparencia (porcentaje)** , escriba **30**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     La superficie de diseño muestra los condados como semitransparentes.  

    ![report-builder-map-transparency](../reporting-services/media/report-builder-map-transparency.png)
  
## <a name="6-vary-county-color-based-on-sales"></a><a name="Vary"></a>6. Variar los colores de condado de acuerdo con las ventas  
Cada condado de la capa de polígono tiene un color diferente porque el procesador de informes asigna automáticamente un valor de color de la paleta de colores en función del tema que eligió en la última página del Asistente para mapas.  
  
En esta sección, especifique una regla de color para asociar colores concretos a un rango de ventas de almacén para cada condado. Los colores rojo, verde y amarillo indican unas ventas anuales altas, medias o bajas relativas. Dé formato a la escala de colores para mostrar la moneda. Muestre los rangos de ventas anuales en una nueva leyenda. En los condados que no contengan almacenes, no use ningún color para mostrar que no hay ningún dato asociado.  
  
### <a name="6a-build-a-relationship-between-spatial-and-analytical-data"></a><a name="Relationship"></a>6a. Compilar una relación entre los datos espaciales y los datos analíticos  
Para variar las formas del condado por el color según los datos analíticos, debe asociar primero los datos analíticos a los datos espaciales. En este tutorial, utilizará el nombre del condado para la coincidencia. 
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capas de mapa** .  
  
3.  Haga clic en la flecha situada junto a PolygonLayer1 y, después, haga clic en **Datos de la capa**. Se abre el cuadro de diálogo **Propiedades de capa de polígono de mapa** .  
  
4.  En la pestaña **Datos analíticos** , en **Conjunto de datos analíticos**, seleccione DataSet1. El asistente ha creado este conjunto de datos al crear la consulta de datos espaciales para los condados.  
  
6.  En **Campos en los que establecer coincidencias**, haga clic en **Agregar**. Se agrega una nueva fila.  
  
7.  En **Desde el conjunto de datos espaciales**, haga clic en COUNTYNAME.  
  
8.  En **Desde el conjunto de datos analíticos**, haga clic en [County].  

    ![report-builder-map-county-colors](../reporting-services/media/report-builder-map-county-colors.png)
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Obtenga una vista previa del informe.  

    ![report-builder-map-county-highlight](../reporting-services/media/report-builder-map-county-highlight.png)
  
Al especificar un campo coincidente del origen de datos espaciales y el conjunto de datos analíticos, el procesador de informes puede agrupar los datos analíticos según los elementos de mapa. Un elemento de mapa enlazado a datos tiene una coincidencia correcta para los valores que especificó.  
  
Cada condado que contiene un almacén tiene un color que está basado en la paleta de colores correspondiente el estilo que eligió en el asistente. Los demás condados aparecen en gris.  
  
### <a name="6b-specify-color-rules-for-polygons"></a><a name="ColorRules"></a>6b. Especificar las reglas de color para polígonos  
Para crear una regla que varía el color de cada condado basándose en las ventas por almacén, debe especificar los valores de rango, el número de divisiones dentro de ese rango que desea mostrar y los colores que se van a usar.  
  
#### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>Especificar las reglas de color para todos los polígonos que tienen datos asociados  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga clic en la flecha situada junto a PolygonLayer1 y, después, haga clic en **Regla de color de polígono**. El cuadro de diálogo **Propiedades de reglas de color de mapa** se abre. Observe que la opción de la regla de color **Visualizar datos mediante la paleta de colores** está seleccionada. Esta opción se estableció en el asistente.  
  
3.  Seleccione **Visualizar datos mediante los rangos de colores**. La opción de la paleta se reemplaza con las opciones de color inicial, color intermedio y color final.  
  
4.  Defina los valores de rango para las ventas de cada condado. En **Campo de datos**, en la lista desplegable, seleccione `[Sum(Sales)]`.  
  
5.  Para cambiar el formato para mostrar la moneda en millares, cambie la expresión a la siguiente: `=Sum(Fields!Sales.Value)/1000`  
  
6.  Cambie **Color inicial** a **Rojo**.  
  
7.  Cambie **Color final** a **Verde**.  
  
    **Rojo** representa valores de ventas bajos, **Amarillo** representa valores de ventas intermedios y **Verde** representa valores de ventas altos. El procesador de informes calcula un rango de colores según estos valores y las opciones que elija en la página **Distribución** .  
    
    ![report-builder-map-county-color-rules](../reporting-services/media/report-builder-map-county-color-rules.png)
  
8.  Haga clic en **Distribución**.  
  
9. Compruebe que el tipo de distribución es **Óptimo**. Para la expresión del paso 5, la distribución óptima divide los valores en subrangos que equilibren el número de elementos y la amplitud de cada rango.  
  
10. Acepte los valores predeterminados de las demás opciones de esta página. Al seleccionar el tipo de distribución óptimo, el número de subrangos se calcula cuando se ejecuta el informe.  
  
11. Haga clic en **Leyenda**.  
  
12. En **Opciones de escala de colores**, compruebe que la opción **Mostrar en escala de colores** está seleccionada.  
  
13. En **Mostrar en esta leyenda**, en la lista desplegable, seleccione la línea en blanco. Por ahora, mostrará los rangos de colores solo en la escala de colores.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  

15. Obtenga una vista previa del informe.

    ![report-builder-map-county-color-rule-preview](../reporting-services/media/report-builder-map-county-color-rule-preview.png)
  
    La escala de colores muestra cuatro colores: rojo, naranja, amarillo y verde. Cada color representa un rango de ventas que se calcula automáticamente de acuerdo con las ventas por condado.  
  
### <a name="6c-format-the-data-in-the-color-scale-as-currency"></a><a name="ColorScale"></a>6c. Dar formato a los datos en la escala de color como moneda  
De forma predeterminada, los datos tienen un formato general. En esta sección, aplicará formatos personalizados.  
  
1. Cambie a la vista de diseño.  

2. Seleccione la escala de colores. En la pestaña **Inicio** > sección **Número**, haga clic en **Moneda**.  
  
4.  Aún en la sección **Número** , haga clic en el botón **Disminuir decimales** dos veces.  
  
    La escala de colores muestra las ventas anuales en el formato de moneda para cada rango.  
  
### <a name="6d-add-a-legend-title"></a><a name="NewLegend"></a>6d. Agregar un título a la leyenda   
  
1.  Con la escala de colores aún seleccionada, en el panel Propiedades verá las propiedades de **MapColorScale**. 
  
2. Expanda la sección Título y, en la propiedad Leyenda, escriba **Ventas (miles)** .

3. Cambie la propiedad TextColor a **Blanco**.  

    ![report-builder-map-color-scale-title](../reporting-services/media/report-builder-map-color-scale-title.png)
  
8.  Obtenga una vista previa del informe.  
  
Los condados que tienen asociados almacenes y ventas se muestran e acuerdo con las reglas de color. Los condados que no tienen ventas tampoco tienen un color.  
  
### <a name="6f-change-color-for-counties-with-no-data"></a><a name="NoData"></a>6f. Cambiar el color en los condados sin datos  
Puede configurar las opciones de presentación predeterminadas para todos los elementos de mapa de una capa. Las reglas de color tienen prioridad sobre estas opciones de presentación.  
  
#### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>Para establecer las propiedades de presentación de todos los elementos de una capa  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** .  
  
3.  Haga clic en la flecha abajo en PolygonLayer1 y, a continuación, haga clic en **Propiedades del polígono**. 

     ![report-builder-map-polygon-layer-properties](../reporting-services/media/report-builder-map-polygon-layer-properties.png)

     El cuadro de diálogo **Propiedades de polígono de mapa** se abre. Las opciones de presentación configuradas en este cuadro de diálogo se aplican a todos los polígonos de la capa antes de que se apliquen las opciones de presentación basadas en reglas.  
  
4.  En la pestaña **Relleno** , compruebe que el estilo de relleno es **Sólido.** Los degradados y patrones se aplican a todos los colores.  
  
6.  En **Color**, seleccione **Azul acero claro**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Obtenga una vista previa del informe.  
  
Los condados que no tienen datos asociados se muestran como azul grisáceo. Solo los condados que tienen datos analíticos asociados tienen los colores **Rojo** a **Verde** de las reglas de color que ha especificado.  
  
## <a name="7-add-a-custom-point"></a><a name="CustomPoint"></a>7. Agregar un punto personalizado  
Para representar un nuevo almacén que aún no se ha generado, en esta sección especificará un punto con el tipo de marcador **Estrella** .  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** . En la barra de herramientas, haga clic en **Agregar capa** ![rs_IconMapAddLayer](../reporting-services/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer") y después en **Capa de punto**.  
  
    Una nueva capa de punto se agrega al mapa. De forma predeterminada, la capa de punto tiene el tipo de datos espaciales **Incrustado**.  
  
3.  Haga clic en la flecha de PointLayer2 > **Agregar punto**.  
  
4.  Mueva el puntero sobre la ventanilla del mapa. El cursor cambia a la forma de cruz.  
  
5.  Haga clic en la ubicación del mapa donde desee agregar un punto. En este tutorial, haga clic en una ubicación del condado de Oneida. Se agrega un punto marcado por un círculo a la capa en la ubicación en la que ha hecho clic. De forma predeterminada, el punto se selecciona.  

    ![report-builder-map-custom-point](../reporting-services/media/report-builder-map-custom-point.png)
  
6.  Haga clic con el botón derecho en el punto que ha agregado y, después, haga clic en **Propiedades de punto incrustado**.  
  
7.  Seleccione **Invalidar opciones de punto para esta capa**. Aparecen páginas adicionales en el cuadro de diálogo. Los valores que establece aquí tienen prioridad sobre las opciones de presentación de la capa o sobre las reglas de color.  

    ![report-builder-map-custom-point-general](../reporting-services/media/report-builder-map-custom-point-general.png)
  
8.  En la pestaña **Marcador** , en **Tipo de marcador**, seleccione **Estrella**.  

10. Cambie **Tamaño de marcador** a **18pt**.
  
3.  En **Etiquetas** , en **Texto de etiqueta**, escriba **Nuevo almacén**.  
  
5.  En **Colocación**, haga clic en **Superior**.  

13. En la pestaña **Fuente** , elija el tamaño de fuente **10pt** y **Negrita**.

    ![report-builder-map-custom-point-font](../reporting-services/media/report-builder-map-custom-point-font.png)
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Obtenga una vista previa del informe.  
  
Aparece la etiqueta sobre la ubicación del almacén.  

![report-builder-map-custom-point-new-store](../reporting-services/media/report-builder-map-custom-point-new-store.png)
  
## <a name="8-center-and-resize-the-map"></a><a name="CenterView"></a>8. Centrar y cambiar el tamaño del mapa   
En esta sección, aprenderá a cambiar el centro del mapa y otro método para cambiar el nivel de zoom.  
 
1.  Cambie a la vista de diseño.  

1.  Seleccione el mapa, haga clic con el botón derecho y haga clic en **Propiedades de ventanilla**.  
  
2.  En la pestaña **Centrar y hacer zoom** , asegúrese de que la opción **Establecer un nivel de zoom y centrado de la vista** está seleccionada.  

4. Establezca **Nivel de zoom (porcentaje)** en **125**.
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Haga clic en el mapa y arrastre para centrarlo en donde quiera.  
  
6.  También puede usar la rueda del mouse para cambiar el nivel de zoom.  
  
7.  Obtenga una vista previa del informe.  
  
En la vista Diseño, el mapa de la superficie de presentación y la vista se basan en los datos de ejemplo. En el informe representado, la vista del mapa se centra en la vista que especificó.  
  
## <a name="9-add-a-report-title"></a><a name="Title"></a>9. Agregar un título de informe  
  
1.  Cambie a la vista de diseño.
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba **Ventas en almacenes de Nueva York** y, a continuación, haga clic fuera del cuadro de texto.  
  
Este título aparecerá en la parte superior del informe. Cuando no hay ningún encabezado de página definido, los elementos de la parte superior del cuerpo del informe son el equivalente a un encabezado de informe.  
  
## <a name="10-save-the-report"></a><a name="Save"></a>10. Guardar el informe  
  
1.  En la vista Diseño o Vista previa, en el menú **Archivo** > **Guardar como**.
 
3.  En **Nombre**, escriba **Ventas de almacenes en Nueva York**.  

3. Guárdelo en el equipo local o en un servidor de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] .
  
4. Haga clic en **Save**(Guardar). 

Si lo guarda en un servidor de informes, puede verlo allí.

![report-builder-map-in-portal](../reporting-services/media/report-builder-map-in-portal.png) 
  
## <a name="next-steps"></a>Pasos siguientes  
De esta forma se concluye el tutorial sobre cómo agregar un mapa a un informe.  
  
Para obtener más información, vea [Mapas &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
[Tutoriales del Generador de informes](../reporting-services/report-builder-tutorials.md)  
[Generador de informes en SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
[Asistente para mapas y Asistente para capas de mapa &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
[Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  

