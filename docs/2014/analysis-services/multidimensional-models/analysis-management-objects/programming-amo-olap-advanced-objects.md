---
title: Objetos avanzados OLAP en AMO programación | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- programming [AMO]
- Analysis Management Objects, OLAP
- OLAP [AMO]
- AMO, OLAP
ms.assetid: b75f35a7-32df-4f22-983d-324aa98e15a9
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6408cfd8dd3a7b8f7d6993ca84c3325bedddee24
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107322"
---
# <a name="programming-amo-olap-advanced-objects"></a>Programar objetos avanzados OLAP en AMO
  En este tema se explican los detalles de la programación de objetos avanzados OLAP en Objetos de administración de análisis (AMO). Este tema contiene las siguientes secciones:  
  
-   [Objetos Action](#Action)  
  
-   [Objetos KPI](#KPI)  
  
-   [Objetos de perspectiva](#Persp)  
  
-   [Objetos ProactiveCaching](#PC)  
  
-   [Objetos Translation](#Transl)  
  
##  <a name="Action"></a> Objetos Action  
 Las clases Action se utilizan para crear una respuesta activa al examinar ciertas áreas del cubo. Los objetos Action pueden definirse mediante AMO, pero se utilizan desde la aplicación cliente que examina los datos. Las acciones pueden ser de distintos tipos y se deben crear según su tipo. Las acciones pueden ser:  
  
-   Acciones de obtención de detalles, que devuelven el conjunto de filas que representa los datos subyacentes de las celdas seleccionadas del cubo donde se produce la acción.  
  
-   Acciones de elaboración de informes, que devuelven un informe de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] asociado con la sección seleccionada del cubo donde se produce la acción.  
  
-   Acciones estándar, que devuelven el elemento de acción (URL, HTML, DataSet, RowSet y otros elementos) asociado a la sección seleccionada del cubo donde se produce la acción.  
  
 La creación de un objeto de acción requiere los pasos siguientes:  
  
1.  Crear el objeto de acción derivado y rellenar los atributos básicos.  
  
     Los atributos básicos son el tipo de acción, la sección o el tipo de destino del cubo, el área de destino o específica del cubo donde está disponible la acción, el título y el lugar donde el título es una expresión MDX.  
  
2.  Rellenar los atributos específicos del tipo de acción.  
  
     Los atributos son diferentes para los tres tipos de acciones, vea el ejemplo de código que se muestra a continuación para los parámetros.  
  
3.  Agregar la acción a la colección de cubos y actualizar el cubo. La acción no es un objeto actualizable.  
  
 Para probar la acción se requiere una aplicación de programa diferente. Puede probar su acción en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. En primer lugar, debe instalar [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] ejemplos, vea [procesamiento del objeto de modelo multidimensionales](../processing-a-multidimensional-model-analysis-services.md).  
  
 El código muestra siguiente replica tres acciones diferentes del proyecto de muestra Adventure Works de Analysis Services. Puede diferenciar las acciones porque las que se introducen mediante el ejemplo siguiente empiezan por "My".  
  
```  
static public void CreateActions(Cube cube)  
{  
    #region Adding a drillthrough action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Reseller Details"))  
        cube.Actions.Remove("My Drillthrough Action",true);  
  
    //Create a Drillthrough action  
    DrillThroughAction dtaction = new DrillThroughAction("My Reseller Details", "My Drillthrough Action");  
  
    //Define the Action  
    dtaction.Type = ActionType.DrillThrough;  
    dtaction.TargetType = ActionTargetType.Cells;  
    dtaction.Target = "MeasureGroupMeasures(\"Reseller Sales\")";  
    dtaction.Caption = "My Drillthrough...";  
    dtaction.CaptionIsMdx = false;  
  
    #region create drillthrough action specifics  
    //Adding Drillthrough columns  
    //Adding Measure columns to the drillthrough  
    MeasureGroup mg = cube.MeasureGroups.FindByName("Reseller Sales");  
    MeasureBinding mb1 = new MeasureBinding();  
    mb1.MeasureID = mg.Measures.FindByName( "Reseller Sales Amount").ID;  
    dtaction.Columns.Add(mb1);  
  
    MeasureBinding mb2 = new MeasureBinding();  
    mb2.MeasureID = mg.Measures.FindByName("Reseller Order Quantity").ID;  
    dtaction.Columns.Add(mb2);  
  
    MeasureBinding mb3 = new MeasureBinding();  
    mb3.MeasureID = mg.Measures.FindByName("Reseller Unit Price").ID;  
    dtaction.Columns.Add(mb3);  
  
    //Adding Dimension Columns to the drillthrough  
    CubeAttributeBinding cb1 = new CubeAttributeBinding();  
    cb1.CubeID = cube.ID;  
    cb1.CubeDimensionID = cube.Dimensions.FindByName("Reseller").ID;  
    cb1.AttributeID = "Reseller Name";  
    cb1.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb1);  
  
    CubeAttributeBinding cb2 = new CubeAttributeBinding();  
    cb2.CubeID = cube.ID;  
    cb2.CubeDimensionID = cube.Dimensions.FindByName("Product").ID;  
    cb2.AttributeID = "Product Name";  
    cb2.Type = AttributeBindingType.All;  
    dtaction.Columns.Add(cb2);  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(dtaction);  
    #endregion  
  
    #region Adding a Standard action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My City Map"))  
        cube.Actions.Remove("My Action", true);  
  
    //Create a Drillthrough action  
    StandardAction stdaction = new StandardAction("My City Map", "My Action");  
  
    //Define the Action  
    stdaction.Type = ActionType.Url;  
    stdaction.TargetType = ActionTargetType.AttributeMembers;  
    stdaction.Target = "[Geography].[City]";  
    stdaction.Caption = "\"My View Map for \" + [Geography].[City].CurrentMember.Member_Caption + \"...\"";  
    stdaction.CaptionIsMdx = true;  
  
    #region create standard action specifics  
    stdaction.Expression = "\"http://maps.msn.com/home.aspx?plce1=\" + " +  
        "[Geography].[City].CurrentMember.Name + \",\" + " +  
        "[Geography].[State-Province].CurrentMember.Name + \",\" + " +  
        "[Geography].[Country].CurrentMember.Name + " +  
        "\"&regn1=\" + " +  
        "Case " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Australia] " +  
                "Then \"3\" " +  
            "When [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[Canada] " +  
                "Or [Geography].[Country].CurrentMember Is " +  
                    "[Geography].[Country].&[United States] " +  
                "Then \"0\" " +  
                "Else \"1\" " +  
        "End ";  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(stdaction);  
  
    #endregion  
  
    #region Adding a Reporting action  
    // Verify That action exists and drop it  
    if (cube.Actions.ContainsName("My Sales Reason Comparisons"))  
        cube.Actions.Remove("My Report Action", true);  
  
    //Create a Report action  
    ReportAction rsaction = new ReportAction("My Sales Reason Comparisonsp", "My Report Action");  
  
    //Define the Action  
    rsaction.Type = ActionType.Report;  
    rsaction.TargetType = ActionTargetType.AttributeMembers;  
    rsaction.Target = "[Product].[Category]";  
    rsaction.Caption = "\"My Sales Reason Comparisons for \" + [Product].[Category].CurrentMember.Member_Caption + \"...\"";  
    rsaction.CaptionIsMdx = true;  
  
    #region create Report action specifics  
    rsaction.ReportServer = "MyRSSamplesServer";  
    rsaction.Path = "ReportServer?/AdventureWorks Sample Reports/Sales Reason Comparisons";  
    rsaction.ReportParameters.Add("ProductCategory", "UrlEscapeFragment( [Product].[Category].CurrentMember.UniqueName )");  
    rsaction.ReportFormatParameters.Add("rs:Command", "Render");  
    rsaction.ReportFormatParameters.Add("rs:Renderer", "HTML5");  
    #endregion  
  
    //Add the defined action to the cube  
    cube.Actions.Add(rsaction);  
  
    #endregion  
}  
```  
  
##  <a name="KPI"></a> Objetos KPI  
 Un indicador clave de rendimiento (KPI) es un conjunto de cálculos asociados a un grupo de medida de un cubo que se utilizan para evaluar el resultado de una empresa. Los objetos <xref:Microsoft.AnalysisServices.Kpi> pueden definirse mediante AMO, pero se utilizan desde la aplicación cliente que examina los datos.  
  
 La creación de un objeto <xref:Microsoft.AnalysisServices.Kpi> requiere los pasos siguientes:  
  
1.  Crear el objeto <xref:Microsoft.AnalysisServices.Kpi> y rellenar los atributos básicos.  
  
     A continuación se proporciona una lista de los atributos básicos: Descripción, Carpeta para mostrar, Grupo de medida asociado y Valor. La carpeta para mostrar indica a la aplicación cliente donde debería estar el KPI para que el usuario final pueda encontrarlo. El grupo de medida asociado indica el grupo de medida al que deberían remitirse todos los cálculos MDX. El valor muestra el valor real del indicador de rendimiento como expresión MDX.  
  
2.  Definir los indicadores KPI: Objetivo, Estado y Tendencia.  
  
     Los indicadores son expresiones MDX que se deberían evaluar entre -1 y 1, pero es la aplicación de exploración la que define el intervalo de valores para los indicadores.  
  
3.  Al examinar indicadores KPI en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], los valores menores que -1 se tratan como -1 y los valores mayores que 1 se tratan como 1.  
  
4.  Definir imágenes gráficas.  
  
     Las imágenes gráficas son valores de cadena que se utilizan como referencia en la aplicación cliente para identificar el conjunto correcto de imágenes que se ha de mostrar. La cadena de imagen gráfica define también el comportamiento de la función de visualización. Normalmente el intervalo se divide en un número de estados impar, de bueno a malo, y se asigna una imagen del conjunto a cada estado.  
  
     Si utiliza [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] para examinar los KPI, el intervalo de indicador se divide en tres o cinco estados, dependiendo de los nombres. Además, hay nombres donde se invierte el intervalo; es decir, -1 es "Bueno" y 1 es "Malo". En [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], los tres estados del intervalo son los siguientes:  
  
    -   Malo = De -1 a -0,5  
  
    -   Suficiente = De -0,4999 a 0,4999  
  
    -   Bueno = De 0,50 a 1  
  
     En [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], los cinco estados del intervalo son los siguientes:  
  
    -   Malo = De -1 a -0,75  
  
    -   Riesgo = De -0,7499 a -0,25  
  
    -   Suficiente = De -0,2499 a 0,2499  
  
    -   En progreso = De 0,25 a 0,7499  
  
    -   Bueno = De 0,75 a 1  
  
 En la siguiente tabla se especifica el uso, el nombre y el número de estados asociados a la imagen.  
  
|Uso de la imagen|Nombre de la imagen|Número de estados|  
|-----------------|----------------|----------------------|  
|Estado|Formas|3|  
|Estado|Semáforo|3|  
|Estado|Señales viales|3|  
|Estado|Medidor|3|  
|Estado|Medidor invertido|5|  
|Estado|Termómetro|3|  
|Estado|Cilindro|3|  
|Estado|Caras|3|  
|Estado|Flecha de varianza|3|  
|Tendencia|Flecha estándar|3|  
|Tendencia|Flecha de estado|3|  
|Tendencia|Flecha de estado invertida|5|  
|Tendencia|Caras|3|  
  
1.  Agregar el KPI a la colección de cubos y actualizar el cubo, ya que el KPI no es un objeto actualizable.  
  
 Para probar el KPI se requiere una aplicación de programa diferente. Puede probar el KPI en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
 En el ejemplo de código siguiente se crea una KPI en la carpeta "Financial Perspective/Grow Revenue" para el cubo de Adventure Works incluido en el proyecto de ejemplo Adventure Works de Analysis Services.  
  
```  
static public void CreateKPIs(Cube cube)  
{  
    Kpi kpi = cube.Kpis.Add("My Internet Revenue", "My Internet Revenue");  
    kpi.Description = "(My) Revenue achieved through direct sales via Interner";  
    kpi.DisplayFolder = "\\Financial Perspective\\Grow Revenue";  
    kpi.AssociatedMeasureGroupID = "Internet Sales";  
    kpi.Value = "[Measures].[Internet Sales Amount]";  
    #region Goal  
    kpi.Goal = "Case" +  
               "     When IsEmpty" +  
               "          (" +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          )" +   
               "     Then [Measures].[Internet Sales Amount]" +  
               "     Else 1.10 *" +  
               "          (" +  
               "            [Measures].[Internet Sales Amount]," +  
               "            ParallelPeriod" +  
               "            (" +  
               "              [Date].[Fiscal Time].[Fiscal Year]," +  
               "              1," +  
               "              [Date].[Fiscal Time].CurrentMember" +  
               "            )" +  
               "          ) " +  
               " End";  
    #endregion  
    #region Status  
    kpi.Status = "Case" +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .95 " +  
                 "   Then 1 " +  
                 "   When KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) <  .95 " +  
                 "        And  " +  
                 "        KpiValue( \"Internet Revenue\" ) / KpiGoal ( \"Internet Revenue\" ) >= .85 " +  
                 "   Then 0 " +  
                 "   Else -1 " +  
                 "End";  
    #endregion  
    #region Trend  
    kpi.Trend = "Case " +  
                "    When VBA!Abs " +  
                "         ( " +  
                "           KpiValue( \"Internet Revenue\" ) -  " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           ) / " +  
                "           ( " +  
                "             KpiValue ( \"Internet Revenue\" ), " +  
                "             ParallelPeriod " +  
                "             (  " +  
                "               [Date].[Fiscal Time].[Fiscal Year], " +  
                "               1, " +  
                "               [Date].[Fiscal Time].CurrentMember " +  
                "             ) " +  
                "           )   " +  
                "         ) <=.02  " +  
                "    Then 0 " +  
                "    When KpiValue( \"Internet Revenue\" ) -  " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         ) / " +  
                "         ( " +  
                "           KpiValue ( \"Internet Revenue\" ), " +  
                "           ParallelPeriod " +  
                "           (  " +  
                "             [Date].[Fiscal Time].[Fiscal Year], " +  
                "             1, " +  
                "             [Date].[Fiscal Time].CurrentMember " +  
                "           ) " +  
                "         )  >.02 " +  
                "    Then 1 " +  
                "    Else -1 " +  
                "End";  
    #endregion  
    kpi.TrendGraphic = "Standard Arrow";  
    kpi.StatusGraphic = "Cylinder";  
}.  
```  
  
##  <a name="Persp"></a> Objetos de perspectiva  
 Los objetos <xref:Microsoft.AnalysisServices.Perspective> pueden definirse mediante AMO, pero se utilizan desde la aplicación cliente que examina los datos.  
  
 La creación de un objeto <xref:Microsoft.AnalysisServices.Perspective> requiere los pasos siguientes:  
  
1.  Crear el objeto <xref:Microsoft.AnalysisServices.Perspective> y rellenar los atributos básicos.  
  
     A continuación se proporciona una lista de los atributos básicos: Nombre, Medida predeterminada, Descripción y Anotaciones.  
  
2.  Agregar todos los objetos del cubo primario que deberían estar visibles para el usuario final.  
  
     Agregue dimensiones del cubo (atributos y jerarquías), grupos de medida (medida y grupo de medida), acciones, indicadores KPI y cálculos.  
  
3.  Agregar la perspectiva a la colección de cubos y actualizar el cubo, ya que la perspectiva no es un objeto actualizable.  
  
 Para probar la perspectiva se requiere una aplicación de programa diferente. Puede probar la perspectiva en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
 En el ejemplo de código siguiente se crea una perspectiva denominada "Direct Sales" para el cubo proporcionado.  
  
```  
static public void CreatePerspectives(Cube cube)  
{  
    Perspective perspective = cube.Perspectives.Add("Direct Sales", "Direct Sales");  
    CubeDimension dim1 = cube.Dimensions.GetByName("Date");  
    PerspectiveDimension pdim1 = perspective.Dimensions.Add(dim1.DimensionID);  
    pdim1.Attributes.Add("Date");  
    pdim1.Attributes.Add("Calendar Year");  
    pdim1.Attributes.Add("Fiscal Year");  
    pdim1.Attributes.Add("Calendar Quarter");  
    pdim1.Attributes.Add("Fiscal Quarter");  
    pdim1.Attributes.Add("Calendar Month Number");  
    pdim1.Attributes.Add("Fiscal Month Number");  
    pdim1.Hierarchies.Add("Calendar Time");  
    pdim1.Hierarchies.Add("Fiscal Time");  
  
    CubeDimension dim2 = cube.Dimensions.GetByName("Product");  
    PerspectiveDimension pdim2 = perspective.Dimensions.Add(dim2.DimensionID);  
    pdim2.Attributes.Add("Product Name");  
    pdim2.Attributes.Add("Product Line");  
    pdim2.Attributes.Add("Model Name");  
    pdim2.Attributes.Add("List Price");  
    pdim2.Attributes.Add("Size");  
    pdim2.Attributes.Add("Weight");  
    pdim2.Hierarchies.Add("Product Model Categories");  
    pdim2.Hierarchies.Add("Product Categories");  
  
    PerspectiveMeasureGroup pmg = perspective.MeasureGroups.Add("Internet Sales");  
    pmg.Measures.Add("Internet Sales Amount");  
    pmg.Measures.Add("Internet Order Quantity");  
    pmg.Measures.Add("Internet Unit Price");  
  
    pmg = perspective.MeasureGroups.Add("Reseller Sales");  
    pmg.Measures.Add("Reseler Sales Amount");  
    pmg.Measures.Add("Reseller Order Quantity");  
    pmg.Measures.Add("Reseller Unit Price");  
  
    PerspectiveAction pact = perspective.Actions.Add("Drillthrough Action");  
  
    PerspectiveKpi pkpi = perspective.Kpis.Add("Internet Revenue");  
    Cube.Update();  
}  
```  
  
##  <a name="PC"></a> Objetos ProactiveCaching  
 Los objetos <xref:Microsoft.AnalysisServices.ProactiveCaching> pueden definirse mediante AMO.  
  
 La creación de un objeto <xref:Microsoft.AnalysisServices.ProactiveCaching> requiere los pasos siguientes:  
  
1.  Crear el objeto <xref:Microsoft.AnalysisServices.ProactiveCaching>.  
  
     No hay ningún atributo básico que definir.  
  
2.  Agregar especificaciones de caché.  
  
|Especificación|Descripción|  
|-------------------|-----------------|  
|AggregationStorage|Tipo de almacenamiento para las agregaciones.<br /><br /> Solo se aplica a la partición. Su dimensión debe ser `Regular.`.|  
|SilenceInterval|Cantidad mínima de tiempo que existe la memoria caché antes de iniciar la creación de imágenes MOLAP.|  
|Latencia|Cantidad de tiempo entre la notificación más antigua y el momento en el que se destruyen las imágenes MOLAP.|  
|SilenceOverrideInterval|Tiempo transcurrido después de una notificación inicial tras el cual se inicia incondicionalmente la creación de imágenes MOLAP.|  
|ForceRebuildInterval|Tiempo (a partir del momento en que se quita una nueva imagen MOLAP) tras el cual se inicia incondicionalmente (sin notificaciones) la creación de imágenes MOLAP.|  
|OnlineMode|Cuando la imagen MOLAP está disponible.<br /><br /> Puede ser `Immediate` u `OnCacheComplete`.|  
  
1.  Agregar el objeto <xref:Microsoft.AnalysisServices.ProactiveCaching> a la colección principal. Deberá actualizar el elemento primario, ya que <xref:Microsoft.AnalysisServices.ProactiveCaching> no es un objeto actualizable.  
  
 En el ejemplo de código siguiente se crea un objeto <xref:Microsoft.AnalysisServices.ProactiveCaching> en todas las particiones del grupo de medida Internet Sales en el cubo Adventure Works de una base de datos especificada.  
  
```  
static public void SetProactiveCachingSettings(Database db)  
{  
    ProactiveCaching pc;  
    if (db.Cubes.ContainsName("Adventure Works") && db.Cubes.FindByName("Adventure Works").MeasureGroups.ContainsName("Internet Sales"))  
    {  
        ProactiveCachingTablesBinding pctb;  
        TableNotification tn;  
  
        MeasureGroup mg = db.Cubes.FindByName("Adventure Works").MeasureGroups.FindByName("Internet Sales");  
        foreach(Partition part in mg.Partitions)  
        {  
            pc = new ProactiveCaching();  
            pc.AggregationStorage = ProactiveCachingAggregationStorage.MolapOnly;  
            pc.SilenceInterval = TimeSpan.FromSeconds(10);  
            pc.Latency = TimeSpan.FromSeconds(-1);  
            pc.SilenceOverrideInterval = TimeSpan.FromMinutes(10);  
            pc.ForceRebuildInterval = TimeSpan.FromSeconds(-1);  
            pc.Enabled = true;  
            pc.OnlineMode = ProactiveCachingOnlineMode.OnCacheComplete;  
            pctb = new ProactiveCachingTablesBinding();  
            pctb.NotificationTechnique = NotificationTechnique.Server;  
            tn = new TableNotification("[FactInternetSales]", "dbo");  
            pctb.TableNotifications.Add( tn);  
            pc.Source = pctb;  
  
            part.ProactiveCaching = pc;  
            part.Update();  
        }  
    }  
}  
```  
  
##  <a name="Transl"></a> Objetos Translation  
 Los objetos Translation pueden definirse mediante AMO, pero se utilizan desde la aplicación cliente que examina los datos. Los objetos Translation son objetos simples para codificar. Las traducciones de los títulos de objeto se proporcionan mediante pares de Identificador de configuración regional y Título traducido. Pueden habilitarse varias traducciones para cada título. Se pueden proporcionar traducciones para la mayoría de los objetos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], como dimensiones, atributos, jerarquías, cubos, grupos de medida, medidas, etc.  
  
 En el ejemplo de código siguiente se proporciona una traducción al español para el nombre del atributo Product Name.  
  
```  
static public void CreateTranslations(Database db)  
{  
    //Spanish Tranlations for Product Category in Product Dimension  
    Dimension dim = db.Dimensions["Product"];  
    DimensionAttribute atr = dim.Attributes["Product Name"];  
    Translation tran = atr.Translations.Add(3082);  
    tran.Caption = "Nombre Producto";  
  
    dim.Update(UpdateOptions.ExpandFull);  
  
}  
```  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices>   
 [Introducción a las clases AMO](amo-classes-introduction.md)   
 [Clases de OLAP en AMO](amo-olap-classes.md)   
 [Arquitectura lógica &#40;Analysis Services - datos multidimensionales&#41;](../olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de base de datos &#40;Analysis Services - datos multidimensionales&#41;](../olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [Procesamiento de objetos de modelo multidimensional](../processing-a-multidimensional-model-analysis-services.md)  
  
  