---
title: "Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10538"
- "10537"
- sql13.rtp.rptdesigner.mapembeddedpolygonlayerproperties.general.f1
- MICROSOFT.REPORTDESIGNER.MAPMARKER.MARKERSTYLE
- sql13.rtp.rptdesigner.mapembeddedlinelayerproperties.general.f1
- sql13.rtp.rptdesigner.mapembeddedpointlayerproperties.general.f1
- "10531"
- "10536"
- sql13.rtp.rptdesigner.maplinelayerproperties.widthrules.f1
ms.assetid: 7f1f5584-37b4-4fa2-ae44-8988c5f0c744
caps.latest.revision: "12"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 464731c279d55f20b725193cde9db1e5f2974bf2
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="vary-polygon-line-and-point-display-by-rules-and-analytical-data"></a>Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos
  Las opciones de presentación de polígonos, líneas y puntos en una capa de mapa se controlan estableciendo las opciones de la capa y las reglas para los elementos de mapa de la capa, o invalidando las opciones de elementos de mapa insertados concretos de una capa.  
  
 Las opciones de presentación se aplican con una prioridad concreta, que se menciona de menor a mayor:  
  
1.  Las opciones establecidas en una capa de polígono, una capa de línea o una capa de punto se aplican a todos los elementos de mapa de dicha capa, tanto si los elementos de mapa se incrustan en la definición de informe como si no.  
  
2.  Las opciones establecidas para las reglas se aplican a todos los elementos de mapa de una capa. Todas las opciones de visualización de datos se aplican únicamente a los elementos de mapa que están asociados a datos espaciales. Una opción de visualización de datos exige que se especifique un campo de datos en el que basar las variaciones de la presentación. Debe haber establecido los campos coincidentes de los datos analíticos y espaciales para poder aplicar las reglas de visualización de datos. Para más información, vea [Mapas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
3.  Las opciones que establece para los elementos de mapa insertados seleccionados. Tenga en cuenta que, al invalidar las opciones de capa, los cambios que realice en la definición de informe serán permanentes. Puede cambiar los valores de los campos de datos así como invalidar las opciones de presentación para personalizar la manera en que polígonos, líneas y puntos concretos aparecen en una capa.  
  
 Además de controlar la presentación de los elementos de mapa en una capa, puede controlar la transparencia de las capas para permitir que las capas dibujadas anteriormente se muestren a través de las capas que se dibujen después. Para más información sobre cómo cambiar las opciones que afectan al mapa o la capa de mapa completa, vea [Personalizar los datos y la presentación de un mapa o una capa de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Rules"></a> Descripción de las reglas  
 Puede establecer cuatro tipos de reglas que permiten al procesador de informes ajustar automáticamente las propiedades de presentación de los elementos de mapa en una capa. Las reglas varían en función del tipo de elemento de mapa: polígonos, líneas o puntos.  
  
-   **Polígonos.** Varíe el color del polígono.  
  
    -   **Puntos centrales de polígono.** Para los marcadores que se muestran en el punto central de cada polígono, varíe el color, el tamaño y el tipo de marcador.  
  
-   **Líneas.** Varíe el color y el ancho de línea.  
  
-   **Puntos.** Para los marcadores que se muestran para cada punto, varíe el color, el tamaño y el tipo de marcador.  
  
##  <a name="Color"></a> Descripción de las reglas de color  
 Las reglas de color se aplican a los colores de relleno para los polígonos, líneas y marcadores que representan puntos o puntos centrales del polígono.  
  
 Las reglas de color admiten cuatro opciones:  
  
-   Aplicar estilo de plantilla. El tema que eligió en el asistente define el estilo de plantilla para la capa. El tema establece el estilo para la fuente, el estilo de borde y la paleta.  
  
-   Visualizar datos mediante el uso de la paleta de colores. Especifique una paleta por el nombre. El procesador de informes establece el color de cada elemento de mapa de una capa recorriendo cada color de la paleta y aplicando consecutivamente tonalidades más claras de cada color en la paleta.  
  
-   Visualizar datos mediante el uso de rangos de colores. Se especifica un color inicial, intermedio y final. A continuación, se especifican las opciones de distribución. El procesador de informes utiliza los valores de opción de distribución para crear un conjunto de colores que produzca una presentación similar a un mapa térmico. Un mapa térmico muestra el color en relación con la temperatura. Por ejemplo, en una escala de 0 a 100, los valores bajos se muestran en color azul para representar frío y los valores altos en color rojo para representar calor.  
  
-   Visualizar datos mediante el uso de colores personalizados. Se especifica un conjunto de colores. El procesador de informes establece el color de cada elemento de mapa de la capa recorriendo los valores que se especifican.  
  
 La paleta predeterminada incluye el color blanco. Para evitar el fuerte contraste entre el blanco y otros colores de la paleta, especifique un color inicial claro en la paleta.  
  
 Para mostrar sin color los elementos de mapa que no estén asociados a datos, establezca **Ningún color** como color predeterminado de los elementos de mapa de la capa.  
  
### <a name="color-scale"></a>Escala de colores  
 De forma predeterminada, todos los valores de regla de color aparecen en la escala de colores, además de aparecer en la primera leyenda. La escala de colores está diseñada para mostrar una gama de colores. Elija los datos más importantes para mostrarse en la escala de colores.  
  
 Para quitar los valores que no desee en la escala de colores, borre la opción correspondiente para cada regla de color de cada capa.  
  
##  <a name="Width"></a> Descripción de las reglas de ancho de línea  
 Las reglas de ancho se aplican a las líneas. Admiten dos opciones:  
  
-   Usar ancho de línea predeterminado. Especifique el ancho de línea en puntos.  
  
-   Visualizar datos mediante el uso de ancho de línea. Establezca los anchos máximo y mínimo para la línea, especifique el campo de datos que desea utilizar para variar el ancho y, a continuación, especifique las opciones de distribución que se aplicarán a esos datos.  
  
##  <a name="Size"></a> Descripción de las reglas del tamaño de marcador  
 Las reglas de tamaño se aplican a los marcadores que representan puntos o puntos centrales de polígono. Las reglas de tamaño admiten dos opciones:  
  
-   Usar tamaño de marcador predeterminado. Especifique el tamaño en puntos.  
  
-   Visualizar datos mediante el uso de tamaño. Establezca los tamaños máximo y mínimo para el marcador, especifique el campo de datos que desea utilizar para variar el tamaño y, a continuación, especifique las opciones de distribución que se aplicarán a esos datos.  
  
##  <a name="Marker"></a> Descripción de las reglas del tipo de marcador  
 Las reglas de tipo de marcador se aplican a los marcadores que representan puntos o puntos centrales de polígono. Las reglas de tipo de marcador admiten dos opciones:  
  
-   Usar tipo de marcador predeterminado. Especifique uno de los tipos de marcador disponibles.  
  
-   Visualizar datos mediante el uso de marcadores. Especifique un conjunto de marcadores y el orden en el que desea utilizarlos. Entre los tipos de marcadores se incluyen: **Circle**, **Diamond**, **Pentagon**, **PushPin**, **Rectangle**, **Star**, **Triangle**, **Trapezoid**y **Wedge**.  
  
##  <a name="Distribution"></a> Descripción de las opciones de distribución  
 Para crear una distribución de valores, puede dividir los datos en intervalos. Especifique el tipo de distribución, el número de subintervalos y los valores mínimo y máximo del intervalo.  
  
 En la lista siguiente, suponga que tiene tres elementos de mapa y seis valores analíticos relacionados que van de 1 a 9999 con los valores siguientes: 1, 10, 200, 2000, 4777 y 8999.  
  
-   **EqualInterval** . Cree intervalos que dividan los datos en intervalos de rangos iguales. En el ejemplo, los tres intervalos serían 0-2999, 3000-5999, 6000-8999. Subintervalo 1: 1, 10, 200, 500. Subintervalo 2: 4777. Subintervalo 3: 8999. Este método no tiene en cuenta cómo se distribuyen los datos. Los valores muy grandes o muy pequeños pueden sesgar los resultados de la distribución.  
  
-   **EqualDistribution** . Cree intervalos que dividan los datos de modo que cada intervalo tenga un número igual de elementos. En los datos de ejemplo, los tres intervalos serían 0-10, 11-500, 501-8999. Subintervalo 1: 1, 10. Subintervalo 2: 200, 500. Subintervalo 3: 4777, 8999. Este método puede sesgar la distribución al crear divisiones que abarcan intervalos muy grandes o muy pequeños.  
  
-   **Óptimo** . Cree intervalos que ajusten automáticamente la distribución para crear subintervalos equilibrados. El algoritmo determina el número de subintervalos.  
  
-   **Personalizado.** Especifique su propio número de intervalos para controlar la distribución de valores. En los datos de ejemplo, puede especificar tres intervalos: 1-2, 3-8, 9.  
  
 Las reglas utilizan los valores de distribución para variar los valores de presentación de los elementos de mapa.  
  
##  <a name="Legends"></a> Descripción de las leyendas y sus elementos  
 Las reglas que se especifican para cada capa crean automáticamente los elementos de leyenda. Las opciones de regla controlan cuántos elementos se crean y en qué leyenda aparecen. De forma predeterminada, todos los elementos de todas las reglas se agregan a la primera leyenda. Para retirar los elementos de la primera leyenda, cree tantas leyendas adicionales como sean necesarias y, para cada regla, especifique la leyenda que se utilizará para mostrar los elementos que sean resultado de la regla. Para ocultar los elementos en función de una regla, especifique un nombre de leyenda en blanco.  
  
 Para controlar dónde aparece una leyenda, utilice el cuadro de diálogo Propiedades de la leyenda a fin de especificar una posición en relación a la ventanilla del mapa. Para más información, vea [Cambiar leyendas de mapa, escala de colores y reglas asociadas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
 Las leyendas se expanden automáticamente para mostrar el título o el texto. Para dar formato al texto de los elementos de leyenda, use palabras clave y formatos personalizados de leyenda de mapa. Para más información, consulte [To change the format of content in a legend](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md#ChangeFormatItems).  
  
 En las tablas siguientes se muestran ejemplos de distintos formatos que puede usar.  
  
|Palabra clave y formato|Description|El ejemplo de lo que aparece como texto en la leyenda|  
|------------------------|-----------------|---------------------------------------------------|  
|`#FROMVALUE {C0}`|Muestra la moneda del valor total sin posiciones decimales.|400 $|  
|`#FROMVALUE {C2}`|Muestra la moneda del valor total con dos posiciones decimales.|400,55 $|  
|`#TOVALUE`|Muestra el valor numérico real del campo de datos.|10000|  
|`#FROMVALUE{N0} - #TOVALUE{N0}`|Muestra los valores numéricos reales del principio y el fin del intervalo.|10 - 790|  
  
## <a name="see-also"></a>Vea también  
 [Cambiar leyendas de mapa, escala de colores y reglas asociadas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)   
 [Mapas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Asistente para mapas y Asistente para capas de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
