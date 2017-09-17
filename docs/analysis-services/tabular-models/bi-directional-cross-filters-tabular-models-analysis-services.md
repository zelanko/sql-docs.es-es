---
title: -Modelos tabulares - Analysis Services los filtros cruzados bidireccionales | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5e810707-f58d-4581-8f99-7371fa75b6ac
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 98a16bacbaf839d65555b1495e7010d98a88e857
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="bi-directional-cross-filters---tabular-models---analysis-services"></a>-Modelos tabulares - Analysis Services los filtros cruzados bidireccionales
  Como novedad en SQL Server 2016 se ha introducido un enfoque integrado para permitir los *filtros cruzados bidireccionales* en los modelos tabulares, lo que elimina la necesidad de usar soluciones DAX manuales para propagar el contexto de filtro en las relaciones entre tablas.  
  
 Si descomponemos el concepto en sus componentes, el *filtrado cruzado* es la capacidad de establecer un contexto de filtro en una tabla en función de los valores de una tabla relacionada, mientras que la transferencia de un contexto de filtro a una segunda tabla relacionada en el otro lado de una relación de tabla es *bidireccional* . Como su nombre indica, es posible realizar la segmentación en ambas direcciones de la relación, en lugar de en una sola.  Internamente, el filtrado bidireccional expande el contexto de filtro para consultar un superconjunto de los datos.  
  
 ![SSAS-BIDI-1-Filteroption](../../analysis-services/tabular-models/media/ssas-bidi-1-filteroption.PNG "SSAS-BIDI-1-Filteroption")  
  
 Hay dos tipos de filtros cruzados: el filtrado unidireccional y el filtrado bidireccional. El filtrado unidireccional es la dirección de filtrado tradicional de varios a uno entre las tablas de hechos y dimensiones de una relación. El filtrado bidireccional es un filtro cruzado que permite usar el contexto de filtro de una relación como contexto de filtro para otra relación de tabla, con una tabla común a ambas relaciones.  
  
 Dados **DimDate** y **DimProduct** con relaciones de clave externa con **FactOnlineSales**, un filtro cruzado bidireccional equivale al uso simultáneo de **FactOnlineSales-to-DimDate** más **FactOnlineSales-to-DimProduct** .  
  
 Los filtros cruzados bidireccionales pueden ser una solución fácil para el problema del diseño de consultas varios a varios que supuso todo un reto en el pasado para los desarrolladores de modelos tabulares y de Power Pivot. Si ha usado la solución DAX para las relaciones varios a varios en modelos tabulares o de Power Pivot, puede intentar aplicar un filtro bidireccional para ver si se generan los resultados previstos.  
  
 Al crear un filtro cruzado bidireccional, debe tener en cuenta los puntos siguientes:  
  
-   Piense antes de habilitar un filtro bidireccional.  
  
     Si habilita filtros bidireccionales en todas partes, los datos podrían filtrarse en exceso de maneras inesperadas.  También podría introducir ambigüedad accidentalmente al crear más de una ruta de consulta posible. Para evitar ambos problemas, intente usar una combinación de filtros unidireccionales y bidireccionales.  
  
-   Realice pruebas incrementales para comprobar cómo afecta cada cambio de filtro en el modelo. [Analizar en Excel](../../analysis-services/tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md) funciona bien en las pruebas incrementales. Se recomienda que realice un seguimiento periódico con pruebas llevadas a cabo mediante otros clientes de informes para asegurarse de que no se produzcan sorpresas.  
  
> [!NOTE]  
>  A partir de CTP 3.2, SSDT incluye un valor predeterminado que determina si se intentan usar automáticamente los filtros cruzados bidireccionales. Si habilita los filtros bidireccionales de forma predeterminada, SSDT habilitará el filtrado bidireccional solo si el modelo articula claramente una ruta de consulta a través de una cadena de relaciones de tabla.  
  
## <a name="set-the-default"></a>Establecer el valor predeterminado  
 Los filtros direccionales únicos son el valor predeterminado. Puede cambiar el valor predeterminado de todos los proyectos nuevos creados en el diseñador o puede hacerlo en el propio modelo cuando el proyecto ya exista.  
  
 En el nivel de proyecto, la configuración se evalúa cuando se crea el proyecto. Por esta razón, si cambia el valor predeterminado a bidireccional, verá los efectos de la selección cuando cree el proyecto siguiente.  
  
1.  En SSDT, seleccione **Herramientas** > **Opciones** > **Diseñadores tabulares de Analysis Services** > **Configuración de nuevo proyecto**.  
  
2.  Establezca **Default filter direction** (Dirección de filtrado predeterminada) en **Single direction** (Dirección única) o **Both directions**(Ambas direcciones).  
  
 También puede cambiar el valor predeterminado en el modelo.  
  
1.  En el Explorador de soluciones, seleccione **Model.bim** > **Propiedades** .  
  
2.  Establezca **Default filter direction** (Dirección de filtrado predeterminada) en **Single direction** (Dirección única) o **Both directions**(Ambas direcciones).  
  
## <a name="walkthrough-an-example"></a>Tutorial de ejemplo  
 La mejor manera de comprender el valor del filtrado cruzado bidireccional es a través de un ejemplo. Considere el siguiente conjunto de datos de [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279), que refleja la cardinalidad y los filtros cruzados que se crean de forma predeterminada.  
  
 ![SSAS-BIDI-2-modelo](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "modelo-SSAS-BIDI-2")  
  
> [!NOTE]  
>  De forma predeterminada, durante la importación de datos, las relaciones de tablas se crean automáticamente en las configuraciones de varios a uno derivadas de las relaciones de clave externa y clave principal entre la tabla de hechos y las tablas de dimensiones relacionadas.  
  
 Observe que la dirección del filtro va de las tablas de dimensiones a la tabla de hechos. Las promociones, los productos, las fechas, el cliente y la geografía del cliente son filtros válidos que producen correctamente la agregación de una medida, con un valor real que varía según las dimensiones usadas.  
  
 ![SSAS-bidi-3-defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "ssas-bidi-3-defaultrelationships")  
  
 En este sencillo esquema de estrella, las pruebas en Excel confirman que los datos se segmentan bien cuando los flujos procedentes de las tablas de dimensiones en filas y columnas se filtran en datos agregados proporcionados por la medida **Sum of Sales** (Suma de ventas) que se encuentra en la tabla central **FactOnlineSales** .  
  
 ![SSAS-bidi-4-excelSumSales](../../analysis-services/tabular-models/media/ssas-bidi-4-excelsumsales.PNG "ssas-bidi-4-excelSumSales")  
  
 Siempre y cuando las medidas se extraigan de la tabla de hechos y el contexto de filtro finalice en la tabla de hechos, las agregaciones se filtrarán correctamente para este modelo. Pero ¿qué ocurre si quiere crear medidas en otra parte, como un recuento distintivo en la tabla de productos o clientes, o un promedio de descuento en la tabla de promociones, y le interesa que el contexto de filtro existente se extienda a esa medida?  
  
 Probemos a agregar un recuento distintivo de **DimProducts** a la tabla dinámica. Observe los valores que se repiten en **Count Products**(Recuento de productos). A primera vista, parece como si faltara alguna relación de tabla, pero en nuestro modelo podemos ver que todas las relaciones están completamente definidas y activas. En este caso, los valores se repiten porque no hay ningún filtro de fecha en las filas de la tabla de productos.  
  
 ![SSAS-bidi-5-prodcount-nofilter](../../analysis-services/tabular-models/media/ssas-bidi-5-prodcount-nofilter.png "ssas-bidi-5-prodcount-nofilter")  
  
 Después de agregar un filtro cruzado bidireccional entre **FactOnlineSales** y **DimProduct**, las filas de la tabla de productos se filtran correctamente por fabricante y fecha.  
  
 ![SSAS-bidi-6-prodcount-withfilter](../../analysis-services/tabular-models/media/ssas-bidi-6-prodcount-withfilter.png "ssas-bidi-6-prodcount-withfilter")  
  
## <a name="learn-step-by-step"></a>Aprendizaje paso a paso  
 Puede probar los filtros cruzados bidireccionales llevando a cabo los pasos de este tutorial. Para poder continuar, necesita:  
  
-   Instancia de SQL Server 2016 Analysis Services, modo tabular y última versión de CTP.  
  
-   [SQL Server Data Tools para Visual Studio 2015 (SSDT)](http://go.microsoft.com/fwlink/p/?LinkID=627574), lanzado a la vez que la última versión de CTP.  
  
-   [ContosoRetailDW](http://www.microsoft.com/en-us/download/details.aspx?id=18279)  
  
-   Permisos de lectura para estos datos.  
  
-   Excel (para su uso con Analizar en Excel)  
  
### <a name="create-a-project"></a>Crear un proyecto  
  
1.  Inicie SQL Server Data Tools para Visual Studio 2015.  
  
2.  Haga clic en **Archivo** > **Nuevo** > **Proyecto** > **Modelo tabular de Analysis Services**.  
  
3.  En el Diseñador de modelos tabulares, establezca la base de datos del área de trabajo en una instancia de SQL Server 2016 Preview Analysis Services en modo de servidor tabular.  
  
4.  Compruebe el nivel de compatibilidad de modelo se establece en **SQL Server 2016 RTM (1200)** o superior.  
  
     Haga clic en **Aceptar** para crear el proyecto.  
  
### <a name="add-data"></a>Agregar datos  
  
1.  Haga clic en **Modelo** > **Importar desde el origen de datos** > **Microsoft SQL Server**.  
  
2.  Especifique el servidor, la base de datos y el método de autenticación.  
  
3.  Elija la base de datos ContosoRetailDW.  
  
4.  Haga clic en **Siguiente**.  
  
5.  En selección de tabla, presione Ctrl y seleccione las tablas siguientes:  
  
    -   FactOnlineSales  
  
    -   DimCustomer  
  
    -   DimDate  
  
    -   DimGeography  
  
    -   DimPromotion  
  
     En este momento puede editar los nombres si quiere que sean más legibles en el modelo.  
  
     ![SSAS-bidi-7-ImportData](../../analysis-services/tabular-models/media/ssas-bidi-7-importdata.PNG "ssas-bidi-7-ImportData")  
  
6.  Importe los datos.  
  
 Si se producen errores, confirme que la cuenta usada para conectarse a la base de datos tiene un inicio de sesión de SQL Server con permisos de lectura en el almacenamiento de datos de Contoso. En una conexión remota, también podría interesarle comprobar la configuración del puerto en el firewall para SQL Server.  
  
### <a name="review-default-table-relationships"></a>Revisar las relaciones de tabla predeterminadas  
 Cambie a la vista de diagrama: **Modelo** > **Vista de modelo** > **Vista de diagrama**. La cardinalidad y las relaciones activas se indican visualmente. Todas las relaciones son relaciones uno a varios entre dos tablas cualesquiera relacionadas.  
  
 ![SSAS-BIDI-2-modelo](../../analysis-services/tabular-models/media/ssas-bidi-2-model.PNG "modelo-SSAS-BIDI-2")  
  
 También puede hacer clic en **Tabla** > **Administrar relaciones** para ver la misma información en un diseño de tabla.  
  
 ![SSAS-bidi-3-defaultrelationships](../../analysis-services/tabular-models/media/ssas-bidi-3-defaultrelationships.PNG "ssas-bidi-3-defaultrelationships")  
  
### <a name="create-measures"></a>Crear medidas  
 Necesitará una agregación para sumar las cantidades de ventas por distintas facetas de datos dimensionales. En **DimProduct,** puede crear una medida que cuente los productos y usarla después en un análisis de comercialización de productos que muestre un recuento de cuántos productos participaron en las ventas de un año determinado, una región determinada o un tipo de cliente.  
  
1.  Haga clic en **Modelo** > **Vista de modelo** > **Vista de diagrama**.  
  
2.  Haga clic en **FactOnlineSales**.  
  
3.  Seleccione la columna **SalesAmount** .  
  
4.  Haga clic en **Columna** > **Autosuma** > **Suma** para crear una medida para las ventas.  
  
5.  Haga clic en **DimProduct**.  
  
6.  Seleccione la columna **ProductKey**.  
  
7.  Haga clic en **Columna** > **Autosuma** > **DistinctCount** para crear una medida para los productos únicos.  
  
### <a name="analyze-in-excel"></a>Analizar en Excel  
  
1.  Haga clic en **Modelo** > **Analizar en Excel** para reunir todos los datos en una tabla dinámica.  
  
2.  Seleccione las dos medidas que acaba de crear en la lista de campos.  
  
3.  Seleccione **Productos** > **Fabricante**.  
  
4.  Seleccione **Fecha** > **Año natural**.  
  
 Observe que las ventas se dividen por año y fabricante, según lo esperado. Esto se debe a que el contexto de filtro predeterminado entre **FactOnlineSales**, **DimProduct**y **DimDate** funciona correctamente para las medidas del lado de "varios" de la relación.  
  
 Al mismo tiempo, puede ver que el recuento de productos no selecciona el mismo contexto de filtro que las ventas. Aunque los recuentos de productos están filtrados correctamente por fabricante (el fabricante y los recuentos de productos están en la misma tabla), el filtro de fecha no se propaga al recuento de productos.  
  
### <a name="change-the-cross-filter"></a>Cambiar el filtro cruzado  
  
1.  De nuevo en el modelo, seleccione **Tabla** > **Administrar relaciones**.  
  
2.  Edite la relación que existe entre **FactOnlineSales** y **DimProduct**.  
  
     Cambie la dirección del filtro en ambas tablas.  
  
3.  Guarde la configuración.  
  
4.  En el libro, haga clic en **Actualizar** para volver a leer el modelo.  
  
 Ahora debería ver que los recuentos de productos y las ventas se filtran según el mismo contexto de filtro, que incluye no solo los fabricantes de **DimProducts** sino el año natural de **DimDate**.  
  
## <a name="conclusion-and-next-steps"></a>Conclusión y pasos siguientes  
 Para entender cómo y cuándo se usa un filtro cruzado bidireccional, puede que tenga que realizar una serie de pruebas para ver cómo funciona en su escenario. En ocasiones, considerará que los comportamientos integrados no son suficientes y tendrá que recurrir a cálculos DAX para realizar el trabajo. En la sección **Vea también** , encontrará varios vínculos a recursos adicionales sobre este tema.  
  
 En la práctica, el filtrado cruzado puede habilitar formas de exploración de datos que normalmente solo se ofrecen a través de una construcción varios a varios. Dicho esto, es importante reconocer que el filtrado cruzado bidireccional no es una construcción varios a varios.  En el diseñador de modelos tabulares de esta versión sigue sin admitirse una configuración real de tabla varios a varios.  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar relaciones en Power BI Desktop](https://support.powerbi.com/knowledgebase/articles/464155-create-and-manage-relationships-in-power-bi-desktop)   
 [Un ejemplo práctico de cómo administrar las relaciones de varios a many simples en los modelos tabulares de Power Pivot y SSAS](http://social.technet.microsoft.com/wiki/contents/articles/22202.a-practical-example-of-how-to-handle-simple-many-to-many-relationships-in-power-pivotssas-tabular-models.aspx)   
 [Resolver las relaciones de varios a varios aprovechando DAX entre tablas filtrado](http://blog.gbrueckl.at/2012/05/resolving-many-to-many-relationships-leveraging-dax-cross-table-filtering/)   
 [Muchos a muchos revolution (SQLBI blog)](http://www.sqlbi.com/articles/many2many/)  
  
  
