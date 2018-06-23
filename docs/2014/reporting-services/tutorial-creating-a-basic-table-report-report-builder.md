---
title: 'Tutorial: Crear un informe de tabla básico (Generador de informes) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d9e30521-f8ae-4c45-89c3-d40727f622f7
caps.latest.revision: 12
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 7c197e6f13497b82655f8c20872637d8bc8e7ed0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113969"
---
# <a name="tutorial-creating-a-basic-table-report-report-builder"></a>Tutorial: Crear un informe de tabla básico (Generador de informes)
  Este tutorial muestra cómo crear un informe de tabla básico basado en datos de ventas de ejemplo. En la siguiente ilustración se muestra el informe que va a crear.  
  
 ![rs_CreateBasicReportTutorial](../../2014/tutorials/media/rs-createbasicreporttutorial.gif "rs_CreateBasicReportTutorial")  
  
##  <a name="BackToTop"></a> Qué aprenderá  
 En este tutorial, aprenderá a realizar las siguientes tareas:  
  
1.  [Crear un nuevo informe desde Introducción](#CreateTable)  
  
    1.  [Especificar una conexión de datos en el Asistente para tablas](#DataConnection)  
  
    2.  [Crear una consulta en el Asistente para tablas](#Query)  
  
    3.  [Organizar los datos en grupos en el Asistente para tablas](#Groups)  
  
    4.  [Agregar filas Subtotal y de Total en el Asistente para tablas](#Subtotals)  
  
    5.  [Elegir un estilo en el Asistente para tablas](#Style)  
  
2.  [Dar formato a datos como moneda](#FormatCurrency)  
  
3.  [Dar formato a datos como fecha](#FormatDate)  
  
4.  [Cambiar el ancho de columna](#Width)  
  
5.  [Agregar un título de informe](#Title)  
  
6.  [Guardar el informe](#Save)  
  
7.  [Exportar el informe](#Export)  
  
 Tiempo estimado para completar este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obtener más información sobre los requisitos, consulte [Requisitos previos para los tutoriales &#40;Generador de informes&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="CreateTable"></a> 1. Crear un informe desde Introducción  
 Crear un informe de tabla desde el **Introducción** cuadro de diálogo. Existen dos modos: diseño de informe y el diseño de conjunto de datos compartido. En el modo de diseño de informe, los datos se especifican en el panel Datos de informe y el diseño del informe se especifica en la superficie de diseño. En modo de diseño de conjunto de datos compartido, se crean consultas de conjunto de datos para compartir con otros usuarios. En este tutorial, utilizará el modo de diseño de informe.  
  
#### <a name="to-create-a-new-report"></a>Para crear un informe nuevo  
  
1.  Haga clic en **Inicio**, seleccione **Programas**, **Generador de informes de Microsoft SQL Server 2012**y, a continuación, haga clic en **Generador de informes**.  
  
     El **Introducción** abre el cuadro de diálogo.  
  
    > [!NOTE]  
    >  Si el **Introducción** cuadro de diálogo no aparece, desde el **Report Builder** botón, haga clic en **nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel derecho, compruebe que **Asistente para tabla o matriz** está seleccionado.  
  
##  <a name="DataConnection"></a> 1a. Especificar una conexión de datos en el Asistente para tablas  
 Una conexión de datos contiene la información para conectarse a un origen de datos externo, por ejemplo una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Normalmente, la información de conexión y el tipo de credenciales que se debe usar utilizar se obtienen del propietario del origen de datos. Para especificar una conexión de datos, puede utilizar un origen de datos compartido del servidor de informes o crear un origen de datos incrustado que solo se utilice en este informe.  
  
 En este tutorial, utilizará un origen del datos incrustado. Para obtener más información sobre cómo usar orígenes de datos compartidos, consulte [Maneras alternativas de obtener una conexión de datos &#40;Generador de informes&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
#### <a name="to-create-an-embedded-data-source"></a>Para crear un origen de datos incrustado  
  
1.  En la página **Elegir un conjunto de datos** , seleccione **Crear un conjunto de datos**y, después, haga clic en **Siguiente**. Se abre la página **Elegir una conexión a un origen de datos** .  
  
2.  Haga clic en **Nueva**. Se abre el cuadro de diálogo **Propiedades del origen de datos** .  
  
3.  En **nombre**, tipo **ventas del producto** un nombre para el origen de datos.  
  
4.  En **Seleccionar un tipo de conexión**, compruebe que está seleccionado **Microsoft SQL Server** .  
  
5.  En **cadena de conexión**, escriba el texto siguiente, donde  *\<servername >* es el nombre de una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
    ```  
    Data Source=<servername>  
    ```  
  
     Puesto que va a usar una consulta con los datos en lugar de recuperar los datos de una base de datos, la cadena de conexión no incluye el nombre de la base de datos. Para obtener más información, consulte [Requisitos previos para los tutoriales&#40;Generador de informes&#41;](../reporting-services/report-builder-tutorials.md).  
  
6.  Haga clic en **Credenciales**. Escriba las credenciales necesarias para tener acceso al origen de datos externo.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     Volverá a encontrarse en la página **Elegir una conexión a un origen de datos** .  
  
8.  Para comprobar que se puede conectar al origen de datos, haga clic en **Probar conexión**.  
  
     Aparece un mensaje que indica que la conexión se ha creado correctamente.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
10. Haga clic en **Siguiente**.  
  
##  <a name="Query"></a> 1b. Crear una consulta en el Asistente para tablas  
 En un informe puede usar un conjunto de datos compartido que tenga una consulta predefinida o crear un conjunto de datos incrustado para usarlo exclusivamente en ese informe. En este tutorial, creará un conjunto de datos incrustado.  
  
> [!NOTE]  
>  En este tutorial, la consulta contiene los valores de datos, de forma que no necesita un origen de datos externo. Esto hace que la consulta requiera bastante tiempo. En un entorno empresarial, la consulta no contendría los datos. Esto es solo con fines de aprendizaje.  
  
#### <a name="to-create-a-query"></a>Para crear una consulta  
  
1.  En la página **Diseñar una consulta** , el diseñador de consultas relacionales está abierto. En este tutorial, usará el diseñador de consultas basado en texto.  
  
     Haga clic en **Editar como texto**. El diseñador de consultas basado en texto muestra un panel de consulta y un panel de resultados.  
  
2.  Pegue la siguiente consulta [!INCLUDE[tsql](../includes/tsql-md.md)] en el cuadro **Consulta** .  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Accessories' as Subcategory,   
       'Carrying Case' as Product, CAST(9924.60 AS money) AS Sales, 68 as Quantity  
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
  
3.  En la barra de herramientas del diseñador de consultas, haga clic en **Ejecutar** (**!**).  
  
     La consulta se ejecuta y muestra el conjunto de resultados para los campos SalesDate, Subcategory, Product, Sales y Quantity.  
  
     En el conjunto de resultados, los encabezados de columna están basados en los nombres de la consulta. En el conjunto de datos, los encabezados de columna se convierten en nombres de campo y se guardan en el informe. Después de completar el asistente, puede usar el panel Datos de informe para ver la colección de campos del conjunto de datos.  
  
4.  Haga clic en **Siguiente**.  
  
##  <a name="Groups"></a> c de 1. Organizar datos en grupos en el Asistente para tablas  
 Al seleccionar los campos por los que desea agrupar, diseña una tabla que tiene filas y columnas en las que se muestran datos detallados y datos agregados.  
  
#### <a name="to-organize-data-into-groups"></a>Para organizar los datos en grupos  
  
1.  En la página **Organizar campos** , arrastre Product hasta **Valores**.  
  
2.  Arrastre Quantity hasta **Valores** y colóquelo debajo de Product.  
  
     Quantity se suma automáticamente mediante la función Sum, que es el agregado predeterminado para los campos numéricos. El valor es [Sum(Quantity)].  
  
     Puede abrir la lista desplegable para ver las demás funciones de agregado disponibles. No cambie la función de agregado.  
  
3.  Arrastre Sales hasta **Valores** y colóquelo debajo de [Sum(Quantity)].  
  
     La función Sum agrega Sales. El valor es [Sum(Sales)].  
  
     Los pasos 1, 2 y 3 especifican los datos que deben mostrarse en la tabla.  
  
4.  Arrastre SalesDate hasta **Grupos de filas**.  
  
5.  Arrastre Subcategory hasta **Grupos de filas** y colóquelo debajo de SalesDate.  
  
     Los pasos 4 y 5 organizan los valores de los campos primero por fecha y, después, por la subcategoría de producto de esa fecha.  
  
6.  Haga clic en **Siguiente**.  
  
##  <a name="Subtotals"></a> 1D. Agregar filas de subtotal y de total en el Asistente para tablas  
 Después de crear grupos, puede agregar filas y darles formato, para mostrar en ellas los valores agregados de los campos. Puede decidir si mostrar todos los datos o permitir que los usuarios expandan y contraigan de forma interactiva los datos agrupados.  
  
#### <a name="to-add-subtotals-and-totals"></a>Para agregar subtotales y totales  
  
1.  En la página **Elegir el diseño** , en **Opciones**, compruebe que esté seleccionada la opción **Mostrar subtotales y totales generales** .  
  
2.  Compruebe que esté seleccionada la opción **Bloqueado, subtotal abajo** .  
  
     El panel Vista previa del asistente muestra una tabla con cinco filas. Al ejecutar el informe, cada fila se mostrará de la siguiente forma:  
  
    1.  La primera fila se repetirá una vez en la tabla para mostrar los encabezados de columna.  
  
    2.  La segunda fila se repetirá una vez en cada artículo de línea del pedido de venta y mostrará el nombre del producto, la cantidad del pedido y el total de línea.  
  
    3.  La tercera fila se repetirá una vez en cada pedido de venta para mostrar los subtotales de cada pedido.  
  
    4.  La cuarta fila se repetirá una vez en cada fecha de pedido para mostrar los subtotales por día.  
  
    5.  La quinta fila se repetirá una vez en la tabla para mostrar los totales generales.  
  
3.  Desactive la opción **Expandir o contraer grupos**. En este tutorial, el informe que ha creado no usa la característica de obtención de detalles que permite a un usuario expandir una jerarquía de grupos primarios para mostrar filas de grupos secundarios y filas de detalles.  
  
4.  Haga clic en **Siguiente**.  
  
##  <a name="Style"></a> 1E. Elegir un estilo en el Asistente para tablas  
 Un estilo especifica un estilo de fuente, un conjunto de colores y un estilo de borde.  
  
#### <a name="to-specify-a-table-style"></a>Para especificar un estilo de tabla  
  
1.  En el **elegir un estilo** página, en el panel Estilos, seleccione Océano.  
  
     El panel Vista previa muestra un ejemplo de la tabla con ese estilo.  
  
2.  Opcionalmente, haga clic en los otros estilos para ver el ejemplo con ellos aplicados.  
  
3.  Haga clic en **Finalizar**.  
  
 La tabla se agrega a la superficie de diseño. La tabla tiene 5 columnas y 5 filas. El panel Grupos de filas muestra tres grupos de filas: SalesDate, Subcategory y Details. Los datos detallados son todos los datos recuperados por la consulta del conjunto de datos.  
  
##  <a name="FormatCurrency"></a> 2. Dar formato a los datos como moneda  
 De forma predeterminada, los datos de resumen del campo Sales se muestran en forma de número general. Aplíquele el formato adecuado para mostrar el número como moneda. Alterne **Estilos de marcador de posición** para mostrar los cuadros de texto con formato y el texto de marcador de posición como valores de ejemplo.  
  
#### <a name="to-format-a-currency-field"></a>Para dar formato a un campo de moneda  
  
1.  Haga clic en **Diseño** para cambiar a la vista de diseño.  
  
2.  Haga clic en la celda en la segunda fila (bajo la fila de encabezados de columna) en la columna Sales y arrástrela hacia abajo para seleccionar todas las celdas que contienen `[Sum(Sales)]`.  
  
3.  En la pestaña **Inicio** , en el grupo **Número** , haga clic en el botón **Moneda** . Las celdas cambian para mostrar la moneda con formato.  
  
     Si la configuración regional es Inglés (Estados Unidos), el texto de ejemplo predeterminado es [**$12,345.00**]. Si no ve un valor de moneda de ejemplo, haga clic en **estilos de marcador de posición** en el **números** de grupo y, a continuación, haga clic en **valores de ejemplo**.  
  
4.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
 Los valores de resumen de Sales se muestran como moneda.  
  
##  <a name="FormatDate"></a> 3. Dar formato a los datos como fecha  
 De forma predeterminada, en el campo SalesDate se muestra información de fecha y hora. Puede darle formato para mostrar solo la fecha.  
  
#### <a name="to-format-a-date-field-as-the-default-format"></a>Para dar formato a un campo de fecha como el formato predeterminado  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic en la celda que contiene `[SalesDate]`.  
  
3.  En la cinta de opciones, en el **inicio** ficha la **número** grupo, en la lista desplegable, seleccione **fecha**.  
  
     La celda muestra la fecha de ejemplo **[1/31/2000]**. Si no ve un valor de fecha de ejemplo, haga clic en **Estilos de marcador de posición** en el grupo **Números** y, después, haga clic en **Valores de ejemplo**.  
  
4.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
 Los valores SalesDate se muestran en el formato de fecha predeterminado.  
  
#### <a name="to-change-the-date-format-to-a-custom-format"></a>Para cambiar el formato de fecha a un formato personalizado  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic en la celda que contiene `[SalesDate]`.  
  
3.  En el **inicio** ficha la **número** grupo, haga clic en el selector de cuadro de diálogo.  
  
     El selector es la pequeña flecha situada en la esquina derecha del grupo. Se abre el cuadro de diálogo **Propiedades del cuadro de texto** .  
  
4.  En el panel Categoría, compruebe que está seleccionada la opción **Fecha** .  
  
5.  En el panel **Tipo** , seleccione **31 de enero de 2000**.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     La celda muestra la fecha de ejemplo **[31 de enero de 2000]**.  
  
7.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
 El valor SalesDate se muestra con el nombre del mes en lugar del número del mes.  
  
##  <a name="Width"></a> 4. Cambiar el ancho de columna  
 De forma predeterminada, cada celda de una tabla contiene un cuadro de texto. Un cuadro de texto se expande verticalmente para alojar el texto cuando se representa la página. En el informe representado, cada fila se expande hasta el alto del cuadro de texto más alto representado de la fila. El alto de la fila en la superficie de diseño no tiene efecto alguno en el alto de la fila en el informe representado.  
  
 Para reducir la cantidad de espacio vertical que ocupa cada fila, expanda el ancho de columna para dar cabida en una línea al contenido previsto de los cuadros de texto de la columna.  
  
#### <a name="to-change-the-width-of-table-columns"></a>Para cambiar el ancho de las columnas de la tabla  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic en la tabla para que los identificadores de columna y de fila aparezcan encima y al lado de la tabla.  
  
     Las barras grises situadas en la parte superior y en el lado de la tabla son los identificadores de fila y de columna.  
  
3.  Sitúe el cursor en la línea que hay entre los controladores de columna para que cambie a una flecha doble. Arrastre las columnas hasta que tengan el tamaño deseado. Por ejemplo, expanda la columna Producto para que el nombre de producto se muestre en una línea.  
  
4.  Haga clic en **Ejecutar** para obtener una vista previa del informe.  
  
##  <a name="Title"></a> 5. Agregar un título de informe  
 Los títulos de informe aparecen en la parte superior. Puede situar el título del informe en un encabezado de informe o, si el informe no lo utiliza, en un cuadro de texto en la parte superior del cuerpo del informe. En este tutorial, deberá utilizar el cuadro de texto que se coloca automáticamente en la parte superior del cuerpo del informe.  
  
 El texto se puede mejorar aún más aplicando estilos de fuente, tamaños y colores diferentes a las frases y caracteres individuales. Para obtener más información, vea [Dar formato al texto en un cuadro de texto &#40;Generador de informes y SSRS&#41;](report-design/format-text-in-a-text-box-report-builder-and-ssrs.md).  
  
#### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba **Ventas del producto**y después haga clic fuera del cuadro de texto.  
  
3.  Haga clic con el botón secundario en el cuadro de texto que contiene **Ventas del producto** y haga clic en **Propiedades de cuadro de texto**.  
  
4.  En el cuadro de diálogo **Propiedades de cuadro de texto** , haga clic en **Fuente**.  
  
5.  En la lista **Tamaño** , seleccione **18 pt**.  
  
6.  En la lista **Color** , seleccione **Azul aciano**.  
  
7.  Seleccione **Negrita**.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="Save"></a> 6. Guardar el informe  
 Guarde el informe un servidor de informes o en su equipo. Si no guarda el informe en el servidor de informes, varias características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como los elementos de informe y los subinformes, no estarán disponibles.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Para guardar el informe en un servidor de informes  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Sitios y servidores recientes**.  
  
3.  Seleccione o escriba el nombre del servidor de informes donde tiene el permiso para guardar los informes.  
  
     Aparecerá el mensaje "Conectando con el servidor de informes". Una vez completada la conexión, se mostrará el contenido de la carpeta de informes que el administrador del servidor de informes especificó como ubicación predeterminada para los informes.  
  
4.  En **Nombre**, reemplace el nombre predeterminado por **Ventas de producto**.  
  
5.  Haga clic en **Guardar**.  
  
 El informe se guarda en el servidor de informes. El nombre del servidor de informes al que está conectado aparecerá en la barra de estado en la parte inferior de la ventana.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Para guardar el informe en el equipo  
  
1.  En el botón **Generador de informes** , haga clic en **Guardar como**.  
  
2.  Haga clic en **Escritorio**, **Mis documentos**o **Mi PC**y vaya a la carpeta donde quiere guardar el informe.  
  
3.  En **Nombre**, reemplace el nombre predeterminado por **Ventas de producto**.  
  
4.  Haga clic en **Guardar**.  
  
##  <a name="Export"></a> 7. Exportar el informe  
 Los informes se pueden exportar a diversos formatos, por ejemplo Microsoft Excel y valores separados por comas (CSV). Para obtener más información, consulte [exportar informes &#40;el generador de informes y SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md).  
  
 En este tutorial, exportará el informe a Excel y establecerá una propiedad en el informe para proporcionar un nombre personalizado para la pestaña del libro.  
  
#### <a name="to-specify-the-workbook-tab-name"></a>Para especificar el nombre de la pestaña del libro  
  
1.  Haga clic en **Diseño** para volver a la vista de diseño.  
  
2.  Haga clic en cualquier lugar fuera del informe.  
  
3.  . En el panel Propiedades, busque la propiedad InitialPageName y escriba **Excel de ventas del producto**.  
  
    > [!NOTE]  
    >  Si el panel de propiedades no está visible, haga clic en la pestaña de vista en la cinta de opciones y, a continuación, haga clic en **propiedades**.  
  
#### <a name="to-export-a-report-to-excel"></a>Exportar un informe a Excel  
  
1.  Haga clic en **Ejecutar** para obtener la vista previa del informe.  
  
2.  . En la cinta de opciones, haga clic en **exportar**y, a continuación, haga clic en **Excel**.  
  
     Se abre el cuadro de diálogo **Guardar como** .  
  
3.  Vaya a la **documentos** carpeta.  
  
4.  En el **nombre de archivo** cuadro de texto, escriba **Excel de ventas del producto**.  
  
5.  Compruebe que el tipo de archivo es **libro de Excel**.  
  
6.  Haga clic en **Guardar**.  
  
#### <a name="to-view-the-report-in-excel"></a>Ver el informe en Excel.  
  
1.  Abra la **documentos** carpeta y haga doble clic en **ventas del producto.xlsx**.  
  
2.  Compruebe que el nombre de la pestaña del libro es **Excel de Ventas del producto**.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Aquí termina el tutorial sobre la creación de un informe de tabla básico. Para obtener más información, consulte [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales &#40;generador de informes&#41;](report-builder-tutorials.md)   
 [Generador de informes en SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  