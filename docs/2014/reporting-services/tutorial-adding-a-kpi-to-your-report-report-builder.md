---
title: 'Tutorial: Agregar un KPI a un informe (Generador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a1b158b6fc504a0917e0c268846da93be3aa59b9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098974"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>Tutorial: Agregar un KPI a un informe (Generador de informes y SSRS)
  Un indicador clave de rendimiento (KPI) es un valor medible que tiene importancia para la empresa. Este tutorial lo enseñará a incluir un KPI en un informe. En este escenario, el resumen de ventas por subcategorías de producto es el KPI. El estado actual del KPI se muestra mediante colores, medidores e indicadores.  
  
 En la siguiente ilustración se muestra el informe que creará.  
  
 ![rs_AddKPITutorial](../../2014/tutorials/media/rs-addkpitutorial.gif "rs_AddKPITutorial")  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>Qué aprenderá  
 En este tutorial, aprenderá agregar un KPI estableciendo el color de fondo de las celdas de la tabla en función del valor de celda, así como a agregar y configurar un medidor y un indicador. También aprenderá a escribir la expresión que establece el color de fondo de las celdas de la tabla.  
  
 Este tutorial contiene los siguientes procedimientos:  
  
1.  [Crear un informe de tabla y un conjunto de datos con el asistente para tablas o matrices](#Table)  
  
2.  [Organizar datos, elegir el diseño y el estilo con el asistente para tablas o matrices](#CompleteWizard)  
  
3.  [Utilizar los colores de fondo para mostrar un KPI](#BackgroundColors)  
  
4.  [Mostrar un KPI usando un medidor](#Gauge)  
  
5.  [Mostrar un KPI usando un indicador](#Indicator)  
  
6.  [Agregar un título de informe](#Title)  
  
7.  [Guardar el informe](#Save)  
  
> [!NOTE]  
>  En este tutorial, los pasos del asistente se fusionan en dos procedimientos: uno para crear el conjunto de datos y otro para crear una tabla. Para obtener instrucciones paso a paso sobre cómo ir hasta un servidor de informes, elegir un origen de datos, crear un conjunto de datos y ejecutar el asistente, vea el primer tutorial de esta serie: [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
 Tiempo estimado para completar este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obtener más información sobre los requisitos, consulte [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="1-create-a-table-report-and-dataset-from-the-table-or-matrix-wizard"></a><a name="Table"></a>1. crear un informe de tabla y un conjunto de informes desde el Asistente para tablas o matrices  
 En el cuadro de diálogo **Introducción** , elija un origen de datos compartido, cree un conjunto de datos incrustado y muestre los datos en una tabla.  
  
> [!NOTE]  
>  En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
#### <a name="to-create-a-new-table"></a>Para crear una tabla  
  
1.  Haga clic en **Inicio**, seleccione **Programas**, **Generador de informes de Microsoft SQL Server 2012**y, a continuación, haga clic en **Generador de informes**.  
  
     Aparece el cuadro de diálogo **Introducción** .  
  
    > [!NOTE]  
    >  Si el cuadro de diálogo **Introducción** no aparece, en el botón generador de informes, haga clic en **nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel de la derecha, haga clic en **Asistente para tabla o matriz**.  
  
4.  En la página Elegir un conjunto de datos , haga clic en **Crear un conjunto de datos**.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página **elegir una conexión a un origen de datos** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos. Si no está disponible ningún origen de datos o no tiene acceso a un servidor de informes, puede utilizar un origen del datos incrustados en su lugar. Para más información, vea [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
9. Copie y pegue la siguiente consulta en el panel de consulta:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2009-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2009-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2009-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2009-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2009-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. Haga clic en **Siguiente**.  
  
##  <a name="2-organize-data-choose-layout-and-style-from-the-table-or-matrix-wizard"></a><a name="CompleteWizard"></a>2. organizar datos, elegir el diseño y el estilo desde el Asistente para tablas o matrices  
 Utilice el asistente para proporcionar un diseño inicial en el que mostrar los datos. El panel de vista previa del asistente le ayudará a visualizar el resultado de las agrupaciones de datos antes de completar la tabla o el diseño de la matriz.  
  
#### <a name="to-organize-data-into-groups-choose-a-layout-and-a-style"></a>Para organizar los datos en grupos, elija un diseño y un estilo  
  
1.  En la página Organizar campos, arrastre Product hasta **Valores**.  
  
2.  Arrastre Quantity hasta **Valores** y colóquelo debajo de Product.  
  
     El campo Quantity se resume con la función Sum, que es la función predeterminada para resumir campos numéricos.  
  
3.  Arrastre Sales hasta **Valores** y colóquelo debajo de Quantity.  
  
     Los pasos 1, 2 y 3 especifican los datos que deben mostrarse en la tabla.  
  
4.  Arrastre SalesDate hasta **Grupos de filas**.  
  
5.  Arrastre Subcategory hasta **Grupos de filas** y colóquelo debajo de SalesDate.  
  
     Los pasos 4 y 5 organizan los valores de los campos por fecha primeramente y, después, por todas las ventas de esa fecha.  
  
6.  Haga clic en **Siguiente**.  
  
     Al ejecutar el informe, la tabla muestra cada fecha, todos los pedidos de cada fecha, y todos los productos, cantidades y totales de ventas de cada pedido.  
  
7.  En la página elegir el diseño, en **Opciones**, compruebe que esté seleccionada la opción **Mostrar subtotales y totales generales** .  
  
8.  Compruebe que esté seleccionada la opción **Bloqueado, subtotal abajo** .  
  
9. Desactive la opción **Expandir o contraer grupos**.  
  
     En este tutorial, el informe creado no usa la característica de obtención de detalles que permite a un usuario expandir una jerarquía de grupos primarios para mostrar filas de grupos secundarios y filas de detalles.  
  
10. Haga clic en **Siguiente**.  
  
11. En la página Elegir un estilo, en el panel Estilos, seleccione un estilo.  
  
     En la ilustración del informe completado se muestra el informe con el estilo Ocean.  
  
12. Haga clic en **Finalizar**  
  
     La tabla se agrega a la superficie de diseño. La tabla tiene cinco columnas y cinco filas. El panel Grupos de filas muestra tres grupos de filas: SalesDate, Subcategory y Details. Los datos detallados son todos los datos recuperados por la consulta del conjunto de datos.  
  
13. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 Para cada producto vendido en una fecha concreta, la tabla muestra el nombre del producto, la cantidad vendida y el total de ventas. Los datos se organizan primero por fecha de ventas y, a continuación, por subcategoría.  
  
##  <a name="3-use-background-colors-to-display-a-kpi"></a><a name="BackgroundColors"></a>3. usar colores de fondo para mostrar un KPI  
 Los colores de fondo se pueden establecer en una expresión que se evalúe al ejecutar el informe.  
  
#### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>Para mostrar el estado actual de un KPI mediante colores de fondo  
  
1.  En la tabla, haga clic con el botón secundario en dos `[Sum(Sales)]` celdas hacia abajo en la celda (la fila de subtotal que muestra las ventas de una subcategoría) y, a continuación, haga clic en **propiedades de cuadro de texto**.  
  
2.  En **relleno**, haga clic en el botón **FX** situado junto a la opción **color de relleno** y escriba la siguiente expresión en el campo **establecer expresión para: BackgroundColor** :  
  
 `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
 Esto cambia a verde el color del fondo, utilizando la tonalidad de verde denominada "Lima", para cada celda que contiene una suma agregada para `[Sum(Sales)]` igual o superior a 5000. Los valores de `[Sum(Sales)]` entre 2500 y 5000 están coloreados en amarillo. Los valores inferiores a 2500 están coloreados en rojo.  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 En la fila de subtotal que muestra las ventas de una subcategoría, el color de fondo de la celda será rojo, amarillo o verde en función del valor de la suma de ventas.  
  
##  <a name="4-display-a-kpi-by-using-a-gauge"></a><a name="Gauge"></a>4. mostrar un KPI usando un medidor  
 Un medidor muestra un valor único de un conjunto de datos. En este tutorial se utiliza un medidor lineal horizontal porque su forma y simplicidad hacen que resulte fácil leerlo, incluso cuando tiene un tamaño pequeño y se usa dentro de la celda de una tabla. Para obtener más información, vea [Medidores &#40;Generador de informes y SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md).  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>Para mostrar el estado actual de un KPI usando un medidor  
  
1.  Cambie a la vista de diseño.  
  
2.  En la tabla, haga clic con el botón secundario en el controlador de columna de la celda que ha cambiado en el procedimiento anterior, elija **Insertar columna**y, a continuación, haga clic en **derecha**. Se agregará una nueva columna a la tabla.  
  
3.  Escriba **KPI** en el encabezado de columna.  
  
4.  En la pestaña **Insertar** , en el grupo **regiones de datos** , haga clic en **medidor**y, a continuación, haga clic en la superficie de diseño fuera de la tabla. Aparece el cuadro de diálogo **Seleccionar tipo de medidor** .  
  
5.  Haga clic en **lineal**. Se selecciona el primer tipo de medidor lineal, **horizontal**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Se agregará un medidor a la superficie de diseño.  
  
7.  En el panel Datos de informe, arrastre el campo Sales hasta el medidor. Al arrastrar Sales al medidor, se abrirá el panel de datos del medidor.  
  
8.  Coloque las ventas en la lista **valores** .  
  
     Al arrastrar el campo al medidor, el campo se agrega usando la función integrada Sum.  
  
9. Haga clic con el botón derecho en el puntero en el medidor y haga clic en **propiedades del puntero**.  
  
10. En **tipo de puntero**, seleccione **barra**. Esto cambia el puntero de un marcador a una barra que estará más visible cuando el medidor se agregue a la tabla.  
  
11. Haga clic en el **relleno del puntero**. En **color secundario,** elija **amarillo**. El modelo de relleno de degradado cambiará de blanco a amarillo.  
  
12. Haga clic con el botón derecho en la escala del medidor y haga clic en **Propiedades de escala**.  
  
13. Establezca la opción **máximo** en 25000.  
  
    > [!NOTE]  
    >  En lugar de una constante como 25 000, puede usar una expresión para calcular dinámicamente el valor de la opción **Máximo** . La expresión usaría el agregado de la característica de agregados y es similar a la expresión `=Max(Sum(Fields!Sales.value), "Tablix1")`.  
  
14. Arrastre el medidor dentro de la tabla a la tercera celda en la fila de subtotal que muestra las ventas para una subcategoría de la columna que insertó.  
  
    > [!NOTE]  
    >  Puede que tenga que cambiar el tamaño de la columna para que el medidor lineal horizontal quepa en la celda. Para cambiar el tamaño de la columna, haga clic en el encabezado de columna y use los controladores de tamaño para cambiar el tamaño de las celdas horizontal y verticalmente.  
  
15. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
     La longitud horizontal de la barra en el medidor cambia en función del valor del KPI.  
  
16. (Opcional) Agregue un tope máximo para controlar el desbordamiento, de modo que cualquier valor que supere el máximo de la escala siempre señale al tope máximo:  
  
    1.  Abra el panel de propiedades.  
  
    2.  Haga clic en la escala. Las propiedades de la escala lineal se muestran en el panel de propiedades.  
  
    3.  En la categoría **PIN de escala** , expanda el nodo **MaximumPin** .  
  
    4.  Establezca la propiedad **Habilitar** en `True`. Aparece un tope después del valor máximo en la escala.  
  
    5.  Establezca **BorderColor** en `Lime`.  
  
17. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="5-display-a-kpi-by-using-an-indicator"></a><a name="Indicator"></a>5. mostrar un KPI usando un indicador  
 Los indicadores son medidores pequeños y simples que comunican los valores de datos de un vistazo. Debido a su tamaño y simplicidad, los indicadores se utilizan a menudo en tablas y matrices. Para más información, vea [Indicadores &#40;Generador de informes y SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md).  
  
#### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>Para mostrar el estado actual de un KPI usando un indicador  
  
1.  Cambie a la vista de diseño.  
  
2.  En la tabla, haga clic con el botón secundario en el controlador de columna de la celda que ha cambiado en el procedimiento anterior, elija **Insertar columna**y, a continuación, haga clic en **derecha**. Se agregará una nueva columna a la tabla.  
  
3.  Escriba **KPI** en el encabezado de columna.  
  
4.  Haga clic en la celda del subtotal de la subcategoría.  
  
5.  En la pestaña **Insertar** , en el grupo **regiones de datos** , haga doble clic en **indicador.**  
  
     Se abrirá el cuadro de diálogo **Seleccionar tipo de indicador** .  
  
6.  Haga clic en **formas**. Se selecciona el primer tipo de forma, 3 semáforos (sin marco **)** .  
  
     Utilice este indicador en el tutorial.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     El indicador se agregará a la superficie de diseño.  
  
8.  Haga clic con el botón derecho en el indicador y, después, haga clic en **Propiedades de indicador**.  
  
9. Haga clic en **valores y Estados**.  
  
10. En la lista desplegable valor, seleccione **[SUM (sales)]**, pero no cambie ninguna otra opción.  
  
     De manera predeterminada, la sincronización de datos se produce en la región de datos y podrá ver el valor **Tablix1**, el nombre de la región de datos de la tabla del informe, en el cuadro **Ámbito de sincronización** .  
  
     En este informe, podrá cambiar también el ámbito de un indicador colocado en la celda del subtotal de la subcategoría para realizar la sincronización en el campo SalesDate.  
  
11. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="6-add-a-report-title"></a><a name="Title"></a>6. agregar un título de informe  
 Los títulos de informe aparecen en la parte superior. Puede situar el título del informe en un encabezado de informe o, si el informe no lo utiliza, en un cuadro de texto en la parte superior del cuerpo del informe. Deberá utilizar el cuadro de texto que se coloca automáticamente en la parte superior del cuerpo del informe.  
  
 El texto se puede mejorar aún más aplicando estilos de fuente, tamaños y colores diferentes a las frases y caracteres individuales. Para obtener más información, vea [Dar formato al texto en un cuadro de texto &#40;Generador de informes y SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
#### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba **KPI de ventas del producto**y, a continuación, haga clic fuera del cuadro de texto.  
  
3.  Opcionalmente, haga clic con el botón secundario en el cuadro de texto que contiene **KPI de ventas de productos**, haga clic en propiedades de cuadro de **texto**y, a continuación, en la pestaña fuente, seleccione los diferentes estilos de fuente, tamaños y colores.  
  
4.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
##  <a name="7-save-the-report"></a><a name="Save"></a>7. guardar el informe  
 Guarde el informe un servidor de informes o en su equipo. Si no guarda el informe en el servidor de informes, varias características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como los elementos de informe y los subinformes, no estarán disponibles.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Para guardar el informe en un servidor de informes  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Sitios y servidores recientes**.  
  
3.  Seleccione o escriba el nombre del servidor de informes donde tiene el permiso para guardar los informes.  
  
     Aparecerá el mensaje "Conectando con el servidor de informes". Una vez completada la conexión, se mostrará el contenido de la carpeta de informes que el administrador del servidor de informes especificó como ubicación predeterminada para los informes.  
  
4.  En **Nombre**, reemplace el nombre predeterminado por **KPI de ventas del producto**.  
  
5.  Haga clic en **Guardar**.  
  
 El informe se guarda en el servidor de informes. El nombre del servidor de informes al que está conectado aparecerá en la barra de estado en la parte inferior de la ventana.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Para guardar el informe en el equipo  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Escritorio**, **Mis documentos**o **Mi PC**y vaya a la carpeta donde quiere guardar el informe.  
  
> [!NOTE]  
>  Si no tiene acceso a un servidor de informes, haga clic en **Escritorio**, **Mis documentos**o **Mi PC** y guarde el informe en su equipo.  
  
1.  En **Nombre**, reemplace el nombre predeterminado por **KPI de ventas del producto**.  
  
2.  Haga clic en **Guardar**.  
  
## <a name="next-steps"></a>Pasos a seguir  
 Ha completado correctamente el tutorial Agregar un KPI a un informe. Para obtener más información, consulte indicadores de medidores (Generador de informes) [&#40;generador de informes y SSRS&#41;](report-design/indicators-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Tutoriales &#40;Generador de informes&#41;](report-builder-tutorials.md)   
 [Generador de informes en SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
