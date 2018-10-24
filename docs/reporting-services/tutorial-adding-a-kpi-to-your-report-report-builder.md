---
title: 'Tutorial: Agregar un KPI a un informe (Generador de informes) | Microsoft Docs'
ms.date: 06/15/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 1bf77859-0b33-4f40-abaf-ebeeb6ebb1f8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6364a5c3aec5a96bfa3b05cdccc7e91da6f50b71
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2018
ms.locfileid: "48905795"
---
# <a name="tutorial-adding-a-kpi-to-your-report-report-builder"></a>Tutorial: Agregar un KPI a un informe (Generador de informes y SSRS)
En este tutorial de [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)] , agregue un indicador de rendimiento clave (KPI) a un informe paginado de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] .  

Los KPI son valores medibles con significado empresarial. En este escenario, el resumen de ventas por subcategorías de producto es el KPI. El estado actual del KPI se muestra con colores, medidores e indicadores.
  
La ilustración siguiente es similar al informe que va a crear.  
  
![generador-de-informes-informe-kpi](../reporting-services/media/report-builder-kpi-report.png)
    
> [!NOTE]  
> En este tutorial, los pasos del asistente se fusionan en dos procedimientos: uno para crear el conjunto de datos y otro para crear una tabla. Para obtener instrucciones paso a paso sobre cómo ir hasta un servidor de informes, elegir un origen de datos, crear un conjunto de datos y ejecutar el asistente, vea el primer tutorial de esta serie: [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
Tiempo estimado para completar este tutorial: 15 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obtener información sobre los requisitos, vea [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="Table"></a>1. Crear un informe de tabla y un conjunto de datos con el asistente para tablas o matrices  
En esta sección, elija un origen de datos compartido, cree un conjunto de datos incrustado y muestre los datos en una tabla.  
 
### <a name="to-create-a-table-with-an-embedded-dataset"></a>Para crear una tabla con un conjunto de datos incrustado  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el equipo, el portal web de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o el modo integrado de SharePoint.  
  
    Se abre el cuadro de diálogo **Nuevo informe o conjunto de datos** .  
  
    Si no ve el cuadro de diálogo **Nuevo informe o conjunto de datos**, vaya al menú **Archivo** > **Nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel de la derecha, haga clic en **Asistente para tabla o matriz**.  
  
4.  En la página **Elegir un conjunto de datos** , haga clic en **Crear un conjunto de datos**.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página **Elegir una conexión a un origen de datos** , seleccione un origen de datos existente o vaya al servidor de informes y seleccione un origen de datos. Si no está disponible ningún origen de datos o no tiene acceso a un servidor de informes, puede utilizar un origen del datos incrustados en su lugar. Para más información, vea [Tutorial: Crear un informe de tabla básico &#40;Generador de informes&#41;](../reporting-services/tutorial-creating-a-basic-table-report-report-builder.md).  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página **Diseñar una consulta** , haga clic en **Editar como texto**.  
  
9. Copie y pegue la siguiente consulta en el panel de consulta:  

    > [!NOTE]  
    > En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
    ```  
    SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Mini Battery Charger' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Telephoto Conversion Lens' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,'Accessories' as Subcategory,    
       'USB Cable' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Business Videographer' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Social Videographer' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-11' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Advanced Digital' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Compact Digital' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Consumer Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera 35mm' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'SLR Camera' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
10. En la barra de herramientas del diseñador de consultas, haga clic en Ejecutar (**!**).

11. Haga clic en **Siguiente**.  
  
## <a name="CompleteWizard"></a>2. Organizar datos y elegir el diseño en el asistente  
El Asistente para tabla o matriz proporciona un diseño inicial en el que se van a mostrar los datos. El panel de vista previa del asistente le ayudará a visualizar el resultado de las agrupaciones de datos antes de completar la tabla o el diseño de la matriz.  
  
### <a name="to-organize-data-into-groups-and-choose-a-layout"></a>Para organizar los datos en grupos y elegir un diseño 
  
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
  
7.  En la página Elegir el diseño, en **Opciones**, compruebe que esté seleccionada la opción **Mostrar subtotales y totales generales** .  
  
8.  Compruebe que esté seleccionada la opción **Bloqueado, subtotal abajo** .  
  
9. Desactive la opción **Expandir o contraer grupos**.  
  
    En este tutorial, el informe que ha creado no usa la característica de obtención de detalles que permite a un usuario expandir una jerarquía de grupos primarios para mostrar filas de grupos secundarios y filas de detalles.  
  
10. Haga clic en **Siguiente**.  
  
11. Haga clic en **Finalizar**.  
  
      La tabla se agrega a la superficie de diseño. La tabla tiene cinco columnas y cinco filas. El panel Grupos de filas muestra tres grupos de filas: SalesDate, Subcategory y Details. Los datos detallados son todos los datos recuperados por la consulta del conjunto de datos. El panel Grupos de columnas está vacío.  
      
      ![generador-de-informes-kpi-fila-grupos](../reporting-services/media/report-builder-kpi-row-groups.png)
  
12. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
Para cada producto vendido en una fecha concreta, la tabla muestra el nombre del producto, la cantidad vendida y el total de ventas. Los datos se organizan primero por fecha de ventas y, a continuación, por subcategoría. 

![generador-de-informes-kpi-tabla-básica](../reporting-services/media/report-builder-kpi-basic-table.png)
    
### <a name="format-dates-and-currency"></a>Aplicar formato de fecha y moneda
Vamos a hacer las columnas más anchas y establecer el formato de moneda y fecha.

1. Haga clic en **Diseño** para volver a la vista Diseño.

2. Los nombres de producto podrían usar más espacio. Para hacer que la columna Product sea más ancha, seleccione la tabla completa y arrastre el borde derecho del controlador de columna a la parte superior de la columna Product.

3. Presione la tecla CTRL y, después, seleccione las cuatro celdas que contienen [Sum(Sales)].

4. En la pestaña **Inicio** > **Número** > **Moneda**. Las celdas cambian para mostrar la moneda con formato.

   Si la configuración regional es Inglés (Estados Unidos), el texto de ejemplo predeterminado es [$12,345.00]. Si no ve un valor de moneda de ejemplo, haga clic en **Estilos de marcador de posición** en el grupo **Números** > **Valores de ejemplo**.
    
    ![generador-de-informes-marcador de posición-botón-valor](../reporting-services/media/report-builder-placeholder-value-button.png)

5. (Opcional) En la pestaña **Inicio** , en el grupo **Número** , haga clic dos veces en el botón **Disminuir decimales** para mostrar las cifras en dólares sin centavos.

6. Haga clic en la celda que contiene [SalesDate].

6. En el grupo **Número** > **Fecha**.

   La celda muestra la fecha de ejemplo [1/31/2000]. 

12. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
 
![generador-de-informes-kpi-formato-números](../reporting-services/media/report-builder-kpi-format-numbers.png)

## <a name="BackgroundColors"></a>3. Utilizar los colores de fondo para mostrar un KPI  
Los colores de fondo se pueden establecer en una expresión que se evalúe al ejecutar el informe.  
  
### <a name="to-display-the-present-state-of-a-kpi-by-using-background-colors"></a>Para mostrar el estado actual de un KPI mediante colores de fondo  
  
1.  En la tabla, haga clic con el botón derecho en la segunda celda de `[Sum(Sales)]` (la fila de subtotal que muestra las ventas de una subcategoría) y, después, haga clic en **Propiedades de cuadro de texto**. 

    Asegúrese de que ha seleccionado la celda, no el texto de la celda, para ver **Propiedades de cuadro de texto**. 
    
    ![generador-de-informes-cuadro-de-texto-propiedades](../reporting-services/media/report-builder-text-box-properties.png)
  
2.  En la pestaña **Relleno** , haga clic en el botón **fx** situado junto a la opción **Color de relleno** y escriba la siguiente expresión en el campo **Establecer expresión para: BackgroundColor** :  
  
    `=IIF(Sum(Fields!Sales.Value) >= 5000 ,"Lime", IIF(Sum(Fields!Sales.Value) < 2500, "Red","Yellow"))`  
  
     Esto cambia el color de fondo a verde "lima" de cada celda con una suma agregada de `[Sum(Sales)]` superior o igual a 5000. Los valores de `[Sum(Sales)]` entre 2500 y 5000 son "amarillos". Los valores inferiores a 2500 son "rojos".  
  
1.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
2.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
En la fila de subtotal que muestra las ventas de una subcategoría, el color de fondo de la celda será rojo, amarillo o verde en función del valor de la suma de ventas.  

![generador-de-informes-kpi-colores](../reporting-services/media/report-builder-kpi-colors.png)
  
## <a name="Gauge"></a>4. Mostrar un KPI usando un medidor  
Un medidor muestra un valor único de un conjunto de datos. En este tutorial se usa un medidor lineal horizontal porque su forma y simplicidad hacen que resulte fácil leerlo, incluso cuando tiene un tamaño pequeño y está dentro de la celda de una tabla. Para obtener más información, vea [Medidores &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/gauges-report-builder-and-ssrs.md).  
  
### <a name="to-display-the-present-state-of-a-kpi-using-a-gauge"></a>Para mostrar el estado actual de un KPI usando un medidor  
  
1.  Cambie de nuevo a la vista Diseño.  
  
2.  En la tabla, haga clic con el botón derecho en el controlador de columna para la columna Ventas > **Insertar columna** > **Derecha**. Se agregará una nueva columna a la tabla.  

    ![generador-de-informes-kpi-insertar-columna](../reporting-services/media/report-builder-kpi-insert-column.png)
  
3.  Escriba **KPI lineal** en el encabezado de columna.  
  
4.  En la pestaña **Insertar** > **Visualizaciones de datos** > **Medidor** y, después, haga clic en la superficie de diseño fuera de la tabla.   
  
5.  En el cuadro de diálogo **Seleccionar tipo de medidor** , seleccione el primer tipo de medidor lineal, **Horizontal**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Se agregará un medidor a la superficie de diseño.  
  
7.  Del conjunto de datos en el panel Datos de informe, arrastre el campo `Sales` al medidor. El panel **Medidor de datos** se abre.  
  
    Al arrastrar el campo `Sales` al medidor, este se dirige a la lista **Valores** y se agrega mediante la función Sum integrada.  
   
    ![generador-de-informes-kpi-arrastrar-campo-ventas](../reporting-services/media/report-builder-kpi-drag-sales-field.png)
   
9. En el panel **Datos del medidor** , haga clic en la flecha junto a **LinearPointer1** > **Propiedades de puntero**.  
  
10. En el cuadro de diálogo **Propiedades del puntero lineal** > **Opciones de puntero** > **Tipo de puntero**, asegúrese de que **Barra** está seleccionado. 
 
11. Haga clic en **Aceptar**.  
  
12. Haga clic con el botón derecho en la escala del medidor y haga clic en **Propiedades de escala**.  
  
13. En el cuadro de diálogo **Propiedades de escala lineal** > pestaña **General**, establezca **Máximo** en 25 000.  

    > [!NOTE]  
    > En lugar de una constante como 25 000, puede usar una expresión para calcular dinámicamente el valor de la opción **Máximo** . La expresión usaría el agregado de la característica de agregados y es similar a la expresión `=Max(Sum(Fields!Sales.value), "Tablix1")`.  

14. En la pestaña **Etiquetas** , compruebe **Ocultar etiquetas de escala**.

15. Haga clic en **Aceptar**.
  
14. Arrastre el medidor dentro de la tabla a la segunda celda vacía de la columna KPI lineal, en la fila que muestra las ventas subtotales del campo `Subcategory` situado junto al campo donde ha agregado la fórmula del color de fondo.  
  
    > [!NOTE]  
    > Puede que tenga que cambiar el tamaño de la columna para que el medidor lineal horizontal se ajuste a la celda. Para cambiar el tamaño de la columna, seleccione la tabla y arrastre los controladores de columna. La superficie de diseño del informe cambia de tamaño para ajustarse a la tabla.  
  
15. Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
    La longitud horizontal de la barra verde del medidor cambia en función del valor del KPI.  
  
![generador-de-informes-kpi-lineal](../reporting-services/media/report-builder-linear-kpi.png) 
  
## <a name="Indicator"></a>5. Mostrar un KPI usando un indicador  
Los indicadores son medidores pequeños y simples que comunican los valores de datos de un vistazo. Debido a su tamaño y simplicidad, los indicadores se utilizan a menudo en tablas y matrices. Para más información, vea [Indicadores &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/indicators-report-builder-and-ssrs.md).  
  
### <a name="to-display-the-present-state-of-a-kpi-using-an-indicator"></a>Para mostrar el estado actual de un KPI usando un indicador  
  
1.  Cambie a la vista de diseño.  
  
2.  En la tabla, haga clic con el botón derecho en el controlador de columna de la columna KPI lineal que agregó en el último procedimiento > **Insertar columna** > **Derecha**. Se agregará una nueva columna a la tabla.  
  
3.  Escriba **Luz KPI** en el encabezado de columna.  
  
4.  Haga clic en la celda del subtotal de la subcategoría, junto al medidor lineal que ha agregado en el último procedimiento.  
  
5.  En la pestaña **Insertar** > **Visualizaciones de datos** > haga doble clic en **Indicador**.  
  
6.  En el cuadro de diálogo **Seleccionar tipo de indicador** , en **Formas**, seleccione el primer tipo de forma, **3 semáforos (sin marco)**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    El indicador se agrega a la celda en la nueva columna Luz KPI.  
  
8.  Haga clic con el botón derecho en el indicador y, después, haga clic en **Propiedades de indicador**.  
  
9. En la pestaña **Valores y estados** , en el cuadro **Valor** , seleccione **[Sum(Sales)]**. No cambie ninguna de las otras opciones.  
  
    De manera predeterminada, la sincronización de datos se produce en la región de datos y podrá ver el valor **Tablix1**, el nombre de la región de datos de la tabla del informe, en el cuadro **Ámbito de sincronización** .  
  
    En este informe, podrá cambiar también el ámbito de un indicador colocado en la celda del subtotal de la subcategoría para realizar la sincronización en el campo SalesDate.  
  
11. Haga clic en **Aceptar**.

11. Haga clic en **Ejecutar** para obtener la vista previa del informe.  

![generador-de-informes-kpi-luz](../reporting-services/media/report-builder-kpi-stoplight.png)
  
## <a name="Title"></a>6. Agregar un título de informe  
Los títulos de informe aparecen en la parte superior. Puede situar el título del informe en un encabezado de informe o, si el informe no lo utiliza, en un cuadro de texto en la parte superior del cuerpo del informe. En esta sección, usa el cuadro de texto que se coloca automáticamente en la parte superior del cuerpo del informe.  
  
Puede mejorar aún más el texto aplicando estilos de fuente, tamaños y colores diferentes a las frases y los caracteres individuales de este. Para obtener más información, vea [Dar formato al texto en un cuadro de texto &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba **KPI de ventas del producto**y, después, haga clic fuera del cuadro de texto.  
  
3.  De manera opcional, haga clic con el botón derecho en el cuadro de texto que contiene **KPI de ventas del producto**, haga clic en **Propiedades de cuadro de texto**y, después, en la pestaña Fuente, seleccione los diferentes estilos de fuente, tamaños y colores.  
  
4.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
## <a name="Save"></a>7. Guardar el informe  
Guarde el informe un servidor de informes o en su equipo. Si no guarda el informe en el servidor de informes, varias características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como los elementos de informe y los subinformes, no estarán disponibles.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para guardar el informe en un servidor de informes  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Sitios y servidores recientes**.  
  
3.  Seleccione o escriba el nombre del servidor de informes donde tiene el permiso para guardar los informes.  
  
    Aparecerá el mensaje "Conectando con el servidor de informes". Una vez completada la conexión, se mostrará el contenido de la carpeta de informes que el administrador del servidor de informes especificó como ubicación predeterminada para los informes.  
  
4.  En **Nombre**, reemplace el nombre predeterminado por **KPI de ventas del producto**.  
  
5.  Haga clic en **Guardar**.  
  
El informe se guarda en el servidor de informes. El nombre del servidor de informes al que está conectado aparecerá en la barra de estado en la parte inferior de la ventana.  
  
### <a name="to-save-the-report-on-your-computer"></a>Para guardar el informe en el equipo  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Escritorio**, **Mis documentos**o **Mi PC**y vaya a la carpeta donde quiere guardar el informe.  
  
> [!NOTE]  
> Si no tiene acceso a un servidor de informes, haga clic en **Escritorio**, **Mis documentos**o **Mi PC** y guarde el informe en su equipo.  
  
1.  En **Nombre**, reemplace el nombre predeterminado por **KPI de ventas del producto**.  
  
2.  Haga clic en **Guardar**.  
  
## <a name="next-steps"></a>Next Steps  
Ha completado correctamente el tutorial Agregar un KPI a un informe. Para obtener más información, vea:
*  [Medidores](../reporting-services/report-design/gauges-report-builder-and-ssrs.md)
* [Indicadores](../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Ver también  
* [Tutoriales del Generador de informes](../reporting-services/report-builder-tutorials.md)
* [Generador de informes en SQL Server 2016](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  
  

