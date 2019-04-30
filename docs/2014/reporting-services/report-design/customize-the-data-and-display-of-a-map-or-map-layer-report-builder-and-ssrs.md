---
title: Personalizar los datos y la presentación de un mapa o una capa de mapa (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10521"
- sql12.rtp.rptdesigner.shared.shadowdv.f1
- "10515"
- "10512"
- "10520"
- "10523"
- sql12.rtp.rptdesigner.mapgroupproperties.variables.f1
- sql12.rtp.rptdesigner.mapgroupproperties.filter.f1
- sql12.rtp.rptdesigner.shared.number.f1
- sql12.rtp.rptdesigner.shared.font.f1
- sql12.rtp.rptdesigner.mapgroupproperties.general.f1
- "10507"
ms.assetid: fdd9b994-d138-4990-a291-279b0249eb72
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d3bd3ef7205591d0353d7e8ee75e2d0ec49a221d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185474"
---
# <a name="customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs"></a>Personalizar los datos y la presentación de un mapa o una capa de mapa (Generador de informes y SSRS)
  Después de agregar un mapa o una capa de mapa a un informe utilizando un asistente, puede que desee cambiar el aspecto del mapa en el informe. Puede realizar mejoras considerando las ideas siguientes:  
  
-   Para ayudar a los usuarios a entender cómo interpretar la presentación de los datos en un mapa, puede agregar leyendas y una escala de colores, además de etiquetas e información sobre herramientas.  
  
-   Para hacer que el mapa sea más fácil de leer, cambie el centro y el nivel de zoom, agregue una escala de distancia y muestre una cuadrícula de fondo.  
  
-   Para ayudar a controlar el tiempo de dibujo del mapa al ejecutar el informe, puede ajustar la resolución para simplificar sus elementos.  
  
-   Puede incrustar los elementos del mapa en la definición de informe y, a continuación, cambiar el modo en que aparece cada elemento individual. Por ejemplo, puede mostrar la ubicación de la oficina principal con un pin y la de las demás oficinas con un círculo.  
  
-   Puede agregar regiones personalizadas especificando sus propias expresiones de grupo de datos.  
  
-   Puede agregar una ubicación personalizada en un punto que especifique en una capa de mapa que tenga puntos incrustados. Puede establecer el valor y mostrar las propiedades de los puntos personalizados independientemente de otros puntos en una capa de punto.  
  
-   Para proporcionar más detalles, puede agregar vínculos a los elementos de mapa de cada capa en los que un usuario pueda hacer clic para abrir los informes relacionados.  
  
 Para obtener más ideas sobre cómo mejorar un informe, vea [Planear un informe &#40;Generador de informes&#41;](planning-a-report-report-builder.md).  
  
 Las opciones de pantalla afectan a cómo aparecen en el informe un mapa o las partes de un mapa. Algunas opciones controlan la apariencia del mapa, como los bordes y las fuentes, o el área que se representa en el mapa. Otras opciones controlan el contenido de cada capa, por ejemplo los tamaños de burbuja, los tipos de marcador, las etiquetas o la información sobre herramientas.  
  
 Un elemento de informe de mapa incluye las siguientes partes: el propio mapa, una ventanilla de mapa, un conjunto de títulos, un conjunto de leyendas (leyenda, escala de color y escala de distancia), un conjunto de capas, y un conjunto de elementos de mapa en cada capa (polígonos o líneas o puntos). Utilice la información de las secciones siguientes para saber qué cuadro de diálogo de propiedades controla las opciones de presentación de las diferentes partes de un mapa.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Map"></a> Cambiar las opciones de un mapa  
 En un elemento de informe de mapa, puede hacer lo siguiente:  
  
-   Agregar varios títulos.  
  
-   Agregar varias leyendas. Para cambiar el contenido de una leyenda, tiene que crear más leyendas y, a continuación, cambiar las reglas para especificar en qué leyenda se escriben los elementos de leyenda creados por cada regla.  
  
-   Agregar más capas.  
  
-   Ocultar o mostrar la escala de distancia o la escala de colores.  
  
-   Dar ilusión de profundidad especificando una sombra.  
  
 Para cambiar estas opciones, haga clic con el botón derecho en el mapa, haga clic en **Mapa**y cámbielas.  
  
 
  
##  <a name="Viewport"></a> Cambiar las opciones de la ventanilla  
 Utilice las opciones de la ventanilla para cambiar la vista del mapa que aparece en un informe.  
  
 El origen de datos espaciales podría proporcionar más espacio del que haya que mostrar en el informe. Puede utilizar la ventanilla para establecer el centro y el nivel de zoom, y para recortar el área del mapa.  
  
 Se pueden establecer las opciones siguientes para la ventanilla:  
  
-   Elegir el sistema de coordenadas y, para un sistema de coordenadas geográficas, elegir la proyección.  
  
-   Elegir el centro del mapa.  
  
-   Recortar la vista del mapa.  
  
-   Definir el nivel de zoom.  
  
-   Resolución y simplificación. Buscar un equilibro entre el tiempo de dibujo y los contornos detallados de las líneas y polígonos.  
  
 Para cambiar estas opciones, haga clic con el botón derecho en la ventanilla del mapa y use la página [Cuadro de diálogo Propiedades de ventanilla de mapa, General](../map-viewport-properties-dialog-box-general.md) y las páginas relacionadas.  
  

  
##  <a name="Legends"></a> Cambiar las opciones de las leyendas  
 Las leyendas ayudan a los usuarios a interpretar los datos de un mapa.  
  
 De forma predeterminada, todas las reglas que especifique para una capa agregan elementos a la primera leyenda. Además, todas las reglas de color muestran valores en la escala de colores.  
  
-   Para cambiar las opciones de presentación de la apariencia de la leyenda, incluida su posición en relación a la ventanilla, establezca las opciones en la propia leyenda.  
  
-   Para cambiar el contenido o el formato del contenido de una leyenda, cambie las opciones de la leyenda para las reglas correspondientes de una capa.  
  
 Para obtener más información, vea [Cambiar leyendas de mapa, escala de colores y reglas asociadas &#40;Generador de informes y SSRS&#41;](change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  

  
##  <a name="Layer"></a> Cambiar las opciones de la capa  
 Para mostrar las capas de un mapa, haga clic en él para seleccionarlo. Aparece el panel Mapa. Para cambiar las opciones de una capa, haga clic con el botón secundario en ella y utilice el menú contextual.  
  
 Una capa puede ser de uno de tres tipos en función de los datos espaciales que devuelva el origen de datos espaciales: una capa de polígono, una capa de línea o una capa de punto.  
  
 Se pueden establecer las opciones siguientes para la capa:  
  
-   Los datos analíticos y los campos coincidentes asociados. El origen de los datos espaciales se muestra en el panel Mapa debajo del nombre de la capa. Cuando se incrusta el origen, los elementos de mapa de la capa forman parte de la definición de informe. Si no se incrusta el origen, los datos espaciales se recuperan en tiempo de ejecución y el procesador de informes crea los elementos de mapa para la capa al procesar el informe. Para cambiar las opciones de datos de la capa, utilice la página Datos analíticos del cuadro de diálogo Capa del mapa.  
  
-   El orden de dibujo de las capas. El orden en que se ven las capas en panel Mapa es el orden inverso al orden en que se dibujan. Primero se dibuja la última capa de la lista. Por ejemplo, si desea que los puntos de una capa de punto aparezcan encima de los polígonos en la capa de polígono, la capa de punto debe ser la primera y la de polígono la segunda.  
  
-   La visibilidad de las capas, incluida la transparencia. Para hacer que una capa se muestre a través de otra, establezca la transparencia en un valor mayor que 0. El valor 100% significa que la capa no se ve. Para trabajar con una capa individual, puede mostrar u ocultar con facilidad cada capa de forma independiente utilizando el icono **Visibilidad** del panel Mapa. También puede establecer opciones de nivel de zoom para especificar cuándo se han de mostrar u ocultar los elementos de mapa de la capa según el nivel de zoom.  
  
-   Agregar una capa de mosaico de Bing Maps para el centro de la ventanilla actual y el nivel de zoom. No tiene que especificar las coordenadas geográficas para una capa de mosaico. Los mosaicos se cargan automáticamente para que coincidan con el área de ventanilla cuando el sistema de coordenadas es Geográfico, la proyección es Mercator, hay servidores de Bing Maps disponibles y el servidor de informes se ha configurado para admitir esta característica. Para cada informe, puede especificar si desea usar una conexión segura para recuperar los mosaicos.  
  
 Para más información sobre capas, vea [Agregar, cambiar o eliminar un mapa o una capa de mapa &#40;Generador de informes y SSRS&#41;](add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
##  <a name="DataGrouping"></a> Cambiar la agrupación de datos para la capa  
 Puede personalizar la forma de agregar datos espaciales para sus propias formas. Para establecer las propiedades de grupo de una capa, seleccione la capa en el panel Mapa y, en el panel de propiedades de la capa, haga clic en **Grupo**; luego, haga clic en los puntos suspensivos (...) para abrir las propiedades de grupo. En este cuadro de diálogo puede especificar expresiones de grupo, crear variables de grupo y filtrar datos que se usan para agrupar.  
  
 La expresión de grupo especifica cómo se agregan los datos analíticos que tienen relación con los datos espaciales para cada elemento de mapa de la capa. De forma predeterminada, la expresión de grupo es el conjunto de campos coincidentes que se especificó para la relación entre los datos espaciales y los datos analíticos. Por ejemplo, en un mapa de burbujas que muestra las ubicaciones de las ciudades y el tamaño de la población de un país o región, los campos coincidentes incluyen el nombre de la ciudad [City] y el nombre de la región [Region] porque puede haber varias ciudades con el mismo nombre. La expresión de grupo correspondiente incluye dos campos: [City ] y [Region].  
  
 Para obtener más información, consulte [Sugerencias sobre mapas: Cómo importar archivos de forma en SQL Server y agregar datos espaciales](https://go.microsoft.com/fwlink/?LinkID=214991).  
  
 
  
##  <a name="MapElements"></a> Cambiar las opciones de los elementos de mapa de la capa  
 Los elementos de mapa son los puntos, líneas o polígonos de una capa que se basan en los datos espaciales. Se pueden establecer las opciones siguientes para los elementos de mapa. Estas opciones se aplican a todos los elementos de mapa de la capa, tanto si están incrustados como si no:  
  
-   Etiquetas, visibilidad de etiquetas, desplazamiento de etiquetas y formato.  
  
-   Bordes y relleno.  
  
-   Acciones de obtención de detalles.  
  
-   Opciones de presentación.  
  
 Las opciones de presentación de los elementos de mapa siguen un orden de prioridad basado en la capa, el elemento de mapa, las reglas de los elementos de mapa y las opciones de invalidación de los elementos de mapa incrustados.  
  
 Para cambiar estas opciones, haga clic con el botón secundario en el elemento de mapa y utilice el cuadro de diálogo de propiedades incrustado. Por ejemplo, para un polígono incrustado, utilice el cuadro de diálogo Propiedades de polígono incrustado de mapa, página General y páginas relacionadas.  
  

  
##  <a name="Precedence"></a> Descripción de la prioridad de las opciones de presentación  
 Si desea controlar la apariencia de la presentación de un punto, línea o polígono en una capa de mapa, debe saber dónde se pueden establecer las opciones de presentación y qué opciones tienen una prioridad mayor. Las opciones de presentación siguientes se muestran de menor a mayor. Las opciones de presentación superiores invalidan las inferiores de esta lista:  
  
-   Opciones de las capas.  
  
-   Opciones de puntos, líneas o polígonos de cada capa. Se aplican tanto si los elementos de mapa se recuperan dinámicamente al procesar el informe como si están incrustados en la definición de informe. Por ejemplo, especifique un color de relleno para todos los elementos de una capa.  
  
-   Reglas. Puede establecer reglas para controlar el color, el tamaño, el ancho o el tipo de marcador de todos los elementos de mapa de una capa. Las reglas que puede establecer dependen del tipo de elemento de mapa.  
  
    -   Reglas de color. Se aplican a los marcadores para los puntos, líneas y polígonos, y a los marcadores para los puntos centrales de los polígonos.  
  
    -   Reglas de tamaño. Se aplican a los marcadores para los puntos y a los marcadores para los puntos centrales de los polígonos.  
  
    -   Reglas de ancho. Se aplican a los anchos de línea.  
  
    -   Reglas de tipo de marcador. Se aplican a los marcadores para los puntos y a los marcadores para los puntos centrales de los polígonos.  
  
-   Opciones de invalidación de los puntos, líneas o polígonos incrustados individuales de una capa. Los cambios que realice son permanentes. Para revertir estos cambios, debe volver a cargar los datos de la capa.  
  
 Para obtener más información, vea [Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos &#40;Generador de informes y SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  

  
## <a name="see-also"></a>Vea también  
 [Asistente para mapas y Asistente para capas de mapa &#40;Generador de informes y SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)   
 [Mapas &#40;Generador de informes y SSRS&#41;](maps-report-builder-and-ssrs.md)  
  
  
