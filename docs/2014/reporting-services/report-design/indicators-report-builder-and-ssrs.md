---
title: Indicadores (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10545"
- "10547"
- sql12.rtp.rptdesigner.indicatorproperties.general.f1
- sql12.rtp.rptdesigner.indicatorproperties.action.f1
- "10546"
- sql12.rtp.rptdesigner.indicatorproperties.validateandstates.f1
ms.assetid: 2edbd279-be39-4d97-b1b6-ddbc5b17c422
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a6f13d8d76854c3fdf01dceeeb61c4d06f2a0e16
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48142465"
---
# <a name="indicators-report-builder-and-ssrs"></a>Indicadores (Generador de informes y SSRS)
  Los indicadores son medidores mínimos que comunican el estado del valor de un dato de un vistazo. Los iconos que representan a los indicadores y sus estados son simples y visualmente efectivos incluso cuando su tamaño es pequeño.  
  
 Puede usar indicadores de estado en los informes para mostrar lo siguiente:  
  
-   Tendencias por tendencia al alta, planas (ningún cambio) o tendencia a la baja.  
  
-   El estado usando símbolos reconocidos habitualmente como marcas de verificación y signos de admiración.  
  
-   Condiciones mediante formas reconocidas habitualmente como semáforos y signos.  
  
-   Calificaciones con formas reconocidas comunes y símbolos que muestran el progreso como un número de cuadrantes en un cuadrado y estrellas.  
  
 Aunque los indicadores se pueden utilizar solos en paneles o en informes de forma libre, se suelen usar más en tablas o matrices para visualizar los datos en filas o columnas. El siguiente diagrama muestra una tabla con un indicador de semáforo que comunica las ventas anuales hasta la fecha por persona y territorio de ventas.  
  
 ![rs_IndicatorTableTrafficLight](../media/rs-indicatortabletrafficlight.gif "rs_IndicatorTableTrafficLight")  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona conjuntos de indicadores integrados e iconos de indicadores para usarlos tal cual, pero también puede personalizar iconos de indicadores individuales y conjuntos de indicadores para satisfacer sus necesidades.  
  
 Para obtener más información sobre el uso de indicadores como KPI, vea [Tutorial: Agregar un KPI a un informe &#40;Generador de informes&#41;](../tutorial-adding-a-kpi-to-your-report-report-builder.md).  
  
> [!NOTE]  
>  Puede publicar indicadores por separado de un informe como elementos de informe. [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="ComparingIndicatorsToGauges"></a> Comparar indicadores con medidores  
 Aunque parecen muy diferentes, los indicadores no son más que unos medidores sencillos. Los indicadores y los medidores muestran un valor de datos único. Las diferencias clave son que los medidores tienen elementos como marcos y punteros. Los indicadores solo tienen estados, iconos y (opcionalmente) etiquetas. Los estados de los indicadores son parecidos a los intervalos de los medidores.  
  
 Igual que los medidores, los indicadores se colocan dentro del panel de un medidor. Si desea configurar un indicador mediante el cuadro de diálogo **Propiedades de los indicadores** o el panel Propiedades, debe seleccionar el indicador en lugar del panel. De lo contrario, las opciones disponibles son solo las correspondientes al panel del medidor y no puede configurar el indicador. La imagen siguiente muestra un indicador seleccionado en su panel de medidor.  
  
 ![rs_GaugePanelWithIndicator](../media/rs-gaugepanelwithindicator.gif "rs_GaugePanelWithIndicator")  
  
 Dependiendo de cómo desee representar el valor de datos, los medidores podrían ser más eficaces que los indicadores. Para obtener más información, vea [Medidores &#40;Generador de informes y SSRS&#41;](gauges-report-builder-and-ssrs.md).  
  
  
##  <a name="ChoosingIndicatorTypes"></a> Elegir el tipo de indicador para usar  
 Usar el conjunto de indicadores adecuado es esencial para comunicar el significado de los datos al instante, tanto si los datos están en una fila de detalle o en un grupo de filas o de columnas en una tabla o matriz, o solos en el cuerpo o el panel del informe. Los conjuntos de indicadores integrados tienen tres iconos o más. Los iconos pueden variar en la forma, color o ambos. Cada icono comunica un estado de los datos diferente.  
  
 En la siguiente tabla se enumeran los conjuntos de indicadores integrados y se describen algunos de sus usos habituales.  
  
|Conjunto de indicadores|Tipo de indicador|  
|-------------------|--------------------|  
|![Rs_DirectionalIcons](../media/rs-directionalicons.gif "Rs_DirectionalIcons")|Direccional: indica las tendencias mediante flechas hacia arriba, abajo, plana (sin cambios), de tendencia al alza o de tendencia a la baja.|  
|![Rs_SymbolIcons](../media/rs-symbolicons.gif "Rs_SymbolIcons")|Símbolos: indica los estados utilizando símbolos muy conocidos como marcas de verificación y signos de admiración.|  
|![Rs_ShapeIcons](../media/rs-shapeicons.gif "Rs_ShapeIcons")|Forma: indica las condiciones utilizando formas muy conocidas, como señales de tráfico y formas romboidales.|  
|![rs_RatingIcons](../media/rs-ratingicons.gif "rs_RatingIcons")|Clasificaciones: indica las clasificaciones mediante formas y símbolos muy conocidos que muestran valores progresivos, como el número de cuadrantes en un cuadrado.|  
  
 Después de elegir un conjunto de indicadores, puede personalizar la apariencia de cada icono de indicador del conjunto estableciendo sus propiedades en los cuadros de diálogo para indicadores o en el panel Propiedades. Puede usar los colores, iconos y tamaños integrados o expresiones para configurar los indicadores.  
  
  
##  <a name="CustomizingIndicators"></a> Personalizar indicadores  
 Los indicadores se pueden personalizar para satisfacer sus necesidades. Puede modificar los conjuntos de indicadores y el icono de indicador individual de un conjunto como se indica a continuación:  
  
-   Cambiar los colores de los iconos de indicador. Por ejemplo, podría desear que la combinación de colores de un conjunto de indicadores sea monocroma o utilizar colores que no sean los predeterminados.  
  
-   Cambiar el icono en el conjunto de indicadores. Por ejemplo, podría desear usar los iconos de estrella, círculo y cuadrado en un conjunto de indicadores.  
  
-   Especificar los valores inicial y final de un indicador. Por ejemplo, podría desear presentar de manera sesgada la visualización de los datos utilizando un icono para el 75 por ciento de los valores del indicador.  
  
-   Agregar iconos al conjunto de indicadores. Por ejemplo, podría desear agregar iconos adicionales a los conjuntos de indicadores para diferenciar los valores de indicador de una forma más detallada.  
  
-   Eliminar iconos del conjunto de indicadores para que los datos se muestren de forma más sencilla, utilizando solo unos cuantos iconos.  
  
 Para obtener más información, vea [Change Indicator Icons and Indicator Sets &#40;Report Builder and SSRS&#41;](change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md).  
  
  
##  <a name="UsingIndicatorsInTablesMatrices"></a> Usar indicadores en tablas y matrices  
 Las formas simples de los indicadores hacen que sean idóneos para su uso en tablas y matrices. Los indicadores son efectivos incluso si su tamaño es pequeño. Esto les confiere su utilidad en las filas de detalle o de grupo de los informes.  
  
 El siguiente diagrama muestra un informe con una tabla que usa el conjunto de indicadores direccionales **Four Arrows (Colored)** para indicar las ventas. Los iconos de indicador del informe se configuran de forma que usen tonos de azul en lugar de los colores predeterminados: rojo, amarillo y verde.  
  
 ![rs_IndicatorReportBlueArrows](../media/rs-indicatorreportbluearrows.gif "rs_IndicatorReportBlueArrows")  
  
 Para obtener más información sobre cómo agregar, modificar y eliminar indicadores, vea [Add or Delete an Indicator &#40;Report Builder and SSRS&#41;](add-or-delete-an-indicator-report-builder-and-ssrs.md).  
  
 La primera vez que se agrega un indicador a un informe, se configura para que use los valores predeterminados. Posteriormente, los valores se pueden cambiar para que el indicador represente los datos de la manera deseada. Puede cambiar la apariencia de los iconos del indicador, la manera en que el indicador elige qué icono utilizar, y cambiar los iconos utilizados por un conjunto de indicadores. Para obtener más información, vea [Change Indicator Icons and Indicator Sets &#40;Report Builder and SSRS&#41;](change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md).  
  
 De forma predeterminada, los indicadores se configuran para utilizar los porcentajes como la unidad de medida y detectar automáticamente los valores máximo y mínimo en los datos. Cada icono del conjunto de indicadores tiene un intervalo de porcentaje. El número de intervalos de porcentaje depende del número de iconos en el conjunto de iconos, pero los intervalos tienen el mismo tamaño y son secuenciales. Por ejemplo, si el conjunto de iconos tiene cinco iconos, hay cinco intervalos de porcentaje, cada uno de un tamaño del 20 por ciento. El primero comienza en 0 y finaliza en 20, el segundo comienza en 20 y finaliza en 40, y así sucesivamente. El indicador del informe utiliza el icono del conjunto de indicadores que tenga un intervalo de porcentaje dentro del que se encuentra el valor de los datos del indicador. Puede cambiar el intervalo de porcentaje para cada icono del conjunto. Los valores máximo y mínimo se pueden establecer explícitamente proporcionando un valor o una expresión. Puede cambiar la unidad de medida para que sea un valor numérico en su lugar. En esta situación, no se especifica el valor mínimo ni el máximo de los datos. Por el contrario, solo se proporcionan los valores de inicio y finalización para cada icono que el indicador utiliza. Para obtener más información, consulte [conjunto y configurar unidades de medida &#40;generador de informes y SSRS&#41;](set-and-configure-measurement-units-report-builder-and-ssrs.md).  
  
 Los indicadores transmiten los valores de datos sincronizando los valores de datos del indicador que están en un ámbito especificado. De forma predeterminada, el ámbito es el contenedor primario del indicador, por ejemplo la tabla o matriz que contiene el indicador. Puede cambiar la sincronización del indicador eligiendo otro ámbito, por ejemplo un grupo, en función del diseño del informe. El indicador puede omitir la sincronización. Para obtener más información, vea [Establecer el ámbito de sincronización &#40;Generador de informes y SSRS&#41;](set-synchronization-scope-report-builder-and-ssrs.md).  
  
 Para obtener información general sobre la descripción y el ámbito de configuración de informes, vea [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Los indicadores solo usan un valor único. Si tiene que mostrar varios valores de datos, use un minigráfico o una barra de datos en lugar de un indicador. Los indicadores pueden representar varios valores de datos, pero son sencillos, fáciles de entender en tamaños pequeños y funcionan bien en tablas y matrices. Para obtener más información, vea [Sparklines and Data Bars &#40;Report Builder and SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
  
##  <a name="SizingIndicatators"></a> Ajustar el tamaño de los indicadores para maximizar su impacto visual  
 Además del color, dirección y forma, puede usar el tamaño para maximizar el impacto visual de los indicadores. Imagine un informe que utilice indicadores para mostrar la satisfacción del cliente con distintos tipos de bicicletas. El icono utilizado por el indicador se puede configurar para que tenga tamaños distintos en función de la satisfacción del cliente. Cuanto mayor sea el grado de satisfacción, más grande será el icono que se muestra en el informe. En la siguiente imagen se muestra un informe sobre ventas de bicicletas; los tamaños del icono reflejan la cantidad de las ventas.  
  
 Puede usar expresiones para establecer de manera dinámica el tamaño de las estrellas, en función de los valores del campo utilizado por el indicador. Para obtener más información, consulte [especificar el tamaño de un indicador al usar una expresión &#40;generador de informes y SSRS&#41;](specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs.md).  
  
 Para obtener más información sobre cómo escribir y usar expresiones, vea [Expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
  
##  <a name="IncludingIndicatorsInGauges"></a> Incluir indicadores y medidores en paneles de medidor  
 Los indicadores siempre se colocan dentro de un panel de medidor. El panel de medidor es un contenedor de nivel superior que puede incluir uno o varios medidores e indicadores de estado. El panel de medidor puede contener medidores o indicadores secundarios o adyacentes. Si usa un indicador como elemento secundario de un medidor, puede visualizar mejor los datos mostrando el estado del valor de los datos que se muestra en el medidor. Por ejemplo, un indicador dentro de un medidor puede mostrar un círculo verde para indicar que el valor al que señala el medidor señala está en el 33 por ciento superior del intervalo de valores. Con un medidor y un indicador en paralelo, puede representar los datos de distintas maneras. En cualquier caso, el indicador y el medidor pueden usar los mismos campos de datos o campos distintos.  
  
 En el siguiente diagrama se muestra un indicador en paralelo de un medidor y dentro de él.  
  
 ![rs_GaugePanelWithIndicatorAndGauge](../media/rs-gaugepanelwithindicatorandgauge.gif "rs_GaugePanelWithIndicatorAndGauge")  
  
 Para obtener más información, vea [Include Indicators and Gauges in a Gauge Panel &#40;Report Builder and SSRS&#41;](include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs.md).  
  
 Para obtener más información sobre el uso de medidores, vea [Gauges &#40;Report Builder and SSRS&#41;](gauges-report-builder-and-ssrs.md).  
  
  
##  <a name="SequenceIndicatorStates"></a> Secuencia de estados de indicador  
 La secuencia de estados de indicador en la pestaña de **Valor y estados** del cuadro de diálogo **Propiedades de indicador** afectan al icono indicador que se muestra para un valor de datos cuando se superponen los valores iniciales y finales de los estados de indicador.  
  
 Esto puede suceder si usa la unidad de medida de estado de porcentaje o numérica. Es más probable que se produzca cuando se usa la unidad de medida numérica porque se proporcionan valores específicos para esta medida. También es más probable que suceda cuando redondea valores de datos porque tiende a crear valores menos discretos.  
  
 Los escenarios siguientes describen cómo la visualización de los datos se ve afectada cuando se cambia la secuencia de los tres estados en el indicador de dirección **3 flechas (en color)** . De forma predeterminada, la secuencia es:  
  
1.  Flecha roja hacia abajo  
  
2.  Flecha amarilla horizontal  
  
3.  Flecha verde hacia arriba  
  
 En los escenarios siguientes se muestran cuatro secuencias de estado distintas y sus rangos de valores, además de mostrar las secuencias que afectan a la visualización de datos.  
  
 En estos casos, el indicador **3 flechas (en color)** usa medidas de estado numéricas.  
  
|Secuencia de estado|Valor inicial|Valor final|  
|--------------------|-----------------|---------------|  
|Rojo|0|3500|  
|Amarillo|3500|5000|  
|Verde|5000|10000|  
  
 La flecha roja hacia abajo representa el valor 3500 y la flecha amarilla horizontal, 5000.  
  
|Secuencia de estado|Valor inicial|Valor final|  
|--------------------|-----------------|---------------|  
|Verde|5000|10000|  
|Amarillo|3500|5000|  
|Rojo|0|3500|  
  
 La flecha amarilla horizontal representa el valor 3500 y la flecha green hacia arriba, 5000.  
  
|Secuencia de estado|Valor inicial|Valor final|  
|--------------------|-----------------|---------------|  
|Verde|5000|10000|  
|Rojo|0|3500|  
|Amarillo|3500|5000|  
  
 La flecha roja hacia abajo representa el valor 3500 y la flecha verde hacia arriba, 5000.  
  
|Secuencia de estado|Valor inicial|Valor final|  
|--------------------|-----------------|---------------|  
|Amarillo|3500|5000|  
|Rojo|0|3500|  
|Verde|5000|10000|  
  
 La flecha amarilla hacia abajo ahora representa tanto el valor 3500 como el 5000.  
  
 En resumen, se inicia la evaluación y el principio de la lista de estados de indicador, y el informe muestra el icono de indicador asociado al primer estado de indicador que tenga un rango de valores en el que encajen los datos. Por lo tanto, al cambiar la secuencia de estados de indicador se puede ver afectada la visualización de los valores de datos.  
  
  
##  <a name="HowTo"></a> Temas de procedimientos  
 En esta sección se enumeran procedimientos que muestran cómo agregar, cambiar y eliminar indicadores, cómo configurar y personalizar indicadores, y cómo usar indicadores en medidores.  
  
-   [Agregar o eliminar un indicador &#40;generador de informes y SSRS&#41;](add-or-delete-an-indicator-report-builder-and-ssrs.md)  
  
-   [Cambiar iconos de indicador y conjuntos de indicadores &#40;generador de informes y SSRS&#41;](change-indicator-icons-and-indicator-sets-report-builder-and-ssrs.md)  
  
-   [Establecer y configurar unidades de medida &#40;generador de informes y SSRS&#41;](set-and-configure-measurement-units-report-builder-and-ssrs.md)  
  
-   [Establecer el ámbito de sincronización &#40;generador de informes y SSRS&#41;](set-synchronization-scope-report-builder-and-ssrs.md)  
  
-   [Especifique el tamaño de un indicador utilizando una expresión &#40;generador de informes y SSRS&#41;](specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs.md)  
  
-   [Incluir indicadores y medidores en un Panel de medidores &#40;generador de informes y SSRS&#41;](include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs.md)  
  
  
## <a name="see-also"></a>Vea también  
 [Los medidores &#40;generador de informes y SSRS&#41;](gauges-report-builder-and-ssrs.md)   
 [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [Los gráficos &#40;generador de informes y SSRS&#41;](charts-report-builder-and-ssrs.md)  
  
  
