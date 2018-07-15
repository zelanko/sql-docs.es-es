---
title: 'Tutorial: Informe de asignaciones (Generador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8d831356-7efa-40cc-ae95-383b3eecf833
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 76795367b5f03e65673468d4af8e7f7c7222e73b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249745"
---
# <a name="tutorial-map-report-report-builder"></a>Tutorial: Informe de asignaciones (Generador de informes)
  Este tutorial le ayudará a obtener información sobre las características de mapa que puede utilizar para mostrar los datos de informe sobre un fondo geográfico.  
  
 Los mapas están basados en datos espaciales que normalmente está compuestos de puntos, líneas y polígonos. Por ejemplo, un polígono puede representar el perfil de un condado, una línea puede representar una carretera y un punto puede representar la ubicación de una ciudad. Cada tipo de datos espaciales se muestra en una capa de mapa independiente, como un conjunto de elementos de mapa.  
  
 Para variar la apariencia de los elementos de mapa, especifique un campo que tenga valores que hagan coincidir los elementos de mapa con los datos analíticos de un conjunto de datos. También puede definir las reglas que varían el color, tamaño u otras propiedades basadas en rangos de datos.  
  
 En este tutorial, compilará un informe de mapa que muestre ubicaciones de almacenes en los condados del Estado de Nueva York.  
  
##  <a name="BackToTop"></a> Qué aprenderá  
 En este tutorial, aprenderá a realizar las siguientes tareas:  
  
1.  [Crear un mapa con una capa de polígono desde el Asistente para mapas](#Map)  
  
2.  [Agregar una capa de punto de mapa para mostrar Store ubicaciones](#PointLayer)  
  
3.  [Agregar una capa de línea de mapa para mostrar una ruta](#LineLayer)  
  
4.  [Agregar un fondo de mosaico de Bing Maps](#TileLayer)  
  
5.  [Hacer una capa transparente](#Transparent)  
  
6.  [Variar los colores de condado de acuerdo con las ventas](#Vary)  
  
    1.  [Crear una relación entre datos espaciales y analíticos](#Relationship)  
  
    2.  [Especificar reglas de Color para polígonos](#ColorRules)  
  
    3.  [Dar formato a los datos de la escala de Color como moneda](#ColorScale)  
  
    4.  [Crear una nueva leyenda](#NewLegend)  
  
    5.  [Asociar la leyenda y las reglas de Color](#Associate)  
  
    6.  [Borrar el Color en los condados sin datos](#NoData)  
  
7.  [Agregar un punto personalizado](#CustomPoint)  
  
8.  [Centro de la vista del mapa](#CenterView)  
  
9. [Agregar un título de informe](#Title)  
  
10. [Guardar el informe](#Save)  
  
> [!NOTE]  
>  En este tutorial, los pasos del asistente se fusionan en dos procedimientos: uno para crear el conjunto de datos y otro para crear una tabla. Para obtener instrucciones paso a paso sobre cómo ir hasta un servidor de informes, elegir un origen de datos, crear un conjunto de datos y ejecutar el asistente, vea el primer tutorial de esta serie: [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tiempo estimado para completar este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obtener información sobre los requisitos, vea [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Map"></a> 1. Crear un mapa con una capa de polígono desde el Asistente para mapas  
 Agregar un mapa al informe desde la galería de mapas. El mapa tiene una capa que muestra los condados del Estado de Nueva York. La forma de cada condado es un polígono basado en los datos espaciales que se incrustan en el mapa desde la galería de mapas.  
  
#### <a name="to-add-a-map-with-the-map-wizard-in-a-new-report"></a>Para agregar un mapa con el Asistente para mapas en un informe nuevo  
  
1.  Haga clic en **iniciar**, apunte a **programas**, apunte a [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] **Report Builder**y, a continuación, haga clic en **Report Builder**.  
  
     Aparecerá el cuadro de diálogo Introducción.  
  
    > [!NOTE]  
    >  Si el cuadro de diálogo Introducción no aparece, en el botón Generador de informes, haga clic en **Nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Informe** .  
  
3.  En el panel derecho, haga clic en **Asistente para mapas**.  
  
4.  Haga clic en **Crear**.  
  
5.  En la página**Elegir un origen de datos espaciales** , compruebe que **Galería de mapas** está seleccionado.  
  
6.  En el panel Galería de mapas, expanda **Estados por condado** en **EE.UU.** y haga clic en **Nueva York**.  
  
     El panel Vista previa del mapa muestra el mapa del condado de Nueva York.  
  
7.  Haga clic en **Siguiente**.  
  
8.  En **Elegir opciones de datos espaciales y vista de mapa** , acepte los valores predeterminados. De forma predeterminada, los elementos de mapa de una galería de mapas se incrustarán automáticamente en la definición de informe.  
  
9. Haga clic en **Siguiente**.  
  
10. En la página **Elegir visualización de mapa** , compruebe que la opción **Mapa básico** está seleccionada y haga clic en **Siguiente**.  
  
11. En la página **Elegir tema de color y visualización de datos** , seleccione la opción **Mostrar etiquetas** .  
  
12. Si está seleccionada, desactive la opción **Mapa de un color** .  
  
13. En la lista desplegable **Campo de datos** , haga clic en #COUNTYNAME. El panel Vista previa del mapa del asistente muestra los elementos siguientes:  
  
    -   Un título con el texto **Título del mapa**.  
  
    -   Un mapa que muestra los condados de Nueva York, donde cada condado es de un color diferente y su nombre aparece siempre que se pasa el puntero sobre el área del condado.  
  
    -   Una leyenda que contiene un título y una lista de los elementos 1 a 5.  
  
    -   Una escala de colores que contiene los valores 0 a 160 y ningún color.  
  
    -   Una escala de distancia que muestra kilómetros (km) y millas (mi).  
  
14. Haga clic en **Finalizar**.  
  
     Se agrega el mapa a la superficie de diseño.  
  
15. Haga clic en el mapa para seleccionarlo y mostrar el panel **Capas de mapa**. El panel **Capas de mapa** muestra una capa de polígono del tipo **Incrustado**. Cada condado es un elemento de mapa incrustado en esta capa.  
  
    > [!NOTE]  
    >  Si no ve el panel **Capas de mapa** , quizá se esté mostrando fuera de su vista actual. Use la barra de desplazamiento de la parte inferior de la ventana de la vista Diseño para cambiar la vista. O bien, en la pestaña **Ver** , desactive la opción **Propiedades** o **Datos del informe** para proporcionar una mayor área de diseño expuesta.  
  
16. Haga clic con el botón secundario en el título del mapa y, a continuación, haga clic en **Propiedades del título**.  
  
17. Reemplace el texto de título con **Ventas por almacén**.  
  
18. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
19. Obtenga una vista previa del informe.  
  
 El informe representado muestra el título del mapa, el mapa y la escala de distancia. Los condados están en una capa de polígono de mapa. Cada condado es un polígono que varía según el color de una paleta de colores, pero los colores no están asociados a ningún dato. La escala de distancia muestra las distancias en kilómetros y millas.  
  
 La leyenda de mapa y la escala del color no aparecen todavía, porque no hay datos analíticos asociados a cada condado. Agregará los datos analíticos posteriormente en este tutorial.  
  
##  <a name="PointLayer"></a> 2. Agregar una capa de punto de mapa para mostrar las ubicaciones del almacén  
 Utilice el asistente para capas de mapa para agregar una capa de punto que muestre las ubicaciones de almacenes.  
  
> [!NOTE]  
>  En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
#### <a name="to-add-a-point-layer-based-on-a-sql-server-spatial-query"></a>Para agregar una capa de punto según una consulta espacial de SQL Server  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** . En la barra de herramientas, haga clic en el botón **Asistente para nueva capa** ![rs_IconMapLayerWizard](../../2014/tutorials/media/rs-iconmaplayerwizard.gif "rs_IconMapLayerWizard").  
  
3.  En la página **Elegir un origen de datos espaciales** , seleccione **Consulta espacial de SQL Server**y haga clic en **Siguiente**.  
  
4.  En la página **Elija un conjunto de datos con datos espaciales de SQL Server** , haga clic en **Agregar un nuevo conjunto de datos con datos espaciales de SQL Server**y después haga clic en **Siguiente**.  
  
5.  En la página **Elegir una conexión con un origen de datos espaciales de SQL Server** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos.  
  
6.  Haga clic en **Siguiente**.  
  
7.  En la página Diseñar una consulta, haga clic en **Editar como texto**.  
  
8.  Pegue el texto siguiente en el panel de consulta:  
  
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
    UNION ALL Select 124 as StoreKey, 'Contoso Rochester No.2 Store' as StoreName, 700 as SellingArea, 'Rochester' as City, 'Monroe' as County,    
     CAST(100000 as money) as Sales, CAST('POINT(-77.6240415667866 43.1547066024338)' as geography) AS SpatialLocation  
    UNION ALL Select 125 as StoreKey, 'Contoso Queens Store' as StoreName, 700 as SellingArea,'Queens' as City, 'New York City' as County,  
     CAST(500000 as money) as Sales, CAST('POINT(-73.7930979029883 40.7152781765927)' as geography) AS SpatialLocation  
    UNION ALL Select 126 as StoreKey, 'Contoso Elmira Store' as StoreName, 680 as SellingArea, 'Elmira' as City, 'Chemung' as County,  
     CAST(800000 as money) as Sales, CAST('POINT(-76.7397414783301 42.0736492742663)' as geography) AS SpatialLocation  
    UNION ALL Select 127 as StoreKey, 'Contoso Poestenkill Store' as StoreName, 455 as SellingArea, 'Poestenkill' as City, 'Rensselaer' as County,    
    CAST(1500000 as money) as Sales, CAST('POINT(-73.5626737425063 42.6940551238618)' as geography) AS SpatialLocation  
    ```  
  
9. En la barra de herramientas del diseñador de consultas, haga clic en **Ejecutar** (**!**).  
  
     El conjunto de resultados muestra siete columnas: StoreKey, StoreName, SellingArea, City, County, Sales y SpatialLocation. Estos datos representan un conjunto de almacenes del Estado de Nueva York que venden bienes de consumo. Cada fila del conjunto de resultados contiene un identificador de almacén, un nombre de almacén, el área disponible para la exhibición del producto, la ciudad y el condado donde se encuentra el almacén, el total de ventas y la ubicación espacial en longitud y latitud. El área de exhibición va de 455 a 1.125 pies cuadrados.  
  
10. Haga clic en **Siguiente**.  
  
     Se ha creado el conjunto de datos de informe denominado DataSet1. Después de completar el asistente, puede usar el panel Datos de informe para ver esta colección de campos.  
  
11. En el **elegir los datos espaciales y las opciones de vista del mapa** , comprueba que el **campo espacial** es `SpatialLocation` y que la **tipo de capa** es **punto**. Acepte los demás valores predeterminados de esta página.  
  
     La vista de mapa muestra círculos que marcan la ubicación de cada almacén.  
  
12. Haga clic en **Siguiente**.  
  
13. Especifique un tipo de mapa que muestre los marcadores que varían según los datos analíticos. En la página Elegir visualización de mapa, haga clic en **Mapa de marcadores analítico**y, a continuación, haga clic en **Siguiente**.  
  
14. En la página **Elegir el conjunto de datos analíticos** , haga clic en DataSet1. Este conjunto de datos contiene datos analíticos y datos espaciales que se mostrarán en la nueva capa de punto.  
  
15. Haga clic en **Siguiente**.  
  
16. En la página **Elegir tema de color y visualización de datos** , desactive la opción **Usar colores de marcador para visualizar datos** y después seleccione la opción **Usar tipos de marcador para visualizar datos**.  
  
17. En **Campo de datos**, seleccione `[Sum(SellingArea)]` para variar los tipos de marcador de acuerdo con el tamaño del área que un almacén separa para mostrar productos.  
  
18. Haga clic en **Finalizar**.  
  
     La capa de mapa se agrega al informe. La leyenda muestra los tipos de marcador según los valores de SellingArea.  
  
     Haga doble clic en el mapa para mostrar el panel **Capa de mapa** . El panel **Capa de mapa** muestra una nueva capa, PointLayer1, con el tipo de origen de datos espaciales **DataRegion**.  
  
19. Agregue un título a la leyenda. Haga clic con el botón secundario en el título de la leyenda y, a continuación, haga clic en **Propiedades del título de la leyenda**.  
  
20. Elimine el título y escriba **Área de presentación (pies cuadrados)**.  
  
21. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
22. Vea los valores predeterminados que fueron establecidos por el asistente. En el panel **Capas de mapa**, haga clic con el botón secundario en la capa de punto y, a continuación, haga clic en **Regla de tipo de marcador**.  
  
     En la pestaña **General** , los marcadores se enumeran en el orden en el que aparecen en la leyenda. En la pestaña **Distribución** , el número de subrango es 5. En la pestaña **Leyenda** , el texto de la leyenda se establece para mostrar el valor de inicio y el valor final de cada rango.  
  
23. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
24. Obtenga una vista previa del informe.  
  
 El mapa muestra las ubicaciones de los almacenes del Estado de Nueva York. El tipo de marcador para cada almacén está basado en el área de presentación. Se calcularon automáticamente para usted cinco rangos de área de presentación.  
  
##  <a name="LineLayer"></a> 3. Agregar una capa de línea de mapa para mostrar una ruta  
 Use el Asistente para capas de mapa para agregar una capa de mapa que muestre una ruta entre dos almacenes. En este tutorial, la ruta de acceso se crea a partir de tres ubicaciones de almacén. En una aplicación empresarial, la ruta podría ser la ruta mejor entre los almacenes.  
  
#### <a name="to-add-a-line-layer-to-map"></a>Para agregar una capa de línea al mapa  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** . En la barra de herramientas, haga clic en **Asistente para nueva capa**.  
  
3.  En la página **Elegir un origen de datos espaciales** , seleccione **Consulta espacial de SQL Server** y haga clic en **Siguiente**.  
  
4.  En la página **Elija un conjunto de datos con datos espaciales de SQL Server** , haga clic en **Agregar un nuevo conjunto de datos con datos espaciales de SQL Server** y haga clic en **Siguiente**.  
  
5.  En **Elegir una conexión con un origen de datos espaciales de SQL Server**, seleccione DataSource1, el origen de datos que creó en el primer procedimiento.  
  
6.  Haga clic en **Siguiente**.  
  
7.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**. El diseñador de consultas cambia al modo basado en texto.  
  
8.  Pegue el texto siguiente en el panel de consulta:  
  
    ```  
    SELECT N'Path' AS Name, CAST('LINESTRING(  
       -76.5001866085881 42.4310489934743,  
       -76.4602850815536 43.4353224527794,  
       -73.4728622833178 44.7028831413324)' AS geography) as Route  
    ```  
  
9. Haga clic en **Siguiente**.  
  
     En el mapa aparece una ruta de acceso que conecta tres almacenes.  
  
10. En la página **Elegir opciones de datos espaciales y vista de mapa** , compruebe que el **Campo espacial** es **Route** y que el **Tipo de capa** es **Línea**. Acepte los otros valores predeterminados.  
  
     La vista de mapa muestra una ruta desde un almacén de la parte septentrional del Estado de Nueva York a otro de la parte meridional.  
  
11. Haga clic en **Siguiente**.  
  
12. En la página **Elegir visualización de mapa** , haga clic en **Mapa de líneas básico**y, después, en **Siguiente**.  
  
13. En **Elegir tema de color y visualización de datos**, seleccione la opción **Mapa de un color**. La ruta aparece en un color basado en el tema seleccionado.  
  
14. Haga clic en **Finalizar**.  
  
 El mapa muestra una nueva capa de línea con el tipo de origen de datos espaciales **DataSet**. En este ejemplo, los datos espaciales proceden de un conjunto de datos, pero ningún dato analítico se asocia a la línea.  
  
##  <a name="TileLayer"></a> 4. Agregar un fondo de mosaico de Bing Maps  
 Agregue una capa de mapa que muestre un fondo de mosaico de Bing Maps.  
  
#### <a name="to-add-a-virtual-earth-tile-background"></a>Para agregar un fondo de mosaico Virtual Earth  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** . En la barra de herramientas, haga clic en **Agregar capa**![rs_IconMapAddLayer](../../2014/tutorials/media/rs-iconmapaddlayer.gif "rs_IconMapAddLayer").  
  
3.  En la lista desplegable, haga clic en **Capa de mosaico**.  
  
     La última capa del panel **Capa de mapa** es TileLayer1. De forma predeterminada, la capa de mosaico muestra el estilo de mapa de carreteras.  
  
    > [!NOTE]  
    >  En el asistente, también puede agregar una capa de mosaico en la página **Elegir opciones de datos espaciales y vista de mapa** . Para ello, seleccione **Agregar un fondo de Bing Maps a esta vista de mapa**. En un informe representado, el fondo de mosaico muestra mosaicos de Bing Maps en el centro de la ventanilla del mapa actual y en el nivel de zoom.  
  
4.  Haga clic en la flecha abajo en TileLayer1 y, a continuación, haga clic en **Propiedades del mosaico**.  
  
5.  En **Tipo**, seleccione **Aéreo**. La vista aérea no contiene texto.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Transparent"></a> 5. Hacer una capa transparente  
 Para permitir que los elementos de una capa se muestren a través de otra capa, puede ajustar el orden de las capas y la transparencia de cada una para obtener el efecto que desea.  
  
#### <a name="to-set-the-transparency-of-a-layer"></a>Para establecer la transparencia de una capa  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** .  
  
3.  Haga clic en la flecha abajo en PolygonLayer1 y, a continuación, haga clic en **Datos de la capa**. Se abre el cuadro de diálogo **Propiedades de capa de polígono de mapa** .  
  
4.  Haga clic en **Visibilidad**.  
  
5.  En **Transparencia (%)**, escriba **30**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 La superficie de diseño muestra los condados como semitransparentes.  
  
##  <a name="Vary"></a> 6. Variar los colores de condado de acuerdo con las ventas  
 Cada condado de la capa de polígono tiene un color diferente porque el procesador de informes asigna automáticamente un valor de color de la paleta de colores en función del tema que eligió en la última página del Asistente para mapas.  
  
 En los pasos siguientes, especifique una regla de color para asociar colores concretos a un rango de valores de almacén para cada condado. Los colores rojo, verde y amarillo indican unas ventas anuales altas, medias o bajas relativas. Dé formato a la escala de colores para mostrar la moneda. Muestre los rangos de ventas anuales en una nueva leyenda. En los condados que no contengan almacenes, no use ningún color para mostrar que no hay ningún dato asociado.  
  
###  <a name="Relationship"></a> 6a. Compilar una relación entre los datos espaciales y los datos analíticos  
 Para variar las formas del condado por el color según los datos analíticos, debe asociar primero los datos analíticos a los datos espaciales. En este tutorial, utilizará el nombre del condado para la coincidencia.  
  
##### <a name="to-build-a-relationship-between-spatial-data-and-analytical-data"></a>Para generar una relación entre los datos espaciales y los datos analíticos  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** .  
  
3.  Haga clic en la flecha abajo en PolygonLayer1 y, a continuación, haga clic en **Datos de la capa**. Se abre el cuadro de diálogo **Propiedades de capa de polígono de mapa** .  
  
4.  Haga clic en **Datos analíticos**.  
  
5.  En la lista desplegable, seleccione DataSet1. El asistente creó este conjunto de datos cuando se especificó la consulta de datos espaciales para los condados.  
  
6.  En **Campos en los que establecer coincidencias**, haga clic en **Agregar**. Se agrega una nueva fila.  
  
7.  En **Desde el conjunto de datos espaciales**, en la lista desplegable, haga clic en COUNTYNAME.  
  
8.  En **Desde el conjunto de datos analíticos**, en la lista desplegable, haga clic en [County].  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Obtenga una vista previa del informe.  
  
 Al especificar un campo coincidente del origen de datos espaciales y el conjunto de datos analíticos, el procesador de informes puede agrupar los datos analíticos según los elementos de mapa. Un elemento de mapa enlazado a datos tiene una coincidencia correcta para los valores que especificó.  
  
 Cada condado que contiene un almacén tiene un color que está basado en la paleta de colores correspondiente el estilo que eligió en el asistente.  
  
###  <a name="ColorRules"></a> 6b. Especificar las reglas de color para polígonos  
 Para crear una regla que varía el color de cada condado basándose en las ventas por almacén, debe especificar los valores de rango, el número de divisiones dentro de ese rango que desea mostrar y los colores que se van a usar.  
  
##### <a name="to-specify-color-rules-for-all-polygons-that-have-associated-data"></a>Especificar las reglas de color para todos los polígonos que tienen datos asociados  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga clic en la flecha abajo en PolygonLayer1 y, a continuación, haga clic en **Regla de color de polígono**. El cuadro de diálogo **Propiedades de reglas de color de mapa** se abre. Observe que la opción de la regla de color **Visualizar datos mediante la paleta de colores** está seleccionada. Esta opción se estableció en el asistente.  
  
3.  Seleccione **Visualizar datos mediante los rangos de colores**. La opción de la paleta se reemplaza con las opciones de color inicial, color intermedio y color final.  
  
4.  Defina los valores de rango para las ventas de cada condado. En **Campo de datos**, en la lista desplegable, seleccione `[Sum(Sales)]`.  
  
5.  Para cambiar el formato para mostrar la moneda en millares, cambie la expresión a la siguiente: `=Sum(Fields!Sales.Value)/1000`  
  
6.  Cambie **Color inicial** a **Rojo**.  
  
7.  Cambie **Color final** a **Verde**.  
  
     **Rojo** representa valores de ventas bajos, **Amarillo** representa valores de ventas intermedios y **Verde** representa valores de ventas altos. El procesador de informes calcula un rango de colores según estos valores y las opciones que elija en la página **Distribución** .  
  
8.  Haga clic en **Distribución**.  
  
9. Compruebe que el tipo de distribución es **Óptimo**. Para la expresión del paso 5, la distribución óptima divide los valores en subrangos que equilibren el número de elementos y la amplitud de cada rango.  
  
10. Acepte los valores predeterminados de las demás opciones de esta página. Al seleccionar el tipo de distribución óptimo, el número de subrangos se calcula cuando se ejecuta el informe.  
  
11. Haga clic en **Leyenda**.  
  
12. En **Opciones de escala de colores**, compruebe que la opción **Mostrar en escala de colores** está seleccionada.  
  
13. En **Mostrar en esta leyenda**, en la lista desplegable, seleccione la línea en blanco. Por ahora, mostrará los rangos de colores solo en la escala de colores.  
  
14. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
 La escala de colores muestra cinco colores: rojo, naranja, amarillo, verde amarillento y verde. Cada color representa un rango de ventas que se calcula automáticamente de acuerdo con las ventas por condado.  
  
###  <a name="ColorScale"></a> 6C. Dar formato a los datos en la escala de color como moneda  
 De forma predeterminada, los datos tienen un formato general. Puede aplicar formatos personalizados.  
  
##### <a name="to-set-the-format-for-the-color-scale"></a>Establecer el formato de la escala de colores  
  
1.  Haga clic con el botón secundario en la escala de colores y, a continuación, haga clic en **Propiedades de escala de colores**.  
  
2.  Haga clic en **Número**.  
  
3.  En **Categoría**, haga clic en **Moneda**.  
  
4.  En **Posiciones decimales**, escriba **0**. Este formato no especifica ninguna posición decimal para la moneda.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Obtenga una vista previa del informe.  
  
 La escala de colores muestra las ventas anuales en el formato de moneda para cada rango.  
  
###  <a name="NewLegend"></a> 6D. Crear una nueva leyenda  
 De forma predeterminada, todas las reglas se muestran en la primera leyenda. Para mejorar la presentación de un mapa, puede agregar leyendas.  
  
 Cambiar la presentación predeterminada requiere dos pasos: crear una nueva leyenda y, a continuación, asociar los resultados de la regla para una capa de mapa con la nueva leyenda.  
  
##### <a name="to-create-a-new-legend"></a>Crear una nueva leyenda  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga clic con el botón secundario en el mapa fuera de la ventanilla y, a continuación, haga clic en **Agregar leyenda**. Una leyenda nueva se agrega al mapa en una ubicación predeterminada.  
  
3.  Haga clic con el botón secundario en la leyenda y, después, haga clic en **Propiedades de la leyenda**.  
  
4.  En **Opciones de posición**, haga clic en la ubicación que especifica dónde desea que la leyenda aparezca en relación con la ventanilla. El mapa de la superficie del diseño cambia para mostrar el efecto de las selecciones.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Haga clic en **Título** en la leyenda para seleccionar el título de la misma.  
  
7.  Haga clic de nuevo en **Título** para especificar el modo de inserción para el texto. Reemplace **Título** por **Ventas (miles)** y, a continuación, haga clic fuera del texto.  
  
 La leyenda se expande para mostrar el título.  
  
###  <a name="Associate"></a> 6E. Asociar la leyenda y las reglas de color  
 Cada leyenda puede mostrar uno o más conjuntos de resultados de la regla.  
  
##### <a name="to-associate-a-legend-with-color-rules"></a>Asociar una leyenda a reglas de color  
  
1.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** .  
  
2.  Haga clic en la flecha abajo en PolygonLayer1 y, a continuación, haga clic en **Regla de color de polígono**. El cuadro de diálogo **Propiedades de reglas de color de mapa** se abre.  
  
3.  Haga clic en **Leyenda**.  
  
4.  En **Opciones de escala de colores**, desactive **Mostrar en escala de colores**.  
  
5.  En **Opciones de leyenda**, en la lista desplegable, seleccione Legend2. Aparece la opción de texto de la leyenda. De forma predeterminada, se da formato al texto de la leyenda con una cadena de formato [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] general. Los 0 en N0 no especifican dígitos decimales.  
  
6.  En **texto de leyenda**, use el siguiente formato para especificar la moneda sin los dígitos decimales: `#FROMVALUE {C0} - #TOVALUE {C0}`  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     En la superficie de diseño, la leyenda muestra los rangos de color con datos de ejemplo con formato de moneda.  
  
8.  Obtenga una vista previa del informe.  
  
 Los condados que tienen asociados almacenes y ventas se muestran e acuerdo con las reglas de color. Los condados que no tienen ventas tampoco tienen un color.  
  
###  <a name="NoData"></a> 6f. Cambiar el color en los condados sin datos  
 Puede configurar las opciones de presentación predeterminadas para todos los elementos de mapa de una capa. Las reglas de color tienen prioridad sobre estas opciones de presentación.  
  
##### <a name="to-set-the-display-properties-for-all-elements-on-a-layer"></a>Para establecer las propiedades de presentación de todos los elementos de una capa  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** .  
  
3.  Haga clic en la flecha abajo en PolygonLayer1 y, a continuación, haga clic en **Propiedades del polígono**. El cuadro de diálogo **Propiedades de polígono de mapa** se abre. Las opciones de presentación configuradas en este cuadro de diálogo se aplican a todos los polígonos de la capa antes de que se apliquen las opciones de presentación basadas en reglas.  
  
4.  Haga clic en **Relleno**.  
  
5.  Compruebe que el estilo de relleno es **Sólido.** Los degradados y patrones se aplican a todos los colores.  
  
6.  En **Color**, haga clic en la flecha abajo y, a continuación, haga clic en **Azul acero claro**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Obtenga una vista previa del informe.  
  
 Los condados que no tienen datos asociados se presentan como azul. Solo los condados que tienen datos analíticos asociados aparecen en los colores **Rojo** a **Verde** de las reglas de color que especificó.  
  
##  <a name="CustomPoint"></a> 7. Agregar un punto personalizado  
 Para representar un nuevo almacén que no se ha generado todavía, especifique un punto y utilice el tipo de marcador **Pin** .  
  
#### <a name="to-add-a-custom-point"></a>Para agregar un punto personalizado  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga doble clic en el mapa para mostrar el panel **Capa de mapa** . En la barra de herramientas, haga clic en **Agregar capa**y, a continuación, haga clic en **Capa de punto**.  
  
     Una nueva capa de punto se agrega al mapa. De forma predeterminada, la capa de punto tiene el tipo de datos espaciales **Incrustado**.  
  
3.  Haga clic en la flecha abajo en PointLayer2 y, a continuación, haga clic en **Agregar punto**.  
  
4.  Mueva el puntero sobre la ventanilla del mapa. El cursor cambia a la forma de cruz.  
  
5.  Haga clic en la ubicación del mapa donde desee agregar un punto. En este tutorial, haga clic en una ubicación de un condado próxima al inicio de la ruta. Un punto marcado por un círculo se agrega a la capa en la ubicación donde hizo clic. De forma predeterminada, el punto se selecciona.  
  
6.  Haga clic con el botón secundario en el punto que agregó y, a continuación, haga clic en **Propiedades de punto incrustado**.  
  
7.  Seleccione la opción **Invalidar opciones de punto para esta capa**. Aparecen páginas adicionales en el cuadro de diálogo. Los valores que establece aquí tienen prioridad sobre las opciones de presentación de la capa o sobre las reglas de color.  
  
8.  Haga clic en **Marcador**.  
  
9. En **Tipo de marcador**, seleccione **Estrella**.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Obtenga una vista previa del informe.  
  
 El nuevo punto que agregó aparece como una **Estrella**.  
  
#### <a name="to-add-a-label-for-the-custom-point"></a>Para agregar una etiqueta para el punto personalizado  
  
1.  Cambie a la vista de diseño.  
  
2.  Haga clic con el botón secundario en el punto recién agregado y, a continuación, haga clic en **Propiedades de punto incrustado**.  
  
3.  Haga clic en **Etiquetas**.  
  
4.  En **Texto de etiqueta**, escriba **Nuevo almacén**.  
  
5.  En **Colocación**, haga clic en **Superior**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Obtenga una vista previa del informe.  
  
 Aparece la etiqueta sobre la ubicación del almacén.  
  
##  <a name="CenterView"></a> Centro de la vista del mapa  
 Cambie el centro de la ventanilla de mapas y la capa de zoom.  
  
#### <a name="to-change-the-viewport"></a>Para cambiar la ventanilla  
  
1.  Haga clic con el botón secundario en la ventanilla del mapa y, a continuación, haga clic en **Propiedades de ventanilla**.  
  
2.  Haga clic en **Centrar y hacer zoom**.  
  
3.  Compruebe que está seleccionada la opción **Establecer un nivel para centrar y hacer zoom de la vista** .  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Haga clic con el botón primario en la ventanilla de mapas y arrastre el centro de la ventanilla hacia la ubicación que desea.  
  
6.  Utilice la rueda del mouse para cambiar el nivel de zoom de la ventanilla.  
  
7.  Obtenga una vista previa del informe.  
  
 En la vista Diseño, el mapa de la superficie de presentación y la vista se basan en los datos de ejemplo. En el informe representado, la vista del mapa se centra en la vista que especificó.  
  
##  <a name="Title"></a> Agregar un título de informe  
  
#### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba **Ventas en almacenes de Nueva York** y, a continuación, haga clic fuera del cuadro de texto.  
  
 Este título aparecerá en la parte superior del informe. Cuando no hay ningún encabezado de página definido, los elementos de la parte superior del cuerpo del informe son el equivalente a un encabezado de informe.  
  
##  <a name="Save"></a> Guardar el informe  
  
#### <a name="to-save-the-report"></a>Para guardar el informe  
  
1.  Cambie a la vista de diseño.  
  
2.  En el botón Generador de informes, haga clic en **Guardar como**.  
  
3.  En **Nombre**, escriba **Ventas de almacenes en Nueva York**.  
  
 Haga clic en **Guardar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
 De esta forma se concluye el tutorial sobre cómo agregar un mapa a un informe.  
  
 Para obtener más información, consulte [mapas &#40;generador de informes y SSRS&#41; ](report-design/maps-report-builder-and-ssrs.md) y la entrada de blog [ajuste cartográfico de datos espaciales de SQL Server Reporting Services](http://go.microsoft.com/fwlink/?LinkId=152771) en blogs.msdn.com.  
  
 Para obtener más tutoriales, vea [tutoriales &#40;Report Builder&#41;](report-builder-tutorials.md).  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales &#40;generador de informes&#41;](report-builder-tutorials.md)   
 [Generador de informes en SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)   
 [Asistente para mapas y Asistente para capas de mapa &#40;Generador de informes y SSRS&#41;](report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)   
 [Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos &#40;Generador de informes y SSRS&#41;](report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md)  
  
  
