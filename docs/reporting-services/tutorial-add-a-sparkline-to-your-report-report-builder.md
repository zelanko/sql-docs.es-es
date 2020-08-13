---
title: 'Tutorial: Agregar un minigráfico a un informe (Generador de informes) | Microsoft Docs'
description: Aprenda a usar el Generador de informes para crear una tabla básica con un minigráfico en un informe paginado de Reporting Services.
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 18c90a36-48bf-4805-a960-2d1e8f00c2dc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: fe0d52f55905721002a1590f54ada84d7732f2a0
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245662"
---
# <a name="tutorial-add-a-sparkline-to-your-report-report-builder"></a>Tutorial: Adición de un minigráfico a un informe (Generador de informes)

En este tutorial del [!INCLUDE[ssRBnoversion_md](../includes/ssrbnoversion.md)], puede crear una tabla básica con un minigráfico en un informe paginado de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] .   
  
Los minigráficos y las barras de datos son gráficos simples y pequeños que contienen mucha información en poco espacio, a menudo en tablas y matrices de los informes de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] . En la siguiente ilustración se muestra un informe similar al que creará.  
  
![generador-de-informes-minigráfico-final](../reporting-services/media/report-builder-sparkline-final.png)  
     
Tiempo estimado para completar este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para obtener más información sobre los requisitos, consulte [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="1-create-a-report-with-a-table"></a><a name="CreateTable"></a>1. Crear un informe con una tabla  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el equipo, el portal web de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o el modo integrado de SharePoint.  
  
    Se abre el cuadro de diálogo **Nuevo informe o conjunto de datos** .  
  
    Si no ve el cuadro de diálogo **Nuevo informe o conjunto de datos**, vaya al menú **Archivo** > **Nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel de la derecha, haga clic en **Asistente para tabla o matriz**.  
  
4.  En la página **Elegir un conjunto de datos** , seleccione **Crear un conjunto de datos** > **Siguiente**. Se abre la página **Elegir una conexión a un origen de datos** .  
  
    > [!NOTE]  
    > Para este tutorial no se necesitan datos concretos, solo una conexión a una base de datos de SQL Server. Si ya tiene una conexión de origen de datos enumerada en **Conexiones de origen de datos**, puede seleccionarla e ir al paso 10. Para obtener más información, consulte [Maneras alternativas de obtener una conexión de datos &#40;Generador de informes&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
5.  Haga clic en **Nueva**. Se abre el cuadro de diálogo **Propiedades del origen de datos** .  
  
6.  En **Nombre**, escriba **Ventas de producto**como nombre del origen de datos.  
  
7.  En **Seleccionar un tipo de conexión**, compruebe que está seleccionado **Microsoft SQL Server** .  
  
8.  En **Cadena de conexión**, escriba el texto siguiente:  
  
    `Data Source\=<servername>`  
  
    La expresión `<servername>`, por ejemplo Report001, especifica un equipo en el que se ha instalado una instancia del motor de SQL Server Database. Dado que los datos del informe no se extraen de una base de datos de SQL Server, no necesita incluir el nombre de una base de datos. Para analizar la consulta se utiliza la base de datos predeterminada en el servidor especificado.  
  
9. Haga clic en **Credenciales**. Escriba las credenciales necesarias para tener acceso al origen de datos externo.  
  
10. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Volverá a encontrarse en la página **Elegir una conexión a un origen de datos** .  
  
11. Para comprobar que se puede conectar al origen de datos, haga clic en **Probar conexión**.  
  
    Aparece un mensaje que indica que la conexión se ha creado correctamente.  
  
12. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
13. Haga clic en **Next**.  
  
## <a name="2-create-a-query-and-table-layout-in-the-table-wizard"></a><a name="Query"></a>2. Crear una consulta y un diseño de tabla en el Asistente para tablas  
En un informe puede usar un conjunto de datos compartido que tenga una consulta predefinida o crear un conjunto de datos incrustado para usarlo exclusivamente en ese informe. En este tutorial, creará un conjunto de datos incrustado.  
  
> [!NOTE]  
> En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
### <a name="to-create-a-query-and-table-layout-in-the-table-wizard"></a>Para crear una consulta y un diseño de tabla en el Asistente para tablas 
  
1.  En la página **Diseñar una consulta** , el diseñador de consultas relacionales está abierto. En este tutorial, usará el diseñador de consultas basado en texto.  
  
2.  Haga clic en **Editar como texto**. El diseñador de consultas basado en texto muestra un panel de consulta y un panel de resultados.  
  
3.  Pegue la siguiente consulta [!INCLUDE[tsql](../includes/tsql-md.md)] en el cuadro **Consulta** .  
  
    ```  
    SELECT CAST('2015-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Carrying Case' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-04' AS date) as SalesDate, 'Accessories' as Subcategory,  
       'Budget Movie-Maker' as Product, CAST(1056.00 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,  'Accessories' as Subcategory,  
       'Slim Digital' as Product, CAST(1380.00 AS money) AS Sales, 18 as Quantity  
    UNION SELECT CAST('2015-01-05' AS date) as SalesDate,'Accessories' as Subcategory,    
       'Budget Movie-Maker' as Product, CAST(780.00 AS money) AS Sales, 26 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3798.00 AS money) AS Sales, 9 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(10400.00 AS money) AS Sales, 13 as Quantity  
    UNION SELECT CAST('2015-01-09' AS date) as SalesDate, 'Camcorders' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(3000.00 AS money) AS Sales, 60 as Quantity  
    UNION SELECT CAST('2015-01-10' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Budget Movie-Maker' as Product, CAST(7234.50 AS money) AS Sales, 39 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Carrying Case' as Product, CAST(10836.00 AS money) AS Sales, 84 as Quantity  
    UNION SELECT CAST('2015-01-07' AS date) as SalesDate,  'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(2550.00 AS money) AS Sales, 17 as Quantity  
    UNION SELECT CAST('2015-01-04' AS date) as SalesDate, 'Digital' as Subcategory,   
       'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity  
    UNION SELECT CAST('2015-01-08' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(18530.00 AS money) AS Sales, 34 as Quantity  
    UNION SELECT CAST('2015-01-06' AS date) as SalesDate, 'Digital SLR' as Subcategory,   
       'Slim Digital' as Product, CAST(26576.00 AS money) AS Sales, 88 as Quantity  
    ```  
  
4.  En la barra de herramientas del diseñador de consultas, haga clic en Ejecutar ( **!** ).  
  
    La consulta se ejecuta y muestra el conjunto de resultados para los campos **SalesDate**, **Subcategory**, **Product**, **Sales**y **Quantity**.  
  
5.  Haga clic en **Next**.  
  
6.  En la página **Organizar campos** , arrastre **Sales** hasta **Valores**.  
  
    La función Sum agrega**Sales** . El valor es [Sum(Sales)].  
  
7.  Arrastre **Product** hasta **Grupos de filas**.  
  
8.  Arrastre **SalesDate** hasta **Grupos de columnas**.  

    ![generador-de-informes-minigráfico-organizar-campos](../reporting-services/media/report-builder-sparkline-arrange-fields.png)
  
9. Haga clic en **Next**.  
  
10. En la página **Elegir el diseño** , en **Opciones**, compruebe que esté seleccionada la opción **Mostrar subtotales y totales generales** .  
  
    El panel Vista previa del asistente muestra una tabla con tres filas. Al ejecutar el informe, cada fila se mostrará de la siguiente forma:  
  
    *  La primera fila aparecerá una vez en la tabla para mostrar los encabezados de columna.  
  
    *  La segunda fila se repetirá una vez en cada producto y mostrará el nombre del producto, el total por día y el total de línea.  
  
    *  La tercera fila aparecerá una vez en la tabla para mostrar los totales generales.  
    
    ![generador-de-informes-minigráfico-elegir-diseño](../reporting-services/media/report-builder-sparkline-choose-layout.png)
  
11. Haga clic en **Next**.  
  
12. Haga clic en **Finalizar**  
  
14. La tabla se agrega a la superficie de diseño. La tabla tiene tres columnas y tres filas.  
  
    Busque en el panel Agrupación. Si no ve el panel Agrupación, en el menú **Vista** , haga clic en **Agrupación**. El panel Grupos de filas muestra un grupo de filas: **Product**. El panel Grupos de columnas muestra un grupo de columnas: **SalesDate**. Los datos detallados son todos los datos recuperados por la consulta del conjunto de datos.  
    
    ![generador-de-informes-minigráfico-panel-agrupación](../reporting-services/media/report-builder-sparkline-grouping-pane.png)
  
15. Haga clic en **Ejecutar** para obtener la vista previa del informe.  

### <a name="2a-format-data-as-currency"></a><a name="FormatCurrency"></a>2a. Dar formato a los datos como moneda  
De manera predeterminada, los datos de resumen del campo **Sales** se muestran en forma de número general. Aplíquele el formato adecuado para mostrar el número como moneda. Alterne **Estilos de marcador de posición** para mostrar los cuadros de texto con formato y el texto de marcador de posición como valores de ejemplo.  
  
1.  Haga clic en **Diseño** para cambiar a la vista de diseño.  
  
2.  Haga clic en la celda en la segunda fila (bajo la fila de encabezados de columna) en la columna **SalesDate** . Mantenga presionada la tecla CTRL y seleccione todas las celdas que contienen `[Sum(Sales)]`. 

    ![generador-de-informes-seleccionar-sum-sales](../reporting-services/media/report-builder-select-sum-sales.png) 
  
3.  En la pestaña **Inicio** > grupo **Número**, haga clic en **Moneda**. Las celdas cambian para mostrar la moneda con formato.  

    ![generador-de-informes-marcador de posición-moneda](../reporting-services/media/report-builder-placeholder-currency.png)
  
    Si la configuración regional es Inglés (Estados Unidos), el texto de ejemplo predeterminado es [ **$12,345.00**]. Si no ve un valor de moneda de ejemplo, haga clic en **Estilos de marcador de posición** en el grupo **Números** > **Valores de ejemplo**.  
    
    ![generador-de-informes-botón-valor-marcador-de-posición](../reporting-services/media/report-builder-placeholder-value-button.png)
   
### <a name="2b-optional-format-data-as-dates"></a><a name="FormatDates"></a>2b. (Opcional) Dar formato a datos como fechas  
De manera predeterminada, en el campo **SalesDate** se muestra información de fecha y hora. Puede darle formato para mostrar solo la fecha.  
  
1.  Haga clic en la celda que contiene `[SalesDate]`.  
  
3.  En la pestaña **Inicio** > grupo **Número** > **Fecha**.  
  
    La celda muestra la fecha de ejemplo **[1/31/2000]** .
     
4.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
Los valores **SalesDate** se muestran en el formato de fecha predeterminado, y los valores de resumen para **Sales** se muestran como moneda.   
  
## <a name="3-add-a-sparkline"></a><a name="Sparkline"></a>3. Agregar un minigráfico    
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Seleccione la columna Total en su tabla.  
  
3.  Haga clic con el botón derecho, señale **Insertar columna**y, después, haga clic en **Izquierda**.  

    ![generador-de-informes-agregar-columna-izquierda](../reporting-services/media/report-builder-add-column-left.png)
  
4.  En la nueva columna, haga clic con el botón derecho en la celda de la fila `[Product]` > **Insertar** > **Minigráfico**.  

    ![generador-de-informes-insertar-minigráfico](../reporting-services/media/report-builder-insert-sparkline.png)
  
5.  En el cuadro de diálogo **Seleccionar tipo de minigráfico** , asegúrese de que está seleccionado el primer minigráfico de la fila **Columna** y, después, haga clic en **Aceptar**.  
  
6.  Haga clic en el minigráfico para mostrar el panel Datos del gráfico.  
  
7.  Haga clic en el signo más (+) en el cuadro Valores y, después, haga clic en **Sales**. 

    ![generador-de-informes-valores-minigráfico](../reporting-services/media/report-builder-sparkline-values.png) 
  
    Los valores del campo **Sales** son ahora los valores para el minigráfico.  
  
8.  Haga clic en el signo más (+) en el cuadro Grupos de categorías y, después, haga clic en **SalesDate**.  
  
9. Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
    Tenga en cuenta que las barras de los minigráficos no están alineadas entre sí. Solo hay cuatro barras en la segunda fila de datos, por lo que las barras son más anchas que las de la primera fila, que tiene seis. No puede comparar los valores para cada producto por día. Deben alinearse.  
  
    Además, para cada fila, la barra más alta es el alto de la fila. Esto también induce a error porque los valores mayores de cada fila no son iguales: el valor mayor para Budget Movie-Maker es 10 400 $, pero para Slim Digital es 26 576 $, más del doble. Además, las barras más grandes de esas dos filas tienen aproximadamente el mismo alto. Todos los minigráficos necesitan usar la misma escala.  
  
     ![generador-de-informes-minigráfico-desalineados](../reporting-services/media/report-builder-sparkline-misaligned.png)
  
## <a name="4-align-the-sparklines-vertically-and-horizontally"></a><a name="AlignSparklines"></a>4. Alinear los minigráficos vertical y horizontalmente  
Los minigráficos son difíciles de leer cuando todos no usan las mismas medidas. Los ejes horizontal y vertical de cada uno tienen que coincidir con el resto.  
   
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic con el botón derecho en el minigráfico y, después, haga clic en **Propiedades del eje vertical**.  
  
3.  Active la casilla **Alinear ejes en** . Tablix1 es la única opción de la lista.  
  
     Establece el alto de las barras en cada minigráfico con respecto a los demás. 
  
4.  Haga clic en **OK**.  
  
5.  Haga clic con el botón derecho en el minigráfico y, después, haga clic en **Propiedades del eje horizontal**.  
  
6.  Active la casilla **Alinear ejes en** . Tablix1 es la única opción de la lista. 
  
    Establece el ancho de las barras en cada minigráfico con respecto a los demás. Si algunos minigráficos tienen menos barras que otros, dichos minigráficos tendrán espacios en blanco correspondientes a los datos que faltan.  
  
7.  Haga clic en **OK**.  
  
8.  Para volver a obtener una vista previa de un informe, haga clic en **Ejecutar** .  
  
Ahora todas las barras de cada minigráfico se alinean con las barras de los otros minigráficos, y el alto es relativo.  
  
![generador-de-informes-minigráfico-alineados](../reporting-services/media/report-builder-sparkline-aligned.png)
  
## <a name="7-optional-change-column-widths"></a><a name="Width"></a>7. (Opcional) Cambiar el ancho de columna  
De forma predeterminada, cada celda de una tabla contiene un cuadro de texto. Un cuadro de texto se expande verticalmente para alojar el texto cuando se representa la página. En el informe representado, cada fila se expande hasta el alto del cuadro de texto más alto representado de la fila. El alto de la fila en la superficie de diseño no tiene efecto alguno en el alto de la fila en el informe representado.  
  
Para reducir la cantidad de espacio vertical que ocupa cada fila, expanda el ancho de columna para dar cabida en una línea al contenido previsto de los cuadros de texto de la columna.  
  
### <a name="to-change-the-width-of-columns"></a>Para cambiar el ancho de las columnas  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic en la tabla para que las barras grises aparezcan encima y al lado de la tabla. Esos son los controladores de columna y fila
  
3.  Sitúe el cursor en la línea que hay entre los controladores de columna para que cambie a una flecha doble. Arrastre la columna **Product** para que el nombre de producto se muestre en una línea.  
  
4.  Haga clic en **Ejecutar** para obtener una vista previa del informe y ver si tiene un ancho suficiente.  
  
## <a name="8-optional-add-a-report-title"></a><a name="Title"></a>8. (Opcional) Agregar un título de informe  
Los títulos de informe aparecen en la parte superior. Puede situar el título del informe en un encabezado de informe o, si el informe no lo utiliza, en un cuadro de texto en la parte superior del cuerpo del informe. En este tutorial, deberá utilizar el cuadro de texto que se coloca automáticamente en la parte superior del cuerpo del informe.  
  
El texto se puede mejorar aún más aplicando estilos de fuente, tamaños y colores diferentes a las frases y caracteres individuales. Para obtener más información, vea [Dar formato al texto en un cuadro de texto &#40;Generador de informes y SSRS&#41;](../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba **Ventas por fecha**y, después, haga clic fuera del cuadro de texto.  
  
3.  Seleccione el cuadro de texto que contiene **Ventas de producto**.  
  
4.  En la pestaña Inicio > grupo **Fuente** > seleccione **Verde azulado** para **Color**.  
  
7.  Seleccione **Negrita**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="9-save-the-report"></a><a name="Save"></a>9. Guardar el informe  
Guarde el informe un servidor de informes o en su equipo. Si no guarda el informe en el servidor de informes, varias características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como los elementos de informe y los subinformes, no estarán disponibles.  
  
### <a name="to-save-the-report-on-a-report-server"></a>Para guardar el informe en un servidor de informes  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Sitios y servidores recientes**.  
  
3.  Seleccione o escriba el nombre del servidor de informes donde tiene el permiso para guardar los informes.  
  
    Aparecerá el mensaje "Conectando con el servidor de informes". Una vez completada la conexión, se mostrará el contenido de la carpeta de informes que el administrador del servidor de informes especificó como ubicación predeterminada para los informes.  
  
4.  En **Nombre**, reemplace el nombre predeterminado por **Ventas de producto**.  
  
5.  Haga clic en **Save**(Guardar).  
  
El informe se guarda en el servidor de informes. El nombre del servidor de informes al que está conectado aparecerá en la barra de estado en la parte inferior de la ventana.  
  
### <a name="to-save-the-report-on-your-computer"></a>Para guardar el informe en el equipo  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Escritorio**, **Mis documentos**o **Mi PC**y vaya a la carpeta donde quiere guardar el informe.  
  
3.  En **Nombre**, reemplace el nombre predeterminado por **Ventas de producto**.  
  
4.  Haga clic en **Save**(Guardar).  
  
## <a name="next-steps"></a>Pasos siguientes  

Esto concluye el tutorial para crear un informe de tabla con minigráficos. Para obtener más información sobre los minigráficos, vea [Minigráficos y barras de datos](../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md).  
  
[Tutoriales (Generador de informes)](../reporting-services/report-builder-tutorials.md) 
[Generador de informes en SQL Server](../reporting-services/report-builder/report-builder-in-sql-server-2016.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
