---
title: "Planear un informe de mapa (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dc0c27a4-7e31-4a15-a0bc-3a02479d5b02
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 9
---
# Planear un informe de mapa (Generador de informes y SSRS)
Los buenos informes presentan información que motiva acciones o conocimientos. Para presentar datos analíticos como totales de ventas o datos demográficos en un contexto geográfico, puede agregar un mapa al informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]. Un mapa puede contener varias capas, y en cada una se muestran elementos de mapa definidos por un tipo concreto de datos espaciales: puntos que representan ubicaciones, líneas que representan rutas o polígonos que representan áreas. Puede asociar los datos analíticos a elementos de mapa en cada capa.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="MapPurpose"></a> Especificar el propósito del mapa  
 Un diseño de informe apropiado proporciona información que ayuda a los usuarios a tomar medidas para resolver los problemas. Para crear una presentación de mapa útil y fácilmente entendible, decida qué cuestiones desea que el mapa ayude a responder. Por ejemplo, en un mapa puede visualizar los tipos siguientes de datos para identificar oportunidades de mercado:  
  
-   Ventas relativas de cada almacén.  
  
-   Ventas clasificadas por los datos demográficos del cliente, según la ubicación del cliente en relación con las ubicaciones del almacén.  
  
-   Ventas comparativas u otros datos financieros por territorio de ventas.  
  
-   Ventas comparativas para diferentes estrategias de descuento en varios almacenes.  
  
 Después de identificar el propósito de la presentación del mapa, debe analizar qué datos necesita. Los datos analíticos proceden de conjuntos de datos de informe. Los datos de ubicación proceden de orígenes de datos espaciales que debe especificar.  
  
##  <a name="Data"></a> Especificar los datos espaciales y analíticos  
 Debe especificar qué datos espaciales y analíticos necesita.  
  
 Los datos analíticos pueden proceder de un conjunto de datos de informe, de los datos de ejemplo de un mapa de la galería de mapas o de los datos analíticos incluidos con los datos espaciales en un archivo de forma ESRI.  
  
 Los datos espaciales vienen en tres formas: puntos, líneas y polígonos.  
  
-   **Puntos.** Los puntos especifican las ubicaciones una ciudad; por ejemplo, una dirección de un almacén, restaurante o centro de convenciones. Debe proporcionar los datos espaciales de cada ubicación que desee mostrar en un mapa. Después de agregar los puntos a un mapa, puede mostrar un marcador en la ubicación del mismo y variar el tipo de marcador, tamaño y color.  
  
-   **Líneas.** Las líneas especifican las rutas de acceso, por ejemplo, las rutas de entrega o del vuelo. Después de agregar una línea a un mapa, puede variar su color y su ancho.  
  
-   **Polígonos.** Los polígonos especifican áreas, por ejemplo regiones, territorios, países, estados, provincias, condados, ciudades o áreas cubiertas por ciudades, códigos postales, centrales telefónicas o distritos del censo. Después de agregar polígonos a un mapa, además de mostrar el contorno, puede mostrar un marcador en el punto central del área del polígono.  
  
 Después de identificar qué datos espaciales necesita, debe buscar un origen para ellos.  
  
### Buscar un origen para los datos espaciales  
 Para buscar los datos espaciales que se usarán en un mapa, puede utilizar los orígenes siguientes:  
  
-   Archivos de forma ESRI, que incluyen los archivos de forma disponibles públicamente que puede encontrar en Internet.  
  
-   Datos espaciales de orígenes de datos espaciales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Mapas de los informes de la galería de mapas.  
  
-   Sitios de terceros que proporcionan datos espaciales como archivos de forma ESRI o datos espaciales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Mosaicos de Bing Maps, que proporcionan un fondo para la vista del mapa. Para mostrar los mosaicos en un mapa, se debe configurar el servidor de informes para que admita Servicios web de Bing Maps.  
  
 Para obtener más información, vea "¿Dónde se pueden obtener archivos de forma ESRI?" en [Asistente para mapas y Asistente para capas de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  
  
 Los datos espaciales pueden ser políticamente delicados y es posible que estén sometidos a copyright. Compruebe las condiciones de uso y las declaraciones de privacidad de los orígenes de datos espaciales para saber cómo puede utilizarlos en un informe.  
  
 Cuando encuentre los datos que desea, puede incrustarlos en la definición de informe o recuperarlos dinámicamente al procesar el informe. Para obtener más información, vea [Equilibrar el tamaño de la definición de informe y el tiempo de procesamiento del informe](#Embedding) , más adelante en este tema.  
  
### Determinar los datos espaciales y los campos coincidentes de datos espaciales  
 Para mostrar datos analíticos en un mapa y variar el tamaño, color o tipo de marcador, debe especificar los campos que relacionan los datos espaciales y los datos analíticos.  
  
 Los datos espaciales deben contener los campos siguientes:  
  
-   **.** Campo de datos espaciales que tiene los conjuntos de coordenadas que definen cada punto, línea o polígono.  
  
-   **Campos coincidentes.** Uno o varios campos que identifican de forma única cada campo de datos espaciales. Por ejemplo, para un punto de ubicación de un almacén, podría utilizar el nombre del almacén. Si el nombre del almacén no es único en los datos espaciales, podría incluir el nombre de la ciudad además del almacén.  
  
 Los campos coincidentes se utilizan para relacionar los datos espaciales con los datos analíticos.  
  
### Determinar los campos coincidentes de datos analíticos y datos espaciales  
 Después de identificar los datos espaciales, debe identificar los datos analíticos. Los datos analíticos pueden proceder de alguno de los orígenes siguientes:  
  
-   Un conjunto de datos de informe existente. Los campos se especifican como expresiones de campo sencillas, por ejemplo, [Sales] o =Fields!Sales.Value.  
  
-   Campos de datos que proporciona el origen de datos espaciales. Los campos se especifican como palabras clave que comienzan con el símbolo # seguido del nombre de campo del origen de datos espaciales.  
  
 A continuación, debe determinar los nombres de los campos coincidentes:  
  
-   Campos coincidentes. Uno o varios campos que especifican la misma información que los campos coincidentes de datos espaciales para crear una relación entre los datos espaciales y los datos analíticos. En los campos coincidentes debería corresponderse el tipo de datos además del formato.  
  
 Cuando haya identificado el origen de datos espaciales, los datos espaciales, el origen de datos analíticos, los datos analíticos y los campos coincidentes, estará en disposición de decidir qué tipo de mapa agregar al informe.  
  
##  <a name="MapType"></a> Elegir un tipo de mapa  
 Al ejecutar el Asistente para mapas, agrega al informe un mapa y la primera capa de mapa. El asistente le permite agregar uno de los tipos siguientes de mapas a un informe:  
  
-   Un mapa básico que muestra las ubicaciones sin datos analíticos asociados.  
  
-   Un mapa que tiene un valor analítico asociado a cada elemento de mapa, por ejemplo el total de ventas de cada ubicación del almacén.  
  
-   Un mapa que tiene más de un valor analítico asociado a un elemento de mapa, por ejemplo el número de clientes y el total de ventas de cada ubicación del almacén.  
  
 La tabla siguiente describe cada tipo de mapa. Todos los tipos de mapa le permiten seleccionar un tema que controla la paleta, el estilo de borde y la fuente, así como mostrar etiquetas.  
  
|Icono del asistente|Estilo de la capa|Tipo de capa|Descripción y opciones|  
|-----------------|-----------------|----------------|-----------------------------|  
|![rs_MapType_Polygon_Basic](../../reporting-services/report-design/media/rs-maptype-polygon-basic.png "rs_MapType_Polygon_Basic")|Mapa básico|Polígono|Mapa que solo muestra áreas, por ejemplo territorios de ventas.<br /><br /> Opciones: varíe el color según la paleta o utilice un único color. Una paleta es un conjunto predefinido de colores. Cuando se han asignado todos los colores de una paleta, se asignan las sombras de los colores.|  
|![rs_MapType_Polygon_ColorAnalytical](../../reporting-services/report-design/media/rs-maptype-polygon-coloranalytical.png "rs_MapType_Polygon_ColorAnalytical")|Mapa analítico de color|Polígono|Mapa que muestra los datos analíticos mediante la variación del color, por ejemplo los datos de ventas por área.|  
|![rs_MapType_Polygon_Bubble](../../reporting-services/report-design/media/rs-maptype-polygon-bubble.png "rs_MapType_Polygon_Bubble")|Mapa de burbujas|Polígono|Mapa que muestra los datos analíticos variando el tamaño de burbuja centrada en las áreas, por ejemplo los datos de ventas por área.<br /><br /> Opciones: varíe los colores del área según un segundo campo analítico y especifique reglas de color.|  
|![rs_MapType_Line_Basic](../../reporting-services/report-design/media/rs-maptype-line-basic.png "rs_MapType_Line_Basic")|Mapa de líneas básico|Línea|Mapa que muestra únicamente líneas, por ejemplo las rutas de entrega.<br /><br /> Opciones: varíe el color según la paleta o utilice un único color.|  
|![rs_MapType_Line_Analytical](../../reporting-services/report-design/media/rs-maptype-line-analytical.png "rs_MapType_Line_Analytical")|Mapa de líneas analítico|Línea|Mapa que varía el color y ancho de las líneas, por ejemplo el número de paquetes entregados y las métricas de tiempo por ruta.<br /><br /> Opciones: varíe el ancho de línea con un campo analítico, varíe el color de línea con un segundo campo analítico y especifique las reglas de color.|  
|![rs_MapType_Marker_Basic](../../reporting-services/report-design/media/rs-maptype-marker-basic.png "rs_MapType_Marker_Basic")|Mapa de marcadores básico|Punto|Mapa que muestra un marcador en cada ubicación, por ejemplo las ciudades.<br /><br /> Opciones: varíe el color por paleta o utilice un único color y cambie el estilo de marcador.|  
|![rs_MapType_Marker_Bubble](../../reporting-services/report-design/media/rs-maptype-marker-bubble.png "rs_MapType_Marker_Bubble")|Mapa de marcadores de burbuja|Punto|Mapa que muestra una burbuja para cada ubicación y varía el tamaño de burbuja mediante un campo de datos analíticos, por ejemplo los datos de ventas por ciudad.<br /><br /> Opciones: varíe el color de las burbujas con un segundo campo analítico y especifique las reglas de color.|  
|![rs_MapType_Marker_Analytical](../../reporting-services/report-design/media/rs-maptype-marker-analytical.png "rs_MapType_Marker_Analytical")|Mapa de marcadores analítico|Punto|Mapa que muestra un marcador en cada ubicación y varía el color, el tamaño y el tipo de los marcadores según datos analíticos, por ejemplo los productos de mayores ventas, el intervalo de ganancia y la estrategia de descuentos.<br /><br /> Opciones: varíe el tipo de los marcadores con un campo analítico, varíe el tamaño de los marcadores con un segundo campo analítico, varíe el color de los marcadores con un tercer campo analítico y especifique las reglas de color.|  
  
 Después de agregar un mapa con el Asistente para mapas, puede crear capas adicionales o cambiar las opciones de una capa utilizando el Asistente para capas. Para más información sobre los asistentes, vea [Asistente para mapas y Asistente para capas de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  
  
 Puede personalizar las opciones de datos o de presentación de cada capa de forma independiente. Para más información sobre cómo personalizar un mapa después de ejecutar un asistente, vea [Personalizar los datos y la presentación de un mapa o una capa de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
##  <a name="Legend"></a> Planear las leyendas  
 Para ayudar a los usuarios a interpretar un mapa, puede agregar varias leyendas de mapa, una escala de colores y una escala de distancia. Al diseñar un mapa, planee donde desea que se muestren las leyendas. Puede especificar la información siguiente sobre cada leyenda:  
  
-   **Ubicación de la leyenda.** Por ejemplo, las leyendas se pueden mostrar dentro o fuera de la ventanilla, y en 12 ubicaciones discretas en relación con la ventanilla.  
  
-   **Estilos de leyenda**. Por ejemplo, puede especificar el estilo de fuente, estilo de borde, línea de separación y propiedades de relleno.  
  
-   **Título de la leyenda.** Por ejemplo, puede especificar el texto del título y controlar independientemente si mostrar el título de la leyenda de un mapa o la escala de colores.  
  
-   **Diseño de la leyenda de mapa.** Por ejemplo, las leyendas de mapa se pueden mostrar como tablas altas o como tablas anchas.  
  
 El contenido de la leyenda se crea automáticamente durante el procesamiento del informe según las opciones de regla que se establezcan para cada capa.  
  
 De forma predeterminada, todas las capas muestran los resultados de las reglas en la primera leyenda del mapa. Puede crear varias leyendas y, a continuación, para cada regla, asignar qué leyenda utilizar para mostrar los resultados.  
  
 Para más información, vea [Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/vary polygon, line, and point display by rules and analytical data.md) y [Cambiar leyendas de mapa, escala de colores y reglas asociadas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
##  <a name="Embedding"></a> Equilibrar el tamaño de la definición de informe y el tiempo de procesamiento del informe  
 Un buen diseño de informe para mapas requiere que equilibre las opciones que controlan el rendimiento del informe y el tamaño de su definición. Los elementos de un mapa que se basan en datos espaciales, o mosaicos de Bing Maps, pueden ser estáticos e incrustarse en la definición de informe, o dinámicos y crearse cada vez que se procesa el mismo. Debe evaluar las ventajas comparativas de los datos de mapas estáticos y dinámicos, y encontrar el equilibrio que resulte apropiado en sus circunstancias. Considere la información siguiente para tomar esta decisión:  
  
-   Los elementos de mapa incrustados pueden aumentar considerablemente el tamaño de la definición de informe, pero reducen el tiempo necesario para ver el mapa en el informe. El servidor de informes podría tener límites de tamaño que haya que mantener.  
  
-   La definición de informe especifica los límites del número de puntos de datos espaciales que se pueden procesar y un valor independiente que especifique el número de elementos de mapa que pueden incluirse en la definición de informe.  
  
-   Los elementos de mapa dinámicos reducen el tamaño de la definición de informe, pero aumentan el tiempo necesario para procesar y representar el mapa.  
  
-   Cuando el origen de datos espaciales se encuentra en el equipo, los elementos de mapa siempre se incrustan en la definición de informe. Esto incluye los datos espaciales de la Galería de mapas o de los archivos de forma ESRI que se han instalado localmente.  
  
 Para utilizar los datos espaciales dinámicos, el origen de datos espaciales debe estar en el servidor de informes. Cuando los informes se diseñan en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], los orígenes de datos espaciales se pueden agregar a un proyecto y publicar en el servidor de informes junto con la definición de informe. Si usa el Generador de informes para diseñar informes, debe cargar primero los datos espaciales en el servidor de informes y, a continuación, en las propiedades de las capas o el asistente, especificar ese origen de datos espaciales para la capa de mapa.  
  
## Vea también  
 [Personalizar los datos y la presentación de un mapa o una capa de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Tutorial: informe de asignaciones &#40;Generador de informes&#41;](../../reporting-services/tutorial-map-report-report-builder.md)   
 [Mapas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Solucionar problemas de los informes: informes de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  