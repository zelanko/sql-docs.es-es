---
title: 'Tutorial: Agregar un gráfico circular a un informe (generador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: eaadf7bf-c312-428a-b214-0a1fbf959c3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 30966fc1ccc592539e543869aef03f555ca59b2d
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020106"
---
# <a name="tutorial-add-a-pie-chart-to-your-report-report-builder"></a>Tutorial: Agregar un gráfico circular a un informe (generador de informes)
  Los gráficos circulares y los gráficos de anillos muestran los datos como una proporción del total. Los gráficos circulares se usan normalmente para realizar comparaciones entre grupos. Los gráficos circulares y de anillos, junto con los gráficos de pirámide y embudo, forman un grupo de gráficos conocidos como gráficos de formas. Los gráficos de formas no tienen ejes. Cuando se coloca un campo numérico en un gráfico de formas, el gráfico calcula el porcentaje de cada valor en relación con el total.  
  
 Si hay demasiados puntos de datos en un gráfico circular, es posible que las etiquetas de los puntos de datos estén demasiado amontonadas y no puedan leerse. En ese caso, considere la posibilidad de usar un gráfico de líneas. Considere usar únicamente gráficos circulares después de haber agregado los datos en algunos puntos de datos.  
  
 La siguiente ilustración muestra el gráfico circular que creará.  
  
 ![rs_TutorialPieChartConcave](../../2014/tutorials/media/rs-tutorialpiechartconcave.gif "rs_TutorialPieChartConcave")  
  
##  <a name="BackToTop"></a> Qué aprenderá  
 En este tutorial, aprenderá a:  
  
1.  [Crear un gráfico circular desde el Asistente para gráficos](#Chart)  
  
2.  [Elija el tipo de gráfico](#ChartType)  
  
3.  [Mostrar porcentajes en cada sector](#Percentages)  
  
4.  [Unir los sectores pequeños en un solo sector](#CombineSlices)  
  
5.  [Personalizar el efecto de dibujo](#DrawingEffect)  
  
6.  [Agregar un título de informe](#Title)  
  
7.  [Guardar el informe](#Save)  
  
> [!NOTE]  
>  En este tutorial, los pasos del asistente se encuentran reunidos en dos procedimientos. Para obtener instrucciones paso a paso sobre cómo ir hasta un servidor de informes, agregar un origen de datos y agregar un conjunto de datos, vea el primer tutorial de esta serie: [Tutorial: Creación de un informe de tabla básico &#40;generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tiempo estimado para completar este tutorial: 10 minutos  
  
## <a name="requirements"></a>Requisitos  
 Para obtener más información sobre los requisitos, consulte [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Chart"></a> 1. Crear un gráfico circular a partir del Asistente para gráficos  
 En el cuadro de diálogo Introducción, use el Asistente para gráficos con el fin de crear un conjunto de datos incrustado, elegir un origen de datos compartido y crear un gráfico circular.  
  
> [!NOTE]  
>  En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
#### <a name="to-create-a-new-chart-report"></a>Para crear un informe de gráfico  
  
1.  Haga clic en **Inicio**, seleccione **Programas**, **Generador de informes de Microsoft SQL Server 2012**y, a continuación, haga clic en **Generador de informes**.  
  
     Aparecerá el cuadro de diálogo Introducción.  
  
    > [!NOTE]  
    >  Si el cuadro de diálogo Introducción no aparece, en el botón Generador de informes, haga clic en **Nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel derecho, haga clic en **Asistente para gráficos**.  
  
4.  En la página **Elegir un conjunto de datos** , haga clic en **Crear un conjunto de datos**y, después, haga clic en **Siguiente**.  
  
5.  En la página **Elegir una conexión a un origen de datos** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos, y después haga clic en **Siguiente**. Puede que necesite escribir un nombre de usuario y contraseña.  
  
    > [!NOTE]  
    >  El origen de datos que elija no importa, con tal de que tenga los permisos adecuados. No está recibiendo datos del origen de datos. Para obtener más información, consulte [Maneras alternativas de obtener una conexión de datos &#40;Generador de informes&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
7.  Pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT 'Advanced Digital Camera' AS Product, CAST(254995.21 AS money) AS Sales  
    UNION SELECT 'Slim Digital Camera' AS Product, CAST(164499.04 AS money) AS Sales  
    UNION SELECT 'SLR Digital Camera' AS Product, CAST(782176.79 AS money) AS Sales  
    UNION SELECT 'Lens Adapter' AS Product, CAST(36333.08 AS money) AS Sales  
    UNION SELECT 'Macro Zoom Lens' AS Product, CAST(40199.3 AS money) AS Sales  
    UNION SELECT 'USB Cable' AS Product, CAST(53245.5 AS money) AS Sales  
    UNION SELECT 'Independent Filmmaker Camcorder' AS Product, CAST(452288.0 AS money) AS Sales  
    UNION SELECT 'Full Frame Digital Camera' AS Product, CAST(247250.85 AS money) AS Sales  
    ```  
  
8.  (Opcional) Haga clic en el botón Ejecutar (**!**) para ver los datos en los que se basará su gráfico.  
  
9. Haga clic en **Siguiente**.  
  
##  <a name="ChartType"></a> 2. Elegir el tipo de gráfico  
 Podrá elegir entre varios tipos de gráfico predefinidos.  
  
#### <a name="to-add-a-pie-chart"></a>Para agregar un gráfico circular  
  
1.  En el **elegir un tipo de gráfico** página, haga clic en **circular**y, a continuación, haga clic en **siguiente**. Se abrirá la página **Organizar campos del gráfico** .  
  
     En la página **Organizar campos del gráfico** , arrastre el campo Product hasta el panel **Categorías** . Las categorías definen el número de segmentos del gráfico circular. En este ejemplo, habrá ocho segmentos, uno para cada producto.  
  
2.  Arrastre el campo Sales hasta el panel **Valores** . Sales representa la cantidad de ventas para la subcategoría. El panel **Valores** muestra `[Sum(Sales)]` porque el gráfico muestra al agregado para cada producto.  
  
3.  Haga clic en **Siguiente**.  
  
4.  En el **elegir un estilo** página, en el panel Estilos, seleccione un estilo.  
  
     Un estilo especifica un estilo de fuente, un conjunto de colores y un estilo de borde. Al seleccionar un estilo, el panel Vista previa muestra un ejemplo del gráfico con ese estilo.  
  
5.  Haga clic en **Finalizar**.  
  
     El gráfico se agrega a la superficie de diseño.  
  
6.  Haga clic en el gráfico para mostrar las asas del gráfico. Arrastre la esquina inferior derecha del gráfico para aumentar su tamaño. Observe que la superficie de diseño del informe aumenta de tamaño para adaptarse al tamaño del gráfico.  
  
7.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 El informe muestra el gráfico circular con ocho segmentos, uno para cada producto. El tamaño de cada segmento representa las ventas de ese producto. Tres de los sectores son bastante finos.  
  
##  <a name="Percentages"></a> 3. Mostrar porcentajes en cada sector  
 En cada sector del gráfico circular, puede mostrar un porcentaje de este sector respecto al círculo entero.  
  
#### <a name="to-display-percentages-in-each-slice-of-the-pie-chart"></a>Para mostrar porcentajes en cada sector del gráfico circular  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic con el botón derecho en el gráfico circular y haga clic en **Mostrar etiquetas de datos**. Las etiquetas de datos aparecen en el gráfico.  
  
3.  Haga clic en una etiqueta y, a continuación, haga clic en **propiedades de la etiqueta de serie**.  
  
4.  En los datos de etiqueta, en el cuadro de lista desplegable, seleccione **#PERCENT**.  
  
     Para mostrar los valores como porcentajes, la propiedad UseValueAsLabel debe ser falsa. Si se le pide que establezca este valor en el cuadro de diálogo **Confirmar acción** , haga clic en **Sí**.  
  
5.  (Opcional) Para especificar el número de posiciones decimales muestra la etiqueta, escriba `#PERCENT{Pn}` donde *n* es el número de posiciones decimales que se muestran. Por ejemplo, para no mostrar ninguna posición decimal, escriba `#PERCENT{P0}`.  
  
    > [!NOTE]  
    >  La opción**Formato de número** del cuadro de diálogo **Propiedades de la etiqueta de la serie** no tiene ningún efecto al dar formato a los porcentajes. Esto aplica formato de porcentaje a las etiquetas, pero no calcula el porcentaje del gráfico circular que cada sector representa.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 El informe muestra el porcentaje de la totalidad para cada sector del gráfico circular.  
  
##  <a name="CombineSlices"></a> 4. Unir los sectores pequeños en un solo sector  
 Tres de los sectores del gráfico son bastante pequeños. Puede unir varios sectores pequeños en un sector mayor que represente a todos ellos.  
  
#### <a name="to-combine-any-slices-on-the-pie-chart-smaller-than-5-percent-into-one-slice"></a>Para unir los sectores del gráfico circular menores del 5 por ciento en un solo sector  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  En el **vista** ficha la **mostrar u ocultar** grupo, seleccione **propiedades**.  
  
3.  En la superficie de diseño, haga clic en cualquier sector del gráfico circular. Las propiedades de la serie se muestran en el panel de propiedades.  
  
4.  En la sección **General** , expanda el nodo **CustomAttributes** .  
  
5.  Establezca la propiedad **CollectedStyle** en **SingleSlice**.  
  
6.  Compruebe que la propiedad **CollectedThreshold** esté establecida en 5.  
  
7.  Compruebe que la propiedad **CollectedThresholdUsePercent** esté establecida en **True**.  
  
8.  En la cinta de opciones, en el **inicio** , haga clic **ejecutar** para obtener una vista previa del informe.  
  
 En la leyenda, ahora existe la categoría "Other". El nuevo sector del gráfico circular combina todos los sectores que estaban por debajo del 5% en un sector que es el 6% de todo el gráfico circular.  
  
##  <a name="DrawingEffect"></a> 5. Personalizar el efecto de dibujo  
 En el Asistente para gráficos, el estilo predeterminado para un gráfico circular es Océano, que tiene un efecto de dibujo Cóncavo. Puede cambiarlo después de ejecutar el asistente.  
  
#### <a name="to-add-a-drawing-effect-to-the-pie-chart"></a>Para agregar un efecto de dibujo al gráfico circular  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Si el panel de propiedades no está ya abierto, en el **vista** ficha, seleccione **propiedades**.  
  
3.  Haga doble clic en el propio gráfico circular. Las propiedades de la serie para el gráfico circular se muestran en el panel de propiedades.  
  
4.  En el panel de propiedades, expanda el nodo **CustomAttributes** .  
  
5.  Establecer el **PieDrawingStyle** a **SoftEdge**.  
  
    > [!NOTE]  
    >  Los efectos de dibujo y los efectos tridimensionales son opciones exclusivas. Si un gráfico tiene aplicados efectos tridimensionales, **PieDrawingStyle** no está disponible en el panel de propiedades.  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 La siguiente ilustración muestra el gráfico circular con efecto de borde suave.  
  
 ![rs_TutorialPieChartSoftEdge](../../2014/tutorials/media/rs-tutorialpiechartsoftedge.gif "rs_TutorialPieChartSoftEdge")  
  
##  <a name="Title"></a> 6. Agregar un título de informe  
  
#### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba **Ventas de cámaras y cámaras de vídeo**, pulse ENTRAR y, después, escriba **Como porcentaje de ventas totales**, de modo que tenga este aspecto:  
  
     **Ventas de cámaras y cámaras de vídeo**  
  
     **Como porcentaje de ventas totales**  
  
3.  Seleccione **ventas de cámaras y cámaras de vídeo**y haga clic en el **negrita** botón desde la **fuente** sección de la **inicio** pestaña de la cinta de opciones.  
  
4.  Seleccione **como porcentaje de ventas totales**y en el **fuente** sección en la **inicio** pestaña, establezca el tamaño de fuente en **10**.  
  
5.  (Opcional) Es posible que necesite hacer más alto el cuadro de texto Título para que quepan las dos líneas de texto.  
  
     Este título aparecerá en la parte superior del informe. Cuando no hay ningún encabezado de página definido, los elementos de la parte superior del cuerpo del informe son equivalentes a un encabezado de informe.  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="Save"></a> 7. Guardar el informe  
  
#### <a name="to-save-the-report"></a>Para guardar el informe  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  En el botón Generador de informes, haga clic en **Guardar como**.  
  
3.  En **Nombre**, escriba **Gráfico circular de ventas**.  
  
4.  Haga clic en **Guardar**.  
  
 El informe se guardará en el servidor de informes.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha completado correctamente el tutorial Agregar un gráfico circular al informe. Para obtener más información sobre los gráficos, vea [Gráficos &#40;Generador de informes y SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) y [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales &#40;generador de informes&#41;](report-builder-tutorials.md)   
 [Generador de informes en SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
