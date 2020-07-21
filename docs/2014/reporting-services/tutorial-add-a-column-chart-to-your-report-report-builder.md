---
title: 'Tutorial: Agregar un gráfico de columnas a un informe (Generador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 723e8fe5f657d3b9eda2d6ab73966830a13a3aac
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099125"
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>Tutorial: Agregar un gráfico de columnas a un informe (Generador de informes)
  Un gráfico de columnas muestra una serie como un conjunto de barras verticales agrupadas por categorías. Un gráfico de columnas puede ser útil para:  
  
-   Mostrar los cambios realizados en los datos a lo largo de un período de tiempo.  
  
-   Comparar el valor relativo de varias series.  
  
-   Mostrar una media móvil para mostrar tendencias.  
  
 En la ilustración siguiente se muestra el gráfico de columnas que creará, con una media móvil.  
  
 ![rs_TutorialColChartFinished](../../2014/tutorials/media/rs-tutorialcolchartfinished.gif "rs_TutorialColChartFinished")  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>Qué aprenderá  
 En este tutorial, aprenderá a realizar las siguientes tareas:  
  
1.  [Crear un gráfico a partir del Asistente para gráficos](#Chart)  
  
2.  [Elegir el tipo de gráfico](#ChartType)  
  
3.  [Dar formato al eje horizontal y etiquetarlo](#Horizontal)  
  
4.  [Mover la leyenda](#Legend)  
  
5.  [Titular el gráfico](#ChartTitle)  
  
6.  [Dar formato al eje vertical y etiquetarlo](#Vertical)  
  
7.  [Agregar una media móvil](#Average)  
  
8.  [Agregar un título de informe](#Title)  
  
9. [Guardar el informe](#Save)  
  
> [!NOTE]  
>  En este tutorial, los pasos del asistente se encuentran reunidos en un único procedimiento. Para obtener instrucciones paso a paso sobre cómo ir hasta un servidor de informes, elegir un origen de datos y crear un conjunto de datos, consulte el primer tutorial de esta serie: [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tiempo estimado para completar este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obtener información sobre los requisitos, vea [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="1-create-a-chart-report-from-the-chart-wizard"></a><a name="Chart"></a>1. crear un informe de gráfico a partir del Asistente para gráficos  
 En el cuadro de diálogo **Introducción** , use el Asistente para gráficos con el fin de crear un conjunto de datos incrustado, elegir un origen de datos compartido y crear un gráfico de columnas.  
  
> [!NOTE]  
>  En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
#### <a name="to-create-a-new-chart-report"></a>Para crear un informe de gráfico  
  
1.  Haga clic en **Inicio**, seleccione **Programas**, **Generador de informes de Microsoft SQL Server 2012**y, a continuación, haga clic en **Generador de informes**.  
  
     Aparece el cuadro de diálogo **Introducción** .  
  
    > [!NOTE]  
    >  Si el cuadro de diálogo **Introducción** no aparece, en el botón **generador de informes** , haga clic en **nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel derecho, haga clic en **Asistente para gráficos**.  
  
4.  En la **Página elegir un conjunto**de los, haga clic en **crear un conjunto**de los y, a continuación, en **siguiente**.  
  
5.  En la página **Elegir una conexión a un origen de datos** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos, y después haga clic en **Siguiente**. Puede que necesite escribir un nombre de usuario y contraseña.  
  
    > [!NOTE]  
    >  El origen de datos que elija no importa, con tal de que tenga los permisos adecuados. No está recibiendo datos del origen de datos. Para obtener más información, consulte [Maneras alternativas de obtener una conexión de datos &#40;Generador de informes&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
7.  Pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT CAST('2009-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2009-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2009-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2009-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2009-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2009-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2009-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2009-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2009-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2009-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2009-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2009-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2009-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2009-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2009-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2009-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (Opcional) Haga clic en el botón Ejecutar (**!**) para ver los datos en los que se basará su gráfico.  
  
9. Haga clic en **Next**.  
  
##  <a name="2-choose-the-chart-type"></a><a name="ChartType"></a>2. elegir el tipo de gráfico  
 Podrá elegir entre varios tipos de gráfico predefinidos.  
  
#### <a name="to-add-a-column-chart"></a>Para agregar un gráfico de columnas  
  
1.  En la página **Elegir un tipo de gráfico** , el gráfico de columnas es el tipo de gráfico predeterminado. Haga clic en **Siguiente**.  
  
2.  En la página **Organizar campos del gráfico** , arrastre el campo SalesDate hasta **Categorías**. Categorías se muestra en el eje horizontal.  
  
3.  Arrastre el campo Sales hasta **Valores**. El cuadro **Valores** muestra Sum(Sales), porque la suma del valor total de ventas se agrega para cada fecha. Valores se muestra en el eje vertical.  
  
4.  Haga clic en **Siguiente**.  
  
5.  En la página **elegir un estilo** , en el cuadro estilos, seleccione un estilo.  
  
     Un estilo especifica un estilo de fuente, un conjunto de colores y un estilo de borde. Al seleccionar un estilo, el panel Vista previa muestra un ejemplo del gráfico con ese estilo.  
  
6.  Haga clic en **Finalizar**  
  
     El gráfico se agrega a la superficie de diseño.  
  
7.  Haga clic en el gráfico para mostrar las asas del gráfico. Arrastre la esquina inferior derecha del gráfico para aumentar su tamaño. Observe que la superficie de diseño del informe aumenta de tamaño para adaptarse al tamaño del gráfico.  
  
8.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="3-format-and-label-the-horizontal-axis"></a><a name="Horizontal"></a>3. dar formato al eje horizontal y etiquetarlo  
 De forma predeterminada, el eje horizontal muestra los valores en un formato general que se escala automáticamente para ajustarse al tamaño del gráfico.  
  
#### <a name="to-format-a-date-on-the-horizontal-axis"></a>Para dar formato a una fecha en el eje horizontal  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic con el botón secundario en el eje horizontal y, a continuación, haga clic en **propiedades del eje horizontal**.  
  
3.  Haga clic en **Número**.  
  
4.  En **categoría**, seleccione **fecha**.  
  
5.  En el cuadro **Tipo** , seleccione **31 Ene 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  En la pestaña Inicio, haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
 La fecha se mostrará en el formato de fecha que haya seleccionado. Tenga en cuenta que el gráfico no etiqueta todas las categorías del eje horizontal. De forma predeterminada, solo se incluyen las etiquetas que caben a lo largo del eje.  
  
 Puede personalizar la presentación de las etiquetas girándolas y especificando el intervalo.  
  
#### <a name="to-rotate-the-axis-labels-and-change-the-display-interval-along-the-horizontal-axis"></a>Para girar las etiquetas del eje y cambiar el intervalo de presentación a lo largo del eje horizontal  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic con el botón secundario en el título del eje horizontal y, a continuación, haga clic en **Mostrar título del eje** para quitar el título. Dado que el eje horizontal muestra las fechas, no es necesario el título.  
  
3.  Haga clic con el botón secundario en el eje horizontal y, a continuación, haga clic en **propiedades del eje horizontal**.  
  
4.  En la página **Opciones del eje** , en **rango e**intervalo del eje, escriba **3** para **intervalo**. El gráfico mostrará una fecha de cada tres.  
  
5.  Haga clic en **Etiquetas**.  
  
6.  En **cambiar las opciones de ajuste automático de las etiquetas de eje**, seleccione **deshabilitar ajuste automático**.  
  
7.  En **Ángulo de giro de etiqueta**, seleccione **-90**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     El texto de ejemplo del eje horizontal girará 90 grados.  
  
9. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 En el gráfico, las etiquetas se giran y se muestra la etiqueta de cada tercera fecha.  
  
##  <a name="4-move-the-legend"></a><a name="Legend"></a>4. Mueva la leyenda  
 La leyenda se crea automáticamente a partir de los datos de las categorías y las series.  
  
#### <a name="to-move-the-legend-below-the-chart-area-of-a-column-chart"></a>Para mover la leyenda debajo del área de gráfico de un gráfico de columnas  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic con el botón secundario en la leyenda del gráfico y, a continuación, haga clic en propiedades de la **leyenda**.  
  
3.  En **diseño y posición**, seleccione una posición diferente. Por ejemplo, sitúe la leyenda centrada en la parte inferior.  
  
     Cuando la leyenda se coloca en la parte superior o inferior de un gráfico, su diseño cambia de vertical a horizontal. Puede seleccionar un diseño diferente en la lista desplegable **Diseño** .  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (Opcional) Dado que solo hay una categoría en este tutorial, no es necesaria la leyenda. Para quitar la leyenda, haga clic con el botón secundario en la leyenda y, a continuación, haga clic en **eliminar leyenda**.  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="5-title-the-chart"></a><a name="ChartTitle"></a>5. título del gráfico  
  
#### <a name="to-change-the-chart-title-above-the-chart-area"></a>Para cambiar el título del gráfico encima del área de gráfico  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Seleccione las palabras **título del gráfico** en la parte superior del gráfico y, a continuación, escriba el siguiente texto: **total de pedidos de venta de tiendas**.  
  
3.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="6-format-and-label-the-vertical-axis"></a><a name="Vertical"></a>6. dar formato al eje vertical y etiquetarlo  
 De forma predeterminada, el eje vertical muestra los valores en un formato general que se escala automáticamente para ajustarse al tamaño del gráfico.  
  
#### <a name="to-format-as-currency-the-numbers-on-the-vertical-axis"></a>Para dar formato de moneda a los números del eje vertical  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga doble clic en las etiquetas del eje vertical a lo largo del lateral del gráfico para seleccionarlas.  
  
3.  En la cinta de opciones, en la pestaña **Inicio** , en el grupo **número** , haga clic en el botón **moneda** . Las etiquetas del eje cambiarán para mostrar el formato de moneda.  
  
4.  En la cinta de opciones, en la pestaña **Inicio** , en el grupo **número** , haga clic dos veces en el botón **disminuir decimales** para mostrar el número redondeado al dólar más próximo.  
  
5.  Haga clic con el botón secundario en el eje vertical y haga clic en **propiedades del eje vertical**.  
  
6.  Haga clic en **Número**. Tenga en cuenta que **moneda** ya está seleccionado en el cuadro **categoría** y **posiciones decimales** ya es **0** (cero).  
  
7.  En el cuadro **Mostrar valores en** , haga clic en **miles**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Haga clic con el botón secundario en el título del eje vertical a lo largo del lateral del gráfico y haga clic en **propiedades del título del eje**.  
  
10. Reemplace el texto del campo **texto del título** con el siguiente texto: **total de ventas (en miles)**. También puede especificar una gran variedad de opciones de formato para el título.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="7-add-a-moving-average"></a><a name="Average"></a>7. agregar una media móvil  
  
#### <a name="to-add-a-moving-average"></a>Para agregar una media móvil  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga doble clic en el gráfico para mostrar el panel **Datos del gráfico** .  
  
3.  Haga clic con el botón secundario en el campo **[SUM (sales)]** que se encuentra en el área **valores** y, a continuación, haga clic en **Agregar serie calculada**.  
  
4.  En **Fórmula**, compruebe que esté seleccionada la opción **Media móvil** .  
  
5.  En **Establecer parámetros de fórmula**, para **Período**, seleccione **4**.  
  
6.  Haga clic en **borde**.  
  
7.  En **ancho de línea**, seleccione **3 PT**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 El gráfico muestra una línea que muestra la media móvil del total de ventas por fecha, promediado cada cuatro fechas.  
  
##  <a name="8-add-a-report-title"></a><a name="Title"></a>8. agregar un título de informe  
  
#### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
3.  Escriba **gráfico de ventas**, presione entrar y, a continuación, escriba **enero a diciembre de 2009**, de modo que tenga este aspecto:  
  
     **Gráfico de ventas**  
  
     **Enero a diciembre de 2009**  
  
4.  Seleccione **gráfico de ventas**y haga clic en el botón **negrita** en la sección **fuente** de la pestaña **Inicio** de la cinta de opciones.  
  
5.  Seleccione **enero a diciembre 2009**y, en la sección **fuente** de la pestaña **Inicio** , establezca el tamaño de fuente en **10**.  
  
6.  Opta Es posible que tenga que hacer que el cuadro de texto del **título** sea más alto para dar cabida a las dos líneas de texto al hacer clic en el centro del borde inferior.  
  
     Este título aparecerá en la parte superior del informe. Cuando no hay ningún encabezado de página definido, los elementos de la parte superior del cuerpo del informe son equivalentes a un encabezado de informe.  
  
7.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="9-save-the-report"></a><a name="Save"></a>9. guardar el informe  
  
#### <a name="to-save-the-report"></a>Para guardar el informe  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  En el botón Generador de informes , haga clic en **Guardar como**.  
  
3.  En **Nombre**, escriba **Gráfico de columnas de pedidos de ventas**.  
  
4.  Haga clic en **Guardar**.  
  
## <a name="next-steps"></a>Pasos a seguir  
 Ha completado correctamente el tutorial Agregar un gráfico de columnas al informe. Para obtener más información sobre los gráficos, vea [Gráficos &#40;Generador de informes y SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) y [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Tutoriales &#40;Generador de informes&#41;](report-builder-tutorials.md)   
 [Generador de informes en SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
