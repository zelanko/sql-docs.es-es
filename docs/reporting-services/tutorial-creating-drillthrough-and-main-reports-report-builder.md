---
title: "Tutorial: Crear informes principales (generador de informes) y obtención de detalles | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 7168c8d3-cef5-4c4a-a0bf-fff1ac5b8b71
caps.latest.revision: 14
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 0c67ffbd38887cd9428551a369a4d864d8b972d8
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="tutorial-creating-drillthrough-and-main-reports-report-builder"></a>Tutorial: Crear informes principales y de obtención de detalles (Generador de informes)
En este tutorial se explica cómo crear dos tipos de informes paginados de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] : un informe detallado y un informe principal. Los datos de ventas de ejemplo utilizados en estos informes se recuperan de un cubo de Analysis Services. 

En la siguiente ilustración se muestran los informes que creará y se muestra cómo aparece en el título del informe detallado el valor de campo Games and Toys del informe principal. Los datos del informe detallado pertenecen a la categoría de producto de Games and Toys.  
  
![rs_DrillthroughCubeTutorial](../reporting-services/media/rs-drillthroughcubetutorial.gif "rs_DrillthroughCubeTutorial")  
   
Tiempo estimado para completar este tutorial: 30 minutos.  
  
## <a name="requirements"></a>Requisitos  
Para realizar este tutorial se requiere acceso al cubo de ventas de Contoso para los informes principal y detallado. Este conjunto de datos está formado por el almacenamiento de datos de ContosoDW y la base de datos de procesamiento analítico en línea (OLAP) de Contoso_Retail. Los informes que creará en este tutorial recuperan los datos del informe desde el cubo de ventas de Contoso. La base de datos OLAP de Contoso_Retail se puede descargar desde el [Centro de descarga Microsoft](http://go.microsoft.com/fwlink/?LinkID=191575). Solo necesita descargar el archivo ContosoBIdemoABF.exe. Contiene la base de datos OLAP.  
  
El otro archivo, ContosoBIdemoBAK.exe, es para el almacenamiento de datos de ContosoDW, que no se utiliza en este tutorial.  
  
El sitio web incluye instrucciones de extracción y recuperación del archivo de copia de seguridad ContosoRetail.abf a la base de datos OLAP de Contoso_Retail.  

Debe tener acceso a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en donde instalar la base de datos OLAP.  
    
Para obtener más información sobre los requisitos generales, consulte [Requisitos previos para los tutoriales&#40;Generador de informes&#41;](../reporting-services/prerequisites-for-tutorials-report-builder.md).  
  
## <a name="DMatrixAndDataset"></a>1. Crear un Informe detallado desde el Asistente para tabla o matriz  
En el cuadro de diálogo Introducción, cree un informe de matriz usando el **Asistente para tabla o matriz**. Hay dos modos disponibles en el asistente: diseño de informe y diseño de conjunto de datos compartido. En este tutorial, utilizará el modo de diseño de informe.  
  
#### <a name="to-create-a-new-report"></a>Para crear un informe nuevo  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el equipo, el portal web de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o el modo integrado de SharePoint.  
  
    Se abre el cuadro de diálogo **Nuevo informe o conjunto de datos**.  
  
    Si no ve el cuadro de diálogo **Nuevo informe o conjunto de datos**, vaya al menú **Archivo** > **Nuevo**.  
  
2.  En el panel de la izquierda, compruebe que está seleccionada la opción **Nuevo informe** .  
  
3.  En el panel derecho, compruebe que **Asistente para tabla o matriz** está seleccionado.  
  
## <a name="DConnection"></a>1a. Especificar una conexión de datos  
Una conexión de datos contiene la información necesaria para conectarse a un origen de datos externo, por ejemplo un cubo de Analysis Services o una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para especificar una conexión de datos, puede utilizar un origen de datos compartido del servidor de informes o crear un origen de datos incrustado que solo se utilice en este informe. En este tutorial, utilizará un origen del datos incrustado. Para obtener más información sobre cómo usar orígenes de datos compartidos, vea [Maneras alternativas de obtener una conexión de datos &#40;Generador de informes&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
#### <a name="to-create-an-embedded-data-source"></a>Para crear un origen de datos incrustado  
  
1.  En la página **Elegir un conjunto de datos** , seleccione **Crear un conjunto de datos**y, después, haga clic en **Siguiente**. Se abre la página **Elegir una conexión a un origen de datos** .  
  
2.  Haga clic en **Nueva**. Se abre el cuadro de diálogo **Propiedades del origen de datos** .  
  
3.  En **Nombre**, escriba **Detalle de ventas en línea y por distribuidor** como nombre del origen de datos.  
  
4.  En **Seleccionar un tipo de conexión**, seleccione **Microsoft SQL Server Analysis Services**y, después, haga clic en **Compilar**.  
  
5.  En **Origen de datos**, compruebe que el origen de datos es **Microsoft SQL Server Analysis Services (AdomdClient)**.  
  
6.  En **Nombre del servidor**, escriba el nombre de un servidor donde esté instalada una instancia de Analysis Services.  
  
7.  En la lista **Seleccione o escriba un nombre de base de datos**, seleccione el cubo de Contoso.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Compruebe que **Cadena de conexión** contiene la siguiente sintaxis:  
  
    ```  
    Data Source=<servername>; Initial Catalog = Contoso  
    ```  
  
    `<servername>` es el nombre de una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con Analysis Services instalado.  
  
10. Haga clic en **Tipo de credenciales**.  
  
    > [!NOTE]  
    > Dependiendo de cómo se configuran los permisos en el origen de datos, podría necesitar cambiar las opciones de autenticación predeterminadas. Para más información, vea [Seguridad &#40;Generador de informes&#41;](../reporting-services/report-builder/security-report-builder.md).  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    Se abre la página **Elegir una conexión a un origen de datos**.  
  
12. Para comprobar que se puede conectar al origen de datos, haga clic en **Prueba de conexión**.  
  
    Aparece el mensaje **Conexión creada correctamente** .  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
14. Haga clic en **Siguiente**.  
  
## <a name="DMDXQuery"></a>1b. Crear una consulta MDX  
En un informe puede usar un conjunto de datos compartido que tenga una consulta predefinida o crear un conjunto de datos incrustado para usarlo exclusivamente en ese informe. En este tutorial, creará un conjunto de datos incrustado.  
  
#### <a name="to-create-query-filters"></a>Crear filtros de consulta  
  
1.  En la página **Diseñar una consulta** , en el panel Metadatos, haga clic en el botón **(…)**.  
  
2.  En el cuadro de diálogo **Selección de cubo** , haga clic en Ventas y, después, en **Aceptar**.  
  
    > [!TIP]  
    > Si no desea compilar la consulta MDX manualmente, haga clic en el ![cambiar al modo de diseño](../reporting-services/media/rsqdicon-designmode.gif "Switch to Design mode") icono, alterne el Diseñador de consultas en modo de consulta, pegue el MDX completado al diseñador de consultas y, a continuación, vaya al paso 6 de [para crear el conjunto de datos](#DSkip).  
  
    ```  
    SELECT NON EMPTY { [Measures].[Sales Amount], [Measures].[Sales Return Amount] } ON COLUMNS, NON EMPTY { ([Channel].[Channel Name].[Channel Name].ALLMEMBERS * [Product].[Product Category Name].[Product Category Name].ALLMEMBERS * [Product].[Product Subcategory Name].[Product Subcategory Name].ALLMEMBERS ) } DIMENSION PROPERTIES MEMBER_CAPTION, MEMBER_UNIQUE_NAME ON ROWS FROM ( SELECT ( { [Date].[Calendar Year].&[2009] } ) ON COLUMNS FROM ( SELECT ( { [Sales Territory].[Sales Territory Group].&[North America] } ) ON COLUMNS FROM ( SELECT ( STRTOSET(@ProductProductCategoryName, CONSTRAINED) ) ON COLUMNS FROM ( SELECT ( { [Channel].[Channel Name].&[2], [Channel].[Channel Name].&[4] } ) ON COLUMNS FROM [Sales])))) WHERE ( [Sales Territory].[Sales Territory Group].&[North America], [Date].[Calendar Year].&[2009] ) CELL PROPERTIES VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
    ```  
  
3.  En el panel de Grupo de medida, expanda Canal y, después, arrastre la columna Nombre de canal hasta la columna **Jerarquía** del panel de filtro.  
  
    El nombre de la dimensión, Canal, se agrega automáticamente a la columna **Dimensión** . No cambie las columnas de **Dimensión** u **Operador** .  
  
4.  Para abrir la lista **Filtrar expresión** , haga clic en la flecha abajo en la columna **Filtrar expresión** .  
  
5.  En la lista de expresiones de filtro, expanda **Todos los canales**, haga clic en **En línea**, en **Distribuidor**y, después, en **Aceptar**.  
  
    La consulta incluye ahora un filtro para incluir solo estos canales: En línea y Distribuidor.  
  
6.  Expanda la dimensión Territorio de ventas y arrastre el Grupo del territorio de ventas a la columna **Jerarquía** (bajo **Nombre de canal**).  
  
7.  Abra la lista **Filtrar expresión** , expanda **All Sales Territory**(Todos los territorios de ventas), haga clic en **Norteamérica**y haga clic en **Aceptar**.  
  
    La consulta tiene ahora un filtro para incluir solamente las ventas de Norteamérica  
  
8.  En el panel Grupo de medida, expanda Fecha y, después, arrastre Año natural a la columna **Jerarquía** en el panel de filtro.  
  
    El nombre de la dimensión, Fecha, se agrega automáticamente a la columna **Dimensión** . No cambie las columnas de **Dimensión** u **Operador** .  
  
9. Para abrir la lista **Filtrar expresión** , haga clic en la flecha abajo en la columna **Filtrar expresión** .  
  
10. En la lista de expresiones de filtro, expanda **Todas las fechas**, haga clic en **Año 2009**y, después, haga clic en **Aceptar**.  
  
    La consulta incluye ahora un filtro para incluir solo el año natural 2009.  
  
#### <a name="to-create-the-parameter"></a>Crear el parámetro  
  
1.  Expanda la dimensión Producto y, después, arrastre el miembro Nombre de categoría de producto hasta la columna **Jerarquía** , bajo **Año natural**.  
  
2.  Abra la lista **Expresión de filtro** , haga clic en **Todos los productos**y, después, haga clic en **Aceptar**.  
  
3.  Active la casilla **Parámetro** . La consulta incluye ahora el parámetro ProductProductCategoryName.  
  
    > [!NOTE]  
    > El parámetro contiene los nombres de categorías de producto. Al hacer clic en el informe principal en un nombre de categoría de producto, su nombre se pasa al informe detallado utilizando este parámetro.  
  
### <a name="DSkip"></a>Crear el conjunto de datos  
  
1.  Desde la dimensión Canal, arrastre Nombre de canal hasta el panel de datos.  
  
2.  Desde la dimensión Producto, arrastre Nombre de categoría de producto hasta el panel de datos y, después, colóquelo a la derecha de Nombre del canal.  
  
3.  Desde la dimensión Producto, arrastre Product Subcategory Name (Nombre de subcategoría de producto) hasta el panel de datos y, después, colóquelo a la derecha de Nombre de categoría de producto.  
  
4.  En el panel Metadatos, expanda **Medida**y, después, expanda Ventas.  
  
5.  Arrastre la medida Importe de venta hasta el panel de datos y, después, colóquela a la derecha de Product Subcategory Name (Nombre de subcategoría de producto).  
  
6.  En la barra de herramientas del diseñador de consultas, haga clic en **Ejecutar (!)**.  
  
7.  Haga clic en **Siguiente**.  
  
## <a name="DLayout"></a>1c. Organizar los datos en grupos  
Al seleccionar los campos por los que desea agrupar los datos, diseñe una matriz con filas y columnas que muestre datos detallados y datos agregados.  
  
#### <a name="to-organize-data-into-groups"></a>Para organizar los datos en grupos  
  
1.  Para cambiar a la vista de diseño, haga clic en **Diseño**.  
  
2.  En la página **Organizar campos** , arrastre Product_Subcategory_Name a **Grupos de filas**.  
  
    > [!NOTE]  
    > Los espacios en los nombres se reemplazan con caracteres de subrayado (_). Por ejemplo, Nombre de categoría de producto (Product Category Name) es Product_Category_Name.  
  
3.  Arrastre Channel_Name a **Grupos de columnas**.  
  
4.  Arrastre Sales_Amount a **Valores**.  
  
    Sales_Amount se agrega automáticamente mediante la función Sum, que es el agregado predeterminado para los campos numéricos. El valor es `[Sum(Sales_Amount)]`.  
  
    Puede abrir la lista desplegable Para ver las demás funciones de agregado disponibles, abra la lista desplegable (no cambie la función de agregado).  
  
5.  Arrastre Sales_Return_Amount hacia **Valores**y, después, colóquelo bajo `[Sum(Sales_Amount)]`.  
  
    Los pasos 4 y 5 especifican los datos que deben aparecer en la matriz.  
  
6.  Haga clic en **Siguiente**.  
  
## <a name="DTotals"></a>1d. Agregar subtotales y totales  
Después de crear grupos, puede agregar filas y darles formato, donde se mostrarán los valores agregados para los campos. Puede decidir también si mostrar todos los datos o permitir que los usuarios expandan y contraigan de forma interactiva los datos agrupados.  
  
#### <a name="to-add-subtotals-and-totals"></a>Para agregar subtotales y totales  
  
1.  En la página **Elegir el diseño** , en **Opciones**, compruebe que esté seleccionada la opción **Mostrar subtotales y totales generales** .  
  
    El panel Vista previa del asistente muestra una matriz con cuatro filas.  
  
2.  Haga clic en **Siguiente**.  
  
2.  Haga clic en **Finalizar**.  
  
    La tabla se agrega a la superficie de diseño.  
  
3.  Haga clic en **Ejecutar (!)**para obtener la vista previa del informe.  
  
## <a name="DFormat"></a>2. Dar formato a los datos como moneda  
Aplique el formato de moneda a los campos de cantidad de ventas en el informe detallado.  
  
#### <a name="to-format-data-as-currency"></a>Dar formato a los datos como moneda  
  
1.  Para cambiar a la vista de diseño, haga clic en **Diseño**.  
  
2.  Para seleccionar y dar formato una vez a varias celdas, presione la tecla Ctrl y, a continuación, seleccione las celdas que contienen los datos de ventas numéricos.  
  
3.  En la pestaña **Inicio** , en el grupo **Número** , haga clic en el botón **Moneda**.  
  
## <a name="DSparkline"></a>3. Agregar columnas para mostrar valores de ventas en minigráficos  
En lugar de mostrar de ventas y retornos de ventas como valores de moneda, el informe muestra los valores en un minigráfico.  
  
#### <a name="to-add-sparklines-to-columns"></a>Para agregar minigráficos a las columnas  
  
1.  Para cambiar a la vista de diseño, haga clic en **Diseño**.  
  
2.  En el grupo Total de la matriz, Haga clic con el botón derecho en la columna **Importe de venta** , haga clic en **Insertar Columna**y, después, en **Derecha**.  
  
    Se agrega una columna vacía a la derecha de **Importe de venta**.  
  
3.  En la cinta de opciones, haga clic en **Rectángulo**y, después, haga clic en la celda vacía situada a la derecha de la celda `[Sum(Sales_Amount)]` en el grupo de filas [Product_Subcategory].  
  
4.  En la cinta de opciones, haga clic en el icono **Minigráficos** y, después, haga clic en la celda donde se agregó el rectángulo.  
  
5.  En el cuadro de diálogo **Seleccionar tipo de minigráfico** , compruebe que está seleccionado el tipo **Columna** .  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
7.  Haga clic con el botón secundario en el minigráfico.  
  
8.  En el panel Datos del gráfico, haga clic en el icono **Agregar campo** y, después, haga clic en Sales_Amount.  
  
9. Haga clic con el botón secundario en la columna `Sales_Return_Amount` y, a continuación, agregue una columna a la derecha.  
  
10. Repita los pasos del 2 al 6.  
  
11. Haga clic con el botón secundario en el minigráfico.  
  
12. En el panel Datos del gráfico, haga clic en el icono **Agregar campo** y, después, haga clic en Sales_Return_Amount.  
  
13. Haga clic en **Ejecutar**para obtener la vista previa del informe.  
  
## <a name="DReportTitle"></a>4. Agregar el título de informe con el nombre de categoría del producto  
Los títulos de informe aparecen en la parte superior. Puede situar el título del informe en un encabezado de informe o, si el informe no lo utiliza, en un cuadro de texto en la parte superior del cuerpo del informe. En este tutorial, deberá utilizar el cuadro de texto que se coloca automáticamente en la parte superior del cuerpo del informe.  
  
#### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  Para cambiar a la vista de diseño, haga clic en **Diseño**.  
  
2.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
3.  Escriba **Ventas y devoluciones por categoría:**.  
  
4.  Haga clic con el botón derecho y, después, haga clic en **Crear marcador de posición**.  
  
5.  Haga clic en el botón **(fx)** , a la derecha de la lista **Valor** .  
  
6.  En el cuadro de diálogo **Expresión** , en el panel Categoría, haga clic en **Conjunto de datos**y, después, haga doble clic en **en la lista** Valores `First(Product_Category_Name)`.  
  
    El cuadro **Expresión** contiene la siguiente expresión:  
  
    ```  
    =First(Fields!Product_Category_Name.Value, "DataSet1")  
    ```  
  
7.  Haga clic en **Ejecutar**para obtener la vista previa del informe.  
  
El título del informe incluye el nombre de la primera categoría de producto. Después, tras ejecutar este informe como un informe detallado, el nombre de la categoría de producto cambiará dinámicamente, para reflejar el nombre de la categoría de producto en la que se hizo clic en el informe principal.  
  
## <a name="DParameter"></a>5. Actualizar las propiedades de parámetro  
De forma predeterminada los parámetros están visibles, lo que no es adecuado para este informe. Actualizará las propiedades de parámetro para el informe detallado.  
  
#### <a name="to-hide-a-parameter"></a>Ocultar un parámetro  
  
1.  En el panel Datos de informe, expanda **Parámetros**.  
  
2.  Haga clic con el botón derecho en @ProductProductCategoryNamey, después, haga clic en **Propiedades de parámetro**.  
  
    > [!NOTE]  
    > El el carácter @ situado al lado del nombre indica que se trata de un parámetro.  
  
3.  En la pestaña **General** , haga clic en **Oculto**.  
  
4.  En el cuadro **Pedir datos** , escriba **Categoría de producto**.  
  
    > [!NOTE]  
    > Dado que se oculta el parámetro, nunca se utiliza esta petición.  
  
5.  Opcionalmente, haga clic en **Valores disponibles** y en **Valores predeterminados** para revisar sus opciones. No cambie ninguna opción en estas pestañas.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="DSave"></a>6. Guardar el informe en una biblioteca de SharePoint  
Puede guardar el informe en una biblioteca de SharePoint, en un servidor de informes o en su equipo. Si guarda el informe en su equipo, no estarán disponibles varias características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , como elementos de informe y subinformes, no estarán disponibles. En este tutorial guardará el informe en una biblioteca de SharePoint.  
  
#### <a name="to-save-the-report"></a>Para guardar el informe  
  
1.  Desde el botón Generador de informes, haga clic en **Guardar**. Se abre el cuadro de diálogo **Guardar como informe** .  
  
    > [!NOTE]  
    > Si vuelve a guardar un informe, automáticamente se guarda en su ubicación anterior. Para cambiar la ubicación, use la opción **Guardar como** .  
  
2.  Para mostrar una lista de servidores de informes y sitios de SharePoint usados recientemente, haga clic en **Sitios y servidores recientes**.  
  
3.  Seleccione o escriba el nombre del sitio de SharePoint donde tiene el permiso para guardar los informes.  
  
    La URL de la biblioteca de SharePoint tiene la siguiente sintaxis:  
  
    ```  
    Http://<ServerName>/<Sites>/  
    ```  
  
4.  Haga clic en **Guardar**.  
  
    En**Sitios y servidores recientes** se enumeran las bibliotecas del sitio de SharePoint.  
  
5.  Navegue hasta la biblioteca donde guardará el informe.  
  
6.  En el cuadro **Nombre** , reemplace el nombre predeterminado por **ResellerVSOnlineDrillthrough**.  
  
    > [!NOTE]  
    > Guardará el informe principal en la misma ubicación. Si quiere guardar los informes detallados y principal en sitios o bibliotecas diferentes, debe actualizar la ruta de acceso de la acción **Ir a informe** en el informe principal.  
  
7.  Haga clic en **Guardar**.  
  
## <a name="MMatrixAndDataset"></a>1. Crear el informe principal desde el Asistente para tabla o matriz  
En el cuadro de diálogo **Introducción**, cree un informe de matriz usando el **Asistente para tabla o matriz**.  
  
#### <a name="to-create-the-main-report"></a>Para crear el informe principal  
  
1.  [Inicie el Generador de informes](../reporting-services/report-builder/start-report-builder.md) desde el equipo, el portal web de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] o el modo integrado de SharePoint.  
  
    Se abre el cuadro de diálogo **Nuevo informe o conjunto de datos**.  
  
    Si no ve el cuadro de diálogo **Nuevo informe o conjunto de datos**, vaya al menú **Archivo** > **Nuevo**.  
 
2.  En el cuadro de diálogo **Introducción** , compruebe que está seleccionado **Nuevo informe** y, después, haga clic en **Asistente para tabla o matriz**.  
  
## <a name="MConnection"></a>1a. Especificar una conexión de datos  
Agregará un origen de datos incrustados al informe principal.  
  
#### <a name="to-create-an-embedded-data-source"></a>Para crear un origen de datos incrustado  
  
1.  En la página **Elegir un conjunto de datos** , seleccione **Crear un conjunto de datos**y, después, haga clic en **Siguiente**.  
  
2.  Haga clic en **Nueva**.  
  
3.  En **Nombre**, escriba **Ventas principales en línea y de distribuidor** como el nombre del origen de datos.  
  
4.  En **Seleccionar un tipo de conexión**, seleccione **Microsoft SQL Server Analysis Services**y, después, haga clic en **Compilar**.  
  
5.  En **Origen de datos**, compruebe que el origen de datos es **Microsoft SQL Server Analysis Services (AdomdClient)**.  
  
6.  En **Nombre del servidor**, escriba el nombre de un servidor donde esté instalada una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
7.  En la lista **Seleccione o escriba un nombre de base de datos**, seleccione el cubo de Contoso.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
9. Compruebe que la **Cadena de conexión** contiene la siguiente sintaxis:  
  
    ```  
    Data Source=<servername>; Initial Catalog = Contoso  
    ```  
  
10. Haga clic en **Tipo de credenciales**.  
  
    Dependiendo de cómo se configuran los permisos en el origen de datos, podría necesitar cambiar la autenticación predeterminada.  
  
11. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
12. Para comprobar que se puede conectar al origen de datos, haga clic en **Prueba de conexión**.  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
14. Haga clic en **Siguiente**.  
  
## <a name="MMDXQuery"></a>1b. Crear una consulta MDX  
Después, cree un conjunto de datos incrustado. Para esto, utilizará el diseñador de consultas para crear filtros, parámetros y miembros calculados, así como el propio conjunto de datos.  
  
#### <a name="to-create-query-filters"></a>Crear filtros de consulta  
  
1.  En la página **Diseñar una consulta** , en la sección de cubo del panel Metadatos, haga clic en el botón de puntos suspensivos **(…)**.  
  
2.  En el cuadro de diálogo **Selección de cubo** , haga clic en Ventas y, después, en **Aceptar**.  
  
    > [!TIP]  
    > Si no desea compilar la consulta MDX manualmente, haga clic en el ![cambiar al modo de diseño](../reporting-services/media/rsqdicon-designmode.gif "Switch to Design mode") icono, alterne el Diseñador de consultas en modo de consulta, pegue el MDX completado al diseñador de consultas y, a continuación, vaya al paso 5 de [para crear el conjunto de datos](#MSkip).  
  
    ```  
    WITH MEMBER [Measures].[Net QTY] AS [Measures].[Sales Quantity] -[Measures].[Sales Return Quantity] MEMBER [Measures].[Net Sales] AS [Measures].[Sales Amount] - [Measures].[Sales Return Amount] SELECT NON EMPTY { [Measures].[Net QTY], [Measures].[Net Sales] } ON COLUMNS, NON EMPTY { ([Channel].[Channel Name].[Channel Name].ALLMEMBERS * [Product].[Product Category Name].[Product Category Name].ALLMEMBERS ) } DIMENSION PROPERTIES MEMBER_CAPTION, MEMBER_UNIQUE_NAME ON ROWS FROM ( SELECT ( { [Date].[Calendar Year].&[2009] } ) ON COLUMNS FROM ( SELECT ( STRTOSET(@ProductProductCategoryName, CONSTRAINED) ) ON COLUMNS FROM ( SELECT ( { [Sales Territory].[Sales Territory Group].&[North America] } ) ON COLUMNS FROM ( SELECT ( { [Channel].[Channel Name].&[2], [Channel].[Channel Name].&[4] } ) ON COLUMNS FROM [Sales])))) WHERE ( [Sales Territory].[Sales Territory Group].&[North America], [Date].[Calendar Year].&[2009] ) CELL PROPERTIES VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGSQuery text: Code.  
    ```  
  
3.  En el panel de Grupo de medida, expanda Canal y, después, arrastre la columna Nombre de canal hasta la columna **Jerarquía** del panel de filtro.  
  
    El nombre de la dimensión, Canal, se agrega automáticamente a la columna **Dimensión** . No cambie las columnas de **Dimensión** u **Operador** .  
  
4.  Para abrir la lista **Filtrar expresión** , haga clic en la flecha abajo en la columna **Filtrar expresión** .  
  
5.  En la lista de expresiones de filtro, expanda **Todos los canales**, haga clic en **En línea** y en **Distribuidor**y, después, en **Aceptar**.  
  
    La consulta incluye ahora un filtro para incluir solo estos canales: En línea y Distribuidor.  
  
6.  Expanda la dimensión Territorio de ventas y arrastre el Grupo del territorio de ventas a la columna **Jerarquía** (bajo **Nombre de canal**).  
  
7.  Abra la lista **Filtrar expresión** , expanda **All Sales Territory**(Todos los territorios de ventas), haga clic en **Norteamérica**y haga clic en **Aceptar**.  
  
    La consulta tiene ahora un filtro para incluir solamente las ventas de Norteamérica  
  
8.  En el panel Grupo de medida, expanda Fecha y, después, arrastre Año natural a la columna **Jerarquía** en el panel de filtro.  
  
    El nombre de la dimensión, Fecha, se agrega automáticamente a la columna **Dimensión** . No cambie las columnas de **Dimensión** u **Operador** .  
  
9. Para abrir la lista **Filtrar expresión** , haga clic en la flecha abajo en la columna **Filtrar expresión** .  
  
10. En la lista de expresiones de filtro, expanda **Todas las fechas**, haga clic en **Año 2009**y, después, haga clic en **Aceptar**.  
  
    La consulta incluye ahora un filtro para incluir solo el año natural 2009.  
  
#### <a name="to-create-the-parameter"></a>Crear el parámetro  
  
1.  Expanda la dimensión Producto y, después, arrastre el miembro Nombre de categoría de producto hasta la columna **Jerarquía** , bajo **Grupo del territorio de ventas**.  
  
2.  Abra la lista **Expresión de filtro** , haga clic en **Todos los productos**y, después, haga clic en **Aceptar**.  
  
3.  Active la casilla **Parámetro** . La consulta incluye ahora el parámetro ProductProductCategoryName.  
  
#### <a name="to-create-calculated-members"></a>Crear miembros calculados  
  
1.  Coloque el cursor dentro del panel Miembros calculados, haga clic con el botón derecho y, después, haga clic en **Nuevo miembro calculado**.  
  
2.  En el panel Metadatos, expanda **Medidas** y, después, expanda Ventas.  
  
3.  Arrastre la medida Sales Quantity al cuadro **Expresión** , escriba el carácter de resta (-) y, después, arrastre la medida Sales Return Quantity al cuadro **Expresión** ; colóquela después del carácter de resta.  
  
    El siguiente código muestra la expresión:  
  
    ```  
    [Measures].[Sales Quantity] - [Measures].[Sales Return Quantity]  
    ```  
  
4.  En el cuadro Nombre, escriba **Net QTY**y haga clic en **Aceptar**.  
  
    En el panel Miembros calculados se muestra el miembro calculado **Net QTY** .  
  
5.  Haga clic con el botón derecho en **Miembros calculados**y, después, haga clic en **Nuevo miembro calculado**.  
  
6.  En el panel Metadatos, expanda **Medidas**y, después, expanda Ventas.  
  
7.  Arrastre la medida Sales Amount al cuadro **Expresión** , escriba el carácter de resta (-) y, después, arrastre la medida Sales Return Amount al cuadro **Expresión** ; colóquela después del carácter de resta.  
  
    El siguiente código muestra la expresión:  
  
    ```  
    [Measures].[Sales Amount] - [Measures].[Sales Return Amount]  
    ```  
  
8.  En el cuadro **Nombre** , escriba  **Ventas netas**y, después, haga clic en **Aceptar**. En el panel Miembros calculados se muestra el miembro calculado **Ventas netas** .  
  
### <a name="MSkip"></a>Crear el conjunto de datos  
  
1.  Desde la dimensión Canal, arrastre Nombre de canal hasta el panel de datos.  
  
2.  Desde la dimensión Producto, arrastre Nombre de categoría de producto hasta el panel de datos y, después, colóquelo a la derecha de Nombre del canal.  
  
3.  Desde **Miembros calculados**, arrastre `Net QTY` al panel de datos y colóquelo a la derecha de Nombre de categoría de producto.  
  
4.  Desde Miembros calculados, arrastre Ventas netas al panel de datos y colóquelo a la derecha de `Net QTY`.  
  
5.  En la barra de herramientas del diseñador de consultas, haga clic en **Ejecutar (!)**.  
  
    Revise el conjunto de resultados de la consulta.  
  
6.  Haga clic en **Siguiente**.  
  
## <a name="MLayout"></a>1c. Organizar los datos en grupos  
Al seleccionar los campos por los que desea agrupar los datos, diseñe una matriz con filas y columnas que muestre datos detallados y datos agregados.  
  
#### <a name="to-organize-data-into-groups"></a>Para organizar los datos en grupos  
  
1.  En la página **Organizar campos** , arrastre Product_Category_Name a **Grupos de filas**.  
  
2.  Arrastre Channel_Name a **Grupos de columnas**.  
  
3.  Arrastre `Net_QTY` a **Valores**.  
  
    `Net_QTY` se suma automáticamente mediante la función Sum, que es el agregado predeterminado para los campos numéricos. El valor es `[Sum(Net_QTY)]`.  
  
    Para ver las demás funciones de agregado disponibles abra la lista desplegable . No cambie la función de agregado.  
  
4.  Arrastre `Net_Sales_Return` a **Valores** y después colóquelo bajo `[Sum(Net_QTY)]`.  
  
    Los pasos 3 y 4 especifican los datos que deben mostrarse en la matriz.  
  
## <a name="MTotals"></a>1d. Agregar subtotales y totales  
Puede mostrar subtotales y totales generales en informes. Los datos del informe principal muestran como un indicador; quitará el total general cuando complete el asistente.  
  
#### <a name="to-add-subtotals-and-grand-totals"></a>Agregar subtotales y totales generales  
  
1.  En la página **Elegir el diseño** , en **Opciones**, compruebe que esté seleccionada la opción **Mostrar subtotales y totales generales** .  
  
    El panel Vista previa del asistente muestra una matriz con cuatro filas.  Al ejecutar el informe, cada fila se mostrará de la siguiente manera: la primera fila es el grupo de columnas, la segunda fila contiene los encabezados de columna, la tercera fila contiene los datos de la categoría de producto (`[Sum(Net_ QTY)]` y `[Sum(Net_Sales)]`y la fila cuarta contiene los totales.  
  
2.  Haga clic en **Siguiente**.  
  
3.  Haga clic en **Finalizar**.  
  
3.  Haga clic en **Ejecutar**para obtener la vista previa del informe.  
  
## <a name="MGrandTotal"></a>2. Quitar la fila Total general  
Los valores de datos se muestran como estados del indictor, incluyendo los totales del grupo de columna. Quite la fila que muestra el total general.  
  
#### <a name="to-remove-the-grand-total-row"></a>Quitar la fila del total general  
  
1.  Para cambiar a la vista de diseño, haga clic en **Diseño**.  
  
2.  Haga clic en la fila Total (la última fila de la matriz), haga clic con el botón derecho y, después, haga clic en **Eliminar filas**.  
  
3.  Haga clic en **Ejecutar**para obtener la vista previa del informe.  
  
## <a name="MDrillthrough"></a>3. Configurar la acción del cuadro de texto para la obtención de detalles  
Para habilitar la obtención de detalles, especifique una acción en un cuadro de texto en el informe principal.  
  
#### <a name="to-enable-an-action"></a>Habilitar una acción  
  
1.  Para cambiar a la vista de diseño, haga clic en **Diseño**.  
  
2.  Haga clic con el botón derecho en la celda que contiene Product_Category_Name y, después, haga clic en **Propiedades de cuadro de texto**.  
  
3.  Haga clic en la pestaña **Acción** .  
  
4.  Seleccione **Ir a informe**.  
  
5.  En **Especificar un informe**, haga clic en **Examinar**y, después, ubique el informe detallado denominado ResellerVSOnlineDrillthrough.  
  
6.  Agregue un nuevo parámetro para pasárselo al informe detallado y haga clic en **Agregar**.  
  
7.  En la lista **Nombre** , seleccione ProductProductCategoryName.  
  
8.  En **Valor**, escriba `[Product_Category_Name.UniqueName]`.  
  
    Product_Category_Name es un campo del conjunto de datos.  
  
    > [!IMPORTANT]  
    > Debe incluir la propiedad **UniqueName** porque la acción de obtención de detalles requiere un valor único.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-format-the-drillthrough-field"></a>Dar formato al campo de obtención de detalles  
  
1.  Haga clic con el botón derecho en la celda que contiene `Product_Category_Name`y, después, haga clic en **Propiedades de cuadro de texto**.  
  
2.  Haga clic en la pestaña **Fuente** .  
  
3.  En la lista **Efectos** , seleccione **Subrayado**.  
  
4.  En la lista **Color** , seleccione **Azul**.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
6.  Para obtener una vista previa de un informe, haga clic en **Ejecutar**.  
  
Los nombres de la categoría de producto tienen el formato de vínculo común (azul y subrayado).  
  
## <a name="MIndicators"></a>4. Reemplazar los valores numérico por indicadores  
Utilice los indicadores para mostrar el estado de cantidades y ventas para los canales En línea y Distribuidor.  
  
#### <a name="to-add-an-indicator-for-net-qty-values"></a>Agregar un indicador para los valores Net QTY  
  
1.  Para cambiar a la vista de diseño, haga clic en **Diseño**.  
  
2.  En la cinta de opciones, haga clic en el icono **Rectángulo** y, después, haga clic en la celda `[Sum(Net QTY)]` del grupo de filas `[Product_Category_Name]` del grupo de columnas `Channel_Name` .  
  
3.  En la cinta de opciones, haga clic en el icono **Indicador** y, después, haga clic dentro del rectángulo. El cuadro de diálogo **Seleccionar tipo de indicador** se abre con el indicador **Direccional** seleccionado.  
  
4.  Escriba el tipo **3 Señales** y haga clic en **Aceptar**.  
  
5.  Haga clic con el botón derecho en el indicador y en el panel de Datos del medidor, haga clic en la flecha abajo situada junto a **(No especificado)**. Seleccione `Net_QTY`.  
  
6.  Repita los pasos del 2 al 5 para la celda `[Sum(Net QTY)]` del grupo de filas `[Product_Category_Name]` dentro de **Total**.  
  
#### <a name="to-add-an-indicator-for-net-sales-values"></a>Agregar un indicador para los valores Net Sales  
  
1.  En la cinta de opciones, haga clic en el icono **Rectángulo** y, después, haga clic dentro de la celda `[Sum(Net_Sales)]` del grupo de filas `[Product_Category_Name]` del grupo de columnas `Channel_Name` .  
  
2.  En la cinta de opciones, haga clic en el icono **Indicador** y, después, haga clic dentro del rectángulo.  
  
3.  Escriba el tipo **3 Señales** y haga clic en **Aceptar**.  
  
4.  Haga clic con el botón derecho en el indicador y en el panel de Datos del medidor, haga clic en la flecha abajo situada junto a **(No especificado)**. Seleccione `Net_Sales`.  
  
5.  Repita los pasos del 1 al 4 para la celda `[Sum(Net_Sales)]` del grupo de filas `[Product_Category_Name]` dentro de **Total**.  
  
6.  Para obtener una vista previa de un informe, haga clic en **Ejecutar**.  
  
## <a name="MParameter"></a>5. Actualizar las propiedades de parámetro  
De forma predeterminada, los parámetros están visibles, lo que no es adecuado para este informe. Actualizará las propiedades de parámetro para hacer el parámetro interno.  
  
#### <a name="to-make-the-parameter-internal"></a>Realizar el parámetro interno  
  
1.  En el panel Datos de informe, expanda **Parámetros**.  
  
2.  Haga clic con el botón derecho en `@ProductProductCategoryName,` y, después, haga clic en **Propiedades de parámetro**.  
  
3.  En la pestaña **General** , haga clic en **Interno**.  
  
4.  Opcionalmente, haga clic en las pestañas **Valores disponibles** y **Valores predeterminados** para revisar sus opciones. No cambie ninguna opción en estas pestañas.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="MTitle"></a>6. Agregar un título de informe  
Agregar un título al informe principal.  
  
#### <a name="to-add-a-report-title"></a>Para agregar un título de informe  
  
1.  En la superficie de diseño, haga clic en **Haga clic para agregar título**.  
  
2.  Escriba **Ventas por categoría de producto de 2009: categoría En línea y Distribuidor**.  
  
3.  Seleccione el texto que escribió.  
  
4.  En la pestaña **Inicio** de la cinta de opciones, en el grupo Fuentes, seleccione la fuente **Times New Roman** , tamaño **16 pt** , y los estilos **negrita** y **cursiva** Cinta de opciones.  
  
5.  Para obtener una vista previa de un informe, haga clic en **Ejecutar**.  
  
## <a name="MSave"></a>7. Guardar el informe principal en una biblioteca de SharePoint  
Guarde el informe principal en una biblioteca de SharePoint  
  
#### <a name="to-save-the-report"></a>Para guardar el informe  
  
1.  Para cambiar a la vista de diseño, haga clic en **Diseño**.  
  
2.  Desde el botón Generador de informes, haga clic en **Guardar**.  
  
3.  Si quiere mostrar una lista de servidores de informes y sitios de SharePoint usados recientemente, puede hacer clic en **Sitios y servidores recientes**.  
  
4.  Seleccione o escriba el nombre del sitio de SharePoint donde tiene el permiso para guardar los informes. La URL de la biblioteca de SharePoint tiene la siguiente sintaxis:  
  
    ```  
    Http://<ServerName>/<Sites>/  
    ```  
  
5.  Navegue hasta la biblioteca donde quieren guardar el informe.  
  
6.  En **Nombre**, reemplace el nombre predeterminado por **ResellerVSOnlineMain**.  
  
    > [!IMPORTANT]  
    > Guarde el informe principal en la misma ubicación donde guardó el informe detallado. Para guardar los informes detallados y principal en sitios o bibliotecas diferentes, confirme que la acción **Ir a informe** del informe principal señala a la ubicación correcta del informe detallado.  
  
7.  Haga clic en **Guardar**.  
  
## <a name="MRunReports"></a>8. Ejecutar los informes principal y detallado  
Ejecute el informe principal y, a continuación, haga clic en los valores de la columna de categoría de producto para ejecutar el informe detallado.  
  
#### <a name="to-run-the-reports"></a>Para ejecutar los informes  
  
1.  Abra la biblioteca de SharePoint donde los informes están guardados.  
  
2.  Haga doble clic en ResellerVSOnlineMain.  
  
    El informe se ejecuta y muestra la información de ventas de la categoría de producto.  
  
3.  Haga clic en el vínculo **Games and Toys** de la columna que contiene los nombres de categoría de producto.  
  
    Se ejecuta el informe detallados, mostrando solo los valores para la categoría de producto Games and Toys.  
  
4.  Para volver al informe principal, haga clic en el botón atrás de Internet Explorer.  
  
5.  Opcionalmente, explore otras categorías de producto haciendo clic en sus nombres.  
  
## <a name="see-also"></a>Vea también  
[Tutoriales del Generador de informes](../reporting-services/report-builder-tutorials.md)  
  

