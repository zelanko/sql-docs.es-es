---
title: 'Tutorial: Agregar un gráfico de columnas a un informe (Generador de informes) | Microsoft Docs'
ms.date: 09/02/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 63480059-b7b9-44b5-9d7f-91780db708b6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 55a74bcd165fd06d55eccd6afa718ccd775c7faf
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/30/2018
ms.locfileid: "52711491"
---
# <a name="tutorial-add-a-column-chart-to-your-report-report-builder"></a>Tutorial: Agregar un gráfico de columnas a un informe (Generador de informes)
En este tutorial, creará un informe paginado de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] con un gráfico de columnas que muestra una serie como un conjunto de barras verticales agrupadas por categoría. 

Los gráficos de columna son útiles para:  
  
-   Mostrar los cambios realizados en los datos a lo largo de un período de tiempo.  
-   Comparar el valor relativo de varias series.  
-   Mostrar una media móvil para mostrar tendencias.  
  
En la ilustración siguiente se muestra el gráfico de columnas que creará, con una media móvil.  
  
![report-builder-column-chart-tutorial](../reporting-services/media/report-builder-column-chart-tutorial.png)    
> [!NOTE]  
> En este tutorial, los pasos del asistente se encuentran reunidos en un único procedimiento. Para obtener instrucciones paso a paso sobre cómo ir hasta un servidor de informes, elegir un origen de datos y crear un conjunto de datos, consulte el primer tutorial de esta serie: [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tiempo estimado para completar este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obtener información sobre los requisitos, vea [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Chart"></a>1. Crear un informe de gráfico a partir del Asistente para gráficos  
En esta sección, usará el Asistente para gráficos con el fin de crear un conjunto de datos incrustado, elegir un origen de datos compartido y crear un gráfico de columnas.  
  
> [!NOTE]  
> En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
### <a name="to-create-a-chart-report"></a>Para crear un informe de gráfico  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el equipo, el portal web de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o el modo integrado de SharePoint.  
  
    Se abre el cuadro de diálogo **Nuevo informe o conjunto de datos** .  
  
    Si no ve el cuadro de diálogo **Nuevo informe o conjunto de datos**, vaya al menú **Archivo** > **Nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel derecho, haga clic en **Asistente para gráficos**.  
  
4.  En la **página Elegir un conjunto de datos**, haga clic en **Crear un conjunto de datos**y,después, haga clic en **Siguiente**.  
  
5.  En la página **Elegir una conexión a un origen de datos** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos, y después haga clic en **Siguiente**. Puede que necesite escribir un nombre de usuario y contraseña.  
  
    > [!NOTE]  
    > El origen de datos que elija no importa, con tal de que tenga los permisos adecuados. No está recibiendo datos del origen de datos. Para obtener más información, consulte [Maneras alternativas de obtener una conexión de datos &#40;Generador de informes&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
7.  Pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT CAST('2015-01-01' AS date) AS SalesDate, CAST(54995.21 AS money) AS Sales  
    UNION SELECT CAST('2015-01-05' AS date) AS SalesDate, CAST(64499.04 AS money) AS Sales  
    UNION SELECT CAST('2015-02-11' AS date) AS SalesDate, CAST(37821.79 AS money) AS Sales  
    UNION SELECT CAST('2015-03-18' AS date) AS SalesDate, CAST(53633.08 AS money) AS Sales  
    UNION SELECT CAST('2015-04-23' AS date) AS SalesDate, CAST(24019.3 AS money) AS Sales  
    UNION SELECT CAST('2015-05-01' AS date) AS SalesDate, CAST(93245.5 AS money) AS Sales  
    UNION SELECT CAST('2015-06-06' AS date) AS SalesDate, CAST(55288.0 AS money) AS Sales  
    UNION SELECT CAST('2015-06-16' AS date) AS SalesDate, CAST(68733.5 AS money) AS Sales  
    UNION SELECT CAST('2015-07-16' AS date) AS SalesDate, CAST(24750.85 AS money) AS Sales  
    UNION SELECT CAST('2015-08-23' AS date) AS SalesDate, CAST(43452.3 AS money) AS Sales  
    UNION SELECT CAST('2015-09-24' AS date) AS SalesDate, CAST(58656. AS money) AS Sales  
    UNION SELECT CAST('2015-10-15' AS date) AS SalesDate, CAST(44583. AS money) AS Sales  
    UNION SELECT CAST('2015-11-21' AS date) AS SalesDate, CAST(81568. AS money) AS Sales  
    UNION SELECT CAST('2015-12-15' AS date) AS SalesDate, CAST(45973. AS money) AS Sales  
    UNION SELECT CAST('2015-12-26' AS date) AS SalesDate, CAST(96357. AS money) AS Sales  
    UNION SELECT CAST('2015-12-31' AS date) AS SalesDate, CAST(81946. AS money) AS Sales  
    ```  
  
8.  (Opcional) Haga clic en el botón Ejecutar (**!**) para ver los datos en los que se basará su gráfico.  
  
9. Haga clic en **Siguiente**.  
  
## <a name="ChartType"></a>2. Elegir el tipo de gráfico  
Puede elegir entre varios tipos de gráfico predefinidos y luego modificar el gráfico después de completar el asistente.  
  
### <a name="to-add-a-column-chart"></a>Para agregar un gráfico de columnas  
  
1.  En la página **Elegir un tipo de gráfico** , el gráfico de columnas es el tipo de gráfico predeterminado. Haga clic en **Siguiente**.  
  
2.  En la página **Organizar campos del gráfico** , arrastre el campo SalesDate hasta **Categorías**. Categorías se muestra en el eje horizontal.  
  
3.  Arrastre el campo Sales hasta **Valores**. El cuadro **Valores** muestra Sum(Sales), porque la suma del valor total de ventas se agrega para cada fecha. Valores se muestra en el eje vertical.  
  
4.  Haga clic en **Siguiente**.  
 
6.  Haga clic en **Finalizar**.  
  
    El gráfico se agrega a la superficie de diseño. Tenga en cuenta que el nuevo gráfico de columnas solo muestra los datos de representación. La leyenda dice Fecha de ventas A, Fecha de ventas B, etc., solo para dar una idea del aspecto que tendrá el informe. 
    
    ![generador-informes-gráfico-columnas-vista-diseño-1](../reporting-services/media/report-builder-column-chart-1-design-view.png)
  
7.  Haga clic en el gráfico para mostrar las asas del gráfico. Arrastre la esquina inferior derecha del gráfico para aumentar su tamaño. Observe que la superficie de diseño del informe aumenta de tamaño para adaptarse al tamaño del gráfico.  
  
8.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  

    ![generador-informes-gráfico-columnas-vista-previa-1](../reporting-services/media/report-builder-column-chart-1-preview.png)

Tenga en cuenta que el gráfico no etiqueta todas las categorías del eje horizontal. De forma predeterminada, solo se incluyen las etiquetas que caben a lo largo del eje. 
  
## <a name="Horizontal"></a>3. Dar formato a una fecha en el eje horizontal  
De forma predeterminada, el eje horizontal muestra los valores en un formato general que se escala automáticamente para ajustarse al tamaño del gráfico.  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic con el botón derecho en el eje horizontal > **Propiedades del eje horizontal**.  
  
3.  En la pestaña **Número** , en **Categoría**, seleccione **fecha**.  
  
5.  En el cuadro **Tipo** , seleccione **31 Ene 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  En la pestaña Inicio, haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
La fecha se mostrará en el formato de fecha que haya seleccionado. El gráfico todavía no etiqueta todas las categorías del eje horizontal. 

![generador-informes-gráfico-columnas-vista-previa-2](../reporting-services/media/report-builder-column-chart-2-preview.png)
  
Puede personalizar la presentación de las etiquetas girándolas y especificando el intervalo.  
  
## <a name="4-rotate-the-axis-labels-on-the-horizontal-axis"></a>4. Girar las etiquetas del eje en el eje horizontal  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic con el botón derecho en el título del eje horizontal y, después, haga clic en **Mostrar título del eje** para quitar el título. Dado que el eje horizontal muestra las fechas, no es necesario el título.  
  
3.  Haga clic con el botón derecho en el eje horizontal > **Propiedades del eje horizontal**.  
  
5.  En la pestaña **Etiquetas** , bajo **Cambiar opciones de ajuste automát. de etiquetas de eje**, seleccione **Deshabilitar el ajuste automático**.  
  
7.  En **Ángulo de giro de etiqueta**, seleccione **-90**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    El texto de ejemplo del eje horizontal girará 90 grados.  
    
    ![generador-informes-gráfico-columnas-girar-eje-x](../reporting-services/media/report-builder-column-chart-rotate-x-axis.png)
  
9. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
En el gráfico, las etiquetas se giran.  

![generador-informes-gráfico-columnas-girar-eje-x-vista-previa](../reporting-services/media/report-builder-column-chart-rotate-x-axis-preview.png)
  
## <a name="Legend"></a>5. Mover la leyenda  
La leyenda se crea automáticamente a partir de los datos de las categorías y las series. Puede mover la leyenda debajo del área de gráfico de un gráfico de columnas.  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic con el botón derecho en la leyenda del gráfico > **Propiedades de la leyenda**.  
  
3.  En **Diseño y posición**, seleccione una posición diferente. Por ejemplo, seleccione la opción centrada en la parte inferior.  
  
    Cuando la leyenda se coloca en la parte superior o inferior de un gráfico, su diseño cambia de vertical a horizontal. Puede seleccionar un diseño diferente en el cuadro **Diseño** .  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  (Opcional) Como en este tutorial solo hay una categoría, el gráfico no necesita una leyenda. Para quitarla, haga clic con el botón derecho en la leyenda > **Eliminar leyenda**.  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
## <a name="ChartTitle"></a>6. Titular el gráfico  
    
1.  Cambie a la vista de diseño del informe.  
  
2.  Seleccione las palabras **Título del gráfico** en la parte superior del gráfico y, después, escriba **Total de pedidos de venta en tiendas**.  
  
3.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
## <a name="Vertical"></a>7. Dar formato al eje vertical y etiquetarlo  
De forma predeterminada, el eje vertical muestra los valores en un formato general que se escala automáticamente para ajustarse al tamaño del gráfico.   
  
1.  Cambie a la vista de diseño del informe.  
  
2. Haga clic en las etiquetas del eje vertical a lo largo del lateral izquierdo del gráfico para seleccionarlas.  
  
3.  En la pestaña **Inicio** > grupo **Número**, haga clic en el botón **Moneda**. Las etiquetas del eje cambiarán para mostrar el formato de moneda.  
  
4.  Haga clic dos veces en el botón **Disminuir decimales** para mostrar el número redondeado al dólar más próximo.  
  
5.  Haga clic con el botón derecho en el eje vertical > **Propiedades del eje vertical**.  
  
6.  En la pestaña **Número** , observe que **Moneda** ya está seleccionado en el cuadro **Categoría** y **Posiciones decimales** ya tiene el valor **0** (cero).  
  
7.  Active **Mostrar valores en**. **Miles** ya está seleccionado.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Haga clic con el botón derecho en el eje vertical > **Mostrar título del eje**. 

10. Haga clic con el botón derecho en el título del eje vertical > **Propiedades del título del eje**.  
  
10. Reemplace el texto del campo **Texto del título** con **Total de ventas (en miles)**. También puede especificar una gran variedad de opciones de formato para el título.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Haga clic en **Ejecutar** para obtener la vista previa del informe.  

    ![generador-informes-gráfico-columnas-formato-eje-x](../reporting-services/media/report-builder-column-chart-format-y-axis.png)
    
## <a name="8-show-all-the-labels-on-the-horizontal-x-axis"></a>8. Mostrar todas las etiquetas del eje horizontal (x)

Observe que solo se muestran algunas de las etiquetas del eje x. En esta sección, se establece una propiedad en el panel Propiedades para mostrarlas todas.

1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic en el gráfico y, después, seleccione las etiquetas del eje horizontal.

3. En el panel Propiedades, establezca LabelInterval en 1.

    ![generador-informes-gráfico-columnas-establecer-intervalo-etiquetas](../reporting-services/media/report-builder-column-chart-set-label-interval.png)

    El gráfico tiene el mismo aspecto en la vista Diseño. 
    
5.  Haga clic en **Ejecutar** para obtener la vista previa del informe.

    ![report-builder-column-chart-label-interval-one-preview](../reporting-services/media/report-builder-column-chart-label-interval-one-preview.png)
    
    Ahora el gráfico muestra todas sus etiquetas.
  
## <a name="Average"></a>9. Agregar una media móvil con una serie calculada  

Una media móvil es una media de los datos de la serie, calculada en el tiempo. La media móvil puede identificar tendencias.
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga doble clic en el gráfico para mostrar el panel **Datos del gráfico** .  
  
3.  Haga clic con el botón derecho en el campo **[Sum(Sales)]** en el área **Valores** y, después, haga clic en **Agregar serie calculada**.  

     ![generador-informes-gráfico-columnas-agregar-serie-calculada](../reporting-services/media/report-builder-column-chart-add-calculated-series.png)
  
4.  En **Fórmula**, compruebe que esté seleccionada la opción **Media móvil** .  
  
5.  En **Establecer parámetros de fórmula**, para **Período**, seleccione **4**.  
  
6.  En la pestaña **Borde** , en **Ancho de línea**, seleccione **3pt**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
El gráfico muestra una línea que muestra la media móvil del total de ventas por fecha, promediado cada cuatro fechas. Obtenga más información sobre [Agregar una media móvil a un gráfico](../reporting-services/report-design/add-a-moving-average-to-a-chart-report-builder-and-ssrs.md). 

![generador-informes-gráfico-columnas-media-móvil](../reporting-services/media/report-builder-column-chart-moving-average.png)
  
## <a name="Title"></a>10. Agregar un título de informe  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
3.  Escriba **Gráfico de ventas**, pulse ENTRAR y, después, escriba **Enero a diciembre de 2015**, para que tenga este aspecto:  
  
    **Gráfico de ventas**  
  
    **Enero a diciembre de 2015**  
  
4.  Seleccione **Gráfico de ventas** y, en la pestaña **Inicio** sección > **Fuente** > **Negrita**.  
  
5.  Seleccione **Enero a diciembre de 2015** y, en la pestaña **Inicio** > sección **Fuente** > establezca el tamaño de fuente en **10**.  
  
6.  (Opcional) Es posible que necesite hacer más alto el cuadro de texto **Título** para que quepan las dos líneas de texto. Despliegue las flechas de dos puntas al hacer clic en el centro del borde inferior. Es posible que necesite arrastrar la parte superior del gráfico para que no se superponga el título.  
  
    Este título aparece en la parte superior del informe. Cuando no hay ningún encabezado de página definido, los elementos de la parte superior del cuerpo del informe son equivalentes a un encabezado de informe.  
  
7.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
## <a name="Save"></a>11. Guardar el informe  
  
### <a name="to-save-the-report"></a>Para guardar el informe  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  En el botón Generador de informes, haga clic en **Guardar como**.  

    Puede guardarlo en el equipo o en el servidor de informes.
  
3.  En **Nombre**, escriba **Gráfico de columnas de pedidos de ventas**.  
  
4.  Haga clic en **Guardar**.  
  
## <a name="next-steps"></a>Next Steps  
Ha completado correctamente el tutorial Agregar un gráfico de columnas al informe. Para obtener más información sobre los gráficos, vea [Gráficos &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/charts-report-builder-and-ssrs.md) y [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Ver también  
-    [Tutoriales del Generador de informes](../reporting-services/report-builder-tutorials.md) 
-    [Generador de informes en SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

