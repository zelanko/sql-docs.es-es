---
title: Agregar visualizaciones a informes móviles de Reporting Services | Microsoft Docs
description: 'Obtenga información sobre los tres tipos de gráficos básicos que puede usar en informes para dispositivos móviles de Reporting Services: hora, categoría y totales, y sus correspondientes gráficos de comparación.'
ms.date: 09/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 3b220b74-9ecd-4084-93fb-545208d5d7a2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ed45f77f509d3206340a2f52e6d3b31ac6824d87
ms.sourcegitcommit: ea0bf89617e11afe85ad85309e0ec731ed265583
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/28/2020
ms.locfileid: "92907193"
---
# <a name="add-visualizations-to-reporting-services-mobile-reports"></a>Agregar visualizaciones a informes móviles de Reporting Services
Los gráficos son una parte esencial de la visualización de datos. Obtenga más información sobre los gráficos que puede utilizar en los informes móviles de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] para cubrir una variedad de escenarios. 

[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-long.md)] tiene tres tipos de gráficos básicos: tiempo, categoría y totales. Estos tres tipos de gráfico tienen datos de comparación correspondientes, que son útiles para comparar dos conjuntos de series distintos.  

## <a name="shared-chart-properties"></a>Propiedades de gráficos compartidos

Algunas propiedades se aplican en todos los gráficos, mientras que otras solo se aplican en gráficos específicos. Estas son algunas de las propiedades compartidas.

### <a name="number-format"></a>Formato de número
Puede asignar diferentes formatos a números de un gráfico en [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] (por ejemplo, general, moneda con o sin decimales, porcentajes con y sin decimales, etc.). En un gráfico, el formato de número se aplica en las anotaciones del eje, así como en los mensajes emergentes de punto de datos. Se establece el formato de número en cada gráfico de forma individual, no en el informe móvil en conjunto. 

* Para establecer el formato de número, seleccione la pestaña **Diseño** , seleccione un gráfico en la superficie de diseño y, en el panel **Propiedades de los elementos visuales** , seleccione un **Formato de número**. 
  
### <a name="legend"></a>Leyenda
* Para mostrar la leyenda de un gráfico, seleccione la pestaña **Diseño** , seleccione un gráfico en la superficie de diseño y, en el panel **Propiedades de los elemenens visuales** , establezca **Mostrar leyenda** en **Activado**.
  
### <a name="series"></a>Serie
Cada métrica individual o valor mostrados en un gráfico se conoce como una serie; varias series pueden compartir (y, de hecho, comparten) tanto un eje X común como un eje Y común. Las series se definen en el panel de propiedades de datos de la vista de datos seleccionando uno o varios campos y tablas de datos. Cada campo dará como resultado una serie individual de puntos de datos en la visualización del gráfico con su propio color.  

### <a name="change-aggregation"></a>Cambiar agregación 
Para campos numéricos en gráficos, la agregación predeterminada es sumar. Puede cambiarla a media, recuento, mínimo, máximo, primero, último.

* Haga clic en la pestaña **Datos** y, en **Propiedades de los datos** , seleccione **Opciones** junto al campo numérico y, después, seleccione otra agregación.

### <a name="set-or-clear-filters"></a>Establecer o borrar filtros

Si agrega un navegador para filtrar el informe móvil, puede decidir los gráficos que quiere filtrar.

1. Seleccione la pestaña **Datos** y, en **Propiedades de los datos** , elija **Opciones**.

2. En **Filtrado por** , verá navegadores que puede seleccionar o desactivar.

Para más información, vea [Agregar navegadores para filtrar un informe móvil](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md).
   
## <a name="time-charts"></a>Gráficos de tiempo  
  
El gráfico de tiempo es el gráfico más básico en [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]. El eje de hora (y fecha) del gráfico se establecerá automáticamente en el primer campo de fecha y hora válido de la tabla de datos.  

![Captura de pantalla del gráfico de tiempo de un informe móvil.](../../reporting-services/mobile-reports/media/mobile-report-time-chart.png)

1. Arrastre un **Gráfico de tiempo** desde la pestaña **Diseño** a la superficie de diseño y cambie su tamaño.

2. De forma predeterminada, es un gráfico de barras apiladas. Puede cambiar esto en **Visualización de serie**.

3. Si el gráfico necesita datos que aún no están en el informe, haga clic en la pestaña **Datos** > **Agregar datos** para [obtener datos de Excel o de un conjunto de datos compartido](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

3. En el panel **Propiedades de los datos** , **Serie principal** es **SimulatedTable**. Seleccione la flecha en el cuadro y seleccione la tabla.

5. Si establece **Estructura de datos** en **Por columnas** (en la pestaña **Diseño** > panel **Propiedades de los elementos visuales** ), en el panel **Propiedades de los datos** puede seleccionar varias columnas o valores numéricos.

   Si establece **Estructura de datos** en **Por filas** (en el panel **Propiedades de los datos** ), puede seleccionar un **Campo de nombre de serie** y una columna de valores numéricos.
   
Para más información, vea [Agrupar datos por columnas o filas](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md).
  
## <a name="category-charts"></a>Gráficos de categoría  
  
Al contrario que en un gráfico de tiempo, en un gráfico de categoría se agrupa en un campo distinto de un campo de hora y fecha en el eje X. Esta agrupación, denominada *coordinada de categoría* , tiene que estar en un campo de cadena, no en un campo numérico.

![Captura de pantalla del gráfico de categoría de un informe móvil.](../../reporting-services/mobile-reports/media/mobile-report-category-chart.png)   

1. Arrastre un **Gráfico de categoría** desde la pestaña **Diseño** hasta la superficie de diseño, cambie su tamaño y, si es necesario, [obtenga datos de este](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

2. Seleccione la pestaña **Datos** y, en el panel **Propiedades de los datos** , en **Coordinada de categoría** , seleccione una tabla y un campo por el que agrupar. Este campo estará en el eje X del gráfico resultante.

3. En **Serie principal** , seleccione la tabla y los campos numéricos que se agregarán para cada categoría. 
  
## <a name="totals-charts"></a>Gráfico de valores totales  

![Captura de pantalla del gráfico de valores totales de un informe móvil.](../../reporting-services/mobile-reports/media/mobile-report-totals-chart.png)
  
El gráfico de totales cumple dos objetivos distintos: 
* Presenta varias series (solo la suma o el total de la serie principal definida). 
* Ofrece la opción de agrupar datos por columnas y filas. Agrupar por columnas puede resultar útil al trabajar con datos planos. Al agrupar por columnas, solo está disponible la propiedad de la serie principal, ya que la columna de categoría se determina automáticamente según el número de campos seleccionados para la propiedad de la serie principal.  

Para más información, vea [Agrupar datos por columnas o filas](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md). 
  
## <a name="comparison-charts"></a>Gráficos de comparación  
  
Los gráficos de tiempo, categoría y totales también están disponibles como *gráficos de comparación*. En un diagrama de comparación, puede especificar no solo una serie principal, sino también una segunda serie de comparación. Las series principales de comparación se pueden mostrar de tres formas distintas.

![Captura de pantalla del gráfico de tiempo de comparación de un informe móvil.](../../reporting-services/mobile-reports/media/mobile-report-comparison-time-chart.png)

1. Arrastre uno de los **Gráficos de comparación** (tiempo, categoría o totales) desde la pestaña **Diseño** a la superficie de diseño, cambie su tamaño y, si es necesario, [obtenga datos de este](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

2. En el panel **Propiedades de los elementos visuales** , en **Visualización de serie** , seleccione una de las opciones siguientes: 
   * Barra o barra delgada
   * Línea o barra
   * Barra o área de pasos 

En gráficos de comparación, puede elegir tener los mismos colores de gráfico en los valores principales y de comparación de una serie.

* En el panel **Propiedades de los elementos visuales** , establezca la opción **Volver a usar los colores en las series de comparación** en **Activado**.

   Si se establece en **Activado** , la paleta de colores se reiniciará entre dibujar la serie principal y la de comparación para que coincidan los valores relacionados de la serie principal y la de comparación. 

   Si se establece en **Desactivado** , la paleta de colores continuará su giro normal al dibujar la serie principal después de la serie de comparación, evitando una coordinación de color posiblemente errónea entre los dos conjuntos de series.  
  
## <a name="pie-and-funnel-charts"></a>Gráficos circulares y gráficos de embudo  
  
Los gráficos circulares y de embudo se encuentran entre los más sencillos para las visualizaciones. Puede estructurar los datos por filas o columnas. 
* Los **gráficos circulares** en informes móviles de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] pueden ser circulares, de anillos o de anillos con un total en el centro. Los gráficos circulares son adecuados para mostrar el tamaño relativo de las diferentes partes de un total. Si hay demasiados segmentos, puede resultar difícil verlos.
* Los **gráficos de embudo** suelen usarse para mostrar las fases de un proceso, como ventas.

![Captura de pantalla del gráfico de embudo de un informe móvil.](../../reporting-services/mobile-reports/media/mobile-report-funnel-chart.png)

### <a name="structure-pie-and-funnel-chart-data-by-rows-or-by-columns"></a>Datos de gráfico circular de estructura y gráfico de embudo por filas o por columnas
1. Arrastre un **gráfico circular** o un **gráfico de embudo** desde la pestaña **Diseño** hasta la superficie de diseño, cambie su tamaño y, si es necesario, [obtenga datos de este](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).
2. En el panel **Propiedades de los elementos visuales** , en **Estructura de datos** , seleccione una de estas opciones:
   * **Por columnas**
   * **Por filas**
3. Si ha seleccionado **Por columnas** , seleccione la pestaña **Datos** y, en el panel **Propiedades de los datos** , en **Serie principal** , seleccione la tabla y todos los campos que quiera agregar en el gráfico circular o en el gráfico de embudo. Los nombres de campos se usarán para etiquetar cada una de las áreas del gráfico resultante.

   Si ha seleccionado **Por filas** , seleccione la pestaña **Datos** y, en el panel **Propiedades de los datos** , en **Columna de categoría** , seleccione la tabla y la columna con los valores que quiera usar para agrupar y asignar etiquetas en el gráfico circular. En Columna de serie principal, seleccione un campo numérico para los valores del gráfico.

Para más información, vea [Agrupar datos por columnas o filas](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md). 

## <a name="treemaps"></a>Gráficos de rectángulos  
  
Los gráficos de rectángulos muestran métricas al aplicar sus valores en el tamaño y color de los iconos en una cuadrícula rectangular. 

![Captura de pantalla del gráfico de rectángulos de un informe móvil.](../../reporting-services/mobile-reports/media/mobile-report-group-treemap.png)

1. Arrastre un **gráfico de rectángulos** desde la pestaña **Diseño** hasta la superficie de diseño, cambie su tamaño y, si es necesario, [obtenga datos de este](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).
2.  Seleccione la pestaña **Datos** y, en el panel **Propiedades de los datos** : 

     * En **El tamaño representa** , seleccione un campo numérico del tamaño de los iconos.
     * En **El color representa** , seleccione un campo numérico para el color de los iconos. 
     * (opcional) **Valor de centro personalizado** solo puede usar **Valor de centro personalizado** cuando el tipo de visualización es HeatMapWithCustomCenterValue.
     
         El valor central decide el color de un cuadro. Cuánto mejor es la métrica en comparación con el valor central, más verde es. Cuánto peor es la métrica, más rojo es.
     
     * [opcional] Para mostrar un mensaje emergente cuando los visores seleccionen un icono de la cuadrícula, en **Etiquetas emergentes** , seleccione uno o varios campos. En los mensajes emergentes del gráfico de rectángulos se pueden mostrar campos de texto de campos numéricos.  

De forma predeterminada, los gráficos de rectángulos son jerárquicos, agrupan los iconos primero por categoría y, después, por tamaño y color.
* En la pestaña **Datos** , en **Agrupar por** , seleccione una tabla y un campo.

Puede desactivar la agrupación para que los iconos se organicen solo por tamaño y color. 

* Seleccione la pestaña **Diseño** y establezca la opción **Gráfico de rectángulos de dos niveles** en **Desactivado**.   

## <a name="waterfall-charts"></a>Gráficos de cascada

Un gráfico de cascada muestra un total acumulado conforme se agregan o se restan valores. Es útil para comprender cómo resulta afectado un valor inicial (por ejemplo, los ingresos netos) por una serie de cambios positivos y negativos.

Las columnas están codificadas con color verde para los casos de aumento y con rojo para la disminución, por lo que puede ver rápidamente a qué corresponde cada valor. Las columnas de valor inicial y final a menudo empiezan por cero, mientras que los valores intermedios son columnas flotantes. Debido a este aspecto, los gráficos de cascada se conocen también como gráficos de puente.

### <a name="when-to-use-a-waterfall-chart"></a>Cuándo usar un gráfico de cascada

Los gráficos de cascada son una buena opción en estos casos:
* Cuando tenga cambios para la medida a lo largo de una serie temporal o diferentes categorías para auditar los cambios más importantes que contribuyen al valor total.
* Para trazar el beneficio anual de su compañía, mostrando varias fuentes de ingresos y llegar a la ganancia (o pérdida) total.
* Para ilustrar el principio y final del número de empleados de su empresa en un año.
* Para visualizar los ingresos y los gastos de cada mes y el saldo acumulado de su cuenta. 

### <a name="create-a-waterfall-chart"></a>Crear un gráfico de cascada

1. Arrastre un **Gráfico de cascada** desde la pestaña **Diseño** hasta la superficie de diseño, cambie su tamaño y, si es necesario, [obtenga datos de este](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

    ![Captura de pantalla del icono del gráfico de cascada de un informe móvil.](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart-icon.png)
    
2.  Seleccione la pestaña **Datos** y, en el panel **Propiedades de datos** , seleccione un campo de categoría en los datos para **Category Coordinate** (Coordenada de categoría) y un campo numérico para **Serie principal** : 

    ![Captura de pantalla de los datos en cascada de un informe móvil.](../../reporting-services/mobile-reports/media/mobile-report-waterfall-data.png)
    
3. Seleccione la pestaña **Diseño** para ver el gráfico de cascada en la vista previa.

   ![Captura de pantalla del gráfico de cascada de un informe móvil.](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart.png)
   
   Los meses con pérdidas, como febrero, junio y julio, se muestran en rojo. 
   Los meses con ganancias, como septiembre, octubre y noviembre, se muestran en verde. 

## <a name="see-also"></a>Consulte también 
* [Mapas de informes móviles de Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Navegadores en informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Agregar cuadrículas de datos a informes móviles | Reporting Services](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)
* [Medidores en informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
  

