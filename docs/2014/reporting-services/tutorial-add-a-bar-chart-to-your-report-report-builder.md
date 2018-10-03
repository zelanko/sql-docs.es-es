---
title: 'Tutorial: Agregar un gráfico de barras a un informe (Generador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6956ebd6-0217-4087-a4fa-5cc1c3804691
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 25d3fafc654ab1c272d7688e49d67cd2af5d1820
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106805"
---
# <a name="tutorial-add-a-bar-chart-to-your-report-report-builder"></a>Tutorial: Agregar un gráfico de barras a un informe (Generador de informes)
  Un gráfico de barras muestra los datos de categoría horizontalmente. Esto puede ayudar a:  
  
-   Mejorar la legibilidad de los nombres de categoría largos.  
  
-   Mejorar la comprensión de las fechas u horas representadas mediante valores.  
  
-   Comparar el valor relativo de varias series.  
  
 La siguiente ilustración muestra el gráfico de barras que creará en orden alfabético, con ventas para 2008 y 2009, para los cinco vendedores superiores.  
  
 ![rs_BarChartTutorial](../../2014/tutorials/media/rs-barcharttutorial.gif "rs_BarChartTutorial")  
  
##  <a name="BackToTop"></a> Qué aprenderá  
 En este tutorial, aprenderá a realizar las siguientes tareas:  
  
1.  [Crear un gráfico desde el Asistente para gráficos](#Chart)  
  
2.  [Elija el tipo de gráfico](#ChartType)  
  
3.  [Mostrar todos los valores de categoría en el eje Vertical](#AllValues)  
  
4.  [Modificar la presentación de nombres en el eje Vertical](#Sort)  
  
5.  [Mover la leyenda](#Legend)  
  
6.  [Mover el título del gráfico](#ChartTitle)  
  
7.  [Dar formato el eje Horizontal y etiquetarlo](#Horizontal)  
  
8.  [Agregar un filtro para mostrar cinco valores superiores](#Filter)  
  
9. [Agregar un título de informe](#Title)  
  
10. [Guardar el informe](#Save)  
  
> [!NOTE]  
>  En este tutorial, los pasos del asistente se encuentran reunidos en un único procedimiento. Para obtener instrucciones paso a paso sobre cómo ir hasta un servidor de informes, crear un conjunto de datos y elegir un origen de datos, vea el primer tutorial de esta serie: [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tiempo estimado para completar este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obtener más información sobre los requisitos, consulte [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="Chart"></a> 1. Crear un informe de gráfico a partir del Asistente para gráficos  
 Desde el **Introducción** cuadro de diálogo, crear un conjunto de datos incrustado, elegir un origen de datos compartido y crear un gráfico de barras con el Asistente para gráficos.  
  
> [!NOTE]  
>  En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
#### <a name="to-create-a-new-chart-report"></a>Para crear un informe de gráfico  
  
1.  Haga clic en **Inicio**, seleccione **Programas**, **Generador de informes de Microsoft SQL Server 2012**y, a continuación, haga clic en **Generador de informes**.  
  
     Aparecerá el cuadro de diálogo **Introducción** .  
  
    > [!NOTE]  
    >  Si el **Introducción** cuadro de diálogo no aparece, haga clic en el botón Generador de informes y, a continuación, haga clic en **New**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel derecho, haga clic en **Asistente para gráficos**.  
  
4.  En la página **Elegir un conjunto de datos** , haga clic en **Crear un conjunto de datos**y, después, haga clic en **Siguiente**.  
  
5.  En la página **Elegir una conexión a un origen de datos** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos, y después haga clic en **Siguiente**. Puede que necesite escribir un nombre de usuario y contraseña.  
  
    > [!NOTE]  
    >  El origen de datos que elija no importa, con tal de que tenga los permisos adecuados. No está recibiendo datos del origen de datos. Para obtener más información, consulte [Maneras alternativas de obtener una conexión de datos &#40;Generador de informes&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
6.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
7.  Pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT 'Luis' as FirstName, 'Alverca' as LastName, CAST(170000.00 AS money) AS SalesYear2009, CAST(150000. AS money) AS SalesYear2008  
    UNION SELECT 'Jeffrey' as FirstName, 'Zeng' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(190000. AS money) AS SalesYear2008  
    UNION SELECT 'Houman' as FirstName, 'Pournasseh' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Robin' as FirstName, 'Wood' as LastName, CAST(75000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'Daniela' as FirstName, 'Guaita' as LastName,  CAST(170000. AS money) AS SalesYear2009, CAST(175000. AS money) AS SalesYear2008  
    UNION SELECT 'John' as FirstName, 'Yokim' as LastName, CAST(160000. AS money) AS SalesYear2009, CAST(195000. AS money) AS SalesYear2008  
    UNION SELECT 'Delphine' as FirstName, 'Ribaute' as LastName, CAST(180000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Robert' as FirstName, 'Hernady' as LastName, CAST(140000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Tanja' as FirstName, 'Plate' as LastName, CAST(150000. AS money) AS SalesYear2009, CAST(160000. AS money) AS SalesYear2008  
    UNION SELECT 'David' as FirstName, 'Bradley' as LastName, CAST(210000. AS money) AS SalesYear2009, CAST(180000. AS money) AS SalesYear2008  
    UNION SELECT 'Michal' as FirstName, 'Jaworski' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(220000. AS money) AS SalesYear2008  
    UNION SELECT 'Chris' as FirstName, 'Ashton' as LastName, CAST(195000. AS money) AS SalesYear2009, CAST(205000. AS money) AS SalesYear2008  
    UNION SELECT 'Pongsiri' as FirstName, 'Hirunyanitiwatna' as LastName, CAST(175000. AS money) AS SalesYear2009, CAST(215000. AS money) AS SalesYear2008  
    UNION SELECT 'Brian' as FirstName, 'Burke' as LastName, CAST(187000. AS money) AS SalesYear2009, CAST(207000. AS money) AS SalesYear2008  
    ```  
  
8.  (Opcional) Haga clic en el botón Ejecutar (**!**) para ver los datos en los que se basará su gráfico.  
  
9. Haga clic en **Siguiente**.  
  
##  <a name="ChartType"></a> 2. Elegir el tipo de gráfico  
 Podrá elegir entre varios tipos de gráfico predefinidos.  
  
#### <a name="to-add-a-column-chart"></a>Para agregar un gráfico de columnas  
  
1.  En la página **Elegir un tipo de gráfico** , el gráfico de columnas es el tipo de gráfico predeterminado.  
  
2.  Haga clic en **Barras**y después en **Siguiente**.  
  
     En el **organizar campos del gráfico** página, hay cuatro campos en el **campos disponibles** panel: FirstName, LastName, SalesYear2009 y SalesYear2008.  
  
3.  Arrastre LastName hasta el panel Categorías.  
  
4.  Arrastre SalesYear2009 hasta el panel Valores. SalesYear2009 representa la cantidad de ventas de cada vendedor durante el año 2009. El panel Valores muestra `[Sum(SalesYear2009)]` porque el gráfico muestra al agregado para cada producto.  
  
5.  Arrastre SalesYear2008 hacia el panel Valores bajo SalesYear2009. SalesYear2008 representa la cantidad de ventas de cada vendedor durante el año 2008.  
  
6.  Haga clic en **Siguiente**.  
  
7.  En el **elegir un estilo** página, en el panel Estilos, seleccione un estilo.  
  
     Un estilo especifica un estilo de fuente, un conjunto de colores y un estilo de borde. Al seleccionar un estilo, el panel Vista previa muestra un ejemplo del gráfico con ese estilo.  
  
8.  Haga clic en **Finalizar**.  
  
     El gráfico se agrega a la superficie de diseño.  
  
9. Haga clic en el gráfico para mostrar las asas del gráfico. Arrastre la esquina inferior derecha del gráfico para aumentar su tamaño.  
  
10. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 El informe muestra el gráfico de barras de ventas correspondiente a cada vendedor para los años 2008 y 2009. La longitud de la barra corresponde al total de ventas.  
  
##  <a name="AllValues"></a> 3. Modificar la presentación de nombres en el eje vertical  
 De forma predeterminada, solo aparecen algunos de los valores del eje vertical. Puede cambiar el gráfico para mostrar todas las categorías.  
  
#### <a name="to-display-all-sales-persons-along-the-category-axis-of-a-bar-chart"></a>Mostrar todos los vendedores en el eje de categorías de un gráfico de barras  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic en el eje vertical y, a continuación, haga clic en **propiedades del eje Vertical**.  
  
3.  En **Rango e intervalo del eje**, en el cuadro **Intervalo** , escriba **1**.  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Haga clic en la vertical **título del eje** y desactive el **Mostrar título del eje** casilla de verificación.  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
> [!NOTE]  
>  Si no se leen los nombres de vendedor en el eje vertical, puede hacer más alto el gráfico o cambiar las opciones de formato para las etiquetas del eje.  
  
###  <a name="CategoryExpression"></a> Mostrar Last Name y First Name en eje Vertical  
 Puede cambiar la expresión de categoría para incluir para cada vendedor el apellido seguido por el nombre.  
  
##### <a name="to-change-the-category-expression"></a>Para cambiar la expresión de categoría  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga doble clic en el gráfico para mostrar el panel **Datos del gráfico** .  
  
3.  En el área **Grupos de categorías** , haga clic con el botón secundario en [LastName] y, después, haga clic en **Propiedades del grupo de categorías**.  
  
4.  En Etiqueta, haga clic en el botón de expresión (Fx).  
  
5.  Escriba la siguiente expresión: `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
     Esta expresión concatena el apellido, una coma y el nombre.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
8.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 Si los nombres no aparecen al ejecutar el informe, puede actualizar los datos manualmente. Estando todavía en modo de vista previa, en la pestaña **Ejecutar** en el grupo **Navegación** , haga clic en **Actualizar**.  
  
> [!NOTE]  
>  Si no se leen los nombres de vendedor en el eje vertical, puede hacer más alto el gráfico o cambiar las opciones de formato para las etiquetas del eje.  
  
##  <a name="Sort"></a> 4. Cambiar el criterio de ordenación para los nombres en del eje vertical  
 Al ordenar los datos en un gráfico, está cambiando el orden de valores en el eje de categoría.  
  
#### <a name="to-sort-the-names-in-alphabetical-order-on-the-bar-chart"></a>Ordenar los nombres alfabéticamente en el gráfico de barras  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga doble clic en el gráfico para mostrar el panel **Datos del gráfico** .  
  
3.  En el área **Grupos de categorías** , haga clic con el botón secundario en [LastName] y, después, haga clic en **Propiedades del grupo de categorías**.  
  
4.  Haga clic en **Ordenar**. La página **Cambiar opciones de ordenación** muestra una lista de expresiones de ordenación. De forma predeterminada, esta lista tiene una expresión de ordenación que es igual que la expresión de grupo de categorías original.  
  
5.  En Ordenar por, haga clic en la expresión (**Fx**) botón.  
  
6.  Escriba la siguiente expresión: `=Fields!LastName.Value & ", " & Fields!FirstName.Value`  
  
7.  Haga clic en **Aceptar**.  
  
8.  En el **propiedades del grupo de categorías** página, en el **orden** lista desplegable, seleccione **Z a**. De este modo se selecciona el orden alfabético inverso para que los nombres aparezcan ordenados de arriba abajo.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 Los nombres en el eje horizontal están ordenados en orden inverso, con **Alerca** en la parte superior y **Zeng** en la parte inferior.  
  
##  <a name="Legend"></a> 5. Mover la leyenda  
 Para mejorar la legibilidad de los valores del gráfico, es posible que le interese mover la leyenda correspondiente. Por ejemplo, en un gráfico de barras, donde las barras se muestran horizontalmente, puede cambiar la posición de la leyenda para que aparezca debajo o encima del área de gráfico. Esto proporciona más espacio horizontal para las barras.  
  
#### <a name="to-display-the-legend-below-the-chart-area-of-a-bar-chart"></a>Para mostrar la leyenda debajo del área de gráfico de un gráfico de barras  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic con el botón secundario en la leyenda del gráfico.  
  
3.  Seleccione **Propiedades de la leyenda**.  
  
4.  Para **Posición de la leyenda**, seleccione una posición diferente. Por ejemplo, sitúe la leyenda centrada en la parte inferior.  
  
     Cuando la leyenda se coloca en la parte superior o inferior de un gráfico, su diseño cambia de vertical a horizontal. Puede seleccionar un diseño diferente en la lista desplegable **Diseño** .  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="ChartTitle"></a> 6. Titular el gráfico  
  
#### <a name="to-change-the-chart-title-above-the-chart-area-of-a-bar-chart"></a>Cambiar el título del gráfico situado por encima del área de gráfico de un gráfico de barras  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Seleccione las palabras **título del gráfico** en la parte superior del gráfico y, a continuación, escriba el siguiente texto: **ventas para 2008 y 2009**.  
  
3.  Haga clic en cualquier lugar fuera del texto.  
  
4.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="Horizontal"></a> 7. Dar formato al eje horizontal y etiquetarlo  
 De forma predeterminada, el eje horizontal muestra los valores en un formato general que se escala automáticamente para ajustarse al tamaño del gráfico.  
  
#### <a name="to-format-the-numbers-on-the-horizontal-axis"></a>Dar formato a los números en el eje horizontal  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga clic en el eje horizontal a lo largo de la parte inferior del gráfico para seleccionarlo.  
  
     En la cinta de opciones, en el **inicio** ficha la **número** grupo, haga clic en el **moneda** botón. Las etiquetas del eje horizontal cambian al formato de moneda.  
  
3.  (Opcional) Quite los dígitos decimales. Cerca del botón **Moneda** , haga clic dos veces en el botón **Disminuir decimales** .  
  
4.  Haga clic con el botón secundario en el eje horizontal y, después, haga clic en **Propiedades del eje horizontal**.  
  
5.  En el **número** ficha, seleccione **mostrar valores en miles.**  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Haga clic en **título del eje** y haga clic en **propiedades del título del eje**.  
  
8.  En el **texto de título** , escriba **ventas en miles** y haga clic en **Aceptar**.  
  
9. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 El informe muestra el importe de ventas en el eje horizontal como moneda en miles y no tiene ningún dígito decimal.  
  
##  <a name="Filter"></a> 8. Agregar un filtro para mostrar cinco valores superiores  
 Puede agregar un filtro al gráfico para especificar qué datos del conjunto de datos se van a incluir o excluir del gráfico.  
  
#### <a name="to-add-a-filter-and-display-the-top-five-values"></a>Agregar un filtro para mostrar los cinco valores superiores  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  Haga doble clic en el gráfico para mostrar el panel **Datos del gráfico** .  
  
3.  En el área **Grupos de categorías** , haga clic con el botón secundario en el campo [LastName] y, después, haga clic en **Propiedades del grupo de categorías**.  
  
4.  Haga clic en **Filtros**. La página **Cambiar filtros** puede mostrar una lista de expresiones de filtro. Esta lista aparece vacía de forma predeterminada.  
  
5.  Haga clic en **Agregar**. Aparece un nuevo filtro en blanco.  
  
6.  En **expresión**, tipo **[SUM (salesyear2009)]**. Esto crea la expresión subyacente `=Sum(Fields!SalesYear2009.Value)`, que puede ver si hace clic en el **fx** botón.  
  
7.  Compruebe que el tipo de datos es **Texto**.  
  
8.  En **Operador**, seleccione **Superior N** en la lista desplegable.  
  
9. En **Valor**, escriba la siguiente expresión: **=5**  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
11. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 Si no se filtran los resultados al ejecutar el informe, puede actualizar los datos manualmente. En la pestaña **Ejecutar** , en el grupo **Navegación** , haga clic en **Actualizar**.  
  
 El gráfico muestra los nombres de los cinco vendedores superiores del conjunto de datos de ventas de 2009.  
  
##  <a name="Title"></a> 9. Agregar un título de informe  
  
#### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Tipo **gráfico de barras de ventas**, presione ENTRAR y, a continuación, escriba **cinco vendedores superiores para 2009**, por lo que este aspecto:  
  
     **Gráfico de barras de ventas**  
  
     **Cinco vendedores superiores de 2009**  
  
3.  Seleccione **Gráfico de barras de ventas**y haga clic en el botón **Negrita** .  
  
4.  Seleccione **cinco vendedores superiores para 2009**y en el **fuente** sección en la **inicio** pestaña, establezca el tamaño de fuente en **10**.  
  
5.  (Opcional) Es posible que necesite hacer más alto el cuadro de texto Título para que quepan las dos líneas de texto.  
  
     Este título aparecerá en la parte superior del informe. Cuando no hay ningún encabezado de página definido, los elementos de la parte superior del cuerpo del informe son equivalentes a un encabezado de informe.  
  
6.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="Save"></a> 10. Guardar el informe  
  
#### <a name="to-save-the-report"></a>Para guardar el informe  
  
1.  Cambie a la vista de diseño del informe.  
  
2.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
3.  En **Nombre**, escriba **Gráfico de barras de ventas**.  
  
4.  Haga clic en **Guardar**.  
  
 El informe se guardará en el servidor de informes.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Ha completado correctamente el tutorial Agregar un gráfico de barras al informe. Para obtener más información sobre los gráficos, vea [Gráficos &#40;Generador de informes y SSRS&#41;](report-design/charts-report-builder-and-ssrs.md) y [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales &#40;generador de informes&#41;](report-builder-tutorials.md)   
 [Generador de informes en SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
