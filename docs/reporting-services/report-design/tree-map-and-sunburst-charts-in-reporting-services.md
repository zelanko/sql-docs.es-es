---
title: "Gráficos de rectángulos y de proyección solar en Reporting Services | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/31/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12307c8f-bca7-4d21-8ad5-0c07d819865b
caps.latest.revision: 17
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e09afe4634c02db6e74413e7c1c10565450b3559
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="tree-map-and-sunburst-charts-in-reporting-services"></a>Gráficos de rectángulos y de proyección solar en Reporting Services
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

  Las visualizaciones de rectángulos y proyección solar de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] resultan excepcionales para representar visualmente datos jerárquicos.   En este tema se describe cómo agregar un gráfico de rectángulos o de proyección solar a un informe de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Aquí también encontrará una consulta de AdventureWorks de ejemplo para ayudarlo a ponerse manos a la obra.  
  
##  <a name="bkmk_treemap_chart"></a> Gráfico de rectángulos  
 ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
  
 Un gráfico de rectángulos divide el área del gráfico en los rectángulos que representan los diferentes niveles y tamaños relativos de la jerarquía de datos. La distribución se asemeja a las ramas de un árbol, que parten de un tronco y se dividen en ramas cada vez más pequeñas. Cada rectángulo se divide en rectángulos más pequeños que representan el siguiente nivel en la jerarquía. Los rectángulos de nivel superior del gráfico se ordenan de forma que el rectángulo más grande quede en la esquina superior izquierda y el más pequeño, en la inferior derecha.  Dentro de cada rectángulo, el siguiente nivel del más alto también se organiza con rectángulos en la misma distribución, de la esquina superior izquierda a la inferior derecha.  
  
 Por ejemplo, en la siguiente imagen del gráfico de rectángulos de ejemplo, el territorio del suroeste de EE. UU. es el más grande y Alemania es el más pequeño. En el suroeste de EE. UU., las bicicletas de carretera se han vendido más que las de montaña.  
  
 ![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-tree-map-chart-and-configure-for-the-sample-adventureworks-data"></a>Para insertar un gráfico de rectángulos y configurarlo con los datos de AdventureWorks de ejemplo, siga estos pasos:  
 **Nota:** Antes de agregar un gráfico al informe, crear un origen y un conjunto de datos.  Para obtener una consulta y datos de ejemplo, consulte la sección [Datos de ejemplo de AdventureWorks](#bkmk_sample_data) de este tema.  
  
1.  Haga clic con el botón derecho en la superficie de diseño y seleccione **Insertar**y, después, **Gráfico** .  
  
     Seleccione el gráfico de rectángulos ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon").  
  
     ![ssrs_insert_treemap_sunburst](../../reporting-services/report-design/media/ssrs-insert-treemap-sunburst.png "ssrs_insert_treemap_sunburst")  
  
2.  Cambie la posición y el tamaño del gráfico.   Para utilizarlo con los datos de ejemplo, puede empezar con un gráfico de 5 pulgadas de ancho.  
  
3.  Agregue los siguientes campos de los datos de ejemplo:  
  
    |||  
    |-|-|  
    |![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")|**Valores:** LineTotal<br /><br /> **Grupos de categorías:** agréguelos en el siguiente orden:<br /><br /> 1) CategoryName<br /><br /> 2) SubcategoryName<br /><br /> **Grupos de series:** TerritoryName|  
  
4.  Si desea optimizar el tamaño de página para la forma general de un gráfico de rectángulos, establezca la posición de la leyenda en la parte inferior.  
  
5.  Para agregar información sobre herramientas en la que se muestre la subcategoría y el total de línea, haga clic con el botón derecho en **LineTotal** y, después, en **Propiedades de la serie**.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     Establezca la propiedad **Información sobre herramientas** en la siguiente cadena:  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
     Para obtener más información, vea [Mostrar la información sobre herramientas en una serie &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  Cambie el título predeterminado del gráfico a "Ventas categorizadas por territorio".  
  
7.  El número de valores de etiqueta que se muestran viene determinado por el tamaño de la fuente, del área general del gráfico y de los rectángulos específicos.  Para ver más etiquetas, cambie la propiedad Fuente de etiqueta de LineTotal a 10 pt en lugar del valor predeterminado de 8 pt.  
  
  
##  <a name="bkmk_sunburst_chart"></a> Gráfico de proyección solar  
 ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
 En un gráfico de proyección solar, la jerarquía se representa a mediante una serie de círculos; el nivel más alto de la jerarquía se muestra en el centro y los inferiores se visualizan como anillos colocados fuera del centro.  El nivel más bajo de la jerarquía es el anillo exterior.  
  
 ![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-configure-for-the-sample-adventureworks-data"></a>Para insertar un gráfico de proyección solar y configurarlo con los datos de AdventureWorks de ejemplo, siga estos pasos:  
 **Nota:** Antes de agregar un gráfico al informe, crear un origen y un conjunto de datos.  Para obtener una consulta y datos de ejemplo, consulte la sección [Datos de ejemplo de AdventureWorks](#bkmk_sample_data) de este tema.  
  
1.  Haga clic con el botón derecho en la superficie de diseño y seleccione **Insertar**y, después, **Gráfico** .  
  
     Seleccione el gráfico de proyección solar ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon").  
  
     ![ssrs_insert_treemap_sunburst](../../reporting-services/report-design/media/ssrs-insert-treemap-sunburst.png "ssrs_insert_treemap_sunburst")  
  
2.  Cambie la posición y el tamaño del gráfico.   Para utilizarlo con los datos de ejemplo, puede empezar con un gráfico de 5 pulgadas de ancho.  
  
3.  Agregue los siguientes campos de los datos de ejemplo:  
  
    |||  
    |-|-|  
    |![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")|**Valores:** LineTotal<br /><br /> **Grupos de categorías:** agréguelos en el siguiente orden:<br /><br /> 1) CategoryName<br /><br /> 2) SubcategoryName<br /><br /> 3) SalesReasonName<br /><br /> **Grupos de series:** TerritoryName|  
  
4.  Si desea optimizar el tamaño de página para la forma general de un gráfico de proyección solar, establezca la posición de la leyenda en la parte inferior.  
  
5.  Cambie el título predeterminado del gráfico a "Ventas categorizadas por territorio, con motivo de venta".  
  
6.  |||  
    |-|-|  
    |![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")|Para agregar los valores de los grupos de categorías al gráfico de proyección solar como etiquetas, establezca la propiedad de etiqueta **Visible** en True y **UseValueAsLabel**en False.<br /><br /> Los valores de etiqueta que se muestran vienen determinados por el tamaño de la fuente, del área general del gráfico y de los rectángulos específicos.  Para ver más etiquetas, cambie la propiedad Fuente de etiqueta de LineTotal a 8 pt en lugar del valor predeterminado de 10 pt.|  
  
7.  Si desea utilizar una gama de colores distinta, cambie la propiedad **Paleta** del gráfico.  
  
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a> Datos de ejemplo de AdventureWorks  
 En esta sección se incluye una consulta de ejemplo y los pasos básicos para crear un origen y un conjunto de datos en [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]. Si el informe ya contiene un origen y un conjunto de datos, puede omitir esta sección.  
  
 La consulta devuelve los datos detallados de los pedidos de venta de AdventureWorks con la información sobre el territorio de ventas, la categoría del producto, la subcategoría del producto y los motivos de la venta.  
  
1.  **Obtener los datos:**  
  
     La consulta de esta sección se ha creado a partir de la base de datos de AdventureWorks, que puede descargar en  [aquí](https://msftdbprodsamples.codeplex.com/releases/view/125550)con el nombre Adventure Works 2014 Full Database Backup.zip.  
  
     Para obtener más información sobre cómo instalar la base de datos, consulte [How to install Adventure Works 2014 Sample Databases.pdf](https://msftdbprodsamples.codeplex.com/releases/view/125550)(Instalación de las bases de datos de ejemplo de AdventureWorks 2014).  
  
2.  **Crear un origen de datos:**  
  
    1.  En el panel **Datos de informe** , haga clic con el botón derecho **Orígenes de datos** y, después, haga clic en **Agregar origen de datos**.  
  
    2.  Seleccione **Usar una conexión incrustada en el informe**.  
  
    3.  Seleccione **Microsoft SQL Server**como el tipo de conexión.  
  
    4.  Escriba la cadena de conexión a su servidor y base de datos; por ejemplo, la siguiente:  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2014  
        ```  
  
    5.  Se recomienda verificarla con el botón **Probar conexión** . Después, haga clic en **Aceptar**.  
  
     Para obtener más información sobre la creación de un origen de datos, vea [Agregar y comprobar una conexión de datos o un origen de datos &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **Crear un conjunto de datos:**  
  
    -   En el panel **Datos de informe** , haga clic con el botón derecho en **Conjuntos de datos** y haga clic en **Agregar conjunto de datos**.  
  
    -   Seleccione **Usar un conjunto de datos insertado en el informe**.  
  
    -   Seleccione el origen de datos que creó en los pasos anteriores.  
  
    -   Seleccione **Texto** como el tipo de consulta y copie y pegue la siguiente consulta en el cuadro de texto **Consulta** :  
  
        ```  
        SELECT    Sales.SalesOrderHeader.SalesOrderID, Sales.SalesOrderHeader.OrderDate, Sales.SalesOrderDetail.SalesOrderDetailID, Sales.SalesOrderDetail.ProductID, Sales.SalesOrderDetail.LineTotal,   
                                 Sales.SalesOrderDetail.UnitPrice, Sales.SalesOrderDetail.OrderQty, Production.Product.Name, Production.Product.ProductNumber, Sales.SalesTerritory.TerritoryID, lower(Sales.SalesTerritory.Name) AS TerritoryName,   
                                 Production.ProductSubcategory.Name AS SubcategoryName, Production.ProductCategory.Name AS CategoryName, Sales.SalesReason.SalesReasonID, Sales.SalesReason.Name AS SalesReasonName  
        FROM            Sales.SalesOrderDetail INNER JOIN  
                                 Sales.SalesOrderHeader ON Sales.SalesOrderDetail.SalesOrderID = Sales.SalesOrderHeader.SalesOrderID INNER JOIN  
                                 Production.Product ON Sales.SalesOrderDetail.ProductID = Production.Product.ProductID INNER JOIN  
                                 Sales.SalesTerritory ON Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID AND   
                                 Sales.SalesOrderHeader.TerritoryID = Sales.SalesTerritory.TerritoryID INNER JOIN  
                                 Production.ProductSubcategory ON Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID AND   
                                 Production.Product.ProductSubcategoryID = Production.ProductSubcategory.ProductSubcategoryID INNER JOIN  
                                 Production.ProductCategory ON Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID AND   
                                 Production.ProductSubcategory.ProductCategoryID = Production.ProductCategory.ProductCategoryID INNER JOIN  
                                 Sales.SalesOrderHeaderSalesReason ON Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID AND   
                                 Sales.SalesOrderHeader.SalesOrderID = Sales.SalesOrderHeaderSalesReason.SalesOrderID INNER JOIN  
                                 Sales.SalesReason ON Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID AND   
                                 Sales.SalesOrderHeaderSalesReason.SalesReasonID = Sales.SalesReason.SalesReasonID  
        ```  
  
    -   Haga clic en **Aceptar**.  
  
     Para obtener más información sobre la creación de un conjunto de datos, vea [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>Vea también  
 [Vista de diseño de conjunto de datos compartidos &#40;Generador de informes&#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
 [Mostrar la información sobre herramientas en una serie &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)   
 [Tutorial: Gráficos de rectángulos en Power BI](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)   
 [Gráfico de rectángulos: Aplicaciones de visualización de datos de investigaciones de Microsoft para Office](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
  
  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]


