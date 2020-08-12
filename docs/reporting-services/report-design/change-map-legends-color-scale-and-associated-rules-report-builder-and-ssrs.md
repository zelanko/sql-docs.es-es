---
title: Cambiar leyendas de mapa, escala de colores y reglas asociadas en Generador de informes y SSRS | Microsoft Docs
description: Obtenga información sobre cómo cambiar las leyendas de los mapas para ayudar a los usuarios a interpretar la visualización de datos en los mapas del Generador de informes.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.mapcolorscaleproperties.labels.f1
- sql13.rtp.rptdesigner.mappointlayerproperties.typerules.f1
- sql13.rtp.rptdesigner.shared.maprulesdistribution.f1
- "10512"
- "10539"
- "10533"
- sql13.rtp.rptdesigner.maplegendtitleproperties.general.f1
- "10534"
- "10516"
- sql13.rtp.rptdesigner.mapdistancescaleproperties.general.f1
- sql13.rtp.rptdesigner.mapcolorscaleproperties.general.f1
- sql13.rtp.rptdesigner.mapcolorscaletitleproperties.general.f1
- "10514"
- sql13.rtp.rptdesigner.mappointlayerproperties.sizerules.f1
- "10513"
- sql13.rtp.rptdesigner.shared.mapruleslegend.f1
- sql13.rtp.rptdesigner.shared.embeddedlabels.f1
- "10510"
- "10509"
- sql13.rtp.rptdesigner.maplegendproperties.general.f1
- "10540"
- "10517"
ms.assetid: a1d691b2-c5ae-420f-af60-b7c54a7385a4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: deb79a6a1216f584bdbda3a54b276326e5152f01
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054239"
---
# <a name="change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs"></a>Cambiar leyendas de mapa, escala de colores y reglas asociadas (Generador de informes y SSRS)
  En un informe paginado de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , un mapa puede contener leyendas de mapa, una escala de colores y una escala de distancia. Estas partes de un mapa ayudan a los usuarios a interpretar la visualización de los datos del mapa.  
  
 Las leyendas incluyen las siguientes partes de un mapa:  
  
-   **Leyenda del mapa:** muestra una guía para ayudar a interpretar los datos analíticos que varían la presentación de los elementos de mapa en una capa de mapa. Un mapa puede tener varias leyendas. En cada capa de mapa, especifique qué leyenda se va a utilizar. Una leyenda puede proporcionar una guía a más de una capa de mapa.  
  
-   **Escala de color:** Muestra una guía para ayudar a interpretar los colores del mapa. Un mapa tiene una escala del color. Varios capas pueden proporcionar los datos de la escala de color.  
  
-   **Escala de distancia:** Muestra una guía para ayudar a interpretar la escala del mapa. Un mapa tiene una escala de distancia. El valor de zoom de la ventanilla central del mapa actual determina la escala de distancia.  
  
 ![rs_MapElements](../../reporting-services/report-design/media/rs-mapelements.gif "rs_MapElements")  
  
##  <a name="to-change-the-position-of-a-legend-relative-to-the-viewport"></a><a name="Viewport"></a> Para cambiar la posición de una leyenda con respecto a la ventanilla  
  
#### <a name="to-change-the-position-of-a-legend-relative-to-the-viewport"></a>Para cambiar la posición de una leyenda con respecto a la ventanilla  
  
1.  En la vista Diseño, haga clic con el botón derecho en la leyenda y abra la página **Propiedades de** _\<report item>_ .  
  
2.  En **Posición**, haga clic en la ubicación que especifica dónde desea mostrar la leyenda con respecto a la ventanilla.  
  
3.  Para mostrar la leyenda fuera de la ventanilla, seleccione **Mostrar \<report item> fuera de la ventanilla**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  En la vista previa, las leyendas de mapa y la escala de colores solo aparecen cuando hay resultados de las reglas relacionadas con esa leyenda. Si no hay ningún elemento que mostrarse, la leyenda no aparece en el informe representado.  
  
##  <a name="to-change-the-layout-of-a-map-legend"></a><a name="MapLegend"></a> Cambiar el diseño de la leyenda de un mapa  
  
#### <a name="to-change-the-layout-of-a-map-legend"></a>Cambiar el diseño de la leyenda de un mapa  
  
1.  En la vista Diseño, haga clic con el botón derecho en la leyenda y, después, abra la página **Propiedades de la leyenda** .  
  
2.  En **Diseño de la leyenda**, haga clic en el diseño de la tabla que desea utilizar para la leyenda. Según haga clic en las diferentes opciones, cambiará la disposición de la superficie de diseño.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-show-or-hide-a-map-legend-title"></a><a name="MapLegendTitle"></a> Mostrar u ocultar el título de una leyenda de mapa  
  
#### <a name="to-show-or-hide-a-map-legend-title"></a>Mostrar u ocultar el título de una leyenda de mapa  
  
-   Haga clic con el botón derecho en la leyenda de mapa en la superficie de diseño y, después, haga clic en **Mostrar título de leyenda**.  
  
##  <a name="to-show-or-hide-a-color-scale-title"></a><a name="ColorScaleTitle"></a> Mostrar u ocultar el título de una escala de colores  
  
#### <a name="to-show-or-hide-a-color-scale-title"></a>Mostrar u ocultar el título de una escala de colores  
  
-   Haga clic con el botón derecho en la escala de colores en la superficie de diseño y, después, haga clic en **Mostrar título de escala de colores**.  
  
##  <a name="to-move-items-out-of-the-first-legend"></a><a name="MoveItems"></a> Sacar elementos de la primera leyenda  
 Cree tantas leyendas adicionales cuando necesite y, a continuación, actualice las reglas para cada capa de mapa especificando qué leyenda muestran los resultados de la regla.  
  
#### <a name="to-create-a-new-legend"></a>Crear una nueva leyenda  
  
-   En la vista Diseño, haga clic con el botón derecho fuera de la ventanilla del mapa y, después, haga clic en **Agregar leyenda**.  
  
     Una nueva leyenda aparece en el mapa.  
  
#### <a name="to-display-rule-results-in-a-legend"></a>Mostrar los resultados de la regla en una leyenda  
  
1.  En la vista Diseño, haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa que contenga los datos que quiere y, después, haga clic en **Regla de color de** _\<map element type>_ .  
  
3.  Haga clic en **Leyenda**.  
  
4.  En la lista desplegable **Mostrar en esta leyenda** , haga clic en el nombre de la leyenda para mostrar los resultados de la regla.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-vary-map-element-colors-based-on-a-template-style"></a><a name="TemplateStyle"></a> Variar los colores del elemento de mapa según un estilo de plantilla  
  
#### <a name="to-vary-map-element-colors-based-on-a-template-style"></a>Variar los colores del elemento de mapa según un estilo de plantilla  
  
1.  En la vista Diseño, haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa que contenga los datos que quiere y, después, haga clic en **Regla de color de** _\<map element type>_ .  
  
3.  Haga clic en **Aplicar estilo de plantilla**.  
  
     Un estilo de plantilla especifica una fuente, un estilo de borde y una paleta de colores. Cada elemento de mapa tiene asignado un color diferente de la paleta de colores para el tema que se especificó en el Asistente para mapas o en el Asistente para capas de mapa. Esta es la única opción que se aplica a las capas que no tienen asociados datos analíticos.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-vary-map-element-colors-based-on-color-palette"></a><a name="ColorPalette"></a> Variar los colores del elemento de mapa según la paleta de colores  
  
#### <a name="to-vary-map-element-colors-based-on-color-palette"></a>Variar los colores del elemento de mapa según la paleta de colores  
  
1.  En la vista Diseño, haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa que contenga los datos que quiere y, después, haga clic en **Regla de color de** _\<map element type>_ .  
  
3.  Haga clic en **Visualizar datos mediante la paleta de colores**.  
  
     Esta opción usa una paleta integrada o personalizada que especifique. Según los datos analíticos relacionados, a cada elemento de mapa se le asigna un color o tonalidad de color diferente de la paleta.  
  
4.  En **Campo de datos**, escriba el nombre del campo que contenga los datos analíticos que desea visualizar por color.  
  
5.  En **Paleta**, en la lista desplegable, seleccione el nombre de la paleta que quiere usar.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-vary-map-element-colors-based-on-color-ranges"></a><a name="ColorRanges"></a> Variar los colores del elemento de mapa según las gamas de colores  
  
#### <a name="to-vary-map-element-colors-based-on-color-ranges"></a>Variar los colores del elemento de mapa según las gamas de colores  
  
1.  En la vista Diseño, haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa que contenga los datos que quiere y, después, haga clic en **Regla de color de** _\<map element type>_ .  
  
3.  Haga clic en **Visualizar datos mediante los rangos de colores**.  
  
     Esta opción, combinada con los colores inicial, intermedio y final que especifique en esta página y las opciones que especifique en la página **Distribución** , divide los datos analíticos relacionados en rangos. El procesador de informes asigna el color adecuado a cada elemento de mapa en función de sus datos asociados y del intervalo en el que están englobados.  
  
4.  En **Campo de datos**, escriba el nombre del campo que contenga los datos analíticos que desea visualizar por color.  
  
5.  En **Color inicial**, especifique el color que desea utilizar para el intervalo inferior.  
  
6.  En **Color intermedio**, especifique el color que desea utilizar para el intervalo intermedio.  
  
7.  En **Color final**, especifique el color que desea utilizar para el intervalo superior.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-vary-map-element-colors-based-on-custom-colors"></a><a name="CustomColors"></a> Variar los colores del elemento de mapa según los colores personalizados  
  
#### <a name="to-vary-map-element-colors-based-on-custom-colors"></a>Variar los colores del elemento de mapa según los colores personalizados  
  
1.  En la vista Diseño, haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa que contenga los datos que quiere y, después, haga clic en **Regla de color de** _\<map element type>_ .  
  
3.  Haga clic en **Visualizar datos mediante los colores personalizados**.  
  
     Esta opción usa la lista de colores que especifique. Según los datos analíticos relacionados, a cada elemento de mapa se le asigna un color de la lista. Si hay más elementos de mapa que colores, no se asigna ningún color.  
  
4.  En **Campo de datos**, escriba el nombre del campo que contenga los datos analíticos que desea visualizar por color.  
  
5.  En **Colores personalizados**, haga clic en **Agregar** para especificar cada color personalizado.  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-set-distribution-options-for-a-legend"></a><a name="DistributionOptions"></a> Establecer las opciones de distribución de una leyenda  
  
#### <a name="to-set-distribution-options-for-a-legend"></a>Establecer las opciones de distribución de una leyenda  
  
1.  En la vista Diseño, haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa que contenga los datos que quiere y, después, haga clic en **Regla de color de** _\<map element type>_ .  
  
3.  Seleccione la opción **Visualizar datos mediante** \<rule type>. Para utilizar las opciones de distribución, debe crear intervalos en la página **Distribución** según los datos analíticos asociados a la capa.  
  
4.  Haga clic en **Distribución**.  
  
5.  Seleccione uno de los tipos de distribución siguientes:  
  
    -   **EqualInterval**. Especifica intervalos que dividen los datos en subintervalos iguales.  
  
    -   **EqualDistribution**. Especifica intervalos que dividen los datos de modo que cada intervalo tenga un número igual de elementos.  
  
    -   **Óptimo**. Especifica intervalos que ajustan automáticamente la distribución para crear subintervalos equilibrados.  
  
    -   **Personalizado**. Especifique su propio número de intervalos para controlar la distribución de valores.  
  
     Para obtener más información sobre las opciones de distribución, vea [Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
6.  En **Número de subrangos**, escriba el número de subrangos que va a utilizar. Cuando el tipo de distribución es **Óptimo**, el número de subrangos se calcula automáticamente.  
  
7.  En **Inicio de intervalo**, escriba el valor mínimo del intervalo. Todos los valores menores que este número son el mismo que el mínimo del intervalo.  
  
8.  En **Final de intervalo**, escriba el valor máximo del intervalo. Todos los valores mayores que este número son el mismo que el máximo del rango.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-change-the-contents-of-a-rule-legend"></a><a name="RuleLegend"></a> Cambiar el contenido de una leyenda de la regla  
  
#### <a name="to-change-the-contents-of-a-color-size-width-or-marker-type-legend"></a>Cambiar el contenido de una leyenda de tipo de color, tamaño, ancho o marcador  
  
1.  En la vista Diseño, haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa que contenga los datos que quiere y, después, haga clic en **Regla de** _\<map element type>_ .  
  
3.  Compruebe que se ha seleccionado **Visualizar datos mediante** \<*rule type*>.  
  
4.  En **Campo de datos**, compruebe que los datos analíticos que está visualizando en la capa están seleccionados.  
  
    > [!NOTE]  
    >  Si no aparece ningún campo en la lista desplegable, haga clic con el botón derecho en la capa y, después, haga clic en **Datos de la capa** para abrir la página Datos analíticos del cuadro de diálogo Propiedades de datos de capa de mapa y comprobar que ha especificado los datos analíticos para esta capa.  
  
5.  Haga clic en **Leyenda**.  
  
6.  En **Mostrar en esta leyenda**, seleccione la leyenda de mapa que desea utilizar para mostrar los resultados de la regla.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-change-the-contents-of-the-color-scale"></a><a name="ColorScale"></a> Cambiar los contenidos de la escala de colores  
  
#### <a name="to-change-the-contents-of-the-color-scale-or-a-color-legend"></a>Para cambiar el contenido de la escala de colores o una leyenda de regla de colores  
  
1.  En la vista Diseño, haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa que contenga los datos que quiere y, después, haga clic en **Regla de color de** _\<map element type>_ .  
  
3.  Seleccione la opción de regla de color que desee usar. Para mostrar los elementos en una leyenda de mapa o escala de colores, debe seleccionar una de las opciones de **Visualizar datos mediante** \<rule type>.  
  
4.  En **Campo de datos**, compruebe que los datos analíticos que está visualizando en la capa están seleccionados.  
  
    > [!NOTE]  
    >  Si no aparece ningún campo en la lista desplegable, haga clic con el botón derecho en la capa y, después, haga clic en **Datos de la capa** para abrir la página Datos analíticos del cuadro de diálogo Propiedades de datos de capa de mapa y comprobar que ha especificado los datos analíticos para esta capa.  
  
5.  Haga clic en **Leyenda**.  
  
6.  En **Opciones de escala de colores**, seleccione **Mostrar en escala de colores** para mostrar los resultados de la regla en la escala de colores. Puede especificar esta opción para más de una regla de color.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-remove-all-items-from-a-legend"></a><a name="HideItems"></a> Quitar todos los elementos de una leyenda  
  
#### <a name="to-hide-items-based-on-a-rule"></a>Ocultar elementos basados en una regla  
  
1.  En la vista Diseño, haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa que contenga los datos que quiere y, después, haga clic en **Regla de** _\<map element type>_ .  
  
3.  Haga clic en **Leyenda**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="to-change-the-format-of-content-in-a-legend"></a><a name="ChangeFormatItems"></a> Cambiar el formato del contenido de una leyenda  
 Establezca las opciones de leyenda para la regla que está asociada a la leyenda de mapa.  
  
#### <a name="to-change-the-format-of-content-in-a-legend"></a>Cambiar el formato del contenido de una leyenda  
  
1.  En la vista Diseño, haga clic en el mapa hasta que aparezca el panel Mapa.  
  
2.  Haga clic con el botón derecho en la capa que contenga los datos que quiere y, después, haga clic en **Regla de** _\<map element type>_ .  
  
3.  Haga clic en **Leyenda**.  
  
4.  **Texto de leyenda** muestra las palabras clave que especifican qué datos aparecen en la leyenda. Use las palabras clave y los formatos personalizados para ayudar a controlar el formato del texto de la leyenda. Por ejemplo, #FROMVALUE {C2} especifica un formato de moneda con dos posiciones decimales. Para obtener más información, vea [Variar la presentación de polígonos, líneas y puntos usando reglas y datos analíticos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Mapas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Agregar, cambiar o eliminar un mapa o una capa de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Personalizar los datos y la presentación de un mapa o una capa de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Solucionar problemas de los informes: informes de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)   
 [Asistente para mapas y Asistente para capas de mapa &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
