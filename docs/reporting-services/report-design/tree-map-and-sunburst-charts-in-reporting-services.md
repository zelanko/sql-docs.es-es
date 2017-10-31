---
title: "Gráficos de gráfico de rectángulos y proyección solar en SQL Server Reporting Services | Documentos de Microsoft"
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 5e15fa8674a09821becd437e78cfb0bb472e3bc8
ms.openlocfilehash: 50224e926c08951887a6423ab1c95eb7ac23a944
ms.contentlocale: es-es
ms.lasthandoff: 10/30/2017

---
# <a name="treemap-and-sunburst-charts-in-reporting-services"></a>Gráficos de gráfico de rectángulos y proyección solar en Reporting Services
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

El servidor SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] visualizaciones gráfico de rectángulos y proyección solar resultan excepcionales para representar visualmente datos jerárquicos. Este artículo es una visión general de cómo agregar un gráfico de gráfico de rectángulos o de proyección solar a un [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] informes. El artículo también incluye una consulta de ejemplo de AdventureWorks para ayudarle a empezar a trabajar.  
  
##  <a name="bkmk_treemap_chart"></a>Gráfico de gráfico de rectángulos  

Un gráfico de gráfico de rectángulos divide el área del gráfico en los rectángulos que representan los diferentes niveles y tamaños relativos de la jerarquía de datos. La distribución se asemeja a las ramas de un árbol, que parten de un tronco y se dividen en ramas cada vez más pequeñas. Cada rectángulo se divide en rectángulos más pequeños que representan el siguiente nivel en la jerarquía. Los rectángulos de nivel superior del gráfico de rectángulos se ordenan de forma que el rectángulo más grande en la esquina superior izquierda del gráfico para el rectángulo más pequeño en la esquina inferior derecha.  Dentro de cada rectángulo, el siguiente nivel del más alto también se organiza con rectángulos en la misma distribución, de la esquina superior izquierda a la inferior derecha.  

Por ejemplo, en la siguiente imagen de gráfico de rectángulos de ejemplo, el territorio del suroeste es la más grande y Alemania es el más pequeño. En el suroeste de EE. UU., las bicicletas de carretera se han vendido más que las de montaña.  
 
![ssrs_treemap_example](../../reporting-services/report-design/media/ssrs-treemap-example.png "ssrs_treemap_example")  
  
### <a name="to-insert-a-treemap-chart-and-set-up-the-sample-adventureworks-data"></a>Para insertar un gráfico de gráfico de rectángulos y configurar los datos de ejemplo AdventureWorks  
   
> [!NOTE]
> Antes de agregar un gráfico a un informe, cree un origen de datos y un conjunto de datos.  Para datos de ejemplo y una consulta de ejemplo, vea [datos de ejemplo AdventureWorks](#bkmk_sample_data).  
  
1.  Haga clic en la superficie de diseño, a continuación, seleccione **insertar** > **gráfico**. Seleccione el **Treemap** icono.

    ![ssrs_treemap_icon](../../reporting-services/media/ssrs-treemap-icon.png "ssrs_treemap_icon")  
   
2.  Cambie la posición y el tamaño del gráfico. Para usar con los datos de ejemplo, un gráfico de 5 pulgadas de ancho es un buen punto de partida.  
  
3.  Agregue los siguientes campos de los datos de ejemplo:  
  
    * **Valores**: LineTotal
    * **Grupos de categorías** (en el siguiente orden):
        1. nombreDeCategoría
        2. SubcategoryName
    * **Grupos de series**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  Para optimizar el tamaño de página para la forma general de un gráfico de rectángulos, establezca la posición de la leyenda en la parte inferior.  
  
5.  Para agregar información sobre herramientas que muestre la subcategoría y el total de línea, haga clic en **LineTotal**y, a continuación, seleccione **propiedades de la serie**.  
  
     ![ssrs_visualization_seriesproperties](../../reporting-services/report-design/media/ssrs-visualization-seriesproperties.png "ssrs_visualization_seriesproperties")  
  
     Establecer el **información sobre herramientas** valor para la propiedad siguiente:  
  
    ```  
    =Fields!SubcategoryName.Value &": " &Format(Sum(Fields!LineTotal.Value),"C")  
    ```  
  
    Para obtener más información, vea [mostrar información sobre herramientas en una serie &#40; El generador de informes y SSRS &#41; ](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md).  
  
6.  Cambie el título de gráfico predeterminada a **clasifica por categorías de ventas por territorio**.  
  
7.  El número de valores de etiqueta que se muestran viene determinado por el tamaño de la fuente, del área general del gráfico y de los rectángulos específicos. Para ver más etiquetas, cambie la **fuente de etiqueta** propiedad de **LineTotal** a **10 pto** desde el valor predeterminado de **8 pt**.  
  
  
##  <a name="bkmk_sunburst_chart"></a>Gráfico de proyección solar  
 
En un gráfico de proyección solar, la jerarquía se representa mediante una serie de círculos. El nivel más alto de la jerarquía se encuentra en el centro y niveles inferiores de la jerarquía son anillos muestra fuera del centro.  El nivel más bajo de la jerarquía es el anillo exterior.  
  
![ssrs_sunburst_example](../../reporting-services/report-design/media/ssrs-sunburst-example.png "ssrs_sunburst_example")  
  
### <a name="to-insert-a-sunburst-chart-and-set-up-the-sample-adventureworks-data"></a>Para insertar un gráfico de proyección solar y configurar los datos de ejemplo AdventureWorks  
> [!NOTE] 
> Antes de agregar un gráfico a un informe, cree un origen de datos y un conjunto de datos. Para datos de ejemplo y una consulta de ejemplo, vea [datos de ejemplo AdventureWorks](#bkmk_sample_data).  
  
1.  Haga clic en la superficie de diseño y, a continuación, seleccione **insertar** > **gráfico**. Seleccione el **proyección solar** icono.
     
     ![ssrs_sunburst_icon](../../reporting-services/media/ssrs-sunburst-icon.png "ssrs_sunburst_icon")  
  
2.  Cambie la posición y el tamaño del gráfico. Para usar con los datos de ejemplo, un gráfico de 5 pulgadas de ancho es un buen punto de partida.  
  
3.  Agregue los siguientes campos de los datos de ejemplo:  

    * **Valores**: LineTotal
    * **Grupos de categorías** (en el siguiente orden):
        1. nombreDeCategoría
        2. SubcategoryName
        3. SalesReasonName
    * **Grupos de series**: TerritoryName  

    ![ssrs_treemap_example_properties](../../reporting-services/report-design/media/ssrs-treemap-example-properties.png "ssrs_treemap_example_properties")
  
4.  Para optimizar el tamaño de página para la forma general de un gráfico de proyección solar, establezca la posición de la leyenda en la parte inferior.  
  
5.  Cambie el título de gráfico predeterminada a **clasifica por categorías ventas por territorio, con motivo de venta**.  
  
6. Para agregar los valores de los grupos de categorías al gráfico de proyección solar como etiquetas, establecer las propiedades de etiqueta **Visible = true** y **UseValueAsLabel = false**.<br /><br /> Los valores de etiqueta que se muestran vienen determinados por el tamaño de la fuente, del área general del gráfico y de los rectángulos específicos.  Para ver más etiquetas, cambie la **fuente de etiqueta** propiedad de **LineTotal** a **10 pto** desde el valor predeterminado de **8 pt**.

    ![ssrs_sunburst_linetotalproperties](../../reporting-services/report-design/media/ssrs-sunburst-linetotalproperties.png "ssrs_sunburst_linetotalproperties")
  
7.  Si desea utilizar una gama de colores distinta, cambie la propiedad **Paleta** del gráfico.  
    
     ![ssrs_visualization_palette](../../reporting-services/report-design/media/ssrs-visualization-palette.png "ssrs_visualization_palette")  
  
  
##  <a name="bkmk_sample_data"></a>Datos de ejemplo AdventureWorks  
 Esta sección incluye una consulta de ejemplo y los pasos básicos para crear un origen de datos y el conjunto de datos en [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion-md.md)]. Si el informe ya contiene un origen de datos y un conjunto de datos, puede omitir esta sección.  
  
 La consulta devuelve datos de detalle de pedido de ventas de AdventureWorks con territorio de ventas, categoría de producto, subcategoría de producto y datos de la razón de venta.  
  
1.  **Obtener los datos**.  
  
     La consulta en esta sección se basa en la base de datos AdventureWorks, que está disponible para su descarga desde GitHub: [copia de seguridad completa de 2016 de AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases).  
  
  
2.  **Crear un origen de datos**.  
  
    1.  En **datos de informe**, haga clic en **orígenes de datos**y, a continuación, seleccione **agregar origen de datos**.  
  
    2.  Seleccione **Usar una conexión incrustada en el informe**.  
  
    3.  Para el tipo de conexión, seleccione **Microsoft SQL Server**.  
  
    4.  Escriba la cadena de conexión con el servidor y la base de datos. Por ejemplo:  
  
        ```  
        Data Source=[server name];Initial Catalog=AdventureWorks2016  
        ```  
  
    5.  Para comprobar la conexión, seleccione la **Probar conexión** y, a continuación, seleccione **Aceptar**.  
  
     Para obtener más información acerca de cómo crear un origen de datos, vea [agregar y comprobar una conexión de datos &#40; El generador de informes y SSRS &#41; ](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
3.  **Crear un conjunto de datos**.  
  
    1. En **datos de informe**, haga clic en **conjuntos de datos**y, a continuación, seleccione **Agregar conjunto de datos**.  
  
    2. Seleccione **Usar un conjunto de datos insertado en el informe**.  
  
    3. Seleccione el origen de datos que ha creado.  
  
    4. Seleccione el **texto** tipo, de consulta y, a continuación, copie y pegue la siguiente consulta en el **consulta** cuadro de texto:  
  
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
  
    5. Seleccione **Aceptar**.  
  
     Para obtener más información acerca de cómo crear un conjunto de datos, vea [crear un conjunto de datos compartido o conjunto de datos incrustado &#40; El generador de informes y SSRS &#41; ](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>Vea también  
* [Compartir la vista de diseño de conjunto de datos &#40; El generador de informes &#41;](../../reporting-services/report-builder/shared-dataset-design-view-report-builder.md)   
* [Mostrar información sobre herramientas en una serie &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/show-tooltips-on-a-series-report-builder-and-ssrs.md)
* [Tutorial: Gráficos de rectángulos en Power BI](https://support.powerbi.com/knowledgebase/articles/556200-tutorial-treemaps-in-power-bi)
* [Gráfico de rectángulos: Aplicaciones de visualización de datos de investigaciones de Microsoft para Office](http://research.microsoft.com/en-us/projects/msrdatavis/treemap.aspx)  
<br>  
[!INCLUDE[feedback_stackoverflow_msdn_connect_md](../../includes/feedback-stackoverflow-msdn-connect-md.md)]


