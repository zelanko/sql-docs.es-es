---
title: Programar objetos básicos OLAP en AMO | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: be1452c21d75f90210ddcaea6f1bea31e899e26b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="programming-amo-olap-basic-objects"></a>Programar objetos básicos OLAP en AMO
  La creación de objetos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] es un proceso sencillo y directo, pero requiere prestar atención a los detalles. En este tema se explican los detalles de la programación de objetos básicos OLAP. Este tema contiene las siguientes secciones:  
  
-   [Objetos de dimensión](#Dim)  
  
-   [Objetos de cubo](#Cub)  
  
-   [Objetos MeasureGroup](#MG)  
  
-   [Objetos de partición](#Part)  
  
-   [Objetos Aggregation](#AD)  
  
##  <a name="Dim"></a> Objetos de dimensión  
 Para administrar o procesar una dimensión, debe programar el objeto <xref:Microsoft.AnalysisServices.Dimension>.  
  
### <a name="creating-dropping-and-finding-a-dimension"></a>Crear, quitar y buscar un objeto Dimension  
 La creación de un objeto <xref:Microsoft.AnalysisServices.Dimension> se realiza en cuatro pasos:  
  
1.  Crear el objeto de dimensión y rellenar los atributos básicos.  
  
     Los atributos básicos son el nombre, el tipo de dimensión, el modo de almacenamiento, el enlace de origen de datos, el nombre del miembro All del atributo y otros atributos de dimensión.  
  
     Antes de crear una dimensión, debe comprobar que no existe aún. Si la dimensión ya existe, se quita y se vuelve a crear.  
  
2.  Crear los atributos que definen la dimensión.  
  
     Cada atributo debe agregarse individualmente al esquema antes de utilizarlo (busque el método CreateDataItem al final del código de ejemplo) y, a continuación, se puede agregar a la colección de atributos de la dimensión.  
  
     La columna de clave y de nombre debe definirse en todos los atributos.  
  
     El atributo clave principal de la dimensión debe definirse como AttributeUsage.Key para que quede claro que este atributo es el acceso clave a la dimensión.  
  
3.  Crear las jerarquías a las que el usuario tendrá acceso para navegar por la dimensión.  
  
     Al crear jerarquías, el orden de los niveles se define mediante su orden de creación de arriba a abajo. El nivel superior es el primero que se agrega a la colección de niveles de la jerarquía.  
  
4.  Actualizar el servidor con el método Update de la dimensión actual.  
  
 El código de ejemplo siguiente crea la dimensión Product de la tabla de productos de Adventure Works en la base de datos de ejemplo.  
  
```  
static void CreateProductDimension(Database db, string datasourceName)  
{  
    // Create the Product dimension  
    Dimension dim = db.Dimensions.FindByName("Product");  
    if ( dim != null)  
       dim.Drop();  
    dim = db.Dimensions.Add("Product");  
    dim.Type = DimensionType.Products;  
    dim.UnknownMember = UnknownMemberBehavior.Hidden;  
    dim.AttributeAllMemberName = "All Products";  
    dim.Source = new DataSourceViewBinding(datasourceName);  
    dim.StorageMode = DimensionStorageMode.Molap;  
  
    #region Create attributes  
  
    DimensionAttribute attr;  
  
    attr = dim.Attributes.Add("Product Name");  
    attr.Usage = AttributeUsage.Key;  
    attr.Type = AttributeType.Product;  
    attr.OrderBy = OrderBy.Name;  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "EnglishProductName");  
  
    attr = dim.Attributes.Add("Product Line");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLine"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProduct", "ProductLineName");  
  
    attr = dim.Attributes.Add("Model Name");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ModelName"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Product Line"));  
    attr.AttributeRelationships.Add(new AttributeRelationship("Subcategory"));  
  
    attr = dim.Attributes.Add("Subcategory");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "ProductSubcategoryKey"));  
    attr.KeyColumns[0].NullProcessing = NullProcessing.UnknownMember;  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductSubcategory", "EnglishProductSubcategoryName");  
    attr.AttributeRelationships.Add(new AttributeRelationship("Category"));  
  
    attr = dim.Attributes.Add("Category");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "ProductCategoryKey"));  
    attr.NameColumn = CreateDataItem(db.DataSourceViews[0], "DimProductCategory", "EnglishProductCategoryName");  
  
    attr = dim.Attributes.Add("List Price");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "ListPrice"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Size");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Size"));  
    attr.AttributeHierarchyEnabled = false;  
  
    attr = dim.Attributes.Add("Weight");  
    attr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "DimProduct", "Weight"));  
    attr.AttributeHierarchyEnabled = false;  
  
    #endregion  
  
    #region Create hierarchies  
  
    Hierarchy hier;  
  
    hier = dim.Hierarchies.Add("Product Model Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    hier = dim.Hierarchies.Add("Product Categories");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Category").SourceAttributeID = "Category";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Subcategory";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Product Name";  
  
    hier = dim.Hierarchies.Add("Product Model Lines");  
    hier.AllMemberName = "All Products";  
    hier.Levels.Add("Subcategory").SourceAttributeID = "Product Line";  
    hier.Levels.Add("Model Name").SourceAttributeID = "Model Name";  
  
    #endregion  
  
    dim.Update();  
}  
  
static DataItem CreateDataItem(DataSourceView dsv, string tableName, string columnName)  
{  
    DataTable dataTable = ((DataSourceView)dsv).Schema.Tables[tableName];  
    DataColumn dataColumn = dataTable.Columns[columnName];  
    return new DataItem(tableName, columnName,  
        OleDbTypeConverter.GetRestrictedOleDbType(dataColumn.DataType));  
}  
  
```  
  
### <a name="processing-a-dimension"></a>Procesar una dimensión  
 Procesar una dimensión es tan simple como utilizar el método Process del objeto <xref:Microsoft.AnalysisServices.Dimension>.  
  
 El procesamiento de una dimensión puede afectar a todos los cubos que la utilizan. Para obtener más información acerca de las opciones de procesamiento, vea [procesar un modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 El código siguiente realiza una actualización incremental en todas las dimensiones de una base de datos proporcionada:  
  
```  
static void UpdateAllDimensions(Database db)  
{  
    foreach (Dimension dim in db.Dimensions)  
        dim.Process(ProcessType.ProcessUpdate);  
}  
```  
  
##  <a name="Cub"></a> Objetos de cubo  
 Para administrar o procesar un cubo, debe programar el objeto <xref:Microsoft.AnalysisServices.Cube>.  
  
### <a name="creating-dropping-and-finding-a-cube"></a>Crear, quitar y buscar un objeto Cube  
 La administración de los cubos es similar a la de las dimensiones. La creación de un objeto <xref:Microsoft.AnalysisServices.Cube> se realiza en cuatro pasos:  
  
1.  Crear el objeto de cubo y rellenar los atributos básicos.  
  
     Los atributos básicos son el nombre, el modo de almacenamiento, el enlace de origen de datos, la medida predeterminada y otros atributos de cubo.  
  
     Antes de crear un cubo, debe comprobar que éste no existe. En el ejemplo, si el cubo ya existe, se quita y se vuelve a crear.  
  
2.  Agregar las dimensiones del cubo.  
  
     Las dimensiones se agregan a la colección de dimensiones de cubo actual de la base de datos; las dimensiones del cubo son referencias a la colección de dimensiones de la base de datos. Cada dimensión debe asignarse al cubo individualmente. En el ejemplo, para asignar las dimensiones se proporciona: el identificador interno de la dimensión de la base de datos, un nombre para la dimensión en el cubo y un id. para la dimensión con nombre en el cubo.  
  
     En el código de ejemplo, observe que la dimensión "Date" se agrega tres veces, cada una de ellas con un nombre de dimensión de cubo distinto: Fecha, fecha de envío, fecha de entrega. Estas dimensiones se denominan dimensiones "realizadoras de roles". La dimensión base es la misma (Date), pero en la tabla de hechos la dimensión se utiliza con distintos "roles" (Order Date, Ship Date, Delivery Date). Vea "Crear, quitar y buscar un objeto MeasureGroup" más adelante en este documento para entender cómo se definen las dimensiones "realizadoras de roles".  
  
3.  Crear los grupos de medida a los que el usuario tendrá acceso para explorar los datos del cubo.  
  
     La creación de grupos de medida se explicará en "Crear, quitar y buscar un objeto MeasureGroup" más adelante en este documento. El ejemplo incluye la creación de grupos de medida en métodos diferentes, uno para cada grupo de medida.  
  
4.  Actualizar el servidor con el método Update del cubo actual.  
  
     El método Update se utiliza con la opción de actualización ExpandFull para asegurarse de que todos los objetos se actualizan por completo en el servidor.  
  
 El ejemplo de código siguiente crea los componentes del cubo Adventure Works. El ejemplo de código no crea todas las dimensiones o grupos de medida que se incluyen en el proyecto de ejemplo Adventure Works de Analysis Services.  
  
```  
static void CreateAdventureWorksCube(Database db, string datasourceName)  
{  
    // Create the Adventure Works cube  
    Cube cube = db.Cubes.FindByName("Adventure Works");  
    if ( cube != null)  
       cube.Drop();  
    db.Cubes.Add("Adventure Works");  
    cube.DefaultMeasure = "[Reseller Sales Amount]";  
    cube.Source = new DataSourceViewBinding(datasourceName);  
    cube.StorageMode = StorageMode.Molap;  
  
    #region Create cube dimensions  
  
    Dimension dim;  
  
    dim = db.Dimensions.GetByName("Date");  
    cube.Dimensions.Add(dim.ID, "Date", "Order Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Ship Date",  
        "Ship Date Key - Dim Time");  
    cube.Dimensions.Add(dim.ID, "Delivery Date",  
        "Delivery Date Key - Dim Time");  
  
    dim = db.Dimensions.GetByName("Customer");  
    cube.Dimensions.Add(dim.ID);  
  
    dim = db.Dimensions.GetByName("Reseller");  
    cube.Dimensions.Add(dim.ID);  
    #endregion  
  
    #region Create measure groups  
  
    CreateSalesReasonsMeasureGroup(cube);  
    CreateInternetSalesMeasureGroup(cube);  
    CreateResellerSalesMeasureGroup(cube);  
    CreateCustomersMeasureGroup(cube);  
    CreateCurrencyRatesMeasureGroup(cube);  
  
    #endregion  
  
    cube.Update(UpdateOptions.ExpandFull);  
}  
```  
  
### <a name="processing-a-cube"></a>Procesar un cubo  
 Procesar un cubo es tan simple como utilizar el método Process del objeto <xref:Microsoft.AnalysisServices.Cube>. Al procesar un cubo, también se procesan todos los grupos de medida incluidos en éste y todas las particiones del grupo de medida. En un cubo, las particiones son los únicos objetos que se pueden procesar; para fines de procesamiento, los grupos de medida solamente son contenedores de particiones. El tipo de procesamiento especificado para el cubo se propaga a las particiones. El procesamiento interno de cada cubo y grupo de medida se resuelve en el procesamiento de dimensiones y particiones.  
  
 Para obtener más información acerca de las opciones de procesamiento, vea [Processing Objects &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md), y [procesar un modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 El código siguiente realizará un procesamiento completo de todos los cubos de una base de datos especificada:  
  
```  
foreach (Cube cube in db.Cubes)  
             cube.Process(ProcessType.ProcessFull);  
     }  
```  
  
##  <a name="MG"></a> Objetos MeasureGroup  
 Para administrar o procesar un grupo de medida, debe programar el objeto <xref:Microsoft.AnalysisServices.MeasureGroup>.  
  
### <a name="creating-dropping-and-finding-a-measuregroup"></a>Crear, quitar y buscar un objeto MeasureGroup  
 La administración de los grupos de medida es similar a la administración de las dimensiones y los cubos. La creación de un objeto <xref:Microsoft.AnalysisServices.MeasureGroup> se realiza en los siguientes pasos:  
  
1.  Crear el objeto de grupo de medida y rellenar los atributos básicos.  
  
     Entre los atributos básicos se incluyen el nombre, el modo de almacenamiento, el modo de procesamiento, la medida predeterminada y otros atributos de grupo de medida.  
  
     Antes de crear un grupo de medida, compruebe que éste no existe. En el ejemplo de código siguiente, si el grupo de medida existe, se quita y se vuelve a crear.  
  
2.  Crear las medidas del grupo de medida. Para cada medida creada se asignan los siguientes atributos: nombre, función de agregación, columna de origen, cadena de formato. También se pueden asignar otros atributos. Observe que en el código de ejemplo que se muestra a continuación, el método CreateDataItem agrega la columna al esquema.  
  
3.  Agregar las dimensiones del grupo de medida.  
  
4.  Las dimensiones se agregan a la colección de dimensiones del grupo de medida actual desde la colección de dimensiones del cubo primario. Tan pronto como se incluya la dimensión en la colección de dimensiones del grupo de medida, puede asignarse una columna de clave de la tabla de hechos a la dimensión para que el grupo de medida se pueda explorar a través de la dimensión.  
  
     En el código de ejemplo que se muestra a continuación, vea las líneas que aparecen bajo "Mapping dimension and key column from fact table". La dimensiones realizadoras de roles se implementan al vincular distintas claves suplentes a la misma dimensión con nombres diferentes. Cada una de las dimensiones realizadoras de roles (Date, Ship Date, Delivery Date) se vincula a una clave suplente distinta (OrderDateKey, ShipDateKey, DueDateKey). Todas las claves pertenecen a la tabla de hechos FactInternetSales.  
  
5.  Agregar las particiones diseñadas del grupo de medida.  
  
     En el código de ejemplo que se muestra a continuación, la creación de la partición se ajusta en un método.  
  
6.  Actualizar el servidor con el método Update del grupo de medida actual.  
  
     En el código de ejemplo que se muestra a continuación, todos los grupos de medida se actualizan al actualizar el cubo.  
  
 El código muestra siguiente creará el grupo de medida InternetSales del proyecto de ejemplo Adventure Works de Analysis Services.  
  
```  
static void CreateInternetSalesMeasureGroup(Cube cube)  
{  
    // Create the Internet Sales measure group  
    Database db = cube.Parent;  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Internet Sales");  
    if ( mg != null)  
       mg.Drop();  
    mg = cube.MeasureGroups.Add("Internet Sales");  
    mg.StorageMode = StorageMode.Molap;  
    mg.ProcessingMode = ProcessingMode.LazyAggregations;  
    mg.Type = MeasureGroupType.Sales;  
  
    #region Create measures  
  
    Measure meas;  
  
    meas = mg.Measures.Add("Internet Sales Amount");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesAmount");  
  
    meas = mg.Measures.Add("Internet Order Quantity");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderQuantity");  
  
    meas = mg.Measures.Add("Internet Unit Price");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    meas.FormatString = "Currency";  
    meas.Visible = false;  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "UnitPrice");  
  
    meas = mg.Measures.Add("Internet Total Product Cost");  
    meas.AggregateFunction = AggregationFunction.Sum;  
    //meas.MeasureExpression = "[Internet Total Product Cost] * [Average Rate]";  
    meas.FormatString = "Currency";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "TotalProductCost");  
  
    meas = mg.Measures.Add("Internet Order Count");  
    meas.AggregateFunction = AggregationFunction.Count;  
    meas.FormatString = "#,#";  
    meas.Source = CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey");  
  
    #endregion  
  
    #region Create measure group dimensions  
  
    CubeDimension cubeDim;  
    RegularMeasureGroupDimension regMgDim;  
    ManyToManyMeasureGroupDimension mmMgDim;  
    MeasureGroupAttribute mgAttr;  
  
    //   Mapping dimension and key column from fact table  
    //      > select dimension and add it to the measure group  
    cubeDim = cube.Dimensions.GetByName("Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
  
    //      > add key column from dimension and map it with   
    //        the surrogate key in the fact table  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);   // this is dimension key column  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "OrderDateKey"));   // this surrogate key in fact table  
  
    cubeDim = cube.Dimensions.GetByName("Ship Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ShipDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Delivery Date");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Date").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "DueDateKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Customer");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Full Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CustomerKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Product");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Product Name").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "ProductKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Source Currency");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Currency").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "CurrencyKey"));  
  
    cubeDim = cube.Dimensions.GetByName("Sales Reason");  
    mmMgDim = new ManyToManyMeasureGroupDimension();  
    mmMgDim.CubeDimensionID = cubeDim.ID;  
    mmMgDim.MeasureGroupID = cube.MeasureGroups.GetByName("Sales Reasons").ID;  
    mg.Dimensions.Add(mmMgDim);  
  
    cubeDim = cube.Dimensions.GetByName("Internet Sales Order Details");  
    regMgDim = new RegularMeasureGroupDimension(cubeDim.ID);  
    mg.Dimensions.Add(regMgDim);  
    mgAttr = regMgDim.Attributes.Add(cubeDim.Dimension.Attributes.GetByName("Sales Order Key").ID);  
    mgAttr.Type = MeasureGroupAttributeType.Granularity;  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderNumber"));  
    mgAttr.KeyColumns.Add(CreateDataItem(db.DataSourceViews[0], "FactInternetSales", "SalesOrderLineNumber"));  
  
    #endregion  
  
    #region Create partitions  
  
    CreateInternetSalesMeasureGroupPartitions( mg)  
  
    #endregion  
}  
```  
  
### <a name="processing-a-measure-group"></a>Procesar un grupo de medida  
 Procesar un grupo de medida es tan simple como utilizar el método Process del objeto <xref:Microsoft.AnalysisServices.MeasureGroup>. Al procesar un grupo de medida, se procesarán todas las particiones que pertenecen a dicho grupo. El procesamiento interno de un grupo de medida se resuelve en el procesamiento de dimensiones y particiones. Vea la sección [Procesar una partición](#ProcPart) de este documento.  
  
 Para obtener más información acerca de las opciones de procesamiento, vea [Processing Objects &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md), y [procesar un modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 El código siguiente realizará un procesamiento completo en todos los grupos de medida de un cubo proporcionado.  
  
```  
static void FullProcessAllMeasureGroups(Cube cube)  
{  
    foreach (MeasureGroup mg in cube.MeasureGroups)  
        mg.Process(ProcessType.ProcessFull);  
}  
```  
  
##  <a name="Part"></a> Objetos de partición  
 Para administrar o procesar una partición, debe programar un objeto <xref:Microsoft.AnalysisServices.Partition>.  
  
### <a name="creating-dropping-and-finding-a-partition"></a>Crear, quitar y buscar un objeto Partition  
 Las particiones son objetos simples que se pueden crear en dos pasos.  
  
1.  Crear el objeto de partición y rellenar los atributos básicos.  
  
     Los atributos básicos son el nombre, el modo de almacenamiento, el origen de la partición, el segmento y otros atributos de grupo de medida. El origen de la partición define la instrucción SELECT de SQL para la partición actual. "Segmento" es una expresión MDX que especifica una tupla o un conjunto que delimita una parte de las dimensiones del grupo de medida primario que se incluye en la partición actual. Para las particiones MOLAP, la segmentación se determina automáticamente cada vez que se procesa la partición.  
  
     Antes de crear una partición, debe comprobar que ésta no existe. En el ejemplo de código siguiente, si la partición existe, se quita y se vuelve a crear.  
  
2.  Actualizar el servidor con el método Update de la partición actual.  
  
     En el código de ejemplo que se muestra a continuación, todas las particiones se actualizan al actualizar el cubo.  
  
 El ejemplo de código siguiente crea particiones para el grupo de medida "'InternetSales".  
  
```  
static void CreateInternetSalesMeasureGroupPartitions(MeasureGroup mg)  
{  
    Partition part;  
    part = mg.Partitions.FindByName("Internet_Sales_184");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_184");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey <= '184'");  
    part.Slice = "[Date].[Calendar Year].&[2001]";  
    part.Annotations.Add("LastOrderDateKey", "184");  
  
    part = mg.Partitions.FindByName("Internet_Sales_549");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_549");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '184' AND OrderDateKey <= '549'");  
    part.Slice = "[Date].[Calendar Year].&[2002]";  
    part.Annotations.Add("LastOrderDateKey", "549");  
  
    part = mg.Partitions.FindByName("Internet_Sales_914");  
    if ( part != null)  
       part.Drop();  
    part = mg.Partitions.Add("Internet_Sales_914");  
    part.StorageMode = StorageMode.Molap;  
    part.Source = new QueryBinding(db.DataSources[0].ID, "SELECT * FROM [dbo].[FactInternetSales] WHERE OrderDateKey > '549' AND OrderDateKey <= '914'");  
    part.Slice = "[Date].[Calendar Year].&[2003]";  
    part.Annotations.Add("LastOrderDateKey", "914");  
}  
```  
  
###  <a name="ProcPart"></a> Procesar una partición  
 Procesar una partición es tan simple como utilizar el método Process del objeto <xref:Microsoft.AnalysisServices.Partition>.  
  
 Para obtener más información acerca de las opciones de procesamiento, vea [Processing Objects &#40;XMLA&#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/processing-objects-xmla.md) y [procesar un modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 El ejemplo de código siguiente realiza un procesamiento completo de todas las particiones de un grupo de medida especificado.  
  
```  
static void FullProcessAllPartitions(MeasureGroup mg)  
{  
    foreach (Partition part in mg.Partitions)  
        part.Process(ProcessType.ProcessFull);  
}  
```  
  
### <a name="merging-partitions"></a>Mezclar particiones  
 Mezclar particiones significa realizar cualquier operación cuyo resultado sea que dos o más particiones se consoliden en una sola.  
  
 La mezcla de las particiones es un método del objeto <xref:Microsoft.AnalysisServices.Partition>. Esta comando mezcla los datos de una o varias particiones de origen en una partición de destino y elimina las particiones de origen.  
  
 Solamente puede mezclar particiones si todas ellas cumplen los siguientes criterios:  
  
-   Las particiones están en el mismo grupo de medida.  
  
-   Las particiones están almacenadas del mismo modo (MOLAP, HOLAP y ROLAP).  
  
-   Las particiones residen en el mismo servidor; las particiones remotas pueden mezclarse si están en el mismo servidor.  
  
 A diferencia de las versiones anteriores, en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] no es necesario que todas las particiones de origen tengan un diseño de agregaciones idénticos.  
  
 El conjunto de agregaciones resultante para la partición de destino es el mismo conjunto de agregaciones del estado anterior a la ejecución del comando merge.  
  
 El ejemplo de código siguiente mezcla todas las particiones de un grupo de medida especificado. Las particiones se mezclan en la primera partición del grupo de medida.  
  
```  
static void MergeAllPartitions(MeasureGroup mg)  
{  
    if (mg.Partitions.Count > 1)  
    {  
        Partition[] partArray = new Partition[mg.Partitions.Count - 1];  
        for (int i = 1; i < mg.Partitions.Count; i++)  
            partArray[i - 1] = mg.Partitions[i];  
        mg.Partitions[0].Merge(partArray);  
        //To have last changes in the server reflected in AMO  
        mg.Refresh();  
    }  
```  
  
##  <a name="AD"></a> Objetos Aggregation  
 Para diseñar una agregación y aplicarla a una o más particiones, debe programar el objeto <xref:Microsoft.AnalysisServices.Aggregation>.  
  
### <a name="creating-and-dropping-aggregations"></a>Crear y quitar agregaciones  
 Las agregaciones se pueden crear y asignar fácilmente a grupos de medida o particiones mediante el método DesignAggregations del objeto <xref:Microsoft.AnalysisServices.AggregationDesign>. El objeto <xref:Microsoft.AnalysisServices.AggregationDesign> es un objeto independiente de la partición; el objeto <xref:Microsoft.AnalysisServices.AggregationDesign> está incluido en el objeto <xref:Microsoft.AnalysisServices.MeasureGroup>. Las agregaciones pueden diseñarse de acuerdo con un nivel especificado de optimización (de 0 a 100) o con un nivel especificado de almacenamiento (bytes). Varias particiones pueden utilizar el mismo diseño de agregaciones.  
  
 El ejemplo de código siguiente crea agregaciones para todas las particiones de un grupo de medida proporcionado. Las agregaciones existentes en las particiones se quitan.  
  
```  
static public String DesignAggregationsOnPartitions(MeasureGroup mg, double optimizationWanted, double maxStorageBytes)  
{  
    double optimization = 0;  
    double storage = 0;  
    long aggCount = 0;  
    bool finished = false;  
    AggregationDesign ad = null;  
    String aggDesignName;  
    String AggregationsDesigned = "";  
    aggDesignName = mg.AggregationPrefix + "_" + mg.Name;  
    ad = mg.AggregationDesigns.Add();  
    ad.Name = aggDesignName;  
    ad.InitializeDesign();  
    while ((!finished) && (optimization < optimizationWanted) && (storage < maxStorageBytes))  
    {  
        ad.DesignAggregations(out optimization, out storage, out aggCount, out finished);  
    }  
    ad.FinalizeDesign();  
    foreach (Partition part in mg.Partitions)  
    {  
        part.AggregationDesignID = ad.ID;  
        AggregationsDesigned += aggDesignName + " = " + aggCount.ToString() + " aggregations designed\r\n\tOptimization: " + optimization.ToString() + "/" + optimizationWanted.ToString() + "\n\r\tStorage: " + storage.ToString() + "/" + maxStorageBytes.ToString() + " ]\n\r";  
     }  
     return AggregationsDesigned;  
}  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Introducción a las clases AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-classes-introduction.md)   
 [Clases de OLAP en AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)   
 [Arquitectura lógica & #40; Analysis Services - datos multidimensionales & #41;](../../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de base de datos & #40; Analysis Services - datos multidimensionales & #41;](../../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Procesar un modelo multidimensional &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Instalar datos de ejemplo y proyectos para el Tutorial de modelado Multidimensional de Analysis Services](../../../analysis-services/install-sample-data-and-projects.md)  
  
  
